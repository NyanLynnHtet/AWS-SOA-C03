# Launch instance, stop instance
1. Launch an EC2 instance
aws ec2 run-instances --image-id ami-0e70827346a834dca --instance-type t3.micro --placement AvailabilityZone=ap-southeast-7a
2. Stop the EC2 instance
aws ec2 stop-instances --instance-id i-0c4b9a5ac1e93e6fc
3. Terminate the EC2 instance
aws ec2 terminate-instances --instance-id i-0f8af4b40b2043b8d

## Python code for function
```python
import json

def lambda_handler(event, context):
    print('LogEC2StopInstance')
    print('Received event:', json.dumps(event, indent=2))
    return {
        'statusCode': 200,
        'body': 'Finished'
    }
```