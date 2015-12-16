# -*- mode: ruby -*-
# vi: set ft=ruby :

AWS_ACCESS_KEY_ID = ENV['AWS_ACCESS_KEY_ID']
AWS_SECRET_ACCESS_KEY = ENV['AWS_SECRET_ACCESS_KEY']
PRIVATE_KEY_PATH = ENV['PRIVATE_KEY_PATH']

Vagrant.configure(2) do |config|
  config.vm.box = "dummy"

  config.vm.provider :aws do |aws, override|
    aws.access_key_id = AWS_ACCESS_KEY_ID
    aws.secret_access_key = AWS_SECRET_ACCESS_KEY

    aws.associate_public_ip = true
    
    # The Concourse AMI is currently only available in us-east-1
    aws.ami = 'ami-5c104436'
    aws.region = 'us-east-1'

    # t2 not available for this AMI, fails with error:
    # Virtualization type 'hvm' is required for instances of type 't2.medium'
    aws.instance_type = 'm3.large'

    # Manually created. Could be a dedicated "Concourse build" subnet
    aws.subnet_id = 'subnet-b99f4fcf'

    # Manually created. Could be a dedicated "Concourse build" security group
    aws.security_groups = ['sg-f5ac6a8c']

    # Could be replaced by key per user
    aws.keypair_name = 'insecure-deployer'
    override.ssh.username = "ubuntu"
    override.ssh.private_key_path = PRIVATE_KEY_PATH
  end

end
