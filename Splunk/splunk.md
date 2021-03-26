# Splunk Scenario

You have just been hired as an SOC Analyst by Vandalay Industries, an importing and exporting company.

•	Vandalay Industries uses Splunk for their security monitoring and have been experiencing a variety of security issues against their online systems over the past few months.
•	You are tasked with developing searches, custom reports and alerts to monitor Vandalay's security environment in order to protect them from future attacks.

## Vandalay Industries Monitoring Activity Instructions

Step 1: The Need for Speed

Background: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.

Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

Task: Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed. Upload the following file of the system speeds around the time of the attack (Speed Test File).

Command in New Search on Splunk: 
```source="server_speedtest.csv" | eval ratio = ( UPLOAD_MEGABITS / DOWNLOAD_MEGABITS ) | table _time, IP_ADDRESS, DOWNLOAD_MEGABITS, UPLOAD_MEGABITS, ratio```

![splunk](/images/splunk_speedtest.png)

Based on the report created, what is the approximate date and time of the attack?

The attack first occurred on 02-23-2020 on IP addresses 198.153.194.1 and 198.153.194.2 at 06:30:00 A.M. At 06:30:00 A.M., you can see the attack occurred on IP address 198.153.194.2 when the download speed dropped from its normal download range of 65-110 megabits  down to 12.76 megabits (a dramatic decrease), and its upload speed range dropped from its normal range of 5-12 megabits down to 2.19 megabits. At the same time this occurred, IP address 198.153.194.1 dropped its download speed range of 65-110 megabits down to 7.87 megabits, and its upload speed range that is normally 5-12 also dropped dramatically down to 1.83 megabits. The ratios dropped down to 0.233, 0.172 and 0.195 from 0.0520-0.1170+!

How long did it take your systems to recover?

It took about 2 hours for IP address 198.153.194.2 to return to its normal speeds as indicated at 10:30:00 A.M. when the download speed became 107.91 megabits and the upload speed was 13.51 megabits. At 12:30:00 P.M., IP address 198.153.194.1 returned to its normal range of upload speed 108.91 megabits and download speed 8.51 megabits. Their ratios also increased. 

## Step 2: Are We Vulnerable?

Background: Due to the frequency of attacks, your manager needs to be sure that sensitive customer data on their servers is not vulnerable. Since Vandalay uses Nessus vulnerability scanners, you have pulled the last 24 hours of scans to see if there are any critical vulnerabilities.

I created a report that shows the count of critical vulnerabilities from the customer database server on IP 10.11.36.23 by doing the following search on Splunk:

```source=”nessus_logs.csv” dest_ip=”10.11.36.23” severity=”critical” | top severity```

Keep in mind that the activity wanted me to check the last 24 hours of scans. By doing so, my search results showed nothing which is boring. So, I also did a search result for the past week, month, and quarter to see if anything showed up and got nothing. Then, I decided to do another search for the past year, and it turns out there is only data from 02/20/2020. Therefore, I attached a screenshot of those results.

![splunk](/images/splunk2.png)

^^ As you can see, the last 24 hours showed nothing.

![splunk](/images/splunk3.png)

^^ The previous year shows a count of 49 critical vulnerabilities.

![splunk](/images/splunk4.png)

^^ When I viewed the critical vulnerabilities (a total count of 49), they were all from 2020 (scroll down to the bottom of the page to view counts).

3.	Build an alert that monitors every day to see if this server has any critical vulnerabilities. If a vulnerability exists, have an alert emailed to soc@vandalay.com. 

![splunk](images/splunk5.png)

^^ This is to show you that I know how to create an alert. 