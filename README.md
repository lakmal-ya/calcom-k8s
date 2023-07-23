# calcom-k8s
Setting Up Calcom and PostgreSQL in Kubernetes for Streamlined Scheduling and Data Management

Introduction:
<br>In today's fast-paced world, effective scheduling and calendar management are crucial for productivity and time optimization. The Calcom application emerges as a sophisticated solution to address these needs, offering powerful features and a user-friendly interface. Concurrently, PostgreSQL, a renowned open-source relational database management system, complements Calcom with its robustness, scalability, and extensibility. In this article, we will explore the process of setting up Calcom and PostgreSQL in Kubernetes, combining their capabilities to streamline scheduling and data management.

What is Calcom Application?
<br>The Calcom application is designed to enhance productivity and time management by simplifying event scheduling and availability management. With a focus on providing a seamless scheduling experience, Calcom offers customizable settings and synchronization with preferred calendars. Its user-friendly interface enables users to manage their calendars efficiently and receive detailed telemetry and analytics to optimize calendar usage. Whether for individual use or team collaboration, Calcom helps users stay organized and improve efficiency in managing their daily tasks.

What is PostgreSQL?
<br>PostgreSQL, often referred to as "Postgres," is a robust and advanced open-source relational database management system. Developed as an evolution of the Ingres database, PostgreSQL boasts a rich history of active development and a thriving community of contributors. Its adherence to the SQL standard and support for ACID transactions make it a reliable choice for managing relational data. PostgreSQL's extensibility allows users to define custom data types, operators, and functions, tailoring the database to specific application needs. With features like advanced indexing, JSON support, and full-text search capabilities, PostgreSQL has become a preferred choice for a wide range of applications.

> :warning: **if you are using postgresql oder than 15**
<br>This has fully tested on postgresql version 15. if you using older version you might be face some issue on prisma database migratino setup. some table will not migrate.

Setting Up Calcom and PostgreSQL in Kubernetes:
To deploy Calcom and PostgreSQL in Kubernetes, follow these steps:

1. **Prerequisites**:
   - Install Kubernetes on your local machine or preferred cloud provider.
   - Set up the necessary tools for managing Kubernetes, such as kubectl.

2. **Create Kubernetes Namespace**:
    - Start by creating a Kubernetes namespace to isolate the   Calcom and PostgreSQL resources.
    - Use the kubectl create namespace calcom command to create the "calcom" namespace.

3. **Deploy PostgreSQL**:
   - Create a PostgreSQL Deployment and Service manifest YAML file with the necessary configuration, such as the database credentials and data storage options.All the details on **postgres-config.yaml**

> :information_source: **Additional Information**:(**change database POSTGRES_USER & POSTGRES_PASSWORD default user:admin & password: psltest**)
   - Use following commond to deploy the postgresql
   ```
   kubectl apply -f postgres-config.yaml     -n calcom   #to deploy PostgreSQL configMap.
   kubectl apply -f postgres-pvc-pv.yaml     -n calcom   #to deploy PostgreSQL presistent volume and Persistent volume claim.
   kubectl apply -f postgres-deployment.yaml -n calcom   #to deploy PostgreSQL.
   kubectl apply -f postgres-service.yaml    -n calcom   #to expose PostgreSQL service.
   ```

4. **Create Calcom Deployment**:
   - Create a Calcom Deployment manifest YAML file with the appropriate environment variables, specifying the PostgreSQL database URL and other configuration details.
   - Use following commond to deploy the calcom
   ```
   kubectl apply -f calcom-configmap.yaml      -n calcom  #to deploy the Calcom application ConfigMap.
   kubectl apply -f calcom-deployment.yaml     -n calcom  #to deploy the Calcom application and Calcom services.
   ```

Conclusion:
By setting up Calcom and PostgreSQL in Kubernetes, you can harness the power of these robust tools to streamline scheduling and data management. The Calcom application offers an intuitive interface, empowering users to efficiently manage events and availability. PostgreSQL complements Calcom with its scalability and extensibility, providing a reliable and powerful backend for managing data. Together, they form a dynamic duo, supporting individuals and teams alike in staying organized and maximizing productivity. Whether you're a busy professional or a team collaborating on projects, the Calcom and PostgreSQL setup in Kubernetes offers an effective solution for optimized scheduling and data management.
