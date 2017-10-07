---
title: "tooLog aaaConnect виртуальных машин Azure Analytics | Документы Microsoft"
description: "Для Windows и Linux виртуальных машин, работающих в Azure, hello рекомендуется способ сбора журналов и является метрики, установив расширение виртуальной Машины Azure Analytics журнала hello. Можно использовать портал Azure hello или hello tooinstall PowerShell анализа журналов расширение виртуальной машины на виртуальных машинах Azure."
services: log-analytics
documentationcenter: 
author: richrundmsft
manager: ewinner
editor: 
ms.assetid: ca39e586-a6af-42fe-862e-80978a58d9b1
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2017
ms.author: richrund
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ac96c242d03ed3a22ca96368e5a8cc53f9a993db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a><span data-ttu-id="ee2e6-104">Подключения виртуальных машин Azure tooLog аналитика с агентом анализа журналов</span><span class="sxs-lookup"><span data-stu-id="ee2e6-104">Connect Azure virtual machines tooLog Analytics with a Log Analytics agent</span></span>

<span data-ttu-id="ee2e6-105">Для компьютеров Windows и Linux hello рекомендуется использовать метод для сбора журналов и является метрики, установив агент hello анализа журналов.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-105">For Windows and Linux computers, hello recommended method for collecting logs and metrics is by installing hello Log Analytics agent.</span></span>

<span data-ttu-id="ee2e6-106">Hello простым способом tooinstall hello анализа журналов агент на виртуальных машинах Azure — с помощью hello расширение ВМ аналитика журналов.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-106">hello easiest way tooinstall hello Log Analytics agent on Azure virtual machines is through hello Log Analytics VM Extension.</span></span>  <span data-ttu-id="ee2e6-107">С помощью расширения hello упрощает процесс установки hello и автоматически настраивает hello агента toosend toohello анализа журналов область данных, можно указать.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-107">Using hello extension simplifies hello installation process and automatically configures hello agent toosend data toohello Log Analytics workspace that you specify.</span></span> <span data-ttu-id="ee2e6-108">Hello агент также обновляется автоматически, убедитесь, что существует hello новейшие функции и исправления.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-108">hello agent is also upgraded automatically, ensuring that you have hello latest features and fixes.</span></span>

<span data-ttu-id="ee2e6-109">Для виртуальных машин Windows включен hello *Microsoft Monitoring Agent* расширение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-109">For Windows virtual machines, you enable hello *Microsoft Monitoring Agent* virtual machine extension.</span></span>
<span data-ttu-id="ee2e6-110">Для виртуальных машин Linux включить hello *агента OMS для Linux* расширение виртуальной машины.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-110">For Linux virtual machines, you enable hello *OMS Agent For Linux* virtual machine extension.</span></span>

