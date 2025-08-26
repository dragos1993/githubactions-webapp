#Label green pods with a shared label
kubectl label pods -l app=argocd-web-app-green app=argocd-web-app-active --overwrite

#Patch the Service to use the shared label
kubectl patch service argocd-web-app-service-blue -n default \
  --type='merge' \
  -p '{"spec": {"selector": {"app": "argocd-web-app-active"}}}'

#Remove the shared label from blue pods
kubectl label pods -l app=argocd-web-app-blue app-