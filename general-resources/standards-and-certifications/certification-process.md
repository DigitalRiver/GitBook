---
description: Understand the quality and security certification process.
---

# Certification process

Here you'll find both an overview and a [detailed description](certification-process.md#detailed-certification-process) of the commerce connector quality and security certification review process.

During the review, you'll need to provide an ecommerce front end, created in your ecosystem, that demonstrates how the connector functions. More specifically, the front-end must:

* Include a test commerce site
* Contain an admin interface for conducting configurations and customer service
* Allow orders to be placed, using all available payment methods, in the [Production Test Environment (PTE)](../glossary.md#production-test-environment-pte)
* Execute a minimal scenario set, provided by Digital River, that demonstrates evidence of your connector's health
* Provide access to a source code wrapping SDK that enables the ecommerce workflow

You'll also need to supply us with credentials for both the admin portal and a test account in the customer portal.

## Phases of the certification process

To help you work through these commerce connector quality and certification requirements, we've organized them into five phases:

* [Phase 1](certification-process.md#planning-and-prerequisites): Planning and prerequisites
* [Phase 2](certification-process.md#tool-development): Tool development and test site validation by ecosystem partner
* [Phase 3](certification-process.md#tool-submission-and-certification): Security validation by Digital River
* [Phase 4](certification-process.md#tool-submission-and-certification): Front end test site validation by Digital River
* [Phase 5](certification-process.md#tool-submission-and-certification): Production payment validation by Digital River

### Planning and prerequisites

Phase 1 consists of project planning. By the time you start this phase, we assume you're currently working with Digital River and ready to build a connector. The main goals of phase 1 are to create function specs, documents, schedules, test scenarios, team assignments, and the defect triage matrix.

### Tool development

During phase 2, you're responsible for creating a working test environment and updating Digital River on your development status. During this phase, the bulk of the development work is performed in the Digital River [PTE](../glossary.md#production-test-environment-pte). This is in preparation for the initial certification tests you must pass, which consist of:

* Deploying a working storefront that acts as a front end test environment
* Finalizing test cases and workflows
* Accounting for all applicable Digital River use-cases

Your ultimate goal in phase 2 is to present your complete integrated tool on the PTE test site and demonstrate that you've accounted for all priority 1 defects.

{% hint style="info" %}
For more information on how defects are prioritized, refer to the _Priority Matrix_ section in the [full certification process document](certification-process.md#detailed-certification-process).
{% endhint %}

### Tool submission and certification

In phases 3 through 5, Digital River performs manual and automated validations of your tool in the [PTE](../glossary.md#production-test-environment-pte) test site. We also help you resolve any defects and compliance issues before you proceed any further in the certification process.

The following provides a high-level overview of these three phases:

* **Phase 3**: We perform security and automated validation scans on your tool and its source code
* **Phase 4**: Our QA teams run test scenarios against your PTE test site
* **Phase 5**: Using live payment systems, our QA teams verify the integrity of all payment methods

At the end of phase 5, your tool is certified and ready to be deployed on your clients' [end site implementations](certification-process.md#end-site-implementations).

### Detailed certification process

You can find a more detailed explanation of the certification process, along with a diagram outlining the sequences, in the following documents:

{% file src="../../.gitbook/assets/Certification_Process (1).docx" %}

{% file src="../../.gitbook/assets/Certification_Sequence_Diagram (1).pdf" %}

## End site implementations

After your tool is certified, you can use it to implement multiple end sites. The end sites you implement, however, are not part of the tool certification process. These sites must undergo a separate [production checkout certification](compliance-requirements.md#production-checkout-certification).

Since each end site that uses your tool is treated as a separate entity, it must be deployed independently. This means that individual end sites are required to obtain a unique Digital River API account. These accounts provide the client with a set of API keys for use in test and production environments.

## Change management

The Digital River API is versioned based on [breaking changes](../versioning.md#breaking-changes) that require you to modify your workflow. The way we implement versioning allows you to remain on your current version until you're ready to [update to the latest one](../../administration/dashboard/developers/api-keys/updating-your-api-version.md). When you decide to update your version, we provide [several options for handling the conversion](../../developer-resources/best-practices.md#versioning-and-api-keys).

We also release [non-breaking changes](../versioning.md#non-breaking-changes) that, whatever the version you're on, require no modification of your code.
