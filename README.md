 Auto Configuration :
Debug = True
 
 
Certain condition needs to match for the auto configuration to work.
DispatcherServlet has to be found on class path to enable the DispatcherServlet Autoconfiguration
These are the positive matches.


These are the negative matches:
 
 
 
 
 
In the above class @primary annotation should be given be one of the bean otherwise there would be an ambiguity.
 
Metadata for the autoconfiguration
 
 
These conditions has to be verified to auto-configure the JPA feature.
 

Approach 1:
Creating object by our self
 
Creating the interface and creating the object.
Implementing the factory design


 
Now if we want to implement instagram in future then then we just need to change the value from facebook to instagram. There is no tightly coupling but still there is better approach. This approach will fail if we give the wrong value. This factory design approach is dependent upon the alias name.

Here the dependency injection concept simplifies the concept of ours.
 
No default constructor only the parameterized constructor is allowed for the dependency injection.
Constructor injection is manatory whereas setter injection isn’t. so, you’ve to choose which injection accordingly.

Any preprocessing logic that you want to carry out before the application startup then use the Command Line Runner.
Command Line Runner is the functional interface and we need to override the run method.
 
First run the override run method and then only the main method will run.
 
 
Conversion or mapper goes in the util package.
 
 
 
 
 
Session two:
Add two dependency :
 
Entity:
 
 
Bean Validation
 
 
 
 
 
 
 
 
 
 
BEST PRACTISE to handle the exception in the service layer
 
 
 
 
 
Logging level as trace..It will show everything so not suggested for production application.
 
 
For trace and debug we need to define in the application.properties file.
 
 
To write the log to the file
 

 

SWAGGER or OPENAPI:
 
 
 
 
 
 


 
To consume the rest services using RestTemplate.
Concept of actuator:
 
 
Enable all the endpoint then in application properties file:
 
This will increase the number of end-points:
 
 
 
 
 
 

 

 
This build-info will load all the data from target class meta info to the info actuator

To create your own build-info:
 
OUTPUT:
 
Custom actuator endpoint:
 
POST operation:
 

 
If you want to run method on application startup then use postconstruct.

 
In conventional JDBC we have to make the connection and statement and excute query for every method that we use. But Spring JDBC provide us the way to define this simply. In spring JDBC we provide the connection and statement one time and then we can call only the JDBC method to execute the query.
 
Shift + f6 to refactor name of class or packages;
Spring JDBC doesn’t have direct access to play with object

To get all the data from the database using sql command (select * from database)
We have to make use of RowMapper because we know that jdbc can’t play directly with object so all the values will come in RESULTSET and we can get value of that result set and insert into our particular employee object method.
Here we’re trying to get the value from result set and put that into the particular object of the Employee.
 
 
With lambda we can implement rowmapper in same method:
 
Instead of using this logic we can make use of another logic called BeanPropertyRowMapper<>(Employee.class). 
Why to use BeanProperty row mapper? => Because in row mapper we have to manually map every object to the result set but what if there are 1000 of records then at that situation we have to map 1000’s of data which is very tedious job.
So in order to get out from this we make muse of BeanProperty row mapper.
 














Spring Data JPA:
 

 
We create data.sql and on the start of the application the data.sql is read automatically on the earlier verison of the spring boot but now the spring boot latest version we have to provide config to read the data sql on the application start.
 
Usually data.sql and schema.sql come parallel because data is to insert data and schema to create, drop or alter the table. So if you are not creating table by giving schema.sql and relying on JPA for us to create that then we need to provide that info application.yml file.
Here :
 
Defer-datasource config says same thing that we’re not providing any schema.sql.






 
Data are loading in the sql but we have huge problem here, the data is getting duplicated. Everytime we restart the application the same data is getting added again and again. So to fix this we have certain config that we need to add.
 
After running the application for the first time to not duplicate the data we need to clean the sql.init.mode: always command from properties.

DEFINING OWN QUERY BY USING NATIVE POSITON BASED AND NAMED BASED PARAM:
 

