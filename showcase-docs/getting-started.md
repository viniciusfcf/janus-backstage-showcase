# Getting Started running Backstage Showcase

There are several different methods for running the Backstage Showcase app today. We currently have support for running the application locally, using a helm chart to deploy to a cluster, and manifests for deployment using ArgoCD.

## Running Locally with a basic configuration

The easiest and fastest method for getting started: Backstage Showcase app, running it locally only requires a few simple steps.

1. Copy `app-config.example.yaml` and rename it as `app-config.local.yaml`.

## Running Locally with the Optional Plugins

1. Create an `app-config.local.yaml` file that will be used for storing the environment variables that the showcase app needs

2. Copy the required code snippet from `app-config.yaml` into `app-config.local.yaml`. Note: Each plugin has a `# Plugin: <PLUGIN_NAME>` comment above the required code snippet(s).

   - Enable plugins (All plugins have a default of `false`)

     - `${K8S_ENABLED}`: Set to `true` to enable the Kubernetes backend plugin.
     - `${TECHDOCS_ENABLED}` Set to `true` to enable the Techdocs backend plugin.
     - `${ARGOCD_ENABLED}` Set to `true` to enable the ArgoCD backend plugin.
     - `${SONARQUBE_ENABLED}` Set to `true` to enable the SonarQube backend plugin.
     - `${KEYCLOAK_ENABLED}` Set to `true` to enable the Keycloak backend plugin.
     - `${OCM_ENABLED}` Set to `true` to enable the OCM backend plugin.
     - `${GITHUB_ENABLED}` Set to `true` to enable the GitHub Entity backend plugin.
     - `${GITHUB_ORG_ENABLED}` Set to `true` to enable the GitHub Org Entity backend plugin.
     - `${GITLAB_ENABLED}` Set to `true` to enable the GitLab Entity backend plugin.
     - `${AZURE_ENABLED}` Set to `true` to enable the Azure DevOps Entity backend plugin.
     - `${JENKINS_ENABLED}` Set to `true` to enable the Jenkins Entity backend plugin.

   - Setup the GitHub plugins (GitHub Issues and GitHub Pull Request)

     - This [URL](https://backstage.io/docs/integrations/github/github-apps) can be used to quickly create a GitHub app, you can name the yaml file `github-app-backstage-showcase-credentials.local.yaml`
     - `${GITHUB_APP_CLIENT_ID}`: client id
     - `${GITHUB_APP_CLIENT_SECRET}`: client secret

   - Setup the GitLab plugin

     - This [URL](https://docs.gitlab.com/ee/user/profile/personal_access_tokens.html) can be used to quickly create a GitLab personal access token
     - `${GITLAB_TOKEN}`: personal access token

   - Setup the Azure DevOps plugin

     - This [URL](https://learn.microsoft.com/en-us/azure/devops/organizations/accounts/use-personal-access-tokens-to-authenticate?view=azure-devops&tabs=Windows) can be used to quickly create an Azure personal access token
     - `${AZURE_TOKEN}`: personal access token
     - `${AZURE_ORG}`: Azure DevOps Services (cloud) Organization name or the Azure DevOps Server

   - Setup the Jira plugin

     - This [URL](https://github.com/RoadieHQ/roadie-backstage-plugins/tree/main/plugins/frontend/backstage-plugin-jira#how-to-use-jira-plugin-in-backstage) explains how to use the Jira plugin
     - `${JIRA_URL}`: URL for the Jira instance
     - `${JIRA_TOKEN}`: API token
     - `${JIRA_USER_AGENT}`: User-Agent (UA) string (Any dummy string without whitespace works because Jira APIs reject browser origin requests)

   - Setup the Jfrog Artifactory plugin

     - This [URL](https://github.com/janus-idp/backstage-plugins/tree/main/plugins/jfrog-artifactory#getting-started) explains how to use the Jfrog Artifactory plugin
     - `${ARTIFACTORY_URL}`: URL for the Jfrog Artifactory instance
     - `${ARTIFACTORY_TOKEN}`: API token
     - `${ARTIFACTORY_SECURE}`: Change to `false` in case of using self hosted artifactory instance with a self-signed certificate

   - Setup the ArgoCD instances(s)

     - If using a shared username and password across the instances, you can define them in the username and password variables and arbitrarily assign the urls and tokens
     - If using tokens for each individual instance, you can assign arbitrary variables to the tokens
     - `${ARGOCD_USERNAME}` Username for the instance(s)
     - `${ARGOCD_PASSWORD}` Password for the instance(s)
     - `${ARGOCD_INSTANCE1_URL}`: URL to the instance
     - `${ARGOCD_AUTH_TOKEN}`: token to the instance
     - `${ARGOCD_INSTANCE2_URL}`: URL to the instance
     - `${ARGOCD_AUTH_TOKEN2}`: token to the instance

   - Setup the Keycloak instance(s)

     - `${KEYCLOAK_BASE_URL}`: base URL of the Keycloak instance
     - `${KEYCLOAK_LOGIN_REALM}`: login realm
     - `${KEYCLOAK_REALM}`: realm
     - `${KEYCLOAK_CLIENT_ID}`: client id
     - `${KEYCLOAK_CLIENT_SECRET}`: client secret

   - Setup the kubernetes cluster plugin

     - `${K8S_CLUSTER_NAME}`: cluster name
     - `${K8S_CLUSTER_URL}`: cluster url
     - `${K8S_CLUSTER_TOKEN}`: cluster token

   - Setup the Open Cluster Management plugin

     - `${OCM_HUB_NAME}`: hub cluster name
     - `${OCM_HUB_URL}`: hub cluster url
     - `${moc_infra_token}`: hub token

   - Setup the SonarQube instance

     - `${SONARQUBE_URL}` the url at which sonarqube can be found. Mandatory if plugin is enabled
     - `${SONARQUBE_TOKEN}` a sonarqube [token](https://docs.sonarqube.org/9.8/user-guide/user-account/generating-and-using-tokens/) with enough permission to read all the SonaQube projects. Mandatory if plugin is enabled

   - Setup the Techdocs plugin with an external S3 bucket storage

     - `${TECHDOCS_BUILDER_TYPE}` Set to 'local' for simple setup, or 'external' to use a pipeline
     - `${TECHDOCS_GENERATOR_TYPE}` Set to 'local' for most of the use cases. You can use also 'docker'
     - `${TECHDOCS_PUBLISHER_TYPE}` Set to 'local' for simple setup, or 'awsS3' to use a S3 storage. 'googleGcs' is not supported at the moment.
     - `${BUCKET_NAME}` the bucket name
     - `${BUCKET_REGION_VAULT}` the bucket region
     - `${BUCKET_URL}` the bucket url
     - `${AWS_ACCESS_KEY_ID}` the AWS credentials Key Id
     - `${AWS_SECRET_ACCESS_KEY}` the AWS credentials Access Key

   - Setup a Jenkins instance and then pass the following environment variables to backstage:

     - `${JENKINS_URL}` with the URL where your Jenkins instance can be accessed
     - `${JENKINS_USERNAME}` with the name of the user to be accessed through the API
     - `${JENKINS_TOKEN}` with the API token to be used for the given user

   - Setup the Segment plugin

     - `${SEGMENT_WRITE_KEY}`: Segment write key
     - `${SEGMENT_MASK_IP}`: prevents IP addresses to be sent if true
     - `${SEGMENT_TEST_MODE}`: prevents data from being sent if true

   - Setup the Bitbucket Server Instance

     - `${BITBUCKET_SERVER_HOST}`: The host of the bitbucket Server Instance. e.g. `bitbucket.mycompany.com`
     - `${BITBUCKET_API_BASE_URL}`: The URL of the Bitbucket Server API. For self-hosted installations, it is commonly at `https://<host>/rest/api/1.0`
     - `${BITBUCKET_SERVER_USERNAME}`: Basic Auth Username for Bitbucket Server
     - `${BITBUCKET_SERVER_PASSWORD}`: Basic Auth Password for Bitbucket Server. A [token](https://confluence.atlassian.com/bitbucketserver/personal-access-tokens-939515499.html) can be used in place of the password.

   - Setup the PagerDuty plugin

     - `${PAGERDUTY_TOKEN}` with the [API token](https://support.pagerduty.com/docs/api-access-keys#generating-a-general-access-rest-api-key) used to make requests to the [PagerDuty API](https://developer.pagerduty.com/docs/rest-api-v2/rest-api/). Note that this will require a PaperDuty Admin role.
     - To integrate with a PagerDuty Service, you will need to annotate the appropriate entity with the [PagerDuty Integration key](https://github.com/backstage/backstage/tree/master/plugins/pagerduty#integrating-with-a-pagerduty-service) in its `.yaml` configuration file:

     ```yaml
     annotations:
       pagerduty.com/integration-key: [INTEGRATION_KEY]
     ```

     - Alternatively, you can integrate with the [PagerDuty ServiceID](https://github.com/backstage/backstage/tree/master/plugins/pagerduty#annotating-with-service-id) instead of the integration key:

     ```yaml
     annotations:
       pagerduty.com/service-id: [SERVICE_ID]
     ```

   - Setup the Lighthouse plugin

     - `${LIGHTHOUSE_BASEURL}`: Base URL for the `lighthouse-audit-service` instance
     - To integrate the Lighthouse plugin into the catalog so that the Lighthouse audit info for a component can be displayed in that component's entity page, it is necessary to annotate the entity as shown below.
     - Please note that it is **essential** to include the `https://` or `http::/` in front of the link for this plugin to function correctly.

     ```yaml
     apiVersion: backstage.io/v1alpha1
     kind: Component
     metadata:
       # ...
       annotations:
         lighthouse.com/website-url: # A single website url e.g. https://backstage.io/
     ```

     - Also please note that ending the website url with a `/` will cause it to be treated as a separate link compared to the same url without the `/`.
       - i.e. `https://backstage.io/` and `https://backstage.io` are not considered the same, therefore audits for each will be grouped separately.

3. Run `yarn install` to install the dependencies

4. Start the application using `yarn start`

5. Navigate to <http://localhost:3000>

## Running with Helm

COMING SOON

## Deploying with ArgoCD

COMING SOON
