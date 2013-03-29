Justine Arreche
---------------

12 column grid http://960.gs/

* skeleton responsive design (susy)
* responsive is a bitch but you have to do it.
* trying to do too much (simple would be better) KISS
* design world live (minimalist)

# Important References:

* Book: bootstraping design.
* open communication between dev and designer. 

Performance
-----------

* No pensando en la performance, en el trabajo.
* Importa porque a los usuarios les importa. UX (Nielsen Norman Group, 100 ms) 1/10 ya la computadora mantiene la atencion.
* 2011 ~ 5 tarda una pagina. 2013, hoy en dia la aplicacion se soportan, 2 segundos.
* Medir, testear, optimizar.

3 formas clasicas de obtener metricas 
* test de concurrencia, jmeter. 
* test de benchmarking, railsguides.
* profiling

## Bases de Datos

* N+1
* Slow Queries y usos
* Uso inadecuado de una DB.

Percona toolkit, query-reviewer MySQL.

## Foundation

Conocer nuestro framework y Ruby (2.0).
Turbolinks y Mailer.
Rails footnotes/New Relic.

##Codigo

Uso de caching de aplicacion, cachealo. 
Diseño general de la solucion.
Perftools.rb

## Tests

Validar los cambios con tests (TDD)
Ben Orenstein http://google.gl/FCelg


## Rails vs. OOP

Cohesion and Coupling. 

* Low Cohesion, separate with a concern.
* Coupling. Active Record Base is an example (SRP). Domain Logic and presistence are tightly coupled.

SOLID Principles.

Singles responsibility principle base to cricize rails in usual. 
"A reason for change" = Uncle Bob. (That depends on the application)

Data vs. Responsibility (Practicing ruby)

Data Centric. (More classic) > Domain Driven Approach. (Low Cohesion). Rails uses this approach.

Modelling Around Behavior Centric. Artifacts that we create and are as part of th solution. (SRP is easy but leads to an anemic model). Growing OO.. JJ2E follows this.

Ceremony vs. essence..
Ending legacy code in out lifetime. > legacy as trying to capture irrelevant detail.
Coding need to effectively transmit intent.

