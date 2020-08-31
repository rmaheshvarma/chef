This is boot strap the chef clinet

1. First install the chef-workstation/Chef-DK on desrired environmnet wheather it is windows laptop or Linux Laptop or central server
2. Once you setup the chef-workstation/ChefDK. 
3. If it in cloud whether it is AWS/AZURE launch server.
4. Create a account in Hosted chef server. 
5. Once Launch the server Bootstarp the insatnce. 
6. If you want to bootstarp the launched AWS instance, in work station we have to download the started kit. 
7. How to Download the starter Kit.
8. From Hosted chef server, go to Administartion--> Plese slect the your Organization--> StartKIt.
9. You can create numer of oranizations, for each oranization we have one start kit. 
10. Once you dowload the starter kit, we have to keep that starte kit in Chef workstarting in our desire location. 
11. Once you dowload the start kit--> AGain again we shoud not doanlod the starter kit from same oranization, if you download the start kit again again we will loose the connectivity between, Chef workstation and Chef server/Hosted chef server. Becarefull while Downloading the starter kit second time. 

Note:
Before download the starter kit chek from you team/chek yourslef once and download the start-kit. 
Why we shoud not download again again, because, hosted chef server/chef server authentication details will be there and using this authentication, it will establish a connection from chef workstation to chef server. 


12. Once you download the start kit, AFter you exctract the starter kit. We can called it as "chef repo"
13. All the chef operations we have to do from "Chef-repo"

From "chef-repo" we have to to Bootstarp. 

Bootstarp commands:

cd <chef-repo>
knife --help
knife bootstrap --help

knife bootstrap <ipaddress> -x <username> -P <password> --sudo -N <nodename>

knife bootstrap <ipaddress> -x <username> -i <identityfile> --sudo -N <nodename>


example:

knife bootstrap 172.31.63.146 -x ubuntu -i /root/chef/linux-test.pem --sudo -N first-ubuntu






What is bootstap?


Chef bootstap is nothing but a Add a server to Chef server. 

Note:
Only During the bootstarp time only Chef work station and Chef-Node will communicate. Once bootstap will finish, chef workstation/ChefDK and Chef-node can not comminicate. 





chef-repo/.chef


config.rb  hostedchef.pem




cat config.rb
# See http://docs.chef.io/config_rb.html for more information on knife configuration options

current_dir = File.dirname(__FILE__)
log_level                :info
log_location             STDOUT
node_name                "rmaheshvarma"
client_key               "#{current_dir}/rmaheshvarma.pem"
chef_server_url          "https://api.chef.io/organizations/msrchef"
cookbook_path            ["#{current_dir}/../cookbooks"]




