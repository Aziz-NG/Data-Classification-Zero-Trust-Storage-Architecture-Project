🛡️ Enterprise Data Classification & Zero Trust Storage Architecture

Azure Infrastructure Security | Microsoft Purview | Compliance Logging

📌 Executive Summary

This project demonstrates the design and validation of a cloud-native Zero Trust data protection architecture using Microsoft Purview and Microsoft Azure.

Instead of relying on traditional perimeter defenses, the architecture enforces a defense-in-depth model built on:

Data classification and governance
Complete network isolation using Private Endpoints
End-to-end audit logging and monitoring

By disabling all public access and routing traffic through Azure’s private backbone, data assets are fully hidden from the public internet.

The solution concludes with a verified audit trail in Azure Monitor, supporting compliance requirements such as ISO 27001 and SOC 2.

🎯 Project Objectives
Data Governance
Classify data assets by sensitivity (Public, Confidential, PII) using Microsoft Purview
Network Isolation
Remove public exposure of Azure Storage via Private Endpoints
Audit & Visibility
Enable diagnostic logging for all data-plane operations
Compliance Alignment
Map controls to:
NIST 800-53
ISO 27001
SOC 2
Quebec Bill 25
🏗️ Architecture Overview
Layer	Technology Used
Governance	Microsoft Purview
Storage	Azure Blob Storage
Network Security	Virtual Network (VNet) + Private Endpoint
Monitoring	Azure Monitor + Log Analytics
🔐 Data Classification Strategy

A classification schema was defined in Microsoft Purview:

Label	Description	Technical Controls
Public	Low-risk data	Minimal restrictions
Confidential	Internal business data	Encryption + policy enforcement
PII	Highly sensitive personal data	Strict encryption + regulatory scope

⚠️ Note: Client-side enforcement (M365 apps) was out of scope. Policies were validated within the Purview control plane.

☁️ Secure Storage & Network Isolation
🚫 Public Access Disabled
Public access to the storage account was completely turned off

Test Performed

Attempted blob access via public URL

Result

❌ Access denied
✅ Resource inaccessible from the internet
🌐 Private Endpoint Implementation

A Private Endpoint was configured to assign a private IP to the storage account inside a VNet.

Validation

Connected via VM within the VNet using Azure Storage Explorer
Successfully performed:
Upload
Download

Result

✅ Secure internal access confirmed
❌ No external exposure
🔍 Monitoring & Auditability
Diagnostic Logging Configuration

Enabled the following logs:

StorageRead
StorageWrite
StorageDelete

Destination

Log Analytics Workspace
🧪 Activity Testing
Scenario	Source	Expected Result
Upload / Download	Internal VM	Success
Unauthorized access attempt	External	Blocked
📊 Log Verification (KQL)

Using Azure Monitor:

✅ Successful operations logged with internal IP
❌ Unauthorized attempts captured and traceable

This ensures full auditability for incident response and compliance.

📊 Compliance Mapping
Framework	Controls Implemented
NIST 800-53	SC-7 (Boundary Protection), AU-2 (Logging)
ISO 27001	A.12.4 (Logging), A.13 (Network Security)
SOC 2	Confidentiality & access restriction
Quebec Bill 25	PII protection & auditability
🧨 Threat Modeling
Threat	Control Applied	Outcome
Public Exposure	Public access disabled	Blocked
Data Exfiltration	Private Endpoint	Blocked
Unauthorized Access	Encryption + labeling	Restricted
🧾 Key Takeaways
Zero Trust ≠ just identity — network isolation plays a critical role
Eliminating public endpoints dramatically reduces attack surface
Data classification strengthens governance and compliance posture
Azure Monitor provides continuous visibility and audit readiness

Even without RBAC, this architecture significantly limits exposure and aligns with modern privacy regulations like Quebec Bill 25.
