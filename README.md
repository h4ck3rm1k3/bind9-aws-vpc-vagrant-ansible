# test-repo
testing

vagrant/Vagrantfile

#
external = File.read '<path to local system file containing AWS access keys>':
$aws_key_id = "<...>"
$aws_secret = "<...>"

#  { :instance_name => 'dns-a-1', :ssh_user => 'ubuntu', :instance_ip => '10.10.10.2', :public_ip => 'false', :ami => 'ami-XXXXXXXX', :subnet => 'subnet-XXXXXXXX', :sg => 'sg-XXXXXXX', :instance_type => 't2.micro' }
instance_name = Name tag
ssh_user = AMI's default sudo user
instance_ip = private IP if desired to set statically
public_ip = 'true' if desired, 'false' if not set
ami = ami id
subnet = VPC's subnet
sg = security group id
instance_type = instance type

#ec2 keypair name
aws.keypair_name = "<...>"

#local pem file used to ssh into instance; associated with aws.keypair_name
override.ssh.private_key_path = "<...>"

aws.availability_zone = "us-east-1d"


#ansible/ansible_hosts -- populate ansible hosts file with private ip and hostname of dns instance
[aws-dns] 
<local ip of dns instance> hostname=<hostname of dns instance>

ansible/group_vars
???

#ansible/roles/util-dns-bind-config/files/db.site
change 10.10.10.2 to desired ip of your dns host
change testsite to whatever your site suffix will be 

#named.conf.local
testsite to your site

#named.conf.options -- make specific for your VPC
forwarders {172.31.0.2; };
allow-recursion {localnets; 172.31.2.0/24;};


