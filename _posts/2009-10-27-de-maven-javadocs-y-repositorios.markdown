--- 
layout: post 
title: De maven, javadocs y repositorios. 
published: true 
date: 2009-10-27 
categories: [programming]
--- 
Resulta que maven puede descargar los javadocs de las dependencias de tu proyecto (si existen en el repositorio, claro ;-) ). Es tan sencillo como:

mvn dependency:resolve -Dclassifier=javadoc

Para que tus javadocs esten en el repositorio: [http://maven.apache.org/plugins/maven-javadoc-plugin/faq.html\#How\_to\_deploy\_Javadoc\_jar\_file](http://maven.apache.org/plugins/maven-javadoc-plugin/faq.html#How_to_deploy_Javadoc_jar_file)

Si eres de los que usan Netbeans, puedes hacer lo mismo en un proyecto definido con maven: 
[http://wiki.netbeans.org/TaT\_GettingJavadocFromMavenNB](http://wiki.netbeans.org/TaT_GettingJavadocFromMavenNB)
