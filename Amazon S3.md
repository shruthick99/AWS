## Amazon S3 ##
 * Main building block of AWS
 * Amazon S3 is infinitely scaling storage.
## Buckets ##
 * S3 allows people to store objects(files) in buckets.
 * Buckets must have globally unique name.
 * Buckets are defined at regional level
## Objects ##
 * Objects (files) must have a key.
 * Max object size is 5TB.
 * Objects can have metadata
 * Objects can have tags.
## Amazon S3 Versioning ##
 * Can version your files in Amazon S3.
 * It is enabled at bucket level.
 * It protects against unintented deletes (ability to restore a version).
 * The version ID will show null if we upload the object before versioning.
 * Deleting an object while having versioning enabled, does not actually delete the object but creates a delete marker (with a versionID)
## S3 Encryption for Objects ##
4 methods
 ## SSE-S3 : (Server Side Encryption - S3) ##
 * encryption using keys handled & managed by Amazon S3
 * object is encrypted server side
 * HTTP/ HTTPS to be used to upload the object into S3
 * AES-256 encryption (algorithm)
 * must set header - "x-amz-server-side-encryption":"AES256"
 ## SSE-KMS : (Server Side Encryption - Key Management service) ##
* encryption using keys handled & managed by KMS
 * Advantage : user control, audit trail
 * object is encrypted server side
 * HTTP/ HTTPS to be used to upload the object into S3
* must set header - "x-amz-server-side-encryption":"aws:kms"
 ## SSE-C : ##
 * encryption using data keys fully managed by the customer outside of AWS
* S3 doesn't store the encryption keys
* HTTPS must be used to upload the object into S3
* Encryption must be provided in HTTP header for every HTTP request made
 ## Client side encryption : ##
 * Client library such as Amazon S3 Encrytpion Client enables us to perform the Client side encryption
 * Clients must encrypt and decrypt data themselves before sending to and when receiving from S3
 * Customer fully manages the keys and encryption cycle

## S3 Security ##
 * User based
   * IAM Policies - which API callas should be allowed for a specific user from IAM console.
 * Resource based
   * Bucket Policies - bucket wide rules from the S3 console - allows cross account
   * Object Access control list (ACL)
 * An IAM prinicipal can access an S3 object if:
   * the user IAM permission allow it or the resourece policy allows it.
   * And there is no explicit deny.

## S3 Bucket Policies
 * JSON based policies ( Resources, Actions, Effect, Prinicipal)
 * Grant public access to the bucket
 * Force objects to be encrypted at upload
 * Grant access to another account.

 ## Bucket Settings for Block Public Access ##
 * Blocks public access to buckets and objects granted through :
   * new access control list (ACLs)
   * any access control list (ACLs)
   * new public bucket or access point policies
 * These settings were created to prevent company data leaks

 ## S3 Security ##
 * Networking
   * Supports VPC Endpoints
 * Logging and audit
   * S3 Access logs can be stored in other S3 bucket
   * API calls can be logged in AWS Cloud Trail
 * User Security
   * MFA delete
   * Pre - Signed URLs: URLs that are valid only for a limited time.

 ## S3 CORS ##
 * Cross Origin Resource Sharing
 * An origin is a scheme(protocol), host(domain) and port
   * Ex: https://example.com
   * protocol - https
   * domain - example.com
   * Port 443 for HTTPS
 * Same origins: http://example.com/app1 & http://example.com/app2
 * Different Origins: http://example.com/ & http://mynotes.com/

 * CORS is a web browser based mechanism to allow request to other origins while visiting main origin
 * The requests won't be fulfilled unless the other origin allows for the requests using CORS Headers (ex: Access-Control-Allow-Origin)
 * If a client needs to do a cross-origin request on our S3 bucket, we need to enable the correct CORS headers
 * You can allow for a specific origin or for all origins (*)

# ADVANCED AMAZON S3 #
## S3 MFA Delete ##
 * forces user to generate a code on a device before doing imporatant operations on S3.
 * To use MFA delete. you need to enable versioning.
 * You will need MFA to
   * permanently delete an object version.
   * suspend versioning on bucket
 * Only bucket owner (root account) can enable/disable MFA delete.
 * MFA delete can be enabled using the CLI.

## S3 Access Logs##
 * For audit purpose, you may want to log all access to S3 buckets.
 * Request made to S3, from any account, authorized or denied, will be logged into another S3 bucket.
 * Do not set your logging bucket to be the monitored bucket.
 * It will create a logging loop and your bucket will grow in sixe exponentially.

