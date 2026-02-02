
# How to properly set up SPF and DKIM records
 | MailReach Helpdesk

## URL
https://help.mailreach.co/en/article/how-to-properly-set-up-spf-and-dkim-records-1hlbcuq/

## Metadata
- Depth: 0
- Timestamp: 2026-02-02T10:44:58.211722

## Content

Go to website
Home
# How to properly set up SPF and DKIM records
****Table of Contents****

 1. What are SPF & DKIM?
 2. How to set up your SPF record
 3. How to fix the error: Invalid SPF record found
 4. How to set up your DKIM record(s)
 5. How to fix the error: Missing or Invalid DKIM record found
 6. Frequently Asked Questions

# What are SPF & DKIM?

Simply put, SPF (Sender Policy Framework) and DKIM (DomainKeys Identified Mail) are tools that help prove your emails are legitimate, thus preventing them from being marked as spam.

SPF specifies which servers are authorized to send emails on behalf of your domain.

DKIM lets you add a digital signature to your emails, confirming they originated from your domain and remained unaltered in transit.

# How to set up your SPF record

## Step 1: List your Email Service Providers

Very important: your SPF record has to cover ****all the email service providers used to send emails from your domain****. 

MailReach is not considered a provider, it simply triggers the sending from your provider. In other words, your SPF record shouldn't include MailReach. 

Let's say your domain is __mydomain.com__

From this domain, let's say you use Google Workspace to send your day-to-day emails and cold outreach sequences (even if that's automated by using a tool like Outreach, Reply.io, Emelia or whatever).

On top of Google Workspace, you sometimes use Brevo to send newsletters to your subscribers.

That means your SPF record will have to include both Gmail (Google Workspace) and Brevo. 

That being said, list down all the providers used to send emails from your domain and go to the next step.

## Step 2: Go to your domain's DNS settings

Every domain has DNS (Domain Name System) settings, typically managed by the company where you registered your domain (e.g., GoDaddy, Namecheap, Gandi, OVH, Bluehost, etc).

 1. ****Go to your domain registrar****
 2. ****Select your domain****
 3. ****Find the DNS settings**** : after selecting your domain, search for a section called "DNS Settings", "Manage DNS", "DNS Zone Editor", or something similarly named. This section allows you to edit the various records associated with your domain.

## Step 3: Create or update your SPF Record

Your domain's DNS should include ****only one SPF record, never more****. But, as said above, one SPF record can cover multiple Email Service Providers.

Within your DNS settings, look for an existing SPF record: if you already have one it will start with v=spf1. If this exists, you'll need to edit it. If not, you'll create a new TXT record for your SPF.

****SPF record example for Gmail / Google Workspace only:****

```
v=spf1 include:_spf.google.com ~all
```

****SPF record example for Outlook / Office365 only:****

```
v=spf1 include:spf.protection.outlook.com -all
```

For each Email Service Provider, there's a unique SPF "include" statement. Here are some more examples:

 * SendGrid: include:sendgrid.net
 * Mailgun: include:mailgun.org
 * Brevo: include:spf.brevo.com
 * Amazon SES: include:amazonses.com
 * GoDaddy Email: include:secureserver.net
 * For any other provider, use Google and search "setup SPF for __[Your Provider]__ "

### If you use multiple Email Service Providers, combine the "include" statements in one SPF record

Example if you're using both Google Workspace and SendGrid:

```
v=spf1 include:_spf.google.com include:sendgrid.net ~all
```

Example if you're using Outlook, Mailgun and Brevo

```
v=spf1 include:spf.protection.outlook.com include:mailgun.org include:spf.brevo.com ~all
```

## Step 4: Save and wait 48 hours

After adjusting your SPF record, save your DNS settings. Remember, DNS updates can take from minutes to 48 hours to propagate.

If you're using MailReach, come back in 48 hours to see if your SPF record is seen as valid. 

# How to fix the error: Invalid SPF record found

## Step 1: Make sure your SPF record matches the way your emails are sent on MailReach

