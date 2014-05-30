--- 
layout: post 
title: "Controlando la evolución de la base de datos con liquibase y maven" 
published: true 
date: 2009-12-11
categories: [programming]
---

En uno de mis últimos proyectos, se manifestó la necesidad para controlar los cambios en la base de datos. Debe ser que [Refactoring Databases](http://www.amazon.com/Refactoring-Databases-Evolutionary-Database-Design/dp/0321293533) esta haciendo efectos, pero la idea de poder guardar la evolución de los esquemas de base de datos en el control de versiones pareció bastante lógica e interesante, y también bastante práctica, al permitir que nuevos miembros del equipo de desarrollo pudieran replicar fácilmente el esquema en sus máquinas de desarrollo.

Después de analizar varias opciones (guardar los scripts DDL, hacer un volcado de los esquemas sin datos, ...) pareció buena idea usar [liquibase](http://www.liquibase.org/), una libreria que permite describir en un fichero xml la evolución de un esquema de base de datos y replicar dicha evolución en un esquema nuevo, o en uno parcialmente sincronizado con dicha evolución. Para hacer el seguimiento de los cambios ya replicados, *liquibase* crea un par de tablas en el mismo esquema de trabajo, dónde va registrando los pasos que ya ha ejecutado.

Para hacer su trabajo, *liquibase* necesita dos ficheros. El primero es un fichero de propiedades en el que se define la conexión con base de datos:
```
driver=com.mysql.jdbc.Driver
changeLogFile=src/main/resources/db.changelog.xml 
url=jdbc://.../esquema
username=user 
password=pass 
```

,y el segundo, referenciado por la propiedad changeLogFile, que contiene los pasos para la replicación del esquema de la base de datos:

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
    <databaseChangeLog xmlns="[http://www.liquibase.org/xml/ns/dbchangelog/1.9](http://www.liquibase.org/xml/ns/dbchangelog/1.9)" xmlns:xsi="[http://www.w3.org/2001/XMLSchema-instance](http://www.w3.org/2001/XMLSchema-instance)" xsi:schemaLocation="[http://www.liquibase.org/xml/ns/dbchangelog/1.9](http://www.liquibase.org/xml/ns/dbchangelog/1.9) [http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-1.9.xsd](http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-1.9.xsd)">
    <changeSet author="amisai" id="creacion tabla1"> 
        <createTable tableName="tabla1"> 
            <column autoIncrement="true" name="identificador" type="int unsigned"> 
                <constraints nullable="false" primaryKey="true"/>
            </column> 
            <column name="campo1" type="int unsigned"/> 
            <column defaultValueNumeric="-1" name="campo2" type="INT"/> 
            <column name="campo3" type="VARCHAR(20)"/> 
            <column name="fecha" type="DATETIME"/> 
        </createTable> 
    </changeSet> 
    <changeSet author="amisai" id="creacion de indices"> 
        <createIndex indexName="indice\_campo1" tableName="tabla1" unique="false"> 
            <column name="campo1"/> 
        </createIndex> 
    </changeSet> 
. . .
    </databaseChangeLog\> 
```

El conjunto de operaciones que *liquibase* permite describir en el fichero de cambios es bastante completo y el conjunto de motores de bases de datos soportados es bastante amplio. Además, la documentación del proyecto es bastante extensa y permite usar *liquibase* con comodidad sin necesidad de muchas búsquedas adicionales por internet.

La integración de *liquibase* con *maven*, que es la herramienta de construcción usada en el proyecto, es inmediata, ya que hay un plugin para *maven* que permite usarlo automaticamente (también existe la opción de integrar *liquibase* con *ant*, si fuera necesario como se indica [aquí](http://www.liquibase.org/manual/ant)):

```xml
. . . 
<plugin> 
    <groupId>org.liquibase</groupId>
    <artifactId>liquibase-plugin</artifactId> 
    <version>1.9.3.0</version>
    <executions> 
        <execution> 
        <id>BBDDreal</id>
        <phase>process-resources</phase> 
        <configuration>
            <propertyFile>src/main/resources/liquibase.properties</propertyFile>
        </configuration> 
        <goals> 
            <goal>update</goal> 
        </goals> 
        </execution>
    </executions> 
</plugin> 
. . . 
```

En un paso más, se planteó el poder hacer el fichero de propiedades de *liquibase* independiente de la configuración del equipo del desarrollador, y para ello se decidió insertar dentro del fichero *settings.xml* de *maven* todo aquello dependiente del entorno (url de conexión a la base de datos, nombre y contraseña del usuario). Así, se insertó en el fichero *settings.xml* de cada desarrollador los valores correspondientes:

```xml 
. . . 
<properties>
    <mysql.url>jdbc:mysql://localhost:3306</mysql.url>
    <mysql.username>root</mysql.username>
    <mysql.password>root</mysql.password> 
</properties> 
. . . 
```

,se modificó el fichero *liquibase.properties* para tener en cuenta dichos valores:

```xml
driver=com.mysql.jdbc.Driver
changeLogFile=src/main/resources/db.changelog.xml
url=${mysql.url}/esquema 
username=${mysql.username}
password=${mysql.password} 
```

y se añadió una operación de filtrado de variables en el fichero *pom.xml* de *maven*, indicándosele también al plugin de *liquibase* que utilizara el fichero de configuración con los cambios pertinentes:

```xml
<build> 
    <resources> 
        <resource> 
            <filtering>true</filtering>
            <directory>src/main/resources</directory> 
        </resource> 
    </resources> 
. . . 
    <plugin> 
        <groupId>org.liquibase</groupId>
        <artifactId>liquibase-plugin</artifactId> 
        <version>1.9.3.0</version>
        <executions> 
            <execution> 
                <id>bbdd</id>
                <phase>process-resources</phase> 
                <configuration>
                    <propertyFile>target/classes/liquibase.properties</propertyFile>
                </configuration> 
                    <goals> 
                        <goal>update</goal> 
                    </goals> 
            </execution>
        </executions> 
    </plugin>
. . . 
```

Como resultado, cada vez que se compila el proyecto se actualiza el esquema de la base de datos de trabajo de manera automática y limpia.
