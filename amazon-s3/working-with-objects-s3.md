# Practice with the AWS CLI

1. Create a bucket (replace BUCKET-NAME with a unique name)
aws s3 mb s3://nlhmagbucket

2. Upload a single file
aws s3 cp localfile.txt s3://nlhmagbucket/

3. Upload a whole folder
aws s3 cp ./myfolder s3://nlhmagbucket/ --recursive

4. List all objects in a bucket
aws s3 ls s3://nlhmagbucket/

5. Download a single file
aws s3 cp s3://nlhmagbucket/localfile.txt ./downloaded.txt

6. Download everything in a bucket
aws s3 cp s3://nlhmagbucket/ ./localfolder --recursive

7. Delete a single object
aws s3 rm s3://nlhmagbucket/testfile1.txt

8. Delete all objects in a bucket
aws s3 rm s3://nlhmagbucket/ --recursive

9. Delete the bucket itself (must be empty first)
aws s3 rb s3://nlhmagbucket

# Use a Python Script for Uploading to S3

1. Create a new bucket for this test
aws s3 mb s3://nlhmagbucket
2. Install python
sudo yum install python3-pip
pip3 install boto3
3. Create python script ***and add/edit code (below), then save***
nano upload_to_s3.py 
4. Run the script
python3 upload_to_s3.py

***Python Code - update nlhmagbucket and FILE-NAME***

```python
import boto3

s3 = boto3.resource('s3')

# Replace with your S3 bucket name and the name to give the object
bucket_name = 'nlhmagbucket'
object_name = 'pythonfile.txt'

# Replace with the local file path to upload
file_path = '/home/cloudshell-user/pythonfile.txt'

# Upload the file to S3
try:
    s3.Bucket(bucket_name).upload_file(file_path, object_name)
    print('Successfully uploaded {} to s3://{}/{}'.format(file_path, bucket_name, object_name))
except Exception as e:
    print('Error uploading file to S3: {}'.format(e))
```
