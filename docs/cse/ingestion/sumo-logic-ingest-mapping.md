---
id: sumo-logic-ingest-mapping
title: Configure a Sumo Logic Ingest Mapping - Cloud SIEM
sidebar_label: Configure a Sumo Logic Ingest Mapping
description: Learn how to configure Sumo Logic and Cloud SIEM to enable Sumo Logic to send log messages to Cloud SIEM, and Cloud SIEM to select a mapper to process the messages it receives from Sumo Logic.
---

import useBaseUrl from '@docusaurus/useBaseUrl';
import Iframe from 'react-iframe'; 

This topic has instructions for creating a Cloud SIEM ingest mapping for a data source. An ingest mapping gives Cloud SIEM the information it needs in order to map message fields to record attributes. These are referred to as mapping hints, and include: Format, Vendor, Product, and Event ID Pattern.

:::note
The use of ingest mappings is recommended only if there is no Sumo Logic parser or Cloud-to-Cloud connector for the target data source. For more information, see [Cloud SIEM Ingestion Best Practices](/docs/cse/ingestion/cse-ingestion-best-practices/).
:::

:::sumo Micro Lesson

Watch this micro lesson to learn more about ingest mapping for Cloud SIEM:

<Iframe url="https://fast.wistia.net/embed/iframe/vv7p1hquqj?web_component=true&seo=true&videoFoam=false"
  width="854px"
  height="480px"
  title="Micro Lesson: Preprocessing Data for Ingestion into Cloud SIEM Video"
  id="wistiaVideo"
  className="video-container"
  display="initial"
  position="relative"
  allow="autoplay; fullscreen"
  allowfullscreen
/>

Watch this micro lesson to learn about forwarding ingested data to Cloud SIEM:

<Iframe url="https://fast.wistia.net/embed/iframe/krg64dumyv?web_component=true&seo=true&videoFoam=false"
  width="854px"
  height="480px"
  title="Micro Lesson: Forward data from Sumo Logic to Cloud SIEM Video"
  id="wistiaVideo"
  className="video-container"
  display="initial"
  position="relative"
  allow="autoplay; fullscreen"
  allowfullscreen
/>

:::

## Before you start

Before you create ingest mapping for your messages, you need to determine the information described in the following subsections.

### How are your log messages formatted?

You need to know how your messages are formatted. Cloud SIEM supports messages in the following formats:

* Unstructured messages with a syslog header
* Unstructured messages without a syslog header
* JSON messages without a syslog header
* JSON messages with a syslog header
* CEF or LEEF messages with a syslog header
* CEF or LEEF messages without a syslog header
* Structured syslog data (key-value pairs) with a syslog header
* Microsoft Windows event logs in XML format
* Winlogbeats
* Messages that have been processed by Sumo Logic [Field Extraction Rules](/docs/manage/field-extractions).

### Determining Product, Vendor, and Event ID pattern

When you fill out the **Add Ingest Mapping** page, for most of the supported message formats, all you need to select a value for **Format**. However, for the following formats, you also need to tell Cloud SIEM the **Product**, **Vendor**, and **Event ID template** for the messages:

* JSON messages without a syslog header
* JSON messages with a syslog header
* Structured syslog data (key-value pairs) with a syslog header
* Messages that have been processed by Sumo Logic Field Extraction Rules.

For these formats, Cloud SIEM uses the values you configure for **Product**, **Vendor**, and **Event ID** (in addition to **Format**) to select the appropriate Cloud SIEM mapper to process the messages. To verify the correct values, you can go to the **Log Mapping Details** page for the mapper in the Cloud SIEM UI. To do so:

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the top menu select **Configuration**, and then under **Incoming Data** select **Log Mappings**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the top menu select **Configuration**, and then under **Cloud SIEM Integrations** select **Log Mappings**. You can also click the **Go To...** menu at the top of the screen and select **Log Mappings**.  
1. The **Log Mappings** tab displays a list of mappers.<br/><img src={useBaseUrl('img/cse/log-mappings-page.png')} alt="Log Mappings page" width="800"/>
1. In the **Filters** area, you can filter the list of log mappings by
    typing in a keyword, or by selecting a field to filter by.<br/><img src={useBaseUrl('img/cse/log-mapping-filters.png')} alt="Log Mappings filters" style={{border: '1px solid gray'}} width="400"/>
