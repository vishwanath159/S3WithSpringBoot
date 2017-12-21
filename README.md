# S3WithSpringBoot
S3 client apis with spring boot application

Introduction.


Amazon S3
Amazon Simple Storage Service is storage for the Internet. It is designed to make web-scale computing easier for developers.Amazon S3 has a simple web services interface that we can use to store and retrieve any amount of data, at any time, from anywhere on the web. It gives any developer access to the same highly scalable, reliable, fast, inexpensive data storage infrastructure that Amazon uses to run its own global network of web sites. The service aims to maximize benefits of scale and to pass those benefits on to developers.
Advantages to Amazon S3

Amazon S3 is intentionally built with a minimal feature set that focuses on simplicity and robustness. Following are some of advantages of the Amazon S3 service
•	Create Buckets – Create and name a bucket that stores data. Buckets are the fundamental container in Amazon S3 for data storage.
•	Store data in Buckets – Store an infinite amount of data in a bucket. Upload as many objects as you like into an Amazon S3 bucket. Each object can contain up to 5 TB of data. Each object is stored and retrieved using a unique developer-assigned key.
•	Download data – Download your data or enable others to do so. Download your data any time you like or allow others to do the same.
•	Permissions – Grant or deny access to others who want to upload or download data into your Amazon S3 bucket. Grant upload and download permissions to three types of users. Authentication mechanisms can help keep data secure from unauthorized access.
•	Standard interfaces – Use standards-based REST and SOAP interfaces designed to work with any Internet-development toolkit.
Buckets 
A bucket is a container for objects stored in Amazon S3. Every object is contained in a bucket. For example, if the object named photos/puppy.jpg is stored in the johnsmith bucket, then it is addressable using the URL http://johnsmith.s3.amazonaws.com/photos/puppy.jpgBuckets serve several purposes: they organize the Amazon S3 namespace at the highest level, they identify the account responsible for storage and data transfer charges, they play a role in access control, and they serve as the unit of aggregation for usage reporting. You can configure buckets so that they are created in a specific region.. You can also configure a bucket so that every time an object is added to it, Amazon S3 generates a unique version ID and assigns it to the object. For more information, 
Objects 
Objects are the fundamental entities stored in Amazon S3. Objects consist of object data and metadata. The data portion is opaque to Amazon S3. The metadata is a set of name-value pairs that describe the object. These include some default metadata, such as the date last modified, and standard HTTP metadata, such as Content-Type. You can also specify custom metadata at the time the object is stored.An object is uniquely identified within a bucket by a key (name) and a version ID. For more information. 
Keys 
A key is the unique identifier for an object within a bucket. Every object in a bucket has exactly one key. Because the combination of a bucket, key, and version ID uniquely identify each object, Amazon S3 can be thought of as a basic data map between "bucket + key + version" and the object itself. Every object in Amazon S3 can be uniquely addressed through the combination of the web service endpoint, bucket name, key, and optionally, a version. For example, in the URL http://doc.s3.amazonaws.com/2006-03-01/AmazonS3.wsdl, "doc" is the name of the bucket and "2006-03-01/AmazonS3.wsdl" is the key.
Regions
You can choose the geographical region where Amazon S3 will store the buckets you create. You might choose a region to optimize latency, minimize costs, or address regulatory requirements. Amazon S3 currently supports the following regions:
•	US East (N. Virginia) Region Uses Amazon S3 servers in Northern Virginia
•	US East (Ohio) Region Uses Amazon S3 servers in Columbus Ohio
•	US West (N. California) Region Uses Amazon S3 servers in Northern California
•	US West (Oregon) Region Uses Amazon S3 servers in Oregon
•	Canada (Central) Region Uses Amazon S3 servers in Canada
•	Asia Pacific (Mumbai) Region Uses Amazon S3 servers in Mumbai
•	Asia Pacific (Seoul) Region Uses Amazon S3 servers in Seoul
•	Asia Pacific (Singapore) Region Uses Amazon S3 servers in Singapore
•	Asia Pacific (Sydney) Region Uses Amazon S3 servers in Sydney
•	Asia Pacific (Tokyo) Region Uses Amazon S3 servers in Tokyo
•	EU (Frankfurt) Region Uses Amazon S3 servers in Frankfurt
•	EU (Ireland) Region Uses Amazon S3 servers in Ireland
•	EU (London) Region Uses Amazon S3 servers in London
•	South America (São Paulo) Region Uses Amazon S3 servers in Sao Paulo
Objects stored in a region never leave the region unless you explicitly transfer them to another region. For example, objects stored in the EU (Ireland) region never leave it. 
Amazon S3 Data Consistency Model
Amazon S3 provides read-after-write consistency for PUTS of new objects in your S3 bucket in all regions with one caveat. The caveat is that if you make a HEAD or GET request to the key name (to find if the object exists) before creating the object, Amazon S3 provides eventual consistency for read-after-write. Amazon S3 offers eventual consistency for overwrite PUTS and DELETES in all regions. Updates to a single key are atomic. For example, if you PUT to an existing key, a subsequent read might return the old data or the updated data, but it will never write corrupted or partial data. Amazon S3 achieves high availability by replicating data across multiple servers within Amazon's data centers. If a PUT request is successful, your data is safely stored. However, information about the changes must replicate across Amazon S3, which can take some time, and so you might observe the following behaviors:
•	A process writes a new object to Amazon S3 and immediately lists keys within its bucket. Until the change is fully propagated, the object might not appear in the list.
•	A process replaces an existing object and immediately attempts to read it. Until the change is fully propagated, Amazon S3 might return the prior data.
•	A process deletes an existing object and immediately attempts to read it. Until the deletion is fully propagated, Amazon S3 might return the deleted data.
•	A process deletes an existing object and immediately lists keys within its bucket. Until the deletion is fully propagated, Amazon S3 might list the deleted object.








