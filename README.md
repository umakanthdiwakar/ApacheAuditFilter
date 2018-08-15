# ApacheAuditFilter

During instrumentation of a distributed application, one very critical feature we needed was to be able to print a particular XML element, that is part of the SOAP request in the Apache access logs. While it is easy to print the http headers in the Apache access log through the %{element-name} feature in httpd.conf, Apache does not have any native capability to parse XML and print an element in its access log.

This filter applies its logic only when the requests are POST requests and the Content-Type is text/xml, which is always the case with SOAP requests. It then extracts a particular element from within the SOAP payload and injects a HTTP header into the request. This enables this element to be logged as part of the Apache access log.

Here are some simple steps to create a skeleton Apache module. 

Let us assume that apache is installed in /usr/local/apache2. Let us also assume that you want to create a filter called as myfilter.

$ cd /usr/local/apache2

$ bin/apxs -g -n myfilter

$ cd myfilter

$ vi mod_myfilter.c

Perform your edits of the file here. Please refer apache documentation to understand the purpose of each function in the skeleton.

$ ../bin/apxs -c -i mod_myfilter.c

This will compile and deploy your module as a shared library in the "modules" directory.

Now add the following line to httpd.conf

LoadModule module_myfilter modules/mod_myfilter.so
