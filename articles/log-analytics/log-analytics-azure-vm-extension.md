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
# <a name="connect-azure-virtual-machines-toolog-analytics-with-a-log-analytics-agent"></a>Подключения виртуальных машин Azure tooLog аналитика с агентом анализа журналов

Для компьютеров Windows и Linux hello рекомендуется использовать метод для сбора журналов и является метрики, установив агент hello анализа журналов.

Hello простым способом tooinstall hello анализа журналов агент на виртуальных машинах Azure — с помощью hello расширение ВМ аналитика журналов.  С помощью расширения hello упрощает процесс установки hello и автоматически настраивает hello агента toosend toohello анализа журналов область данных, можно указать. Hello агент также обновляется автоматически, убедитесь, что существует hello новейшие функции и исправления.

Для виртуальных машин Windows включен hello *Microsoft Monitoring Agent* расширение виртуальной машины.
Для виртуальных машин Linux включить hello *агента OMS для Linux* расширение виртуальной машины.

Дополнительные сведения о [расширения виртуальных машин Azure](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) и hello [агент Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

При использовании коллекции на основе агентов для данных журнала, необходимо настроить [источники данных в службе анализа журналов](log-analytics-data-sources.md) toospecify hello метрик, которые должны toocollect и журналы.

> [!IMPORTANT]
> Если данные журнала tooindex анализа журналов настройки с помощью [диагностики Azure](log-analytics-azure-storage.md), и настройте hello агента toocollect hello же журналы, а затем дважды сбора журналов hello. Плата взимается за использование обоих источников данных. Если установлен агент hello, затем сбора данных журнала с помощью только hello агента - не Настройка данных журнала toocollect анализа журналов из службы диагностики Azure.
>
>

Существует три способа легко расширение виртуальной машины tooenable hello анализа журналов:

* С помощью портала Azure hello
* с помощью Azure PowerShell;
* с помощью шаблона Azure Resource Manager.

## <a name="enable-hello-vm-extension-in-hello-azure-portal"></a>Включение расширения виртуальной Машины hello в hello портал Azure
Можно установить агент hello для анализа журналов и подключения виртуальной машины для Azure, на котором работает с помощью hello hello [портал Azure](https://portal.azure.com).

### <a name="tooinstall-hello-log-analytics-agent-and-connect-hello-virtual-machine-tooa-log-analytics-workspace"></a>tooinstall hello агента анализа журналов и подключите hello виртуальной машины tooa анализа журналов рабочей
1. Вход в hello [портал Azure](http://portal.azure.com).
2. Выберите **Обзор** на hello слева от оператора hello портала, а затем перейдите слишком**аналитика журналов (OMS)** и выберите его.
3. В списке рабочих областей для анализа журналов выберите hello один нужных toouse с hello виртуальной Машине Azure.  
   ![Рабочие области OMS](./media/log-analytics-azure-vm-extension/oms-connect-azure-01.png)
4. В меню **Управление службой Log Analytics** выберите плитку **Виртуальные машины**.  
   ![Виртуальные машины](./media/log-analytics-azure-vm-extension/oms-connect-azure-02.png)
5. В списке hello **виртуальные машины**, выберите hello виртуальной машины, на котором будет tooinstall hello агента. Hello **состояние подключения OMS** для hello виртуальной Машины указывает, что он является **не подключен**.  
   ![Виртуальная машина не подключена](./media/log-analytics-azure-vm-extension/oms-connect-azure-03.png)
6. В сведениях о hello для виртуальной машины, выберите **Connect**. Hello агент будет автоматически устанавливается и настраивается для рабочей области аналитики журналов. Этот процесс занимает несколько минут, во время которого является hello состояние подключения OMS *подключение...*  
   ![Подключение виртуальной машины](./media/log-analytics-azure-vm-extension/oms-connect-azure-04.png)
7. После установки и подключения агента hello hello **подключение OMS** состояние будет обновленные tooshow **этой рабочей области**.  
   ![Подключено](./media/log-analytics-azure-vm-extension/oms-connect-azure-05.png)

## <a name="enable-hello-vm-extension-using-powershell"></a>Включение расширения виртуальной Машины hello, с помощью PowerShell
При настройке виртуальной машины с помощью PowerShell необходимо tooprovide hello **ИД рабочей области** и **workspaceKey**. имена свойств Hello в конфигурации json, **с учетом регистра**.

Здравствуйте, идентификатор и ключ на hello можно найти **параметры** страницы портала OMS hello, или с помощью PowerShell, как показано в предшествующих пример hello.

![Идентификатор рабочей области и первичный ключ](./media/log-analytics-azure-vm-extension/oms-analyze-azure-sources.png)

Существуют разные команды для классических виртуальных машин Azure и виртуальных машин, созданных с помощью Resource Manager. Ниже представлено несколько примеров для виртуальных машин обоих типов.

Для классических виртуальных машин используйте следующий пример PowerShell hello.

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

Диспетчер ресурсов виртуальных машин Linux с помощью следующих CLI hello
```azurecli
az vm extension set --resource-group myRGMonitor --vm-name myMonitorVM --name OmsAgentForLinux --publisher Microsoft.EnterpriseCloud.Monitoring --version 1.3 --protected-settings ‘{"workspaceKey": "<workspace-key>"}’ --settings ‘{"workspaceId": "<workspace-id>"}’ 
```

Для виртуальных машин диспетчера ресурсов используйте следующий пример PowerShell hello.

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


## <a name="deploy-hello-vm-extension-using-a-template"></a>Развертывание расширения hello виртуальной Машины, с помощью шаблона
С помощью диспетчера ресурсов Azure, можно создать шаблон (в формате JSON), определяющий hello развертывания и настройки приложения. Этот шаблон называется шаблона диспетчера ресурсов и предоставляет toodefine декларативным способом развертывания. С помощью шаблона, можно повторно развернуть приложение на протяжении жизненного цикла приложения hello и уверенность что ресурсы развертываются в согласованном состоянии.

Как часть шаблона диспетчера ресурсов, включая hello анализа журналов агента, можно убедитесь, что каждая виртуальная машина является рабочей областью аналитики журналов предварительно настроенных tooreport tooyour.

Дополнительную информацию о шаблонах Resource Manager см. в статье [Создание шаблонов Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

Ниже приведен пример шаблона диспетчера ресурсов, который используется для развертывания виртуальной машины под управлением Windows с hello установлены расширения Microsoft Monitoring Agent. Этот шаблон является шаблоном обычной виртуальной машины, с hello следующие дополнения:

* Параметры workspaceId и workspaceName.
* Раздел расширения ресурса Microsoft.EnterpriseCloud.Monitoring.
* Выходные данные toolook hello ИД рабочей области и workspaceSharedKey

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

Можно развернуть шаблон с помощью hello следующую команду PowerShell:

```PowerShell
New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath
```

## <a name="troubleshooting-hello-log-analytics-vm-extension"></a>Устранение неполадок расширений ВМ аналитика журналов hello
Если что-то не работает должным образом, как правило, вы должны получить сообщение, отправленное либо порталом Azure, либо средствами Azure PowerShell.

1. Вход в hello [портал Azure](http://portal.azure.com).
2. Найти hello ВМ и откройте сведения о виртуальной Машине.
3. Нажмите кнопку **расширения** toocheck, если расширение OMS включено или нет.

   ![Представление расширения виртуальной машины](./media/log-analytics-azure-vm-extension/oms-vmview-extensions.png)

4. Нажмите кнопку hello *MicrosoftMonitoringAgent*(Windows) или *OmsAgentForLinux*расширения и просмотреть подробные сведения (Linux). 

   ![Сведения о расширении виртуальной машины](./media/log-analytics-azure-vm-extension/oms-vmview-extensiondetails.png)

### <a name="troubleshooting-windows-virtual-machines"></a>Устранение неполадок на виртуальных машинах Windows
Если hello *Microsoft Monitoring Agent* расширение агент ВМ не устанавливает или отчетов, можно выполнить следующие шаги tootroubleshoot hello проблема hello.

1. Проверьте установлен агент ВМ Azure hello и работе правильно, с помощью hello шагов в [2965986 КБ](https://support.microsoft.com/kb/2965986#mt1).
   * Можно также просмотреть файл журнала агента ВМ hello`C:\WindowsAzure\logs\WaAppAgent.log`
   * Если журнал hello не существует, не установлен агент ВМ hello.
     * [Установите hello агента ВМ Azure на классическом виртуальные машины](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)
2. Подтверждение hello Microsoft Monitoring Agent, расширение пульса задача выполняется с помощью hello следующие шаги:
   * Войдите в виртуальную машину toohello
   * Откройте планировщик заданий и найти hello `update_azureoperationalinsight_agent_heartbeat` задач
   * Подтвердите задачу hello включено и выполняется раз в минуту
   * Проверьте файл журнала пульса hello`C:\WindowsAzure\Logs\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent\heartbeat.log`
3. Просмотрите файлы журналов расширение виртуальной Машине агент наблюдения Microsoft hello в`C:\Packages\Plugins\Microsoft.EnterpriseCloud.Monitoring.MicrosoftMonitoringAgent`
4. Убедитесь, что hello виртуальной машины можно запускать скрипты PowerShell
5. Убедитесь, что разрешения на доступ к папке C:\Windows\temp не были изменены.
6. Просмотр состояния hello hello Microsoft Monitoring Agent, введя следующую команду в окне PowerShell с повышенными привилегиями на виртуальной машине hello hello`  (New-Object -ComObject 'AgentConfigManager.MgmtSvcCfg').GetCloudWorkspaces() | Format-List`
7. Просмотрите файлы журналов программы установки Microsoft Monitoring Agent hello в`C:\Windows\System32\config\systemprofile\AppData\Local\SCOM\Logs`

Подробные сведения см. в статье об [устранении неполадок расширений для виртуальных машин Windows](../virtual-machines/windows/extensions-troubleshoot.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

### <a name="troubleshooting-linux-virtual-machines"></a>Устранение неполадок на виртуальных машинах Linux
Если hello *агента OMS для Linux* расширение агент ВМ не устанавливает или отчетов, можно выполнить следующие шаги tootroubleshoot hello проблема hello.

1. Если состояние расширения hello *Неизвестный* проверьте, установлены ли агент ВМ Azure hello и работают правильно, просмотрев файл журнала агента ВМ hello`/var/log/waagent.log`
   * Если журнал hello не существует, не установлен агент ВМ hello.
   * [Установка hello агента ВМ Azure на виртуальных машинах Linux](../virtual-machines/linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
2. Для других неработоспособное статусы hello Обзор агента OMS для расширения ВМ Linux файлы журналов `/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/extension.log` и`/var/log/azure/Microsoft.EnterpriseCloud.Monitoring.OmsAgentForLinux/*/CommandExecution.log`
3. Если состояние расширения hello находится в работоспособном состоянии, но данных не отправляется для файлов журнала Linux в просмотрите hello агента OMS`/var/opt/microsoft/omsagent/log/omsagent.log`

## <a name="next-steps"></a>Дальнейшие действия
* Настройка [источники данных в службе анализа журналов](log-analytics-data-sources.md) toocollect toospecify hello журналов и показателей.
* данные виртуальных машин toogather [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).
* [С помощью системы диагностики Azure соберите данные](log-analytics-azure-storage.md) для других ресурсов, работающих в Azure.

Для компьютеров, которые не находятся в Azure можно установить агент hello анализа журналов с помощью hello методов, описанных в hello в следующих статьях:

* [Подключение компьютеров Windows tooLog аналитика](log-analytics-windows-agents.md)
* [Подключение компьютеров Linux tooLog аналитика](log-analytics-linux-agents.md)
