# spring-cloud-serverless repo

This repo provides a simple serverless Hello web app based on Spring Boot and Spring Cloud Function.

It can be deployed as a standalone web app, as a Tanzu Application Platform workload resource or, as a Kubernetes Deployment and Service.

## The code

> **NOTE**: The project uses Spring Boot 3.0 and is configured for Java 17.

The project contains the following Function bean definition:

```text
	@Bean
	public Function<String, String> hello() {
		return (in) -> {
			return "Hello " + in;
		};
	}
```

This simple serverless app returns the input value, prefixed with "Hello ". This is just a simple example what a Spring Cloud Function app can do. 
It is defined in `src/main/java/com/example/helloapp/HelloAppApplication.java`

## Deployment

This app can be deployed as a stand-alone web app, as a Tanzu Application
Platform (TAP) workload resource, as a Tanzu Application Service (TAS) app, or
as a Kubernetes Deployment and Service.

### Standalone app with embedded Tomcat server

You can build the project using Maven:

```bash
mvn clean package
```

To run the app using the embedded Tomcat server you can run this command:

```bash
mvn spring-boot:run
```

You can access the app using `curl`:

```bash
curl -w'\n' -H 'Content-Type: text/plain' localhost:8080 -d "Fun"
```
### Deploying on Tanzu Application Service

Build a JAR file locally using Maven:
```bash
mvn clean package
```

Deploy the JAR on TAS using the `cf` CLI:
```bash
cf push -p ./target/spring-cloud-serverless-0.0.1-SNAPSHOT.jar -f manifest.yaml`
```

### Accessing the App Pushed to Tanzu Application Service

Determine the URL to use to access the app by running:

```
cf app spring-cloud-serverless
```

To query the deployed app run the following `curl` command in another terminal window:

```
curl ${URL} -w'\n' -H 'Content-Type: text/plain' -d Fun
```
