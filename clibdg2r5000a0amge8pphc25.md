---
title: "Odyssey of the big data processing"
datePublished: Wed May 31 2023 07:14:01 GMT+0000 (Coordinated Universal Time)
cuid: clibdg2r5000a0amge8pphc25
slug: odyssey-of-the-big-data-processing
tags: azure, big-data, apache-spark, databricks

---

Recently I started using Azure Databricks and I got into a rabbit hole of this world so here are some clarifictions of questions we have in mind but too shy to ask so that we don't appear ignorant

# What is big data processing engine ?

A big data processing engine is a software system that is designed to analyze and process large volumes of data. These large volumes of data come from multiple sources and can consist of structured, semi-structured, and unstructured data. A big data processing engine is typically used to perform various tasks such as data ingestion, data preparation, data analysis, data visualization, and more.

Some examples of big data processing engines include Apache Hadoop, Apache Spark, Apache Flink, and Apache Beam. These processing engines use distributed computing to distribute the processing of the data across a large number of nodes, which allows for the processing of large volumes of data quickly and efficiently. They can also integrate with other big data tools and technologies, such as databases and data warehouses, to enable seamless data processing and analysis.

# What is Apache ?

Apache is an open-source organization that provides a variety of web server and software products that are free to use and distribute. It is also known as the Apache Software Foundation (ASF) and was created in 1999. The ASF has been at the forefront of web technology for over two decades and has developed a reputation for providing high-quality, reliable, and secure software.

Since its inception, the ASF has been committed to the development of open-source software that is freely available to users worldwide. The ASF has over 300 projects that vary from web servers to applications, machine learning tools, and more. Some well-known Apache projects include Apache HTTP Server, Tomcat, Kafka, Maven, and Hadoop. These are just a few examples of the vast range of software projects that the ASF has taken on over the years.

One of the main reasons why Apache is so widely used is that it is open-source. This means that the software source code is available for anyone to access, use, and modify. This provides developers with a lot of flexibility to customize the software to their specific needs. Additionally, the open-source software is scrutinized by many developers worldwide, which leads to the development of more secure, stable, and efficient software over time.

Apache has a very diverse community of developers from around the world, who contribute to the projects in different ways. Some developers contribute by writing code, implementing new features, or fixing bugs. Others contribute by writing documentation, testing the software, or providing support to other developers or users. This diversity allows for the development of software that is comprehensive and can be used in multiple languages and platforms.

The Apache HTTP Server is the most prominent project of the Apache Software Foundation. It is an open-source web server that is widely used worldwide. According to Netcraft, as of February 2021, Apache is used by 26% of websites on the internet, making it the most popular web server in the world. Apache HTTP Server provides a stable, secure, and scalable platform for websites and web applications. It supports many programming languages, such as PHP, Python, and Perl, and can run on multiple operating systems like Linux, Unix, and Windows.

Another project of the ASF is Tomcat. Tomcat is a web application server that provides a container to run Java web applications. It supports Java Servlet, JavaServer Pages (JSP), and WebSocket. Tomcat provides an environment to run web applications developed using Java and can work with other Apache projects, such as Apache Struts, to produce full-stack web applications.

Kafka is another popular Apache project. It is a distributed streaming platform that allows developers to build real-time data pipelines. Kafka can handle thousands of events per second and process them in real-time. It provides a scalable, fault-tolerant, and durable platform for real-time processing of data. Kafka can be used for various use cases such as streaming analytics, event sourcing, and fraud detection.

Maven is a software project management tool that is also an Apache project. It is used to manage software projects, build them, and centralize all the dependencies and plugins required by the project. Maven uses a declarative XML-based configuration file to describe the project's dependencies, build process, and test cases. It then downloads all the required components and plugins and manages them efficiently.

But today we are diving deep into Apache Spark.  

# What is Apache Spark ?

Apache Spark is an open-source, distributed computing system that was developed to work with Big Data. It is designed for processing massive amounts of data through a fault-tolerant and distributed architecture. The project was originally developed at the University of California, Berkeley's AMPLab in 2009, and then later became an Apache project in 2013, under the stewardship of the Apache Software Foundation.

One of the primary reasons why Big Data processing is challenging is the volume, variety, and velocity of data being produced and collected. The data is often structured, semi-structured, or unstructured and stored in different locations. Apache Spark simplifies the task of processing Big Data by providing a unified, fast, and reliable solution that enables data processing in real-time.

Apache Spark provides a variety of tools and libraries that allow for distributed data processing, machine learning, graph processing, and streaming. It is built on the concept of a Resilient Distributed Dataset (RDD), which is an immutable data structure that is distributed across a cluster of machines. The RDDs are resilient because they can recover automatically from node failures and distributed because they compute in parallel across a cluster.

