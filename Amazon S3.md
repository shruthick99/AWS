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
























