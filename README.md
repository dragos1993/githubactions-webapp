Is a Hellow world Web App, which is deployed via GitHub Action. And was tested it the bllue-green Deployment Strategy

#Label green pods with a shared label
kubectl label pods -l app=argocd-web-app-green app=argocd-web-app-active --overwrite

#Patch the Service to use the shared label
kubectl patch service argocd-web-app-service-blue -n default \
  --type='merge' \
  -p '{"spec": {"selector": {"app": "argocd-web-app-active"}}}'

#Remove the shared label from blue pods
kubectl label pods -l app=argocd-web-app-blue app-

#delete ingress green
kubectl delete ingress ingress-ssl-green

#delete svc green
kubectl delete svc argocd-web-app-service-green

#delete the deploy of blue
kubectl delete deploy argocd-web-app-deployment-blue

#kubectl edit deploy argocd-web-app-deployment-green
A copy of your changes has been stored to "/tmp/kubectl-edit-1006304040.yaml"
error: At least one of apiVersion, kind and name was changed
vrinc@Vrinceanu:~/master/test/top2/githubactions-webapp$ kubectl apply -f /tmp/kubectl-edit-1006304040.yaml
deployment.apps/argocd-web-app-deployment-blue created

#delete the old deploy name
kubectl delete deployment.apps/argocd-web-app-deployment-green
