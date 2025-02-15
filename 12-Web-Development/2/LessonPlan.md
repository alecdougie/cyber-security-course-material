## 12.2 Lesson Plan: Microservices and Web Application Architecture

### Class Overview

In the preceding class, we took a close look at how the HTTP request and response communication framework works to relay information between a web server and client. We also learned how web servers and clients use cookies to establish sessions.

Today's class will look at the web application infrastructure that makes the web client&ndash;server model possible. Specifically, we will cover: 

- Why the original paradigm of monolith web application architecture evolved to the microservices model

- The different components of web applications

- Specific examples of web application components or "stacks"

- The deployment of web application architecture

- The database component of web applications and how to interact with data

### Class Objectives

By the end of class, students will be able to:

- Understand how microservices and architecture work to deliver more robust, reliable, and repeatable infrastructure as code.
- Define the different services within a LEMP stack.
- Deploy a Docker Compose container set and test the deployment's functionality.
- Describe how relational databases store and retrieve data.
- Create SQL queries to view, enter, and delete data.

### Instructor Notes

For the second half of the day, you will use Docker and Docker Compose to manage the activity's web application. 

- `docker-compose up` and `docker-compose down` instantiate container environments specific to the directory they're run in. 

- :warning: **Head's Up:** Don't forget to run `docker-compose down` whenever you are done working in a directory where you ran `docker-compose up`.

#### Docker and Docker Compose Resources

The following are useful Docker and Docker Compose commands and resources:

