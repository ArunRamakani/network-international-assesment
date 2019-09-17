## Network International Assesment

# Requirement in Short 

1) Design a micro-service that receives a set of information that is 
  - Sensitive (Secured data).
  - Huge size.
  - needs validation
  
2) Validate\Verify the request, then route the request to another Business logic micro-service that persist the recived set of information in to DB. 

3) Setep up a micro-services environment (service discovery, config management, API gateway, fault-tolerance, log tracing)

4) Design the API interface in such a way that its loosely-coupled and you are able to scale horizontally, and accommodate future updates.

5) Design the architecture to high performance and optimum memory usage


# Quick Logical View of the requiement

![alt Logical Solution](https://i.ibb.co/52JM7q1/Screen-Shot-2019-09-17-at-9-18-17-PM.png)

# Assumptions 

1) To keep the use-case simple for the assessment, we will transfer a set of User objects with attributes id, name, and message.

2) id and name are the attributes that need validation 

3) Secure data transfer needs to use HTTPS. This piece of the solution is covered in the solution proposal. The actual Https implementation is not done because of infrastructure availability.

4) It's assumed that the requirements are greenfield in nature, which allow as to go open in choosing the best possible technology stack fit for the use-case. Real-life solutions / technical stack selection will have to align with project/enterprise strategies

5) There is a bias in choosing technology stack towards open source components considering the limited resource availability for the assessment POC.     





