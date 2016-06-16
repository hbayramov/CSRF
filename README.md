
### Overview

In this experiment, you are going to deal with Cross Site Request Forgery (CSRF) attacks. In this context, the attacker exploits CSRF vulnerability of a web site by forcing a logged-in user to perform an action unaware of anything. The user is tricked by the attacker into entering a  page of a malicious website or clicking a malicious link to perform unauthorized actions like payment, money transfer, etc. 
The main factor utilized is validity of the user’s authentication session. Trust of a website against a user’s browser is exploited by this way.

### Setup

We are going to work on a publicly available open-source vulnerable web applica-
tion: OWASP Mutillidae 2. This application contains various web vulnerabilities
including XSS attack.  It is based on PHP and MySQL and part of the OWASP
(Open Web Application Security Project). You need to download OWASP Virtual
Machine to obtain OWASP Mutillidae 2. The virtual machine can be downloaded
from [here](https://sourceforge.net/projects/owaspbwa/files/1.2/) and OWASP Mutillidae 2 can be run from any browser in Windows, Mac
or Linux

### Page for adding a blog entry

We've created simple HTML page as main page to redirect user to links and make a specific attack.
There is simple page with blue background color and three buttons. These buttons open new HTML
page when user click on it. We've also used CSS animation framework to make things a little more
interesting. Let's start with L Pictures. User can see pictures of L when he/she'll click to L Pictures
button.

#### Entry Page

There is iframe tag that runs blog.php file on localhost when this page opens. In order to hide this
iframe from user we've added “display: none” to style. The three images of L will be displayed on
screen and user cannot realize anything about attack. Let's talk about blog.php that runs on
localhost.

When GET request is not allowed to be used to avoid a CSRF attack. We can use POST request
instead of it and perform CSRF attack successfully. User can add blog entry by using the given form
in the Add to your blog page.

If we get input and textarea names of form that page uses to add blog entry then we can submit
hidden form.

#### PHP Code

blog.php code used to add blog for user.

When the user clicks the L Pictures button, an HTTP POST request will be sent that contain above
parameters along with their values. Form will be submitted automatically when body loads. We've
take each parameter from form of add to your blog page and added proper values to it. Text area
contains text that will be added to blog. We came across a small problem when adding spaces
between words. If you try to add text by using “echo “Hey! I am L” ” it gives a error as cannot
insert value. Non-breaking space is good option to add spaces between words. It prevents automatic
line break at its position. If string does not fit at the end of line it is moved to next line and will not
be broken. Last input tag is save blog entry button. You can save blog entry by adding “Save Blog
Entry” value to submit button.

### Page for registering a new user

#### Register Page

register.php code used to add blog for user. Rest of code is the same as entry HTML page.

#### PHP Code

The user creates account by using simple form. We can get parameters of form and add proper
values to it as we did in blog-entry. Then rest of code is same as blog.php. We've just changed link
of action and value in form.

### Poll Question

Our page is a simple news page, where news taken from Zaytung.com. When user visits the page, it
contains an iframe with a url to target site and performs CSRF attack.

Another way of making this attack is using post request. For this scenario, I made a button which
makes the request when user clicked on it to see the whole news.

### Security Level

All of these happened when security level was at 0. When we raise the security level to 5, a new
blog post still added, but encoding of the texts changed.
