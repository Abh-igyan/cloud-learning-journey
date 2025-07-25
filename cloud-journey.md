# Day 1 : Introduction to Cloud Computing & Storage STuff
Learning usecases of Cloud Storage and SQL & NoSQL Storage

## Unstructured Data Storage
* Unstructured data is information stored in a non-tabular form, such as documents, images, audio files, emails, social media posts, chats.
* It's usually best suited to Cloud Storage.
* About 80% of all data in world is unstructured.
* Organizations are focusing increasingly on mining unstructured data for insights that will provide them with a competitive
   edge as these don’t fit into neat tables (like rows and columns in Excel or databases). So they'll serve users better, and make smarter decisions.

## Structured Data Storage
* Most people are used to working with,
* E.g.,: names, addresses, contact numbers, dates, and billing info.
* typically fits within columns and rows in spreadsheets or relational databases.
* It's organized and clearly defined and usually easy to capture, access, and analyze.
* can be understood by programming languages,
* two types: transactional workloads and analytical workloads.

## Using Cloud Storage for Unstructured Data Storage
* CLoud is a fully managed scalable service
* Cloud Storage’s primary use is whenever binary large-object storage (BLOB) is needed for online content like: photos/videos, backup & archiving & storing intermediate results
* OBject storage: A computer data storage architecture that manages data as “objects” and not as a file and folder hierarchy (file storage), or as chunks of a disk (block storage).
* These objects are stored in a packaged format that contains the binary form of the actual data itself, relevant associated metadata, and a globally unique identifier (in the form of URLs).
  That's why object storage interacts well with web technologies.
* Data commonly stored as objects includes video, pictures, and audio recordings.
* There are four primary storage classes in Cloud Storage, and stored data is managed and billed according to
  which class it belongs in.: Standard storage, nearline storage, coldline storage and archive storage.
###  BUCKETS
* Cloud Storage files are organized into buckets.
* A bucket needs:
    * globally unique name
    * specific geographic location for where it should be stored, and
* an ideal location for a bucket is where latency is minimized.
*  You should choose a bucket location closest to the users or services accessing it — so it loads faster.
*  The storage objects offered by Cloud Storage are “immutable” and a new version is created with every change made.
*  within a bucket, we may allow versioning or by default every new change made will overwrite the existing versions.
*  Versioning:  We can list the archived versions of an object, restore an object to an older state, or permanently delete a version of an object, as needed.

# Day 2
## Labs
* During Labs open Google Cloud Console only in incognito with the given student id and pass.
* During lab, can verify our work from navigation-->Cloud Storage.
* ![image](https://github.com/user-attachments/assets/9991c4c7-320f-4c2e-aedb-1b89b2686e40)
* Always Activate Cloud Shell from the Activate Cloud Shell icon at the top of the Google Cloud console.
* gcloud is the command-line tool for Google Cloud (supports auto=completion).
* For lisiting active account name: `gcloud auth list`
* For listing project ID: `gcloud config list project`
* Setting project region for a lab: `gcloud config set compute/region "REGION"`

## LAB Cloud Storage: Qwik Start - CLI/SDK:
### Task 1. Create a bucket
1) Universal Bucket naming rules
* Do not include sensitive information in the bucket name, because the bucket namespace is global and publicly visible.
* must contain only lowercase letters, numbers, dashes (-), underscores (_), and dots (.). Names containing dots require verification.
* must start and end with a number or letter.
* must contain 3 to 63 characters. Names containing dots can contain up to 222 characters, but each dot-separated component can be no longer than 63 characters.
* Bucket names cannot be represented as an IP address in dotted-decimal notation (for example, 192.168.5.4).
* cannot begin with the "goog" prefix.
* cannot contain "google" or close misspellings of "google".
* Also, for DNS compliance and future compatibility, you should not use underscores (_) or have a period adjacent to another period or dash. For example, ".." or "-."          or ".-" are not valid in DNS names.
2) `gcloud storage buckets create gs://<YOUR-BUCKET-NAME>`
3) Bucket created with default settings: see in Navigation menu > Cloud Storage > bucket name > Configuration tab.
4) Each bucket has a default storage class, which you can specify when you create your bucket (using gsutil):
   * `gsutil mb -c nearline -l asia-south1 gs://my-unique-bucket-name/`
   * (-c nearline: sets Nearline as default storage class, -l asia-south1: sets location (e.g. Mumbai))

