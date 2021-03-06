/*    Copyright (c) 2012 Zuora, Inc.
 *
 *   Permission is hereby granted, free of charge, to any person obtaining a copy of 
 *   this software and associated documentation files (the "Software"), to use copy, 
 *   modify, merge, publish the Software and to distribute, and sublicense copies of 
 *   the Software, provided no fee is charged for the Software.  In addition the
 *   rights specified above are conditioned upon the following:
 *
 *   The above copyright notice and this permission notice shall be included in all
 *   copies or substantial portions of the Software.
 *
 *   Zuora, Inc. or any other trademarks of Zuora, Inc.  may not be used to endorse
 *   or promote products derived from this Software without specific prior written
 *   permission from Zuora, Inc.
 *
 *   THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
 *   IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
 *   FITNESS FOR A PARTICULAR PURPOSE AND NON-INFRINGEMENT. IN NO EVENT SHALL
 *   ZUORA, INC. BE LIABLE FOR ANY DIRECT, INDIRECT OR CONSEQUENTIAL DAMAGES
 *   (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES;
 *   LOSS OF USE, DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON
 *   ANY THEORY OF LIABILITY, WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT
 *   (INCLUDING NEGLIGENCE OR OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS
 *   SOFTWARE, EVEN IF ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.
 */

Zuora PHP Toolkit

INTRODUCTION
------------

The PHP toolkit provides useful utilities for Zuora developers to introspect, pull data from and develop against the Zuora APIs.

Zuora Support does not troubleshoot content from GitHub. The sample code is as an example of code 
that has worked for previous implementations and was created by both Zuora and non-Zuora authors. 
Please send any GitHub-related comments and feedback to Dev-Support@zuora.

REQUIREMENTS
------------

This utility requires PHP with add-ons. The following are required to run this package.

PHP 5.2.9+
-SOAP
-OpenSSL
-XML-RPC
-XSL

CONTENTS
--------

call-lib.php - re-usable library of Zuora API calls
index.php - API utility front page
queryMore.xml - queryMore() template
readme.txt -this file
subscribe.xml - subscribe() template, latest version
subscribeV9.xml- subscribe() template, version 9
subscribeV11.xml - subscribe() template, version 11
subscribeWithExistingAccount.xml - subscribeWithExistingAccount() template, latest version
subscribeWithExistingAccountV9.xml- subscribe() template, version 9
zuora-19.0-sandbox-AllOptions.wsdl - v19 WSDL, sandbox
zuora-25.0-sandbox-AllOptions.wsdl - v25 WSDL, sandbox
zuora-27.0-sandbox-AllOptions.wsdl - v27 WSDL, sandbox
loader/index.php - Loader utility front page
loader/call.php - Loader command line code
loader/settings.php - Loader common settings file

INSTALLATION INSTRUCTIONS (Windows)
-----------------------------------

The following instructions assume that you're going to use Xampp (http://www.apachefriends.org/en/xampp.html) on the localhost as the web server.

a) Make sure no other application is running on port 80. You can verify this by running "netstat -a -n -o" on the command prompt. Terminate the offending app, if running on port 80.

b) Install Xampp for Windows using default path.

c) Run the Xampp config tool.

d) Click on Port Check button on the Xamp control panel. Make sure Port 80 is available.

e) In the Xampp control panel start Apache server.

f) In the Xampp directory, extract the zip file (Zuora source) under a folder named api-util.

g) Make sure Apache is running.

h) In a web browser type http://localhost/api-util/. This should load up the API Utility for Zuora. http://localhost/api-util/loader/ should load the API Loader.

INSTALLATION INSTRUCTIONS (Mac OS X)
-----------------------------------
By Richard Sawey, March 2012

Validate you have the necessary PHP level and modules by opening a Terminal window. Type 'php -v' to get the version, type 'php -m' to see the built in modules. My Mac, running Mac OS X 10.6.8 has all the modules installed and a more recent version of PHP, v5.3.8, than that needed by Zuora.

