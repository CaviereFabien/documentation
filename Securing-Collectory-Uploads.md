# Securing the uploads into a collectory instance

To this, it is recommend to use a IP whitelist in Apache (which sits infront of a tomcat instance) like so:

```
<Location /upload/>
  Order deny,allow
  Deny from all
  Allow from 35.157.*
</Location>
```