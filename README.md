# Network International Assessment

## Requirement in Short 

1) Design a micro-service that receives a set of information that is 

    a) Sensitive (Secured data).
    b) Huge size.
    c) needs validation
  
2) Validate\Verify the request, then route the request to another Business logic micro-service that persist the recived set of information in to DB. 

3) Setep up a micro-services environment (service discovery, config management, API gateway, fault-tolerance, log tracing)

4) Design the API interface in such a way that its loosely-coupled and you are able to scale horizontally, and accommodate future updates.

5) Design the architecture to high performance and optimum memory usage

## Quick Logical View of the Requiement

![alt Logical Solution](https://i.ibb.co/52JM7q1/Screen-Shot-2019-09-17-at-9-18-17-PM.png)
## Assumptions 

1) To keep the use-case simple for the assessment, we will transfer a set of User objects with attributes id, name, and message.

2) id and name are the attributes that need validation 

3) Secure data transfer needs to use HTTPS. This piece of the solution is covered in the solution proposal. The actual Https implementation is not done because of infrastructure availability.

4) It's assumed that the requirements are greenfield in nature, which allow as to go open in choosing the best possible technology stack fit for the use-case. Real-life solutions / technical stack selection will have to align with project/enterprise strategies

5) There is a bias in choosing technology stack towards open source components considering the limited resource availability for the assessment POC.

6) Estimation approach is provided considering the agile software development methodology and assuming a single team member taking all stakeholders point of view.    

# Solution Approach

## Transmitting Large Data Sets

Transmitting large data sets over the wires has its one challenges. I am trying to capture as some of the important constraints here

1) Network latency 
2) Long-running connections and connection drop
3) Otmimized data format for low data size 
4) Blocked thread pool for a longer period 
5) Uneven distribution load in the serverside data processing unit

Considering the above fact and our microservice development environment, the following protocols are considered in technology selection

![alt Logical Solution](https://nordicapis.com/wp-content/uploads/When-to-Use-What-REST-GraphQL-Webhooks-gRPC-1.png)

We are choosing gRPC as networking solution among the considered options because of the following advantages for the given use-case over the other protocol 

1) gRPC is built on HTTP/2, which supports traditional Request/Response model and bidirectional streams. Streaming allows moving a large volume of data chunk by chunk.   

2) gRPC is all about Protobuf messages. Protobuf is the best way of encoding structured data.

3) gRPC can connect services in and across data centers with pluggable support for load balancing, tracing, health checking and authentication.  

4) gRPC is based on HTTP/2. HTTP 2 is Binary protocol. Binary protocol is much efficient to parse.

5) gRPC is a CNCF incubating project and sits well in the cloud-native landscape 

6) gRPC is extremely fast when compared to other protocol considered and enables reactive programming / efficient thread pool usage. 

The below picture attempt to make a representation of different gRPC client-server interaction  models

![alt Logical Solution](https://i0.wp.com/technokeeda.com/wp-content/uploads/2018/05/grpc_python.png?w=2000&ssl=1)


## Transmitting Data Secure

1) gRPC enables easy SSL usage to encript data in transit, with a unique pair of certificate for each server client pair.

2) There are standerd token authentication filters available with renew ability in the standard gRPC pack. 

3) Any custom authentication can be easily achieved by writing custom filters 

4) There is support for passing metadata along with the request, this can be used for any custome authentication

Note: In the example developed for this assessment, I achieved authentication using meta-data token. I did test SSL encryption in local but could not get it working in combination with API Gateway as it needs additional development work crossing the limits of the available timeline to submit the assessment. 

## Micro-service Ecosystem

One of the important parts of the requirement is to set up a micro-services environment with service discovery, config management, API gateway, fault-tolerance, log tracing. 

> CNCF Trial map and landscape were referred to chose technology stack [Link](https://github.com/cncf/landscape).
>  Free google cloud credits available for assessment is another major influence in the choice of technology 

We have choosen the below tech stack to implement the usecase. Detailed information on how this environment set up is done is covered in one of my anothere another github repository [Link](https://github.com/ArunRamakani/provision-kubernetes-gke).

Tech Stack  | Usage
------------ | -------------
Google Kubernete Engine | Managed Kubernete for container Orchestration 
Ambassador | API gateway 
Ambassador | Load Balancer
Istio | Connect, Secure, Control and Observe  microservices
Prometheus | Monitoring
Fluentd | Logging

![alt landscape](https://i.ibb.co/X82S1rz/Screen-Shot-2019-09-18-at-8-57-18-AM.png)


## Estimation Approach as a Team Lead 

An obsolute estimate in the idel expectation for better release planning, but an relative estimate is more realistic because of the uncertain nature of software development with respect to the fact that the requirment / technical constrains evolve over time. 

So its good to start with a relative estimate and try to make the estimate more obsolute during the journey. Consideing agile software development methodology estimation can be done in two different stages

1)  Initial Use-case Level estimate - This can be done by sketching a quick logical view of the solution and then comparing the solution with similar/near-close piece of work. Involving people who have done near close/similar solution will add great value. These estimates will be more relative in nature. In the case of "new of its kind" use-case, a quick study should be maid to come up with a ballpark estimate with assumptions and can be shared with word of caution. 


2) Sprint Planning and User Story level estimate - We should have converted the logical view of the solution into user stories and technical requirement before reaching this stage of estimation. Different stakeholders like product owner, architect, the engineering team can be involved as needed during this journey. During the sprint planning session story point, intimate can be done involving the development team members. This estimate is of more absolute than the previous level.

The estimate may evolve during the sprint because of newly identified technical constrain and inter-team dependencies. These change in estimate need to be captured in the daily scrum for stack holder communication and to mitigate the risks.

High variance in the estimation during different stages is a good candidate for sprint retrospection at the end of the sprint.

Considering the apove approach, please find the estimation for the assessment piece of work

*Stage 1 - Part of the requirement(Bulk Data Upload) is new of its kind for me and hence quick research is done to come up with an estimate* 

Item  | Effort in Hours
------------ | -------------
Effort looking at the initial logical solution view | 35


*Stage 2 - The requirement is detailed to identify the exact list of items to be done to complete the task. This involves applying Engineering, Architecture, Security point of views to the solution approach* 

Story Points  | Effort in Hours
------------ | -------------
Setup Free google assesment | 1
Setup Kubernetes | 2
Setup API GateWay and Loadbalancer | 8
Setup Istio | 4
Setup Prometheus | 2
Develope Data Streaming server| 10
Develope Data Streaming Client | 3
Develope Business Logic Microservice | 4
Apply all Security rules and test | 6
Documentation | 4
