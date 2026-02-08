# Launch instances with a tag
aws ec2 run-instances --image-id ami-039a8ebebdd2a1def --count 2 --instance-type t3.micro --tag-specifications 'ResourceType=instance,Tags=[{Key=Department,Value=Operations}]'

# CloudWatch Logs Insights query
fields @timestamp, @message | sort @timestamp desc | limit 25
