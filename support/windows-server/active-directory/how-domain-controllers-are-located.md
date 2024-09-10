---
title: Troubleshoot how domain controllers are located in Windows
description: Describes how domain controllers are located.
ms.date: 09/10/2024
manager: dcscontentpm
audience: itpro
ms.topic: troubleshooting
localization_priority: medium
ms.reviewer: kaushika
ms.custom: sap:Active Directory\On-premises Active Directory domain join, csstroubleshoot
---

# Troubleshoot how domain controllers are located in Windows

Authentication is the first step in virtually all functional scenarios in an Active Directory enterprise environment. Authentication, in turn, can't occur unless the client can first communicate with an Active Directory domain controller.

DC location refers to the algorithm the client machine uses to find a suitable domain controller (DC). DC location is a critical baseline functionality in all enterprise environments. However, if the Active Directory domain controller location algorithm (DC Locator) doesn't work as expected, you must troubleshoot it by following the instructions in this article.

## How to troubleshoot DC Locator

To troubleshoot the DC Locator domain controller locator process:

1. Check the System log on both the client and the server. Also check the Directory Service logs on the server and DNS logs on the DNS server.
1. Check the IP configuration by running the `ipconfig /all` command at a command prompt.
1. Use the Ping utility to verify network connectivity and name resolution. Ping both the IP address and the server name. You may also want to ping the domain name.
1. Use the Netdiag tool to determine whether networking components are working correctly. To send detailed output to a text file, run the following command:

    `netdiag /v >test.txt`  
    Review the log file, looking for problems, and investigate any implicated components. This file also contains other network configuration details.   
1. To fix minor problems, use the Netdiag tool with the following syntax:

    `netdiag /fix`.
1. Run the `nltest /dsgetdc:domainname` command to verify that you can locate domain controller for a specific domain.
1. Use the `NSLookup` tool to verify that DNS entries are correctly registered in DNS. Verify that the server host records and GUID SRV records can be resolved.

    For example, to verify record registration, run the following commands:

    <!-- Robin, I am unclear re: whether the following code should be presented as command prompt or Powershell (I tend to think it is not Powershell.)-->

     ```console
        `nslookup servername. childofrootdomain. rootdomain.com`  
        `nslookup guid._msdcs. rootdomain.com`  
    ```

1. If either of these commands doesn't succeed, use one of the following methods to reregister records with DNS:
   - To force host record registration, enter ipconfig /registerdns.
   - To force domain controller service registration, stop and start the Netlogon service.
   - To detect domain controller problems, run the DCdiag utility from a command prompt. The utility runs many tests to verify that a domain controller is running correctly. Use this command to send the results to the following text file: `dcdiag /v >dcdiag.txt`    

1. Use the Ldp.exe tool to connect and bind to the domain controller to verify appropriate LDAP connectivity.
1. If you suspect that a particular domain controller has problems, it may be helpful to turn on Netlogon debug logging. Use the NLTest utility by entering this command: `nltest /dbflag:0x2000ffff`. The information is then logged in the Debug folder in the Netlogon.log file.`nltest /dbflag:0x2000ffff`. The information is then logged in the Debug folder in the Netlogon.log file.
1. If you still haven't isolated the problem, use Network Monitor to monitor network traffic between the client and the domain controller.

## See also