- [Get started with Docker](https://docs.docker.com/get-started/)

- [Overview of Docker Compose](https://docs.docker.com/compose/)

- [Remove a container volume](https://docs.docker.com/engine/reference/commandline/volume_rm/)

- [Remove Docker Compose volumes](https://docs.docker.com/compose/reference/rm/)

#### Check Docker Compose Status

To find running Docker Compose container names and statuses:

- Navigate to where a `docker-compose.yml` file exists. For example:

  - `cd ~/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_activity` 

- Then run `docker-compose ps` to check the statuses.

  - `docker-compose ps` will return the containers associated with the compose file.

- Alternatively, use `docker container ls` to find all running containers on the system.

#### Directories and Files

To prepare for this class, confirm that the following files are present on your Web Lab virtual machine:

- `/home/instructor/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_demo/docker-compose.yml`

- `/home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_activity/docker-compose.yml`

- `/home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases/docker-compose.yml`

If the above files are missing, it means your virtual machine is outdated and you need to update it. If your students' machines are outdated, they will need to update them too.


### Lab Environment   

<details><summary>Lab Details</summary>
<br>

You will use your local Web Lab virtual machine for today's activities. Please note that instructors and students have different access credentials.

  - Instructor access:
    - Username: `instructor`
    - Password: `instructor`

  - Student access:
    - Username: `sysadmin`
    - Password: `cybersecurity`
    

</details>

### Module Day 2 Contents

- [x] [01. Instructor Do: Review Application Structure](LessonPlan.md#01-instructor-do-review-application-structure-005)
- [x] [02. Instructor Do: Monolith to Microservices](LessonPlan.md#02-instructor-do-monolith-to-microservices-020)
- [x] [03. Student Do: Monolith to Microservices](LessonPlan.md#03-student-do-monolith-to-microservices-015)
- [x] [04. Instructor Review: Monolith to Microservices Activity](LessonPlan.md#04-instructor-review-monolith-to-microservices-activity-005)
- [x] [05. Instructor Do: Web Application Architecture](LessonPlan.md#05-instructor-do-web-application-architecture-015)
- [x] [06. Instructor Do: Deploy and Test a Container Set](LessonPlan.md#06-instructor-do-deploy-and-test-a-container-set-015)
- [x] [07. Student Do: Deploy and Test a Container Set](LessonPlan.md#07-student-do-deploy-and-test-a-container-set-015)
- [x] [08. Break](LessonPlan.md#08-break-015)
- [x] [09. Instructor Review: Deploy and Test a Container Set Activity](LessonPlan.md#09-instructor-review-deploy-and-test-a-container-set-activity-010)
- [x] [10. Instructor Do: Intro to Databases](LessonPlan.md#10-instructor-do-intro-to-databases-020)
- [x] [11. Student Do: Database Management](LessonPlan.md#11-student-do-database-management-025)
- [x] [12. Instructor Review: Database Management Activity](LessonPlan.md#12-instructor-review-database-management-activity-010)
- [x] [13. Instructor Do: Segue in SQL Injections](LessonPlan.md#13-instructor-do-segue-in-sql-injections-005)
- [x] [14. Everyone Do: Azure Personal Account Sign-Up](LessonPlan.md#14-everyone-do-azure-personal-account-sign-up)



### Slideshow  

The slides for today can be viewed on Google Drive here: 
[12.2 Slides](https://docs.google.com/presentation/d/1i_AcsQ2PZQo4lPr4S4hdmjJIZ7u-_dUS9p1PDPLvTC4/edit)

- To add slides to the student-facing repository, download the slides as a PDF by navigating to File > "Download as" and choose "PDF document." Then, add the PDF file to your class repository along with other necessary files.

- **Note:** Editing access is not available for these documents. If you or your students wish to modify the slides, please create a copy by navigating to File > "Make a copy...".

### Time Tracker

The time tracker for today's lesson can be viewed on Google Drive here: [12.2 Time Tracker](https://docs.google.com/spreadsheets/d/17TOcblJ-vKhVVMslUKDHU7BGGMb26qsDKBZ-KoA_axI/edit#gid=1145703143)

---

### 01. Instructor Do: Review Application Structure (0:05)

Welcome students and remind them that on Day 1, they investigated and analyzed the HTTP request and response process, as well as sessions and cookies. These concepts are important for understanding web application communication and identity paradigms. 

In today's class, we'll take a deeper look at the infrastructure behind web applications. Specifically, we'll look at:

- How modern web architecture has evolved to what is known as microservices

- What components make up microservices and their specific software "stacks"

- How web application components can be deployed using containers

- How databases work to understand how web application store and transmit data

In the next module, Web Vulnerabilities, we'll use this foundational knowledge of web application architecture and databases to examine how web attacks like SQL injections can lead to information breaches.

Today, we'll begin with how modern web applications ended up adopting the microservices model.

#### Microservices Overview

To understand why microservices exist, we need to cover the following:

- How an application and its components are organized
- How information flows between components of an application
- How the application's architecture has changed from monoliths to microservices
- How to deconstruct a monolith into microservices

#### Components of a Typical Web App

Let students know that we will look at how an application is constructed in order to understand the paradigm shift in modern web architecture.

Describe the following scenario to students:

- Andrew, a developer, uses a browser to manage a public-facing application (the Employee Directory App), where he retrieves and updates different kinds of employee lists of his company. The app is set up so that Andrew can add, remove, and view employees.

This app needs the following components to function:

-  A **front-end** server responsible for displaying webpages and styling them in a readable format. This server is also responsible for receiving and responding to HTTP requests.

- A **back-end** server for executing business logic and writing or reading corresponding data to and from a database. The back-end server knows how to interact with the database depending on the specific request received.

  - For example, if Andrew requests to add a new employee, the back-end server knows to create a new number (e.g., 109) for the employee and then save that information in the database. 
  
   - After this, the data is sent to the front end and formatted to display "New employee, Bob, created with employee ID, 109" in a new webpage.

- A **database** used to store employee information, such as their employee IDs and names. Critical and sensitive information is found in databases. We'll discuss this more in the second half of the class.

#### Information Flows Between Application Components

Now that we know the main components of a web application, we want to know what happens behind the scenes when a user interacts with a web application, or more specifically, makes an HTTP request to the server.

Let's see how information flows between application components when Andrew requests a list of all employees in the HR department.

- Display the following diagram to students and describe how the application components talk to each other:

  ![A diagram depicts the flow of information between components of an application.](./Images/12.2-information-flows.png)

  1. Andrew loads the application in his browser and clicks a button to see all HR employees.

  2. The front end forwards the HTTP request to the back end.
  
  3. A back-end script queries the database for HR employees.
  
  4. The database searches for all IDs containing "HR."
  
  5. The database sends IDs with "HR" to the back end.
  
  6. A back-end script forwards the list of HR employees to the front end.
  
  7. The front end prepares a new webpage listing all the HR employees.
  
  8. The browser displays a new page to Andrew, with a formatted list of HR employees.

Emphasize that each component of the web application serves one primary function, whether it's serving website data over HTTP or querying the database.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 02. Instructor Do: Monolith to Microservices (0:20)

Explain that understanding what components *do* in an application is key to understanding why microservices are so important in the modern architectural paradigm. 

First, we need to understand the original architecture type, known as **the monolith**, and its issues.

Define a monolith as any machine that hosts all the components required to serve a website or application. In other words, a monolith has the front-end server, back-end server, and database all on one machine.

For example, if Amazon used a monolithic server comprised of a front-end server, back-end server, and database, it would contain:

- A front-end HTML server: A GUI for customers to use when shopping.

- A back-end application server: This server shows inventory and stock and interacts directly with the database.

- A MySQL database: A database of customers, their information, and purchases.

Explain that the components of this machine are highly dependent on each other. If one component malfunctions, the application stops working. This presents a few problems:

- If the company needs to update any of the components&mdash;the front end, back end, or database&mdash;the entire server and all its components must be taken down. This creates long periods of downtime.

- If one component is compromised by a hacker, environmental issue, or human error, the entire machine is potentially compromised.

Explain that today's business standards expect companies to ensure availability by maintaining almost 100% uptime. Because of this, Amazon decides that the monolith architecture comes with too much risk and instead creates a more **modular** setup: a whole consisting of smaller and separate parts.

- Amazon needs to separate its components into different machines, so that system administrators and developers can deploy changes without taking entire applications down for extended periods of time.

- Separating an application's components into their own machines allows the sysadmin to update the front end, reboot it, and only have to verify the front-end components are working. They don't have to worry about the back-end components and database. If any components are compromised by a hacker, the potential damage is restricted to only that one component.

This new approach of separating application components into their own machines is called **microservices**.

#### Microservices

Remind students that so far, we've covered the typical components of an application and how the monolithic design causes maintenance and security issues. Now, we want to separate our components into different machines to implement microservice architecture.

Explain that in the following scenario, Amazon's sysadmins have separated and isolated the front-end, back-end, and database components into their own machines.

- Each of the smaller blocks represents a single, independent machine. Within each machine is a component that executes one primary function or **service**.

Together, these perform the same services as the monolithic server, but without the potential vulnerabilities.

#### Benefits of Microservices

The ultimate goal of microservices is flexibility through modularity, which has the following benefits:

- **Scalability and resiliency:** Replication of identical components allows you to serve more clients and provides identical backup components if one fails.

- **Rapid response:** Since microservice components are inherently smaller than monoliths, they can be replaced and updated quickly.
  - For example, an entire virtual machine might require 150 GB of total disk space. An individual component could have a maximum capacity of 100 or 200 MB. 

- **Isolated improvement:** Since microservices should be reduced to serving one primary function, they can be developed to optimize their functionality.
  - For example, developers working on an **application programming interface (API)** for storing employee data are developing a way to create new employee accounts more quickly. They'll be able to work directly on this API, without the need of a front end to view it. 
  
- **Isolated security:** One compromised component does not equal a compromised application.

#### Creating an API


Discuss the following scenario:

- When an Amazon customer wants to retrieve a list of the newest and most popular books, they don't go to the back-end MySQL server to check the inventory&mdash;they use the front-end microservice. The microservice communicates with the back-end server containing that data and brings it up.

- Customers do not have access to the back-end server. It is configured to only allow direct communication from the front end and does not allow direct communication from users.

- However, Amazon system administrators need to access and query the back end to update product information. Since they need to directly communicate with the back end, they must modify it to accept requests.

- Amazon software developers program the back end to receive&mdash;from sources other than the front-end server&mdash;HTTP requests to add, remove, and view product information.

Explain that in this example, the back-end server is an example of an API.

- An **API** is the implementation of new protocols or features onto an existing software application to alter the way that application is used or accessed.

- In the previous example, the software developers modified the back end to receive HTTP requests from sources other than the front end.

 We can call this back end the Product API.

Explain that the back-end server can now process HTTP requests and responses for product info. However, the front-end server still sends requests and responses for customers requesting product info over the open web as usual.

#### Finalizing New Components and Functions

We have turned our monolith into various microservices. Now we rename the front-end server and database to match their specialized services.  

- The front-end server provides the service of displaying the application to users through a browser, so we'll call it the Product Directory API. 

- The database stores product info, so we'll call it the Amazon Database.

Recap how we separated a monolith into microservices:

1. Separate each component of the monolith by function, moving it into its own machine.
2. Add communication between each microservice.
3. Turn the back-end server into an API to interact with more than just the front end.
4. Rename the rest of the component services to match their main functions.

Explain that microservice complexity and interconnectivity also come with unique security issues, which we'll cover in more depth later.

Let students know that they will need to repeat these steps in the upcoming activity.

#### Challenges of Microservice Scaling

A primary challenge of microservices is the increased complexity and required maintenance as the application and number of components grow.

- For example, suppose there are multiple directory apps for redundancy and one of the app services needs to be taken down for maintenance.

- Show the following example of microservices maintenance:

   ![A diagram depicts the many steps required to conduct routine maintenance on microservices.](./Images/12.2-challenges-of-microservices.png)

- To maintain the third app service, you have to ensure that no new clients are connecting to it, upgrade it, then re-establish its communications within the entire microservice deployment.

- This process is more complex than running a command to download and install all updates and then rebooting a monolithic server; however, it is faster. With the proper setup, it causes no service interruptions.

The solution is to set up a load balancer, which we will do later in the class. 

Let students know we'll now look at how to separate a monolith into microservices using the online diagramming tool draw.io.

#### Diagramming Microservices

In the following activity, students will review a diagram of a monolithic application and transition it into a microservice setup.

- As an example, show students the same application set up as a monolith and as a set of microservices:

  ![Diagrams depict the same application structured as a monolith and as microservices.](./Images/12.2-monolith-microservice.png)

Explain that if any component of the monolith becomes compromised, the entire application is compromised. Therefore, it is separated into the following components:

- A store app user interface (UI) to serve as the front-end service.
- A user API to serve as the back-end service.
- A user database.

To make these changes on a diagram, we:

1. Separate each component of the monolith by its function and make it its own machine.

2. Add communication between each part of the microservice.

3. Add the back-end server to an API to interact with more than just the front end.

4. Rename the rest of the component services based on the main function each provides.

Explain that in the following activity, students will use [draw.io](https://www.draw.io/) to diagram their own microservice setup. The online tool is similar to the Gliffy tool they've used in previous classes. 

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 03. Student Do: Monolith to Microservices (0:15)

Explain the following to students:

- In this activity, you will play the role of a systems engineer.

- Your company has a web store app that is becoming popular. 

- The store must switch its architecture so it can be more redundant and scalable. You decide to make the transition from traditional monolith to microservices.

- You have to design a microservices setup based on the current monolithic web store app diagram.

Send students the following file:

- [Activity File: Monolith to Microservices](./Activities/03_Monolith_to_Microservices/Unsolved/README.md)
- [Draw.io Diagram Template](./Activities/03_Monolith_to_Microservices/Unsolved/activity_one_unsolved.drawio)

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 04. Instructor Review: Monolith to Microservices Activity (0:05)

:bar_chart: Run a comprehension check poll before reviewing the activity. 

For this activity, students were tasked with developing a microservices version of an existing web store app in order to prepare for redundancy and scaling.

Send students the following file:

- [Solution Guide: Monolith to Microservices](./Activities/03_Monolith_to_Microservices/Solved/README.md)

#### Walkthrough

Explain that students should have a microservice diagram similar to the following:

  ![A diagram depicts the solution.](./Images/12.2-microservice-diagram.png)

The microservices include:

- A store app
- A user API
- An authentication API

You also split the monolithic database into three separate databases:

- A **user database** that handles all user information from the store app such as preferences and sessions

- A **credential database** that stores credential information that the **authentication API** will check user logins against

- An **inventory database** that gets updated whenever a user buys something from the store

The microservices connect to their corresponding databases in the following ways:

- The store app exchanges inventory info with the inventory database.

- The user API exchanges user info with the user database.

- The authentication API exchanges authentication info with the credential database.

Lastly, the APIs interact with the store app in the following ways:

- The user API forwards user info to the store app.
- The authentication API forwards authentication grants or denials to the store app.

#### Bonus Solution

For those who completed the bonus, you may have a diagram similar to the following:

![Monolith architecture that is broken up.](./Images/Activity_1_Solution.png)

In this diagram, we now have the additional microservices:

- Two replica store apps for redundancy and scale.
- A load balancer that has rules for balancing user sessions between the two replica store apps.

Explain new connections:

- The connections between the APIs and store app replicas remain the same, but now there are twice as many connections.

- You may have load reporting connections between the store apps and load balancer. These let the load balancer know which store app has less load for handling requests and responses.

- Lastly, the load balancer should have connections going to each store app that show it forwarding requests and responses.

Ask if students have any questions before proceeding.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 05. Instructor Do: Web Application Architecture (0:15)

Explain that in the last activity, we separated a monolith into microservices in order to understand modern web architecture. 

One of the first steps in creating microservices is separating the components into their own individual machines so that each one can run a "service."

A service, such as the front-end server from our earlier examples, is really just an operating system, running a minimum amount of software that has been configured to serve one main purpose, such as handle HTTP requests and responses.

This means that each individual machine requires:

- An operating system to run on in order to run the service's software and store its configurations.

- The software itself, which runs a specific set of instructions for that individual component of the web application.

  - For example, a database service may run Linux as its operating system and then have Microsoft's SQL Server installed on it.

Now we can explore what open-source and commercial software we need to set up to create our web application components.

#### Stacks

Any combination of a base operating system, front-end software, back-end software, and database is called a web **stack**. 

Which stack you run depends on the needs of your organization. For example, let's look at the well-known LAMP stack. This stack consists of: 

- Linux as the base operating system
- Apache to handle the frontend HTTP requests and responses
- MySQL for storing data
- PHP for back-end transformation of front-end requests and responses to database queries. (We'll look at database queries in our last activity.)

The LAMP stack is considered the foundational web stack, with a long history of use in architecting web applications. For example, the following sites either still use or originally used the LAMP stack:

- WordPress
- Facebook
- Tumblr
- Wikipedia
- Slack

:books: Provide the following URL to students if they are interested in learning more about the history of the LAMP stack:

  - [Tedium: The LAMP stack](https://tedium.co/2019/10/01/lamp-stack-php-mysql-apache-history/)

These days, there are many more web stacks that use different software. Note that the stack is simply a description of the software running in the web application. 

- You can technically have a monolith or microservices web application using the same software stack. 

- The difference is that monoliths have one operating system with all the software on it, and microservices have many smaller operating systems, each with the minimum amount of software needed for its own service.

But what stack do we want to use for our own web application?

#### Introduction to Common Web Architecture

Let's start by comparing the different operating systems available for our services.

- The [Alpine Linux](https://alpinelinux.org/about/) is one example. It is a super lightweight Linux distribution with the minimum requirements to run containers.

- Other container-friendly operating systems include most other Linux distributions, such as Ubuntu, and more recent versions of Windows Server. The following are base operating systems used for web applications:

  - Alpine Linux

  - Common Linux distros such as Ubuntu, Red Hat, and SUSE

  - Windows Server 2016 and higher

We also have the front-end server that handles the HTTP requests and responses. This is usually some form of HTTP server running on a lightweight, containerized operating system.

The front-end server is the part of a web application that renders the visual components of a web application. HTML, CSS, and JavaScript are the primary front-end web design languages. 

- The following are specific examples of front-end servers:

  - Apache 

  - nginx (pronounced "engine X")

  - IIS

Data for the application is housed in the database server. Remember that there could be multiple databases, some for storing sessions and cookies and some for storing business logic like a company's employee directory. The following are specific examples of databases:

  - MySQL

    - Note that you may also see MariaDB, which we will use in our activity. MariaDB is a community version of MySQL, created after Oracle acquired MySQL. MariaDB tries to be as close to MySQL as possible, but has an open-source license.

  - PostgreSQL

  - Microsoft SQL Server

  - CouchDB

  - MongoDB

Lastly, you usually need a back-end server that transmits data between the front end and the database. These servers run fully-featured scripting and programming languages.

- The following are specific examples of back-end servers and languages:

  - PHP

  - Perl

  - Python

  - nodeJS

#### The WIMP Stack

There is also a Microsoft-based variation called the WIMP stack that uses the following:

- Windows operating system

- Microsoft's IIS web server in place of Apache and nginx

- Database, such as Microsoft SQL Server

- Back-end language, such as PowerShell

We won't be using WIMP, but it is important to be aware of Microsoft-based web stacks.

- :books: Provide students with the following Wikipedia link for a brief overview of the WIMP stack:

  -  [Wikipedia: WIMP software bundle](https://en.wikipedia.org/wiki/WIMP_(software_bundle))


The web software stack that we'll be using for today's demos and activities consists of Linux, nginx, MariaDB, and PHP. 

This is known as the **LEMP stack**.

#### The LEMP Stack

What goes into the LEMP stack?

- Linux: The standard underlying operating system used for web applications. However, we will be using it with containers. We'll look at these more in a moment.

- nginx: We'll be using nginx for our front-end HTTP server instead of Apache, mainly for its speed. While Apache is considered to have more features and is more compatible with back-end languages, such as Java, nginx is well-known for its performance.

- MariaDB: Unofficially the "other" MySQL, it is a standard relational database that will handle our data storage.

- PHP: Our pages will be generated with data pulled by PHP scripts. We will not need to manage or work with any PHP directly today, but know that it is acting as our back-end language.

This set of Linux, nginx, MariaDB, and PHP is a variation of the LAMP stack we talked about earlier. 

We just covered all the software that we want to use for our web application. But what about the other side of web application architecture: the hardware?

- We need a hardware environment suitable for web application microservices that is both lightweight and easy to deploy. 

- For that, we can use virtualization. And for the purpose of microservices, we need the most lightweight virtual environment possible.

Let's quickly recap why we need a lightweight environment.

#### Microservices Infrastructure with Containers

Microservices require lightweight environments, because:

- Our microservices need to be rapidly deployable.
- We need to be able to scale our microservices to meet growing demand.
- Developers and maintainers need to be able to replicate their own copies of these microservices locally.
- Having full-sized virtual machines for each service would require more resources and be more costly.

:question: **Ask class:** Can anyone think of a technology we've covered in class that can create isolated virtual environments?

Explain that lightweight virtualization environments exist in the form of **containers**.

- Containers run as isolated, virtual operating systems that dynamically allocate resources depending on the container's needs. These are unlike regular virtual machines, where all the hardware is virtualized.

- Docker is the most popular container platform. For the rest of this lesson, we will use Docker's implementations of containers.

Explain that using containers is the primary way microservices are developed and will be the method we use to "miniaturize" the components of our web stack.

#### How a Container Becomes a Microservice

Explain that **containerization** is the process of packaging all the requirements to set up a microservice as a container.

Explain that containerizing a microservice does the following:

- Declares a base operating system for the microservice to run on.
- Stages the microservice's source code to the container.
- Sets a command that launches the microservice and all other needed software when the container is deployed.

Explain that this containerization process is declared in a simple text file called a Dockerfile.

- Dockerfiles contain all the configuration needed for a container in one file, similar to how an Ansible configuration file contains everything it needs to configure a host when you run the command `ansible-playbook your-playbook.yml`.

In the case of the Amazon Product microservices that we saw before, we would create a separate Dockerfile for each of the microservice components.

- Display the following sample of a Dockerfile:

 ```Dockerfile
 ###############################
 # Product Directory Application
 ###############################
 # Required Base OS
 FROM ubuntu:14.04
 ...[truncated]
 ```

- In this Dockerfile, Docker will install an Ubuntu 18.04 image to serve as a base operating system for the microservice.

- Other declarations in the Dockerfile set up the software and configuration required for the microservice. This varies depending on the service.

Explain that a unique Dockerfile is created for each microservice.

Students don't need to know how to construct or maintain a Dockerfile, but they should understand that these Dockerfiles can be used repeatedly to create and configure the same microservice set, similar to what Ansible playbooks do for Ansible.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 06. Instructor Do: Deploy and Test a Container Set (0:15)

While we know that we can set up a single container by using a Dockerfile, deploying containers one at a time can become tedious and unwieldy, especially if businesses require hundreds or thousands of microservices.

Therefore, we need to know how to deploy containers for large-scale environments. Specifically, we need to know how to:

- Deploy multiple _types_ of containers at the same time, e.g., front-end and database services.

- Set up a network for our containers so that they can communicate with each other.

- Preconfigure our containers, such as declaring the credentials for our web application's database.

These requirements are achieved with a tool called Docker Compose. Docker Compose can deploy and configure multiple containers at once. This means we don't have to micromanage multiple individual container instances.

#### Docker Compose Demo

Explain to students that in the upcoming demo, we will use Docker Compose to quickly deploy a web application comprised of multiple microservices.

We will then check our deployment in the browser to ensure that web clients can connect to it. Then we'll enter an interactive bash session into the database's container to ensure that it is up and running.

This will demonstrate how quickly containerized microservices can be deployed to a functional state.

For this web application deployment demo, we'll complete the following steps:

- Examine our YAML file for its current configurations.
- Launch our services with `docker-compose up`.
- Use our browser to verify that our front-end UI services are deployed properly.
- Enter a MySQL session to confirm proper deployment of our database service.

But first, we'll need to see how Docker Compose allows us to to create repeatable, multi-container deployments through its YAML-formatted configuration file.

#### The Docker Compose YAML File

Explain that Docker Compose uses YAML, a language used for building configuration files, to define the containers for a deployment, their networking configuration, and where you will copy files from your host machine into the container.

- Docker Compose also uses the same YAML file type to declare container configurations. These files are often saved as `docker-compose.yml`.

It isn't absolutely crucial for students to understand how a YAML file is constructed. But they will examine and edit one for their activity, so they will need to know where to find certain configurations.

#### Launch the Demo Deployment

**Instructor Note:** These initial steps of depicting a YAML file are displayed on the slides.

1. Explain that we will look at how this YAML file configures the UI (`ui`) and database (`db`): 
  
    - Using the corresponding slides, show students the following: 

      ```YAML
      version: "3.3"

      services:
        ui:
          container_name: demo-ui
          image: httpd:2.4
          ports:
            - 10000:8080
          volumes:
            - ./volume:/home
          networks:
            demo-net:
              ipv4_address: 192.168.1.2
        db:
          container_name: demo-db
          image: mariadb:10.5.1
          restart: always
          environment:
            MYSQL_DATABASE: demodb
            MYSQL_USER: demouser
            MYSQL_PASSWORD: demopass
            MYSQL_RANDOM_ROOT_PASSWORD: "1"
          volumes:
            - db:/var/lib/mysql
          networks:
            demo-net:
              ipv4_address: 192.168.1.3
      networks:
        demo-net:
          ipam:
            driver: default
            config:
              - subnet: "192.168.1.0/24"
      volumes:
        ui:
        db:
      ```

   - Explain that this is a simple YAML file. Students do not _need_ to know what each part of the file means, but we'll cover what they need for their activity.

2. Break down the YAML file by pointing out the services it installs.

    - The UI or front end and the database:

      ```YAML
      services:
        ui:
        db:
      ```

   - Explain that in this YAML file, the `ui` and `db` are our services. Each of these services are container configurations. Let's take a look at the first one:

      ```YAML
        ui:
          container_name: demo-ui
          image: httpd:2.4
          ports:
            - 10000:8080
          volumes:
            - ./volume:/home
          networks:
            demo-net:
              ipv4_address: 192.168.1.2
      ```

   - Cover the contents of this excerpt:

      - `container_name`: Specifies the name of the container. If not specified, Docker automatically names the container using the current directory and services name. This definition allows us to have explicable container names for when we use commands such as `docker exec`.

      - `image`: Points to where Docker Compose will grab the container image from Docker Hub. This will be Apache's `httpd` container. This is equivalent to `FROM ubuntu:14.04` from the Dockerfile we looked at earlier.

        - :books: Have students go to the following link and scroll to the section that explains that PHP can be installed on the `httpd` server to turn it into both an Apache and PHP server.
          - [Docker Hub: httpd](https://hub.docker.com/_/httpd)
      
      - `ports - 10000:8080`: The container's HTTP port is remapped from its default `80` port to `8080`, which is then forwarded, or made available, to the host's `10000` port. 
        - Allowing a container port to be accessible by a host port is called **port binding**.
      - `volumes: - ./volume:/home`: The local destination where the Apache server will save our configuration files.
      -  `networks: demo-net`: The network that this service will connect to. We'll take a look at this configuration in more detail in a moment.
      - `ipv4_address: 192.168.1.2`: The static IP address that we are assigning to this container, which we'll be able to load into our browser.
   
3. Now that we have an idea of how Docker Compose YAML files are constructed, let's see how `docker-compose` actually stands it all up.

   - Navigate to `/home/instructor/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_demo`.

4. Explain that the following command will find a `docker-compose.yml` file in the current directory and spin up the containers configured within it.

   - Run `docker-compose up`. When the containers are ready, you should see the following output:

      ```bash
      demo-ui | 192.168.1.1 - - [29/Sep/2020:15:38:49 +0000] "GET / HTTP/1.1" 200 45
      demo-ui | 192.168.1.1 - - [29/Sep/2020:15:38:49 +0000] "GET /favicon.ico HTTP/1.1" 404 196
      ```

   - Point out that Docker Compose's execution is now taking over the terminal.

   - `docker-compose up` will look for a `docker-compose.yml` file in the current directory and deploy it.


5. Let's verify everything worked by checking the webpage. 

   - Open Firefox and navigate to `192.168.1.2`, which is the IP address we assigned to our recently created container.

     - When you navigate to it, you should be greeted with a webpage that says, "It works!" Refresh the page.

   - Return to the terminal that is running `docker-compose` to show that there are indeed HTTP GET requests received by our `ui` service.

   - Explain that for their activity, students will need to investigate their YAML file and verify that their application's deployment works in the browser.

6. Let's move on to the database service definition in the YAML file. 

    - Reiterate that it is not essential that students understand and create services on their own, but they should understand what the different declarations mean.

      ```YAML
        db:
          container_name: demo-db
          image: mariadb:10.5.1
          environment:
            MYSQL_DATABASE: demodb
            MYSQL_USER: demouser
            MYSQL_PASSWORD: demopass
            MYSQL_RANDOM_ROOT_PASSWORD: "1"
          volumes:
            - db:/var/lib/mysql
          networks:
            demo-net:
              ipv4_address: 192.168.1.3
      ```

    - Break down the contents of this definition: 

      - `demo-db`: The name of our container
      - `image: mariadb:10.5.1`: The container image and version we'll be using (MariaDB database version 10.5.1)
      - `environment`: Contains the setup of the MySQL server
      - `MYSQL_DATABASE: demodb`: The name of the database
      - `MYSQL_USER: demouser`: The default user for the MySQL database
      - `MYSQL_PASSWORD: demopass`: The password for the user
      - `MYSQL_RANDOM_ROOT_PASSWORD: "1"`: Gives the root user a random password for security purposes
      - `volumes: - db:/var/lib/mysql`: The location where we are saving our configuration files
      - `networks`: Using the same network (`demo-net`), assigns this database a static IP address

    - Explain that the top-level `networks` is an application-wide configuration that can be accessed by each service.

7. Now, we'll check the `db` service deployment.

    - In a new terminal, navigate back to the `/home/instructor/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_demo/` directory.

- First, we need to get the name of our database container:
    
    - Run `docker container ls`.
    
    - This command lets us see the names of our containers. Point out the `demo-db` container result.
    
    - Run `docker exec -it demo-db bash`.
    
      - This command lets us enter an interactive bash session in our containers. We have seen this command before.
    
      -  Notice the prompt now includes `root`, which signifies our new shell session.

8. Open a new terminal and display the contents of the `docker-compose` file. (Alternatively, point to the corresponding slide if you have too many terminal windows open.)

    - `cat /home/instructor/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_demo/docker-compose.yml`

  ![YAML information.](Images/YAML2.png)

   - Explain that we can find declared database credentials in the YAML file under the `environment` subheading.

    ```YAML
      db:
        container_name: demo-db
        image: mariadb:10.5.1
        restart: always
        environment:
          MYSQL_DATABASE: demodb
          MYSQL_USER: demouser
          MYSQL_PASSWORD: demopass
          MYSQL_RANDOM_ROOT_PASSWORD: "1"
        volumes:
          - db:/var/lib/mysql
        networks:
          demo-net:
            ipv4_address: 192.168.1.3
    ```

9. Navigate back to the container bash session and type `mysql -u demouser -pdemopass` to enter the database.

   - This command lets us use the username `demouser` found in our YAML file.

   - The `-p` parameter denotes a password, and we will use the `demopass` password declared in our YAML file.

   - If the prompt changes to `MariaDB`, this confirms we're now in a successfully deployed MariaDB database.

     - Notice the prompt shows up as `MariaDB [(none)]>`. The `(none)` means that we have no actual database within MariaDB selected. We'll see how to define this in an upcoming activity.

10. Explain to students that if they want to bring the container set down, they can press Ctrl+ C in the terminal where we ran `docker-compose up`.

    - Demonstrate running `docker-compose down` in that same terminal to bring down the container set configuration.

In the next activity, students will take this one step further. They will:

- Deploy their application

- Ensure that it is running and functional

- Take down their web application and make a few modifications to the YAML file

- Bring up their application again and check to make sure their modifications worked

This activity emphasizes how easily and quickly we can deploy and redeploy web applications via containerized microservice environments.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 07. Student Do: Deploy and Test a Container Set (0:15)

Explain the following:

- In this activity, you will act as a DevOps engineer overseeing the process of standing up a container set for your company using Docker Compose.

- The risk management team recently approved the use of the WordPress container in the organization's cloud infrastructure.

- You are tasked with locally deploying multiple containers with Docker Compose and running tests to verify the functionality of the containers. You also need to edit the Docker Compose file and test the results.

Send students the following files:

- [Activity File: Deploy and Test a Container Set](Activities/07_Docker_Compose/Unsolved/README.md)
- [Docker Compose File](Activities/07_Docker_Compose/Unsolved/docker-compose.yml)

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 08. Break (0:15)

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---


### 09. Instructor Review: Deploy and Test a Container Set Activity (0:10)

:bar_chart: Run a comprehension check poll before reviewing the activity. 

This activity required students to use Docker Compose to deploy a container set and confirm functionality.

Completing this required the following steps:

- Run `docker-compose up` to run the compose YAML configuration file.
- Check that the WordPress site runs in the browser.
- Use an interactive bash session to test the database's credentials.
- Edit the `docker-compose.yml` configuration so that our WordPress site is available through `192.168.1.2`.

Send students the following solution file:

- [Solution Guide: Deploy and Test a Container Set](Activities/07_Docker_Compose/Solved/README.md)

#### Walkthrough 

1. First, deploy the microservices (this should be done already, but the following contains the students' instructions):

    - Navigate to your `/home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_testing_activity` directory.

  - Deploy the WordPress stack with `docker-compose up`.
    
    - Verify the site is running by navigating to `192.168.2.2` in the browser.

2. In a new terminal window, verify that the application runs properly by completing the following:

    - Use an interactive bash session to enter the container `docker exec -it db bash`. 

    - Verify that the MySQL credentials provided in the `docker-compose.yml` file are functional with `mysql -u [username] -p[password]`.

      - Read the `docker-compose.yml` file to find the username and password. 
      
      - Run `myql -u demouser -pdemopass`.

    - Exit the MySQL session, exit the interactive bash session, and press Ctrl+C in the other launch terminal to stop the Docker Compose stack.

3. Change the IP address and redeploy:

    - Make sure your deployment configurations are cleared with `docker-compose down`.

    - Exit the MySQL session by entering `exit`, exit the interactive bash session, and press Ctrl+C in the terminal where you ran `docker-compose up` to stop the Docker Compose stack.

      ```YAML
        ui1:
          container_name: wp
          image: httpd:2.4
          ports:
            - 10001:8080
          volumes:
            - ./volume:/home
          networks:
            demo-net:
              ipv4_address: 192.168.2.200
      ```

    - Redeploy the stack with `docker-compose up`.

    - Open your browser and navigate to `192.168.2.200` to see the new mapped IP address working!

Ask students if they have any questions before moving onto databases.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 10. Instructor Do: Intro to Databases (0:20)

:warning: **Head's Up:** This demo, activity, and review contain important concepts that will be built on in the upcoming Web Vulnerability module. 

Let's recap everything we've learned so far today:

- How to separate a monolith into microservices
- How to describe web application architecture
- Defining specific web application architectures
- How to deploy and test that a container set is running and functional

Now that we have easily deployable microservice-based web applications, we're going to cover one of the most critical components of a web application: the database.

Databases are critical to web application architecture because they contain the persistent data that flows through the web application. The data in the database can include but isn't limited to:

- The usernames, telephone numbers, and email addresses of customers.

- The session and cookie IDs of site visitors.

And even more critically, a database can have personally identifiable information (PII), such as the full names, dates of birth, credit card numbers, and social security numbers of customers.

For these reasons, it is absolutely crucial that security professionals have a strong understanding of how databases work in web applications.

It is also worth noting that our understanding of databases will be the foundation of our exploration of web vulnerabilities in an upcoming module. 


#### Databases Overview

Summarize the following about databases:

- Databases are used to store large amounts of data.

- Databases are typically kept separate from the other components of a web application.

  - This is for reasons related to both security (compromise of one machine does not imply compromise of the other) and scale (many servers can use the same database). 

As we saw in our last demo and activity, this was the case in our `docker-compose.yml` file.  We had multiple defined services, and the database was its own container `demo-db` in the demo and `db` in the activity.

#### Database Types

Let students know that there are many kinds of databases, but that the most important for our purposes are SQL and NoSQL databases.

- We won't discuss NoSQL databases in class, but emphasize that the techniques covered today only work for SQL databases.

Explain that SQL databases organize data like a spreadsheet:

- Each row is an item in the database and each column is a piece of data in the row.

- A whole "spreadsheet" of rows and columns is called a **table**.

- A collection of tables is called a database.

  ![A database table showing columns and rows.](Images/sql_table.png)

Once you've created a table, there are four main ways to interact with the data it contains:

- **Create** or add new entries. When a user makes a new account in a web app, they create a new database entry with their user info.

- **Read** or view entries. When a web application verifies your login credentials, it is reading the saved credentials it has in the database.

- **Update** or modify existing data. Whenever you need to reset your password in a web application, the password entry (more specifically, the hashed password) is updated with the new password.

- **Delete** or destroy data. If you have the option to delete your account from a web application (e.g., on a GDPR web app), your account info is deleted from the database.

Together, these are as known as **CRUD operations**. These operations are also known as **queries**. 

- We'll use the term query to describe any sort of input that interacts with data.

Let students know that we'll discuss the SQL syntax for these operations to set the stage for studying **SQL injections**. 

- SQL injections are a type of web application attack intended to manipulate queries so that an attacker can use a database in ways the developers did not originally intend.

#### Database Demo

Now that we understand the high-level concepts of database operations, let's see how we can create and enter queries into a web application's database to carry out basic database administration tasks. 

We'll be doing the following database administration tasks in this demo:

- Deploy a web application.
- Navigate to the web application's page to see what data can be viewed by a web client.
- Start a bash session in the database's container and log into the database.
- Use a SQL query to retrieve the contents of the database's primary table.
- Modify that SQL query to find specific data.
- Add new data to the database.
- Delete data from the database.

Let's get started.

1. First, we'll navigate to our application's container set directory and stand it up. 

   - Run the following in a terminal:

      - `cd /home/instructor/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases`

   -  Explain that this directory contains a script called `reset_databases.sh` that will set up the database for this demo. The script will also reset the database back to its original state if, at any point, the wrong SQL query is used.

   -  Students have the same script in their `/home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases` directories.

     - Run the script with `./reset_databases.sh`.

     - Then bring up the app with `docker-compose up`.


2. We should be able to see our deployed web app now:

   - Open Firefox and navigate to `127.0.0.1:10005` to show the GoodCorp Employee Directory page.

   - Scroll down the page and explain that the employee entries here are being read from a database.

3. Open a new terminal window and enter an interactive bash session in the container:

    - `docker exec -it activitydb bash` and the prompt should change to `root@<containerID>`.

    - We should be familiar with how to enter an interactive bash session in a Docker container. 

4. Explain that we're going to enter a MySQL session like earlier, but this time, we will also add the `-D` argument to specify a database to use.

   - Run `mysql -u admin -p123456 -D goodcorpdb`.
   
   - The prompt changes to `MariaDB [goodcorpdb]`.

   - Emphasize that students should never use such an obvious username and password combination.


5. **`SELECT` queries:** Explain that, in this database, we have a table called `employees` that has the list of employees we saw on the webpage earlier. To find all the entries in this table, we can use what is known as the `SELECT` statement to create a query that returns all the entries from the `employees` table. 

    - While in the MySQL session, run `SELECT * FROM employees;`.


     :warning: **Head's Up:** Always remember to end your queries with a semicolon `;` or your database will expect more SQL.

   - Run `SELECT * FROM employees;` to show all the employees we saw earlier:

      ```SQL
      MariaDB [goodcorpdb]> SELECT * FROM employees;
      +----+-----------+-----------+-------------------------+--------------------------+---------------------+
      | id | firstname | lastname  | email                   | department               | date_added          |
      +----+-----------+-----------+-------------------------+--------------------------+---------------------+
      |  1 | Bob       | Brew      | bbrew@goodcorp.net      | Sales and Marketing      | 2020-09-16 11:00:44 |
      |  2 | Andrew    | Americano | aamericano@goodcorp.net | Research and Development | 2020-09-16 11:00:44 |
      |  3 | Caroline  | Cortado   | ccortado@goodcorp.net   | Human Resources          | 2020-09-16 11:00:44 |
      |  4 | Deborah   | Doppio    | ddoppio@goodcorp.net    | Operations               | 2020-09-16 11:00:44 |
      |  5 | Emma      | Espresso  | eespresso@goodcorp.net  | Research and Development | 2020-09-16 11:00:44 |
      +----+-----------+-----------+-------------------------+--------------------------+---------------------+
      5 rows in set (0.000 sec)   
      ```

   - We can see that we have five employees in this table and that they are organized by their employee **ID**, **first name**, **last name**, **department**, and the **date** and **time** they were added to the database.

6. **`WHERE` clause:** Explain that sometimes we want to narrow down results when searching through a database, which we can do by using the `WHERE` clause. We can append the `WHERE` clause to queries to narrow down and modify what it is doing. `WHERE` acts as a conditional statement that will return database results when it is met.

   - In this example, we use `WHERE` to find all employees in the Operations department. To do so, we're going to specify that when we use `SELECT * FROM employees`, we only want the rows where the `department` is equal to `'Operations'`:

   - Run `SELECT * FROM employees WHERE department='Operations';`:

      ```SQL
      MariaDB [goodcorpdb]> SELECT * FROM employees WHERE department='Operations'
          -> ;
      +----+-----------+----------+----------------------+------------+---------------------+
      | id | firstname | lastname | email                | department | date_added          |
      +----+-----------+----------+----------------------+------------+---------------------+
      |  4 | Deborah   | Doppio   | ddoppio@goodcorp.net | Operations | 2020-09-16 11:00:44 |
      +----+-----------+----------+----------------------+------------+---------------------+
      1 row in set (0.001 sec)
      ```

   - Using `WHERE` to modify a SQL query is necessary when dealing with databases with huge amounts of data.

7. **`INSERT INTO` queries:** If we want to add a new employee to our database, we can use the `INSERT INTO` query. 

   - This query is used to add new data to a database and takes the format of:

    ```SQL
    INSERT INTO table_name (column1, column2, column3, ...)
    VALUES (value1, value2, value3, ...);
    ```

    - Construct a query using this format. Enter the following:

      ```SQL
      INSERT INTO employees (firstname, lastname, email, department)  
      VALUES ('Luke', 'Latte', 'llatte@goodcorp.net', 'Logistics');
      ```

        - Explain that we are not entering column values for `Id` or `date_added` because they are automatically incremented when we enter a new row.

        - Run the query to show the `Query OK, 1 row affected (0.001 sec)` output, confirming a successful `INSERT` query.

    - Now we'll check the entire table again with `SELECT * FROM employees;` to see our new employee, Luke, at the bottom of the table:

        ```SQL
        MariaDB [goodcorpdb]> SELECT * FROM employees;
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        | id | firstname | lastname  | email                   | department               | date_added          |
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        |  1 | Bob       | Brew      | bbrew@goodcorp.net      | Sales and Marketing      | 2020-09-16 11:00:44 |
        |  2 | Andrew    | Americano | aamericano@goodcorp.net | Research and Development | 2020-09-16 11:00:44 |
        |  3 | Caroline  | Cortado   | ccortado@goodcorp.net   | Human Resources          | 2020-09-16 11:00:44 |
        |  4 | Deborah   | Doppio    | ddoppio@goodcorp.net    | Operations               | 2020-09-16 11:00:44 |
        |  5 | Emma      | Espresso  | eespresso@goodcorp.net  | Research and Development | 2020-09-16 11:00:44 |
        |  6 | Luke      | Latte     | llatte@goodcorp.net     | Logistics                | 2020-09-16 11:29:00 |
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        6 rows in set (0.000 sec)
        ```

    - Return to Firefox and refresh the page to see how it shows up on the employee directory page.

      - Go back to Firefox and refresh the page to see the new employee listed at the bottom.

8. **`DELETE` queries**: To delete the entry we just created, we can use a `DELETE` query. We'll want to use this together with the `WHERE` clause to specify deleting only a single entry. 

   - Demonstrate the following command:

      - `DELETE FROM employees WHERE email='llatte@goodcorp.net';` and point out the `Query OK` output.

   - :warning: **Head's Up:** You never want to enter a query like `DELETE FROM employees;` as it will delete the entire `employees` table! Take a moment to explain:

      - If attackers gain access to a database, they may use `DELETE` to maliciously wipe out thousands or even millions of records, resulting in significant impact to a business's operations.

    - Let's return to using `SELECT` to verify that our deleted user is no longer listed in the database.

     - `SELECT * FROM employees;` to show that we're back down to five employees:

        ```SQL
        MariaDB [goodcorpdb]> SELECT * FROM employees;
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        | id | firstname | lastname  | email                   | department               | date_added          |
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        |  1 | Bob       | Brew      | bbrew@goodcorp.net      | Sales and Marketing      | 2020-09-16 11:00:44 |
        |  2 | Andrew    | Americano | aamericano@goodcorp.net | Research and Development | 2020-09-16 11:00:44 |
        |  3 | Caroline  | Cortado   | ccortado@goodcorp.net   | Human Resources          | 2020-09-16 11:00:44 |
        |  4 | Deborah   | Doppio    | ddoppio@goodcorp.net    | Operations               | 2020-09-16 11:00:44 |
        |  5 | Emma      | Espresso  | eespresso@goodcorp.net  | Research and Development | 2020-09-16 11:00:44 |
        +----+-----------+-----------+-------------------------+--------------------------+---------------------+
        5 rows in set (0.000 sec)
        ```

    - For visual confirmation via the employee directory, reload the webpage to see that the entry is now gone.

Let students know that they'll be using these same concepts for their activity.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 11. Student Do: Database Management (0:25)

In this activity, you will play the role of a junior web engineer for the GoodCorp company and will manage its web application.

- GoodCorp uses Docker Compose and a set of containers to deploy and maintain its employee database website and application.

- You are tasked with locally deploying GoodCorp's employee directory website with Docker Compose. You also need to manage the data inside the employee directory database.

Send students the following activity file:

- [Activity File: Database Management](Activities/11_Database_Management/Unsolved/README.md)

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 12. Instructor Review: Database Management Activity (0:10)

:bar_chart: Run a comprehension-check poll before reviewing the activity. 

Explain that, to complete this activity, students had to run multiple SQL queries to maintain the employee directory database for GoodCorp.

Completing this required the following steps:

- Run `docker-compose up` to run the compose YAML configuration file.
- Use an interactive bash session to enter the database's container.
- Log into the MySQL database.
- Run queries to retrieve and change information in the database.

Send students the following solution file:

- [Solution Guide: Database Management](Activities/11_Database_Management/Solved/README.md)

#### Walkthrough

1. First, deploy the container set using Docker Compose:

    - `cd /home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases` directory. 
	
    - Run `docker-compose up`.

    - Open Firefox and go to `http://127.0.0.1:10005` in the browser.

2. Find the MySQL credentials in the `/home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases` compose file. 

    - We can check the file with `cat /home/sysadmin/Cybersecurity-Lesson-Plans/12-Web_Dev/deploying_databases/docker-compose.yml`. 

    - We want to use the credentials in the `docker-compose.yml` file:

      ```YAML
      MYSQL_USER: admin
      MYSQL_PASSWORD: 123456
      ```

3. Enter an interactive bash session in the database's container. The container name can also be found in the compose file.

   - Run `docker exec -it activitydb bash` to enter an interactive bash session in the MySQL container.

4. Within the interactive bash session, use the credentials found earlier to enter a MySQL session using the `goodcorpdb` MySQL database.

    - Enter `mysql -u admin -p123456 -D goodcorpdb` to enter a MySQL session.

5. Create a basic `SELECT` query to find all the employee table entries in the `goodcorpdb` database.

    - While in the MySQL session, enter `SELECT * FROM employees;` to retrieve all the entries in the employee table.

6. Using the given information, add the following new user to the employee directory:

    - **First name**: Fran
    - **Last name**: Frappucino
    - **Email address**: ffrappucino@goodcorp.net
    - **Department**: Finance

7. Enter the following query to add the new employee:

     ```SQL
      INSERT INTO employees (firstname, lastname, email, department)  
      VALUES ('Fran', 'Frappucino', 'ffrappucino@goodcorp.net', 'Finance');
     ```

    - Reload the webpage to see the changes.

8. Create a modified `SELECT` query to find all employees in the Research and Development department.

    - While still in the database, run the following query to see all the employees in the Research and Development department:

      - `SELECT * FROM employees WHERE Department = 'Research and Development';`

9. Create a `DELETE` query to remove the entry around Bob.

    - Run the following query to remove Bob via their **Id**:

      - `DELETE FROM employees WHERE Id='1';`

    - Then rerun the SELECT * query to see the new employee table:

      - `SELECT * FROM employees;`

    - Lastly, refresh the webpage to see that the entry around Bob has been deleted.

:question: **Ask the class:** Why do you think we shouldn't just delete the user by the first name "Bob"?

  - **Answer:** Because there may be tens or hundreds of entries in a database that include the first name Bob.

  - Every database requires a unique identifier for each entry and in our case, it's `Id`.

This covers the basic operations and concepts for dealing with relational MySQL databases. 

It's important for security professionals to understand these database concepts, since they directly inform how database vulnerabilities and exploits work.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 13. Instructor Do: Segue in SQL Injections (0:05)

Explain to students that before ending our lesson on databases, we're going to look at some queries that may seem pointless or improperly created but are actually fundamental to how SQL injections work.

- `SELECT * FROM employees WHERE 1=1;`

:question: **Ask the class:** Does anyone know what will happen when this query is run?

- **Answer:** The `1=1` part of the statement will evaluate to true since the number one always equals one, therefore, running the `SELECT * FROM employees` statement.

- Run the query to demonstrate retrieving the entire `employees` table again.

This seems like a pointless condition for the `WHERE` clause, because we can simply use `SELECT * FROM employees`. However, creating a statement that results in being true is one way that SQL injections work.

:question: **Ask the class:** During the previous activity, did anyone forget to add the semicolon to the end of a query?

- Type `SELECT * FROM employees` without a semicolon and press Enter a few times. 

  - Point out that it does not do anything. The database is still waiting for more SQL.

    ```SQL
    MariaDB [goodcorpdb]> SELECT * FROM employees 
        -> 
        -> 
        -> 
        -> 
    ```

Explain to students that this expectation of explicit `;` endings can be leveraged in SQL injections. 

- We'll go into much more depth on exploiting databases in a following module, which will focus much more on offensive security and builds directly on this module's lessons.

:books: Send the students the following resources as supplemental reads on offensive-security definitions of ethical hacking and penetration testing:

  - [Synopsys: Ethical hacking](https://www.synopsys.com/glossary/what-is-ethical-hacking.html)
  - [Rapid7: Penetration testing](https://www.rapid7.com/fundamentals/penetration-testing/)

Summarize that this week's module showed students how web applications are intended to be used.

Wrap up the lesson and answer any questions.

[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

### 14. Everyone Do: Azure Personal Account Sign-Up 

-  Explain that for the upcoming Cloud Security and Project Week modules, students will need their own individual Azure accounts. They will **not** use the cyberxsecurity accounts. 

   - Students will spend the remainder of class (as well as office hours time if needed) signing up for these accounts. 
      
   - Distribute the following instructions if needed: [Personal Azure Account Setup Guide](https://docs.google.com/document/d/1gs_09b7eotl7hzTL82xlqPt-OwOd0aWA78qcQxtMr6Y/edit) 
   
   - Make sure all students are set up prior to the next class. 


[<- Back to Module Contents](LessonPlan.md#module-day-2-contents)

---

&copy; 2023 edX Boot Camps LLC. Confidential and Proprietary. All Rights Reserved.  
