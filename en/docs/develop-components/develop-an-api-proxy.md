# Develop an API Proxy

An API proxy acts as an intermediary between an existing API and Choreo, intercepting all requests made to the API. It also functions as a managed API, which allows you to apply essential API management features such as security policies and rate limiting.

In this guide, you will:

 - Create an API proxy component to expose an existing API.
 - Deploy the API proxy.
 - Test the API proxy to verify its functionality.
 - Manage the API.
 - Consume the API.
 

## Prerequisites

Before you try out this guide, complete the following:

- If you are signing in to the Choreo Console for the first time, create an organization as follows:

    1. Go to [https://console.choreo.dev/](https://console.choreo.dev/), and sign in using your preferred method.
    2. Enter a unique organization name. For example, `Stark Industries`.
    3. Read and accept the privacy policy and terms of use.
    4. Click **Create**.

    This creates the organization and opens the **Project Home** page of the default project created for you.

## Step 1: Create an API proxy

To create an API proxy, you can either upload an OpenAPI specification or provide an OpenAPI specification URL. In this guide, you will specify a URL to an OpenAPI definition of a sample API.
 
Follow the steps given below:

1. Go to [https://console.choreo.dev/](https://console.choreo.dev/) and sign in. This opens the project home page.
2. If you already have one or more components in your project, click **+ Create**. Otherwise, proceed to the next step.
3. Click the **API Proxy** card under **Create a Component**.
   This opens the **Create an API Proxy** pane, where you can upload an OpenAPI definition or provide the URL of an OpenAPI. In this guide, you will define resources manually. Therefore, click **Skip Source** to proceed.
4. Specify the values given in the following table as API proxy details: 

    |  **Field**    | **Value**                                   |
    |---------------|---------------------------------------------|
    | **Name**      | `HR API`                                    |
    | **Context**   | `abc-hr`                                    |
    | **Version**   | `1.0`                                       |
    | **Target**    | `https://samples.choreoapps.dev/company/hr` |
    |**Access Mode**| **External**                                |

5.  Click **Create**.
   
   This creates the API proxy component and takes you to the **Overview** page. Now you can proceed to define resources for the API proxy.

## Step 2: Define resources for the API proxy

To add a new resource that can retrieve the department ID, follow the steps given below:

1. In the left navigation menu, click **Develop** and then click **Resources**.
2. Select **GET** as the **HTTP Verb** and enter `/department/{departmentId}` as the **URI Pattern**.
3. Click **+** to add the resource.
4. Click to expand the added resource and specify appropriate values for the **Operation ID** and **Description** fields. You can specify the values given in the following table:

    | **Field**        | **Value**                            |
    |------------------|--------------------------------------|
    | **Operation ID** | `findDepartment`                     |
    | **Description**  | `Find a department by Department ID` |

 5. To remove the five default resources that start with `/*`, click the delete icon corresponding to each resource. This marks the resources for deletion.
 6. Click **Save**.

## Step 3: Deploy the API proxy

To deploy the API proxy to the development environment, follow the steps given below:

1. In the left navigation menu, click **Deploy**.

2. In the **Build Area** card, click **Configure & Deploy**. This opens the **Configure & Deploy** pane, where you can provide endpoint details depending on your requirement for specific environments. In this guide, you will proceed with the populated endpoint details.

3. Click **Save & Deploy**. The **Development** card indicates the **Deployment Status** as **Active** when the API proxy is successfully deployed.

Now you are ready to test the API proxy.

## Step 3: Test the API proxy

Choreo allows you to test your API proxy using either the [integrated OpenAPI Console](../testing/test-rest-endpoints-via-the-openapi-console.md) or [cURL](../testing/test-apis-with-curl.md).

In this guide, you will use the OpenAPI Console to test the API proxy. 

Follow the steps given below:

!!! tip
          Choreo enables OAuth 2.0 to secure APIs by default. Therefore, you need an access token to invoke an API.

           - Choreo automatically generates a key to test the API via the OpenAPI Console. To view the key, click the show key icon in the **Security Header** field.
           - Choreo allows you to disable security for an entire API or a specific API resource for testing purposes. If you want to disable security, follow these steps:
             1. In the left navigation menu, click **Deploy**.
             2. Go to the **Build Area** card and click **Security Settings**.
             3. In the **Security Settings** pane, perform one of the following actions depending on your requirement:
                 - To disable security for the entire API, clear the **OAuth2** checkbox.
                 - To disable security for a specific API resource, go to the **Permissions** section, click to expand the relevant resource and then turn off the **Security** toggle.
             4. Click **Apply**.

1. In the left navigation menu, click **Test** and then click **OpenAPI Console**.

2. Select **Development** from the environment drop-down list.
   
3. Expand the `GET /department/{departmentId}` resource and click **Try it Out** to test it.

4. Enter `1` as the **departmentId** and click **Execute**. You will see a response similar to the following:

    ![API proxy response](../assets/img/develop-components/develop-a-rest-api-proxy/rest-api-proxy-response.png){.cInlineImage-full}

   This indicates that your API proxy is working as expected.

## Step 4: Manage the API proxy

Now that you have a tested API proxy, you can publish it and make it available for application developers to consume. Depending on your requirement, you can apply security, throttling, and other settings to the API before you publish it.

In this guide, you will apply rate limiting to the  API and publish it.

### Step 4.1: Apply a rate limiting level to the API proxy

To apply a rate limiting level to the API, follow the steps given below:
 
1. In the left navigation menu, click **Deploy**.
2. Go to the required environment card and click the setting icon corresponding to **API Configuration**.
3. In the **API Configuration** pane that opens, click **Rate Limiting** to expand the section.
4. Select **API Level** as the **Rate Limiting Level**.
5. Specify appropriate values for the **Request Limit** and **Time Unit** fields. In this guide, you can proceed with the default values.
   This applies a rate-limiting policy to the entire API. If necessary, you can also apply rate limits at the operation level. For more information, see [API Rate Limiting](../api-management/api-rate-limiting.md). 
6. Click **Apply**. This applies the rate limiting level to the API proxy and redeploys it. 

### Step 4.2: Publish the API proxy
   
To publish the API proxy to the Choreo Developer Portal, follow the steps given below:

1. In the left navigation menu, click **Lifecycle** under **Manage**. This takes you to the **Lifecycle** page where you can see the different lifecycle stages the API can be in. You can see that the current lifecycle stage is **Created**.
2. Click **Publish**. 
3. In the **Publish API** dialog that opens, click **Confirm** to proceed publishing the API with the specified display name. If you want to change the display name, make the necessary changes and then click **Confirm**. This changes the API lifecycle state to **Published**.

## Step 5: Invoke the API 

To generate credentials for the published API and to invoke it via the Choreo Developer Portal, follow the steps below:

1. To open the published API in the Choreo Developer Portal via the **Lifecycle** page, click **Go to Devportal**. This takes you to the `HR API` in the Choreo Developer Portal.

2. To generate credentials to test the API, follow the steps given below:

    1. In the Developer Portal left navigation menu, click **Production** under **Credentials**.
    2. Click **Generate Credentials**. Choreo generates new tokens and populates the **Consumer Key** and **Consumer Secret** fields.

        !!! tip
             If you want to test the API via an API test tool or through code, click **Generate Access Token** and copy the test token that is displayed. Alternatively, click **cURL** and copy the generated cURL command to use via a cURL client. You do not need to generate an access token if you are testing the API via the **Try Out** capability in the Choreo Developer Portal.
 
3. To invoke a resource via the **Try Out** capability in the Choreo Developer Portal, follow the steps given below:

    1. In the Developer Portal left navigation menu, click **Try Out**.
    2. In the **Endpoint** list, select **Development** as the environment to try out the API.
    3. To generate an access token to try out the API, click **Get Test Key**. This populates the **Access Token** field with a test key.
    4. Expand the `GET /department/{departmentId}` resource and click **Try it out**.
    5. Enter `1` as the **departmentId** and click **Execute**. You will see a response similar to the following:

        ![Try out response](../assets/img/develop-components/develop-a-rest-api-proxy/try-out-response.png){.cInlineImage-full}

Now, you have gained hands-on experience creating, deploying, testing, and publishing an API proxy using Choreo API Manager.

To learn more about the API management capabilities supported by Choreo API Manager, see [API Management](../api-management/lifecycle-management.md).
