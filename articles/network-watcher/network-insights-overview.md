---
title: Azure Monitor Network Insights
description: An overview of Azure Monitor Network Insights, which provides a comprehensive view of health and metrics for all deployed network resources without any configuration.
ms.topic: conceptual
ms.service: network-watcher
author: halkazwini
ms.author: halkazwini
ms.date: 09/28/2022
ms.reviewer: shijain
ms.custom: subject-monitoring, ignite-2022
---

# Azure Monitor Network Insights

Azure Monitor Network Insights provides a comprehensive and visual representation through [topologies](network-insights-topology.md), of [health](../service-health/resource-health-checks-resource-types.md) and [metrics](../azure-monitor/essentials/metrics-supported.md) for all deployed network resources, without requiring  any configuration. It also provides access to network monitoring capabilities like [Connection Monitor](../network-watcher/connection-monitor-overview.md), [flow logging for network security groups (NSGs)](../network-watcher/network-watcher-nsg-flow-logging-overview.md), and [Traffic Analytics](../network-watcher/traffic-analytics.md). And it provides other network [diagnostic](../network-watcher/network-watcher-monitoring-overview.md#diagnostics) features.

Azure Monitor Network Insights is structured around these key components of monitoring:
- [Topology](#topology)
- [Network health and metrics](#networkhealth)
- [Connectivity](#connectivity)
- [Traffic](#traffic)
- [Diagnostic Toolkit](#diagnostictoolkit)

## Topology

[Topology](network-insights-topology.md) helps you visualize how a resource is configured. It provides a graphic representation of the entire hybrid network for understanding network configuration. Topology is a unified visualization tool for resource inventory and troubleshooting.

It provides an interactive interface to view resources and their relationships in Azure, spanning across multiple subscriptions, resource groups, and locations. You can also drill down to the basic unit of each topology and view the resource view diagram of each unit. 

## <a name="networkhealth"></a>Network health and metrics

The Azure Monitor Network Insights **Overview** page provides an easy way to visualize the inventory of your networking resources, together with resource health and alerts. It's divided into four key functional areas: search and filtering, resource health and metrics, alerts, and resource view.

### Search and filtering
You can customize the resource health and alerts view by using filters like **Subscription**, **Resource Group**, and **Type**.

You can use the search box to search for resources and their associated resources. For example, a public IP is associated with an application gateway. A search for the public IP's DNS name will return both the public IP and the associated application gateway:

[![Screenshot that shows Azure Monitor Network Insights search results.](media/network-insights-overview/search.png)](media/network-insights-overview/search.png#lightbox)

### Resource health and metrics
In the following example, each tile represents a resource type. The tile displays the number of instances of that resource type deployed across all selected subscriptions. It also displays the health status of the resource. In this example, there are 105 ER and VPN connections deployed. 103 are healthy, and 2 are unavailable.

![Screenshot that shows resource health and metrics in Azure Monitor Network Insights.](media/network-insights-overview/resource-health.png)

If you select the unavailable ER and VPN connections, you'll see a metric view: 

![Screenshot that shows the metric view in Azure Monitor Network Insights.](media/network-insights-overview/metric-view.png)

You can select any item in the grid view. Select the icon in the **Health** column to get resource health for that connection. Select the value in the **Alert** column to go to the alerts and metrics page for the connection. 

### Alerts
The **Alert** box on the right side of the page provides a view of all alerts generated for the selected resources across all subscriptions. Select the alert counts to go to a detailed alerts page.

### Resource view
The Resource view helps you visualize how a resource is configured. The Resource view is currently available for Azure Application Gateway, Azure Virtual WAN, and Azure Load Balancer. For example, for Application Gateway, you can access the resource view by selecting the Application Gateway resource name in the metrics grid view. You can do the same thing for Virtual WAN and Load Balancer.

![Sreenshot that shows Application Gateway view in Azure Monitor Network Insights.](media/network-insights-overview/application-gateway.png)

The resource view for Application Gateway provides a simplified view of how the front-end IPs are connected to the listeners, rules, and backend pool. The connecting lines are color coded and provide additional details based on the backend pool health. The view also provides a detailed view of Application Gateway metrics and metrics for all related backend pools, like Virtual Machine Scale Sets and VM instances.

[![Screenshot that shows dependency view in Azure Monitor Network Insights.](media/network-insights-overview/dependency-view.png)](media/network-insights-overview/dependency-view.png#lightbox)

The dependency graph provides easy navigation to configuration settings. Right-click a backend pool to access other information. For example, if the backend pool is a VM, you can directly access VM Insights and Azure Network Watcher connection troubleshooting to identify connectivity issues:

![Screenshot that shows the dependency view menu in Azure Monitor Network Insights.](media/network-insights-overview/dependency-view-menu.png)

The search and filter bar on the resource view provides an easy way to search through the graph. For example, if you search for **AppGWTestRule** in the previous example, the view will scale down to all nodes connected via AppGWTestRule:

![Screenshot that shows an example of a search in Azure Monitor Network Insights.](media/network-insights-overview/search-example.png)

Various filters help you scale down to a specific path and state. For example, select only **Unhealthy** from the **Health status** list to show all edges for which the state is unhealthy.

Select **View detailed metrics** to open a preconfigured workbook that provides detailed metrics for the application gateway, all backend pool resources, and front-end IPs. 

## <a name="connectivity"></a>Connectivity

The **Connectivity** tab provides an easy way to visualize all tests configured via [Connection Monitor](../network-watcher/connection-monitor-overview.md) and Connection Monitor (classic) for the selected set of subscriptions.

![Screenshot that shows the Connectivity tab in Azure Monitor Network Insights.](media/network-insights-overview/azure-monitor-for-networks-connectivity-tab.png)

Tests are grouped by **Sources** and **Destinations** tiles and display the reachability status for each test. Reachable settings provide easy access to configurations for your reachability criteria, based on checks failed (%) and RTT (ms). After you set the values, the status for each test updates based on the selection criteria.

[![Screenshot that shows connectivity tests in Azure Monitor Network Insights.](media/network-insights-overview/azure-monitor-for-networks-connectivity-tests.png)](media/network-insights-overview/azure-monitor-for-networks-connectivity-tests.png#lightbox)

You can select any source or destination tile to open a metric view:

[![Screenshot that shows connectivity metrics in Azure Monitor Network Insights.](media/network-insights-overview/azure-monitor-for-networks-connectivity-metrics.png)](media/network-insights-overview/azure-monitor-for-networks-connectivity-metrics.png#lightbox)

You can select any item in the grid view. Select the icon in the **Reachability** column to go to the Connection Monitor portal page and view the hop-by-hop topology and connectivity affecting issues identified. Select the value in the **Alert** column to go to alerts. Select the graphs in the **Checks Failed Percent** and **Round-Trip Time (ms)** columns to go to the metrics page for the selected connection monitor.

The **Alert** box on the right side of the page provides a view of all alerts generated for the connectivity tests configured across all subscriptions. Select the alert counts to go to a detailed alerts page.

## <a name="traffic"></a>Traffic
The **Traffic** tab provides access to all NSGs configured for [NSG flow logs](network-watcher-nsg-flow-logging-overview.md) and [Traffic Analytics](../network-watcher/traffic-analytics.md) for the selected set of subscriptions, grouped by location. The search functionality provided on this tab enables you to identify the NSGs configured for the searched IP address. You can search for any IP address in your environment. The tiled regional view will display all NSGs along with the NSG flow logs and Traffic Analytics configuration status.

[![Screenshot that shows the Traffic tab in Azure Monitor Network Insights.](media/network-insights-overview/azure-monitor-for-networks-traffic-view.png)](media/network-insights-overview/azure-monitor-for-networks-traffic-view.png#lightbox)

If you select any region tile, a grid view appears. The grid provides NSG flow logs and Traffic Analytics in a view that's easy to read and configure:  

[![Screenshot that shows the traffic region view in Azure Monitor Network Insights.](media/network-insights-overview/azure-monitor-for-networks-traffic-region-view.png)](media/network-insights-overview/azure-monitor-for-networks-traffic-region-view.png#lightbox)

You can select any item in the grid view. Select the icon in the **Flowlog Configuration Status** column to edit the NSG flow log and Traffic Analytics configuration. Select the value in the **Alert** column to go to the traffic alerts configured for the selected NSG. Similarly, you can go to the Traffic Analytics view by selecting the **Traffic Analytics Workspace**.  

The **Alert** box on the right side of the page provides a view of all Traffic Analytics workspace-based alerts across all subscriptions. Select the alert counts to go to a detailed alerts page.

## <a name="diagnostictoolkit"></a> Diagnostic Toolkit
Diagnostic Toolkit provides access to all the diagnostic features available for troubleshooting the network. You can use this drop-down list to access features like [packet capture](../network-watcher/network-watcher-packet-capture-overview.md), [VPN troubleshooting](../network-watcher/network-watcher-troubleshoot-overview.md), [connection troubleshooting](../network-watcher/network-watcher-connectivity-overview.md), [next hop](../network-watcher/network-watcher-next-hop-overview.md), and [IP flow verify](../network-watcher/network-watcher-ip-flow-verify-overview.md):

![Screenshot that shows the Diagnostic Toolkit tab.](media/network-insights-overview/azure-monitor-for-networks-diagnostic-toolkit.png)

## Availability of resources 

By default, all networking resources are visible in Network Insights. Customers can select the resource type for viewing resource health and metrics (if available), subscription details, location, etc. A subset of networking resources has been _Onboarded_. For Onboarded resources, customers have access to a resource specific topology view and a built-in metrics workbook. These out-of-the-box experiences make it easier to explore resource metrics and troubleshoot issues.  

Resources that have been onboarded are: 
- Application Gateway
- Azure ExpressRoute
- Azure Firewall
- Azure Private Link
- Load Balancer
- Local Network Gateway
- Network Interface
- Network Security Groups
- Public IP addresses
- Route Table / UDR
- Traffic Manager
- Virtual Network
- Virtual Network NAT
- Virtual WAN
- ER/VPN Gateway
- Virtual Hub

## Next steps

- Learn more about network monitoring: [What is Azure Network Watcher?](../network-watcher/network-watcher-monitoring-overview.md).
- Learn the scenarios workbooks are designed to support, how to create reports and customize existing reports, and more: [Create interactive reports with Azure Monitor workbooks](../azure-monitor/visualize/workbooks-overview.md).
