# Company Website CMS Dashboard Exists Unauthorized Access Vulnerability

[Company Website CMS](https://www.sourcecodester.com/php/15517/company-website-cms-php.html) Released by SourceCodester Has Unauthorized Access Vulnerability

The background of the site is `/dashboard`, which requires login to access. In the background, operations such as publishing articles, uploading files, changing websites, and deleting information can be performed. However, the site has an unauthorized access vulnerability, and any operations can still be performed after deleting cookies.

How to test: Log in to `/dashboard` to do anything like modify **Site Settings**, then delete cookies and try again.

Take Site settings as an example:

To modify the site title

![image-20220807000836564](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807000836564.png)

Modify Site Title to 123

![image-20220807000947231](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807000947231.png)

![image-20220807001127808](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807001127808-16598022888061.png)

Delete the cookie, then modify the Site Title to 456

![image-20220807001343169](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807001343169.png)

![image-20220807001454444](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807001454444.png)

After deleting the cookie, the modification is still successful.



## Code analysis

Let's take a look at `/dashboard/index.php` first:

![image-20220807002310654](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807002310654.png)

The `/dashboard/ndex.php` page first contains the `header.php` page, and then gets the username through `$_SESSION`.

`$username` on the `index.php` page is only used to output the username.

![image-20220807002605801](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807002605801.png)

---

Let's look at the header.php page:

if username session is NOT set then this page will jump to login page

![image-20220807002812929](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807002812929.png)

---

Let's look at the code for Site Settings, which is site-settings.php

![image-20220807003110478](Company%20Website%20CMS-Unauthorized%20Access.assets/image-20220807003110478.png)

As you can see, this page does not do any verification for user identity.

The same is true for the rest of the dashboard pages.



## Link

https://www.sourcecodester.com/php/15517/company-website-cms-php.html