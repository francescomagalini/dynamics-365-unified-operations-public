---
title: Enable warehousing telemetry with Application Insights
description: Learn how to set up Microsoft Dynamics 365 Supply Chain Management to send warehousing telemetry data to Application Insights.
author: Mirzaab
ms.author: mirzaab
ms.topic: how-to
ms.date: 11/29/2024
ms.custom: bap-template
ms.reviewer: kamaybac
ms.search.form: SysIntParameters
---

# Enable warehousing telemetry with Application Insights

[!include [banner](../includes/banner.md)]

This article describes how to set up Microsoft Dynamics 365 Supply Chain Management to send warehousing telemetry data to Application Insights.

## Turn the telemetry feature on or off for your system

To use this feature, it must be turned on for your system. As of Supply Chain Management version 10.0.43, it's turned on by default. Admins can turn this functionality on or off by searching for the *Monitoring and telemetry* feature in the [**Feature management** workspace](../../fin-ops-core/fin-ops/get-started/feature-management/feature-management-overview.md).

## Set up Application Insights

Start by setting up Application Insights on your Azure subscription.

1. If you don't already have a subscription to [Azure](https://azure.microsoft.com/), get one.

    > [!NOTE]
    > You can set up the Application Insights resource on any Azure tenant that can be accessed by your system. For example, you might set up Application Insights on a tenant that belongs to your Microsoft partner. In this case, your Microsoft partner will be able to analyze your telemetry data even if they don't have access to your Azure tenant.

1. Sign in to the [Azure portal](https://portal.azure.com/) for the account where you want to install Application Insights.
1. Create an Application Insights resource by following the instructions in [Create an Application Insights resource](/azure/azure-monitor/app/create-new-resource).
1. Keep a copy of the **Instrumentation key** or **Connection string** value for your Application Insights resource. (For more information, see [Create an Application Insights resource](/azure/azure-monitor/app/create-new-resource).) You'll need this value later, when you set up Supply Chain Management to submit the data.

## Set up your apps to send telemetry data to Application Insights

After you've set up Application Insights and have a copy of its instrumentation key, you're ready to enable Supply Chain Management to send telemetry data.

1. Sign in to Supply Chain Management as a user who has system admin privileges.
1. Go to **System administration \> Setup \> Monitoring and telemetry parameters**.
1. On the Configure tab, choose which types of telemetry you'd like to capture. Only the selected types are sent to Application Insights. Of the options listed, only the following are relevant for warehousing telemetry:

    - **User sessions (custom events)** – This must be enabled to capture warehouse events. You should set this option to *Yes*.
    - **Warehouse events** – Specify whether you want to send warehousing telemetry data to Application Insights. You should set this option to *Yes*.

1. On the **Environments** tab, identify the environment mode (*Development*, *Test*, and *Production*) of each environment that you want to send telemetry from. Use the **New** and **Delete** buttons to add and remove rows as needed. You can create as many rows as you want, but we recommend that you create no more than one for each **Environment mode** value (if more than one environment ID is mapped to the same mode, the system selects an ID at random). Make the following settings for each row:

    - **LCS Environment ID** – Enter the ID of the Microsoft Dynamics Lifecycle Services environment that you want to send telemetry data from. To find this ID, [sign in to Lifecycle Services](https://lcs.dynamics.com/Logon/Index), and open the environment details page for your environment. In the **Environment Details** section, look for the **Environment ID** field.
    - **Environment mode** – Select the mode of your selected environment.

1. On the **Application Insights registry** tab, map each environment mode that you use to a target Application Insights connection string or instrumentation key. If a database is copied from one environment to another, the mode will be auto-detected and fail over to the new target endpoint. Environments that aren't mapped default to the *Development* mode. Use the **New** and **Delete** buttons to add and remove rows as needed. You can create up to three rows here (one for each **Environment mode** value). Make the following settings for each row:

    - **Environment mode** – Specify the mode you want to map.
    - **Connection string** or **Instrumentation key** – Enter the value that you copied when you set up Application Insights in Azure.

    > [!NOTE]
    > You can use the same instrumentation key for different environment modes.

1. On the Action Pane, select **Save** to save your settings.

## Pricing

Application Insights is billed based on the volume of telemetry data that your application sends (data ingestion) and the length of time that you want data to be available (data retention). For up-to-date information about pricing, see [Azure Monitor pricing](https://azure.microsoft.com/pricing/details/monitor/).

## Next steps

- [Monitor Warehouse Management usage and performance](application-insights-monitor-usage-performance.md)
