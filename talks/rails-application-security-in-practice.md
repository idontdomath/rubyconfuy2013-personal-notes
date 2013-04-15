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