1. When you find the mapper you’re looking for, you can find the following for a mapper on the **If Input Matches** side of the page:
    * Vendor
    * Product
    * Format
    * Event ID pattern<br/><img src={useBaseUrl('img/cse/mapping.png')} alt="Log Mapping details" style={{border: '1px solid gray'}} width="800"/>

### Quick reference to configuring ingest mappings

This table in this section is a quick reference to supplying values for each supported message format on the **Add Ingest Mapping** page in Cloud SIEM. This reference summarizes the step-by-step instructions provided below. 

| If your messages are... | Select this option for Format | Are Vendor, Product, andEvent ID pattern required? | How Cloud SIEM picks a mapper |
| :-- | :-- | :-- | :-- |
| Unstructured logs lines with a syslog header | Process Syslog with Valid Header | No | Cloud SIEM will send the messages to the mapper whose name is the same as the name of the pattern the message matches. |
| Unstructured log lines without a syslog header | Do not Process Syslog Header | No | Cloud SIEM will send the messages to the mapper whose name is the same as the name of the pattern the message matches.  |
| JSON without a syslog header | JSON | Yes | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** pattern you enter in the **Sumo Ingest Mapping**. |
| JSON with a syslog header	Process Syslog with Valid Header | You’ll be prompted to select whether messages are JSON or key-value pairs. Choose “JSON”. | Yes | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** pattern you enter in the **Sumo Ingest Mapping**. |
| CEF / LEEF with a syslog header | Process Syslog with Valid Header | No | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** from the CEF/LEEF message. |
| CEF / LEEF without a syslog header | Do not Process Syslog Header | No | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** from the CEF/LEEF message. |
| Structured syslog data (KV pairs) with syslog header | Process Syslog with Valid Header<br/>You’ll be prompted to select whether messages are JSON or key-value pairs. Choose “Key-Value”. Then supply delimiters. | Yes | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** pattern you enter in the Sumo Ingest Mapping. |
| Microsoft Windows event logs in XML | Windows | No | Cloud SIEM will send a message to the log mapper whose:<br/>**Format** is “Windows”<br/>**Vendor** is “Microsoft”<br/>**Product** is “Windows”<br/>**Event** ID pattern is the value of `{channel}-{eventid}` from the Windows event, for example, “Security-1234”. |
| Winlogbeats | Winlogbeats | No | Cloud SIEM will send a message to the log mapper whose:<br/>**Format** is “Windows”<br/>**Vendor** is “Microsoft” <br/>**Product** is “Windows” <br/>**Event ID** pattern is the value of `{channel}-{eventid}` from the Windows event, for example, “Security-1234”. |
| Fields extracted from Sumo Logic-ingested messages | Extracted Fields JSON | Yes | Cloud SIEM will send the messages to the log mapper with the **Format**, **Vendor**, **Product**, and **Event ID** pattern you enter in the Sumo **Ingest Mapping.** |

## Configure Sumo Logic Ingest Mapping in Cloud SIEM

In this step, you configure a Sumo Logic Ingest Mapping in Cloud SIEM for the source category assigned to your source or collector you configured. The mapping tells Cloud SIEM the information it needs to select the right mapper to process messages that have been tagged with that source category. 

