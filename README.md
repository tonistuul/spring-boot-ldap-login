# spring-boot-ldap-login
Example project for Spring Boot LDAP/AD web login

##Basics
LDAP authentication is achieved by sending a bind request to the LDAP server. The request must contain the DN
(Distinguished Name - basically location in directory) and password of the user trying to bind. For example:
    DN: cn=Horatio Hornblower,ou=people,o=sevenSeas
    password: secret
Obtaining the DN of the user is usually the most difficult part of LDAP authentication and can be achieved via the
following options:
* Require only the CN of the user and add the rest programmatically.
    + Easy to implement
    - All users might not have the same DN structure (users located in different directories)
* Obtain the DN by performing an LDAP search
    + You choose which field is used for user authentication
    - Unless anonymous access is enabled, search requires binding (create a technical user)

Authorization (verifying resource access rights) is usually achieved by searching for the users DN in different
groups (each group maintains a list of subscribed users).

##Running the application
1. Install ApacheDS server and LDAP browser - [ApacheDS](https://directory.apache.org/)
2. Add the following partition to your LDAP server - ID: SevenSeas, suffix: o=sevenSeas, restart the server
and import example data to the new partition from resources/apache-ds-tutorial.ldif