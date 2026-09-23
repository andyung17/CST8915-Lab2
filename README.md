# CST8915 Lab 1: Algonquin Pet Store on Azure VM

**Student Name**: Andy Ung <br/>
**Student ID**: 041299387 <br/>
**Course**: CST8915 Full-stack Cloud-native Development <br/>
**Semester**: Fall 2026 <br/>

---

## Demo Video

🎥 [Watch Demo Video](https://youtu.be/-xYmPA5PPs4)

---

## Reflection Questions

1. What changes did you make to the order-service and product-service to comply with the Configurations and Backing Services factors of the 12-Factor App methodology?

In order to comply with the 12-factors, `order-service` and `product-service` were changed in the following ways

- Factor 1 Codebase: Adding new distinct repos for `order-service` and `product-service`
- Factor 2 Dependencies: Using `npm install dotenv`, added support for the env file for `order-service`. Made sure that each service had all neeeded dependencies in their respective depedency management files.
- Factor 3 Configurations: Added an `.env` for `order-service` and `product-service` and filled in the necessary connections and public ips to get each service to communicate with eachother over HTTPS
- Factor 4 Backing Services: We want to treat resources such that they can be attached or detached, so a VM was spun up for the RabbitMQ service. `order-service` had a connection string to the rabbitmq service located in the `.env` file such that the service could be attached or detached at will. 

2. Why is it important to use environment variables instead of hard-coding configurations in your application?

Instead of hardcoding the configurations, using an environment variable allows us to maintain security. Hard-coding these configurations leaves a potential risk for public access when using version control platforms. Keeping them into an environment file maintains the security. With config files, this helps with maintainability as different CI/CD pipelines may rely on different configurations that if hardcoded, would break. It is eaiser to locate these secrets or configurations in one file instead of locating them in a large code base. 

3. Why is it important to have separate repositories for each microservice? How does this help maintain independence and scalability of each service?

It is important to have a separate repo for each microservice because
<br/>**Readability**: Makes the repo easier to read as whatever is required is in its corresponding repo
<br/>**Not Including Unnecessary Dependencies**: Makes the deployment and version control eaiser as it will run with exactly what is required. 
<br/>**Scalability**: Makes it easier to scale, and can spin up a specific microservice if needed.

This helps with independence and scalabiltiy as any code changes to the repo would not affect another team / when an automated test runs. When one teams feature changes and leads to a failure, this would block another team if their changes on their project would work just fine. When we seperate repos, this can allow us to scale better and faster. When we spin up a new environment, we are only including the necessary components for it to initialize and run. In addition, if it were grouped together, if one service failed, a whole new initialization needs to be done despite the other services working. 

---

## Challenges and Learnings (Optional)
- Was getting issues with running the product service as my machine had too little RAM. After getting a better VM worked after

---

## Acknowledgments
- https://12factor.net/backing-services