To update the product we’ve to do certain things:
 

 
JPA TO IMPLEMENT DIFFERENT SQL CLAUSE LIKE “IN, BETWEEN, LIKE, GREATER THAN” etc.
REPOSITORY VIEW:
 
Paging and Sorting technique in spring Data JPA:
 

Soring and Pagination in same method:
 

 



 
 
 
 
 
 
 

UNIT TEST REPOSITORY LAYER:
 

 
After making the assertion static we don’t need to class name again and again:
 
Find all method:
 

 




Spring Data REST:
 
 
 
 
Pagination and sorting in url using data rest.
 

All entity expose in the port where we are running the application.
For visualizing in spring data rest we need to make use of HL not swagger.


SPRING DATA JPA => Auditing
Why it is created or why we need it?
 

The concept of spring data auditing came to play role when someone changed the crucial data and they want to know who and when this data was changed. This way you can know the culprit of that problem and why it was done.
   

These annotation createdBy, CreatedDate etc arenot coming from the persistence layer rather they are coming from the import org.springframework.data.annotation.CreatedBy;

 
Where is this AuditingEntityListener class coming from and what it is doing?
This class is saying to our entity that I am going to audit your fields.
The AuditorImpl class at the bottom help us to get the user who has last modified the data. We’re hard coding the user in this context but we can get this data from the database itself.
 

 
Spring Data Envers:

So, auditing is to get the created time, created by and all other those things which I mentioned above but now how can  we trace someone who have modified it.
So, to trace this concept of spring envers comes to play role. This is use to trace the all the modified data.
It will create its own database and through it we can trace the data.
 
 
These three tables are created the first product is the simple entity table that is created through spring data jpa but the other are created by the envers to trace the updated data.
Three things has to be modified to implement the envers.
In main application file: 
In Repository file :
 
Now of which Entity we want to this trace:
Whichever entity we are auditing we are creating the trace for that particular object:
 



JASYPT: encryption and decryption
 
 

Configuration encrypted:
 

 
 
 
 
 


SPRING BATCH:
 
 


 
 

 
 
 
 

 

 
 

JPA ONE TO MANY: 
 
 
 
 
 
 
 

 
Delete child if there parent is also delete. For ex, engineer who aren’t mapped to any project will be deleted from the engineer DB.
 



End to End Integration test:
Service layer:
 

 

To fix this we can put in the @test annotation the following thing:
 
Otherwise you can create the new method:
 
 

@Mock will create the stub or the mock of the object the bean you define and deosn’t load in application context.


@MockBean will create the mock of the object and loads the mock object into the application context.
 
 
 



Spring Batch::
 

 
 

We’re trying to dump this CSV file into the DATABASE by using the batch.
So first we need to create the entity class for all the fields included in the CSV.
 
 

 
Here we’re skipping the 1st line of the CSV file because the first line contains the column name and we don’t want to import that as our java object.

setlineMapper is the making use of lineMapper() function and this function will help us get the data from the CSV file to the java object separated by the comma.

 
 

 
 
 
 
 
 
 
To create the multiple step:
 
 But we have only one step so modify code as:
 
 If you want to filter any data that will be coming from our CSV to the java object then you can put validation in it.
For example, if you want only male gender to pop in your java object then:
 

 
 
 
 
 
We’re making bean of the TaskExecutor in the config file to make the program Asynchronous. We have to feed this taskExecutor to the importCustomerStep() function:
 













Spring Security:
 
 
 

This is the simple security implementation.
•	URL based security and Role Based security:
Now instead of giving username and password in the application.properties file we’re providing it in the config class using configure method.
 
 
Now we have two controller and we want to implement the security feature for only one controller so how can we do it:
By using the URL based security:
 
ROLE BASED SECURITY:
First create the multiple role like ADMIN and USER.
 

 
Only with role ADMIN will be able to access the URL.

SPRING SECURITY USING SPRING DATA JPA + MySQL
 
 
 
 
 
 
 
 
 
 
 
 
 
