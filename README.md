# Case Study:  Optimizing Vendor Connections through Source IP Anchoring

## Overview:
</br>

<img align="left" alt="Portfolio Logo" width="200px" src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQyMk6xX2_L1CvEBpw6xu1ipeeYuMHeE8R6jg&s" />
</br>

- **Position**:  Information Security Analyst, Subject Matter Expert (SME)  
- **Timeframe**:  One month  
- **Objective**:  Optimize vendor connections while maintaining a strong security posture by utilizing source IP anchoring. 
</br>
</br>
</br>


## Background
- **Context**:  A user submitted a service ticket requesting that we whitelist a new vendor's domains in Zscaler ZIA.  It was assumed that Zscaler was blocking the connection.  
- **Stakeholders**:  InfoSec Team, New Vendor's Technical Team, Requesting Department, Compliance Team, Zscaler

## Problem Statement
- The organization needed to connect securely to a vendor's application but encountered a problem when a service ticket requested whitelisting of the vendor’s domains in Zscaler ZIA.  Despite no blocks in Zscaler logs, the vendor provided broad domain requests, prompting the need for a solution that adhered to security protocols

## Approach
- **Research and Analysis**:  Conducted a detailed analysis of the user's machine, the application, and Splunk logs, while reviewing Zscaler documentation to assess our security posture regarding the connection request.
- **Methodology**:  Worked closely with the requesting user and the vendor to clarify connection requirements and gather specific domain information.  Developed a systematic approach for testing the connection.  
- **Tools and Technologies**:  Utilized Zscaler Internet Access (ZIA) for traffic filtering and Zscaler Private Access (ZPA) for secure application access, analyzed connection issues through Splunk logs, and consulted Zscaler documentation for configuration guidance while collaborating with the vendor via video conferencing and email.

## Implementation
**Steps Taken**:
1. Initial Investigation:  Checked Splunk logs for the vendor's domain and found no blocks by Zscaler; all connections were allowed. The second domain had a wildcard: *.s3.amazonaws.com, which posed significant security risks.
2. User Meeting:  Requested a meeting with the vendor to clarify specific domains.
3. Testing Session:  Scheduled a day for testing with the vendor and involved coworkers.  During the testing, the connection failed with Zscaler enabled, but was successful when Zscaler was temporarily disabled.
4. Log Analysis:  Pulled up Splunk logs and identified that Zscaler blocked the connection due to a dropped SSL handshake, indicating a need for an SSL bypass.
5. Domain Whitelisting: E ntered the first domain provided by the vendor and re-enabled Zscaler.  The connection test was successful.
6. Ongoing Connection Issues:  After some time, a connection error occurred, this time linked to one of the AWS domains.
7. Introducing Source IP Anchoring:  Educated the vendor about Zscaler's ZPA and source IP anchoring.  I submitted our public IP ranges to the vendor's firewall team, who agreed to whitelist them.
8. Final Implementation:  Added all vendor domains to Zscaler ZIA and removed the previous SSL bypass entries, ensuring that we presented our organization's public IP instead of a Zscaler IP.  This change allowed successful connections while maintaining security.
9. Testing Confirmation:  Conducted final tests on the application, which were successful.  The entire process, including necessary approvals and change controls, took about a month.

**Challenges Faced**:  The broad wildcard domain (*.s3.amazonaws.com) requested by the vendor posed a significant security risk, as it would allow unrestricted access to a wide range of AWS services.  Additionally, balancing the need for the vendor's application to function while maintaining our organization's security posture required careful analysis.  The SSL handshake failures due to Zscaler's traffic inspection added complexity, and coordinating with the vendor to provide more specific domains took time.  Ensuring a seamless transition to Source IP Anchoring while meeting security and compliance standards, such as NIST 800-53, further challenged the implementation.

## Results
- **Outcomes**:  Successfully implemented Source IP Anchoring for the vendor's application, ensuring secure and seamless connections while maintaining Zscaler traffic inspection.
- **Impact**:  Enhanced the organization's security posture by eliminating the need for an SSL bypass, adhering to NIST 800-53 Rev 5 guidelines, and ensuring secure

## Lessons Learned
- **Departmental Education**:  Ensuring department heads and end-users are more aware of security protocols and potential solutions can help mitigate issues earlier in the process, streamlining troubleshooting and reducing time spent on reactive measures.
- **Proper Use of Zscaler Controls**:  Instead of temporarily disabling Zscaler, signing out of the tool during troubleshooting would reinforce proper usage and prevent end users from inadvertently learning how to bypass security controls.  This approach ensures continued adherence to security protocols without introducing unnecessary risks.

## Conclusion
- By prioritizing source IP anchoring over SSL bypassing, I better aligned our security practices with NIST SP 800-53 Rev 5 controls that advocate for robust access control, monitoring, and data protection.  This approach not only strengthens our security posture but also demonstrates compliance with federal standards for information security.

### References
-
- [Set up Microsoft Defender for Endpoint deployment](https://learn.microsoft.com/en-us/defender-endpoint/production-deployment)
- [Microsoft Defender Antivirus compatibility with other security products](https://learn.microsoft.com/en-us/defender-endpoint/microsoft-defender-antivirus-compatibility)
- [Reference: Endpoint security exclusions](https://help.tanium.com/bundle/ug_client_cloud/page/client/security_exclusions.html)
- [Exclusions overview](https://learn.microsoft.com/en-us/defender-endpoint/navigate-defender-endpoint-antivirus-exclusions)
- [Get started with endpoint data loss prevention](https://learn.microsoft.com/en-us/purview/endpoint-dlp-getting-started)
