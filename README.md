Read me

This repository contains configurations gathered from a variety of videos on YouTube. Kudos to Let's Learn YT (https://www.youtube.com/watch?v=5JqxghWCCiI) for inspiring me to actually log my progress on GitHub. Thank you for providing your initial configurations to the SD-WAN lab. 

Although I have setup the SD-WAB lab on CML, this will be my firt time using Eve-NG for any lab. 


===========================
Note:
When setting up vManage you will need to create an additional drive 100GB using the command line (SSH). 

You will also need to give it pleanty of RAM. I have found out that using 24GB or more is necessary. If you fail to do this, your Cisco SD-WAN GUI for vManaged will not be available. 

I am currently using 32768 MB or 32 GB of RAM.

You can try some commands to check the status of services. 

`request nms all status`
`request nms all start`

Once you have configured vManage, use the vManage IP for VPN 512 on the browser. https://192.168.1.1:8443

To logon to vManage using the console, wait for "System Ready" befor using the default credentials to login. User admin, password admin.

![VManage Login on Ubuntu](vManage-Login.PNG)

This project is a work in progress. Since this scenario does not have internet access, it causes the ubuntu machine to be really slow when accessing vManage GUI. 



=======================================
When working with Certificate Authority for vManage I encounter the error that my vmanger_crt certificate did not have the serial number of the device. ![Putty from Eve-NG](Putty.PNG)I though I was copying my cert from the SSH Putty session, but the QEMU for Ubuntu does not accept paste from external sources. ![SSH from Ubuntu](<Ubuntu _SSH.PNG>)To get around this issue I SSH from Ubuntu and copy the certificate into vManage GUI successfully. ![Successful cert import into vManage GUI](vManageCeret.PNG)



========================================
Adding vBond to vManage
I had the hardest time adding vBond to vManage. This is because VPN 0 now requires tunnel interface and then have the services allowed through the tunnel. The initial configuration was using version 16 of Cisco SD-Wan, and the images I am using are much newer ver. 20. 

The good news is that is not too hard to add the config using the CLI. 
`Configure Terminal`
`VPN 0`
`Interface ge0/0`
`Tunnel-Interface`
`Encapsulation IPsec`
`Allow-Service All`

then don't forget to commit your changes. 
`commit`

![vBond finally added](<vbond cert.PNG>)
![CSR](vbond_csr.PNG)

I have been getting stuck on adding vEdge to vManage. Both vEdges are reacheable from vManage 172.16.1.1 and 172.16.2.1. 

I have successfully create the .csr and then had them signed by vManage, and imported the vEdge_crt successfully. 

The issue is when attempting to upload the WAN Edge List .csv file. I am including the chasis number and serial number. You can get these by using the `Show Certificate Serial` command. 

No matter how I import it I continue to get an error. 

I strongly believe that this has something to do with my not having a Cisco Smart Account. There you can create the templates that can be then uploaded into vManage. 

This is exactly the same place I got stucked while using Cisco Modeling Labs when I attempted a similar lab. 

For now this is all for this project until I find a solution to this issue. 

If you made it here, I hope you enjoyed the lab journey. Eventhough I could not finalize it, it was fun. 
