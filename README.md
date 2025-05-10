# Splunk - Alert Creation


## Forewords and Feedback
This write-up will reflect my thought process during the investigation and reasoning for actions taken during my **Home Lab - Walkthrough - Splunk - Alert Creation**

Feel free to drop any feedback or point out anything I might’ve missed! I’m all about learning from others (and my own slip-ups). I really appreciate you taking the time to check out my project!

## Objective
We have been set the task to create a medium severity alert that should alert if a new user account(s) were created. This alert should run every hour and be sent to the Triggered Alerts page once it meets the criteria.

## Pre-requests
-   VM - _(WMware Workstation)_
-   Ubuntu Server - _(24.04.1 LTS)_
-   Splunk Enterprise _(9.3.1)_
-   Index file to use in Splunk _(5931 Events)_
-   Internet Browser

## Making sure we are using the correct index file for the lab
We are using the command **”index="mydfir-lab1”** to check we have **5931 events** as this will confirm we are working with the correct index file.

![Correct Index File](https://github.com/user-attachments/assets/0545351c-32bf-4412-8259-fc0d6d96b686)

## Building our Query and Alert
We reuse our query from our previous <a href="https://github.com/mejdahlbo/Splunk-Windows-Event-Dashboard">Splunk - Windows Event Dashboard</a> - **index=mydfir-lab1 host=winvm EventCode=4720 user!=*$ user!=SYSTEM |stats count by _time, ComputerName, Subject_Account_Name, New_Account_Account_Name**

![1 - Reuse query](https://github.com/user-attachments/assets/c664f69b-5ac7-46fe-add4-c3f45fb2639d)

We create an alert for this:

![2 - Create Alert](https://github.com/user-attachments/assets/c5db13b4-f5a3-4500-b125-9ec688a87ffa)

With reference to the **MITRE ATT&CK** framework we use the ID **T1136** for naming our alert as this ID is for when an account is created. We give the alert’s title **Endpoint - T1136 - New User Account Created**. We set the **Permissions** to shared so others can view and use the alert. We set the trigger to **greater than 0** so when there is a new account created we will receive an alert.

![3 - T1136](https://github.com/user-attachments/assets/5737361e-3491-425b-82b8-be4a79a8f508)

![4 - Alert Title](https://github.com/user-attachments/assets/e0d7aa6f-84f8-4521-9a14-e2a5f3036fee)

![5 - Trigger](https://github.com/user-attachments/assets/c2bac419-5dcd-4665-9778-78796a7517bc)

Finally we can review our alert, and here we confirm the title we gave the alert, the alert is **Enabled**, and that it is running **Hourly**.

![6  - Alert Created](https://github.com/user-attachments/assets/7a6e0a3c-3ca7-48a3-832e-68d866891b5b)

## Changelog
