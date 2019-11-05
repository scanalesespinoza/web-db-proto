# web-db-proto
Escenario experimental para nuevas adopciones

## Referencias
https://github.com/spring-guides/gs-handling-form-submission

https://github.com/spring-guides/gs-accessing-data-mysql

## Lectura

[Cloud Native Architectures: Design high-availability and cost-effective applications for the cloud](https://www.amazon.com/Cloud-Native-Architectures-high-availability-cost-effective-ebook/dp/B0788SDV7W/ref=pd_rhf_se_s_sspa_dk_rhf_search_pt_sub_0_6/140-3921155-8579238?_encoding=UTF8&pd_rd_i=B0788SDV7W&pd_rd_r=89fb40db-359c-4f2e-9c9b-d00e047a3142&pd_rd_w=HgTBm&pd_rd_wg=3sa4D&pf_rd_p=6b99a1a0-3d79-4d28-99ba-822278a5e800&pf_rd_r=X12RMJBHHK37R39X9VJ3&psc=1&refRID=X12RMJBHHK37R39X9VJ3&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExQzhZQVdOUUY0Nk03JmVuY3J5cHRlZElkPUEwNjU2Njc0MldKSzJZTEpZSk02NyZlbmNyeXB0ZWRBZElkPUEwNDAyNDY4MkNWSktVSUhTVTFLRyZ3aWRnZXROYW1lPXNwX3JoZl9zZWFyY2gmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)


## Instrucciones
```
1 oc login https://master.scjocp3-a9fc.open.redhat.com:443 --token=nwDc3rbn95eXEIWf9kbMcC2enncBiU3rAIXgLfdQErE
2 oc project web-form-demo
  oc delete --all dc,bc,po,svc,secret,pvc,route
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
20 oc rsh mysql-1-t6jpw
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