Granting Access to a Single S3 Bucket Using Amazon IAM

Step 1 :- Login to the IAM AWS console
Login as the owner of the AWS account. Click the IAM tab.

Step 2 :- Create an account alias
This step is optional, but it gives you a nice login URL for your users. Add an account alias in the AWS Account Alias section of the IAM console. Then, your login URL will be youralias.signin.aws.amazon.com. If you don’t do this, your login page URL will be a bunch of random numbers.
Step 3 :- Create a new group or a new user
With IAM you can create a group that has certain permissions, and then assign users to that group. Or, you can just create users piecemeal, but then you can’t reuse permissions. If you want a group, create it first. Then create a user and assign it to that group.
Step 4 :- Set a password for the new user
Click the new user you’ve created and then click the Security Credentials tab. On that page, you can click Manage Password to add a password for your user. Without a password, the user won’t be able to login to the AWS console. Make sure your user knows to use the login page from step #2 in order to login — they can’t use the regular AWS login page. You’ll notice your user also has a AWS access key created: API clients using this key will have the same permissions as the user would in the AWS console.
Step 5 :- Add permissions for your user
Permissions are added either on the group the user is in, or if you decided not to create a group, the user account itself. Click the user or group, then click the Permissions tab. Here you can see which permissions policies are currently attached to the group or user. Click the Attach Policy button. You’ll get a pop-up where you can Manage User Permissions. Here you can select a prerolled policy, use the Policy Generator, or just paste in a custom policy.
There are two permissions that need to be added in order for your user to be able to login, see the bucket list in the S3 console, and manage the one bucket you’ve assigned.
To manage the bucket, you need to grant the s3:* action for the bucket you designate. AWS policies designate resources by their Amazon Resource Name, or ARN and for S3 buckets, they look like: arn:aws:s3:::bucket-name-here. So to grant your user full access to your bucket, you’d paste the policy:


{
  "Statement": [
    {
      "Action": "s3:*",
      "Effect": "Allow",
      "Resource": [
        "arn:aws:s3:::4ormat-knowledge-base",
        "arn:aws:s3:::4ormat-knowledge-base/*"
      ]
    }
  ]
}
Now, you would think that this would be enough to enable the user to use the S3 console to manage the bucket, but you’d be wrong. Turns out the user needs one more permission to do the initial listing of the buckets in order to be able to select a bucket, and its called s3:ListAllMyBuckets. You need to add that permissions too, and it looks like this:
{
  "Statement": [
    {
      "Effect": "Allow",
      "Action": "s3:ListAllMyBuckets",
      "Resource": "arn:aws:s3:::*"
    }
  ]
}
Spring Cloud AWS with Spring Boot
Amazon provides a Java SDK to issue requests for the all services provided by the Amazon Web Service platform. Using the SDK, application developers still have to integrate the SDK into their application with a considerable amount of infrastructure related code. Spring Cloud AWS provides application developers already integrated Spring-based modules to consume services and avoid infrastructure related code as much as possible. The Spring Cloud AWS module provides a module set so that application developers can arrange the dependencies based on their needs for the particular services. The graphic below provides a general overview of all Spring Cloud AWS modules along with the service support for the respective Spring Cloud AWS services.
Spring Cloud AWS Context
 delivers access to the Simple Storage Service via the Spring resource loader abstraction. Moreover developers can send e-mails using the Simple E-Mail Service and the Spring mail abstraction. Further the developers can introduce declarative caching using the Spring caching support and the ElastiCache caching service
