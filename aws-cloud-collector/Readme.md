AWS Collector
=================

AWS Collector is part of Hygieia 2.1 release and bring in Ops view to the already dev capabilities of Hygieia like DevOps Dashboard (Hygieia 1.0) and Program level Dev View (Hygieia 2.0)
The AWS Collector is a microservice with sole task of collecting data from your AWS footprint for the dashboards configured. As again as part of our component architecture this is optional
and if you don't use cloud , you don't need to run this.

Currently supported Cloud platform is Amazon Web Service.

Building and Deploying
--------------------------------------

Run
```
mvn install
```
to package the collector into an executable JAR file. Copy this file to your server and launch it using :
```
java -JAR aws-collector.jar --spring.config.name=aws --spring.config.location=./aws.properties 
```
You will need to provide an **application.properties** file that contains information about how
to connect to the Dashboard MongoDB database instance, as well as properties the AWS collector requires. See
the Spring Boot [documentation](http://docs.spring.io/spring-boot/docs/current-SNAPSHOT/reference/htmlsingle/#boot-features-external-config-application-property-files)
for information about sourcing this properties file.

###Sample application.properties file
--------------------------------------

    #Database Name 
    dbname=dashboard

    #Database HostName - default is localhost
    dbhost=localhost

    #Database Port - default is 27017
    dbport=27017

    #Database Username - default is blank
    dbusername=db

    #Database Password - default is blank
    dbpassword=dbpass
    
    #Logging File location
    logging.file=./logs/cloud.log

    #Collector schedule (required)
    aws.cron=0 0/5 * * * *
    
    #AWS ValidTag Key - To look for tags that you expect on your resource
    aws.validTagKey[0]=ABC
    aws.validTagKey[1]=XYZ

    #AWS Proxy Host
    aws.proxyHost=localhost
    
    #AWS Proxy Port
    aws.proxyPort=3333
    
    #AWS Non Proxy
    aws.nonProxy=xxx.xxx.xxx.xxx
    
    #AWS Profile to be used if any
    aws.profile=