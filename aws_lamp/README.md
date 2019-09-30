
# AWS Lamp

## Challenge

Provide a Cloudformation template defining a redundant, secure and cost effective LAMP stack within AWS.

## Response

- Provide documentation describing your environment
- Provide a link to a public git repository hosting the template (committing frequently so we can see how your solution progressed) 

## Stretch Goal

- Provide a small application that will run on the infrastructure (written in PHP that connects to the MySQL database)  

Notes: Apache, PHP or MySQL not your thing? Feel free to swap any of these out for an alternate technology.

## Design

### Infrastructure

This implementation uses a load balancer, autoscaling group, and dynamodb to provide a redundant, secure, and cost effective infrastructure stack. The builds are parameterised to allow for different settings per environment. Setting the nodecount and subnets to more than one allows for a highly available stack. Setting the AccessIp allows control from where the application can be accessed.

### Application

The application is a python application fronted by apache that queries dynamodb for data storage. The root page is a static page linking to the application, this allows for a response when the python application isn't working and improves debugging speed. The application at /app writes to the dynamodb table then gets a count of the rows stored to validate the read and write functionality.

### Future Improvements

 - Push the application code and apache config to S3 and have the userdata copy in the code, this will be required if the code base becomes larger.  
 - Implement dynamic scaling on thresholds.  
 - Switch the healthcheck from EC2 to ELB and point at the apaches status page.  
 - Separate IAM to improve the stack modification performance and segregate the access control.  
