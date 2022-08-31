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
