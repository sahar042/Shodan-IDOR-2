# Shodan-IDOR-2

I’ve found again! a new IDOR vulnerability (Insecure Direct Object References) in Shodan, the popular search engine for internet-connected devices. This flaw lets users generate detailed reports or access restricted query results without proper authentication or permissions. In short, it’s a textbook case of broken access control, putting sensitive data at risk of exposure to unauthorized users.

<br>
This isn’t my first time discovering an IDOR issue on Shodan. After a previous discovery, I’ve now identified another major vulnerability that points to ongoing problems with their access control mechanisms.

https://mixbanana.medium.com/shodan-idor-827ddac889b7

Affected Feature - Report Generation and Access<br>
Endpoint: https://www.shodan.io/search/report?query=<br>
Parameter: query<br>
Accessible to: Academic Users, Small Business API Subscription, and up.
<br><br>
How It Works<br>
The vulnerability lies in how Shodan handles its query parameter. By tweaking this parameter in the report generation URL, users can bypass access controls and retrieve detailed Shodan reports. Normally, this feature is exclusive to registered or paid accounts, but with this flaw, anyone can access it.
<br><br>
Proof of Concept (PoC)
<br>
1) Go to this URL:
https://www.shodan.io/search/report?query=vuln%3Acve-2021-34473<br>
2) Replace the query parameter with any search term of your choice. For example:
Change vuln%3Acve-2021-34473 to query=vuln:cve-2024-12345 to fetch reports about a specific CVE.
<br>
Example URLs:

```
To pull vulnerability data:
- https://www.shodan.io/search/report?query=vuln%3Acve-2024-12345
To pull honeypot reports:
- https://www.shodan.io/search/report?query=tag%3Ahoneypot
```

<br>Bypass PoC:
![image](https://github.com/user-attachments/assets/9dc3759a-2d97-4838-bbd9-f87451bc3e37)
Credits: Sahar Shlichove.<br>