The userDetails comes from the security itself.
 
 
This concept is allowing only certain user to access the resources.
This is based on the three factors: 

MyPortal is an application running in the port 8080 and we want to allow the client application access the myportal application. So in order to do that we have to disable the CORS.
This can be accomplished in three level:

 
1)	The first level is implementing in the controller layer.
	Above green color highlight showcase how it can be done.
2)	If there are multiple controller and you want to achieve this in the global form then you have to implement this in the class layer:
	Above yellow color highlight is showcasing how it can be done.
3)	If you don’t want to implement in the class layer then you can make a bean of it and configure.



















 
 
 
Transactional management: when if one of the service is failed then at that time the data is not saved in the DB and all rollback happens itself. This is easy in monolith but in microservice arch its little different as each service will have their own database.
 
 
Disadvantages are:
1)	N no of  HTTP Call.
2)	Impact on revenue if there is impact in services.
 
 









JWT:
 
Here to access the different API we have to provide credentials for each URL. This is not cool so what we can do to overcome is implement the concept of JWT .
 

 

 

 
 
 
 
Here @PostConstruct will help us to load the data as we start the application.
 
 
 
Here what we are doing is we’re creating the custom UserDetailsservice that the spring security provides and we are fetching the User from the DB and then we’re providing the name and password of that User to the spring security provided user.
 
 
 

This way we will be implementing the spring security but we want to implement the JWT so for that we need to continue working.
 
We have to write the util class for the JWT implementation.
 
Here what is happening is we are generating the token on the basis of function generateToken() using the username. And then we are validating the token using the function validateToken().
 




Add this bean in the SecurityConfig.
 
In our controller class:
 
 all the end point are secured are secured by spring security right now but we want this end point “/authenticate ” to be use by anyone because that’s how they can create the JWT token. So for that. In the security config add the method which is highlighted as blue in down picture.
  
 
Now if we use this token to run other end point then the end point will not work.
For that we have to provide one more filter chain.
 
Before this token goes to my controller I need to validate this token. So how can we do that?
 
 
Now we have to register this JWTfilter class into securityConfig. 
 
 
Add the code in configure in securityconfig.


Spring Cache:
 
Right now when we try to fetch the data from the postman using the get request then to load the 10,000 data from DB it will almost take 267millsec which is not good so to improve this we have to implement the SPRING CACHE
 
 
Mostly Cache is use for retrieving the data.
Down pic depicts that and we’re implementing that in the service layer.
 
Whenever new data is added to the database then first we need to add to the cache and then only DB. If old data is updated then first update in the cache and then DB.
How can we do that?
The default cache is implemented through the ConcurrentHashMap.
 
By using the cache put in the saving and updating service function we can implement cache. So this way whenever the user try to save or update the value first the value will be save in the cache and then update in the DB.
 
Save method

 
Update method
We’re using the in-memory cache and that have to be cleared as well because we don’t want to waste the memory. So, every time we delete from the DB we have to delete from the cache as well. so, to do that:
 
 


Spring Redis:
 
 

 
 

 

 
 

 

 
 
 
 
 


 

  

 

 

We’re getting the error because we’re sending the data in the Redis server and while sending the data over the network we have to make the Entity as the serializable. 
 
Since we define the serializable, it’s recommended to implement the serialVersionUID.

 


Spring Data Redis as Database:
Editing in the same above project to implement the Spring Data Redis.
 
Now in our service class instead calling the DAO we will call the spring data Repository provided method.
 

Get the repository into the service class through the autowired.
 

 

 
 







PCF(Pivotal Cloud Foundry)
 

Spring Security:
 

401  => we get this during the authentication phase.
403 Forbidden = > we get this during the authorization phase
Before the spring security came into the picture we use to implement the security through the help of filter function. But there we have to make lot of configuration changes.
 

To reduce this spring security came into picture which reduces everything. We just use the classes and methods provided by the spring security.

USERNAME AND PASSWORD METHOD:
 
 
 
