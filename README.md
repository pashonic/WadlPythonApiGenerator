WADL PYTHON API Generator
=============

Description
-------
WADL API Generator is a tool used to auto generate a Python API for each webservice resource defined in a WADL (Web Application Description Language) XML. There are many uses for this tool:

 *  Quickly generating single python API function calls with minimal code overhead.
 *  Loop invoke webservice resources automatically. This will allow you to create automation systems that test new webservice resources automatically without adjusting the test system.
 *  Similar to above; however, sometimes a webservice test automation system requires some manual intervention. For these cases you can keep track of what webservice resource are not being invoked so you know when the test system needs to be updated.
 *  Read all webservice resource and object data for your specific use case. Data includes: URL, Request Type, URL parameters, Data Object Request, Data Object Response.
 *  Log all webservice request and response information. Information includes: User, Password, Request Type, Run Time and much more.

The ultimate goal is to utilize WADL resources to reduce code overhead when invoking webservice resources manually and track/adapt to webservice changes automatically.

Restrictions
-------
 *  Linux (Ubuntu, Fedora, etc.), Cygwin and Windows.
 *  Python 2.7.

Usage
-------
<b>Simple Resource Fuction Call:</b>

The most common use case is to invoke a specific webservice resource. See example below:

```
import WadlApiGenerator

wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])
connection = GetConnection(username, password)
connection.[Resource]_[Request Type](urlParameter = value, xmlDataObjectParameter = value)
```

Below line reads a given WADL XML and processes all the resources and objects
```
wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])
```

Below line creates a connection and generates all the python function calls for each webservice resource.
```
connection = GetConnection(username, password)
```

Below line invokes a specific resource and request type. Python function calls are generated using a [Resource]_[Request Type] format. Resource sub directories are separated using an underscore. The request type is always added to the end of the function call name. URL Parameter's and XML object variable names are automatically matched with data read from WADL XML.
```
connection.[Resource]_[Request Type](urlParameter = value, xmlDataObjectParameter = value)
```

<b>Read Resource and Object Data:</b>

You can use the tool to access resource and object information which was obtain from the WADL XML. See below example:

```
import WadlApiGenerator

wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])

print "Printing Webservice Resource Information"

for resource in wadlManager.Resources:
    print '-' * 10
    print resource
    print wadlManager.Resources[resource]['requesttype']
    print wadlManager.Resources[resource]['url']
    print wadlManager.Resources[resource]['params']
    print wadlManager.Resources[resource]['xmlrequest']
    print wadlManager.Resources[resource]['xmlresponse']

print "Printing Webservice Object Information"

for object in wadlManager.Objects:
    print '-' * 10
    print object
    print wadlManager.Objects[object]['attributes']
    print wadlManager.Objects[object]['bases']
    print wadlManager.Objects[object]['elements']
```

<b>Loop Invoke Webservice Resources:</b>

You can use the tool to loop invoke webservice resources automatically. See below example: 

```
import WadlApiGenerator

wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])
connection = GetConnection(username, password)

for resource in wadlManager.Resources:
    connection.Apis[resource](urlParameter = value, xmlDataObjectParameter = value)
```

<b>Logging Webservice Interactions:</b>

All webservice interactions are logged into a CallLog.txt file in the working directory.

Limitations and Developer Notes
-------

 *  I have NOT tested this tool for other use cases other than my own. If you have issues with the tool for your specific use case contact me or adapt it yourself.
 *  I have only implemented the tool to deal with HTTP data requests and responses in XML format.
