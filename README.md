# web-db-proto
Escenario experimental para nuevas adopciones

## Instrucciones
```
oc login https://master.scjocp3-a9fc.open.redhat.com:443 --token=nwDc3rbn95eXEIWf9kbMcC2enncBiU3rAIXgLfdQErE
oc project web-form-demo
oc new-app --help
oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete
oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java
oc status
oc get pods
oc logs -f gs-accessing-data-mysql-1-build
oc status
oc get pods
oc logs -f gs-accessing-data-mysql-1-mzlgs
oc new-app --search --template=mysql
oc delete --all dc,bc,po,svc,secret,pvc
oc status
oc new-app mysql-persistent -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=admin
oc delete --all dc,bc,po,svc,secret,pvc
oc new-app mysql-persistent -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=admin
oc get pods
oc logs -f mysql-1-t6jpw
oc rhs mysql-1-t6jpw
vim application.properties
oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java
oc create configmap db-config --from-file=application.properties
oc set volume dc/gs-accessing-data-mysql --add --mount-path=/deployments/config --type=configmap --configmap-name=db-config 
oc get pods
oc logs -f gs-accessing-data-mysql-3-9j999
oc rollout latest dc/gs-accessing-data-mysql
oc get pods
oc logs -f gs-accessing-data-mysql-4-hmwsv
oc rsh gs-accessing-data-mysql-4-hmwsv
oc expose service/gs-accessing-data-mysql
oc get route
oc edit configmap db-config
oc rollout latest dc/gs-accessing-data-mysql
oc get pods
oc logs -f gs-accessing-data-mysql-6-9kkp5
oc get service
oc edit configmap db-config
oc rollout latest dc/gs-accessing-data-mysql
oc get pods
oc logs -f gs-accessing-data-mysql-7-wjt4r

curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=First -d email=someemail@someemailprovider.com
curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=jhon -d email=jdoe@someemailprovider.com
curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
oc get pods
oc rsh mysql-1-wwqhs
```
