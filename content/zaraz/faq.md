---
pcx_content_type: faq
title: FAQ
weight: 10
structured_data: true
---

# FAQ

Below you will find answers to our most commonly asked questions. If you cannot find the answer you are looking for, refer to the [community page](https://community.cloudflare.com/) or [Discord channel](https://discord.cloudflare.com) to explore additional resources.

- [General](#general)
- [Tools](#tools)
- [Consent](#consent)

---

## General

### Setting up Zaraz

{{<faq-item>}}
{{<faq-question level=4 text="Why is Zaraz not working?" >}}

{{<faq-answer>}}

If you are experiencing issues with Zaraz, there could be multiple reasons behind it. First, it's important to verify that the Zaraz script is loading properly on your website.

To check if the script is loading correctly, follow these steps:

1. Open your website in a web browser.
2. Open your browser's Developer Tools.
3. In the Console, type `zaraz`.
4. If you see an error message saying `zaraz is not defined`, it means that Zaraz failed to load.

If Zaraz is not loading, please verify the following:

- The domain running Zaraz [is proxied by Cloudflare](/dns/manage-dns-records/reference/proxied-dns-records/).
- Auto Injection is enabled in your [Zaraz Settings](/zaraz/reference/settings/#auto-inject-script).
- Your website's HTML is valid and includes `<head>` and `</head>` tags.
- You have at least [one enabled tool](/zaraz/get-started/add-tool/) configured in Zaraz.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="I'm seeing some data discrepancies. Is there a way to check what data reaches Zaraz?" >}}

{{<faq-answer>}}

Yes. You can use the metrics in [Zaraz Monitoring](/zaraz/monitoring/) to help you find where in the workflow the problem occurred.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Can I use Zaraz with Rocket Loader?" >}}

{{<faq-answer>}}

We recommend disabling [Rocket Loader](/speed/optimization/content/rocket-loader/) when using Zaraz. While Zaraz can be used together with Rocket Loader, there's usually no need to use both. Rocket Loader can sometimes delay data from reaching Zaraz, causing issues.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Is Zaraz compatible with Content Security Policies (CSP)?" >}}

{{<faq-answer>}}

Yes. To learn more about how Zaraz works to be compatible with {{<glossary-tooltip term_id="content security policy (CSP)">}}CSP{{</glossary-tooltip>}} configurations, refer to the [Cloudflare Zaraz supports CSP](https://blog.cloudflare.com/cloudflare-zaraz-supports-csp/) blog post.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Does Cloudflare process my HTML, removing existing scripts and then injecting Zaraz?" >}}

{{<faq-answer>}}

Cloudflare Zaraz does not remove other third-party scripts from the page. Zaraz [can be auto-injected or not](/zaraz/reference/settings/#auto-inject-script), depending on your configuration, but if you have existing scripts that you intend to load with Zaraz, you should remove them.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Does Zaraz work with Cloudflare Page Shield?" >}}

{{<faq-answer>}}

Yes. Refer to [Page Shield](/page-shield/) for more information related to this product.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Is there a way to prevent Zaraz from loading on specific pages, like under `/wp-admin`?" >}}

{{<faq-answer>}}

To prevent Zaraz from loading on specific pages, refer to [Load Zaraz selectively](/zaraz/advanced/load-selectively/).

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="How can I remove my Zaraz configuration?" >}}

{{<faq-answer>}}

Resetting your Zaraz configuration will erase all of your configuration settings, including any tools, triggers, and variables you've set up. This action will disable Zaraz immediately. If you want to start over with a clean slate, you can always reset your configuration.

1. Log in to the [Cloudflare dashboard](https://dash.cloudflare.com/), and select your account and domain.
2. Go to **Zaraz** > **Settings** > **Advanced**.
3. Click "Reset" and follow the instructions.

{{</faq-answer>}}
{{</faq-item>}}

### Zaraz Web API

{{<faq-item>}}
{{<faq-question level=4 text="Why would the `zaraz.ecommerce()` method returns an undefined error?" >}}

{{<faq-answer>}}

E-commerce tracking needs to be enabled in [the Zaraz Settings page](/zaraz/reference/settings/#e-commerce-tracking) before you can start using the E-commerce Web API.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="How would I trigger pageviews manually on a Single Page Application (SPA)?" >}}

{{<faq-answer>}}

Zaraz comes with built-in [Single Page Application (SPA) support](/zaraz/reference/settings/#single-page-application-support) that automatically sends pageview events when navigating through the pages of your SPA. However, if you have advanced use cases, you might want to build your own system to trigger pageviews. In such cases, you can use the internal SPA pageview event by calling `zaraz.track("__zarazSPA")`.

{{</faq-answer>}}
{{</faq-item>}}

---

## Tools

### Google Analytics

{{<faq-item>}}
{{<faq-question level=4 text="After moving from Google Analytics 4 to Zaraz, I can no longer see demographics data. Why?" >}}

{{<faq-answer>}}

You probably have enabled **Hide Originating IP Address** in the [Settings option](/zaraz/get-started/edit-tools-and-actions/) for Google Analytics 4. This tells Zaraz to not send the IP address to Google. To have access to demographics data and anonymize your visitor's IP, you should use [**Anonymize Originating IP Address**](#i-see-two-ways-of-anonymizing-ip-address-information-on-the-third-party-tool-google-analytics-one-in-privacy-and-one-in-additional-fields.-which-is-the-correct-one) instead.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="I see two ways of anonymizing IP address information on the third-party tool Google Analytics: one in Privacy, and one in Additional fields. Which is the correct one?" >}}

{{<faq-answer>}}

There is not a correct option, as the two options available in Google Analytics (GA) do different things.

The **Hide Originating IP Address** option in [Tool Settings](/zaraz/get-started/edit-tools-and-actions/) prevents Zaraz from sending the IP address from a visitor to Google. This means that GA treats Zaraz’s Worker’s IP address as the visitor’s IP address. This is often close in terms of location, but it might not be.

With the **Anonymize Originating IP Address** available in the [Add field](/zaraz/get-started/additional-fields/) option, Cloudflare sends the visitor’s IP address to Google as is, and passes the [`aip` parameter](https://developers.google.com/analytics/devguides/collection/protocol/v1/parameters#aip) to GA. This asks GA to anonymize the data.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="If I set up Event Reporting (enhanced measurements) for Google Analytics, why does Zaraz only report Page View, Session Start, and First Visit?" >}}

{{<faq-answer>}}

This is not a bug. Zaraz does not offer all the automatic events the normal GA4 JavaScript snippets offer out of the box. You will need to build [triggers](/zaraz/get-started/create-trigger/) and [actions](/zaraz/get-started/create-actions/) to capture those events. Refer to [Get started](/zaraz/get-started/) to learn more about how Zaraz works.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Can I set up custom dimensions for Google Analytics with Zaraz?" >}}

{{<faq-answer>}}

Yes. Refer to [Additional fields](/zaraz/get-started/additional-fields/) to learn how to send additional data to tools.

{{</faq-answer>}}
{{</faq-item>}}

### Facebook Pixel

{{<faq-item>}}
{{<faq-question level=4 text="If I set up Facebook Pixel on my Zaraz account, why am I not seeing data coming through?" >}}

{{<faq-answer>}}

It can take between 15 minutes to several hours for data to appear on Facebook’s interface, due the way Facebook Pixel works. You can also use [debug mode](/zaraz/web-api/debug-mode/) to confirm that data is being properly sent from your Zaraz account.

{{</faq-answer>}}
{{</faq-item>}}

### Custom HTML

{{<faq-item>}}
{{<faq-question level=4 text="Can I use Google Tag Manager together with Zaraz?" >}}

{{<faq-answer>}}

You can load Google Tag Manager using Zaraz, but it is not recommended. Tools configured inside Google Tag Manager cannot be optimized by Zaraz, and cannot be restricted by the Zaraz privacy controls. In addition, Google Tag Manager could slow down your website because it requires additional JavaScript, and its rules are evaluated client-side. If you are currently using Google Tag Manager, we recommend replacing it with Zaraz by configuring your tags directly as Zaraz tools.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="Why should I prefer a native tool integration instead of an HTML snippet?" >}}

{{<faq-answer>}}

Adding a tool to your website via a native Zaraz integration is always better than using an HTML snippet. HTML snippets usually depends on additional client-side requests, and require client-side code execution, which can slow down your website. They are often a security risk, as they can be hacked. Moreover, it can be very difficult to control their affect on the privacy of your visitors. Tools included in the Zaraz library are not suffering from these issues - they are fast, executed at the edge, and be controlled and restricted because they are sandboxed.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="How can I set my Custom HTML to be injected just once in my Single Page App (SPA) website?" >}}

{{<faq-answer>}}

If you have enabled "Single Page Application support" in Zaraz Settings, your Custom HTML code may be unnecessarily injected every time a new SPA page is loaded. This can result in duplicates. To avoid this, go to your Custom HTML action and select the "Add Field" option. Then, add the "Ignore SPA" field and enable the toggle switch. Doing so will prevent your code from firing on every SPA pageview and ensure that it is injected only once.

{{</faq-answer>}}
{{</faq-item>}}

### Other tools

{{<faq-item>}}
{{<faq-question level=4 text="What if I want to use a tool that is not supported by Zaraz?" >}}

{{<faq-answer>}}

The Zaraz engineering team is adding support to new tools all the time. You can also refer to the [community space](https://community.cloudflare.com/c/developers/integrationrequest/68) to ask for new integrations.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="I cannot get a tool to load when the website is loaded. Do I have to add code to my website?" >}}

{{<faq-answer>}}

If you proxy your domain through Cloudflare, you do not need to add any code to your website. By default, Zaraz includes an automated `Pageview` trigger. Some tools, like Google Analytics, automatically add a `Pageview` action that uses this trigger. With other tools, you will need to add it manually. Refer to [Get started](/zaraz/get-started/) for more information.

{{</faq-answer>}}
{{</faq-item>}}

{{<faq-item>}}
{{<faq-question level=4 text="I am a vendor. How can I integrate my tool with Zaraz?" >}}

{{<faq-answer>}}

The Zaraz team is working with third-party vendors to build their own Zaraz integrations using the Zaraz SDK. To request a new tool integration, or to collaborate on our SDK, contact us at zaraz@cloudflare.com.

{{</faq-answer>}}
{{</faq-item>}}

---

## Consent

{{<faq-item>}}
{{<faq-question level=4 text="How do I show the consent modal again to all users?" >}}

{{<faq-answer>}}

In such a case, you can change the cookie name in the *Consent cookie name* field in the Zaraz Consent configuration. This will cause the consent modal to reappear for all users. Make sure to use a cookie name that has not been used for Zaraz on your site.

{{</faq-answer>}}
{{</faq-item>}}