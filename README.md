# web-db-proto
Escenario experimental para nuevas adopciones

## Referencias
https://github.com/spring-guides/gs-handling-form-submission

https://github.com/spring-guides/gs-accessing-data-mysql

## Lectura

[Cloud Native Architectures: Design high-availability and cost-effective applications for the cloud](https://www.amazon.com/Cloud-Native-Architectures-high-availability-cost-effective-ebook/dp/B0788SDV7W/ref=pd_rhf_se_s_sspa_dk_rhf_search_pt_sub_0_6/140-3921155-8579238?_encoding=UTF8&pd_rd_i=B0788SDV7W&pd_rd_r=89fb40db-359c-4f2e-9c9b-d00e047a3142&pd_rd_w=HgTBm&pd_rd_wg=3sa4D&pf_rd_p=6b99a1a0-3d79-4d28-99ba-822278a5e800&pf_rd_r=X12RMJBHHK37R39X9VJ3&psc=1&refRID=X12RMJBHHK37R39X9VJ3&spLa=ZW5jcnlwdGVkUXVhbGlmaWVyPUExQzhZQVdOUUY0Nk03JmVuY3J5cHRlZElkPUEwNjU2Njc0MldKSzJZTEpZSk02NyZlbmNyeXB0ZWRBZElkPUEwNDAyNDY4MkNWSktVSUhTVTFLRyZ3aWRnZXROYW1lPXNwX3JoZl9zZWFyY2gmYWN0aW9uPWNsaWNrUmVkaXJlY3QmZG9Ob3RMb2dDbGljaz10cnVl)


## Instrucciones

Ten en consideraciones que varias de las instrucciones tienen como intención generar errores para luego ser resueltos, con el fin de entender el por qué y sus posibles soluciones.

```
#  Login mediante token y/o usuario y contraseña
1  oc login https://master.scjocp3-a9fc.open.redhat.com:443 [--token=nwDc3rbn95eXEIWf9kbMcC2enncBiU3rAIXgLfdQErE]

#  Selección de proyecto
2  oc project web-form-demo

#  Limpieza de recursos
3  oc delete --all dc,bc,po,svc,secret,pvc,route,configmap

#  Creación de aplicaciones
4  oc new-app --help
5  oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete
6  oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java
7  oc status

#  Revisión de logs
8  oc get pods
9  oc logs -f gs-accessing-data-mysql-1-build
10 oc status
11 oc get pods
12 oc logs -f gs-accessing-data-mysql-1-mzlgs

# Busqueda de aplicación/template y parametros de entrada
13 oc new-app --search --template=mysql
14 oc get template mysql-persistent -n openshift -o yaml
15 oc delete --all dc,bc,po,svc,secret,pvc,route,configmap
16 oc status

# Creación de Base de Datos
17 oc new-app mysql-persistent -e MYSQL_USER=admin -e MYSQL_PASSWORD=admin -e MYSQL_DATABASE=sample
18 oc get pods
19 oc logs -f mysql-1-t6jpw
20 oc rsh mysql-1-t6jpw

# Re creación de aplicación
21 oc new-app https://github.com/spring-guides/gs-accessing-data-mysql.git --context-dir=complete --image=openshift/java

# Creación y manejo de configuraciones
22 vim application.properties
23 cat application.properties
spring.jpa.hibernate.ddl-auto=update
spring.datasource.url=jdbc:mysql://127.0.0.1:3306/sample
spring.datasource.username=admin
spring.datasource.password=admin
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
24 oc create configmap db-config --from-file=application.properties
25 oc set volume dc/gs-accessing-data-mysql --add --mount-path=/deployments/config --type=configmap --configmap-name=db-config

# Verificación del funcionamiento
26 oc get pods
27 oc logs -f gs-accessing-data-mysql-3-9j999
28 oc rollout latest dc/gs-accessing-data-mysql
29 oc get pods
30 oc logs -f gs-accessing-data-mysql-4-hmwsv
31 oc rsh gs-accessing-data-mysql-4-hmwsv

# Acceso al servicio
32 oc expose service/gs-accessing-data-mysql
33 oc get route
34 oc edit configmap db-config
35 oc rollout latest dc/gs-accessing-data-mysql
36 oc get pods
37 oc logs -f gs-accessing-data-mysql-6-9kkp5
38 oc get service
39 oc edit configmap db-config
40 oc rollout latest dc/gs-accessing-data-mysql
41 oc get pods
42 oc logs -f gs-accessing-data-mysql-7-wjt4r

# Pruebas funcionales
43 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=First -d email=someemail@someemailprovider.com
44 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
45 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/add -d name=jhon -d email=jdoe@someemailprovider.com
46 curl http://gs-accessing-data-mysql-web-form-demo.apps.scjocp3-a9fc.open.redhat.com/demo/all
47 oc get pods
48 oc rsh mysql-1-wwqhs
```
