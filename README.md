![Image](https://w5t2f7e6.stackpathcdn.com/wp-content/uploads/2022/01/blog_img_dnsfiltering_cover-1024x427.jpg)

# Understanding DNS
We will be exploring DNS in this tutorial. Please make sure you have followed along thus far with the previous labs in order to proceed. The tutorial will cover A-Records on the server, the creation and deletion of records, as well as briefly touching on CNAME records and Root hints.

## Environments and Technologies Used

- Microsoft Azure (Virtual Machines/Compute)
- Remote Desktop Connection (RDC)
- Active Directory Domain Services
- Command Prompt

## Operating Systems Used 

- Windows Server 2022
- Windows 10 Pro (22H2)

## A-Records

Make sure that you are logged into both DC-1 and CLIENT under your admin account (mine being mydomain.com\john_admin).

![image](https://i.imgur.com/aFzME2F.png)

Under CLIENT go into command prompt and type `ping mainframe` and you will notice it cannot be found. The CLIENT will first attempt to check its own cache for the domain name, then its host file, and finally the DNS attached to the Network Interface Card. Once it has cycled through these options with nothing to retrieve, it returns a basic failure because no IP address is found to ping. We get the same result even with `nslookup mainframe`.

![Image](

We will switch back to DC-1 in order to create an A-Record so that it can be discovered by our computers.

On the Server Mangager, dashboard, click on Tools, DNS. Click the drop down on DC-1, Forward Lookup Zones, click  "mydomain.com" (name of your domain) and observe your other A-Records (hostname to ip address mapping is what that is). Right click and manually create a New Host (A or AAAA) and name it mainframe, change the IP address to the same as DC-1 for the sake of ease and create it and it will populate next to your other A-Records. 

In **Server Manager**'s **Dashboard**, click on **Tools**, then select **DNS**. Click the dropdown menu for **DC-1** under **Forward Lookup Zones**, and choose **mydomain.com** (the name of your domain) to observe your other A-Records (which represent hostname-to-IP address mappings). Right-click to manually create a **New Host (A or AAAA record)**, name it "mainframe," change the IP address to match that of **DC-1** for simplicity, and create it. It will then appear alongside your other A-Records.
