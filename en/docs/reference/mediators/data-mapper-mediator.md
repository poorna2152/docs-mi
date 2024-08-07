# Data Mapper Mediator

The Data Mapper mediator is a data mapping solution that can be integrated
into a mediation sequence. It converts and transforms one data format to
another or changes the structure of the data in a message. The WSO2 MI VSCode extension
provides a graphical mapping configuration and
generates the files required for executing this graphical mapping
configuration through the WSO2 Data Mapper engine.

The Data Mapper component utilizes TypeScript to define the mapping when you use the WSO2 MI VSCode Extension. When you build the Integration project using the WSO2 MI VSCode Extension, the Data Mapper component generates the required configuration files needed by the Data Mapper Engine to execute the mapping. These files are stored in the Governance Registry.

!!! Info
    The Data Mapper mediator is a [content-aware]({{base_path}}/reference/mediators/about-mediators/#classification-of-mediators) mediator.

## Syntax

```xml
<datamapper config="name" inputSchema="string" inputType="string" outputSchema="string" outputType="string"/> 
```

## Configuration

The parameters available for configuring the Data Mapper mediator are as follows.

<table>
<thead>
<tr class="header">
<th>Parameter name</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>Mapping Configuration</strong></td>
<td>The file, which contains the script file that is used to execute the mapping. This file is generated when you build the Integration project using WSO2 MI VSCode extension. It is stored under <b>Governance Registry</b>.</td>
</tr>
<tr class="even">
<td><strong>Input Schema</strong></td>
<td>JSON schema, which represents the input message format. This file is generated when you build the Integration project using WSO2 MI VSCode extension. It is stored under <b>Governance Registry</b>.</td>
</td>
</tr>
<tr class="odd">
<td><strong>Output Schema</strong></td>
<td>JSON schema, which represents the output message format. This file is generated when you build the Integration project using WSO2 MI VSCode extension. It is stored under <b>Governance Registry</b>.</td>
</tr>
<tr class="even">
<td><strong>Input Type</strong></td>
<td>Expected input message type (XML/JSON/CSV).</br>
<div class="admonition note">
<p class="admonition-title">Note</p>
<p>By default, the Input type is selected from the Input Schema if you have not provided. If you want to specify Input type, then you can specify it in WSO2 MI VSCode Extension.</p>
</div>

</td>
</tr>
<tr class="odd">
<td><strong>Output Type</strong></td>
<td>Target output message type (XML/JSON/CSV).</br>
<div class="admonition note">
<p class="admonition-title">Note</p>
<p>By default, the Output type is selected from the Output Schema if you have not provided. If you want to specify Output type, then you can specify it in WSO2 MI VSCode Extension.</p>
</div></td>
</tr>
</tbody>
</table>

## Components of Data Mapper

### Mapping configuration file

The Data Mapper component utilizes TypeScript to define the mapping when you use the WSO2 MI VSCode Extension. When you build the integration project using the WSO2 MI VSCode Extension, the data mapping configuration file is compiled into JavaScript, which is used by the Data Mapper engine to map the elements in the MI runtime.

### Input and output files

You can load the following input/output message formats:

-   **XML:** to load a sample XML file
-   **JSON:** to load a sample JSON file
-   **CSV:** to load a sample CSV file with column names as the first
    record
-   **JSONSCHEMA:** to load a JSON schema

![]({{base_path}}/assets/img/integrate/mediators/119131284/119134796.png) 


As per the provided input/output files, the Typescript interfaces are generated inside the Mapping configuration file. JSON schema files are generated when you build a project using the WSO2 MI VSCode Extension. These files are stored in the CAR file and deployed inside the governance registry. These files are used to validate the input and output messages at runtime.

### Data Mapper operations

The operations that the Data Mapper supports as shown below .

#### Common

- **Constant:** defines String, number, or boolean constant values.

- **Custom Function:** defines custom functions to use in the mapping.

- **Properties:** uses product-specific runtime variables.

- **Global Variable:** instantiates global variables that you can access from anywhere.

- **Compare:** compares two inputs in the mapping.

#### Arithmetic

- **Add:** adds two numbers.

- **Subtract:** subtracts two or more numbers.

- **Multiply:** multiplies two or more numbers.

- **Divide:** divides two numbers.

- **Ceiling:** derives the ceiling value of a number (closest larger integer value).

- **Floor:** derives the floor value of a number (closest lower integer value).

- **Round:** derives the nearest integer value.

- **Set Precision:** formats a number into a specified length.

- **Absolute Value:** derives the absolute value of a rational number.

- **Min:** derives the minimum number from given inputs

- **Max:** derives the maximum number from given inputs

#### Conditional

- **IfElse:** uses a condition and selects one input from given two.

#### Boolean

- **AND:** performs the boolean AND operation on inputs.

- **OR:** performs the boolean OR operation on inputs.

- **NOT:** performs the boolean NOT operation on inputs.

#### Type conversion

- **StringToNumber:** converts a String value to number (“0” -> 0).

- **StringToBoolean:** converts a String value to boolean (“true” -> true).

- **ToString:** converts a number or a boolean value to String.

#### String

- **Concat:** concatenates two or more Strings.

- **Split:** splits a String by a matching String value.

- **Uppercase:** converts a String to uppercase letters.

- **Lowercase:** converts a String to lowercase letters.

- **String Length:** gets the length of the String.

- **StartsWith:** checks whether a String starts with a specific value. (This is not supported in Java 7.)

- **EndsWith:** checks whether String ends with a specific value. (This is not supported in Java 7.)

- **Substring:** extracts a part of the String value.

- **Trim:** removes white spaces from the beginning and end of a String.

- **Replace:** replaces the first occurrence of a target String with another.

- **Match** – check whether the input match with a (JS) Regular Expression

## Examples

### Example 1 - Creating a SOAP payload with namespaces

This example creates a Salesforce login SOAP payload using a JSON
payload. The login payload consists of XML namespaces. Even though the
JSON payload does not contain any namespace information, the output JSON
schema will be generated with XML namespace information using the
provided SOAP payload.

![example one Data mapper diagram]({{base_path}}/assets/img/integrate/mediators/119131284/119131296.png)

The sample input JSON payload is as follows.

``` js
{  
   "name":"Watson",
   "password":"watson@123"
}
```

The sample output XML is as follows.

``` xml
<soapenv:Envelope xmlns:urn="urn:enterprise.soap.sforce.com" xmlns:soapenv="http://www.w3.org/2003/05/soap-envelope/">
  <soapenv:Body>
    <urn:login>
      <urn:username><b>user@domain.com</b></urn:username>
      <urn:password><b>secret</b></urn:password>
    </urn:login>
  </soapenv:Body>
</soapenv:Envelope>
```

### Example 2 - Mapping SOAP header elements

This example demonstrates how to map SOAP header elements along with
SOAP body elements to create a certain SOAP payload, by creating a
Salesforce convertLead SOAP payload using a JSON payload. The Convert
Lead SOAP payload needs mapping SOAP header information.  
E.g. `<urn:sessionId>QwWsHJyTPW.1pd0_jXlNKOSU</urn:sessionId>`

![]({{base_path}}/assets/img/integrate/mediators/119131284/119131295.png)

The sample input JSON payload is as follows.

``` js
{  
   "owner":{  
      "ID":"005D0000000nVYVIA2",
      "name":"Smith",
      "city":"CA",
      "code":"94041",
      "country":"US"
   },
   "lead":{  
      "ID":"00QD000000FP14JMAT",
      "name":"Carl",
      "city":"NC",
      "code":"97788",
      "country":"US"
   },
   "sendNotificationEmail":"true",
   "convertedStatus":"Qualified",
   "doNotCreateOpportunity":"true",
   "opportunityName":"Partner Opportunity",
   "overwriteLeadSource":"true",
   "sessionId":"QwWsHJyTPW.1pd0_jXlNKOSU"
}
```

The sample output XML is as follows.

``` xml
<?xml version="1.0" encoding="utf-8"?>  
<soapenv:Envelope xmlns:urn="urn:enterprise.soap.sforce.com" xmlns:soapenv="http://www.w3.org/2003/05/soap-envelope/">
  <soapenv:Header>
     <urn:SessionHeader>
        <urn:sessionId>QwWsHJyTPW.1pd0_jXlNKOSU</urn:sessionId>
     </urn:SessionHeader>
     </soapenv:Header>
     <soapenv:Body>
     <urn:convertLead >
        <urn:leadConverts> <!-- Zero or more repetitions -->
           <urn:convertedStatus>Qualified</urn:convertedStatus>
           <urn:doNotCreateOpportunity>false</urn:doNotCreateOpportunity>
           <urn:leadId>00QD000000FP14JMAT</urn:leadId>
           <urn:opportunityName>Partner Opportunity</urn:opportunityName>
           <urn:overwriteLeadSource>true</urn:overwriteLeadSource>
           <urn:ownerId>005D0000000nVYVIA2</urn:ownerId>
           <urn:sendNotificationEmail>true</urn:sendNotificationEmail>
        </urn:leadConverts>
     </urn:convertLead>
</soapenv:Body>
</soapenv:Envelope>
```

### Example 3 - Mapping primitive types

This example demonstrates how you can map an XML payload with integer,
boolean etc. values into a JSON payload with required primitive types,
by specifying the required primitive type in the JSON schema.

![]({{base_path}}/assets/img/integrate/mediators/119131284/119131294.png) 

The sample input XML payload is as follows.

``` xml
<?xml version="1.0" encoding="UTF-8" ?>
    <root>
        <name>app_name</name>
        <version>version</version>
        <manifest_version>2</manifest_version>
        <description>description_text</description>
        <container>GOOGLE_DRIVE</container>
        <api_console_project_id>YOUR_APP_ID</api_console_project_id>
        <gdrive_mime_types>
            <opendrivedoc>
                <type>image/png</type>
                <type>image/jpeg</type>
                <type>image/gif</type>
                <type>application/vnd.google.drive.ext-type.png</type>
                <type>application/vnd.google.drive.ext-type.jpg</type>
                <type>application/vnd.google.drive.ext-type.gif</type>
                <href>http://your_web_url/</href>
                <title>Open</title>
                <disposition>window</disposition>
            </opendrivedoc>
        </gdrive_mime_types>
        <icons>
            <icon_128>icon_128.png</icon_128>
        </icons>
        <app>
            <launch>
                <web_url>http://yoursite.com</web_url>
            </launch>
        </app>
    </root>
```

The sample output JSON is as follows.

``` js
{
"name" : "app_name",
"version" : "version",
"manifest_version" : 2,
"description" : "description_text",
"container" : "GOOGLE_DRIVE",
"api_console_project_id" : "YOUR_APP_ID",
"gdrive_mime_types": {
  "opendrivedoc": [
    {
      "type": ["image/png", "image/jpeg", "image/gif", "application/vnd.google.drive.ext-type.png",
      "application/vnd.google.drive.ext-type.jpg","application/vnd.google.drive.ext-type.gif"],
      "href": "http://your_web_url/",
      "title" : "Open",
      "disposition" : "window"
    }
  ]
},
"icons": {
  "icon_128": "icon_128.png"
},
"app" : {
  "launch" : {
  "web_url" : "http://yoursite.com"
  }
}
}
```

### Example 4 - Mapping XML to CSV

This example demonstrates how you can map an XML payload to CSV format.

!!! Info
    If you specify special characters (e.g., `&` ,
    `&amp;)` within the `<text>`
    tag when converting from CSV to CSV , they will be displayed as follows
    by default.
    -   `& -> &amp;`
    -   `&amp; -> &amp;amp;`
    -   `< -> &lt;`
    -   `&lt; -> &lt;lt;`

To avoid this and to display the exact special characters as text in the
returned output, add the following properties in the Synapse
configuration.

``` xml
<property name="messageType" value="text/plain" scope="axis2"/>
<property name="ContentType" value="text/plain" scope="axis2"/>
```

<img src="{{base_path}}/assets/img/integrate/mediators/119131284/example4.gif" alt="Example 4">

The sample input XML payload is as follows.

``` xml
<?xml version="1.0"?>
<PurchaseOrder PurchaseOrderNumber="001">
<Address>
    <Name>James Yee</Name>
    <Street>Downtown Bartow</Street>
    <City>Old Town</City>
    <State>PA</State>
    <Zip>95819</Zip>
    <Country>USA</Country>
</Address>
<Address>
    <Name>Elen Smith</Name>
    <Street>123 Maple Street</Street>
    <City>Mill Valley</City>
    <State>CA</State>
    <Zip>10999</Zip>
    <Country>USA</Country>
</Address>
 <DeliveryNotes>Please leave packages in shed by driveway.</DeliveryNotes>
</PurchaseOrder>
```

The sample output CSV is as follows.

``` text
Name,Street,City,State,Zip,Country
James Yee,Downtown Bartow,Old Town,PA,95819,USA
Ellen Smith,123 Maple Street,Mill Valley,CA,10999,USA
```
