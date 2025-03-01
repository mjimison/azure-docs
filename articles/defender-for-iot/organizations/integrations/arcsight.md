---
title: Integrate ArcSight with Microsoft Defender for IoT
description: Learn how to send Microsoft Defender for IoT alerts to ArcSight.
ms.topic: integration
ms.date: 08/02/2022
---

# Integrate ArcSight with Microsoft Defender for IoT

This article describes how to send Microsoft Defender for IoT alerts to ArcSight. Integrating Defender for IoT with ArcSight provides visibility into the security and resiliency of OT networks and a unified approach to IT and OT security.

## Prerequisites

Before you begin, make sure that you have the following prerequisites:

- Access to a Defender for IoT OT sensor as an Admin user.

## Configure the ArcSight receiver type

To configure your ArcSight server settings so that it can receive Defender for IoT alert information:

1. Sign in to your ArcSight server.
1. Configure your receiver type as a **CEF UDP Receiver**.

For more information, see the [ArcSight SmartConnectors Documentation](https://www.microfocus.com/documentation/arcsight/arcsight-smartconnectors-8.4/#gsc.tab=0).

## Create a Defender for IoT forwarding rule

This procedure describes how to create a forwarding rule from your OT sensor to send Defender for IoT alerts from that sensor to ArcSight.

Forwarding alert rules run only on alerts triggered after the forwarding rule is created. Alerts already in the system from before the forwarding rule was created are not affected by the rule.

For more information, see [Forward alert information](../how-to-forward-alert-information-to-partners.md).

1. Sign in to your OT sensor console and select **Forwarding** on the left.

1. Enter a meaningful name for your rule, and then define your rule details, including:

    - The minimal alert level. For example, if you select Minor, you are notified about all minor, major and critical incidents.
    - The protocols you want to include in the rule.
    - The traffic you want to include in the rule.

1. In the **Actions** area, define the following values:

    - **Server**: Select **ArcSight**
    - **Host**: The ArcSight server address
    - **Port**: The ArcSight server port
    - **Timezone**: The timezone of the ArcSight server

1. Select **Save** to save your forwarding rule.

## Next steps

For more information, see:

- [Integrations with partner services](../integrate-overview.md)
- [Forward alert information](../how-to-forward-alert-information-to-partners.md)
- [Manage individual sensors](../how-to-manage-individual-sensors.md)

