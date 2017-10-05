---
title: "Оценка приложений Service Fabric в Azure Log Analytics с помощью PowerShell | Документация Майкрософт"
description: "Решение Service Fabric в Log Analytics можно использовать для оценки риска и работоспособности приложений, микрослужб, узлов и кластеров Service Fabric с помощью PowerShell."
services: log-analytics
documentationcenter: 
author: niniikhena
manager: jochan
editor: 
ms.assetid: 2047b3fa-96b1-4230-af5d-a4c331d973ce
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/06/2017
ms.author: nini
ms.openlocfilehash: ca86787e344aa5e9e68934dee6e9e83aeb4cc340
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="assess-azure-service-fabric-applications-and-micro-services-with-powershell"></a><span data-ttu-id="b3475-103">Оценка приложений и микрослужб Azure Service Fabric с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3475-103">Assess Azure Service Fabric applications and micro-services with PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="b3475-104">Диспетчер ресурсов</span><span class="sxs-lookup"><span data-stu-id="b3475-104">Resource Manager</span></span>](log-analytics-service-fabric-azure-resource-manager.md)
> * [<span data-ttu-id="b3475-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3475-105">PowerShell</span></span>](log-analytics-service-fabric.md)
>
>


![Символ Service Fabric](./media/log-analytics-service-fabric/service-fabric-assessment-symbol.png)

<span data-ttu-id="b3475-107">В этой статье описывается, как с помощью решений Service Fabric в Log Analytics определять и устранять неполадки в кластере Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-107">This article describes how to use the Service Fabric solution in Log Analytics to help identify and troubleshoot issues across your Service Fabric cluster.</span></span> <span data-ttu-id="b3475-108">Это поможет наблюдать за работой узлов Service Fabric и выполнением приложений и микрослужб.</span><span class="sxs-lookup"><span data-stu-id="b3475-108">It helps you see how your Service Fabric nodes are performing and how your applications and micro-services are running.</span></span>

<span data-ttu-id="b3475-109">Решение Service Fabric использует данные системы диагностики Azure, полученные от виртуальных машин Service Fabric, собирая эти данные из таблиц Azure WAD.</span><span class="sxs-lookup"><span data-stu-id="b3475-109">The Service Fabric solution uses Azure Diagnostics data from your Service Fabric VMs, by collecting this data from your Azure WAD tables.</span></span> <span data-ttu-id="b3475-110">Затем Log Analytics считывает следующие события платформы Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="b3475-110">Log Analytics then reads the following Service Fabric framework events:</span></span>

- <span data-ttu-id="b3475-111">**события надежных служб**;</span><span class="sxs-lookup"><span data-stu-id="b3475-111">**Reliable Service Events**</span></span>
- <span data-ttu-id="b3475-112">**события субъектов**;</span><span class="sxs-lookup"><span data-stu-id="b3475-112">**Actor Events**</span></span>
- <span data-ttu-id="b3475-113">**операционные события**;</span><span class="sxs-lookup"><span data-stu-id="b3475-113">**Operational Events**</span></span>
- <span data-ttu-id="b3475-114">**пользовательские события трассировки событий Windows**.</span><span class="sxs-lookup"><span data-stu-id="b3475-114">**Custom ETW events**</span></span>

<span data-ttu-id="b3475-115">На панели мониторинга решения Service Fabric отображаются важные проблемы и соответствующие события в среде Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-115">The Service Fabric solution dashboard shows you notable issues and relevant events in your Service Fabric environment.</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="b3475-116">Установка и настройка решения</span><span class="sxs-lookup"><span data-stu-id="b3475-116">Installing and configuring the solution</span></span>
<span data-ttu-id="b3475-117">Для установки и настройки решения выполните три простых шага, описанных ниже.</span><span class="sxs-lookup"><span data-stu-id="b3475-117">Follow these three easy steps to install and configure the solution:</span></span>