Additionally, Apache Spark provides a general-purpose execution engine that operates in memory, which means it can handle iterative algorithms that process data multiple times. For example, it can parallelize computations for machine learning algorithms, graph algorithms, and SQL-based queries. The in-memory data processing engine enables fast data processing by minimizing the need to access data from the disk, which is much slower than in-memory computation.

Apache Spark has a collection of libraries that provide additional functionality on top of the core engine. These include:

1. Spark Streaming: It enables processing of real-time data streams and integrates with other libraries like Kafka, Flume, and Amazon Kinesis.
    
2. Spark SQL: It brings SQL queries to Spark RDDs and enables users to apply SQL-like functions and commands on distributed data.
    
3. GraphX: It is a library for graph processing that provides distributed algorithms for graph processing and parallel graph computation.
    
4. MLlib: It is a library for machine learning that provides distributed implementation of data mining algorithms like clustering, regression, dimensionality reduction, and collaborative filtering.
    

Overall, Apache Spark provides a powerful platform for distributed computing that simplifies the processing of Big Data. The platform integrates with other tools and libraries to enable real-time and iterative processing of data in large data sets. The key benefits of using Apache Spark are:

1. It allows for faster data processing: Apache Spark is built for speed, and it can process data much faster than other distributed computing systems working with Big Data. By using in-memory computing, the system reduces access and response times for processing data, making it ideal for real-time analysis.
    
2. It Provides scalability for processing and analysis: Spark can handle data sets that grow large and cannot fit into an individual machine's memory. With its distributed architecture, it can handle large volumes of data seamlessly by breaking it down into smaller chunks, which are distributed across multiple machines in a cluster.
    
3. It offers a simple, easy-to-use programming model: Apache Spark offers a simple programming model that can be implemented using various programming languages like Java, Python, Scala, and R. This simplicity of use enables data analysts and developers to take advantage of Spark's advanced analytical capabilities easily.
    
4. It provides support for multiple data sources: The Apache Spark ecosystem connects to different file formats, including Parquet, JSON and CSV. This provides versatility when it comes to retrieving data from various sources, making Spark a valuable tool for data mining and analysis.
    
5. It offers support for streaming data: Apache Spark's real-time processing capabilities ensure that streaming data is processed as quickly as possible. This ensures that users can take advantage of the latest data as it flows into information systems for analysis.
    

# Isn't the engine suppoused to be hosted on a cloud service ?

No, a big data processing engine can be hosted on a variety of platforms, including on-premises infrastructure, cloud-based infrastructure, or a hybrid of both.

In fact, cloud-based infrastructure has become an increasingly popular deployment option for big data processing engines in recent years due to benefits such as scalability, flexibility, and cost efficiency.

Cloud-based platforms like Amazon Web Services (AWS), Microsoft Azure, and Google Cloud Platform (GCP), offer a range of different big data processing services that organizations can use to process and analyze large volumes of data without having to invest in and manage their own infrastructure. These cloud-based services provide access to fully managed instances of popular big data processing engines like Apache Hadoop, Apache Spark, and Apache Flink, amongst others.

# So is Spark a framework or an engine ?

Apache Spark is both a framework and an engine for big data processing and analytics.

At its core, Apache Spark provides a distributed computing engine that allows data processing tasks to be run in parallel across a large number of computers or nodes. This engine is responsible for scheduling and executing tasks on the nodes, managing the distribution of data across the nodes, and ensuring fault tolerance and resilience in the face of node failures.

On top of this distributed computing engine, Spark provides a set of APIs and libraries that allow developers to build applications and perform a wide range of data processing tasks, including batch processing, stream processing, machine learning, and graph processing.

So in summary, Spark is an engine that provides distributed computing capabilities, and a framework that provides APIs and libraries for building data processing applications.

# What powers the Spark's engine ?

At the heart of Apache Spark's engine is its computational core, called the Resilient Distributed Datasets (RDD) engine. The RDD engine allows Spark to perform parallel processing of large datasets across a cluster of machines.

RDDs are fault-tolerant, immutable distributed collections of data that can be stored in memory and processed across many machines in parallel. This allows Spark to efficiently perform complex computations on large datasets by breaking them into smaller, more manageable pieces and processing them in parallel across the cluster.

RDDs are created using transformations on other RDDs or from external data sources, and can be cached in memory for fast access in subsequent computations. RDDs can be used with a variety of programming languages, including Scala, Java, Python, and R.

