# CROSS SITE REQUEST FORGERY (CSRF)

It is an attack which forces an end user to execute unwanted actions on a web application in which he/she is currently 
authenticated. With little help of social engineering (like sending a link via email or chat), an attacker may force
the users of a web application to execute actions of the attacker's choosing.A successful CSRF exploit can compromise
end user data and operation, when it targets a normal user. If targeted end user is the administrator account, a CSRF
attack can compromise the entire web application.

## Example 
Suppose the attacker sends the user an email inducing him to visit an URL referring to a page containing the following
(oversimplified) HTML:
```
 <html><body> 
... 
<img src=”https://www.company.example/action” width=”0” height=”0”> 
... 
</body></html> 
```
What the browser will do when it displays this page is that it will try to display the specified zero-width (i.e., invisible)
image as well. This results in a request being automatically sent to the web application  hosted  on site.Its not important 
that the  image  URL does not refer to a proper image, its presence will trigger the request specified in the src field anyway.
This happens provided that image download is not disabled in the browsers, which is a typical configuration  since  disabling 
images  would  cripple  most  web  applications beyond usability.

##  sample scenario 
Let’s suppose that the victim is logged on to a firewall web management application.  To log in, a user has to authenticate
himself and session information is stored in a cookie.Let’s suppose the firewall web management application has a function 
that  allows  an  authenticated  user  to delete  a  rule  specified by its positional number, or all the rules of the
configuration if the user enters ‘*’ (quite a dangerous feature, but it will make the example  more interesting).  The 
delete page  is shown next. Let’s suppose that the form – for the sake of simplicity – issues a GET request, which will be 
of the form

https://[target]/fwmgt/delete?rule=1 (to delete rule number one)
 https://[target]/fwmgt/delete?rule=* (to delete all rules).
 
 Therefore, if we enter the value ‘’ and press the Delete button, the following GET request is submitted. 
 https://www.company.example/fwmgt/delete?rule= with the effect of deleting all firewall rules (and ending up in a possibly 
 inconvenient situation).
 
 Now, this is not the only possible scenario. The user might have accomplished the same results by manually submitting the
 URL or by following a link pointing, directly or via a redirection, to the above URL. Or, again, by accessing an HTML page
 with an embedded img tag pointing to the same URL. 

https://[target]/fwmgt/delete?rule=*
