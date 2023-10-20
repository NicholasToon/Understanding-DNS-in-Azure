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

Under CLIENT go into command prompt and type `ping mainfraime` and you will notice it cannot be found. The CLIENT will first attempt to check its own cache for the domain name, then its host file, and finally the DNS attached to the Network Interface Card. Once it has cycled through these options with nothing to retrieve, it returns a basic failure because no IP address is found to ping. We get the same result even with `nslookup mainframe`.