1. [**Classic UI**](/docs/get-started/sumo-logic-ui-classic). In the top menu select **Configuration**, and then under **Integrations** select **Sumo Logic**. <br/>[**New UI**](/docs/get-started/sumo-logic-ui). In the top menu select **Configuration**, and then under **Cloud SIEM Integrations** select **Ingest Mappings**. You can also click the **Go To...** menu at the top of the screen and select **Ingest Mappings**.  
1. On the **Ingest Mappings** tab, click **+ Add Ingest Mapping**.
1. On the **Add Ingest Mapping** popup:
    1. **Source Category**. Enter the category you assigned to the HTTP Source or Hosted Collector. 
    1. **Format**. Follow the instructions for the type of messages your source collects:
        * [Unstructured messages with a syslog header](#unstructured-messages-with-a-syslog-header)
        * [Unstructured messages without a syslog header](#unstructured-messages-without-a-syslog-header)
        * [JSON messages without a syslog header](#json-messages-without-a-syslog-header)
        * [JSON messages with a syslog header](#json-messages-with-a-syslog-header)
        * [CEF or LEEF messages with a syslog header](#cef-or-leef-messages-with-a-syslog-header)
        * [CEF or LEEF messages without a syslog header](#cef-or-leef-messages-without-a-syslog-header)
        * [Structured syslog data (key-value pairs) with a syslog header](#structured-syslog-data-key-value-pairs-with-a-syslog-header)
        * [Microsoft Windows event logs in XML format](#microsoft-windows-event-logs-in-xml-format)
        * [Winlogbeats](#winlogbeats)
        * [Fields extracted from Sumo Logic-ingested messages](#fields-extracted-from-sumo-logic-ingested-messages)

### Unstructured messages with a syslog header

If your messages are unstructured with a syslog header, all you need to do is select “Process Syslog with Valid Header” for **Format**. 

<img src={useBaseUrl('img/cse/create-mapping-1.png')} alt="Create mapping" style={{border: '1px solid gray'}} width="400"/>

### Unstructured messages without a syslog header

If your messages are unstructured without a syslog header, all you need to do is select “Do not Process Syslog Header” for **Format**. 

<img src={useBaseUrl('img/cse/create-mapping-3.png')} alt="Create mapping without header" style={{border: '1px solid gray'}} width="400"/>

### JSON messages without a syslog header

If your messages are JSON format without a syslog header, there are required and optional configuration settings.

#### Required settings: Format, Vendor, Product, and Event ID

1. For **Format**, select “JSON”. 
1. You must specify values for **Vendor**, **Product**, and **Event ID**, which Cloud SIEM will use to determine what mapper to use for your messages. If you don’t know these values, see [Determining Product, Vendor, and Event ID pattern](#determining-product-vendor-and-event-id-pattern), above. <br/><img src={useBaseUrl('img/cse/create-mapping-2.png')} alt="Create mapping with JSON format" style={{border: '1px solid gray'}} width="400"/> 

#### Optional settings: Advanced JSON Parsing

If you would like to manipulate the JSON data before it’s flattened and parsed, expand the **Advanced JSON Parsing** section of the popup.<br/><img src={useBaseUrl('img/cse/advanced-json-parsing.png')} alt="Advanced JSON parsing" style={{border: '1px solid gray'}} width="400"/>

1. **JSON Explode**. This option takes a JSON array value (flattened value) and creates multiple copies of the log line, one for each value of the array. You can only apply JSON Explode to one attribute within the JSON. For example, given the following example JSON log:  

    `{ “animals” : { “pets” : [“cat”, “dog”], “owned”: “true”}, “kids”: “none”}`  


    Setting the JSON Explode to `animals.pets` results in the creation of two separate raw log lines:  

    `{ “animals” : { “pets” : “dog”, “owned”: “true”}, “kids”: “none”}{ “animals” : { “pets” : “cat”, “owned”: “true”}, “kids”: “none”}`  

     
1. **JSON Zip Operations**. Collapses JSON arrays in which key-value
    pairs are repeated with a common key identifier and value
    identifier. For example, given the following JSON array:  

    `{ “pets” : [ {“name” : “fluffy”}, {“type”: “cat”}, {“name”: “fido”, “type” : “dog”}, {“name”: “sammy”, “type” : “snake}]}`  

    The JSON Zip operation will turn the array into:   

    `{ “pets” : { “fluffy” : “cat” , “fido” : “dog”, “sammy” : “snake”}}`  

    The JSON Zip parameters are:
    * **Key Name**. The name of the attribute whose value is the array to zip.
    * **Match Key**. The name of the attribute that represents the key in the output. In the example above, it’s `name`.
    * **Match Value**. The attribute in the array object that represents the value in the final output. In the example above it’s `type`.

### JSON messages with a syslog header

If your messages are JSON format with a syslog header:

1. **Format**. Select “Process Syslog with Valid Header”. 
1. **Syslog Format**. Choose “JSON”.
1. You must specify values for **Vendor**, **Product,** and **Event ID**, which Cloud SIEM will use to determine what mapper to use for your messages. If you don’t know these values, see [Determining Product, Vendor, and Event ID pattern](#determining-product-vendor-and-event-id-pattern).<br/><img src={useBaseUrl('img/cse/create-mapping-4.png')} alt="JSON message with syslog header" style={{border: '1px solid gray'}} width="400"/>  

### CEF or LEEF messages with a syslog header

If your messages are CEF or LEEF messages with a syslog header, all you need to do is select “Process Syslog with Valid Header” for **Format**.

Don’t specify **Syslog Format**. 

Don’t specify **Vendor**, **Product,** or **Event ID**. Cloud SIEM can determine those values from the CEF or LEEF message itself.<br/><img src={useBaseUrl('img/cse/create-mapping-1.png')} alt="Process syslog with valid header" style={{border: '1px solid gray'}} width="400"/> 

### CEF or LEEF messages without a syslog header

If your messages are CEF or LEEF messages without a syslog header, all you need to do is select “Do Not Process Syslog Header” for **Format**.

Don’t specify **Syslog Format**. 

Don’t specify **Vendor**, **Product**, or **Event ID**. Cloud SIEM can determine those values from the CEF or LEEF message itself.<br/><img src={useBaseUrl('img/cse/create-mapping-3.png')} alt="CEF or LEEF messages without header" style={{border: '1px solid gray'}} width="400"/>

### Structured syslog data (key-value pairs) with a syslog header

If your messages are structured syslog data (key-value pairs) with a syslog header:

1. **Format**. Select “Process Syslog with Valid Header”. 
1. **Syslog Format**. Choose “Key-Value”.
1. The popup refreshes, with options for syslog delimiters.
1. **Syslog Delimiter**. This is the delimiter between the key-value pairs.
1. **Syslog kv Delimiter**. This is the delimiter between a key and a value.
1. You must specify values for **Vendor**, **Product**, and **Event ID**, which Cloud SIEM will use to determine what mapper to use for your messages. If you don’t know these values, see [Determining Product, Vendor, and Event ID pattern](#determining-product-vendor-and-event-id-pattern).<br/><img src={useBaseUrl('img/cse/syslog-delimiters.png')} alt="Syslog delimiters" style={{border: '1px solid gray'}} width="400"/>  

### Microsoft Windows event logs in XML format

If your messages are Windows event logs in XML format, all you need to do is select “Windows” for **Format**.

Cloud SIEM will determine the appropriate mapper to use from individual events. It will select the mapper whose:

* **Format** is “Windows”.
* **Vendor** is “Microsoft”.
* **Product** is “Windows”.
* **Event ID** is the value of `{channel}-{eventid}`, for example, “Security-1234”.

<img src={useBaseUrl('img/cse/windows.png')} alt="Windows mapping" style={{border: '1px solid gray'}} width="400"/>


### Winlogbeats

If your messages are from Winlogbeats, all you need to do is select “Winlogbeats” for **Format**.

Cloud SIEM will determine the appropriate mapper to use from individual events. It will select the mapper whose:

* **Format** is “Windows”.
* **Vendor** is “Microsoft”.
* **Product** is “Windows”.
* **Event ID** is the value of `{channel}-{eventid}`, for example, “Security-1234”.

<img src={useBaseUrl('img/cse/winlogbeats.png')} alt="Winlogbeats" style={{border: '1px solid gray'}} width="400"/>

### Fields extracted from Sumo Logic-ingested messages

If the messages with the source category you’ve specified in the mapping have had Sumo Logic Field Extraction Rules applied to them:

1. **Format**. Select “Extracted Fields JSON”
1. You must specify values for **Vendor**, **Product**, and **Event ID**, which Cloud SIEM will use to determine what mapper to use for your messages. If you don’t know these values, see [Determining Product, Vendor, and Event ID pattern](#determining-product-vendor-and-event-id-pattern). 

<img src={useBaseUrl('img/cse/extracted-fields-json.png')} alt="Extracted fields JSON" style={{border: '1px solid gray'}} width="400"/>

## Enable mapping

For Cloud SIEM to be able to select a mapper for messages from Sumo Logic, a valid ingest mapping must be configured and enabled for the source category associated with incoming messages. 

To enable the mapping you have created, move the **Enabled** slider to “On”.