Now if we run this application then the default spring security will be implemented and it will ask for the password and username.
If you want to disable this default behavior of the spring security then all you have to do is disable security.
 

You can also add that in the application.property file :
 

Configure your own username and password
 
This way it will be secure for all the endpoints but if we want some to be secure and some not then how we can do that:
URL based authentication:
 

 
 
Spring security always suggest to encrypt and decrypt the password, for that we can make use of the passwordEncoder.
 

 
Now which end point you want to authenticate and allow and which doesn’t.
 

 

Websecurity configure adapter is what we’re using to enable the security in our application but form spring 3.00 this class is deprecated and we’ve to make use of new class. 
NEW WAY OF DOING AT BOTTOM:
 
 
 
 

AUTHORIZATION:
 
 
 
 

 
 









Spring security Auth using the Spring Data JPA + MySql:
 
Here we have provided the details of user and their role by hard coding but we want to have this thing dynamically coming from the database.


 
Add three field that we need to add in the Entity class.
While saving the employee in the database we’ve to encrypt the password.
So, we go to the service class:
 
 

We’re allowing all the employee to onboard themselves, so for that we’ve to remove the pre-authorize annotation in the controller and change the antMatchers in the config:

 
 
 
When new employee is onboarded the role assign will be the default role but HR folks has the authority to change that role.
 

 

 
This is a very important interface, because it loads the user data from the database to the spring application context and we can use that.
Create a new class:
 
 
 

 




 

 

 
Rest everything you can give true



 

Spring security internal flow:
 
 
 




Reverse proxy example:
 


 

 

 


 
 

 
 
 
 
 

 
 
 


 

 

 
Zookeeper manages our kafka server.
To start the kafka server we have to start the zookeeper.
Start the kafka then create the topic and do the partition in the topic and play with it.

 

JWT: JSON web token
 
 
 

 
 
 

 
The thing here right now is, if we call the jwt generate method by anyone then they will give us the token but we don’t want this to happen in real life situation. We want this token to be generated only to those user who are currently in our system or DB. So to authenticate the user is current user or not we have to make use of authentication manager.
In controller:
 
Now create the bean:
 
 
Now we have to bypass this api endpoint in our security otherwise user won’t be able to give the username and password to generate the token.
 

Now if we use this token to hit other api end point then we won’t be able to get the other end point because we don’t have any logic to know that this token is the valid token.
So the first thing we want to do is write our custom filter.
Extract the name from the token and then validate that name against DB whether that user is current use or not.
 
 

Now create the custom filter class:
 
 
 
Create own auth provider:
 
Now tell spring security to use custom filter:
 


Eureka Service Discovery:
  
 

 

Helps in decoupling or tight-coupling between the host and the microservices. To remove the infra dependency.
 
 
To register the services to the eureka we have to add client dependency in the POM
 
 
 
  
To perform the load balance with round robin fashion we will just use this annotation.
This is also one of the feature of eureka service registry.
 
 

===========================================================
ssh -i '.\Ec2 Rabin.pem' ec2-user@44.204.15.8
DOCKER : first image then the container
Mvn-clean install
Mvn spring-boot:run
Mvn spring-boot:build-image
Java –jar target/accounts-0.0.1-SNAPSHOT.jar
Docker build . –t eazybytes/accounts => tag name you can give your name at eazybytes/accounts
Docker images
Docker inspect id
To create the container
Docker run –p 8080:8080  rabin/account => second port is where the docker  will run the application at the port number.
Docker ps –a => check container in background
Dokcer logs container_id
Docker stop container_id
Docker container pause container_id
Docker container unpause  container_id
Dcoker container inspect container_id
Docker kill => instantly stop the container whereas docker stop will have some grace period to stop the container
Docker stats container_id
Docker rm id
To not get any logs while running (The long logs) then run in the deattached mode:
Docker run –d –p 8081:8080 rabin/account

Cloud Native BuildPacks:
Makes everything easier docker.
Source code into runnable interface.
Paketo buildpacks.
 
Mvn spring-boot:build-image

