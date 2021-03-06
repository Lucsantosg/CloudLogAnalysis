---

copyright:
  years: 2017, 2019

lastupdated: "2019-05-01"

keywords: IBM Cloud, logging

subcollection: cloudloganalysis

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}
{:table: .aria-labeledby="caption"}
{:codeblock: .codeblock}
{:tip: .tip}
{:download: .download}
{:important: .important}
{:note: .note}
{:deprecated: .deprecated}


# Kibana FAQ
{: #faq_kibana}

Here are the answers to common questions about using {{site.data.keyword.Bluemix}} logging capabilities. 
{:shortdesc}

{{site.data.keyword.loganalysisfull_notm}} is deprecated. As of 30 April 2019, you cannot provision new {{site.data.keyword.loganalysisshort_notm}} instances. Existing premium plan instances are supported until 30 September 2019. To continue managing system and application logs in {{site.data.keyword.cloud_notm}}, [set up {{site.data.keyword.la_full_notm}}](/docs/services/Log-Analysis-with-LogDNA?topic=LogDNA-getting-started#getting-started).
{: deprecated}

* [What can I do if I cannot see data in the Discover page in Kibana](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#logging_qa_no_data_discover_kibana)
* [What can I do if I get an authentication exception](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#logging_qa_no_data_dashboard_kibana)
* [Why do I see the symbol ? by fields in the Kibana Discover page](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#logging_qa_kibana_question)
* [I get a 403 error when I try to change the default index pattern](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#error_403)
* [Short URL does not work](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#short_url)
* [Can I search my account logs in Bluemix?](/docs/services/CloudLogAnalysis/qa?topic=cloudloganalysis-faq_kibana#acc_logs_1)


## What can I do if I cannot see data in the Discover page in Kibana
{: #logging_qa_no_data_discover_kibana}

There are different scenarios by which you might not see data in Kibana:

1. When you launch Kibana, you might not see any data in the Discover page. You receive the following message: **No results found.**.
2. You might be working in the Discover page in Kibana. However, after a short period of time, you receive the message: **No results found.** when you try to perform a task in Kibana.

To resolve this problem, complete the following steps:

1. Check the *Time Picker* that is set in the Discover page and increase the time period.

    **Note**: By default, in the {{site.data.keyword.Bluemix_notm}}, the *Time Picker* is set to show data for the last 15 minutes.

    For more information on how to set the *Time Picker*, see [Setting a time filter](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-filter_logs#set_time_filter1).

2. Click the magnifying glass that is located in the *Discover* page search bar. The page data is refreshed based on the default search query.

    Alternatively, you can set an *Auto refresh* period.

    **Note**: By default, in {{site.data.keyword.Bluemix_notm}}, the *Auto refresh* period is set to **OFF**.

    For more information on how to enable it, see [Automatically refreshing the data](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analize_logs_interactively#discover_view_refresh_interval).



## What can I do if I get an authentication exception
{: #logging_qa_no_data_dashboard_kibana}

When you cannot see data displayed in your visualizations in a Dashboard page, and you get the error message: **Error: Authorization Exception.**, check your permissions to see data in each visualization.

Consider the following information:
You can configure one or more visualizations in a Dashboard page. When the Dashboard page makes a request to gather the data that is displayed thorugh those visualizations, only one request is issued for all the visualizations. If your do not have permissions to see data one of the visualizations, the entire request fails.

To resolve this problem, complete the following steps:

1. Identify the visualizations for which you do not have permissions.

    1. Click the *pencil* icon of a visualization in the *Dashboard* page. The visualization opens in the *Visualize* page. Alternatively, in the *Visualize* page, load one visualization.
    2. Verify you can see data.

    Repeat these steps for each visualization.

2. Request access to see data in those visualizations from your cloud administrator.

3. Create a new Dashboard page that excludes the visualizations for which you do not have permissions while you are granted access to see data in the visualizations that are causing the problem.

    If you share the Dashboard, do not delete visualizations since that will affect other team members that use the same dashboard.



## Why do I see the symbol ? by fields in the Kibana Discover page
{: #logging_qa_kibana_question}

When you open the Discover page in Kibana, you might see a question mark `?` by fields that are listed in the available fields section instead of the character `t`. When you reload the list of fields, the type of fields is analyzed, and the question mark `?` is replaced by the character `t`. For more information, see [Reloading the list of fields](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-analize_logs_interactively#discover_view_reload_fields).


## I get a 403 error when I try to change the default index pattern
{: #error_403}

The default index pattern cannot be changed.

If you try to set a different index pattern as the new default one, you get the following error: `Config: Error 403 Forbidden`

## Short URL does not work
{: #short_url}

Sharing a search, a visualization, or a dashboard is not supported. Therefore, any short URL for a Kibana object that you want to share does not work either.

## Can I search my account logs in Bluemix?
{: #acc_logs_1}

As an account owner, you can search and analyze your account logs.

Complete the following steps to see your account logs:

1. [Launch Kibana.](/docs/services/CloudLogAnalysis/kibana?topic=cloudloganalysis-launch#launch_Kibana_from_browser) For example for the US South region, use the URL `https://logging.ng.bluemix.net`,

2. Select the option **View AccountName account Logs** to display the account logs. *AccountName* is the name of the account.
