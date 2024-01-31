# Using Integration01 Tenancy
This repo contains mostly documentation and examples for using the `orasenatdpltintegration01` tenancy.  It is not standard product documentation, but rather aims to show where variations were made in order to share resources.  Each section below will cover basic usage of a particular area within the tenancy.

## General Guidelines
The following general guidelines should be adhered to.  Please read over these prior to creating resources:

1) BYOL Only - For any service offering a BYOL or license-included SKU, *NEVER* choose License-Included.  The functionality is the same, so chooe BYOL for the lower price.
2) Cost - Our cost center pays for everything we spin up.  Do not spin up environments the stay running indefinitely.  The smallest possible OCPU count, storage, etc.  Also if it is a new or limited resource, please ask in the channel, as we may need to add limits, permissions, bidgets, etc.
4) Tagging / Naming - Please make sure names make sense.  Calling things "test" or "demo" with no additional context makes things hard to find.
5) Compartments - Each engineer has their own (or can create) under `root / cloud-engineering`.  Put your resources there.
6) Shared Resources - See below, we've worked to bring limited or expensive resources into a shared model.  You will have limited but enough permission to do things.  The next section outlines these.
7) Nightly Shutdown - Most services will allow the tenancy admins to perform nightly shutdown using the Schedule tags that get applied.  Please respect these tags and do not change anything to 24/7 unless there is a reason.  If you come in and find your DB or VMs shut down after creating, simply start them back up.

## Shared Services
Each shared service our tenancy offers to engineers has its own document.  

* Shared Vault - [Vault](/SHARED-VAULT-README.md)
* ExaCS / ADB-D - [ExaCS](/EXACS-README.md)
* Database Services - [Database Tools](/DB-TOOLS-README.md)
* Dynamic Groups - [Dynamic Groups](/DYNAMIC-GROUPS.md)
* Visual Builder Studio - [Visual Builder](/VISUAL-BUILDER-README.md)
* Data Lake / Data Catalog - TBD - we are building out some things in a shared compartment, please ask before trying anything in your own compartment.

## Additional Topics

* Sending Email from APEX on ADB-D - [APEX Mail](/ADB-APEX-MAIL.md)
* Scaling ATP-S Down to save $$$ - [ATP](/ATP-SERVERLESS-SCALE.md)
# Contacting the Admins

Please use the Slack channel for any requests, as this is monitored - [#integration01_tenancy_collaboration](https://sales-tech-div.slack.com/archives/C01SPKENK1C)
