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

