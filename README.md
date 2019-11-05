# web-db-proto
Escenario experimental para nuevas adopciones

## Instrucciones
```
1 oc login https://master.scjocp3-a9fc.open.redhat.com:443 --token=nwDc3rbn95eXEIWf9kbMcC2enncBiU3rAIXgLfdQErE
2 oc project web-form-demo
3 oc new-app --help
4 oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete
5 oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java
6 oc status
7 oc get pods
8 oc logs -f gs-accessing-data-mysql-1-build
9 oc status
10 oc get pods
11 oc logs -f gs-accessing-data-mysql-1-mzlgs
12 oc new-app --search --template=mysql
13 oc delete --all dc,bc,po,svc,secret,pvc
14 oc status
15 oc new-app mysql-persistent -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=admin
16 oc delete --all dc,bc,po,svc,secret,pvc
17 oc new-app mysql-persistent -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DATABASE=sample -e MYSQL_ROOT_PASSWORD=admin
18 oc get pods
19 oc logs -f mysql-1-t6jpw
20 oc rhs mysql-1-t6jpw
21 vim application.properties
22 oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java
23 oc create configmap db-config --from-file=application.properties
24 oc set volume dc/gs-accessing-data-mysql --add --mount-path=/deployments/config --type=configmap --configmap-name=db-config
25 oc get pods
26 oc logs -f gs-accessing-data-mysql-3-9j999
27 oc rollout latest dc/gs-accessing-data-mysql
28 oc get pods
29 oc logs -f gs-accessing-data-mysql-4-hmwsv
30 oc rsh gs-accessing-data-mysql-4-hmwsv
31 oc expose service/gs-accessing-data-mysql
32 oc get route
33 oc edit configmap db-config
34 oc rollout latest dc/gs-accessing-data-mysql
35 oc get pods
36 oc logs -f gs-accessing-data-mysql-6-9kkp5
37 oc get service
38 oc edit configmap db-config
39 oc rollout latest dc/gs-accessing-data-mysql
40 oc get pods
41 oc logs -f gs-accessing-data-mysql-7-wjt4r
42 
43 
44 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=First -d email=someemail@someemailprovider.com
45 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
46 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=jhon -d email=jdoe@someemailprovider.com
47 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
48 oc get pods
49 oc rsh mysql-1-wwqhs
```