Abstraction has a cost in terms of inderection (given we can't control more of 7 levels, as cognitive effort).

Rails vs. OOP

Conflicting trade-offs
Room for debate

Slides: https://speakerdeck.com/cavalle/sustainable-productivity-rails-vs-oop

Rails application secury in practice.
-------------------------------------

codeclimate.com 

10 different attack:

Session hijacking: Firesheep.

* SSL everywhere ()
* secury http only cookies
* strict transport security
Strict transport security
* require password for sensitive active.

Brute force attacks

Use better algorithms BCrypt. (devise, etc).

Insecure Direct Object Reference.

Authorization

4. Mass Assignation

attr_protected
attr_accesible
strong_parameters 

5. CSRF Cross site request forging

protect_from_forgery
ensure gets are safe.

6. Offsite redirects

risk: phising, send the user to malicious site.

Countermeasures: Verify protocl and host
create a whitelist
Best: Use an id instead of a URL.

7. Unexpected code execution

* leaky routes: use strct routes.
* Unsafe render calls. render with a parameter. (use whitelist avoided system).

8. SQL Injection

Know the AR APIs | http://rails-sqli.org

9. XSS 

rails_xss
sanitize user-generated HTML (loofah).
Content Security Policies (CSP).

risks(raw and html_safe)
link_to href attributes

10. YAML Injection

YAML == eval January 8th, 2013.

avoid yaml.

Brakeman

gem install brakeman
brakeman -f html > brakeman.html

railssecurity.com



There are horror stories from the github systems team:

ruby handles raw pointers to C extensions. 

2. GC.stress = true
valgrind/ASAN

1. Static Analysis.

Timeouts en Ruby.

No hay timeouts en ruby. Green Threads (1.8.7) por lo que el kernel no los detecta. 1.9.3 los threads son nativos, el kernel lo pone a dormir pero el GVL no puede actuar. 

Solucion de Dennis Ritchie, unix is the force. Signals en el manejador de ruby, forzamos que se cancele el thread en timeout.

system_timer > usis the 

1.9.3 el codigo nativo elimine el GVL (limpieza).
Riak handbook.

Travis, JRuby, Github API and el timeout. 
Thread is sleeping or stuck in the GVL. JRuby el timeout mas largo es el de preferencia, 

MRI, is a fundamentally flawed VM.
The core ruby team is not interested on fixing it.

Ruby is trapped in a glass tower (Who is going to rescue it?) rubinius/jruby.

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

Mobile Apps
-----------
When you should go native: 

* Startup (New products, building a Most Valuable Player). 
* when experience is critical
* device features are critical

When you should go web:
-----------------------

Channel apps. (it's a separate channel, reach all users)
When you need cross platform.

Frameworks:
-----------

* jquery-mobile, Sencha touch. Based on HTML5, CSS3 and js. Try to mimic iOS native behavior which is bad.

##Native Packaging:

* PhoneGap, trigger.io, Sencha touch 

##Compiles cross platform frameworks:

* Xamarin

Con Ruby

* rubymotion, ruboto

FIREFOX OS
----------

Firefox os apps are just webapps.
WebAPI's.

## Hosted Apps

Manage updates yourself through a familiar upgrade path
Install directly from you own site.

Access to permissions: desktop notifications, geolocation, lots of api's

## Priviledged packed App

Hosted on the Marketplace servers and update from there.
Reviewed and signed (safety for end users).
Distribution Channel (Stats/Error Reporting/Js Error Reporting).

Content Security Policy (CSP): Security needs around js-inline

Access to permissions: Also device (physical) storage, contact API, SystemXHR, TCP-Sockets, Browser API.

## Certified Packaged App (Pushed by TELCO)

## Into the App structure
* Manifest: Application contains a manifest.webapp (Info of the app and permissions).
* Web Activities: Mimic intents on Android.

## More information

* Marketplace Devhub.
* SDK Ide
* Firefox Devtools: Nightly/Aurora Version
* Firefox OS Simulator
* Bootstrapping an app (Firefox OS Boilerplate)
* gluten-free.
* Dev Phone: Keon, 50 EUR shipping april. 
* Javasctipt Testing: Mocha / Chai. 
* Automated Unit Testing: Marionette

Sinatra
-------

DSL (for quickly creating web-applications in Ruby)
Middleware Rack

## Problemas (Que pasa cuando crezco):

* Como organizar los controllers (Rackmount)
* Rutas no restful
* Inline templates, al final del archivo sinatra.

La Solucion (Mi sinatra)

## Apliquemos Buenas Practicas:

* Definir una estructura de directorios.
* ORM y uso de base de datos.
* elegir un test framework
* classic or modular
* Uso de Rack a nuestro favor. 
* configuracion por defecto

Ideas Cinemargentino: User voice.

Puppet
------

* Virtualizacion > Servidores se vuelven mas especificos.
Nos subimos al sistema de packages. 
* Ahora vino esto de la nube, tengo imagenes y sistema de packeges. Aparecen servers y no se porque estan ahi... 

Puppet, es una herramienta de automatizacion. 

MCollective
Dashboard
PuppetDB
Hiera
Facter

Ruby Toolbox

## clap: https://github.com/soveran/clap

Las funciones anonimas responden a arity (cantidad de parametros). 

## gs: https://github.com/soveran/gs (init de un gemset)

variante para el uso de bundler (isolate como variante).

## github.com/cyx/gemfile

Generate a gemfile using installed gems. Enviandolo a heroku

## github.com/lucasefe/gn

A simple file generator.

## github.com/soveran/ost

Redis based queues and workers

## github.com/soveran/cargo

inclusion de librerias en distintas versiones

## github.com/soveran/scrivener

Lighting Talks
--------------

Spy: https://github.com/ryanong/spy
Stop the rant: 	
Intervals: https://github.com/badosu/borel
http://rubygrapevine.com/

Scala en 5 minutos: @fedesilva https://speakerdeck.com/fedesilva/scala-in-5-minutes
tipos unificados

RESOLUTIONS
-----------

## lunes por la tarde
* code reviewing/back to code. 

## 8 de abril
* ir a los meetups de ruby 

## 23 de septiembre
* dejar mi trabajo

A rubyst's guide to Design
--------------------------

Early and often a website design should start where its going to live.

3 Parts for a faster design process:

* Don't fear the white canvas. Sketches in paper.
* You can have a foundation.

## CSS Framework

pick and choose what adds a bit of value.
don't fear to rip out what you are not using.

Grids can be really useless.
But can help to format content.
960.gs (the original ganster)

bootstrap
skeleton
foundation

They are flexy.

Use of media queries, and are really awesome (conditional css).

## Pattern Libraries, on how you write codes:

Pears (http://pea.rs/)

## Visual Patterns

Design is mostly a trained eye. (http://dribbble.com/)
http://dribbble.com/buckets

* CSS for web designers (A Book Apart)
* HTML5 for web designers (A Book Apart)
* http://css3exp.com/moon/

## Icon Fonts, saved my life

in the photoshop flow you redo everything.

## SASS/SCSS

the community is opinionated, but the conputer doesn't care.
light/darken.
syntax errors (quite useful in a rails app).

## Work within constraints

* Styleguides (aren't just for color palettes). Are also for CSS, JS, Ruby Code.

KSS (https://github.com/kneath/kss) A methodology for documenting CSS and generating styleguides

## Prototyping

* It's easy if you write code.
* Use gists, share with other what you are doing, or http://dabblet.com
* Pull requests are an awesome design tool

Summary: http://julieannhorvath.com/resources/

Dissecting Ruby with Ruby
-------------------------

http://www.codetriage.com/
http://schneems.com/ut-rails (rails videos).
@schneems will post 

Lean software development
-------------------------

eliminate waste
amplify learning
decide as late as possible
deliver as fast as possible
empower the team (involve people in the process of what is going to be done)
build integrity in ()
see the whole

Implementing Lean Software development

## Eliminite Waste

* Unnecessary code an functionality
* How much of that do we actually use? Hyp: 50-90%

## Why don't use simpler tools?
* Cons: steeper learning curve. relearning, you move to basic ruby. slower development?
* You win: Performance, Control.
* Their stack: cuba, ohm, ost, mote, shield, cutest.

Lean Leadership a.k.a don't be an asshole
-----------------------------------------

My story: Weird career, bullshit artist. 
Management vs. Leadership.

Buffalo was to be something (3rd in the US), the Erie canal. 
Railways came changed the 
Yale: Learning & Doing. 

Ideas are cheap, execution is everything.
People Patterns: The marshmellow Study. 
Psycohology/Economics: Studies with ask of quarters in the city. Control was a touch in the arm. (Methods of influence, book).
SF: Tenderloin Peace Corp. This is the last place where i managed people (reporting). Try to run a business in an environment was unsafe and inneficient. 3 1/2.
Yahoo! Brickhouse: Czar, division to entrepeneurship. Create new companies Encouraged to fail 8 times to 10. 
Bravo, Fire Eagle.. Macro level killed that. > Turned into etsy.

Betable > social gaming and gambling startup. It didn't work. 

Customer Development: running lean, the lean startup the four steps to the epiphany. (Eric Ries). You can read, but you need to start doing those things by yourself, otherwise you don't train the muscle. (Is not rocket science) You get confidence by reading, the hard is building the right thing.

HP/Snapfish: Monkeys, Bananas, ladder. No punishment, no banana but everybody still is with the old culture.

Bridge Metaphor. To transition your customer, to the future, you need to move them by steps. Try to bridge hp to build other things.

Waterfall vs. the rapids: Agile was of the first things. Go there slowly.

Scrum is more Managament, "is a good tool to" to move people towards agility. Lean product expertise. XP is when the team is flowing better.

Neo: Director of BDD. 

Control is an illusion. The space between circunstances and response. Trust, you need to give benefit of the truth. 

Forgiveness not permission (Edie Rama, TED Talk). Public spaces where a good way of getting people together. act with good intentions and ask for forgiveness.

Management History. 

* Apply scientific methods on business.
* Soldering as science. The science of management.

When we want someone, a degree doesn't mean that is going to cover that is going to be ok with your team.
Extracting efficiency out of working systems (there is where management works).


There are no cluesm, new tech and
steer the team where we don't know were to go? Brave to World. 
More outside the box, thinking (the low hanging fruit is gone).
How we work with 200 years of management.

Plan vs. Planning. Eisenhower
The artifact of a plan is fruta. Is old.
The process is completely needed. The value of the act of planning is needed. Structure facilitates the planning. 

The core of building awesome shit together is trust. 

We are all using different hats. 
Technology, Design, Leadership (TED Talk).

Art makes questions
Design makes solutions
tech makes possibilites
leadership makes actions.

Things are only tools, that will make you

"Control vs. Freedom": You can't control everything, freedom is not going to save success.
Spectrum of Control: 

Reflex: instinctive and inmediate reaction to stimuli
Problem solving: creativity constraied by reality

Intrepeneurs Dilemma.
Xerox Sparc (Freedom)
HP (Control)
Yahoo (somewhere in between)

@joi principles: Media Lab. We are ighting with a balance.
We have a usual 

How Ruby Programmed Me
----------------------
http://www.janodeamerica.com

Que debe haber sentido la banda que cerro woodstock. ellos tocan porque les gusta.
nada que ver sobre el hecho de poner tenedores en mi cabeza.
@hop_in / websitenote
@dynlangchile

## Language & Thought: 

* como el lenguaje modela nuestro pensamiento.
Esto no va ser como hacker news.

## Como los lenguajes de programacion fueron modelando mi forma de pensar.

cerebro: Arcilla esperando a ser modelada por las manos correctas. 
"ars longa, vita brevis."

Paul Graham.
Saber que pasa en otros lados es lo que nos hace crecer tu mundo.

"Let" languages shape your though.

* A quien despues de ser chuck norris le interesa ser un bebe de ninio en otro lenguaje?
* Sigue abierto a aprender. Cual es el estado mental que hay que tener?

La mente del aprendiz:

* Openness (libre de concepciones previas).
* A cup of tea. aria tu taza y esten receptivos a aprender cosas nuevas.

Como se llega a ser un maestro? (Modelo de Dreyfuss)

SHU: Protect / Obey.
HA:  Detach / Disgress
RI:  Leave / Separate (ya no hay reglas que obedecer o que romper)

Hacker vs. Thinker:

Hacker: GTD, Fast, Pecados: Hack. Maintenance Nightmare. Needs More Duct Tape.
Thinker: Thinks about abstractions, maintenance. Too many abstractions. Analysis paralysis.
Needs more layer.

El camino a la perfeccion y creer que hay uno solo? Miedo. 
La vida diaria es el camino. como hago para estudiar el camino? como te vas a preocupar de seguirlo.

Estudiar la forma correcta que no nos preocupamos de hacer las cosa.

Smalltalk in perl disguise. 

Happy thinker (hace felices a los dos programadores) -> Armonia. 

Nos libera de la tradicion de la dicotomia, no pueden existir unos con otros.

The path is NO PATH

Weird fact -> Every developer is a manager -> OMG.
Dejen que ruby cambie sus vidas. Dejen que la programacion cambie sus vidas.

Fork y merge. 

Learn, sean abiertos de mente.
Diviertanse
share

