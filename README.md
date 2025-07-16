# Defend-against-cyberthreats-with-Microsoft-Defender-XDR

![Image](https://github.com/user-attachments/assets/9f6b0a60-06f2-412c-9014-d244480ef49f)

This repository documents a hands-on applied skills exercise based on Microsoft Learn titled "Defend Against Cyberthreats with Microsoft Defender XDR." It includes real-world scenarios demonstrating endpoint onboarding, policy configuration, incident management, and forensic analysis using Microsoft Defender XDR.

# Scenario:
You were recently hired by Contoso, Ltd to help the company's IT team to Defend against threats with Microsoft Defender (XDR). The company's executives are very concerned that all guidelines are followed and that all requirements are met when you complete the activities in their environment.

The guidelines and requirements are detailed in a series of emails. Read the email messages and complete the activities according to the provided requirements. You can complete the activities from the Microsoft Defender portal or from any other Microsoft tool available in the virtual machine.

There are 2 virtual machines involved in this lab namely Client1 and Client2.

### TASK1 - ONBOARD AN ENDPOINT TO MICROSOFT DEFENDER XDR

In this task, I've created a device group named Group1 for windows 10 and 11 and set it to remediate fully and onboarded client 2 to XDR. Ran "AttackScript.ps1" powershell command in order to simulate an attack which will create an incident for us to investigate in the microsoft security portal.

### TASK2 - CREATE AN ENDPOINT SECURITY POLICY

Created an endpoint security policy names EndpointPolicy1 and assigned the policy to the sg-Executive security group. This policy will block Windows 11 devices from using JavaScript to download and run executable content. I achieved this by using the AttackSurfaceReduction Template with the use case: Block Javascript or VBScript from launching downloaded executable content.

### TASK3 - MANAGE A MICROSOFT DEFENDER XDR INCIDENT

The powershell script that we ran earlier created a Microsoft incident named MULTI-STAGE INCIDENT INVOLVING DEFENCE EVASION & DISCOVERY ON ONE ENDPOINT. 

- I reviewed the device timeline of client2. In the timeline, found the entry of the suspicious process injection that indicates the outbound connection to the malicious IP address and the target executable name that performs process hollowing.

- This task involved creating a custom indicator named Indicator1 that will block execution when when a user attempts to download a file from the malicious IP address. Assigned indicator1 to the device group - group1 and configured to generate a high severity alert for the execution category.

- Finally created a custom detection named "Suspicious Powershell" that runs every hour and is scoped to all devices from the advanced hunting blade after constructingh a KQL Query leveraging DeviceProcessEvents table in order to find the powershell.exe events that initiated the target executable found during the timeline review of client2. Collected the investigation package and marked the user as compromised.

### TASK4 - DEVICE INVESTIGATION AND FORENSICS ANALYSIS

On Client1, performed the following tasks:

- Enabled and then initiated a live response session to client2 machine and investigated the current connections using "connnections" command.
- Collected an investigation package from client2 and extracted the Forensics Collection Summary.csv file and isolated the Client2 device.

## Credential:
https://learn.microsoft.com/api/credentials/share/en-us/ABISHEKS-9295/62385954A3D2B68?sharingId=478DF7F6457271A9







