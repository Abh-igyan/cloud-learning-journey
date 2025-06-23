# Day 1 : Introduction to CLoud Computing & Storage STuff
Learning usecases of Cloud STorage and SQL & NoSQL Storage

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
* For lisiting active account name: gcloud auth list
* For listing project ID: gcloud config list project
* Setting project region for a lab: gcloud config set compute/region "REGION"

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
2) gcloud storage buckets create gs://<YOUR-BUCKET-NAME>
3) Bucket created with default settings: see in Navigation menu > Cloud Storage > bucket name > Configuration tab.
4) Each bucket has a default storage class, which you can specify when you create your bucket (using gsutil): gsutil mb -c nearline -l asia-south1 gs://my-unique-bucket-name/ (-c nearline: sets Nearline as default storage class, -l asia-south1: sets location (e.g. Mumbai))
  

