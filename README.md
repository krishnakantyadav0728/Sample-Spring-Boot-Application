# Sample-Spring-Boot-Application

##Step 1: Sample Spring Boot Application

##Create a simple Spring Boot app (or you can clone an existing one). Here’s a minimal example:

#pom.xml (for Maven build)

#cd src/main/java/com/example/demo/DemoApplication.java

#Step 2: Build the JAR

#On your local machine or your build server:

#mvn clean package

#Step 3: Dockerfile

#Create a Dockerfile in the project root:

#Step 4: Build the container image using podman/docker

#podman build -t spring-boot-app:latest .

#Step 5: Push the image to OpenShift internal registry

#podman login -u $(oc whoami) -p $(oc whoami -t) --tls-verify=false default-route-openshift-image-registry.apps.ocp4.imss.co.in

#Tag your image and push:

#podman tag spring-boot-app:latest default-route-openshift-image-registry.apps.ocp4.imss.co.in/test/spring-boot-app:latest

#podman push --tls-verify=false default-route-openshift-image-registry.apps.ocp4.imss.co.in/test/spring-boot-app:latest

#Step 6: Create OpenShift ImageStream

#oc create imagestream spring-boot-app -n test

#oc import-image spring-boot-app:latest --from=default-route-openshift-image-registry.apps.ocp4.imss.co.in/test/spring-boot-app:latest -n test --confirm

#Step 7: Deploy your app on OpenShift

#oc new-app spring-boot-app:latest -n test

#Step 8: Expose the service to get a route

#oc expose svc/spring-boot-app -n test

#Get the route URL:

#oc get route spring-boot-app -n test

#Step 9: Test the app

#Open the route URL in a browser or:

#curl http://<route-url>/