### If you're using MailReach's Email Warmer

Your SPF record has to ****match the provider you selected when connecting your email account to MailReach****. 

When you first connected your email account on MailReach, you selected a specific provider (Gmail, Outlook, SendGrid, Mailgun, Any other SMTP, etc). 

****Your SPF record has to match this provider****. For instance, if you connected your email account to MailReach as a Gmail (Google Workspace), your SPF has to include Gmail. 

If you selected "Any other SMTP" as a provider, make sure to check with your provider how to set up your SPF record. A Google search "setup SPF for __[Your Provider]__ " should help you.

If you don't remember what you selected as a provider when you connected your email account to MailReach:

 * In MailReach, click on the Email Warmer menu
 * Find your email account, click on Show
 * On the right of your email address, the provider is shown

### If you're using our free SPF Checker

Your SPF record has to match the provider you used to send your email to our SPF checker. 

If you used Outlook to send your email to our SPF Checker, your SPF record has to include Outlook. If you used SendGrid to send your email to our SPF Checker, your SPF record has to include SendGrid, etc.

## Step 2: Make sure you don't have multiple SPF records

Your must have ****only one SPF record, never more****. But keep in mind one SPF record can include multiple Email Service Providers (if you use multiple ESPs to send emails)

Check your DNS records and make sure you don't have several records for SPF. If you have, remove one and make sure the one that remains is correct.

## Step 3: Make sure you don't have errors in your record

The value should start with "v=spf1" and contain one or multiple "include" statements according to how many Email Service Providers you use to send your emails. Keep in mind that you need an "include" statement for ALL providers used to send your emails. 

This is an example of a correct SPF record for one email service provider (Gmail) :

```
v=spf1 include:_spf.google.com ~all
```

And this is an example of a correct SPF record for two email service providers (Outlook and SendGrid) : 

```
v=spf1 include:spf.protection.outlook.com include:sendgrid.net ~all
```

## Step 4: Once you've updated your SPF record, wait at least 3 hours and use our SPF Checker to check its validity

The DNS changes can take up to 48 hours to propagate but they usually propagate faster. 

If you're using MailReach's email warmer: MailReach automatically checks your SPF validity once per 24h. If after 24 hours, you still have the orange notification about your SPF, it means it's not fixed. Please re-read this section to test a new iteration until you manage to get it fixed.

If you don't want to wait for the next day, you can use our Free SPF Checker to quickly see if your new SPF record is valid. 

# How to set up your DKIM record(s)

## Step 1: List your Email Service Providers

Unlike the SPF record, you must have a separate DKIM record for each email service provider used to send emails from your domain.

MailReach is not considered a sending provider, it simply triggers the sending from your provider. You don't need a DKIM record for MailReach. 

Let's say your domain is __mydomain.com__

From this domain, let's say you use Google Workspace to send your day-to-day emails and cold outreach sequences (even if that's automated by using a tool like Outreach, Reply.io, Emelia or whatever).

On top of Google Workspace, you sometimes use Brevo to send newsletters to your subscribers.

That means you will have to setup two different DKIM records. One for Gmail (Google Workspace) and one for Brevo. 

That being said, list down all the providers used to send emails from your domain and go to the next step.

## Step 2: Locate Your Domain's DNS Settings

Every domain has DNS settings, typically managed by the company where you registered your domain (e.g., GoDaddy, Namecheap, Gandi, OVH, Bluehost, etc).

 1. ****Go to your domain registrar****
 2. ****Select your domain****
 3. ****Find the DNS settings**** : after selecting your domain, search for a section called "DNS Settings", "Manage DNS", "DNS Zone Editor", or something similarly named. This section allows you to edit the various records associated with your domain.

## Step 3: Generate DKIM Key(s) for your provider(s)

Each email service provider will have a process for generating a DKIM key. You can Google "setup DKIM for [your provider]"

Here are links to the processes of the most used email service providers:

 * Google Workspace
 * Outlook / Office365
 * Mailgun
 * Brevo
 * Amazon SES
 * For any other provider, use Google and search "setup DKIM for __[your Provider]__ "

