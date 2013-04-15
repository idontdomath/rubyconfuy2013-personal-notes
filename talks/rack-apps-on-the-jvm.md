Cristian Rush
-------------

Despliege de aplicaciones rack sobre la JVM.

Flags esenciales de la jvm. 

modo client y modo server -server. Bootstrap mas lento, pero hace optimizaciones mas agresivas.
-Xms512m
-Xms2048m

Plain old ruby sobre JVM? > JRuby. (jdk)
JRuby:

* Minimo soporte para operaciones unix de bajo nivel
- No hay fork pero tenemos native threads.
* Extenciones C no estan soportadas, pero hay alternativas:
-pg > jdbc-postgres
therubyracer > therubyrhino.

Cosas buenas:
1 proceso con multiples hilos (aplicacion debe ser thread safe).
El uso de la JVM implica: Pluralidad de lenguajes. clojure, scala.
Nutter enebo why jruby works.

Otras opciones:

Puma, Mizuno, etc. Lightweight ways > Puma.

* Warbler > crea un war para deployment en cualquier container de servers.
- Desventajas, background tasks.

* Trinidad. Apache tomcat embebido (soporte de extnsiones).

* Torquebox (application server basado en JBoss AS).
Dependencia con el application server.

# Referencias: 

* Deploying with JRuby (http://pragprog.com/book/jkdepj/deploying-with-jruby).
