
Type url→check cache(local and browser)→public DNS server(google 8.8.8.8) check cache —→root servers .com .net—>TLD(Top level domain servers)—>authoritative DNS servers

Types of DNS records
**A Record:**
 - This is the record that directly points to the ip-address 
 - for example tarun.com -->72.72.72.1
**CNAME Record** (Canonical Name Record):
- This is a record which will point to another A-Record provided by some external provider 
- Example blog.tarun.com --->tarun.hashnode.com
**NS record**
- This is a Name Server Record which is used to store name server url or ip adress
- An **NS record** (Name Server record) is a type of DNS (Domain Name System) record that specifies which **DNS servers** are authoritative for a particular domain. These servers are responsible for handling queries related to that domain and resolving them into IP addresses or other DNS records.
- For example i bought the domain from godaddy it will be ns1.godaddy.com
- if i have myserver for DNS 
```
example.com.  IN  NS  ns1.myserver.com.
example.com.  IN  NS  ns2.myserver.com.

```

If i were to make my own dns server 
- It will be program that will be an ec2 in aws whose ip will be an ns record 
- that program should accept connections via UDP on port 53 and follow the DNS protocol specification


DNS Works in UDP protocol on portnumber 53