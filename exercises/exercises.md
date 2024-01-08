# ArgoCD exercises

Note: Keep in mind that ArgoCD synchronises changes from a branch defined inside `targetRevision`. Every participant should create their own target branch to synchronise changes from. Please create a branch from the `k8s-training` branch and give it a unique name/identifier (e.g your name). Moving forward, please make sure you indicate your target branch inside the Application definition where applicable.

## Exercise 1 - Basics


a) Create an ArgoCD-Application-Manifest for the Kubernetes manifests located inside the exercise-1 folder and set its name to `exercise-1-yourName`. Ensure you set the targetRevision to your target branch. The project is `exercise-1`. Set the destination namespace to `exercise-1-yourName`

b) Apply the application to the namespace `argocd` in Argo. (You need to set this value inside the application manifest)  

c) Change the number of replicas in the deployment. Check how Argo handles those changes.  

d) Change the image name in the deployment to something random (an image that does not exist e.g. "silly"). Push the changes to the repository via a new commit. Wait a little, and observe the behaviour of the deployment via the ArgoCD UI.

e) Roll back the changes via the ArgoCD UI. 

## Exercise 2 - Helm

a) Next, you will practise using an ArgoCD application to deploy the K8s-manifests used in the previous example as a Helm Chart. You will find the Helm related setup in the `exercise-2` folder. Create a new ArgoCD-Application-Manifest (`exercise-2-yourName`), set the project value to `exercise-2`. Set the namespace of the application manifest to `argocd`. Set the destination namespace to `exercise-2-yourName`

b) Change the ReplicationCount in the values file and apply the changes via a new Commit. 

## Exercise 3 - App of apps

Change `{YOURNAME}` in the `base-app.yaml` located inside the exercises-3 folder to your name before attempting the next steps.

a) Apply the base-app located inside the `exercise-3` folder as is. Once deployed, have a look at the values of the environment variables of one of the containers inside a microservices pod. What is the value? Can you explain your findings?  

b1) Set the value for the `environmentName` to "dev" inside the base-app. Re-apply the base app to the cluster. Monitor the change inside ArgoCD. Open the Live Manifest of one of the pods and have a look at the environment variables again. What has changed?  

b2) Open the `Parameters` section inside one of the microservices applications. Take a note of the replicaCount. Can you explain where this value originates?   

c) Could you come up with a solution for the following scenario?

The value of the `replicaCount` for "dev" should be changed to:
 - **5** for microservice-1  
 - **1** for microservice-2
 - microservice-3 should maintain the value **3** *independently* of the `environmentName` value. However, the image tag inside the deployment for microservice 3 should be set to `stable-perl` in dev.
