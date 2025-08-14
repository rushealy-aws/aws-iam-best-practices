## AWS IAM Best Practices

## 🔗 Key AWS Documentation Links

### **Primary References:**

1. [IAM Security Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html)
   • Main IAM security guidance document

2. [Secure Access Keys](https://docs.aws.amazon.com/IAM/latest/UserGuide/securing_access-keys.html)
   • Specific guidance on protecting programmatic access credentials

3. [Programmatic Access with AWS Security Credentials](https://docs.aws.amazon.com/IAM/latest/UserGuide/security-creds-programmatic-
access.html)
   • Detailed guidance on programmatic vs console access

4. [AWS Well-Architected Framework - Identity and Access Management](https://docs.aws.amazon.com/wellarchitected/2023-10-03/framework/sec-
iam.html)
   • High-level security principles for identity management

## 🛡️ Security Principles for Separating Console and API Access

### **Why Separate IAM Users for Console vs API Access:**

#### **1. Credential Exposure Risk Reduction**
• **Console passwords** are typically used interactively and stored in password managers

• **Access keys** are used programmatically and may be stored in code, config files, or environment variables

• Separating them limits the blast radius if one credential type is compromised

#### **2. Different Security Requirements**
• **Console access** can enforce MFA more easily for interactive sessions

• **Programmatic access** may need to work in automated environments where MFA is challenging

• Different rotation schedules and policies can be applied

#### **3. Principle of Least Privilege**
• **Console users** may need broader permissions for interactive troubleshooting

• **API users** should have very specific, narrow permissions for their automated tasks

• Separation allows for more granular permission management

#### **4. Audit and Monitoring**
• **Console activities** and API calls have different monitoring requirements

• Easier to track and alert on unusual patterns when access types are separated

• CloudTrail logs can be analyzed more effectively

#### **5. Credential Lifecycle Management**
• **Console passwords** follow human user lifecycle (hiring/termination)
• **Access keys** follow application/service lifecycle
• Different rotation and management policies can be applied

## 📋 AWS Recommended Approach

According to the documentation, AWS actually recommends avoiding long-term IAM users entirely when possible:

### **Preferred Hierarchy:**
1. Best: Use AWS IAM Identity Center with temporary credentials
2. Good: Use IAM Roles with temporary credentials  
3. Acceptable: Use separate IAM users for console vs programmatic access
4. Not Recommended: Single IAM user with both console and programmatic access

### **Key Quote from AWS Documentation:**
│ *"Credentials must not be shared between any user or system. User access should be granted using a least-privilege approach with best 
practices including password requirements and MFA enforced. Programmatic access, including API calls to AWS services, should be performed 
using temporary and limited-privilege credentials."*

## 🔧 Implementation Guidance

If you must use IAM users, the separation principle suggests:

• **Human-Console-User**: Password + MFA, broader interactive permissions

• **Service-API-User**: Access keys only, narrow programmatic permissions, no console access

This approach aligns with the AWS security principle of defense in depth and least privilege access.