<span data-ttu-id="ee2e6-111">Дополнительные сведения о [расширения виртуальных машин Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и hello [агент Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-111">Learn more about [Azure virtual machine extensions](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) and hello [Linux agent](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ee2e6-112">При использовании коллекции на основе агентов для данных журнала, необходимо настроить [источники данных в службе анализа журналов](log-analytics-data-sources.md) toospecify hello метрик, которые должны toocollect и журналы.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-112">When you use agent-based collection for log data, you must configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics that you want toocollect.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ee2e6-113">Если данные журнала tooindex анализа журналов настройки с помощью [диагностики Azure](log-analytics-azure-storage.md), и настройте hello агента toocollect hello же журналы, а затем дважды сбора журналов hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-113">If you configure Log Analytics tooindex log data by using [Azure diagnostics](log-analytics-azure-storage.md), and you configure hello agent toocollect hello same logs, then hello logs are collected twice.</span></span> <span data-ttu-id="ee2e6-114">Плата взимается за использование обоих источников данных.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-114">You are charged for both data sources.</span></span> <span data-ttu-id="ee2e6-115">Если установлен агент hello, затем сбора данных журнала с помощью только hello агента - не Настройка данных журнала toocollect анализа журналов из службы диагностики Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-115">If you have hello agent installed, then collect log data by using only hello agent - don't configure Log Analytics toocollect log data from Azure diagnostics.</span></span>
>
>

<span data-ttu-id="ee2e6-116">Существует три способа легко расширение виртуальной машины tooenable hello анализа журналов:</span><span class="sxs-lookup"><span data-stu-id="ee2e6-116">There are three easy ways tooenable hello Log Analytics virtual machine extension:</span></span>

* <span data-ttu-id="ee2e6-117">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="ee2e6-117">By using hello Azure portal</span></span>
* <span data-ttu-id="ee2e6-118">с помощью Azure PowerShell;</span><span class="sxs-lookup"><span data-stu-id="ee2e6-118">By using Azure PowerShell</span></span>
* <span data-ttu-id="ee2e6-119">с помощью шаблона Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-119">By using an Azure Resource Manager template</span></span>

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a><span data-ttu-id="ee2e6-120">Включение расширения виртуальной Машины hello в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="ee2e6-120">Enable hello VM extension in hello Azure portal</span></span>
<span data-ttu-id="ee2e6-121">Можно установить агент hello для анализа журналов и подключения виртуальной машины для Azure, на котором работает с помощью hello hello [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-121">You can install hello agent for Log Analytics and connect hello Azure virtual machine that it runs on by using hello [Azure portal](https://portal.azure.com).</span></span>

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a><span data-ttu-id="ee2e6-122">tooinstall hello агента анализа журналов и подключите hello виртуальной машины tooa анализа журналов рабочей</span><span class="sxs-lookup"><span data-stu-id="ee2e6-122">tooinstall hello Log Analytics agent and connect hello virtual machine tooa Log Analytics workspace</span></span>
1. <span data-ttu-id="ee2e6-123">Вход в hello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-123">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="ee2e6-124">Выберите **Обзор** на hello слева от оператора hello портала, а затем перейдите слишком**аналитика журналов (OMS)** и выберите его.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-124">Select **Browse** on hello left side of hello portal, and then go too**Log Analytics (OMS)** and select it.</span></span>
3. <span data-ttu-id="ee2e6-125">В списке рабочих областей для анализа журналов выберите hello один нужных toouse с hello виртуальной Машине Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-125">In your list of Log Analytics workspaces, select hello one that you want toouse with hello Azure VM.</span></span>  
   ![Рабочие области OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. <span data-ttu-id="ee2e6-127">В меню **Управление службой Log Analytics** выберите плитку **Виртуальные машины**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-127">Under **Log analytics management**, select **Virtual machines**.</span></span>  
   <span data-ttu-id="ee2e6-128">![Виртуальные машины](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-128">![Virtual machines](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)</span></span>
5. <span data-ttu-id="ee2e6-129">В списке hello **виртуальные машины**, выберите hello виртуальной машины, на котором будет tooinstall hello агента.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-129">In hello list of **Virtual machines**, select hello virtual machine on which you want tooinstall hello agent.</span></span> <span data-ttu-id="ee2e6-130">Hello **состояние подключения OMS** для hello виртуальной Машины указывает, что он является **не подключен**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-130">hello **OMS connection status** for hello VM indicates that it is **Not connected**.</span></span>  
   <span data-ttu-id="ee2e6-131">![Виртуальная машина не подключена](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-131">![VM not connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)</span></span>
6. <span data-ttu-id="ee2e6-132">В сведениях о hello для виртуальной машины, выберите **Connect**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-132">In hello details for your virtual machine, select **Connect**.</span></span> <span data-ttu-id="ee2e6-133">Hello агент будет автоматически устанавливается и настраивается для рабочей области аналитики журналов.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-133">hello agent is automatically installed and configured for your Log Analytics workspace.</span></span> <span data-ttu-id="ee2e6-134">Этот процесс занимает несколько минут, во время которого является hello состояние подключения OMS *подключение...*</span><span class="sxs-lookup"><span data-stu-id="ee2e6-134">This process takes a few minutes, during which time hello OMS Connection status is *Connecting...*</span></span>  
   <span data-ttu-id="ee2e6-135">![Подключение виртуальной машины](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-135">![Connect VM](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)</span></span>
7. <span data-ttu-id="ee2e6-136">После установки и подключения агента hello hello **подключение OMS** состояние будет обновленные tooshow **этой рабочей области**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-136">After you install and connect hello agent, hello **OMS connection** status will be updated tooshow **This workspace**.</span></span>  
   <span data-ttu-id="ee2e6-137">![Подключено](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span><span class="sxs-lookup"><span data-stu-id="ee2e6-137">![Connected](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)</span></span>

## <a name="enable-hello-vm-extension-using-powershell"></a><span data-ttu-id="ee2e6-138">Включение расширения виртуальной Машины hello, с помощью PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee2e6-138">Enable hello VM extension using PowerShell</span></span>
<span data-ttu-id="ee2e6-139">При настройке виртуальной машины с помощью PowerShell необходимо tooprovide hello **ИД рабочей области** и **workspaceKey**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-139">When you configure your virtual machine by using PowerShell, you need tooprovide hello **workspaceId** and **workspaceKey**.</span></span> <span data-ttu-id="ee2e6-140">имена свойств Hello в конфигурации json, **с учетом регистра**.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-140">hello property names in your json configuration are **case-sensitive**.</span></span>

<span data-ttu-id="ee2e6-141">Здравствуйте, идентификатор и ключ на hello можно найти **параметры** страницы портала OMS hello, или с помощью PowerShell, как показано в предшествующих пример hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-141">You can find hello Id and key on hello **Settings** page of hello OMS portal, or by using PowerShell as shown in hello preceding example.</span></span>

![Идентификатор рабочей области и первичный ключ](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

<span data-ttu-id="ee2e6-143">Существуют разные команды для классических виртуальных машин Azure и виртуальных машин, созданных с помощью Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-143">There are different commands for Azure classic virtual machines and Resource Manager virtual machines.</span></span> <span data-ttu-id="ee2e6-144">Ниже представлено несколько примеров для виртуальных машин обоих типов.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-144">Following are examples for both classic and Resource Manager virtual machines.</span></span>

<span data-ttu-id="ee2e6-145">Для классических виртуальных машин используйте следующий пример PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-145">For classic virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Add-AzureAccount

$workspaceId = "enter workspace ID here"
$workspaceKey = "enter workspace key here"
$hostedService = "enter hosted service here"

$vm = Get-AzureVM –ServiceName $hostedService

# For Windows VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'MicrosoftMonitoringAgent' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose

# For Linux VM uncomment hello following line
# Set-AzureVMExtension -VM $vm -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionName 'OmsAgentForLinux' -Version '1.*' -PublicConfiguration "{'workspaceId': '$workspaceId'}" -PrivateConfiguration "{'workspaceKey': '$workspaceKey' }" | Update-AzureVM -Verbose
```

<span data-ttu-id="ee2e6-146">Диспетчер ресурсов виртуальных машин Linux с помощью следующих CLI hello</span><span class="sxs-lookup"><span data-stu-id="ee2e6-146">For Resource Manager Linux VMs using hello following CLI</span></span>
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

<span data-ttu-id="ee2e6-147">Для виртуальных машин диспетчера ресурсов используйте следующий пример PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-147">For Resource Manager virtual machines, use hello following PowerShell example:</span></span>

```PowerShell
Login-AzureRMAccount
Select-AzureRMSubscription -SubscriptionId "**"

$workspaceName = "your workspace name"
$VMresourcegroup = "**"
$VMresourcename = "**"

$workspace = (Get-AzureRmOperationalInsightsWorkspace).Where({$_.Name -eq $workspaceName})

if ($workspace.Name -ne $workspaceName)
{
    Write-Error "Unable toofind OMS Workspace $workspaceName. Do you need toorun Select-AzureRMSubscription?"
}

$workspaceId = $workspace.CustomerId
$workspaceKey = (Get-AzureRmOperationalInsightsWorkspaceSharedKeys -ResourceGroupName $workspace.ResourceGroupName -Name $workspace.Name).PrimarySharedKey

$vm = Get-AzureRmVM -ResourceGroupName $VMresourcegroup -Name $VMresourcename
$location = $vm.Location

# For Windows VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'MicrosoftMonitoringAgent' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'MicrosoftMonitoringAgent' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"

# For Linux VM uncomment hello following line
# Set-AzureRmVMExtension -ResourceGroupName $VMresourcegroup -VMName $VMresourcename -Name 'OmsAgentForLinux' -Publisher 'Microsoft.EnterpriseCloud.Monitoring' -ExtensionType 'OmsAgentForLinux' -TypeHandlerVersion '1.0' -Location $location -SettingString "{'workspaceId': '$workspaceId'}" -ProtectedSettingString "{'workspaceKey': '$workspaceKey'}"


```


## <a name="deploy-hello-vm-extension-using-a-template"></a><span data-ttu-id="ee2e6-148">Развертывание расширения hello виртуальной Машины, с помощью шаблона</span><span class="sxs-lookup"><span data-stu-id="ee2e6-148">Deploy hello VM extension using a template</span></span>
<span data-ttu-id="ee2e6-149">С помощью диспетчера ресурсов Azure, можно создать шаблон (в формате JSON), определяющий hello развертывания и настройки приложения.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-149">By using Azure Resource Manager, you can create a template (in JSON format) that defines hello deployment and configuration of your application.</span></span> <span data-ttu-id="ee2e6-150">Этот шаблон называется шаблона диспетчера ресурсов и предоставляет toodefine декларативным способом развертывания.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-150">This template is known as a Resource Manager template and provides a declarative way toodefine deployment.</span></span> <span data-ttu-id="ee2e6-151">С помощью шаблона, можно повторно развернуть приложение на протяжении жизненного цикла приложения hello и уверенность что ресурсы развертываются в согласованном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-151">By using a template, you can repeatedly deploy your application throughout hello app lifecycle and have confidence that your resources are being deployed in a consistent state.</span></span>

<span data-ttu-id="ee2e6-152">Как часть шаблона диспетчера ресурсов, включая hello анализа журналов агента, можно убедитесь, что каждая виртуальная машина является рабочей областью аналитики журналов предварительно настроенных tooreport tooyour.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-152">By including hello Log Analytics agent as part of your Resource Manager template, you can ensure that each virtual machine is pre-configured tooreport tooyour Log Analytics workspace.</span></span>

<span data-ttu-id="ee2e6-153">Дополнительную информацию о шаблонах Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-153">For more information about Resource Manager templates, see [Authoring Azure Resource Manager templates](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="ee2e6-154">Ниже приведен пример шаблона диспетчера ресурсов, который используется для развертывания виртуальной машины под управлением Windows с hello установлены расширения Microsoft Monitoring Agent.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-154">Following is an example of a Resource Manager template that's used for deploying a virtual machine that's running Windows with hello Microsoft Monitoring Agent extension installed.</span></span> <span data-ttu-id="ee2e6-155">Этот шаблон является шаблоном обычной виртуальной машины, с hello следующие дополнения:</span><span class="sxs-lookup"><span data-stu-id="ee2e6-155">This template is a typical virtual machine template, with hello following additions:</span></span>

* <span data-ttu-id="ee2e6-156">Параметры workspaceId и workspaceName.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-156">workspaceId and workspaceName parameters</span></span>
* <span data-ttu-id="ee2e6-157">Раздел расширения ресурса Microsoft.EnterpriseCloud.Monitoring.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-157">Microsoft.EnterpriseCloud.Monitoring resource extension section</span></span>
* <span data-ttu-id="ee2e6-158">Выходные данные toolook hello ИД рабочей области и workspaceSharedKey</span><span class="sxs-lookup"><span data-stu-id="ee2e6-158">Outputs toolook up hello workspaceId and workspaceSharedKey</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "adminUsername": {
      "type": "string",
      "metadata": {
        "description": "Username for hello Virtual Machine."
      }
    },
    "adminPassword": {
      "type": "securestring",
      "metadata": {
        "description": "Password for hello Virtual Machine."
      }
    },
    "dnsLabelPrefix": {
       "type": "string",
       "metadata": {
          "description": "DNS Label for hello Public IP. Must be lowercase. It should match with hello following regular expression: ^[a-z][a-z0-9-]{1,61}[a-z0-9]$ or it will raise an error."
       }
    },
    "workspaceId": {
      "type": "string",
      "metadata": {
        "description": "OMS workspace ID"
      }
    },
    "workspaceName": {
      "type": "string",
      "metadata": {
         "description": "OMS workspace name"
      }
    },
    "windowsOSVersion": {
      "type": "string",
      "defaultValue": "2012-R2-Datacenter",
      "allowedValues": [
        "2008-R2-SP1",
        "2012-Datacenter",
        "2012-R2-Datacenter",
        "Windows-Server-Technical-Preview"
      ],
      "metadata": {
        "description": "hello Windows version for hello VM. This will pick a fully patched image of this given Windows version. Allowed values: 2008-R2-SP1, 2012-Datacenter, 2012-R2-Datacenter, Windows-Server-Technical-Preview."
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]",
    "apiVersion": "2015-06-15",
    "imagePublisher": "MicrosoftWindowsServer",
    "imageOffer": "WindowsServer",
    "OSDiskName": "osdiskforwindowssimple",
    "nicName": "myVMNic",
    "addressPrefix": "10.0.0.0/16",
    "subnetName": "Subnet",
    "subnetPrefix": "10.0.0.0/24",
    "storageAccountType": "Standard_LRS",
    "publicIPAddressName": "myPublicIP",
    "publicIPAddressType": "Dynamic",
    "vmStorageAccountContainerName": "vhds",
    "vmName": "MyWindowsVM",
    "vmSize": "Standard_DS1",
    "virtualNetworkName": "MyVNET",
    "resourceId": "[resourceGroup().id]",
    "vnetID": "[resourceId('Microsoft.Network/virtualNetworks',variables('virtualNetworkName'))]",
    "subnetRef": "[concat(variables('vnetID'),'/subnets/',variables('subnetName'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "[variables('apiVersion')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "accountType": "[variables('storageAccountType')]"
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIPAddressName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "[variables('publicIPAddressType')]",
        "dnsSettings": {
          "domainNameLabel": "[parameters('dnsLabelPrefix')]"
        }
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": {
          "addressPrefixes": [
            "[variables('addressPrefix')]"
          ]
        },
        "subnets": [
          {
            "name": "[variables('subnetName')]",
            "properties": {
              "addressPrefix": "[variables('subnetPrefix')]"
            }
          }
        ]
      }
    },
    {
      "apiVersion": "[variables('apiVersion')]",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIPAddressName'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses',variables('publicIPAddressName'))]"
              },
              "subnet": {
                "id": "[variables('subnetRef')]"
              }
            }
          }
        ]
      }
    },
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[variables('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Storage/storageAccounts/', variables('storageAccountName'))]",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": {
          "vmSize": "[variables('vmSize')]"
        },
        "osProfile": {
          "computername": "[variables('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "[variables('imagePublisher')]",
            "offer": "[variables('imageOffer')]",
            "sku": "[parameters('windowsOSVersion')]",
            "version": "latest"
          },
          "osDisk": {
            "name": "osdisk",
            "vhd": {
              "uri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net/',variables('vmStorageAccountContainerName'),'/',variables('OSDiskName'),'.vhd')]"
            },
            "caching": "ReadWrite",
            "createOption": "FromImage"
          }
        },
        "networkProfile": {
          "networkInterfaces": [
            {
              "id": "[resourceId('Microsoft.Network/networkInterfaces',variables('nicName'))]"
            }
          ]
        },
        "diagnosticsProfile": {
          "bootDiagnostics": {
             "enabled": "true",
             "storageUri": "[concat('http://',variables('storageAccountName'),'.blob.core.windows.net')]"
          }
        }
      },
      "resources": [
        {
          "type": "extensions",
          "name": "Microsoft.EnterpriseCloud.Monitoring",
          "apiVersion": "[variables('apiVersion')]",
          "location": "[resourceGroup().location]",
          "dependsOn": [
            "[concat('Microsoft.Compute/virtualMachines/', variables('vmName'))]"
          ],
          "properties": {
            "publisher": "Microsoft.EnterpriseCloud.Monitoring",
            "type": "MicrosoftMonitoringAgent",
            "typeHandlerVersion": "1.0",
            "autoUpgradeMinorVersion": true,
            "settings": {
              "workspaceId": "[parameters('workspaceId')]"
            },
            "protectedSettings": {
              "workspaceKey": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces', parameters('workspaceName')), '2015-03-20').primarySharedKey]"
            }
          }
        }
      ]
    }
  ],
  "outputs": {
      "sharedKeyOutput": {
         "value": "[listKeys(resourceId('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').primarySharedKey]",
         "type": "string"
      },
      "workspaceIdOutput": {
         "value": "[reference(concat('Microsoft.OperationalInsights/workspaces/', parameters('workspaceName')), '2015-03-20').customerId]",
        "type" : "string"
      }
  }
}
```

<span data-ttu-id="ee2e6-159">Можно развернуть шаблон с помощью hello следующую команду PowerShell:</span><span class="sxs-lookup"><span data-stu-id="ee2e6-159">You can deploy a template by using hello following PowerShell command:</span></span>

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a><span data-ttu-id="ee2e6-160">Устранение неполадок расширений ВМ аналитика журналов hello</span><span class="sxs-lookup"><span data-stu-id="ee2e6-160">Troubleshooting hello Log Analytics VM extension</span></span>
<span data-ttu-id="ee2e6-161">Если что-то не работает должным образом, как правило, вы должны получить сообщение, отправленное либо порталом Azure, либо средствами Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-161">Usually you receive a message when things don't work, from either Azure portal or Azure powershell.</span></span>

1. <span data-ttu-id="ee2e6-162">Вход в hello [портал Azure](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-162">Sign into hello [Azure portal](http://portal.azure.com).</span></span>
2. <span data-ttu-id="ee2e6-163">Найти hello ВМ и откройте сведения о виртуальной Машине.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-163">Find hello VM and open VM details.</span></span>
3. <span data-ttu-id="ee2e6-164">Нажмите кнопку **расширения** toocheck, если расширение OMS включено или нет.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-164">Click **Extensions** toocheck if OMS extension is enabled or not.</span></span>

   ![Представление расширения виртуальной машины](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. <span data-ttu-id="ee2e6-166">Нажмите кнопку hello *MicrosoftMonitoringAgent*(Windows) или *OmsAgentForLinux*расширения и просмотреть подробные сведения (Linux).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-166">Click hello *MicrosoftMonitoringAgent*(Windows) or *OmsAgentForLinux*(Linux) extension and view details.</span></span> 

   ![Сведения о расширении виртуальной машины](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a><span data-ttu-id="ee2e6-168">Устранение неполадок на виртуальных машинах Windows</span><span class="sxs-lookup"><span data-stu-id="ee2e6-168">Troubleshooting Windows Virtual Machines</span></span>
<span data-ttu-id="ee2e6-169">Если hello *Microsoft Monitoring Agent* расширение агент ВМ не устанавливает или отчетов, можно выполнить следующие шаги tootroubleshoot hello проблема hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-169">If hello *Microsoft Monitoring Agent* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="ee2e6-170">Проверьте установлен агент ВМ Azure hello и работе правильно, с помощью hello шагов в [2965986 КБ](https://support.microsoft.com/kb/2965986#mt1).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-170">Check if hello Azure VM agent is installed and working correctly by using hello steps in [KB 2965986](https://support.microsoft.com/kb/2965986#mt1).</span></span>
   * <span data-ttu-id="ee2e6-171">Можно также просмотреть файл журнала агента ВМ hello`C:\WindowsAzure\logs\WaAppAgent.log`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-171">You can also review hello VM agent log file `C:\WindowsAzure\logs\WaAppAgent.log`</span></span>
   * <span data-ttu-id="ee2e6-172">Если журнал hello не существует, не установлен агент ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-172">If hello log does not exist, hello VM agent is not installed.</span></span>
     * [<span data-ttu-id="ee2e6-173">Установите hello агента ВМ Azure на классическом виртуальные машины</span><span class="sxs-lookup"><span data-stu-id="ee2e6-173">Install hello Azure VM Agent on classic VMs</span></span>](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. <span data-ttu-id="ee2e6-174">Подтверждение hello Microsoft Monitoring Agent, расширение пульса задача выполняется с помощью hello следующие шаги:</span><span class="sxs-lookup"><span data-stu-id="ee2e6-174">Confirm hello Microsoft Monitoring Agent extension heartbeat task is running using hello following steps:</span></span>
   * <span data-ttu-id="ee2e6-175">Войдите в виртуальную машину toohello</span><span class="sxs-lookup"><span data-stu-id="ee2e6-175">Log in toohello virtual machine</span></span>
   * <span data-ttu-id="ee2e6-176">Откройте планировщик заданий и найти hello `update_azureoperationalinsight_agent_heartbeat` задач</span><span class="sxs-lookup"><span data-stu-id="ee2e6-176">Open task scheduler and find hello `update_azureoperationalinsight_agent_heartbeat` task</span></span>
   * <span data-ttu-id="ee2e6-177">Подтвердите задачу hello включено и выполняется раз в минуту</span><span class="sxs-lookup"><span data-stu-id="ee2e6-177">Confirm hello task is enabled and is running every one minute</span></span>
   * <span data-ttu-id="ee2e6-178">Проверьте файл журнала пульса hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-178">Check hello heartbeat logfile in `C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`</span></span>
3. <span data-ttu-id="ee2e6-179">Просмотрите файлы журналов расширение виртуальной Машине агент наблюдения Microsoft hello в`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-179">Review hello Microsoft Monitoring Agent VM extension log files in `C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`</span></span>
4. <span data-ttu-id="ee2e6-180">Убедитесь, что hello виртуальной машины можно запускать скрипты PowerShell</span><span class="sxs-lookup"><span data-stu-id="ee2e6-180">Ensure hello virtual machine can run PowerShell scripts</span></span>
5. <span data-ttu-id="ee2e6-181">Убедитесь, что разрешения на доступ к папке C:\Windows\temp не были изменены.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-181">Ensure permissions on C:\Windows\temp haven’t been changed</span></span>
6. <span data-ttu-id="ee2e6-182">Просмотр состояния hello hello Microsoft Monitoring Agent, введя следующую команду в окне PowerShell с повышенными привилегиями на виртуальной машине hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-182">View hello status of hello Microsoft Monitoring Agent by typing hello following command in an elevated PowerShell window on hello virtual machine `  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`</span></span>
7. <span data-ttu-id="ee2e6-183">Просмотрите файлы журналов программы установки Microsoft Monitoring Agent hello в`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-183">Review hello Microsoft Monitoring Agent setup log files in `C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`</span></span>

<span data-ttu-id="ee2e6-184">Подробные сведения см. в статье об [устранении неполадок расширений для виртуальных машин Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-184">For more information, see [troubleshooting Windows extensions](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

### <a name="troubleshooting-linux-virtual-machines"></a><span data-ttu-id="ee2e6-185">Устранение неполадок на виртуальных машинах Linux</span><span class="sxs-lookup"><span data-stu-id="ee2e6-185">Troubleshooting Linux Virtual Machines</span></span>
<span data-ttu-id="ee2e6-186">Если hello *агента OMS для Linux* расширение агент ВМ не устанавливает или отчетов, можно выполнить следующие шаги tootroubleshoot hello проблема hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-186">If hello *OMS Agent for Linux* VM agent extension is not installing or reporting, you can perform hello following steps tootroubleshoot hello issue.</span></span>

1. <span data-ttu-id="ee2e6-187">Если состояние расширения hello *Неизвестный* проверьте, установлены ли агент ВМ Azure hello и работают правильно, просмотрев файл журнала агента ВМ hello`/var/log/waagent.log`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-187">If hello extension status is *Unknown* check if hello Azure VM agent is installed and working correctly by reviewing hello VM agent log file `/var/log/waagent.log`</span></span>
   * <span data-ttu-id="ee2e6-188">Если журнал hello не существует, не установлен агент ВМ hello.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-188">If hello log does not exist, hello VM agent is not installed.</span></span>
   * [<span data-ttu-id="ee2e6-189">Установка hello агента ВМ Azure на виртуальных машинах Linux</span><span class="sxs-lookup"><span data-stu-id="ee2e6-189">Install hello Azure VM Agent on Linux VMs</span></span>](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. <span data-ttu-id="ee2e6-190">Для других неработоспособное статусы hello Обзор агента OMS для расширения ВМ Linux файлы журналов `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` и`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-190">For other unhealthy statuses, review hello OMS Agent for Linux VM extension logs files in `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` and `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`</span></span>
3. <span data-ttu-id="ee2e6-191">Если состояние расширения hello находится в работоспособном состоянии, но данных не отправляется для файлов журнала Linux в просмотрите hello агента OMS`/var/opt/microsoft/omsagent/log/omsagent.log`</span><span class="sxs-lookup"><span data-stu-id="ee2e6-191">If hello extension status is healthy, but data is not being uploaded review hello OMS Agent for Linux log files in `/var/opt/microsoft/omsagent/log/omsagent.log`</span></span>

## <a name="next-steps"></a><span data-ttu-id="ee2e6-192">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ee2e6-192">Next steps</span></span>
* <span data-ttu-id="ee2e6-193">Настройка [источники данных в службе анализа журналов](log-analytics-data-sources.md) toocollect toospecify hello журналов и показателей.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-193">Configure [data sources in Log Analytics](log-analytics-data-sources.md) toospecify hello logs and metrics toocollect.</span></span>
* <span data-ttu-id="ee2e6-194">данные виртуальных машин toogather [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ee2e6-194">toogather data from virtual machines [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>
* <span data-ttu-id="ee2e6-195">[С помощью системы диагностики Azure соберите данные](log-analytics-azure-storage.md) для других ресурсов, работающих в Azure.</span><span class="sxs-lookup"><span data-stu-id="ee2e6-195">[Collect data by using Azure Diagnostics](log-analytics-azure-storage.md) for other resources that are running in Azure.</span></span>

<span data-ttu-id="ee2e6-196">Для компьютеров, которые не находятся в Azure можно установить агент hello анализа журналов с помощью hello методов, описанных в hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="ee2e6-196">For computers that are not in Azure, you can install hello Log Analytics agent by using hello methods that are described in hello following articles:</span></span>

* [<span data-ttu-id="ee2e6-197">Подключение компьютеров Windows tooLog аналитика</span><span class="sxs-lookup"><span data-stu-id="ee2e6-197">Connect Windows computers tooLog Analytics</span></span>](log-analytics-windows-agents.md)
* [<span data-ttu-id="ee2e6-198">Подключение компьютеров Linux tooLog аналитика</span><span class="sxs-lookup"><span data-stu-id="ee2e6-198">Connect Linux computers tooLog Analytics</span></span>](log-analytics-linux-agents.md)