## S3 Replication ##
 * CRR: Cross Region Replication
 * SRR: Same Region Replication
 * Must enable versioning in both source and destination accounts
 * Replication is asynchronous
 * Buckets can be in different accounts
 * Must give proper IAM permissions to S3
 * CRR - use cases: compliance, lower latency access, replication across accounts.
 * SRR - use cases: log aggreagation, live replication between production and test accounts.
 * Only new objects are replicated.
 * S3 Batch replication can be used to replicate existing objects.
 
 * For delete operations
   * deletions with a version ID are not replicated
   * if you enable delete marker replication, they will be replicated from one bucket to another.
 * There is no chaining of replication
   * if bucket1 has replication into bucket2, which has replication into bucket3, the objects created in bucket1 are not replicated in bucket3

 ## S3 pre-signed URLs ##
 * Pre-signed URLs can be generated using SDK or CLI
   * For downloads (use CLI)
   * For uploads (use SDK)
 * These URLs are valid for a default of 3600s. Can change the duration using --expires-in argument
 * Users given the pre-signed URL inherit the permission of the user who generated the URL for GET / PUT
 * Examples:
   * Only allow logged in users to download a premium video on your S3 bucket
   * Allow an ever changing list of users to download files by generating URLs dynamically
   * Allow temporarily a user to upload a file to a precise location in our bucket

 ## S3 Storage Classes ##
 * Various storage classes are Amazon S3 Standard, Standard Infrequent Access (IA), One-Zone IA, Glacier Instant Retrieval, Glacier Flexible Retieval, Glacier Deep Archive, Intelligent Tiering
 * Can move between these storage classes manually or using S3 Lifecycle Configurations


 ## S3 Standard - General Purpose ##
 * For frequently accessed data
 * Low latency & High Throughput
 * Sustain 2 concurrent facility failures
 * Use cases: Big data analytics, mobile and gaming applications, content distribution...

## S3 Infrequent Access (IA) ##
 * For less frequently accessed data but instant retrieval
 * Lower cost than S3 standard
 * Cost on retrieval
 * We have Standard IA and One Zone IA
   * In One Zone IA, we have high durability in a single AZ; data is lost when AZ is destroyed
   * Use cases for Standard IA: Disaster Recovery, Backups
   * Use cases for One Zone IA: Storing secondary backup copies of on-premises data, or data you can recreate

## Amazon S3 Glacier ##
 * archive / backup data; low-cost object storage
 * Pricing: price for storage + object retrieval cost
 * Amazon S3 Glacier Instant Retrieval
   * Millisecond retrieval, great for data accessed once a quarter
   * Minimum storage duration of 90 days
 * Amazon S3 Glacier Flexible Retrieval
   * Expedited (1-5 minutes); Standard (3-5 hrs); Bulk (5 - 12 hrs) - free
   * Minimum storage duration of 90 days
 * Amazon S3 Glacier Deep Archive - for long term storage
   * Standard (12 hrs); Bulk (48 hrs)
   * Minimum storage duration of 180 days

## S3 Intelligent Tiering ##
Small monthly monitoring and auto-tiering fee
Moves objects automatically between tiers based on usage
There are no retrieval charges in S3 Intelligent Tiering Tiers:
Frequent Access Tier (automatic): default tier
Infrequent Access Tier (automatic): objects not accessed for 30 days
Archive Instant Access Tier (automatic): objects not accessed for 90 days
Archive Access Tier (optional): configurable from 90 days to 700+ days
Deep Archive Access Tier (optional): configurable from 180 days to 700+ days

## S3 Lifecycle rules ##
 * Lifecycle rules are set up to automate moving objects between storage classes.
 * Transition Action: Defines when to transition objects between storage classes. For example,
   * Move objects to Standard IA after 60 days after creation
   * Move to Glacier for archiving after 6 months
 * Expiration Action: Action that is used to expire (delete) objects after certain duration. For example,
   * Can be used to delete log files after 365 days
   * Can be used to delete old version of objects (if versioning is enabled)
   * Can be used to delete incomplete multi-part uploads
 * Rules can be created for specific prefixes you want (ex: s3://mybucket/mp3/*)
 * Rules can be created for specific object tags (ex: Department: Accounts)

## S3 Analytics ##
 * You can set up S3 Analytics to help determine when to transition objects from Standard to Standard-IA
 * Does not work for OnezoneIA or Glacier.
























