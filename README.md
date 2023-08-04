# PHP-Environment-Windows

## Apache Setup

* Download Apache Server from [Link]([Apache VS17 binaries and modules download (apachelounge.com)]). It is  **Apache Lounge** Windows Binaries.
* Download and Install the [Visual C++ Redistributable for Visual Studio 2015-2019 x64](https://support.microsoft.com/en-us/help/2977003/the-latest-supported-visual-c-downloads).
* Add Apache Server files in `C:\Server` directory.
* Go to conf folder and open httpd.conf in any text editor.
* `Define SRVROOT "C:\Server\Apache"` or change the path to your location.
* Then, Add `ServerName localhost:80` and `HostnameLookups Off`.
* Change AllowOverride None to AllowOverride All to enable .htaccess files in your projects `AllowOverride All`
* Check if you the mod_rewrite module is enabled. Find the line

```
#LoadModule rewrite_module modules/mod_rewrite.so
```

* And remove the # from the beginning to enable the module:

```
LoadModule rewrite_module modules/mod_rewrite.so
```

- To serve index.php file automatically if a directory is requested append **index.php** to the DirectoryIndex variable

```
<IfModule dir_module> 
DirectoryIndex index.html index.php 
</IfModule>
```

* To test the installation, open up the command prompt, go to **C:/Server/bin** and run Apache by typing **./httpd.exe** in terminal. I was using powershell.
* If there is no error, open up a browser of your choice and go to **http://localhost
* To **run Apache automatically on startup**, register it as a service. Open the Command Prompt as administrator (right click -> Run as administrator) and type `httpd -k install` 
* Check Apache service in Services and click _Start the service_


## PHP installation

* Download PHP (Thread Safe)  and go to `"C:\Server\PHP"` and paste PHP files there
* Then, open terminal and type `C:>setx path "%PATH%, C:\Server\PHP" /M` to Add PHP to system environment variable.
* Open the **httpd.conf** Apache configuration file again and **add these lines to the end** of the file:

```
PHPIniDir "C:\Server\PHP"
AddHandler application/x-httpd-php .php
LoadModule php_module "C:\Server\PHP\php8apache2_4.dll"
```

**Note**: in PHP 7 `LoadModule php7_module "C:\Server\PHP\php7apache2_4.dll"`  instead of
`LoadModule php_module "C:\Server\PHP\php8apache2_4.dll"`

* **Restart Apache** 2.4 service in Services
* To test the installation, create a file named index.php in **C:/Server/Apache/htdocs** directory and copy these lines to the file:

```
<?php 
phpinfo();
```

* Open a browser of your choice and open http://localhost/
