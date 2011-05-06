Blog based on Django
====

Screenshot
----
+ Show
![Show](./show.png)
+ New
![New](./new.png)
+ Page
![Page](./page.png)

Function
----
+ Drop down Menu, navigate to content page.
+ Markup, User can generate html by a markdown format file.
+ Captcha, User should input a captcha when signup and login.
+ Search, User can search the page content.
+ PDF, User can generate pdf by html.
+ Backend admin
  + Page admin
    + New, user can input the page like a file tree.
    + Update, user can update the page by markup.
    + Delete, user can delete one page. 
  + User admin, CRUD

Layout
----

### Header
+ A logo | one words | Feed  
+ Blog | About | Archives

### Body
#### Left, Post 
+ Title  
+ Author | Publish Date | Category  
+ Tag  
+ Image  
+ Post Body

#### Right, Sidebar

+ Top, By Year/Month
+ Middle, By Category
+ Bottom, By Tag

### Footer
+ CopyRight 

Structure
----
+ app
    + cms
        + model
        + view
        + url
    
+ static
    + js
    + css
  
+ templates
    + cms
    
+ locale
    + zh_CN