Spring boot pm.xml
<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>1.5.1.RELEASE</version>
		<relativePath /> <!-- lookup parent from repository -->
</parent>

	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-tomcat</artifactId>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>org.springframework.cloud</groupId>
			<artifactId>spring-cloud-aws-context</artifactId>
			<version>1.0.2.RELEASE</version>
		</dependency>
    </dependencies>
AWS Configuration Class In Spring Boot

@Configuration
public class AWSConfiguration {
	
	private String accessKey="";
	
	private String secretKey="";

	private String region="AP_SOUTHEAST_1";	

	@Bean
	public BasicAWSCredentials basicAWSCredentials() {
		return new BasicAWSCredentials(accessKey, secretKey);
	}

	@Bean
	public AmazonS3Client amazonS3Client(AWSCredentials awsCredentials) {
		AmazonS3Client amazonS3Client = new AmazonS3Client(awsCredentials);
		amazonS3Client.setRegion(Region.getRegion(Regions.AP_SOUTHEAST_1));
		return amazonS3Client;
	}
}
This is configuration file in spring boot application to create AmazonS3Client object using this object we can many service for object store, retrieve, delete, with key value pair in s3 bucket, and also we can creating, deleting buckets etc..

S3serviceImpl class
This class have some of AmazonS3Client provided methods
@Service
public class S3serviceImpl implements S3service {

	
	@Autowired
	private AmazonS3Client amazonS3Client;
	
	/*
	 * This method is get all Buckets details in our s3
	 */
	
	public List<Bucket> listAllBucketNames() throws DataNotFoundException {
		if (amazonS3Client.listBuckets().size() != 0) {
			return amazonS3Client.listBuckets();
		} else {
			throw new DataNotFoundException(
					DataNotFoundException.BUCKETS_NOT_FOUND);
		}

	}

	/**
	 * This method is used to add object into to a specific bucket with key
	 */
	public String uploadFileToSpecificBucket(String bucketName, String key,
			String path) throws DataNotFoundException {
		if (amazonS3Client.doesBucketExist(bucketName)) {
			File file = new File(path);
			if (file.exists()) {
				amazonS3Client.putObject(new PutObjectRequest(bucketName, key,file));
				return "Successfully file uploaded";
			} else {
				throw new DataNotFoundException(DataNotFoundException.INVALID_BUCKET_NAME);
			}
		} else {
			throw new DataNotFoundException(
					DataNotFoundException.INVALID_BUCKET_NAME);
		}
	}

	/**
	 * This method id used to create a new bucket in s3
	 */
	public String createNewBuket(String bucketName)
			throws HandleAmazonServiceException, HandleAmazonClientException,Conflict {
		try {
			if (!(amazonS3Client.doesBucketExist(bucketName))) {				
				amazonS3Client.createBucket(new CreateBucketRequest(bucketName));
				String bucketLocation = amazonS3Client.getBucketLocation(new GetBucketLocationRequest(bucketName));
				System.out.println("bucket location = " + bucketLocation);
				return "Successfully bucket created." + bucketLocation;
			} else {
				throw new Conflict("Duplicate bucket name");
			}
		} catch (AmazonServiceException ase) {
			throw new HandleAmazonServiceException(ase.getMessage(),
					ase.getStatusCode());
		} catch (AmazonClientException ace) {
			throw new HandleAmazonClientException(ace.getMessage());
		}
	}
	
