--- 
layout: post 
title: del plugin release para maven 2 
published: true
date: 2010-05-27 
categories: [programming] 
--- 
He encontrado un hueco (o lo hemos fabricado, que esto suele ser así) para probar el plugin release de maven, que se encarga de gestionar automaticamente las versiones de los módulos de una aplicación.

En principio, todo el desarrollo de una aplicación (mono- o multi-módulo) con maven debería tener versiones SNAPSHOT, que sólo quedan fijas cuanto se ha terminado el trabajo previsto para esa
versión. Se presenta entonces el problema de actualizar el número de versión en todos los pom.xml de todos los módulos, y de marcar de alguna manera en el SCM el fin de esa versión. El plugin release hace esas 2 tareas:

-   por un lado, cambia el número de versión (de 0.1-SNAPSHOT a 0.2-SNAPSHOT, por ejemplo)
-   por otro, inserta en el SCM una versión final (0.1, en el ejemplo) de la aplicación y la siguiente versión de desarrollo de la aplicación (0.2-SNAPSHOT, en el ejemplo).

Para realizar el proceso, y aunque hay otros goal más, se usa el goal 'release:prepare'.

El goal 'release:prepare' comienza su ejecución comprobando que no hay cambios sin introducir en el SCM y que no quedarán dependencias SNAPSHOT sin resolver. A continuación pide del usuario una serie de valores (numero de versión final, número de la siguiente versión de desarrollo de la aplicación y el tag con el que marcar la versión final en el SCM) y cambia en los pom.xml de todos los módulos los números de versión al número de la versión final. Antes de realizar el commit de los pom.xml, realiza una comprobación (con 'clean verify') comprobando también que los test se ejecutan correctamente. Una vez realizada la comprobación, realiza un commit de esos pom.xml y etiqueta el código en el SCM con el tag solicitado anteriormente: Sólo le queda actualizar de nuevo los
pom.xml para que tengan el número de la siguiente versión de desarrollo y realizar el commit correspondiente.

La verdad es que el proceso de este goal es más largo de enumerar que de ejecutar y el resultado es el esperado, aunque igual por el camino te encuentras, como ha sido mi caso, que el SCM no esta bien configurado para realizar los commit (y push, en el caso de usar git (¿y similares?) y hay que trabajar un poco más de lo deseado para tener bien configurada la infraestructura (pero eso es, claro, la primera vez que se realiza el proceso).
