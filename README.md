# kubernetes-3tier-application
This cloud-based web application is constructed with a variety of technologies.  It is intended to be accessible to users via the internet, allowing them to vote for their preferred programming language among six options: C#, Python, JavaScript, Go, Java, and Node.JS.ion

 **Techincal set**:
 
The application's frontend is created with React and JavaScript. It offers a dynamic and user-friendly interface for voting.
Backend and API: This application's backend is built with Go. It acts as an API for user voting requests. The database backend is MongoDB, which is setup with a replica set to ensure data redundancy and availability.

**Kubernetes Resources**

To deploy and manage this application properly, we use Kubernetes and a range of its resources:

**Namespaces**: in Kubernetes are used to build separate environments for various application components, ensuring separation and organization.

**Secret**: Kubernetes secrets securely store sensitive information, such as API keys or credentials, that the application requires.

**Deployment**: Kubernetes deployments specify how many instances of the application should run and provide instructions for updating and scaling.

**Service**: Kubernetes services ensure that users have access to the application by routing incoming traffic to the proper instances.

**StatefulSet**: Kubernetes StatefulSets are used to preserve order and distinct identities in components that require statefulness, such as the MongoDB replication set.

**PersistentVolume and PersistentVolumeClaim**: These Kubernetes resources manage the application's storage needs, ensuring data persistence and scalability.

**Learning Skills**:

Creating and deploying this cloud-native web voting application with Kubernetes is an excellent learning opportunity. Here are several important takeaways:

**Containerization**: Gain practical expertise with containerization technologies such as Docker for packaging apps and their dependencies.

**Kubernetes Orchestration**: Discover how to use Kubernetes to efficiently manage, deploy, and scale containerized applications in the production environment.

**Microservices Architecture**: Examine the advantages and disadvantages of a microservices architecture, in which the frontend and backend are separated and independently scalable.

**Database Replication**: Learn how to configure and maintain a MongoDB replica set for data redundancy and high availability.

**Security and Secrets Management**: Discover best practices for protecting sensitive information with Kubernetes secrets.

**Stateful Applications**: Understand the intricacies of deploying stateful applications in a container orchestration environment.

**By completing this project, you will gain a better grasp of cloud-native application development, containerization, Kubernetes, and the numerous technologies used to build and deploy modern web apps.**

Start with Minikube as cluster 
**command to install**
```Invoke-WebRequest -Uri "https://storage.googleapis.com/minikube/releases/latest/minikube-windows-amd64.exe" -OutFile "minikube.exe"```

**Install it to /usr/local/bin:**
sudo install minikube-linux-amd64 /usr/local/bin/minikube

**command toStart minikube**
Minikube start

Verfiy installation

``` Minikube version```

MONGO Database Setup

To create Mongo statefulset with Persistent volumes, run the command in manifests folder:
```kubectl apply -f mongo-statefulset.yaml```

Mongo service
```kubectl apply -f mongo-service.yaml```

On the mongo-0 pod, initialise the Mongo database Replica set. In the terminal run the following command:
```cat << EOF | kubectl exec -it mongo-0 -- mongo
rs.initiate();
sleep(2000);
rs.add("mongo-1.mongo:27017");
sleep(2000);
rs.add("mongo-2.mongo:27017");
sleep(2000);
cfg = rs.conf();
cfg.members[0].host = "mongo-0.mongo:27017";
rs.reconfig(cfg, {force: true});
sleep(5000);
EOF ```

To confirm run this in the terminal:

```kubectl exec -it mongo-0 -- mongo --eval "rs.status()" | grep "PRIMARY\|SECONDARY"```
Load the Data in the database by running this command:

cat << EOF | kubectl exec -it mongo-0 -- mongo

```use langdb;
db.languages.insert({"name" : "csharp", "codedetail" : { "usecase" : "system, web, server-side", "rank" : 5, "compiled" : false, "homepage" : "https://dotnet.microsoft.com/learn/csharp", "download" : "https://dotnet.microsoft.com/download/", "votes" : 0}});
db.languages.insert({"name" : "python", "codedetail" : { "usecase" : "system, web, server-side", "rank" : 3, "script" : false, "homepage" : "https://www.python.org/", "download" : "https://www.python.org/downloads/", "votes" : 0}});
db.languages.insert({"name" : "javascript", "codedetail" : { "usecase" : "web, client-side", "rank" : 7, "script" : false, "homepage" : "https://en.wikipedia.org/wiki/JavaScript", "download" : "n/a", "votes" : 0}});
db.languages.insert({"name" : "go", "codedetail" : { "usecase" : "system, web, server-side", "rank" : 12, "compiled" : true, "homepage" : "https://golang.org", "download" : "https://golang.org/dl/", "votes" : 0}});
db.languages.insert({"name" : "java", "codedetail" : { "usecase" : "system, web, server-side", "rank" : 1, "compiled" : true, "homepage" : "https://www.java.com/en/", "download" : "https://www.java.com/en/download/", "votes" : 0}});
db.languages.insert({"name" : "nodejs", "codedetail" : { "usecase" : "system, web, server-side", "rank" : 20, "script" : false, "homepage" : "https://nodejs.org/en/", "download" : "https://nodejs.org/en/download/", "votes" : 0}});

db.languages.find().pretty();
EOF```

Create MongoDb Secret

```kubectl apply -f mongo-secret.yaml```

**API SetUp**

Create GO API deployment by running the following command:

```kubectl apply -f api-deployment.yaml```

Create GO API service to expose by running the following command:

```kubectl apply -f api-service.yaml```

**Frontend setup**

Create the Frontend Deployment resource. In the terminal run the following command:

```kubectl apply -f frontend-deployment.yaml```

Create the Frontend Service resource to expose. run the following command:

```kubectl -f apply api-service.yaml```

Test the full end-to-end cloud native application

Using your local workstation's browser - browse to the URL created in the previous output.

Query the MongoDB database directly to observe the updated vote data. In the terminal execute the following command:

```kubectl exec -it mongo-0 -- mongo langdb --eval "db.languages.find().pretty()"```

**Summary**

In this project, you learnt how to deploy a cloud-native application to Minikube.  Once the application was deployed and functioning, you tested it using the browser on your local computer.  You later validated that your application activity produced data, which was correctly collected and recorded by the MongoDB ReplicaSet backend running within the cluster.