In addition to RDDs, Spark has other abstractions such as DataFrames and Datasets that allow for easier handling of structured data and improved query optimization.

# What is beneath RDDs ?

At the core of Apache Spark's distributed computing model, Resilient Distributed Datasets (RDDs) are the primary abstraction for data processing. RDDs are an immutable, fault-tolerant, and distributed collection of objects, which can be processed in parallel across a cluster. RDDs allow Spark to decouple programming from the underlying distributed storage systems.

However, RDDs are not the lowest level in Spark's distributed computing model. The RDDs are built on top of a distributed file system and a cluster manager, providing a high-level abstraction to users and application developers. Here is a glimpse of what is beneath RDDs:

1. Distributed Storage: Distributed storage is the fundamental building block of a distributed computing system. Apache Spark uses a distributed file system to store data across a cluster of machines. The most commonly used file system in Apache Spark's ecosystem is Hadoop Distributed File System (HDFS). HDFS is a fault-tolerant, scalable, and distributed file system that supports large data sets.
    
2. Cluster Manager: A cluster manager is responsible for managing and coordinating resources in a distributed computing system. Apache Spark supports several cluster managers, including Apache Mesos, Hadoop YARN, and Spark's standalone cluster manager. A cluster manager is responsible for scheduling, monitoring, and running Spark applications on a cluster.
    
3. Executors: An executor is the unit of work in Spark that runs on worker nodes of a cluster. Each executor runs in a separate JVM and is responsible for running tasks. Executors can run multiple tasks at the same time and are responsible for managing memory and CPU resources. Spark can run multiple executors within a single node, allowing for parallel processing of tasks.
    
4. Task Scheduler: The task scheduler is a component of Spark that schedules tasks to run on executors. The task scheduler ensures that tasks are allocated to executors in a way that maximizes resource utilization and minimizes data movement, which reduces network overhead.
    
5. Driver: The driver program drives the execution of a Spark application. It specifies the transformations and actions to perform on RDDs and submits the processing job to the cluster manager. The driver program runs in a separate JVM and communicates with the cluster manager to coordinate the execution of Spark applications.
    

# What is Databricks ?

Databricks was created to provide an easy-to-use, collaborative, and scalable platform for big data processing and analytics. The founders of Databricks, who were also the creators of Apache Spark, recognized that while Spark was a powerful tool for big data processing, it was still difficult to use and required a lot of technical expertise to set up and manage.

Thus, they founded Databricks in 2013 to address some of the challenges associated with using Spark, namely, the complexity of implementing and managing Spark clusters, the lack of a collaborative workspace for data analytics teams, and the absence of integrated machine learning capabilities.

Databricks provides an easy-to-use, cloud-based platform that abstracts the complexity of Spark cluster management and provides a collaborative workspace for data scientists, data engineers, and other stakeholders. Additionally, the platform offers a suite of pre-built machine learning libraries and tools that facilitate the deployment of machine learning models at scale.

##   
Is Databricks an engine ?

Databricks is not an engine in the traditional sense. It is a cloud platform that provides a collaborative workspace for teams to work together on big data projects. The heart of Databricks platform is the Apache Spark engine.

## Is Databricks a cloud provider like AWS and Azure and GCP ?

  
No, Databricks is not a cloud provider like AWS, Azure, and GCP. Instead, Databricks is an analytics and data processing platform that runs on top of cloud providers like AWS, Azure, and GCP.

While AWS, Azure, and GCP offer a wide range of cloud computing services, such as infrastructure as a service (IaaS), platform as a service (PaaS), and software as a service (SaaS), Databricks is more focused on analytics and data processing workloads. Databricks provides additional features such as optimized performance, collaborative notebooks, and workflows that make it easier to manage and work with big data. So, while it runs on cloud providers, it has a more specific purpose compared to the cloud providers themselves.

#   
What is Azure Databricks ?

Azure Databricks provides a fully managed, scalable, and collaborative platform to process and analyze big data, build Machine Learning models, and deploy them to production. It provides an easy-to-use workspace for data teams to collaborate on data projects, utilizing a range of programming languages and built-in libraries for data processing and Machine Learning, such as Python, R, Scala, and SQL.

The platform supports interactive data exploration through notebooks, which are shareable, interactive documents that allow data analysts and data scientists to visualize and explore data. Azure Databricks also provides a range of data connectors that make it easy to access various data sources, including Azure Blob Storage, Azure Data Lake Storage, and Azure SQL Database.

## Why was Azure Databricks created ?

