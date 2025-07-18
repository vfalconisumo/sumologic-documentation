---
title: EclecticIQ
description: ''
---
import useBaseUrl from '@docusaurus/useBaseUrl';

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/logos/eclecticiq.png')} alt="eclecticiq" width="100"/>

***Version: 1.1  
Updated: Jul 06, 2023***

State-of-the-art CTI technology for large enterprises, governments, and MSSPs.

## Actions

* **List Observables** (*Enrichment*) - Retrieve a list of observables.
* **Add Observable** (*Containment*) - Create an observable.
* **Update Observable** (*Containment*) - Update observable by ID.
* **Get Observable Details** (*Enrichment*) - Retrieve detail about an observable by ID.
* **Delete Observable** (*Containment*) - Delete observable by ID.
* **List Entities** (*Enrichment*) - Retrieve a list of entities.
* **Add Entity** (*Containment*) - Create an entity.
* **Update Entity** (*Containment*) - Update entity by ID.
* **Get Entity Details** (*Enrichment*) - Retrieve detail about an entity by ID.
* **Delete Entity** (*Containment*) - Delete entity by ID.
* **List Enrichers** (*Enrichment*) - Retrieve a list of enrichers.
* **Update Enricher** (*Containment*) - Update enricher by ID.
* **Get Enricher Details** (*Enrichment*) - Retrieve detail about an enricher by ID.

## Configure EclecticIQ in Automation Service and Cloud SOAR

import IntegrationsAuth from '../../../../reuse/integrations-authentication.md';
import IntegrationCertificate from '../../../../reuse/automation-service/integration-certificate.md';
import IntegrationEngine from '../../../../reuse/automation-service/integration-engine.md';
import IntegrationLabel from '../../../../reuse/automation-service/integration-label.md';
import IntegrationProxy from '../../../../reuse/automation-service/integration-proxy.md';
import IntegrationTimeout from '../../../../reuse/automation-service/integration-timeout.md';

<IntegrationsAuth/>
* <IntegrationLabel/>
* **URL**. Enter the URL for your EclecticIQ instance.

* **API Token**. Enter an EclecticIQ [API token](https://docs.eclecticiq.com/ic/2.13.0/Create_an_API_token.html).

* **API Version**. Enter the EclecticIQ API version number.
* <IntegrationTimeout/>
* <IntegrationCertificate/>
* <IntegrationEngine/>
* <IntegrationProxy/>

<img src={useBaseUrl('/img/platform-services/automation-service/app-central/integrations/misc/eclecticiq-configuration.png')} style={{border:'1px solid gray'}} alt="EclecticIQ configuration" width="400"/>

For information about EclecticIQ, see the [EclecticIQ documentation](https://docs.eclecticiq.com/).

## Change Log

* November 15, 2021 - First upload
* July 6, 2023 (v1.1) - Updated the integration with Environmental Variables
