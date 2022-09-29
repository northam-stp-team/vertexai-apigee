# Apigee
Sample Apigee proxies for Translation service in Vertex AI integration

Consists of following Apigee proxies:
1. Translation

This proxy uses Service account that has permission to access Vertex AI endpoint.

## Deployment
The following steps rely on a [maven plugin for Apigee](https://github.com/apigee/apigee-deploy-maven-plugin/tree/hybrid). If you do not wish to use maven or the plugin, you can deploy it [manually](https://cloud.google.com/apigee/docs/api-platform/fundamentals/download-api-proxies#upload).

### Pre-requisites
* Access to an [Apigee X](htwtps://cloud.google.com/apigee/docs/api-platform/get-started/what-apigee) instance
* All the pre-requisites required for the [apigee maven plugin](https://github.com/apigee/apigee-deploy-maven-plugin/tree/hybrid)
* The URL of the Vertex AI endpoint that serves as the backend
  * this URL should have been created as part of the [backend deployment](../backend)

### Deployment Steps
1. Define variables
```
# define vars
PROJECT_ID=<project-id>
VERTEXAI_TRANSLATION_URL=<https://translation-endpoint-url>
export APIGEE_ORG=<apigee-org>
export APIGEE_ENV=<apigee-env>
export SERVICE_ACCOUNT_ID=<service-acc-email-id>

# validate vars are set
echo $PROJECT_ID
echo $APIGEE_ORG
echo $APIGEE_ENV

```

2. Update configuration with dynamic values
```
sed -i s,{VERTEXAI_TRANSLATION_URL},$VERTEXAI_TRANSLATION_URL,g ./apigee/apiproxy/targets/default.xml
```

3. Setup `gcloud`
```
# login with gcloud
gcloud auth login

# set project
gcloud config set project ${PROJECT_ID}
```

4. `cd` into each API proxy folder and deploy via mvn command
```
cd apigee
mvn clean install -Peval -Dbearer=$(gcloud auth print-access-token) -DgoogleTokenEmail=${SERVICE_ACCOUNT_ID}@${PROJECT_ID}.iam.gserviceaccount.com

```
