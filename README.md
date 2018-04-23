# SCIM Connector
 
 SCIM Connector provides a Ballerina API to access the Rest API of any service that has implemented SCIM2 specification.
 It handles OAuth2.
 
 
 ## Compatibility
 | Ballerina Language Version| SCIM API Version  |
 | :------------------------:| :----------------:|
 | 0.970.0-beta10             | SCIM2.0           |

 ## Getting Started
  1. Refer https://ballerina.io/learn/getting-started/ to download Ballerina and install tools.
  2. To use SCIM endpoint, you need to provide the following:
      - Client Id
      - Client Secret
      - Access Token
      - Refresh Token
      - Refresh Url
     
     *Please note that, providing ClientId, Client Secret, Refresh Token are optional if you are only providing a valid 
      Access Token vise versa.*
      
   3. Create a new Ballerina project by executing the following command.
   
        `<PROJECT_ROOT_DIRECTORY>$ ballerina init`
   	
 4. Import the scim2 package to your Ballerina program as follows.
    
    ```ballerina
    import ballerina/io;
    import wso2/scim2;
    
    endpoint scim2:Client scimEP {
        baseUrl:"https://localhost:9443",
        clientConfig:{
            auth:{
                scheme:"oauth",
                accessToken:"<access_token>",
                clientId:"<client_id>",
                clientSecret:"<client_secret>",
                refreshToken:"<refresh_token>",
                refreshUrl:"<refresh_url>"
            },
            targets:[{url:"https://localhost:9443"}]
        }
    };
    
    string message;
    string userName = "iniesta";
    var response = scimEP -> getUserByUsername(userName);
    match response {
        User usr => message = usr.userName;
        error er => message = er.message;
    }
    io:println(message);
    ```