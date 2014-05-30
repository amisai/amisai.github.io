--- 
layout: post 
title: primeros pasos con JPA 
published: true 
date: 2010-07-05 
categories: [programming] 
--- 
Aprovechando estas vacaciones caseras :-(, he empezado a practicar con JPA 2, aprovechando algo de codigo antiguo que accede a bases de datos de las que aun tengo datos.

No venía de nuevas, leyendo el libro de Spring in action me dieron un ligero baño en algunas ideas (anotaciones para las columnas, fichero persistence.xml, ...), así que era cuestión de probar, y ver la diferencia (de uso y de configuración) con hibernate y sus ficheros .hbm.xml.

De primeras, el problema con las implementaciones... JPA define un estandar de como acceder a datos en base de datos, pero no te da ninguna implementación para empezar a correr. En principio tienes 2, una proporcionada por hibernate y otra por eclipse (EclipseLink, creo que se llama).

He empezado a probar la de hibernate, por andar por terreno conocido. La primera versión del entity-manager de hibernate que implementa JPA2 es la 3.5.0. Se supone que en el repositorio de maven de jBoss está hasta la 3.5.3 Final, pero el nexus no ha sido capaz de descargarsela !!!. En fin, versión 3.5.0.Beta-1 y a probar.

He empezado leyendome la teoría ([http://download.oracle.com/docs/cd/E17477\_01/javaee/5/tutorial/doc/bnbpy.html](http://download.oracle.com/docs/cd/E17477_01/javaee/5/tutorial/doc/bnbpy.html))
y me he puesto a probar los conceptos básicos.

Lo de las anotaciones (@Id, @Entity, @Column, @Ennumerated, ...) ha sido facil de probar. Definir el fichero persistence.xml ha sido relativamente sencillo, y una vez resuelto un problema con una
dependencia innecesaria de las librerías de hibernate que no se quitaban del classpath ha funcionado perfectamente.

Por el ejemplo que he escogido, necesitaba usar jasypt, que se encarga de encriptar datos, pero no resulta tan directo como con hibernate, igual con algún @Emmedable, o algo así.

En fin, tarde productiva, que seguiremos pronto. Por tener algún enlace, este tutorial me ha parecido bastante bueno:

[http://www.davidmarco.es/blog/entrada.php?id=144](http://www.davidmarco.es/blog/entrada.php?id=144)

, y esto sería interesante probarlo:

[http://musingsofaprogrammingaddict.blogspot.com/2010/01/jpa-2-and-bean-validation-in-action.html](http://musingsofaprogrammingaddict.blogspot.com/2010/01/jpa-2-and-bean-validation-in-action.html)
