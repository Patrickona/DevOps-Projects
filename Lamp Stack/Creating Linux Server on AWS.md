### Creating Virtual Linux Server on AWS ###
This documentation shows the steps taken to create a Linux virtual server on AWS 
# Creating an EC2 instance #
We first create a security group. This is a firewall, setting the rules on the inbound/outband traffic for our instance. In this case we have allowed **all traffic** for both inbound and outband traffic
Note: this is for test case purposes and in building your own EC2 instance, it is expected you will set more stringent rules for better security.
![Below screenshot references security group rule]
