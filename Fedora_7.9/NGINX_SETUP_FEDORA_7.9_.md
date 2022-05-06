# Setting up Django Server on Oracle 7.9

#### Installation of Nginx Server 
##### Prerequisit
* Extra Packages for Enterprise Linux (or EPEL) is a Fedora Special Interest Group that creates, maintains, and manages a high quality set of additional packages for Enterprise Linux.

  > yum install https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm*
                                                                                                                                                                                          

##### Step 1 — Installing the Nginx Web Server
  > yum install nginx 

##### Step 2 — After Installing the Nginx Web Server we need to enable and restart it

  > systemctl enable nginx 
  
  > systemctl restart nginx

_Note : If you face any issue while executing above line , just kill the port number 80 to overcome the issue_

  > fuser -k 80/tcp


##### Step 3 — Check the status of Nginx Web Server
  > systemctl status nginx


##### Step 4 - Check the public ip of your server
  > ip a


##### Step 5 - Check if installation is successful
  > Copy the ip address and paste in browser

  > You should be able to see Nginx landing page

                                                                                                                                                                                   