	/**
	 * This method is used to get all objects summary in a specific bucket 
	 */
	public List<S3ObjectSummary> getBucketObjectSummaries(String bucketName)
			throws HandleAmazonClientException, HandleAmazonServiceException {
		List<S3ObjectSummary> s3ObjectSummaries = new ArrayList<S3ObjectSummary>();
		try {
			ListObjectsRequest listObjectsRequest = new ListObjectsRequest()
					.withBucketName(bucketName);
			ObjectListing objectListing;
			do {
				objectListing = amazonS3Client.listObjects(listObjectsRequest);
				for (S3ObjectSummary objectSummary : objectListing
						.getObjectSummaries()) {
					s3ObjectSummaries.add(objectSummary);
				}
				listObjectsRequest.setMarker(objectListing.getNextMarker());
			} while (objectListing.isTruncated());
		} catch (AmazonServiceException ase) {
			throw new HandleAmazonServiceException(ase.getMessage(),
					ase.getStatusCode());
		} catch (AmazonClientException ace) {
			throw new HandleAmazonClientException(ace.getMessage());
		}
		return s3ObjectSummaries;
	}

	/**
	 * This method is used to list out the all bucket names in a s3
	 */
	public List<String> getBucketObjectNames(String bucketName)
			throws HandleAmazonClientException, HandleAmazonServiceException {
		List<String> s3ObjectNames = new ArrayList<String>();
		List<S3ObjectSummary> s3ObjectSummaries = getBucketObjectSummaries(bucketName);
		for (S3ObjectSummary s3ObjectSummary : s3ObjectSummaries) {
			s3ObjectNames.add(s3ObjectSummary.getKey());
		}
		return s3ObjectNames;
	}
	
    /*
     * This method is used to delete  specific object in a bucket
     */
	public String deleteObjectInBucket(String bucketName, String key)
			throws HandleAmazonServiceException, HandleAmazonClientException,DataNotFoundException {
		try {
			S3Object object = amazonS3Client.getObject(bucketName, key);
			if (object != null) {
				amazonS3Client.deleteObject(new DeleteObjectRequest(bucketName,key));
				return "Successfuly deleted";
			} else {
				throw new DataNotFoundException(DataNotFoundException.OJECT_DOES_NOT_EXIST);
			}			
		} catch (AmazonServiceException ase) {
			throw new HandleAmazonServiceException(ase.getMessage(),ase.getStatusCode());
		} catch (AmazonClientException ace) {
			throw new HandleAmazonClientException(ace.getMessage());
		}
	}

	/**
	 * This method is used to download the specific object from bucket.
	 * And store into specified path and returns byte[] of the object
	 */
	public byte[] downLoadObjectformBucket(String bucketName, String key,String         path)
			throws IOException, DataNotFoundException {
		GetObjectRequest getObjectRequest = new GetObjectRequest(bucketName,key);
		S3Object s3Object = amazonS3Client.getObject(getObjectRequest);
		if (s3Object != null) {
			S3ObjectInputStream objectInputStream = s3Object.getObjectContent();
			byte[] byteRespose=IOUtils.toByteArray(objectInputStream);
			FileUtils.writeByteArrayToFile(new File("F://new.txt"), byteRespose);
			return byteRespose;
		} else {
			throw new DataNotFoundException(DataNotFoundException.OJECT_DOES_NOT_EXIST);
		}
	}
	
    /*
     *  This method is used to delete empty bucket in s3
     */	
	public String deleteBuket(String bucketName) throws DataNotFoundException {
		if (amazonS3Client.doesBucketExist(bucketName)) {
			amazonS3Client.deleteBucket(bucketName);
			return "Bucket deleted successfully";
		}else {
			throw new DataNotFoundException(DataNotFoundException.INVALID_BUCKET_NAME);
		}
	}

	/*
	 * This method is used to generate pre signed url for particular object in bucket 
	 */
	public String GeneratePresignedUrl(String bucketName, String key) {
		  GeneratePresignedUrlRequest generatePresignedUrlRequest = new GeneratePresignedUrlRequest(bucketName, key);
          generatePresignedUrlRequest.setMethod(HttpMethod.GET);
          generatePresignedUrlRequest.setExpiration(DateTime.now().plusYears(1).toDate());
          URL signedUrl = amazonS3Client.generatePresignedUrl(generatePresignedUrlRequest); 
          return  signedUrl.toString();
	}

}

