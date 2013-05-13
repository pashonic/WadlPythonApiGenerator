WADL API Generator
=============

Description
-------
WADL API Generator is a tool used to auto generate a Python API for each resource listed in a WADL (Web Application Description Language) XML. There are many uses for this tool:

 *  Quickly generating single python API function calls with minimal overhead.
 *  Loop invoke webservice automatically. This will allow you to create automation systems that test new webservice resources automatically without adjusting the test system.
 *  Similar to above; however, sometimes a webservice test automation system requires some manual intervention. For these cases you can keep track of what webservice resource are not being invoked so you know when the test system needs adjustment.
 *  Read all webservice resource and object data for your specific use case. Data includes: URL, Request Type, URL parameters, Data Object Request, Data Object Response.
 *  Log all webservice request and response information. Information includes: User, Password, Request Type, Run Time and much more.

Restrictions
-------
 *  Linux (Ubuntu, Fedora, etc.), Cygwin and Windows.
 *  Python 2.7

Usage
-------
<b>Simple Call:</b>

The most common use case is to invoke a specific webservice resource. See example below:

```
import WadlApiGenerator

wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])
connection = GetConnection(username, password)
connection.[Resource]_[Request Type](urlParameter = value, xmlDataObjectParameter = value)
```

Below line reads a given WADL xml and reads all the resources and objects
```
wadlManager = WadlApiGenerator.WadlManager([Link to WADL via http])
```

Below line creates a connection and generates all the python API's for each webservice resource.
```
connection = GetConnection(username, password)
```

Below line invokes a specific resource and request type. Python function calls are generated using a [Resource]_[Request Type] format. Resource sub directories are separated using an underscore. The request type is always added to the end of the function call. URL Parameter's and and XML object variables are automatically matched with data read from WADL XML.
```
connection.[Resource]_[Request Type](urlParameter = value, xmlDataObjectParameter = value)
```