One of the key reasons for creating Azure Databricks is to enable data teams to leverage the power of Apache Spark without the need to set up and manage complex infrastructure and resources. With Azure Databricks, businesses can make use of a fully managed and scalable platform that offers on-demand provisioning of compute and storage, enabling data teams to focus on their data analysis tasks rather than infrastructure management.

Azure Databricks was also created to provide a collaborative workspace for data teams to easily work together on data projects, sharing data, code, and insights in a single integrated platform that supports a variety of programming languages and data sources. The platform was developed to help businesses reduce time-to-insight and time-to-market for their data-driven applications by providing a fast and efficient way to process and analyze large volumes of data.  

##   
Is there an Azure solution that provides similar services like Databricks ?

Azure offers several services that can be used for big data analytics and processing, but when it comes to a unified and collaborative platform that is solely focused on big data processing, Azure Databricks is the main solution. However, there are some other Azure services that have overlapping functionality and can be used in combination with Azure Databricks to create a comprehensive big data analytics solution. Here are a few of them:

1. Azure HDInsight: A managed Apache Hadoop service that enables you to create and run big data applications on a managed Hadoop cluster.
    
2. Azure Data Factory: A cloud-based data integration service that allows you to create, schedule, and orchestrate data processing workflows.
    
3. Azure Stream Analytics: A real-time analytics service that enables you to process and analyze streaming data from various sources.
    
4. Azure Machine Learning: A cloud-based service that enables developers to build, train, and deploy machine learning models at scale.
    

While these services can be used together with Azure Databricks to create a complete big data analytics solution, each of them has a specific focus and is designed to address a specific set of needs.  

#   
Comparison

What better way to highlight the difference but for a table :D

| Point of Comparison | Databricks | Azure Databricks |
| --- | --- | --- |
| 1\. Platform | Standalone platform for running Spark workloads | Built on top of Microsoft Azure cloud services |
| 2\. OS compatibility | Compatible with multiple Operating Systems (Windows, Linux, MacOS) | Compatible only with Linux |
| 3\. Integration with other services | Limited integration with other services and platforms | Deep integration with other Azure services and platforms |
| 4\. Security & Authentication | Username & Password authentication | Integrated with Azure Active Directory & offers role-based access control |
| 5\. Performance | Offers high-speed performance for big data processing | Offers same high-speed performance as Databricks with added benefits of native integration with Azure Cloud Services |
| 6\. Cluster Management | Cluster management is limited and requires user input | Offers Autoscaling and automatic cluster management |
| 7\. Cost | Pay-per-usage pricing model | Pay-per-usage pricing model plus additional costs for Azure services integration |

The differences mainly arise due to the fact that Databricks is a standalone platform, while Azure Databricks is built on top of Microsoft Azure cloud services. Azure Databricks offers deep integration with other Azure services and platforms, which makes it a more robust solution for organizations looking to build on the Azure Cloud. However, both platforms offer high-speed performance for big data processing, data pipeline management, and complex analytics.  

# Uses cases

Here are 2 different use cases that highlight when to use which

### *Use Case 1: Databricks*

A company wants to analyze its large dataset of user clickstream logs to improve customer experience and increase sales. They have data stored in different sources like HDFS, Amazon S3, and Azure Blob Storage. They need to establish a data pipeline to consolidate and transform this data and provide their data analysts with a collaborative platform to perform complex data analysis. They decide to use Apache Spark on Databricks to build their data pipeline and run complex analytics on their big data.

Databricks provides them with a unified platform to run Apache Spark workloads, store and manage data, and collaborate within a team. With Databricks, they can easily connect to different data sources like HDFS, S3, and Blob Storage, and build robust ETL pipelines to transform their data. They can use Databricks Notebooks to share their analysis and collaborate with their team members. By using Databricks, they can easily scale up or down their cluster size based on their needs, and only pay for the resources they use.

### *Use Case 2: Azure Databricks*

A large financial institution wants to build a fraud detection system on their customer transactions. They already have data stored in Azure Blob Storage and want to build an end-to-end solution on the Azure Cloud. They need a scalable and collaborative platform that can maintain their data privacy and security, can easily interact with other Azure services, and can handle complex analytics. They decide to use Azure Databricks to build their solution.

Azure Databricks is built on top of Microsoft Azure and provides all the capabilities of Databricks, with additional integration with other Azure services. With Azure Databricks, they can easily connect to their Azure Blob Storage and integrate with other Azure services like Azure Data Factory or Azure Machine Learning. They can control their data privacy and security using Azure Active Directory, and enable role-based access control for their team members. By using Azure Databricks, they can leverage the autoscaling functionality to automatically scale their cluster size based on their workload, and use Azure Infrastructure-as-Code to manage their deployment.