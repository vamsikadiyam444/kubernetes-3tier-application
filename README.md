# kubernetes-3tier-application
This cloud-based web application is constructed with a variety of technologies.  It is intended to be accessible to users via the internet, allowing them to vote for their preferred programming language among six options: C#, Python, JavaScript, Go, Java, and Node.JS.ion
 Techincal set:
The application's frontend is created with React and JavaScript. It offers a dynamic and user-friendly interface for voting.
Backend and API: This application's backend is built with Go. It acts as an API for user voting requests. The database backend is MongoDB, which is setup with a replica set to ensure data redundancy and availability.
**Kubernetes Resources**
To deploy and manage this application properly, we use Kubernetes and a range of its resources:
Namespaces in Kubernetes are used to build separate environments for various application components, ensuring separation and organization.
Secret: Kubernetes secrets securely store sensitive information, such as API keys or credentials, that the application requires.
Deployment: Kubernetes deployments specify how many instances of the application should run and provide instructions for updating and scaling.
Service: Kubernetes services ensure that users have access to the application by routing incoming traffic to the proper instances.
StatefulSet: Kubernetes StatefulSets are used to preserve order and distinct identities in components that require statefulness, such as the MongoDB replication set.
PersistentVolume and PersistentVolumeClaim: These Kubernetes resources manage the application's storage needs, ensuring data persistence and scalability.
**Learning Skills**:
Creating and deploying this cloud-native web voting application with Kubernetes is an excellent learning opportunity. Here are several important takeaways:
Containerization: Gain practical expertise with containerization technologies such as Docker for packaging apps and their dependencies.
Kubernetes Orchestration: Discover how to use Kubernetes to efficiently manage, deploy, and scale containerized applications in the production environment.
Microservices Architecture: Examine the advantages and disadvantages of a microservices architecture, in which the frontend and backend are separated and independently scalable.
Database Replication: Learn how to configure and maintain a MongoDB replica set for data redundancy and high availability.
Security and Secrets Management: Discover best practices for protecting sensitive information with Kubernetes secrets.
Stateful Applications: Understand the intricacies of deploying stateful applications in a container orchestration environment.
**By completing this project, you will gain a better grasp of cloud-native application development, containerization, Kubernetes, and the numerous technologies used to build and deploy modern web apps.**


