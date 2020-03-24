## Prerequisites

1. An already setup OpenShift cluster

2. Three NFS shares for storage. For a step by step guide on how to install NFS server refer here. [CentOS](https://www.server-world.info/en/note?os=CentOS_7&p=nfs&f=1), [Ubuntu](https://www.server-world.info/en/note?os=Ubuntu_18.04&p=nfs&f=1)

## APIM Server Deployment

1. Create an OpenShift project name `wso2`.

	`oc new-project wso2`

2. Add your subscription details

	`oc create secret docker-registry wso2-image-pull-secret --docker-server=docker.wso2.com --docker-username=<SUBSCRIPTION_USERNAME> --docker-password=<SUBSCRIPTION_PASSWORD>`

3. Deploy WSO2 APIM Server. Use the correct Template.yaml from the respective pattern directory .  Refer more about APIM deployment patterns 

	`oc process -f Template.yaml -p NFS_SERVER_IP=<NFS_SERVER_IP> -p NFS_SHARE_DATABASE=<DATABASE_NFS_SHARE_PATH> -p NFS_SHARE_SYNAPSE=<SYNAPSE_NFS_SHARE_PATH> -p NFS_SHARE_EXECUTION_PLANS=<EXECUTION_PLANS_SHARE_PATH> -p OPENSHIFT_BASE_DOMAIN=<OPENSHIFT_URL> | oc create -f -`

4. Access product management consoles. Obtain the (HOST/PORT) of the route resource

	`oc get route`
	
Try navigating to `https://<HOST/PORT>/carbon`, `https://<HOST/PORT>/publisher` and `https://<HOST/PORT>/devportal` from your favorite browser.