Follow your provider's documentation to generate this key. Once done, you'll get two values: a selector and the public key.

## Step 4: Add DKIM to Your DNS

In your DNS settings, create a new TXT record with the details from your email provider:

Name/Host/Alias: Your provider’s selector, often looking like: selector._domainkey
Value/Answer/Destination: The public key given by your provider.

## Step 5: Save and wait 48 hours

Once the DKIM record is added, save your DNS settings. Remember, DNS updates can take from minutes to 48 hours to propagate.

If you're using MailReach's email warmer: MailReach automatically checks your DKIM validity once per 24h. If after 24 hours, you still have the orange notification about your DKIM, it means it's not fixed. Please re-read this section to test a new iteration until you manage to get it fixed.

If you don't want to wait for 24 hours, you can use our Free DKIM Checker to quickly see if your new DKIM record is valid. 

# How to fix the error: Missing or Invalid DKIM record found

## Step 1: Make sure you have a DKIM record that matches the way your emails are sent on MailReach

You need one DKIM record for every email service provider used to send emails from your domain. And at least one DKIM record should match the way your emails are sent on MailReach. 

### If you're using MailReach's Email Warmer

You need at least one DKIM record that matches ****the provider you selected when connecting your email account to MailReach****. 

When you first connected your email account on MailReach, you selected a specific provider (Gmail, Outlook, SendGrid, Mailgun, Any other SMTP, etc). 

****You need one DKIM record set up for this provider****. For instance, if you connected your email account to MailReach as a Gmail (Google Workspace), you need one DKIM record for Gmail. 

If you selected "Any other SMTP" as a provider, make sure to check with your provider how to set up your DKIM record. A Google search "setup DKIM for __[Your Provider]__ " should help you.

If you don't remember what you selected as a provider when you connected your email account to MailReach:

 * In MailReach, click on the Email Warmer menu
 * Find your email account, click on Show
 * On the right of your email address, the provider is shown

### If you're using our free DKIM Checker

You need at least one DKIM record that matches the provider you used to send your email to our DKIM checker. 

If you used Outlook to send your email to our DKIM Checker, you need at least one DKIM record set up for Outlook. If you used SendGrid to send your email to our DKIM Checker, you need at least one DKIM record set up for SendGrid.

## Step 2: Make sure your DKIM record(s) include the right selector. 

Every DKIM record is associated to a selector that is given by your email service provider. Sometimes you can choose the name of your selector. It doesn't matter. 

What's important is to make sure that the selector set up in your Email Service Provider matches the selector in the DKIM record of your DNS settings. 

## Step 3: Make sure your DKIM record doesn't have any error. 

Make sure to check with your Email Service Provider how to properly set up the DKIM record. 

Double check that both the selector and the record given by your provider are well set up in your DNS settings. 

## Step 4: Once you've updated your DKIM record(s), wait 48 hours and come back on MailReach

The DNS changes can take up to 48 hours to propagate and on top of this delay, MailReach needs to check your latest warming emails to see if they pass the SPF check. 

If after 48 hours the Missing or Invalid DKIM notification is still present, please re-read this section to test a new iteration until you manage to get it fixed. 

# Frequently Asked Questions

## Q: How can I verify my records are correct?

A: MailReach will automatically check your SPF and DKIM record once per 24 hours. Come back in 24 hours and go to your Checks page on MailReach. 

I use multiple email providers. How do I set up SPF & DKIM for all?

For SPF, combine the "include" statements as shown above. For DKIM, you’ll need a separate record for each provider.

## Q: I'm having trouble. Who can assist me?

A: If you're struggling, please consult your email provider's documentation or contact their support. They can provide tailored guidance.
Updated on: 16/10/2024
Was this article helpful?
 * Yes
 * No

Share your feedback
Send My FeedbackCancel
Thank you!
Not finding what you are looking for?
Chat with us or send us an email.
 * Chat with us

© 2026!MailReach Helpdesk


---