Mac OS X has the Apache web server built in, you do not need Xamp. You need to turn Apache on by opening Applications > System Preferences (look for it in your Dock) and go to the Sharing panel. Under the Services table, check Web Sharing. The Apache web server should now be running and will automatically start every time your computer boots unless you change the settings in the System Preferences. Because Apache runs as a background service or daemon and not a normal application, it won't appear as an item in the Dock when it's running.

You can now test your web server is running by typing 'http://localhost' into your web browser. You'll see a blank page apart from the message 'It works!'.
open a Finder window and go to /Library/WebServer/Documents/ (this is /Library starting from your hard drive's root directory, NOT /Library in your personal home directory). You should see a group of HTML and image files including one called index.html.en These files are used in the default Apache page you just viewed.

In this /Library/WebServer/Documents directory create an 'api-util' directory and copy the downloaded files into this directory. 

By default, the PHP Apache module is not activated. After enabling write access, uncomment the line ”LoadModule php5_module libexec/apache2/libphp5.so” in file “/private/etc/apache2/httpd.conf” to enable PHP on Mac OS X Apache web server. By default, access to the httpd.conf is read only. You need to change the file permissions  so you can write to it. I did this with 'sudo chmod 666 httpd.conf' which prompts you for your Mac login password before changing the file permissions. With the file permission changed use a text editor and uncomment the above mentioned line. Save, then stop and restart Apache using the Sharing panel.

Assuming you now have this file tree:
/Library/WebServer/Documents/api-util
with lots of files like:
/Library/WebServer/Documents/api-util/index.php
/Library/WebServer/Documents/api-util/generate.xml
as well as a sub folder:
/Library/WebServer/Documents/api-util/Loader
 
Then this URL should bring up the familiar API utility:
http://localhost/api-util/

Once you've tested this and got the utilities working consider going back and disabling the write permissions on httpd.conf:
sudo chmod 644 httpd.conf
And if you don't think you'll be using Apache for a while, disable in the Sharing panel, it's a potential vulnerability. On the internet (or in your favorite coffee shop) your box's port 80 (where Apache is listening) will be constantly probed.

Finally, the Xamp/Windows instructions include a bunch of proxy setup instructions which I don't need and so haven't attempted here on Mac OS X.

POTENTIAL INSTALLATION ISSUES
-----------------------------
With the latest XAMPP (version 1.7.4), there are a couple of additional things that need to be done in the php.ini file located in the \xampp\php\ folder:

-In the "Error Handling and Logging" section, error_reporting value needs to be changed to (preventing run time errors from displaying with the application):
  error_reporting = E_ALL & ~E_NOTICE 

-In the "Windows Extensions" section, some of the required extensions are commented out, specifically:
  extension=php_openssl.dll
  extension=php_soap.dll
  extension=php_xmlrpc.dll
  extension=php_xsl.dll

Also, it is possible that your enterprise is using a proxy, which will need to be configured, otherwise you'll get an "Unknown Host" error. To set up a proxy with XAMPP (instructions taken from http://stackoverflow.com/questions/724599/setting-up-an-apache-proxy-with-authentication, adapted by Alexander Grinchik):

-Uncomment the following lines in httpd.conf file (found in xampp/apache/conf/):
  LoadModule proxy_module modules/mod_proxy.so
  LoadModule proxy_http_module modules/mod_proxy_http.so

-Include the following line in httpd.conf file:
  # Implements a proxy/gateway for Apache.
  Include "conf/extra/httpd-proxy.conf"

-Create a new file in xampp/apache/conf/extra/ directory called httpd-proxy.conf with the following contents:
#
# Implements a proxy/gateway for Apache.
# # Required modules: mod_proxy, mod_proxy_http
#

<IfModule proxy_module>
<IfModule proxy_http_module>

#
# Reverse Proxy
#
ProxyRequests On
ProxyVia On

<Proxy *>
    Order deny,allow
    Allow from all
</Proxy>

</IfModule>
</IfModule>

DOCUMENTATION & SUPPORT
-----------------------

API Documentation is available at http://developer.zuora.com
