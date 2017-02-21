### HTTP Sessions
HTTP is a stateless protocol which means that when a HTTP server receives a HTTP request it does not know whether it has processed a request from this sender before. This makes building a HTTP Server some what easier but it does cause some problems. Consider a website like amazon.co.uk, everytime you click on a link and go to another web page on amazon, the amazon web site doesn't know that it previously gave you a page - it's doesn't know that you were the person it just gave page X to and now you are asking for page Y. Sometimes this isn't a problem but other times is can cause issues.

Let's assume you have to login to amazon so that you can make a purchase. Once you submit your username and password and amazon verifies that they are correct, amazon return a 'welcome you are logged in' page. Now you click on a book you want to buy, amazon does not know that this new HTTP request is coming from the same client that just logged in. So what does it do? Ask you to log in again? 

HTTP Sessions, coupled with cookies, allow you to get over this. Essentially everyone who comes to a website is given a unique number which is stored in a cookie on the users machine and set to expire in 15 minutes (this can vary, you can set a cookie to never expire but for the purpose of sessions you would typically set the cookie to expire in 15 minutes os something similar). Everytime the user visits the site, within 15 minutes of it previously visiting the site, the cookie is sent to the server (remember it contains a unique number for the user) and the expiry time is reset to 15 minutes from the current time. Using the unique number is the cookie the server can access a unique object it has created just for this user. This unique object is called the users session. The server can store information up on the users session such as their username, whether they have logged in or not, the last page the requested, etc. If the user does not return to the site for, lets say, 20 minutes then no cookie will be sent to the server (as it has expired) and the user sessions object on the server will also have been distroyed. In this scenario the user is typically asked to login again.

#### HTTP Sessions in ExpressJS apps
Using HTTP Sessions in ExpressJS apps is relatively straight forward (ExpressJS & Node do all the heavy lifting). All you need to do is include (require) a module that helps you read/write cookies and another one to help you create user sessions and manage them. You could if you wanted to write code yourself to do all this but it is far easier to use a good 3rd party module, all you have to do is read up on how the modules work.

The module we will be using are:
- [express-sessions](https://github.com/expressjs/session) which has the ability not only to manage user sessions but also cookies. Be sure to read the documentation of how to use it.