DOCKER compose:
If we have 100’s of microservice then at that time we have to individually go to cmd and run the container with above approach . so, to fix this issue the concept of docker compose comes to play the role.
**Docker-compose version

 
**docker-compose up: before we use this command everything has to be  pushed to the docker repository.

Kubernetee:
Maven Commands used in the course
Maven Command	Description
"mvn clean install -Dmaven.test.skip=true"	To generate a jar inside target folder
"mvn spring-boot:run"	To start a springboot maven project
"mvn spring-boot:build-image -Dmaven.test.skip=true"	To generate a docker image using Buildpacks. No need of Dockerfile
Docker Commands used in the course
Docker Command	Description
"docker build . -t eazybytes/accounts"	To generate a docker image based on a Dockerfile
"docker run -p 8081:8080 eazybytes/accounts"	To start a docker container based on a given image
"docker images"	To list all the docker images present in the Docker server
"docker image inspect image-id"	To display detailed image information for a given image id
"docker image rm image-id"	To remove one or more images for a given image ids
"docker image push docker.io/eazybytes/accounts"	To push an image or a repository to a registry
"docker image pull docker.io/eazybytes/accounts"	To pull an image or a repository from a registry
"docker ps"	To show all running containers
"docker ps -a"	To show all containers including running and stopped
"docker container start container-id"	To start one or more stopped containers
"docker container pause container-id"	To pause all processes within one or more containers
"docker container unpause container-id"	To unpause all processes within one or more containers
"docker container stop container-id"	To stop one or more running containers
"docker container kill container-id"	To kill one or more running containers instantly
"docker container restart container-id"	To restart one or more containers
"docker container inspect container-id"	To inspect all the details for a given container id
"docker container logs container-id"	To fetch the logs of a given container id
"docker container logs -f container-id"	To follow log output of a given container id
"docker container rm container-id"	To remove one or more containers based on container ids
"docker container prune"	To remove all stopped containers
"docker compose up"	To create and start containers based on given docker compose file
"docker compose stop"	To stop services
Kubernetes Commands used in the course
Kubernetes Command	Description
"kubectl apply -f filename"	To create a deployment/service/configmap based on a given YAML file
"kubectl get all"	To get all the components inside your cluster
"kubectl get pods"	To get all the pods details inside your cluster
"kubectl get pod pod-id"	To get the details of a given pod id
"kubectl describe pod pod-id"	To get more details of a given pod id
"kubectl delete pod pod-id"	To delete a given pod from cluster
"kubectl get services"	To get all the services details inside your cluster
"kubectl get service service-id"	To get the details of a given service id
"kubectl describe service service-id"	To get more details of a given service id
"kubectl get nodes"	To get all the node details inside your cluster
"kubectl get node node-id"	To get the details of a given node
"kubectl get replicasets"	To get all the replica sets details inside your cluster
"kubectl get replicaset replicaset-id"	To get the details of a given replicaset
"kubectl get deployments"	To get all the deployments details inside your cluster
"kubectl get deployment deployment-id"	To get the details of a given deployment
"kubectl get configmaps"	To get all the configmap details inside your cluster
"kubectl get configmap configmap-id"	To get the details of a given configmap
"kubectl get events --sort-by=.metadata.creationTimestamp"	To get all the events occured inside your cluster
"kubectl scale deployment accounts-deployment --replicas=3"	To increase the number of replicas for a deployment inside your cluster
"kubectl set image deployment accounts-deployment accounts=eazybytes/accounts:k8s"	To set a new image for a deployment inside your cluster
"kubectl rollout history deployment accounts-deployment"	To know the rollout history for a deployment inside your cluster
"kubectl rollout undo deployment accounts-deployment --to-revision=1"	To rollback to a given revision for a deployment inside your cluster
"kubectl autoscale deployment accounts-deployment --min=3 --max=10 --cpu-percent=70"	To create automatic scaling using HPA for a deployment inside your cluster
"kubectl logs node-id"	To get a logs of a given node inside your cluster
      
 
