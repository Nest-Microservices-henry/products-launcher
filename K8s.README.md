Helm commands

Create configuration: helm create <name>
Apply initial configuration: helm install <name> . (shop)
Apply updates: helm upgrade <name> .

K8s commands

Get pods, deployments, and services: kubectl get <pods | deployments | services>

Review all pods: kubectl describe pods

Review a pod: kubectl describe pod <name>

Delete pod: kubectl delete pod <name>

Review logs: kubectl logs <name>

Create deployment:

kubectl create deployment <name> --image=<registry/url/image> --dry-run=client -o yaml > deployment.yml

Create service:

kubectl create service clusterip <name> --tcp=<8888> --dry-run=client -o yaml > service.yml 
kubectl create service nodeport <name> --tcp=<3000> --dry-run=client -o yaml > service.yml

ClusterIP: can only be accessed from within the cluster.
NodePort: can be accessed from outside the cluster.

Secrets

Create secrets, either multiple at once or one by one:

kubectl create secret generic <name> --from-literal=key=value

kubectl create secret generic secret1 --from-literal=key1=value1 --from-literal=key2=value2

Get secrets: kubectl get secrets

View the content of a secret: kubectl get secrets <name> -o yaml

Edit a secret:

-The easiest way is to delete it and recreate it, but if it's more than one secret, we won't want to lose the others. Remember that secrets are in base64, so if we want to edit a secret, we must do it in base64.

-Edit the secret with kubectl edit secret <name>, this will invoke the editor.

-Change the value (you can use an online editor to convert to base64).

-Press i to insert lines and edit the file.


-Put the value to decode on a new line.

-Press esc and then :. ! base64 -D to decode the value.

-Press i to insert or edit the value.

-Press esc and then :. ! base64 to encode the value.

-Edit the file again i and leave the line in its position.

-Press esc and then :wq to save and exit.

-Configure Google Cloud secrets to obtain images

Create secret:

kubectl create secret docker-registry gcr-json-key --docker-server=GOOGLE-SERVER-docker.pkg.dev --docker-username=_json_key --docker-password="$(cat 'PATH/TO/Microservices IAM.json')" --docker-email=YOUR_EMAIL@gmail.com


Path of the secret to use the key:

kubectl patch serviceaccounts default -p '{ "imagePullSecrets": [{ "name":"gcr-json-key" }] }'


Export and apply configurations with files (secrets in this case)

To export the configuration files:

kubectl get secret <name> -o yaml > <name>.yml


Apply the configuration based on the file:


kubectl create -f <name>.yml