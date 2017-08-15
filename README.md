# Description
Provided sample scripts and these instructions will help you to script Web services registration process with Axway API Gateway. These scripts are based on a sample script located under API Gateway installation directory:
```
   <INSTALL_root>/apigateway/samples/scripts/ws/registerWebService.py
```
## API Management Version Compatibilty
This artefact was successfully tested for the following versions:
- V7.5.3

## Install

```
• Place two scripts from the "scripts" folder into the same directory on a server where you run Axway API Management
• Modify scripts as described in the Usage section
• Run upsertWebService.py as described in the Usage section
```

## Usage

* The _upsertWebService.py_ script will register a new Web service (and create a new Web services group if it doesn't exist) or update an existing Web service in a target Gateway.
* The _upsertWebService.py_ script will need to be modified per your environment. These are the values that should be modified to match your environemnt:
  * ___wsdlURL___ – a WSDL URL. This value is hard coded in the current version of the script and should be changed. You may replace it with a variable. The value can be passed as a command line argument.
  * ___listenerGroup___ – it is set to the “Default Services” listener. You may need to change it if you want to use a different listener.
  * ___username___ – a user name for a WSLD protected with HTTP Basic AuthN
  * ___password___ - a password for a WSLD protected with HTTP Basic AuthN
    * _Note_: if a Web service WSDL URL is not protected, then you need to modify the invocation of the retrieveDocument method by removing “username” and “password” parameters:
```
      r = wsg.retrieveDocument(wsdlURL)
```

* Switch to a directory where you've downloaded the scripts.
* Invoke the _upsertWebService.py_ script:
```
   <INSTALL_ROOT>/apigateway/posix/bin/jython upsertWebService.py [OPTIONS]
```   
  * [OPTIONS] (You can add, modify or remove the command line arguments as needed in the _common.py_ file):
    * ___-g___, ___--group___ – this is a gateway group, the default value is “Group1"
    * ___-n___, ___--service___, a gateway instance name, the default value is "APIServer1"
    * ___-u___, ___--username___ – Admin Node Manager user ID, the default value is "user"
    * ___-p___, ___--password___ - password for the Admin Node Manager user, the default value is "password"
    * ___-d___, ___--url___ - Admin Node Manager URL, the default value is "https://localhost:8090/api"
    * ___-w___, ___--wsgroup___ – a Web services group name, the default value is "wsgroup"
 
  This is an example of the script invocation:
```  
  /opt/Axway/APIM-7.5.3/apigateway/posix/bin/jython upsertWebService.py --group DevG1 --service DevI1 --username admin --password changeme --url https://www.mygateway.com:8090/api --wsgroup MathServices
```  
* Once a service is registered, you can develop and apply custom policies for this service using Policy Studio. Consecutive updates to this service using the _upsertWebService.py_ script can be done without touching Policy Studio and redeploying a Gateway configuration.
 
* The "example" folder in this repository contains a sample script for registering a public Web service located at:
  
  [http://www.dneonline.com/calculator.asmx?WSDL](http://www.dneonline.com/calculator.asmx?WSDL)
  
  You can run the example script in your DEV environment by providing correct command line arguments.

## Bug and Caveats

To automate Web services registration, you will need to:
1. Replace hardcoded values in the _upsertWebService.py_ script with variables
2. Create a new script (or further modify the _upsertWebService.py_ script) to loop over a list of the Web services and invoking the _upsertWebService.py_ script

## Contributing

Please read [Contributing.md](https://github.com/Axway-API-Management/Common/blob/master/Contributing.md) for details on our code of conduct, and the process for submitting pull requests to us.


## Team

![alt text][Axwaylogo] Axway Team

[Axwaylogo]: https://github.com/Axway-API-Management/Common/blob/master/img/AxwayLogoSmall.png  "Axway logo"


## License
[Apache License 2.0](/LICENSE)
