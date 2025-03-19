---
title: 'Wordpress Multisites'
date: 2025-03-19T08:19:18-07:00
draft: false
tags: ["wordpress", "multisites", ".htaccess"]
cover:
  image: "/images/wordpress-multisites.png"  # Path to your image
  alt: ""  # Alt text for the image
  caption: ""
  hidden: true  # Set to true if you don't want to show the image in the
  hiddenInList: false  # Show the image in the post list
  hiddenInSingle: true  # Hide the image in the single post view
---
Enabling WordPress Multisite allows you to manage multiple sites from a single WordPress installation. Here’s how you can set it up:

Backup Your Site: Before making any changes, ensure you have a complete backup of your WordPress site.

**Edit wp-config.php:**

Open your wp-config.php file.
Add the following line above the /* That's all, stop editing! Happy publishing. */ line:

```
define('WP_ALLOW_MULTISITE', true);
```

**Access Network Setup:**

- Log in to your WordPress dashboard.
- Go to Tools > Network Setup.
- Choose whether you want to use subdomains (e.g., site1.example.com) or subdirectories (e.g., example.com/site1).
- Click Install.

**Update wp-config.php and .htaccess:**

WordPress will provide some code to add to your wp-config.php and .htaccess files. Follow the instructions provided.
Add the provided code to your wp-config.php file:
```
define('MULTISITE', true);
define('SUBDOMAIN_INSTALL', false); // Set to true if using subdomains
define('DOMAIN_CURRENT_SITE', 'example.com');
define('PATH_CURRENT_SITE', '/');
define('SITE_ID_CURRENT_SITE', 1);
define('BLOG_ID_CURRENT_SITE', 1);
```
Update your .htaccess file with the provided rewrite rules.
```
RewriteEngine On
RewriteRule .* - [E=HTTP_AUTHORIZATION:%{HTTP:Authorization}]
RewriteBase /
RewriteRule ^index\.php$ - [L]

# add a trailing slash to /wp-admin
RewriteRule ^([_0-9a-zA-Z-]+/)?wp-admin$ $1wp-admin/ [R=301,L]

RewriteCond %{REQUEST_FILENAME} -f [OR]
RewriteCond %{REQUEST_FILENAME} -d
RewriteRule ^ - [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(wp-(content|admin|includes).*) $2 [L]
RewriteRule ^([_0-9a-zA-Z-]+/)?(.*\.php)$ $2 [L]
RewriteRule . index.php [L]
```

Log out and log back in to your WordPress dashboard.
**Network Admin Settings:**

You’ll now see a new My Sites menu in the admin bar.
Go to My Sites > Network Admin > Dashboard to manage your network settings.

**Configure Network Settings:**

From the Network Admin dashboard, you can add new sites, install themes and plugins, and manage your network settings.
