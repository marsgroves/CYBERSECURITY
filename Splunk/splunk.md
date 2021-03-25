# Scenario

You have just been hired as an SOC Analyst by Vandalay Industries, an importing and exporting company.

•	Vandalay Industries uses Splunk for their security monitoring and have been experiencing a variety of security issues against their online systems over the past few months.
•	You are tasked with developing searches, custom reports and alerts to monitor Vandalay's security environment in order to protect them from future attacks.

## Vandalay Industries Monitoring Activity Instructions

Step 1: The Need for Speed

Background: As the worldwide leader of importing and exporting, Vandalay Industries has been the target of many adversaries attempting to disrupt their online business. Recently, Vandaly has been experiencing DDOS attacks against their web servers.

Not only were web servers taken offline by a DDOS attack, but upload and download speed were also significantly impacted after the outage. Your networking team provided results of a network speed run around the time of the latest DDOS attack.

Task: Create a report to determine the impact that the DDOS attack had on download and upload speed. Additionally, create an additional field to calculate the ratio of the upload speed to the download speed. Upload the following file of the system speeds around the time of the attack (Speed Test File).

Command in New Search on Splunk: 
source="server_speedtest.csv" | eval ratio = ( UPLOAD_MEGABITS / DOWNLOAD_MEGABITS ) | table _time, IP_ADDRESS, DOWNLOAD_MEGABITS, UPLOAD_MEGABITS, ratio

Based on the report created, what is the approximate date and time of the attack?

The attack first occurred on 02-23-2020 on IP addresses 198.153.194.1 and 198.153.194.2 at 06:30:00 A.M. At 06:30:00 A.M., you can see the attack occurred on IP address 198.153.194.2 when the download speed dropped from its normal download range of 65-110 megabits  down to 12.76 megabits (a dramatic decrease), and its upload speed range dropped from its normal range of 5-12 megabits down to 2.19 megabits. At the same time this occurred, IP address 198.153.194.1 dropped its download speed range of 65-110 megabits down to 7.87 megabits, and its upload speed range that is normally 5-12 also dropped dramatically down to 1.83 megabits. The ratios dropped down to 0.233, 0.172 and 0.195 from 0.0520-0.1170+!