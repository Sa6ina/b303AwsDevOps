# Hands-on Boto3

## Outline

- Part 1 - Installation and Configuration

- Part 2 - Examples of Boto3 usage


## Part 1 - Installation and Configuration

- open an IDE on Cloud9

- use the terminal window to configure before using boto3

- type to see aws cli version and that aws cli is based on botocore

```bash
aws --version
```

- type to see installed packages

```bash
pip freeze
```

- To install Boto3, open your terminal (Commands below works also for Command Prompt-Windows), and type the code below for the latest version.

```bash
pip install boto3
```

- If you are using Python3, try:

```bash
pip3 install boto3
```
- To be able to use Boto3, you need AWS Credential (Access Key and Secret Key). If you have AWS CLI installed and configured you don't need to do anything. If you don't, create '.aws' directory under home (~), and then create config and credentials file with the necessary data in.

```bash
aws configure
```
- Then enter the credentials:

```bash
AWS Access Key ID [****************EMOJ]: 
AWS Secret Access Key [****************/aND]: 
Default region name [us-east-1]: 
Default output format [yaml]: 
```


## Part 2 - Examples of Boto3 usage

### STEP-1: List your S3 Buckets:


- To be able to use Boto3, first you need to import it (import boto3), then you can type other commands regarding it. Create a file  called s3list.py and put the code below in it.


```python
import boto3

# Use Amazon S3
s3 = boto3.resource('s3')

# Print out all bucket names
for bucket in s3.buckets.all():
    print(bucket.name)
```

### STEP-2: Create an S3 bucket and list buckets again

Create a file a called s3cb.py and put the code below in it.

```python
import boto3

# Use Amazon S3
s3 = boto3.resource('s3')

# Create a new bucket
s3.create_bucket(Bucket='my-boto3-bucket-yourname')

# Print out all bucket names
for bucket in s3.buckets.all():
    print(bucket.name)
```

- Show that you can see the new bucket.


### STEP-3: Upload a file to the S3 Bucket

- You need a file in your working directory (test.jpg for this case) to upload.  

- Create a file in your working directory named "test.jpg"

- Create a file a called s3put.py and put the code below in it.

```python
import boto3

# Use Amazon S3
s3 = boto3.resource('s3')

# Upload a new file
data = open('test.jpg', 'rb')
s3.Bucket('my-boto3-bucket-yourname').put_object(Key='test.jpg', Body=data)
```
- Check the "my-boto3-bucket", if your script works fine, you should be able to see your test file in your bucket.

### STEP-4: Launch, Stop and Terminate Instances


- Create a file a called ec2launch.py and put the code below in it to launch an Ubuntu instance. You may change the instance ID to create different types of instances.

```python
import boto3
ec2 = boto3.resource('ec2')

# create a new EC2 instance
instances = ec2.create_instances(
     ImageId='ami-09e67e426f25ce0d7', # ubuntu ami id
     MinCount=1,
     MaxCount=1,
     InstanceType='t2.micro',
     KeyName='yourkeypair without .pem here' # put your keypair
 )
```

- Checked the newly created instance

- Create a file a called ec2stop.py and put the code below in it to stop EC2 instance via boto3.


```python
import boto3
ec2 = boto3.resource('ec2')
ec2.Instance('your InstanceID').stop() # put your instance id
```

- Create a file a called ec2terminate.py and put the code below in it to terminate EC2 instance via boto3.

```python
import boto3
ec2 = boto3.resource('ec2')
ec2.Instance('your InstanceID').terminate() # put your instance id
```
- Check the EC2 instance status from console.

---

Links:

https://aws.amazon.com/sdk-for-python/

https://boto3.amazonaws.com/v1/documentation/api/latest/index.htmlcd