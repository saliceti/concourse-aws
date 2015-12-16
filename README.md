# Concourse AWS

Create a Concourse-lite AWS instance using Vagrant.

# Prepare

## Create VPC in us-east-1
It must have Internet gateway, routing configured and at least one subnet.

## Create security group in VPC
It must allow inbound ports 22 and 8080.

## Customise Vagrantfile

* `ami`. Latest Concourse lite AMIs can be found [here](https://console.aws.amazon.com/ec2/v2/home?region=us-east-1#Images:visibility=public-images;search=concourse;sort=name)
* `subnet_id`. ID of subnet created above.
* `security_groups`. ID of security group created above.
* `keypair_name`. Keypair existing in AWS for which you have the private key.

## Download dummy box

```
$ vagrant box add dummy https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
==> box: Adding box 'dummy' (v0) for provider: 
    box: Downloading: https://github.com/mitchellh/vagrant-aws/raw/master/dummy.box
==> box: Successfully added box 'dummy' (v0) for 'aws'!
```

# Run

```
$ PRIVATE_KEY_PATH=<path/to/private_key> vagrant up --provider aws
...
==> default: Waiting for instance to become "ready"...
==> default: Waiting for SSH to become available...
==> default: Machine is booted and ready for use!
```

It takes about 1:30 min

# Connect to Concourse

Find the instance public IP in the AWS console for example, then connect to port 8080 in a browser or with fly directly.

It has **no authentication**.

# Destroy
In the same directory:

```
$ vagrant destroy
    default: Are you sure you want to destroy the 'default' VM? [y/N] y
==> default: Terminating the instance...
```
