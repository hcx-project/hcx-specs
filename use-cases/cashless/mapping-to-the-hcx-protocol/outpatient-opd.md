---
description: Mapped workflow, key gaps identified and proposed protocol changes
---

# Outpatient (OPD)

The reimagined OPD cashless claims workflow leveraging HCX protocol help us understand how claim requests can processed timely and efficiently. Increased provider network coverage, real time updates and approval of the OPD claims will enhance adoption and trust in the system for policyholder.

Ref: [Typical OPD cashless claims workflow](../typical-workflows/outpatient-opd.md)

{% hint style="info" %}
**Important note :** The work stream's original diagram representing the overall workflow of the OPD cashless claims workflow using HCX is available [here](https://drive.google.com/file/d/1cKb4gfqZjHib4vKOEjYIvcySl4KiO8hR/view?usp=sharing). Based on initial feedback for improving the readability, the sections below detail it in multiple diagrams representing each stage separately.
{% endhint %}

### **OPD cashless claims**

#### **Coverage eligibility flow**

The OPD service delivery and claims process would usually start with the coverage eligibility (optional) check for the beneficiary. The following diagram shows the steps and stakeholders involved in the coverage eligibility flow.

<figure><img src="../../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

#### **Pre-auth flow**

After the coverage eligibility process, the provider would determine the required services or treatment plan for the beneficiary's requirements, along with the associated expenses, and submits it to the payer for pre-authorization. The following diagram provides an overview of the steps and stakeholders involved in the pre-auth flow.&#x20;

<figure><img src="../../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

#### **Claims flow**

Once the Provider has provided the services to the beneficiary in accordance with the treatment plan, it initiates the claim request with the concerned payer through HCX, furnishing the necessary information for the claim adjudication. The following diagram describes the steps and stakeholders involved in the claims flow through HCX.&#x20;

<figure><img src="../../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

The next section details the important implementation considerations for cashless health claims.&#x20;
