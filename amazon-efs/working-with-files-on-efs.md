# Working with Files on EFS

## Launch EC2 instances
1. Create a security group
aws ec2 create-security-group --group-name EFS-Lab --description "Temporary SG for the EC2 and EBS Lab"
2. Add a rule for SSH inbound to the security group
aws ec2 authorize-security-group-ingress --group-name EFS-Lab --protocol tcp --port 22 --cidr 0.0.0.0/0
3. Add rule to the security group to allow the NFS protocol from group members
aws ec2 authorize-security-group-ingress --group-id sg-xxxxxxxxxxxxxxxxx --protocol tcp --port 2049 --source-group sg-xxxxxxxxxxxxxxxxx
4. Launch instance in ap-southeast-1a
aws ec2 run-instances --image-id ami-039a8ebebdd2a1def --instance-type t3.micro --placement AvailabilityZone=ap-southeast-1a --security-group-ids sg-05c8dc3ba87f35094
5. Launch instance in ap-southeast-1b
aws ec2 run-instances --image-id ami-039a8ebebdd2a1def --instance-type t3.micro --placement AvailabilityZone=ap-southeast-1b --security-group-ids sg-05c8dc3ba87f35094

## Create an EFS File System
1. Create an EFS file system (console, and add the EFS-Lab security group to the mount targets for each AZ

## Mount using the NFS Client (perform steps on both instances)
1. Create an EFS mount point
mkdir ~/efs-mount-point
2. Install NFS client
sudo yum -y install nfs-utils
3. Mount using the EFS client
sudo mount -t nfs4 -o nfsvers=4.1,rsize=1048576,wsize=1048576,hard,timeo=600,retrans=2,noresvport fs-0b823ccab22e6d568.efs.ap-southeast-1.amazonaws.com:/ ~/efs-mount-point
4. Create a file on the file system
5. Add a file system policy to enforce encryption in-transit
6. Unmount (make sure to change directory out of efs-mount-point first)
sudo umount ~/efs-mount-point
4. Mount again using the EFS client (what happens?)

## Mount using the EFS utils (perform steps on both instances)
1. Install EFS utils
sudo yum install -y amazon-efs-utils
2. Mount using the EFS mount helper
sudo mount -t efs -o tls fs-0b823ccab22e6d568.efs.ap-southeast-1.amazonaws.com:/ ~/efs-mount-point