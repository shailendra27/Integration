# Troubleshooting

This page intends to capture any issues that you might face while going through the exercises that are part of the CodeJam. 

## Cloud Integration

- #### Why am I unable to edit the integration flow?
    This is because our integration flow is not in edit mode. To switch to edit mode, click the `Edit button` (*upper right corner*).

- #### An internal server error occurred: End of input at line 1 column 1 path $.
    No body was sent in the request. Remember that our integration flow expects a JSON payload. See [request payload sample](exercises/03-build-first-integration-flow/assets/request-payload-sample.json).

- #### There is no HTTP endpoint URL on the deployed content page.
    In case you don't see the HTTP endpoint URL immediately on the deployed content page, it takes a couple of seconds before it is reflected in the UI. Refresh the web page a couple of times and it will then be displayed.

- #### HTTP 401 Unauthorized error when sending requests to the integration flow
    1. Ensure that you are including authorization details in your request. In our case, that would be a Bearer token in the Authorization HTTP header.
    2. If the Authorization header is set, the Bearer token may have expired. Refresh the token by sending a request to the token URL (In Postman collection - `cloud-integration > POST Token`) and then retry sending the request to the integration flow.

- #### HTTP 403 Forbidden error message when posting a message to SAP Cloud Integration
    It's a 403, not a 401... meaning that you are authenticating well to the service but the user you are using for communication doesn't have the right roles assigned to it. Make sure that the user has the ESBMessagingSend.send role in the BTP Cockpit. See the roles set up for the instance in the [prerequisites - Create SAP Cloud Integration runtime client credentials](prerequisites.md#create-sap-cloud-integration-runtime-client-credentials).

- #### HTTP 500 Internal Server error - PKIX path building failed. Unable to find valid certification path to requested target.
    The certificate presented by the service you are communicating with is unknown to your Cloud Integration tenant. You need to import the certificate presented by the service in your Cloud Integration tenant.

    You might face this error when trying to communicate with the services part of this CodeJam. The services are hosted in a Kyma environment and Cloud Integration is missing the certificate root chain presented by the service hosted in Kyma. 
    
    👉 Go to `Monitor > Manage Security - Keystore tile` and `Add` a certificate. Import the [kyma-ondemand-com-chain.pem](assets/kyma-ondemand-com-chain.pem) certificate included in the assets folder and `Confirm` you want to add it.

    1. Add certificate
    ![Manage Keystore](assets/manage-keystore.png)

    2. Browse for certificate
    ![Add certificate](assets/add-certificate-name.png)

    3. Confirm certificate
    ![Confirm certificate](assets/confirm-certificate.png)




- 

## Postman

TBA