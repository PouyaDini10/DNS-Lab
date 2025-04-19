# DNS-Lab

## Objective 

In this lab, I configured and tested DNS records within an Active Directory environment using Azure-hosted virtual machines. The exercises included creating and modifying A-records, working with local DNS caching, and configuring CNAME records to explore domain name resolution behaviors between a domain controller and a client machine.

## Environments Used

- Microsoft Azure (for hosting VMs)
- DC-1 – Windows Server 2022 (Domain Controller)
- Client-1 – Windows 10 Pro (Domain-joined client)
- Active Directory Domain Services (AD DS)
- DNS Manager
- PowerShell / Command Prompt

## A-Record Exercise 

1. Using my DC-1 VM, I will log in using the domain admin account(my domain.com\jane_admin)
2. In the Client-1 VM, I will log in as an admin(mydomian\jane_admin)
3. Attempt to ping "mainframe"(it can be anything) in the Client-1 virtual environment. It will most likely fail. Whenever you ping a hostname, it follows this process: Check the Local DNS Cache (Fastest), the Local Host File(Faster), and then the DNS server. We can even take this further and input ipconfig /displaydns to examine the local DNS cache further, but the record for "mainframe" is absent. 
4. From here, I will run the nslookup command for "mainframe," which will also fail. The nslookup command will query the DNS server for any domain names or IP addresses that match.
5. Next, I will create an A-record for the hostname "mainframe. To do this, I will need access to the DC-1 VM, open Windows Administrative tools, navigate to DNS, and this will be the area to create records. I will make the mainframe A-record and point it to DC-1's private IP address.
6. Back in the Client-1 virtual machine, I will ping mainframe and see if it works.
   

### Initial Ping Test for 'mainframe' from Client-1 (Expected Failure)
![image](https://github.com/user-attachments/assets/607f69bb-70ba-46a7-abfc-a05f715f36a3)

### Check Local DNS Cache on Client-1 (Record Not Found for 'mainframe') 

![image](https://github.com/user-attachments/assets/8c85764c-727f-47d7-be03-95f5fc0d7e1e)

### Check Local Host File for any records of mainframe
A unique aspect of the host file is that you can map a hostname to a particular IP address. 
![image](https://github.com/user-attachments/assets/4b3f7d34-327f-4bf5-8fa5-e872f9402f0d)

### Attempt DNS Lookup for 'mainframe' Using nslookup (Expected Failure)

![image](https://github.com/user-attachments/assets/e8f4a791-a7cc-43df-af79-878459101bd2)

### Create A-Record for 'mainframe' on DC-1 and Point to Private IP

![image](https://github.com/user-attachments/assets/b1de62ae-5874-4ccb-823c-2aeda70a260c)

### Verify A-Record Functionality by Pinging 'mainframe' from Client-1

 ![image](https://github.com/user-attachments/assets/aaa8086e-3a09-4a14-be32-24496d830167)

## Local DNS Cache Exercise 

7. Back in the DC-1 VM, change mainframe’s record address to 8.8.8.8
8. Back in the Client-1 VM, ping “mainframe” again. Observe that it still pings the old address
9. Observe the local dns cache (ipconfig /displaydns)
10. Flush the DNS cache (ipconfig /flushdns).
11. Observe that the cache is empty (ipconfig /displaydns)
12. Attempt to ping “mainframe” again. Observe the address of the new record is showing up

### Update 'mainframe' A-Record on DC-1 to Point to 8.8.8.8
![image](https://github.com/user-attachments/assets/6f9494aa-1fc5-4e73-aad4-635cb6ad5b37)

### Ping 'mainframe' from Client-1 (Old IP Still Cached)

![image](https://github.com/user-attachments/assets/2e9f14a3-b2d4-420f-b467-560c4ec4b5f7)

### View Local DNS Cache Using ipconfig /displaydns

![image](https://github.com/user-attachments/assets/39498d6a-0e9b-4b90-8b8d-f5b5ee5aa9c8)

### Flush the DNS cache (ipconfig /flushdns) in the Powershell interface as an admin

![image](https://github.com/user-attachments/assets/56505e7a-5bea-4c1a-a822-fa5310fc0709)

### Flush and Rebuild DNS Cache to Reflect Updated A-Record for 'mainframe

![image](https://github.com/user-attachments/assets/a17fae27-c850-4111-929e-8a25a5cda0ea)


## CNAME Record Exercise

13. Return to the DC-1 virtual machine and open DNS Manager from the Windows Administrative Tools. Create a new CNAME (Canonical Name) record that maps the alias "search" to "www.google.com".
14. Switch over to the Client-1 VM and attempt to ping "search" from the command line. Observe how the DNS resolution behaves and note the response, which should redirect to Google's servers.
15. On Client-1, run the nslookup command for "search" to further confirm that the CNAME record correctly resolves to www.google.com.


### Create CNAME Record 'search' Pointing to 'www.google.com' on DC-1

![image](https://github.com/user-attachments/assets/aa5bf680-1af7-4d19-b211-04f51e0b9ddb)

### Test CNAME Record Resolution by Pinging 'search' from Client-1

![image](https://github.com/user-attachments/assets/175966d2-c5d9-4c4d-b04f-ce64e7a754f3)

### Use nslookup on Client-1 to Confirm 'search' CNAME Resolves to www.google.com

![image](https://github.com/user-attachments/assets/da40d2a8-52d1-4204-8e86-43522dc3c3e9)