### Task 2. Upload an object into your bucket
1) To download an image name.jpg into bucket: `curl Link_of_image --output name.jpg`
2) To upload the downloaded image to bucket: `gcloud storage cp name.jpg gs://YOUR-BUCKET-NAME`
3) just stored an object in bucket!
4) Removing the downloaded image: `rm name.jpg`

### Task 3. Download an object from your bucket
 Downloading stored image into cloud shell: `gcloud storage cp -r gs://YOUR-BUCKET-NAME/name.jpg .`
### Task 4. Copy an object to a folder in the bucket 
Created MyDevImages folder and copied image to it: `gcloud storage cp gs://YOUR-BUCKET-NAME/name.jpg gs://YOUR-BUCKET-NAME/MyDevImages/`
### Task 5. List contents of a bucket or folder
 `gcloud storage ls gs://YOUR-BUCKET-NAME`

### Task 6. List details for an object
-l flag lists details of name.jpg:  `gcloud storage ls -l gs://YOUR-BUCKET-NAME/ada.jpg`
### Task 7. Make your object publicly accessible
Granting all users read permission for the object stored in my bucket: `gsutil acl ch -u AllUsers:R gs://YOUR-BUCKET-NAME/name.jpg`
* An access control list (ACL) is a mechanism to define who has access to your buckets and objects.
* Go to Navigation > Cloud storage > bucket name > **image with the Public link box** is visible

### Task 8. Remove public access
`gsutil acl ch -d AllUsers gs://YOUR-BUCKET-NAME/ada.jpg`
refresh console
### Delete objects
E.g., delete the image file in your bucket: `gcloud storage rm gs://YOUR-BUCKET-NAME/ada.jpg`
* refresh console > no image on cloud

