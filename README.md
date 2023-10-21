![Image](https://w5t2f7e6.stackpathcdn.com/wp-content/uploads/2022/01/blog_img_dnsfiltering_cover-1024x427.jpg)

# Understanding DNS
We will be exploring DNS in this tutorial. Please make sure you have followed along thus far with the previous labs in order to proceed. The tutorial will cover A-Records on the server, the creation and deletion of records, as well as briefly touching on CNAME records.

*Always delete your resource groups and other environments in Azure to avoid incurring any unwanted charges on your free credits or actual money. Keep resources open at your own discretion.*

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

![image](https://i.imgur.com/Q6PPZL7.png)

Under CLIENT go into command prompt and type `ping mainframe` and you will notice it cannot be found. The CLIENT will first attempt to check its own cache for the domain name, then its host file, and finally the DNS attached to the Network Interface Card. Once it has cycled through these options with nothing to retrieve, it returns a basic failure because no IP address is found to ping. We get the same result even with `nslookup mainframe`.

We will switch back to DC-1 in order to create an A-Record so that it can be discovered by our computers.

![Image](https://i.imgur.com/gZUr7dq.png)

In **Server Manager**'s **Dashboard**, click on **Tools**, then select **DNS**. Click the dropdown menu for **DC-1** under **Forward Lookup Zones**, and choose **mydomain.com** (the name of your domain) to observe your other A-Records (which represent hostname-to-IP address mappings). Right-click to manually create a **New Host (A or AAAA record)**, name it "mainframe," change the IP address to match that of **DC-1** for simplicity, and create it. It will then appear alongside your other A-Records.

![Image](https://i.imgur.com/rXd2qaH.png)

With this new record cataloged, we will return to the CLIENT and ping the mainframe once more, and you will now have a connection.

---

## DNS Cache

![Image](https://i.imgur.com/iSKeMDf.png)

Now that we have some data in our DNS cache we can now manipulate and observe the DNS cache. Return to DC-1 and change mainframe's record address to 8.8.8.8 (Google) and refresh the DNS by right-clicking DC-1 and clicking Refresh

![Image](https://i.imgur.com/D59LazB.png)

On the CLIENT, we will ping the mainframe again. You will notice that it has not changed to 8.8.8.8, but instead, it still has the IP of DC-1. The reason for this is that the old DNS configuration is logged in the DNS cache. But no worries, we have a fix.

![Image](https://i.imgur.com/ZVFXnwy.png)

![Image](https://i.imgur.com/xUWb7TI.png)

Run `ipconfig /displaydns`, and you will once again see that the old IP is logged for the mainframe. To update the DNS, run `ipconfig /flushdns` (if asked for required elevation, ensure you are running Command Prompt as an administrator), and then ping the mainframe once more. With the cache having been cleared using the flush command, the computer can now be in tune with the up-to-date resources.

---

## CNAME Record

![Image](https://i.imgur.com/hvAahXU.png)

To end this tutorial we will touch on CNAME records (we will effecitley map names to other names). Return to DC-1 and repeat the steps we did for A-Records but instead of **New Host (A or AAAA record)** we will create New Alias (CNAME). Type "Search" for the Alias name and www.google.com for the Fully qualified dmain name (FQDN). Go back to CLIENT and repeat the ping and nslookup process to see our success (same process where you are unable to ping to search without the creation of a CNAME but now you can after generation).

![Image](https://i.imgur.com/xA2RV4R.png)

To conclude this tutorial, we will cover CNAME records, effectively mapping names to other names. Return to DC-1 and follow the same steps as we did for A-Records, with one exception: instead of creating a **New Host (A or AAAA record)**, we will create a **New Alias (CNAME)**. Enter "search" as the **Alias name** and "www.google.com" as the Fully Qualified Domain Name (FQDN). Now, return to CLIENT and repeat the ping and nslookup process to observe our success. This is the same process as before, where you couldn't ping "search" without the creation of a CNAME, but now you can after its creation.

---
The resolution of at least some connectivity issues being dumbed down to the simple flushing of a DNS cache amuses me, but it is also an invaluable tool for troubleshooting that I'm glad we've learned. Next, we shall explore [file permissions](https://github.com/NicholasToon/Understanding-File-Permissions-in-Azure). Thank you for your time.











