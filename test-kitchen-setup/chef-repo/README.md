Test-Kitchen Setup with AWS:

Test Kitchen:

What is Kitchen?

Kitchen is a test harness tool to execute Infrastructure as Code(IaC) on one or more platforms
To execute in multiple platforms kitchen have a driver plugin architecture.


Cookbook Development Cycle Consists of following steps

 a. Write Chef Code.
 b. Upload the code to the server using berks.
 c. Wait for Convergence on the node or run chef-client.
 d. Verify if the code written is working.

Problems with this approach:

 a. Need to upload every version to the cookbook, which is untested.
 b. This might lead to some non working versions.
 c. Process is bit more lengthy.

With Kitchen:

 Cookbook development cycle consists of the following steps.

   a. Write Chef code.
   b. Verify the written code with test kitchen.
   c. Upload the code to the chef server using berks.
   d. Wait for Convergence on the node or run chef-client.


Setup Workstation:

  Lets look at different environments using different drivers.
 
  AWS Driver for Linux:

   Prerequisites:

       SSH Client: Git or Putty
       ChefDk installed

 Generate cookbook on the workstation:

  chef generate cookbook <cookbookname>

  chef generate cookbook testkitchendemo

  cd testkitchendemo

 
AWS Preparation:

  1. Create IAM user with at least EC2 permissions (In this demonstration i would create user with Admin.
  2. Authenticate Test Kitchen with AWS
  3. If your workstation is
     Linux or mac: Navigate to file at ~/.aws/credentials
     Windows: Navigate to file at %USERPROFILE%.aws\credentials         
  4. Enter ACCESS_KEY from the iam user to aws_access_key_id and Secret key to aws_secret_access_key
  5. Other way is to use the aws cli command.
         aws configure

    
Go to Kitchen yaml file and try to modify as per requirement 

 $ cd  chef-repo/cookbooks/kitchendemo/kitchen.yml
 $ vim chef-repo/cookbooks/kitchendemo/kitchen.yml

Please check the configuration here, I have modify as my requirement. Since I am planning to setup kitchen in AWS. 

driver:
  name: ec2
  aws_ssh_key_id: linux-test
  security_group_ids: ["sg-06e03bfb18c04fc60"]
  region: us-east-1
  availability_zone: e
  subnet_id: subnet-e1e336df
  instance_type: t2.micro
  image_id: 'ami-0bcc094591f354be2'
  associate_public_ip: true
  interface: dns

transport:
   ssh_key: "/root/chef/linux-test.pem"
   connection_timeout: 10
   connection_retries: 3
   username: ubuntu

verifier:
  name: inspec

platforms:
  - name: ubuntu-18.04

suites:
  - name: default
    run_list:
      - recipe[kitchendemo::default]
    verifier:
      inspec_tests:
        - test/integration/default
    attributes:
 

Once you setup 

kitchen list
kitchen create
kitchen list
kitchen converge


* Now login into the ec2 machine & verify
    ```
    kitchen login


* Once you finish your testing you can continue updating cookbooks & converge.
    * Destroy the created ec2 machine using
    ```
    kitchen destroy