# Day 3
## SQL Managed Services
* Databases are extremely important and **applications/softwares** run databases to get a fast answer to questions like: what's this user's name, given his sign-in info, entries from a directory, what ad to display next to user, etc.
* These apps must be able to write data in and read data out of databases.
* ![Screenshot 2025-06-23 134557](https://github.com/user-attachments/assets/31ea5de7-78ca-4193-8fad-d60d44699b8c)
* Google Cloud offers two managed relational database services: Cloud SQL and Spanner.
  ### Cloud SQL
  * ![Screenshot 2025-06-23 135946](https://github.com/user-attachments/assets/83c3d6d4-aa01-45f1-bd5a-d2d518e3fd33)
  * ![Screenshot 2025-06-23 140055](https://github.com/user-attachments/assets/7fda409c-4f57-4cd5-bf72-f39b33ada151)
## Lab- Cloud SQL for MySQL: Qwik Start
Create and connect to a Cloud SQL for MySQL instance and perform basic SQL operations using the Google Cloud console and the ```mysql``` client.
* Activate Cloud Shell.
### Task 1. Create a Cloud SQL instance
* Instance ID is used to uniquely identify your instance within the project.
  
Go to navigation >  SQL > Instances > Create Instance > Choose MySQL > select Enterprise edition (vvvimp: no "plus" otherwise lab terminates) > In Preset choose **Development (4 vCPU, 16 GB RAM, 100 GB Storage, Single zone)** >> choose database version as MySQL 8 > Enter a Instance_ID > In the password field click on the Generate link (note the password) > At the Cloud Shell prompt, connect to your Cloud SQL instance by: `gcloud sql connect Instance_ID --user=root` > click authorize> enter the root/instance password > Now in mysql prompt, we create and upload data.

* `CREATE DATABASE guestbook;`
* ```sql
     USE guestbook;
     CREATE TABLE entries (guestName VARCHAR(255), content VARCHAR(255),
          entryID INT NOT NULL AUTO_INCREMENT, PRIMARY KEY(entryID));
          INSERT INTO entries (guestName, content) values ("first guest", "I got here!");
     INSERT INTO entries (guestName, content) values ("second guest", "Me too!");
* `SELECT * FROM entries;`
* Created a Cloud SQL for MySQL instance and database, and then uploaded data.

## Spanner as a managed service:
* Spanner is a fully managed relational database service that scales horizontally, is strongly consistent, and speaks SQL.
* **Vertical scaling** is where you make a single instance larger or smaller, while **horizontal scaling** is when you scale by adding and removing servers. (remember scalability)
* important use: manage end-user metadata.
* ![image](https://github.com/user-attachments/assets/52cb3855-82f2-46fa-a604-f9ef84f54c53)
* Working: Synchronous replication --Google uses replication within and across regions to achieve availability, so if one region goes offline, the user’s data can still be served from another region.
  
## NoSQL Managed Database Services Options:
**Firestore** and **Bigtable** 

  ### Firestore
  * Firestore is a fully managed, scalable serverless NoSQL document store that supports ACID(used in relational databases -banks, ecommerce(reliable)) transactions.
  * flexible, horizontally scalable, NoSQL cloud database for mobile, web, and server development.
  * It stores data as documents and these documents are then organized into collections.
    
    ![image](https://github.com/user-attachments/assets/a96b2e61-a057-4aa9-8533-06fea64e458f)
    
  * Firestore uses online & offline data synchronization to update data on any connected device.
  * also designed to make simple, one-time fetch queries efficiently.
  * It caches (*stores a copy of data locally*)  data that an app is actively using, so the app can write, read, listen to, and query data even if the device is offline and syncs any local changes back when the online.

   ### Bigitable: Google's NoSQL big data database service.
   * A petabyte scale, sparse wide column NoSQL database that offers extremely low write latency.
   * used to work with more than 1 TB of semi-structured or structured data.
   * powers many core Google services, including Search, Analytics, Maps, and Gmail.
   * Handles massive workloads and consistent low latency and high throughtput (work completed by a system per sec). 
   * great choice for both operational and analytical applications, including Internet of Things, user analytics, and financial data analysis.
     ![image](https://github.com/user-attachments/assets/af8d326b-2fd9-44f1-afe9-85e0b1d5c9bc)
   * can interact with other Google Cloud services and third-party clients.
   * **APIs** serve data to applications, dashboards, and data services. Using APIs, data can be read from and written to Bigtable through a data service layer like Managed VMs, the HBase REST Server, or a Java Server using the HBase client.
   * Data streamed in through various popular **stream processing frameworks** like Dataflow Streaming, Spark Streaming, and Storm.
   * If no streaming, data can also be read from and written to Bigtable through **batch processes** like Hadoop MapReduce, Dataflow, or Spark.
   * BigQuery is different and sits on the edge between data storage and data processing The usual reason to store data in BigQuery is so you can use its big data analysis and interactive querying capabilities. It is not purely a data storage product.
# Day 5: Using APIs
 ## Purpose of APIs (Application Programming Interfaces)
 * A clean well-def interface.
 * AppDevs structure the software they write so that it presents a clean, well-defined interface that hides unnecessary detail, they provide a documentation of that interface. That’s an API. Its underlying implementation can change.
 * Used to simplify the way different,distinct software resources communicate.
 * Changes to the API are made with versions: we can specify the version we wanna use in our software.
 * **REST API**:
   * A set of constraints that a service must comply with.
   * Service complying with REST constraints, said to be RESTful.
   * uses HTTP requests to perform GET, PUT, POST, and DELETE data
   * REST applies the web architecture to services.
   * APIs intended to be spread widely to consumers and deployed to devices with limited computing resources, like mobile, are well suited to a REST structure.
   * State information does not need to be stored or referenced for the API to run.
   * Great for cloud applications because they are stateless.
   * Authentication via OAuth and security by leveraging tokens.
 * DIfficulty in deploying and managing APIs: Interface definition language/format, Authentication & Authorization, Management & Scalability to meet demand, Logging and monitoring
 * Cloud Endpoints is an API management system supports applications running in App Engine, Google Kubernetes Engine, and Compute Engine?
## Apigee API Management
* A GCP available for developing and managing API proxies
* has a specific focus on business problems, like rate limiting, quotas, and analytics.
* many Apigee API Management users provide a software service to other companies.
* Backend services for Apigee API Management don't have to be in Google Cloud. It just acts as a smart gateway in front of APIs. Our backend(logic,database) can be on AWS, Azure anywhere)
* Used to take apart legacy apps piece-by-piece. Instead of replacing a large, important application in one move, use Apigee to peel off its services individually. Migrate gradually to microservices without breaking the system at once. Apigee manages the transition. This allows them to stand up microservices to implement each in turn, until the legacy application can finally be retired.
## Pub/Sub
* short for Publisher/Subscriber, or publish messages to subscribers.
* Google Cloud Pub/Sub is a fully-managed, real-time messaging service that enables you to send and receive messages between independent applications. It’s designed for event-driven systems, where services communicate by publishing and subscribing to messages asynchronously.
* ensures at-least-once delivery of received messages to subscribing applications, with no provisioning required.
* Its APIs are open, the service is global by default, and it offers end-to-end encryption.
* One of the early stages in a data pipeline --> data ingestion --> large amounts of streaming data are received (may not be from single source but from different events happening asynchronously), ex: IoT.
  * These IoT devices present new challenges to data ingestion:
    * data can be streamed from many different methods and devices which might not talk to each other
    * it can be hard to distribute event messages (notifications) to the right subscribers. A method is needed to collect streaming data from sensors and send them to subscribers.
    * data can arrive quickly and at high volumes. Services must be able to support this.
    * ensuring that services are reliable and secure, and perform as expected.
* End-to-end Pub/Sub architecture:
  
  ![Screenshot 2025-06-27 104958](https://github.com/user-attachments/assets/833a85c9-3492-402b-afb4-911dac202b71)

  Upstream source data comes in from devices all over the globe and is ingested into Pub/Sub --> Pub/Sub reads, stores, and broadcasts to any subscribers of this data topic that new messages are available --> As a subscriber of Pub/Sub, Dataflow (a google cloud fully managed service for processing and transforming data) can ingest and transform those messages in an elastic streaming pipeline and output the results into an analytics data warehouse like BigQuery --> can connect a data visualization tool, like Looker Studio, to visualize and monitor the results of a pipieline --> AI or ML tool such as Vertex AI to explore the data ...
  
* ![Screenshot 2025-06-27 110043](https://github.com/user-attachments/assets/4f9417cf-f994-44c7-ab96-48edae78437a)

  Topic and subscribers are completely decoupled, so they’re free to break without affecting their counterparts.

  e.g., ![Screenshot 2025-06-27 110612](https://github.com/user-attachments/assets/3e332e0c-028b-46e3-ad42-103971bf8def)
  
* ![image](https://github.com/user-attachments/assets/4325a560-3319-4bf3-81e6-9a5351d1b4cc)

  Pub/Sub is a good solution to buffer changes for lightly coupled architectures, like this one, that have many different sources and sinks.
* Pub/Sub supports many different inputs and outputs, and you can even publish a Pub/Sub event from one topic to another.
## Lab   ----Pub/Sub: Qwik Start - Python
* The Pub/Sub service allows applications to exchange messages reliably, quickly, and asynchronously. To accomplish this, a data producer publishes messages to a Cloud Pub/Sub topic. A subscriber client then creates a subscription to that topic and consumes messages from the subscription. Cloud Pub/Sub persists messages that could not be delivered reliably for up to seven days.
* Task 1. Create a virtual environment:
   * Python virtual environments are used to isolate package installation from the system.
   * Install the virtualenv environment: `sudo apt-get install -y virtualenv`
   * Build the virtual environment: `python3 -m venv venv`
   Activate the virtual environment:   `source venv/bin/activate`

* Task 2. Install the client library:
   * install the client library: `pip install --upgrade google-cloud-pubsub`
   * Get the sample code by cloning a GitHub repository: `git clone https://github.com/googleapis/python-pubsub.git`
   * Navigate to the directory: `cd python-pubsub/samples/snippets`
 
* Task 3. Pub/Sub - the Basics:
  * A topic is a shared string that allows applications to connect with one another through a common thread.
  * publisher creates and sends messages to a topic and a subscriber creates a subscription to a topic to receive messages from it.

* Task 4. Create a topic:
   * To publish data to Pub/Sub you create a topic and then configure a publisher to the topic.
   * In Cloud Shell, your Project ID should automatically be stored in the environment variable GOOGLE_CLOUD_PROJECT: `echo $GOOGLE_CLOUD_PROJECT`
   * Ensure the output is the same as the Project ID in your CONNECTION DETAILS.
      publisher.py is a script that demonstrates how to perform basic operations on topics with the Cloud Pub/Sub API.
   * View the content of publisher script:   `cat publisher.py`
   * For information about the publisher script: `python publisher.py -h`
   * Run the publisher script to create Pub/Sub Topic: `python publisher.py $GOOGLE_CLOUD_PROJECT create MyTopic`
   * This command returns a list of all Pub/Sub topics in a given project: `python publisher.py $GOOGLE_CLOUD_PROJECT list`
   * viewing the topic just made in the Cloud Console. Navigate to Navigation menu > Pub/Sub > Topics.
     
* Task 5. Create a subscription:
   * Create a Pub/Sub subscription for topic with subscriber.py script: `python subscriber.py $GOOGLE_CLOUD_PROJECT create MyTopic MySub`
   * This command returns a list of subscribers in given project: `python subscriber.py $GOOGLE_CLOUD_PROJECT list-in-project`
   * For information about the subscriber script: `python subscriber.py -h`
  
* Task 6. Publish messages:
   * Publish the message "Hello" to MyTopic: `gcloud pubsub topics publish MyTopic --message "Hello"`
   * Publish a few more messages to MyTopic—run the following commands (replacing <YOUR NAME> with your name and <FOOD> with a food you like to eat):
      * `gcloud pubsub topics publish MyTopic --message "Publisher's name is <YOUR NAME>"`
      * `gcloud pubsub topics publish MyTopic --message "Publisher likes to eat <FOOD>"`
      * `gcloud pubsub topics publish MyTopic --message "Publisher thinks Pub/Sub is awesome"`
* Task 7. View messages:
   * Use MySub to pull the message from MyTopic: `python subscriber.py $GOOGLE_CLOUD_PROJECT receive MySub`
   * Ctrl+C to stop listening


# Day 6: Security in Cloud
   ## Five layers of protection provided by GOOGLE for data safety (in increasing order):
   * **Hardware Infrastructure**: Hardware design and provenance, Secure boot stack & Premises security
   * **Service Deployment Layer**: Encryption of inter-service communication, User Identity
   * **Storage services layer**: file storage (encryption using Centrally managed keys), Hardware encryption support in HDDs/SSDs
   * **Internet Communication Layer**: Google Front End (ensuring all services are certified and follow best practices such as supporting perfect forward secrecy. Applying protection against Denial of Service DoS attacks), DoS protection (Google also has multi-tier, multi-layer DoS protections that further reduce the risk of any DoS impact on a service running behind a GFE.)
   * **Operational security layer**: Instrusion detection, reducing insider risk, employee U2F use, software dev. practices
   ##  Vulnerability Rewards Program by Google where anyone who can discover and inform us of bugs in the infrastructure or applications is paid.
   ## The Shared Security Model
   * Security responsibilities are shared between the customer and Google Cloud.
   * When customer deploys an application to their on-premises infrastructure, they are responsible for the security of the entire stack: from the physical security of the hardware and the premises to securing the content stored in those applications.
   * But when they move an application to Google Cloud, Google handles many of the lower layers of security, like the physical security, disk encryption, and network integrity. The upper layers of the security stack, including the securing of data, remain the customer’s responsibility. They control who or what has access to their data.
   * Google Cloud provides tools that help them control this access, such as Identity and Access Management, but they must be properly configured to protect your data.
   * ![image](https://github.com/user-attachments/assets/9ac4aa06-f749-41e0-a5a7-0e21366a97e3)
   ## Encryption Options:
   * ![image](https://github.com/user-attachments/assets/96dec2a7-078b-43fe-be0b-666b73edbf4b)
   * **Client-side encryption**: last option is to encrypt your data locally before you store it in the cloud. 
Neither the unencrypted data nor the decryption keys leave their local device.
   * **Default encryption**: happens automatically ![image](https://github.com/user-attachments/assets/ae458a52-797f-4db5-b488-5c9d3ec5a1ee)
   * **CMEK**:
     * Cloud Key Management Service (KMS) automates and simplifies the generation and management of encryption keys. Supports encryption, decryption, signing, and verification of data. Supports automated and at-will key rotation, both symmetric and asymmetric cryptographic keys and various popular algorithms.
     * The keys are managed by the customer and never leave the cloud.
   * **CSEK**: ![image](https://github.com/user-attachments/assets/8b7d3d38-1263-4a76-9142-81aa96a52190)
     * the key only exists in-memory and is discarded after use.
     * Persistent disks, such as those that back virtual machines, can be encrypted with CSEK. data is encrypted before it leaves the virtual machine. 
Even without CSEK or CMEK, persistent disks are still encrypted. When a persistent disk is deleted, the keys are discarded, and the data is rendered irrecoverable by traditional means.
   * Other encryption options: CLIENT SIDE & DISK ENCRYPTION (create own persistent disks and redundantly encrypting them)
# Day 7
   ## Improving security using authentication and authorization with IAM:
   * An organization node contains lots of folders, projects, and resources -> need to restrict access -> IAM comes -> admin decides who can do what on which resources
   * The “who” part of an IAM policy can be a Google Account, a Google group, a service account, or Cloud Identity domain.
   * The “can do what” part of an IAM policy is defined by a role (a collection of permissions). E.g create, delete, start, stop, and change virtual machines in a project.
   * ![image](https://github.com/user-attachments/assets/3042bd1b-ad65-4fde-86d6-b1d7c7041cb5)
   * ![image](https://github.com/user-attachments/assets/f348bec9-56c2-44ee-a1a3-88e1ba988fcf)
   * IAM checks deny policies before allow policies. Deny policies, like allow policies, are inherited through the resource hierarchy.
   * With a tool called **Cloud Identity**, organizations can define policies and manage their users and groups by using the Google Admin console. -- Admins can log in and manage Google Cloud resources by using the same usernames and passwords they already use in existing Active Directory -- if someone leaves they can disable their account.
   * Admins can log in and manage Google Cloud resources by using the same usernames and passwords they already use in existing Active Directory
   ### Three kinds of roles in IAM: basic, predefined, and custom
   * Basic roles: broad in scope - when applied they affect all resources in the project - Basic roles include owner, editor, viewer, and billing administrator.
      * project owners can also examine and modify a resource and also can manage the associate roles and permissions, and set up billing.
      * Billing admins control the billing for a project, but don't have permissions to change the resources in the project.
   * Predefined roles: permissions that are more specifically tailored to meet the needs of typical job roles.
      * Specific Google Cloud services offer sets of predefined roles, and they even define where those roles can be applied. Let’s take Compute Engine, a Google Cloud product that offers virtual machines as a service. E.g., offers instanvceAdmin role
   * Custom roles: ![image](https://github.com/user-attachments/assets/7a326510-4bf0-4ce6-9e50-c88988283e46)
      * Before you start creating custom roles, please note:
        * you must manage the permissions that comprise the custom role you’ve created.
        * custom roles can only be applied to either project or organization level (not folder level).
      * App running in VM needs to store data in cloud. If we wanna restrict access to that data only to that VM, we create a service account to authenticate that VM to Cloud Storage.
      * Service accounts are named with an email address and cryptographic keys(not pass).
      * So, if a service account has been granted Compute Engine’s **Instance Admin** role, this would allow an application that runs in a VM with that service account to create, modify, and delete other VMs.
      * A service account is also a resource! So it can have IAM policies of its own attached to it.
# Day 8
   ## Lab: User Authentication by IAP-
   * is a Google Cloud service that intercepts web requests sent to your application, authenticates the user making the request using the Google Identity Service, and only lets the requests through if they come from a user you authorize. In addition, it can modify the request headers to include information about the authenticated user.
   * IAP is a resource that can be used to set up authentication to https-based applications without the use of VPNs. 
   * Establishes a central authorization layer for applications over TLS, so you can use an application-level access control model instead of relying on network-level firewalls.
   * Only users and groups can access applications and resources protected by IAP through the proxy with the correct IAM role.
   * IAP performs authentication and authorization checks when a user tries to access a IAP-secured resource.
   * IAP secures authentication and authorization of external requests through TLS.
   * IAP doesn't protect against activities inside your VM, such as if someone uses SSH to access the VM. And also within a project, such as VM-to-VM communication within your project over the local network.
   * building a minimal python based web app(displays hello world welcome page) with Google App Engine, and using IAP to restrict access to the app and provide user identity information to it.
   * If I've a .zip file of my app, I may download the file then:
       ```unzip user-authentication-with-iap.zip```
      ``` cd user-authentication-with-iap```
   * **Task 1. Deploy the application and protect it with IAP**
        * Deploy to App Engine:
        * Update python runtime to python39: `sed -i 's/python37/python39/g' app.yaml`
        * Deploy the app to the App Engine Standard environment for Python: `gcloud app deploy`
        * Select a region `REGION` When you are asked if you want to continue, enter Y for yes.
        * Once deployment completes, view app: `gcloud app browse`
        * Restrict access with IAP
            * In the cloud console window, click the Navigation menu Navigation menu icon > Security > Identity-Aware Proxy.
            * Click Enable API.            
            * Click Go to Identity Aware Proxy.            
            * To configure your project's OAuth consent screen, go to the OAuth consent screen            
            * Click Get Started.            
            * For App name, enter `IAP Example`.            
            * Click User support email, and then click the student email and then click Next.            
            * For Audience, select Internal, and then click Next.            
            * Users with access to the project should be able to log in to the app.            
            * On the left panel of the lab instructions, copy the Username.            
            * For Contact information, paste the copied username.            
            * Click Next.            
            * Click Checkbox to agree the User Data Policy and click Continue and then click Create. The consent screen is now set up.            
            * In Cloud Shell, run this command to disable the Flex API:   `gcloud services disable appengineflex.googleapis.com`
            * Return to the IAP page and refresh it. You should now see a list of resources you can protect. Click the toggle button in the IAP column in the App Engine app row to turn IAP on.
            * The domain will be protected by IAP. Click Turn On.
        * Now no email id will be able to access that webapp (since we have not yet told IAP which accounts to allow through.)
        * Return to the IAP page of the console, select the checkbox next to App Engine app, and see the App Engine sidebar to the right.
        * Each email address (or Google Group address, or Workspace domain name) that should be allowed access needs to be added as a Member.
        * Click Add Principal.
        * Enter your Student email address.
        * Then, pick the Cloud IAP > IAP-Secured Web App User role to assign to that address.
        * ![image](https://github.com/user-attachments/assets/344d8a36-8a87-452d-b6fe-7663b2d8a38f)
        * Navigate back to your app and reload the page. You should now see your web app, since you already logged in with a user you authorized.
   * **Task 2. Access user identity information**
        * the application will get the logged-in user's email address and a persistent unique user ID assigned by the Google Identity Service to that user. That data will be displayed to the user in the welcome page.
        * In Cloud Shell, change to the folder for this step:cd  `~/user-authentication-with-iap/2-HelloUser`
        * Update python runtime to 39: `sed -i 's/python37/python39/g' app.yaml`
        * `gcloud app deploy`
        * `gcloud app browse`
        * Now if we open the webapp, we'll get our user info displayed. If we turn off IAP, we'll see the same screen but with no user info.
        * Since the application is now unprotected, a user could send a web request that appeared to have passed through IAP. For example, you can run the following curl command from the Cloud Shell to do that: `curl -X GET <your-url-here> -H "X-Goog-Authenticated-User-Email: totally fake email"`
        * The web page will be displayed on the command line. There is no way for the application to know that IAP has been disabled or bypassed. For cases where that is a potential risk, Cryptographic Verification is used.
   * **Task 3. Use Cryptographic Verification**
        * If there is a risk of IAP being turned off or bypassed, your app can check to make sure the identity information it receives is valid. This uses a third web request header added by IAP, called **X-Goog-IAP-JWT-Assertion**. The value of the header is a cryptographically signed object that also contains the user identity data. Your application can verify the digital signature (requires several extra steps, such as retrieving the latest set of Google public keys) and use the data provided in this object to be certain that it was provided by IAP without alteration.
        * In Cloud Shell, change to the folder for this step: `cd ~/user-authentication-with-iap/3-HelloVerifiedUser`
        * change python runtime and deploy the app.
        * E.g., of user() method to retrieve and verify the cryptographically signed identity information:
    ```def user():
          assertion = request.headers.get('X-Goog-IAP-JWT-Assertion')
          if assertion is None:
              return None, None
          info = jwt.decode(
              assertion,
              keys(),
              algorithms=['ES256'],
              audience=audience()
          )
          return info['email'], info['sub']```
        * The `assertion` is the cryptographically signed data provided in the specified request header
        * Validation uses the public keys that Google provides for checking data it signs, and knowing the audience that the data was prepared for (essentially, the Google Cloud project that is being protected). Helper functions `keys()` and `audience()` gather and return those values.
        * The signed object has two pieces of data we need: the verified email address, and the unique ID value (provided in the `sub`, for subscriber, standard field).
        * after deployment, `gcloud app browse`
        * Open link: no IAP info is visible (since iap disabled).
        * Enable it, verified email and ID of user will be visible.
   * Summary:  deployed an App Engine web application. First, you restricted access to the application to only users you chose. Then you retrieved and displayed the identity of users that IAP allowed access to your application, and saw how that information might be spoofed if IAP were disabled or bypassed. Lastly, you verified cryptographically signed assertions of the user's identity, which cannot be spoofed.
# Day 9
## IAM Authorization best practices
 * Granting roles to groups instead of individuals. This lets you update group memberships instead of changing an IAM policy.
 * AFter doing this, we must make sure to audit memberships of groups used in policies and control the ownership of the Google group used in IAM policies.
 * This example shows a network admin group. Some of those members also need a read_write role, which allows them to read and write to a Cloud Storage bucket, but others need the read_only role. Adding and removing individuals from all three groups controls their total access.
 * <img width="1429" height="735" alt="image" src="https://github.com/user-attachments/assets/823462e7-effd-466a-b895-3506b7d3f853" />
 * <img width="1543" height="719" alt="image" src="https://github.com/user-attachments/assets/e1a5e888-6d87-48f5-87a6-1b2db9dd1b60" />
 
## Lab: Cloud IAM: Qwik Start 
 * Explore the IAM console and project level roles: Select Navigation menu > IAM & Admin > IAM. You are now in the "IAM & Admin" console. Scroll down to Basic in Select a role section, select roles.
 * If a USER has the viewer role. The +GRANT ACCESS button is grayed out for him. He won't be able to grant roles to anyone
 * **Granting CLoud access role to a user**: In the Console, select Navigation menu > IAM & Admin > IAM. Click +GRANT ACCESS button and paste the Username 2 name into the New principals field. In the Select a role field, select Cloud Storage > Storage Object Viewer from the drop-down menu. Click SAVE.
 * Now that user will have cloud storage access: `gsutil ls gs://[YOUR_BUCKET_NAME]` will return bucket details if created already.
