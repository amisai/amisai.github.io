--- 
layout: post 
title: Trabajando con una base de datos de pruebas en local 
published: true 
date: 2009-12-28 
categories: [programming]
--- 
Una vez que *liquibase* ha cumplido ampliamente su encargo de centralizar los cambios en la base de datos, como se comentaba [aquí](http://amisai.posterous.com/controlando-la-evolucion-de-la-base-de-datos), el siguiente problema ha sido el evitar que las pruebas unitarias (o de integración, depende de la definición de *unit tests* que usemos :-) ) interfirieran con los datos usados en las pruebas de la aplicación. La solución evidente es usar 2 esquemas de base de datos :-), uno para las pruebas de la aplicación y otro para las pruebas unitarias... y tener 2 configuraciones de *liquibase*, cada una con información identica en cuanto a los cambios en el esquema de base de datos, pero con la información adecuada con respecto al esquema de base de datos en el que trabajar.

La idea sería que *liquibase* hiciera los cambios primero en el esquema de pruebas unitarias, para poder comprobar que tanto los cambios en la definición del esquema como el código que usa dichos cambios son adecuados y que todo es correcto antes de realizar los cambios en la base de datos de "producción" local. Para ello hacen falta 2 ficheros *liquibase.properties*, uno en src/main/resources, con los datos de la conexión al esquema local de "producción":

```
driver=com.mysql.jdbc.Driver
changeLogFile=src/main/resources/db.changelog.xml
url=${mysql.url}/esquema 
username=${mysql.username}
password=${mysql.password} 
```

, y otro, en src/test/resources, con los datos de la conexión al esquema local de pruebas:

```
driver=com.mysql.jdbc.Driver
changeLogFile=src/test/resources/db.changelog.xml
url=${mysql.url}/esquemaTest 
username=${mysql.username}
password=${mysql.password} 
```

Para evitar actualizaciones indeseadas en el esquema de "producción", utilizaremos 2 ficheros *db.changelog.xml*, uno en src/main/resources y otro en src/test/resources. Primero se modificará el fichero en src/test/resources, y una vez terminado el desarrollo se copiaran los cambios al de src/main/resources. El proceso manual es un engorro, ciertamente, y buscaremos una solución para hacerlo más automático...

Ya sólo resta asociar los ficheros de configuración de *liquibase* con diferentes momentos del ciclo de vida de *maven*, para que la actualización de la base de datos se produzca en los momentos adecuados:

```xml 
<plugin> 
    <groupId>org.liquibase</groupId>
    <artifactId>liquibase-plugin</artifactId> 
    <version>1.9.3.0</version>
    <executions> 
        <execution> 
            <id>BBDDreal</id>
            <phase>process-resources</phase> 
            <configuration>
                <propertyFile>target/classes/liquibase.properties</propertyFile>
            </configuration> 
            <goals> 
                <goal>update</goal> 
            </goals> 
        </execution>
        <execution> 
            <id>BBDDpruebas</id>
            <phase>process-test-resources</phase> 
            <configuration>
                <propertyFile>target/test-classes/liquibase.properties</propertyFile>
            </configuration> 
            <goals> 
                <goal>update</goal> 
            </goals> 
        </execution>
    </executions> 
</plugin> 
```