1. <span data-ttu-id="b3475-118">Привяжите к своей рабочей области подписку Azure, которая использовалась для создания всех ресурсов кластера, включая учетные записи хранения.</span><span class="sxs-lookup"><span data-stu-id="b3475-118">Associate the Azure subscription that you used to create all cluster resources, including storage accounts, with your workspace.</span></span> <span data-ttu-id="b3475-119">Сведения о создании рабочей области Log Analytics см. в статье [Начало работы с Log Analytics](log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="b3475-119">See [Get started with Log Analytics](log-analytics-get-started.md) for information about creating a Log Analytics workspace.</span></span>
2. <span data-ttu-id="b3475-120">Настройте Log Analytics для сбора и просмотра журналов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-120">Configure Log Analytics to collect and view Service Fabric logs.</span></span>
3. <span data-ttu-id="b3475-121">Включите решение Service Fabric в рабочей области.</span><span class="sxs-lookup"><span data-stu-id="b3475-121">Enable the Service Fabric solution in your workspace.</span></span>

## <a name="configure-log-analytics-to-collect-and-view-service-fabric-logs"></a><span data-ttu-id="b3475-122">Настройка Log Analytics для сбора и просмотра журналов Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b3475-122">Configure Log Analytics to collect and view Service Fabric logs</span></span>
<span data-ttu-id="b3475-123">В этом разделе описана настройка Log Analytics для получения журналов Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-123">In this section, you learn how to configure Log Analytics to retrieve Service Fabric logs.</span></span> <span data-ttu-id="b3475-124">Журналы дают возможность просматривать, анализировать и устранять неполадки в кластере, а также в приложениях и службах, работающих в этом кластере, с помощью портала OMS.</span><span class="sxs-lookup"><span data-stu-id="b3475-124">The logs allow you to view, analyze, and troubleshoot issues in your cluster or in the applications and services running in that cluster, using the OMS portal.</span></span>

> [!NOTE]
> <span data-ttu-id="b3475-125">Настройте расширение системы диагностики Azure для передачи журналов для таблиц хранилища.</span><span class="sxs-lookup"><span data-stu-id="b3475-125">Configure the Azure Diagnostics extension to upload the logs for storage tables.</span></span> <span data-ttu-id="b3475-126">Таблицы должны соответствовать журналам, которые ищет Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3475-126">The tables must match what Log Analytics looks for.</span></span> <span data-ttu-id="b3475-127">Дополнительные сведения см. в статье [Сбор журналов с помощью системы диагностики Azure](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span><span class="sxs-lookup"><span data-stu-id="b3475-127">For more information, see [How to collect logs with Azure Diagnostics](../service-fabric/service-fabric-diagnostics-how-to-setup-wad.md).</span></span> <span data-ttu-id="b3475-128">На примерах настроек конфигурации в этой статье вы увидите, какими должны быть имена таблиц хранилища.</span><span class="sxs-lookup"><span data-stu-id="b3475-128">The configuration settings examples in this article show you what the names of the storage tables should be.</span></span> <span data-ttu-id="b3475-129">После настройки диагностики в кластере и отправки журналов в учетную запись хранения можно перейти к настройке Log Analytics для сбора этих журналов.</span><span class="sxs-lookup"><span data-stu-id="b3475-129">Once Diagnostics is set up on the cluster and is uploading logs to a storage account, the next step is to configure Log Analytics to collect these logs.</span></span>
>
>

<span data-ttu-id="b3475-130">Обновите раздел **EtwEventSourceProviderConfiguration** в файле **template.json**, добавив записи для нового канала EventSources, до обновления конфигурации, запустив файл **deploy.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b3475-130">Ensure that you update the **EtwEventSourceProviderConfiguration** section in the **template.json** file to add entries for the new EventSources before you apply the configuration update by running **deploy.ps1**.</span></span> <span data-ttu-id="b3475-131">Таблица для отправки совпадает с таблицей (ETWEventTable).</span><span class="sxs-lookup"><span data-stu-id="b3475-131">The table for upload is the same as (ETWEventTable).</span></span> <span data-ttu-id="b3475-132">На данный момент Log Analytics может только считывать данные трассировки событий Windows приложения из таблицы *WADETWEventTable*.</span><span class="sxs-lookup"><span data-stu-id="b3475-132">At the moment, Log Analytics can only read application ETW events from the *WADETWEventTable* table.</span></span>

<span data-ttu-id="b3475-133">Для выполнения некоторых операций в этом разделе используются следующие инструменты:</span><span class="sxs-lookup"><span data-stu-id="b3475-133">The following tools are used to perform some of the operations in this section:</span></span>

* <span data-ttu-id="b3475-134">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b3475-134">Azure PowerShell</span></span>
* [<span data-ttu-id="b3475-135">Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="b3475-135">Operations Management Suite</span></span>](http://www.microsoft.com/oms)

### <a name="configure-a-log-analytics-workspace-to-show-the-cluster-logs"></a><span data-ttu-id="b3475-136">Настройка рабочей области Log Analytics для отображения журналов кластера</span><span class="sxs-lookup"><span data-stu-id="b3475-136">Configure a Log Analytics workspace to show the cluster logs</span></span>

<span data-ttu-id="b3475-137">После создания рабочей области Log Analytics настройте ее для извлечения журналов из таблиц службы хранилища Azure.</span><span class="sxs-lookup"><span data-stu-id="b3475-137">After you create a Log Analytics workspace, configure the workspace to pull logs from the Azure storage tables.</span></span> <span data-ttu-id="b3475-138">После этого выполните следующий сценарий PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b3475-138">Then, run the following PowerShell script:</span></span>

```
<#
    This script will configure an Operations Management Suite workspace (previously called an Operational Insights workspace) to read Diagnostics from an Azure Storage account.
    It will enable all supported data types (currently Service Fabric Events, ETW Events and IIS Logs).
    It supports Resource Manager storage accounts.
    If you have more than one Azure Subscription, you will be prompted for the subscription to configure.
    If you have more than one Log Analytics workspace you will be prompted for the workspace to configure.
    It will then look through your Service Fabric clusters, and configure your Log Analytics workspace to read Diagnostics from storage accounts that are connected to that cluster and have diagnostics enabled.
#>

try
{
    Get-AzureRMContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Add-AzureRmAccount
}

$validTables = "WADServiceFabric*EventTable", "WADETWEventTable"
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"

            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.Name + " (" + $subscription.Id + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.Id
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  

    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found. `n"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
             Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}

function Check-ETWProviderLogging {
     param(
     [string]$id,
     [string]$provider,
     [string]$expectedTable,
     [string]$table
    )       
         Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
         if ( ($table -eq $null) -or ($table -eq ""))  
         {
             Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
         }  
         elseif ( $table -ne $expectedTable )
         {
             Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
         }  
         else
         {
             Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
         }
 }

function Check-ServiceFabricScaleSetDiagnostics {
     param(
          [psobject]$scaleSetDiagnostics
   )
     $storageAccountsFound = @()
     Write-Verbose ("Checking " + $scaleSetDiagnostics)
     $sfReliableActorTable = $null
     $sfReliableServiceTable = $null
     $sfOperationalTable = $null

     Write-Debug $scaleSetDiagnostics
     $serviceFabricProviderList = ""
     $etwManifestProviderList = ""

     if ( $scaleSetDiagnostics.xmlCfg )  
      {
             Write-Debug ("Found XMLcfg")
             $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
             Write-Debug $xmlCfg
             $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                 
             $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
             $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
      } elseif ($scaleSetDiagnostics.WadCfg )  
     {
         Write-Debug ("Found WADcfg")
         Write-Debug $scaleSetDiagnostics.WadCfg
         $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
         $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
     } else
     {
         Write-Error "Unable to parse Azure Diagnostics setting for $id"
             Write-Warning ("$id does not have diagnostics enabled")
     }
     foreach ($provider in $serviceFabricProviderList)  
     {
         Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
         {
             $sfReliableActorTable = $provider.DefaultEvents.eventDestination  
         } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")  
         {  
             $sfReliableServiceTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }
     foreach ($provider in $etwManifestProviderList)
     {
         Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
         if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
         {
             $sfOperationalTable = $provider.DefaultEvents.eventDestination  
         } else  
         {
             Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
         }
     }

     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
     Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
     Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

     Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)
     $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
     return ($storageAccountsFound)
 }

function Select-StorageAccount {
    $allResources = Get-AzureRmResource #pulls in all resources
    $serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"}) #pulls in all service fabric clusters in the resource
    $storageAccountList = @()
    foreach($cluster in $serviceFabricClusters) {
        Write-Host("Checking cluster: " + $cluster.Name)
         $scaleSet = $allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)})

         foreach($set in $scaleSet) {
             $resource = Get-AzureRmResource -ResourceId $set.ResourceId
             $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions

             foreach($ext in $extensions) {
                 if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                     $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
                 }
             }
          }

         $storageAccountsToCheck = $allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)})

         if ($storageAccountsToCheck.Count -eq "0") {
                Write-Error "No storage accounts found"
           }
           else {
                    foreach ($storageAccount in $storageAccountsToCheck) {
                        Write-Host("Checking Storage Account: " + $storageAccount.Name)
                        $insightsName = $storageAccount.Name + $workspace.Name
                        $existingConfig = ""
                        try
                            {
                                $existingConfig = Get-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -ErrorAction Stop
                            }
                        catch
                            {
                                # HTTP Not Found is returned if the storage insight doesn't exist
                            }
                        if ($existingConfig) {                         
                                  [array]$Tables = $existingConfig.Tables
                                   foreach($table in $validTables) {
                                         if($Tables -notcontains $table) {
                                               $Tables += $table
                                               $dirty = $true;
                                               Write-Host "Adding Table: $table";
                                         }
                                         else {
                                               Write-Host "$table is already configured.`n";
                                             }
                                      }
                                      # If any of the tables from the table list are not already monitored, then we add them
                                   if($dirty -eq $true) {
                                           Set-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -Tables $Tables
                                           Write-Host "Updating Storage Insight. `n"
                                    }
                                    else {
                                           Write-Host "Storage Insight already updated."
                                  }
                          }
                     else {
                            $key = (Get-AzureRmStorageAccountKey -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.Name)[0].Value
                           New-AzureRmOperationalInsightsStorageInsight -Workspace $workspace -Name $insightsName -StorageAccountResourceId $storageAccount.ResourceId -StorageAccountKey $key -Tables $validTables
                            Write-Host "New Azure Storage Insight Configured. `n"
                           }
                    }
             }
      }
      return
     }

