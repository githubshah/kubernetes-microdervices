docker run --name nginx100 -v $PWD/content:/usr/share/nginx/html -d nginx
// MUST use SNAPSHOT while creating iimage

// create exchange image and conversion image.

docker build -t shaid/ce3:0.0.121-SNAPSHOT .                                        (create image)
docker image ls                                                                     (check imgae created or not)

shaid/ce3:0.0.121-SNAPSHOT                                                           (image name looks like this)

// creat deployment for both above images

kubectl create deployment ce3 --image=shaid/ce3:0.0.121-SNAPSHOT                               (create deployment)
 
kubectl expose deployment ce3 --type=LoadBalancer --port=8000                                  (expose deployment)

// check external_ip should be not null and ready shuold be not zero

kubectl get all                                                                      

#kubectl get events --logs pod/ce2-5955df974c-tvt8r

#kubectl scale deployment ce1 --replicas=3

#kubectl rollout restart deployment/ce2

kubectl get deployment cc3 -o yaml                                                         (Check deployment configuration)
kubectl get service cc3_service -o yaml

kubectl get deployment cc3 -o yaml > cc3.yaml                                          (deployment config output to a file)
kubectl get service cc3 -o yaml > cc3_service.yaml                                        (service config output to a file) 


// always create new ymal file for deployment update to avoid conflicts 
// use env properties from cc1.yaml file to new cc3.ymal file you create above 
// optional merge service yaml file into deployment yaml file and saparated with three hyphon ---

kubectl diff -f cc3.yaml                                                                      (diff in ymal exising vs new)
kubectl apply -f cc3.yaml   (only this cmd will create deployment)                            (apply ymal changes in deployment)

#kubectl delete all -l app=<service name>

kubectl logs -f pod/cc3-76bc97985b-gvchp                                                            (view pod logs)

kubectl create configmap cc3 --from-literal=CURRENCY_EXCHANGE_SERVICE_HOST=http://cc3               (create common env config)

kubectl describe deployment                                                                         (view deployment ymal config)

kubectl exec cc3-7b49f4ccc-sxdgs -- printenv                                (view all deployment ENV)





http://localhost:8100/currency-conversion-feign/from/USD/to/INR/quantity/10
http://localhost:8000/currency-exchange/from/USD/to/INR
