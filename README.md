# 🌐 DNS Lab Project

## 🎯 Objective
In this lab, I configured and tested DNS records within an Active Directory environment using Azure-hosted virtual machines. The exercises included creating and modifying A-records, working with local DNS caching, and configuring CNAME records to explore domain name resolution behaviors between a domain controller and a client machine.

---

## 🧰 Environments Used

- **Microsoft Azure** (for hosting VMs)
- **DC-1** – Windows Server 2022 (Domain Controller)
- **Client-1** – Windows 10 Pro (Domain-joined client)
- **Active Directory Domain Services (AD DS)**
- **DNS Manager**
- **PowerShell / Command Prompt**

---

## 📁 A-Record Exercise

1. Log in to **DC-1** as `mydomain.com\jane_admin`
2. Log in to **Client-1** as `mydomain\jane_admin`
3. Attempt to ping `mainframe` from Client-1. This will likely fail.
4. Use `ipconfig /displaydns` to check local DNS cache — record should be absent.
5. Use `nslookup mainframe` — it will also fail as no DNS record exists yet.
6. On DC-1, create an A-record for `mainframe` pointing to DC-1’s private IP.
7. On Client-1, ping `mainframe` again — this time it should succeed.

### 🔎 Initial Ping Test for 'mainframe' from Client-1 (Expected Failure)
<img src="https://github.com/user-attachments/assets/607f69bb-70ba-46a7-abfc-a05f715f36a3" width="600"/>

### 🔍 Check Local DNS Cache on Client-1 (Record Not Found for 'mainframe')
<img src="https://github.com/user-attachments/assets/8c85764c-727f-47d7-be03-95f5fc0d7e1e" width="600"/>

### 🧾 Check Local Host File for any Records of 'mainframe'
<img src="https://github.com/user-attachments/assets/4b3f7d34-327f-4bf5-8fa5-e872f9402f0d" width="600"/>

### ❌ Attempt DNS Lookup for 'mainframe' Using nslookup (Expected Failure)
<img src="https://github.com/user-attachments/assets/e8f4a791-a7cc-43df-af79-878459101bd2" width="600"/>

### ✅ Create A-Record for 'mainframe' on DC-1 and Point to Private IP
<img src="https://github.com/user-attachments/assets/b1de62ae-5874-4ccb-823c-2aeda70a260c" width="600"/>

### ✅ Verify A-Record Functionality by Pinging 'mainframe' from Client-1
<img src="https://github.com/user-attachments/assets/aaa8086e-3a09-4a14-be32-24496d830167" width="600"/>

---

## 🧹 Local DNS Cache Exercise

8. On DC-1, change the `mainframe` A-record to point to `8.8.8.8`
9. On Client-1, ping `mainframe` again — observe it still pings the old address (due to DNS cache)
10. Use `ipconfig /displaydns` to view the cached record
11. Run `ipconfig /flushdns` to clear the DNS cache
12. Re-run `ipconfig /displaydns` to confirm cache is cleared
13. Ping `mainframe` again — it should now resolve to the updated IP

### 🛠️ Update 'mainframe' A-Record on DC-1 to Point to 8.8.8.8
<img src="https://github.com/user-attachments/assets/6f9494aa-1fc5-4e73-aad4-635cb6ad5b37" width="600"/>

### 📶 Ping 'mainframe' from Client-1 (Old IP Still Cached)
<img src="https://github.com/user-attachments/assets/2e9f14a3-b2d4-420f-b467-560c4ec4b5f7" width="600"/>

### 🔍 View Local DNS Cache Using ipconfig /displaydns
<img src="https://github.com/user-attachments/assets/39498d6a-0e9b-4b90-8b8d-f5b5ee5aa9c8" width="600"/>

### 🧼 Flush the DNS Cache in PowerShell
<img src="https://github.com/user-attachments/assets/56505e7a-5bea-4c1a-a822-fa5310fc0709" width="600"/>

### 🔁 Rebuild DNS Cache to Reflect Updated A-Record for 'mainframe'
<img src="https://github.com/user-attachments/assets/a17fae27-c850-4111-929e-8a25a5cda0ea" width="600"/>

---

## 🔗 CNAME Record Exercise

14. On DC-1, open DNS Manager and create a CNAME record that maps `search` to `www.google.com`
15. On Client-1, ping `search` — DNS should resolve to Google's server
16. On Client-1, run `nslookup search` to validate the CNAME record resolution

### 🏷️ Create CNAME Record 'search' Pointing to 'www.google.com' on DC-1
<img src="https://github.com/user-attachments/assets/aa5bf680-1af7-4d19-b211-04f51e0b9ddb" width="600"/>

### 🧪 Test CNAME Record Resolution by Pinging 'search' from Client-1
<img src="https://github.com/user-attachments/assets/175966d2-c5d9-4c4d-b04f-ce64e7a754f3" width="600"/>

### 🔍 Use nslookup on Client-1 to Confirm 'search' Resolves to www.google.com
<img src="https://github.com/user-attachments/assets/da40d2a8-52d1-4204-8e86-43522dc3c3e9" width="600"/>

---

## ✅ Summary

This lab demonstrated the practical use of DNS within a domain environment:
- Creating and modifying A-records and CNAME records
- Observing DNS cache behavior
- Validating configurations using ping, nslookup, and cache management commands