$subscription = Select-Subscription
$subscriptionId = $subscription.SubscriptionId
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
$storageAccount = Select-StorageAccount
```

<span data-ttu-id="b3475-139">Настроив рабочую область Log Analytics для чтения данных из таблиц Azure в своей учетной записи хранения, войдите на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b3475-139">After you've configured the Log Analytics workspace to read from the Azure tables in your storage account, log in to the Azure portal.</span></span> <span data-ttu-id="b3475-140">В разделе **Все ресурсы** выберите рабочую область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3475-140">Select the Log Analytics workspace from **All Resources**.</span></span> <span data-ttu-id="b3475-141">Будет отображено количество журналов учетной записи хранения, подключенной к рабочей области.</span><span class="sxs-lookup"><span data-stu-id="b3475-141">The number of storage account logs connected to the workspace is displayed.</span></span> <span data-ttu-id="b3475-142">Выберите элемент **Журналы учетной записи хранения**.</span><span class="sxs-lookup"><span data-stu-id="b3475-142">Select the **Storage account logs** tile.</span></span> <span data-ttu-id="b3475-143">Просмотрите список журналов учетной записи хранения, чтобы убедиться, что ваша учетная запись хранения подключена к нужной рабочей области.</span><span class="sxs-lookup"><span data-stu-id="b3475-143">Review the list of storage account logs to verify that your storage account is connected to the correct workspace.</span></span>

![Журналы учетной записи хранения](./media/log-analytics-service-fabric/sf1.png)

## <a name="enable-the-service-fabric-solution"></a><span data-ttu-id="b3475-145">Включение решения Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b3475-145">Enable the Service Fabric solution</span></span>
<span data-ttu-id="b3475-146">Используйте следующий сценарий, чтобы добавить решение в рабочую область Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="b3475-146">Use the following script to add the solution to your Log Analytics workspace.</span></span> <span data-ttu-id="b3475-147">Запустите сценарий в PowerShell, используя подписку Azure, связанную с рабочей областью Log Analytics, в которой нужно включить решение Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-147">Run the script in PowerShell, using the Azure subscription that is associated with the Log Analytics workspace that you want to enable the Service Fabric solution in.</span></span>

```
function Select-Subscription {
      $subscription = ""
      $allSubscriptions = Get-AzureRmSubscription
      switch ($allSubscriptions.Count) {
             0 {Write-Error "No Operations Management Suite workspaces found"}
             1 {return $allSubscriptions}
        default {
            $uiPrompt = "Enter the number corresponding to the Azure subscription you would like to work with.`n"
            $count = 1
            foreach ($subscription in $allSubscriptions) {
                $uiPrompt += "$count. " + $subscription.SubscriptionName + " (" + $subscription.SubscriptionId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $subscription = $allSubscriptions[$answer]
             Write-Host $subscription.SubscriptionId
        }  
    }
    return $subscription
}

function Select-Workspace {
    $workspace = ""
    $allWorkspaces = Get-AzureRmOperationalInsightsWorkspace  
    switch ($allWorkspaces.Count) {
        0 {Write-Error "No Operations Management Suite workspaces found"}
        1 {return $allWorkspaces}
        default {
            $uiPrompt = "Enter the number corresponding to the workspace you want to configure.`n"
            $count = 1
            foreach ($workspace in $allWorkspaces) {
                $uiPrompt += "$count. " + $workspace.Name + " (" + $workspace.CustomerId + ")`n"
                $count++
            }
            $answer = (Read-Host -Prompt $uiPrompt) - 1
            $workspace = $allWorkspaces[$answer]
                           Write-Host $workspace.WorkspaceName
        }  
    }
    return $workspace
}
$subscription = Select-Subscription
$subscriptionId = $subscription.Id
$subscription = Select-AzureRmSubscription -SubscriptionId $subscriptionId
$workspace = Select-Workspace
Set-AzureRmOperationalInsightsIntelligencePack -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name -IntelligencePackName "ServiceFabric" -Enabled $true
```

<span data-ttu-id="b3475-148">После включения решения на страницу *Обзор* Log Analytics будет добавлен элемент "Service Fabric".</span><span class="sxs-lookup"><span data-stu-id="b3475-148">After you enable the solution, the Service Fabric tile is added to your Log Analytics *Overview* page.</span></span> <span data-ttu-id="b3475-149">На странице отображается представление важных проблем, таких как сбои runAsync и отмены операций, произошедшие за последние 24 часа.</span><span class="sxs-lookup"><span data-stu-id="b3475-149">The page shows a view of notable issues such as runAsync failures and cancellations that occurred in the last 24 hours.</span></span>

![Плитка Service Fabric](./media/log-analytics-service-fabric/sf2.png)

### <a name="view-service-fabric-events"></a><span data-ttu-id="b3475-151">Просмотр событий Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b3475-151">View Service Fabric events</span></span>
<span data-ttu-id="b3475-152">Щелкните плитку **Service Fabric**, чтобы открыть панель мониторинга Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-152">Click the **Service Fabric** tile to open the Service Fabric dashboard.</span></span> <span data-ttu-id="b3475-153">Панель мониторинга содержит столбцы, перечисленные в приведенной ниже таблице.</span><span class="sxs-lookup"><span data-stu-id="b3475-153">The dashboard includes the columns in the table that follows.</span></span> <span data-ttu-id="b3475-154">В каждом столбце отображены 10 наиболее распространенных событий, соответствующих указанным для столбца критериям, на выбранном диапазоне времени.</span><span class="sxs-lookup"><span data-stu-id="b3475-154">Each column lists the top 10 events by count matching that column's criteria for the specified time range.</span></span> <span data-ttu-id="b3475-155">Можно выполнить поиск по журналам, выводящий весь список, щелкнув элемент **Показать все** в правой нижней части каждого столбца или заголовок этого столбца.</span><span class="sxs-lookup"><span data-stu-id="b3475-155">You can run a log search that provides the entire list by clicking **See all** at the right bottom of each column, or by clicking the column header.</span></span>

| <span data-ttu-id="b3475-156">**Событие Service Fabric**</span><span class="sxs-lookup"><span data-stu-id="b3475-156">**Service Fabric event**</span></span> | <span data-ttu-id="b3475-157">**description**</span><span class="sxs-lookup"><span data-stu-id="b3475-157">**description**</span></span> |
| --- | --- |
| <span data-ttu-id="b3475-158">Важные проблемы</span><span class="sxs-lookup"><span data-stu-id="b3475-158">Notable Issues</span></span> | <span data-ttu-id="b3475-159">Отображаются проблемы, в том числе события RunAsyncFailure, RunAsynCancellation и NodeDown.</span><span class="sxs-lookup"><span data-stu-id="b3475-159">Displays issues including RunAsyncFailures, RunAsynCancellations, and Node Downs.</span></span> |
| <span data-ttu-id="b3475-160">Операционные события</span><span class="sxs-lookup"><span data-stu-id="b3475-160">Operational Events</span></span> | <span data-ttu-id="b3475-161">Отображаются важные операционные события, включая обновление и развертывание приложений.</span><span class="sxs-lookup"><span data-stu-id="b3475-161">Displays notable operational events including application upgrade and deployments.</span></span> |
| <span data-ttu-id="b3475-162">События надежных служб</span><span class="sxs-lookup"><span data-stu-id="b3475-162">Reliable Service Events</span></span> | <span data-ttu-id="b3475-163">Отображаются важные события надежных служб, в том числе события RunAsyncInvocation.</span><span class="sxs-lookup"><span data-stu-id="b3475-163">Displays notable reliable service events including  Runasyncinvocations.</span></span> |
| <span data-ttu-id="b3475-164">События субъектов</span><span class="sxs-lookup"><span data-stu-id="b3475-164">Actor Events</span></span> | <span data-ttu-id="b3475-165">Отображаются важные события субъектов, создаваемые микрослужбами.</span><span class="sxs-lookup"><span data-stu-id="b3475-165">Displays notable actor events generated by your micro-services.</span></span> <span data-ttu-id="b3475-166">К этим событиям относятся исключения, порожденные методом субъекта, активация и деактивация субъектов и т. д.</span><span class="sxs-lookup"><span data-stu-id="b3475-166">Events include exceptions thrown by an actor method, actor activations and deactivations, and so on.</span></span> |
| <span data-ttu-id="b3475-167">События приложений</span><span class="sxs-lookup"><span data-stu-id="b3475-167">Application Events</span></span> | <span data-ttu-id="b3475-168">Отображаются все пользовательские события трассировки событий Windows, создаваемые приложениями.</span><span class="sxs-lookup"><span data-stu-id="b3475-168">Displays all custom ETW events generated by your applications.</span></span> |

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf3.png)

![Панель мониторинга Service Fabric](./media/log-analytics-service-fabric/sf4.png)

<span data-ttu-id="b3475-171">В следующей таблице описаны методы сбора данных, а также приведены сведения о сборе данных для Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="b3475-171">The following table shows data collection methods and other details about how data is collected for Service Fabric:</span></span>

| <span data-ttu-id="b3475-172">платформа</span><span class="sxs-lookup"><span data-stu-id="b3475-172">platform</span></span> | <span data-ttu-id="b3475-173">Direct Agent</span><span class="sxs-lookup"><span data-stu-id="b3475-173">Direct Agent</span></span> | <span data-ttu-id="b3475-174">Агент Operations Manager</span><span class="sxs-lookup"><span data-stu-id="b3475-174">Operations Manager agent</span></span> | <span data-ttu-id="b3475-175">Хранилище Azure</span><span class="sxs-lookup"><span data-stu-id="b3475-175">Azure Storage</span></span> | <span data-ttu-id="b3475-176">Нужен ли Operations Manager?</span><span class="sxs-lookup"><span data-stu-id="b3475-176">Operations Manager required?</span></span> | <span data-ttu-id="b3475-177">Отправка данных агента Operations Manager через группу управления</span><span class="sxs-lookup"><span data-stu-id="b3475-177">Operations Manager agent data sent via management group</span></span> | <span data-ttu-id="b3475-178">частота сбора</span><span class="sxs-lookup"><span data-stu-id="b3475-178">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="b3475-179">Windows</span><span class="sxs-lookup"><span data-stu-id="b3475-179">Windows</span></span> |  |  | <span data-ttu-id="b3475-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="b3475-180">&#8226;</span></span> |  |  |<span data-ttu-id="b3475-181">10 минут</span><span class="sxs-lookup"><span data-stu-id="b3475-181">10 minutes</span></span> |

> [!NOTE]
> <span data-ttu-id="b3475-182">Измените область событий, выбрав **Data based on last seven days** (Данные за последние семь дней) в верхней части панели мониторинга.</span><span class="sxs-lookup"><span data-stu-id="b3475-182">Change the scope of events with **Data based on last seven days** at the top of the dashboard.</span></span> <span data-ttu-id="b3475-183">Кроме того, можно отобразить события, созданные за последние семь дней, один день или шесть часов.</span><span class="sxs-lookup"><span data-stu-id="b3475-183">You can also show events generated within the last seven days, one day, or six hours.</span></span> <span data-ttu-id="b3475-184">Можно также выбрать вариант **Custom** (Другое) и указать диапазон дат.</span><span class="sxs-lookup"><span data-stu-id="b3475-184">Or, you can select **Custom** to specify a custom date range.</span></span>
>
>

## <a name="troubleshoot-your-service-fabric-and-log-analytics-configuration"></a><span data-ttu-id="b3475-185">Устранение неполадок конфигурации Service Fabric и конфигурации Log Analytics</span><span class="sxs-lookup"><span data-stu-id="b3475-185">Troubleshoot your Service Fabric and Log Analytics configuration</span></span>
<span data-ttu-id="b3475-186">Если необходимо проверить конфигурацию Log Analytics, потому что не удается просмотреть данные событий в Log Analytics, используйте приведенный ниже сценарий.</span><span class="sxs-lookup"><span data-stu-id="b3475-186">If you need to verify your Log Analytics configuration because you are unable to view event data in Log Analytics, use the following script.</span></span> <span data-ttu-id="b3475-187">Он выполняет следующие действия:</span><span class="sxs-lookup"><span data-stu-id="b3475-187">It performs the following actions:</span></span>

1. <span data-ttu-id="b3475-188">считывает конфигурацию диагностики Service Fabric;</span><span class="sxs-lookup"><span data-stu-id="b3475-188">Reads your Service Fabric diagnostics configuration</span></span>
2. <span data-ttu-id="b3475-189">проверяет наличие данных, записанных в таблицы;</span><span class="sxs-lookup"><span data-stu-id="b3475-189">Checks for data written into the tables</span></span>
3. <span data-ttu-id="b3475-190">проверяет, настроена ли служба Log Analytics для чтения данных из таблиц.</span><span class="sxs-lookup"><span data-stu-id="b3475-190">Verifies that Log Analytics is configured to read from the tables</span></span>

```
<#
    Verify Service Fabric and Log Analytics configuration
    1. Read Service Fabric diagnostics configuration
    2. Check for data being written into the tables
    3. Verify Log Analytics is configured to read from the tables

    Supported tables:
    WADServiceFabricReliableActorEventTable
    WADServiceFabricReliableServiceEventTable
    WADServiceFabricSystemEventTable
    WADETWEventTable

    Script will write a warning for every misconfiguration detected
    To see items that are correctly configured set $VerbosePreference="Continue"
#>
Param
(
    [Parameter(Mandatory=$true,
    ValueFromPipeline=$true,
    Position=1)]
    [string]$workspaceName
)

$WADtables = @("WADServiceFabricReliableActorEventTable",
               "WADServiceFabricReliableServiceEventTable",
               "WADServiceFabricSystemEventTable",
               "WADETWEventTable"
               )

<#
    Check if OMS Log Analytics is configured to index service fabric events from the specified table
#>

function Check-OMSLogAnalyticsConfiguration {
    param(
    [psobject]$workspace,
    [psobject]$storageAccount,
    [string]$id
    )

    $existingInsights = Get-AzureRmOperationalInsightsStorageInsight -ResourceGroupName $workspace.ResourceGroupName -WorkspaceName $workspace.Name

    if ($existingInsights)
    {
        $currentStorageAccountInsight = $existingInsights.Where({$_.StorageAccountResourceId -eq $storageAccount.ResourceId})

        if ("WADServiceFabric*EventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric actor, service and operational events from " + $storageAccount.Name)
        }
        if ("WADETWEventTable" -in $currentStorageAccountInsight.Tables)
        {
            Write-Verbose ("OMS Log Analytics workspace " + $workspace.Name + " is configured to index service fabric application events from " + $storageAccount.Name)
        } else
        {
            Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + " is not configured to index service fabric application events from " + $storageAccount.Name)
        }
    } else
    {
        Write-Warning ("OMS Log Analytics workspace " + $workspace.Name + "is not configured to read service fabric events from " + $storageAccount.Name)
    }    
}

