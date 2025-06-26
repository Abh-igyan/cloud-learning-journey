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
 ## Purpose of APIs
 * A clean well-def interface.
 * AppDevs structure the software they write so that it presents a clean, well-defined interface that hides unnecessary detail, and then they provide a documentation of that interface. That’s an API. Its underlying implementation can change.
 * Used to simplify the way different,distinct software resources communicate.
 * Changes to the API are made with versions: we can specify the version we wanna use in our software.
 * **REST API**: * A set of constraints that a service must comply with.
                 * Service complying with REST constraints, said to be RESTful.
                 * uses HTTP requests to perform GET, PUT, POST, and DELETE data
                 * REST applies the web architecture to services.
                 * APIs intended to be spread widely to consumers and deployed to devices with limited computing resources, like mobile, are well suited to a REST structure.       * State information does not need to be stored or referenced for the API to run.
                 * Great for cloud applications because they are stateless.
                 * Authentication via OAuth and security by leveraging tokens.
                  * DIfficulty in deploying and managing APIs: Interface definition language/format, Authentication & Authorization, Management & Scalability to meet demand, Logging and monitoring
