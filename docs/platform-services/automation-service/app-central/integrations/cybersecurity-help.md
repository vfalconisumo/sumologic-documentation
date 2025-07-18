---
title: Cybersecurity Help
description: ''
---
import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/logos/cybersecurity-help.png')} alt="cybersecurity-help" width="100"/>

***Version: 1.1  
Updated: Jul 06, 2023***

Cybersecurity Help is a global vulnerability intelligence provider.

## Actions

* **Get Subscription Info** (*Enrichment*) - Retrieve your current subscription status.
* **Get Subscribed Software Status** (*Enrichment*) - Retrieve recent software subscription requests and their current status.
* **List Assets** (*Enrichment*) - List your assets.
* **List Subscribed Software** (*Enrichment*) - List of software that is being monitored according to your subscription settings.
* **List User Tasks** (*Enrichment*) - Retrieve unprocessed tasks.
* **List User Tasks Asset** (*Enrichment*) - Retrieve unprocessed tasks for a particular asset.
* **List User Tasks Group** (*Enrichment*) - Retrieve unprocessed group tasks.
* **Add Subscribed Software Monitoring** (*Containment*) - Configure software subscription for a particular asset.
* **Mark User Task Processed** (*Containment*) - Set current task as processed.
* **Mark User Task Updated** (*Containment*) - Set the current task as updated and update current software version in subscription.
* **Remove Asset** (*Containment*) - Remove an asset and cancel all subscriptions connected with it.
* **Remove Asset Subscribed Software** (*Containment*) - Remove subscribed software for a particular asset.

## Cybersecurity Help configuration

1. Log in to Cybersecurity Help to get your API Key.
1. Select Subscription from the menu, choose Settings and copy your Token.<br/><img src={useBaseUrl('/img/platform-services/automation-service/app-central/integrations/cybersecurity-help/cybersecurity-help-1.png')} style={{border:'1px solid gray'}} alt="cybersecurity" width="600"/>

## Configure Cybersecurity Help in Automation Service and Cloud SOAR

import IntegrationsAuth from '../../../../reuse/integrations-authentication.md';
import IntegrationCertificate from '../../../../reuse/automation-service/integration-certificate.md';
import IntegrationEngine from '../../../../reuse/automation-service/integration-engine.md';
import IntegrationLabel from '../../../../reuse/automation-service/integration-label.md';
import IntegrationProxy from '../../../../reuse/automation-service/integration-proxy.md';
import IntegrationTimeout from '../../../../reuse/automation-service/integration-timeout.md';

<IntegrationsAuth/>
* <IntegrationLabel/>
* **URL**. Enter you Cybersecurity Help URL. The default value is `https://www.cybersecurity-help.cz`

* **Token**. Enter the Cybersecurity Help token you [copied earlier](#cybersecurity-help-configuration).
* <IntegrationTimeout/>
* <IntegrationCertificate/>
* <IntegrationEngine/>
* <IntegrationProxy/>

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/integrations/misc/cybersecurity-help-configuration.png')} style={{border:'1px solid gray'}} alt="Cybersecurity Help configuration" width="400"/>

For information about Cybersecurity Help, see the [Cybersecurity Help website](https://www.cybersecurity-help.cz/).

## Change Log

* October 26, 2022 - First upload
* July 6, 2023 (v1.1) - Updated the integration with Environmental Variables