<#
    Check Azure table storage to confirm there is recent data written by Service Fabric
#>

function Check-TablesForData {
    param(
    [psobject]$storageAccount
    )

    $ctx = (Get-AzureRmStorageAccount -ResourceGroupName $storageAccount.ResourceGroupName -Name $storageAccount.ResourceName).Context

    $createdTables = Get-AzureStorageTable -Context $ctx

    $recently = Get-Date -Format s ((Get-Date).AddMinutes(-20).ToUniversalTime())
    $recently = $recently + "Z"

    foreach ($table in $WADtables)
    {
        if ($table -in $createdTables.Name)
        {
            $tbl = Get-AzureStorageTable -Name $table -Context $ctx
            $query = New-Object Microsoft.WindowsAzure.Storage.Table.TableQuery
            $list = New-Object System.Collections.Generic.List[string]
            $list.Add("RowKey")
            $list.Add("ProviderName")
            $list.Add("Timestamp")
            $query.FilterString = "Timestamp gt datetime'$recently'"
            $query.SelectColumns = $list
            $query.TakeCount = 20
            $entities = $tbl.CloudTable.ExecuteQuery($query)
            Write-Debug $entities
            if ($entities.Count -gt 0)
            {
                Write-Verbose ("Data was written to $table in " + $storageAccount.ResourceName + "after $recently")
            } else
            {
                Write-Warning ("No data after $recently is in  $table in " + $storageAccount.ResourceName)
            }
        } else
        {
            Write-Warning ("$table does not exist in storage account " + $storageAccount.ResourceName)
        }
    }
}

