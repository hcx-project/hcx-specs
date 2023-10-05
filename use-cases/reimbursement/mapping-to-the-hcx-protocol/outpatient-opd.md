---
description: Mapped workflow, key gaps identified and proposed protocol changes
---

# Outpatient (OPD)

The reimagined OPD reimbursement claims workflow leveraging HCX protocol help us understand how claim requests can processed timely and efficiently. Increased provider network coverage, real time updates and approval of the OPD claims will enhance adoption and trust in the system for policyholder.

[Link to the typical OPD reimbursement claims workflow.](../typical-workflows/outpatient-opd.md)

{% hint style="info" %}
**Important note :** The work stream's original diagram representing the overall workflow of the reimagined OPD reimbursement flow using HCX is available [here](https://drive.google.com/file/d/13VEPfN\_dLNlz\_HhwVD3-e5SQr0seoxSw/view?usp=sharing). Based on initial feedback for improving the readability, the sections below detail it in multiple diagrams representing each stage separately. &#x20;
{% endhint %}

### **OPD reimbursement claims**&#x20;

#### **Coverage eligibility flow**

Even in a reimbursement situation, an OPD service delivery and claims process could start with the beneficiary/policyholder checking their coverage eligibility using the BSP interface. This would serve as a pre-notification for the payer, and aid the beneficiary in obtaining the initial details regarding the coverage. The following diagram shows the steps and stakeholders involved in the coverage eligibility flow.

<figure><img src="../../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

#### **Pre-auth flow**

After the coverage eligibility process, once the provider has decided on the services or treatment plan and the costs, the beneficiary could potentially send a preauthorisation to the payer. This could provide payers with an opportunity to assist the beneficiary with their treatment and expenses planning. The following diagram provides an overview of the steps and stakeholders involved in the pre-auth flow.&#x20;

<figure><img src="../../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

#### **Claims flow**

Once the services are provisioned and the beneficiary is discharged, the Beneficiary/policyholder would initiate a reimbursement claim request with the payer through HCX, furnishing the necessary information for the claim adjudication. The beneficiary would use a BSP app to start the claim. Before processing a claim, the Payer would seek consent from the beneficiary to ensure claim authenticity. The following diagram describes the steps and stakeholders involved in the claims flow through HCX.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

The next section details the important implementation considerations for reimbursement health claims. &#x20;