<#
    Check if ETW provider is configured to log events to the expected table storage
#>
function Check-ETWProviderLogging {
    param(
    [string]$id,
    [string]$provider,
    [string]$expectedTable,
    [string]$table
    )      
        Write-Debug ("ID: $id Provider: $provider ExpectedTable $expectedTable ActualTable $table")
        if ( ($table -eq $null) -or ($table -eq ""))
        {
            Write-Warning ("$id No configuration found for $provider. Configure Azure diagnostics to write to $expectedTable.")
        }
        elseif ( $table -ne $expectedTable )
        {
            Write-Warning ("$id $provider events are being written to $table instead of WAD$expectedTable. Events will not be collected by Log Analytics")
        }
        else
        {
            Write-Verbose "$id $provider events are being written to WAD$expectedTable (Correct configuration.)"
        }
}

<#
    Check Azure Diagnostics Configuration for a Service Fabric cluster
#>
function Check-ServiceFabricScaleSetDiagnostics {
    param(
    [psobject]$scaleSetDiagnostics
    )

    $storageAccountsFound = @()
    Write-Verbose ("Checking " + $scaleSetDiagnostics)
    $sfReliableActorTable = $null
    $sfReliableServiceTable = $null
    $sfOperationalTable = $null
    Write-Debug $scaleSetDiagnostics
    $serviceFabricProviderList = ""
    $etwManifestProviderList = ""

    if ( $scaleSetDiagnostics.xmlCfg )
    {
        Write-Debug ("Found XMLcfg")
        $xmlCfg = [System.Text.Encoding]::UTF8.GetString([System.Convert]::FromBase64String($scaleSetDiagnostics.xmlCfg))
        Write-Debug $xmlCfg
        $etwProviders = Select-Xml -Content $xmlCfg -XPath "//EtwProviders"                
        $serviceFabricProviderList = $etwProviders.Node.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $etwProviders.Node.EtwManifestProviderConfiguration
    } elseif ($scaleSetDiagnostics.WadCfg )
    {
        Write-Debug ("Found WADcfg")
        Write-Debug $scaleSetDiagnostics.WadCfg
        $serviceFabricProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwEventSourceProviderConfiguration
        $etwManifestProviderList = $scaleSetDiagnostics.WadCfg.DiagnosticMonitorConfiguration.EtwProviders.EtwManifestProviderConfiguration
    } else
    {
        Write-Error "Unable to parse Azure Diagnostics setting for $id"
        Write-Warning ("$id does not have diagnostics enabled")
    }

    foreach ($provider in $serviceFabricProviderList)
    {
        Write-Debug ("Event Source Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "Microsoft-ServiceFabric-Actors")
        {
            $sfReliableActorTable = $provider.DefaultEvents.eventDestination
        } elseif ($provider.Provider -eq "Microsoft-ServiceFabric-Services")
        {
            $sfReliableServiceTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }
    foreach ($provider in $etwManifestProviderList)
    {
        Write-Debug ("Manifest Provider: " + $provider.Provider + " Destination: " + $provider.DefaultEvents.eventDestination)
        if ($provider.Provider -eq "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8")
        {
            $sfOperationalTable = $provider.DefaultEvents.eventDestination
        } else
        {
            Check-ETWProviderLogging $id $provider.Provider "ETWEventTable" $provider.DefaultEvents.eventDestination
        }
    }

    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Actors" "ServiceFabricReliableActorEventTable" $sfReliableActorTable
    Check-ETWProviderLogging $id "Microsoft-ServiceFabric-Services" "ServiceFabricReliableServiceEventTable" $sfReliableServiceTable
    Check-ETWProviderLogging $id "cbd93bc2-71e5-4566-b3a7-595d8eeca6e8 (System events)" "ServiceFabricSystemEventTable" $sfOperationalTable

    Write-Verbose ("StorageAccount: " + $scaleSetDiagnostics.StorageAccount)

    $storageAccountsFound += ($scaleSetDiagnostics.StorageAccount)
    return ($storageAccountsFound)
}

# This script uses Get-AzureRmVMDiagnosticsExtension and needs a version where -Name is not a required parameter
Import-Module AzureRM.Compute -MinimumVersion 1.2.2

try
{
    Get-AzureRmContext
}
catch [System.Management.Automation.PSInvalidOperationException]
{
    Login-AzureRmAccount
}

$allResources = Get-AzureRmResource

$OMSworkspace = $allResources.Where({($_.ResourceType -eq "Microsoft.OperationalInsights/workspaces") -and ($_.ResourceName -eq $workspaceName)})

if ($OMSworkspace.Name -ne $workspaceName)
{
    Write-Error ("Unable to find Log Analytics Workspace " + $workspaceName)
}

$serviceFabricClusters = $allResources.Where({$_.ResourceType -eq "Microsoft.ServiceFabric/clusters"})
$storageAccountList = @()
foreach($cluster in $serviceFabricClusters) {
    Write-Verbose ("Checking cluster: " + $cluster.Name)
    $scaleSet = ($allResources.Where({($_.ResourceType -eq "Microsoft.Compute/virtualMachineScaleSets") -and ($_.ResourceGroupName -eq $cluster.ResourceGroupName)}))

    foreach($set in $scaleSet) {
        $resource = Get-AzureRmResource -ResourceId $set.ResourceId
        $extensions = $resource.Properties.VirtualMachineProfile.ExtensionProfile.Extensions
        foreach($ext in $extensions) {
            if ($ext.Properties.Publisher -eq "Microsoft.Azure.Diagnostics" -and $ext.Properties.Type -eq "IaaSDiagnostics") {
                $storageAccountList += (Check-ServiceFabricScaleSetDiagnostics $ext.Properties.Settings)
            }
        }
    }
}

$storageAccountList = $storageAccountList | Sort-Object | Get-Unique
$storageAccountsToCheck = ($allResources.Where({($_.ResourceType -eq "Microsoft.Storage/storageAccounts") -and ($_.ResourceName -in $storageAccountList)}))

foreach($storageAccount in $storageAccountsToCheck)
{
    Check-TablesForData $storageAccount
    Check-OMSLogAnalyticsConfiguration $OMSworkspace $storageAccount
}
 ```


## <a name="next-steps"></a><span data-ttu-id="b3475-191">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b3475-191">Next steps</span></span>
* <span data-ttu-id="b3475-192">Подробные сведения о данных событий Service Fabric см. в статье [Поиск по журналам в Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="b3475-192">Use [Log Searches in Log Analytics](log-analytics-log-searches.md) to view detailed Service Fabric event data.</span></span>
