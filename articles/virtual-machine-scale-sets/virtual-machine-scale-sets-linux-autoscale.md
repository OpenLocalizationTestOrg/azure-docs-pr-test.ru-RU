---
title: "Наборы масштабирования виртуальных машин Linux aaaAutoscale | Документы Microsoft"
description: "Настройка масштабирования для набора масштабирования виртуальных машин Linux с помощью интерфейса командной строки Azure"
services: virtual-machine-scale-sets
documentationcenter: 
author: Thraka
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 83e93d9c-cac0-41d3-8316-6016f5ed0ce4
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/27/2016
ms.author: adegeo
ms.openlocfilehash: 4352b94ec2973c37bc5616e3be25bd0c9442632b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-linux-machines-in-a-virtual-machine-scale-set"></a>Автоматическое масштабирование машин Linux в наборе масштабирования виртуальных машин
Наборы масштабирования виртуальных машин упростить для вас toodeploy идентичные виртуальных машин и управление как набор. Масштабируемые наборы обеспечивают высокую степень масштабируемости и персонализацию уровня вычислений для гипермасштабируемых приложений. Кроме того, они поддерживают образы платформ Windows и Linux, а также пользовательские образы и расширения. toolearn более, в разделе [обзор наборов масштабирования виртуальных машин](virtual-machine-scale-sets-overview.md).

Этом учебнике показано, как задать toocreate масштабирования виртуальных машин Linux с помощью последней версии hello Ubuntu Linux. Hello учебнике также показано, как задать tooautomatically машины hello масштабирования в hello. Можно создать шкалу hello установить и настроить масштабирование, создание шаблона диспетчера ресурсов Azure и развертывая его с помощью Azure CLI. Дополнительную информацию о шаблонах см. в статье [Создание шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md). toolearn Дополнительные сведения о автоматического масштабирования наборы масштабирования в разделе [автоматического масштабирования и виртуальной машины задает масштаб](virtual-machine-scale-sets-autoscale-overview.md).

В этом учебнике развертывание hello следующих ресурсов и расширения:

* Microsoft.Storage/storageAccounts
* Microsoft.Network/virtualNetworks
* Microsoft.Network/publicIPAddresses
* Microsoft.Network/loadBalancers
* Microsoft.Network/networkInterfaces
* Microsoft.Compute/virtualMachines
* Microsoft.Compute/virtualMachineScaleSets;
* Microsoft.Insights.VMDiagnosticsSettings;
* Microsoft.Insights/autoscaleSettings.

Дополнительные сведения о ресурсах Resource Manager см. в статье [Azure Resource Manager vs. classic deployment](../azure-resource-manager/resource-manager-deployment-model.md) (Развертывание с помощью Azure Resource Manager и классическое развертывание).

Перед началом работы с hello шаги в этом учебнике [установить hello Azure CLI](../cli-install-nodejs.md).

## <a name="step-1-create-a-resource-group-and-a-storage-account"></a>Шаг 1. Создание группы ресурсов и учетной записи хранения

1. **Войдите в tooMicrosoft Azure**  
В интерфейсе командной строки (Bash, терминалов, командной строке) режима tooResource Manager, а затем [вход с идентификатором рабочей или учебной](../xplat-cli-connect.md#scenario-1-azure-login-with-interactive-login). Следуйте инструкциям hello для интерактивного входа в систему качества tooyour учетная запись Azure.

    ```cli   
    azure config mode arm

    azure login
    ```
   
    > [!NOTE]
    > Если вас есть рабочая идентификатор и не двухфакторная проверка подлинности включена, то следует использовать `azure login -u` с Идентификатором toolog hello в без интерактивного сеанса. Если у вас нет рабочего или учебного идентификатора, его можно [создать в личной учетной записи Майкрософт](../active-directory/active-directory-users-create-azure-portal.md).
    
2. **Создайте группу ресурсов**.  
Все ресурсы должны быть tooa развернутой группы ресурсов. В этом учебнике, имя группы ресурсов hello **vmsstest1**.
   
    ```cli
    azure group create vmsstestrg1 centralus
    ```

3. **Развертывание учетной записи хранения в новую группу ресурсов hello**  
Эта учетная запись хранения —, где хранится шаблон hello. Создайте учетную запись хранения с именем **vmsstestsa**.
   
    ```cli
    azure storage account create -g vmsstestrg1 -l centralus --kind Storage --sku-name LRS vmsstestsa
    ```

## <a name="step-2-create-hello-template"></a>Шаг 2: Создание шаблона hello
Шаблон диспетчера ресурсов Azure позволяет вам toodeploy и управлять ресурсами Azure совместно с помощью описания JSON ресурсов hello и связанных параметров развертывания.

1. В любом редакторе создайте файл hello VMSSTemplate.json и добавьте hello исходного JSON структуры toosupport hello шаблона.

    ```json
    {
      "$schema":"http://schema.management.azure.com/schemas/2014-04-01-preview/VM.json",
      "contentVersion": "1.0.0.0",
      "parameters": {
      },
      "variables": {
      },
      "resources": [
      ]
    }
    ```

2. Параметры обычно не требуется, но они обеспечивают tooinput способом значения при развертывании шаблона hello. Добавление этих параметров hello параметров родительского элемента, что вы добавили шаблон toohello.

    ```json
    "vmName": { "type": "string" },
    "vmSSName": { "type": "string" },
    "instanceCount": { "type": "string" },
    "adminUsername": { "type": "string" },
    "adminPassword": { "type": "securestring" },
    "resourcePrefix": { "type": "string" }
    ```
   
   * Имя для hello отдельной виртуальной машине, используемых tooaccess hello машины в наборе масштабирования hello.
   * Имя для учетной записи хранения hello, где хранится шаблон hello.
   * Hello число экземпляров виртуальных машин tooinitially создать в наборе масштабирования hello.
   * Имя и пароль учетной записи администратора hello на виртуальных машинах hello.
   * Задайте префикс имени hello ресурсов, которые создаются toosupport hello шкалы.

3. Переменные могут использоваться в значениях toospecify шаблона, которые могут часто изменяться или значения, которые необходимо toobe, созданные на основе сочетания значений параметров. Добавьте эти переменные hello переменные родительского элемента, что вы добавили шаблон toohello.

    ```json
    "dnsName1": "[concat(parameters('resourcePrefix'),'dn1')]",
    "dnsName2": "[concat(parameters('resourcePrefix'),'dn2')]",
    "publicIP1": "[concat(parameters('resourcePrefix'),'ip1')]",
    "publicIP2": "[concat(parameters('resourcePrefix'),'ip2')]",
    "loadBalancerName": "[concat(parameters('resourcePrefix'),'lb1')]",
    "virtualNetworkName": "[concat(parameters('resourcePrefix'),'vn1')]",
    "nicName": "[concat(parameters('resourcePrefix'),'nc1')]",
    "lbID": "[resourceId('Microsoft.Network/loadBalancers',variables('loadBalancerName'))]",
    "frontEndIPConfigID": "[concat(variables('lbID'),'/frontendIPConfigurations/loadBalancerFrontEnd')]",
    "storageAccountSuffix": [ "a", "g", "m", "s", "y" ],
    "diagnosticsStorageAccountName": "[concat(parameters('resourcePrefix'), 'a')]",
    "accountid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/','Microsoft.Storage/storageAccounts/', variables('diagnosticsStorageAccountName'))]",
    "wadlogs": "<WadCfg><DiagnosticMonitorConfiguration>",
    "wadperfcounter": "<PerformanceCounters scheduledTransferPeriod=\"PT1M\"><PerformanceCounterConfiguration counterSpecifier=\"\\Processor\\PercentProcessorTime\" sampleRate=\"PT15S\" unit=\"Percent\"><annotation displayName=\"CPU percentage guest OS\" locale=\"en-us\"/></PerformanceCounterConfiguration></PerformanceCounters>",
    "wadcfgxstart": "[concat(variables('wadlogs'),variables('wadperfcounter'),'<Metrics resourceId=\"')]",
    "wadmetricsresourceid": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name ,'/providers/','Microsoft.Compute/virtualMachineScaleSets/',parameters('vmssName'))]",
    "wadcfgxend": "[concat('\"><MetricAggregation scheduledTransferPeriod=\"PT1H\"/><MetricAggregation scheduledTransferPeriod=\"PT1M\"/></Metrics></DiagnosticMonitorConfiguration></WadCfg>')]"
    ```

   * DNS-имена, которые используются в hello сетевых интерфейсов.
   * Hello IP адрес имена и префиксы для hello виртуальную сеть и подсети.
   * Hello имена и идентификаторы hello виртуальной сети, подсистема балансировки нагрузки и сетевых интерфейсов.
   * Имена учетной записи хранения для hello учетных записей, связанных с машинами hello в наборе масштабирования hello.
   * Параметры для расширения диагностики, которая устанавливается на виртуальных машинах hello hello. Дополнительные сведения о hello расширения диагностики см. в разделе [создать Windows виртуальной машины с помощью мониторинга и диагностики с помощью шаблона Azure Resource Manager](../virtual-machines/windows/extensions-diagnostics-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).

4. Добавьте ресурс учетной записи хранения hello hello ресурсы родительского элемента, что вы добавили шаблон toohello. Этот шаблон использует hello toocreate цикла, рекомендуется использовать пять учетных записей хранилища, место хранения hello дисков операционной системы и диагностических данных. Этот набор учетных записей может поддерживать до too100 виртуальных машин в наборе масштабирования, — текущий максимум hello. Каждая учетная запись хранения называется с буквенный код, которое было определено в переменных hello, суффикс "hello", укажите в параметрах hello для шаблона hello.
   
        {
          "type": "Microsoft.Storage/storageAccounts",
          "name": "[concat(parameters('resourcePrefix'), variables('storageAccountSuffix')[copyIndex()])]",
          "apiVersion": "2015-06-15",
          "copy": {
            "name": "storageLoop",
            "count": 5
          },
          "location": "[resourceGroup().location]",
          "properties": { "accountType": "Standard_LRS" }
        },

5. Добавьте ресурс hello виртуальной сети. Дополнительную информацию см. в статье [Поставщик сетевых ресурсов](../virtual-network/resource-groups-networking.md).

    ```json
    {
      "apiVersion": "2015-06-15",
      "type": "Microsoft.Network/virtualNetworks",
      "name": "[variables('virtualNetworkName')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "addressSpace": { "addressPrefixes": [ "10.0.0.0/16" ] },
        "subnets": [
          {
            "name": "subnet1",
            "properties": { "addressPrefix": "10.0.0.0/24" }
          }
        ]
      }
    },
    ```

6. Добавьте hello открытые ресурсы IP-адресов, используемых hello Подсистема балансировки нагрузки и сетевого интерфейса.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP1')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName1')]"
        }
      }
    },
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/publicIPAddresses",
      "name": "[variables('publicIP2')]",
      "location": "[resourceGroup().location]",
      "properties": {
        "publicIPAllocationMethod": "Dynamic",
        "dnsSettings": {
          "domainNameLabel": "[variables('dnsName2')]"
        }
      }
    },
    ```

7. Добавьте ресурс балансировки нагрузки hello, который используется набором масштабирования hello. Дополнительные сведения см. в статье, посвященной [поддержке Azure Resource Manager для подсистемы балансировки нагрузки](../load-balancer/load-balancer-arm.md).

    ```json   
    {
      "apiVersion": "2015-06-15",
      "name": "[variables('loadBalancerName')]",
      "type": "Microsoft.Network/loadBalancers",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
      ],
      "properties": {
        "frontendIPConfigurations": [
          {
            "name": "loadBalancerFrontEnd",
            "properties": {
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses/', variables('publicIP1'))]"
              }
            }
          }
        ],
        "backendAddressPools": [ { "name": "bepool1" } ],
        "inboundNatPools": [
          {
            "name": "natpool1",
            "properties": {
              "frontendIPConfiguration": {
                "id": "[variables('frontEndIPConfigID')]"
              },
              "protocol": "tcp",
              "frontendPortRangeStart": 50000,
              "frontendPortRangeEnd": 50500,
              "backendPort": 22
            }
          }
        ]
      }
    },
    ```

8. Добавьте hello ресурс сетевого интерфейса, используемый hello отдельной виртуальной машине. Поскольку машины в наборе масштабирования не доступны через общедоступный IP-адрес, отдельная виртуальная машина создается в hello же виртуальных машин hello tooremotely доступа к сети.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Network/networkInterfaces",
      "name": "[variables('nicName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Network/publicIPAddresses/', variables('publicIP2'))]",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
      ],
      "properties": {
        "ipConfigurations": [
          {
            "name": "ipconfig1",
            "properties": {
              "privateIPAllocationMethod": "Dynamic",
              "publicIPAddress": {
                "id": "[resourceId('Microsoft.Network/publicIPAddresses', variables('publicIP2'))]"
              },
              "subnet": {
                "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
              }
            }
          }
        ]
      }
    },
    ```

9. Добавьте hello отдельной виртуальной машины в сетевых как набор масштабирования hello hello.

    ```json
    {
      "apiVersion": "2016-03-30",
      "type": "Microsoft.Compute/virtualMachines",
      "name": "[parameters('vmName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/networkInterfaces/', variables('nicName'))]"
      ],
      "properties": {
        "hardwareProfile": { "vmSize": "Standard_A1" },
        "osProfile": {
          "computername": "[parameters('vmName')]",
          "adminUsername": "[parameters('adminUsername')]",
          "adminPassword": "[parameters('adminPassword')]"
        },
        "storageProfile": {
          "imageReference": {
            "publisher": "Canonical",
            "offer": "UbuntuServer",
            "sku": "14.04.4-LTS",
            "version": "latest"
          },
          "osDisk": {
            "name": "[concat(parameters('resourcePrefix'), 'os1')]",
            "vhd": {
              "uri":  "[concat('https://',parameters('resourcePrefix'),'a.blob.core.windows.net/vhds/',parameters('resourcePrefix'),'os1.vhd')]"
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
        }
      }
    },
    ```

10. Добавление ресурса набора масштабирования виртуальных машин hello и укажите расширение диагностики hello, установленного на всех виртуальных машин в наборе масштабирования hello. Многие из параметров hello для этого ресурса похожи hello ресурса виртуальной машины. Ниже перечислены основные различия Hello hello емкости элемент, который задает hello количество виртуальных машин в наборе масштабирования hello и upgradePolicy, указывающее, каким образом производятся изменения toovirtual машины. Hello масштабный набор не создается, пока все учетные записи хранения hello создаются в соответствии с элементом dependsOn hello.

    ```json
    {
      "type": "Microsoft.Compute/virtualMachineScaleSets",
      "apiVersion": "2016-03-30",
      "name": "[parameters('vmSSName')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "storageLoop",
        "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]",
        "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]"
      ],
      "sku": {
        "name": "Standard_A1",
        "tier": "Standard",
        "capacity": "[parameters('instanceCount')]"
      },
      "properties": {
        "upgradePolicy": {
          "mode": "Manual"
        },
        "virtualMachineProfile": {
          "storageProfile": {
            "osDisk": {
              "vhdContainers": [
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[0],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[1],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[2],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[3],'.blob.core.windows.net/vmss')]",
                "[concat('https://', parameters('resourcePrefix'), variables('storageAccountSuffix')[4],'.blob.core.windows.net/vmss')]"
              ],
              "name": "vmssosdisk",
              "caching": "ReadOnly",
              "createOption": "FromImage"
            },
            "imageReference": {
              "publisher": "Canonical",
              "offer": "UbuntuServer",
              "sku": "14.04.4-LTS",
              "version": "latest"
            }
          },
          "osProfile": {
            "computerNamePrefix": "[parameters('vmSSName')]",
            "adminUsername": "[parameters('adminUsername')]",
            "adminPassword": "[parameters('adminPassword')]"
          },
          "networkProfile": {
            "networkInterfaceConfigurations": [
              {
                "name": "networkconfig1",
                "properties": {
                  "primary": "true",
                  "ipConfigurations": [
                    {
                      "name": "ip1",
                      "properties": {
                        "subnet": {
                          "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/virtualNetworks/',variables('virtualNetworkName'),'/subnets/subnet1')]"
                        },
                        "loadBalancerBackendAddressPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/backendAddressPools/bepool1')]"
                          }
                        ],
                        "loadBalancerInboundNatPools": [
                          {
                            "id": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Network/loadBalancers/',variables('loadBalancerName'),'/inboundNatPools/natpool1')]"
                          }
                        ]
                      }
                    }
                  ]
                }
              }
            ]
          },
          "extensionProfile": {
            "extensions": [
              {
                "name":"LinuxDiagnostic",
                "properties": {
                  "publisher":"Microsoft.OSTCExtensions",
                  "type":"LinuxDiagnostic",
                  "typeHandlerVersion":"2.1",
                  "autoUpgradeMinorVersion":false,
                  "settings": {
                    "xmlCfg":"[base64(concat(variables('wadcfgxstart'),variables('wadmetricsresourceid'),variables('wadcfgxend')))]",
                    "storageAccount":"[variables('diagnosticsStorageAccountName')]"
                  },
                  "protectedSettings": {
                    "storageAccountName":"[variables('diagnosticsStorageAccountName')]",
                    "storageAccountKey":"[listkeys(variables('accountid'), '2015-06-15').key1]",
                    "storageAccountEndPoint":"https://core.windows.net"
                  }
                }
              }
            ]
          }
        }
      }
    },
    ```

11. Добавьте ресурс autoscaleSettings hello, который определяет, как набор масштабирования hello корректирует зависимости от использования процессора на машинах hello в наборе hello.

    ```json
    {
      "type": "Microsoft.Insights/autoscaleSettings",
      "apiVersion": "2015-04-01",
      "name": "[concat(parameters('resourcePrefix'),'as1')]",
      "location": "[resourceGroup().location]",
      "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      ],
      "properties": {
        "enabled": true,
        "name": "[concat(parameters('resourcePrefix'),'as1')]",
        "profiles": [
          {
            "name": "Profile1",
            "capacity": {
              "minimum": "1",
              "maximum": "10",
              "default": "1"
            },
            "rules": [
              {
                "metricTrigger": {
                  "metricName": "\\Processor\\PercentProcessorTime",
                  "metricNamespace": "",
                  "metricResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/',resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]",
                  "timeGrain": "PT1M",
                  "statistic": "Average",
                  "timeWindow": "PT5M",
                  "timeAggregation": "Average",
                  "operator": "GreaterThan",
                  "threshold": 50.0
                },
                "scaleAction": {
                  "direction": "Increase",
                  "type": "ChangeCount",
                  "value": "1",
                  "cooldown": "PT5M"
                }
              }
            ]
          }
        ],
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId,'/resourceGroups/', resourceGroup().name,'/providers/Microsoft.Compute/virtualMachineScaleSets/',parameters('vmSSName'))]"
      }
    }
    ```
    
    Для целей этого руководства важны значения следующих параметров:
    
    * **metricName**  
    Это значение является hello то же, что счетчик производительности hello, которое было определено в переменной wadperfcounter hello. С помощью этой переменной, hello расширения диагностики собирает hello **Processor\PercentProcessorTime** счетчика.
    
    * **metricResourceUri**  
    Это значение является идентификатором ресурса hello hello набора масштабирования виртуальных машин.
    
    * **timegrain**  
    Это значение является гранулярности hello hello метрик, которые собираются. В этом шаблоне задается tooone минуты.
    
    * **statistic**  
    Это значение определяет, как метрики hello hello объединенный tooaccommodate автоматического масштабирования действия. Возможные значения Hello: Average, Min, Max. В этом шаблоне собираются hello среднее общее использование ЦП hello виртуальных машин.

    * **timeWindow**  
    Это значение является hello диапазон времени, в котором собираются данные экземпляра. Значение должно составлять от 5 минут до 12 часов.
    
    * **timeAggregation**  
    его значение определяет способ объединения собираемых данных hello со временем. значение по умолчанию Hello — среднее значение. Возможные значения Hello: среднее, минимальное, максимальное, конец, общее, число.
    
    * **operator**  
    Это значение является hello оператор, который используется toocompare hello метрики данных и hello порогового значения. Hello возможными значениями являются: равно NotEquals, GreaterThan, GreaterThanOrEqual, LessThan, LessThanOrEqual.
    
    * **threshold**  
    Это значение запускает действие масштабирования hello. В этом шаблоне машины добавляются в набор при hello средняя загрузка ЦП между машинами в наборе hello более чем на 50% toohello масштабирования.
    
    * **direction**  
    Это значение определяет hello действие, которое предпринимается, когда достигается пороговое значение hello. Возможные значения Hello: увеличиваются или уменьшаются. В этом шаблоне hello количество виртуальных машин в наборе масштабирования hello увеличивается, если пороговое значение hello более чем на 50% hello в определенный период времени.

    * **type**  
    Это значение является hello тип действия, которое должно выполняться и значением tooChangeCount.
    
    * **значение**  
    Это значение является hello число виртуальных машин, которые добавляются или удаляются из набора масштабирования hello. Для этого параметра должно быть указано значение не меньше 1. значение по умолчанию Hello-1. В этом шаблоне hello количество машин в шкале hello набора увеличивается на 1 при достижении порога hello.

    * **cooldown**  
    Это значение является hello объем toowait времени с момента последнего действия масштабирования hello, прежде чем произойдет следующее действие hello. Допустимые значения: от одной минуты до одной недели.

12. Сохраните файл шаблона hello.    

## <a name="step-3-upload-hello-template-toostorage"></a>Шаг 3: Отправка шаблона toostorage hello
можно загрузить шаблон Hello, при условии, что известно имя hello и первичный ключ учетной записи хранения hello, созданный на шаге 1.

1. В интерфейсе командной строки (Bash, терминалов, командной строке) выполните следующие команды переменные среды hello tooset необходимости tooaccess hello учетной записи хранения:

    ```cli   
    export AZURE_STORAGE_ACCOUNT={account_name}
    export AZURE_STORAGE_ACCESS_KEY={key}
    ```
    
    Hello ключ можно получить, щелкнув значок ключа hello при просмотре hello ресурс учетной записи хранения в hello портал Azure. Если вы используете командную строку Windows, введите **set** вместо export.

2. Создание контейнера hello для хранения шаблона hello.
   
    ```cli
    azure storage container create -p Blob templates
    ```

3. Отправьте новый контейнер файла шаблона toohello hello.
   
    ```cli
    azure storage blob upload VMSSTemplate.json templates VMSSTemplate.json
    ```

## <a name="step-4-deploy-hello-template"></a>Шаг 4: Развертывание шаблона hello
Теперь, когда вы создали шаблон hello, можно начать развертывание ресурсов hello. Используйте этот процесс hello toostart команды:

```cli
azure group deployment create --template-uri https://vmsstestsa.blob.core.windows.net/templates/VMSSTemplate.json vmsstestrg1 vmsstestdp1
```

При нажатии клавиши ВВОД, запрашиваемые tooprovide значения переменных hello, назначенные вами. Укажите следующие значения:

```cli
vmName: vmsstestvm1
vmSSName: vmsstest1
instanceCount: 5
adminUserName: vmadmin1
adminPassword: VMpass1
resourcePrefix: vmsstest
```

Для развертывания всех toosuccessfully ресурсы hello он займет около 15 минут.

> [!NOTE]
> Также можно использовать портал hello возможность toodeploy hello ресурсы. Используйте эту ссылку: https://portal.azure.com/#create/Microsoft.Template/uri/<link tooVM Scale Set JSON template>.


## <a name="step-5-monitor-resources"></a>Шаг 5. Мониторинг ресурсов
Сведения о масштабируемых наборах виртуальных машин можно получать, используя следующие методы:

* Здравствуйте, портал Azure — в настоящее время можно получить ограниченный объем информации с помощью портала hello.

* Hello [обозревателя ресурсов Azure](https://resources.azure.com/) -это средство — hello, наилучшим образом подходит для изучения hello текущее состояние набора масштабирования. Выполните этот путь, и вы увидите набор, созданный представление экземпляра hello hello шкалы:
  
    ```cli
    subscriptions > {your subscription} > resourceGroups > vmsstestrg1 > providers > Microsoft.Compute > virtualMachineScaleSets > vmsstest1 > virtualMachines
    ```

* Azure CLI - используйте этот tooget команда некоторые сведения:

    ```cli  
    azure resource show -n vmsstest1 -r Microsoft.Compute/virtualMachineScaleSets -o 2015-06-15 -g vmsstestrg1
    ```

* Подключение toohello jumpbox виртуальной машины, так же, как и любой другой компьютер и затем позволяет осуществлять удаленный доступ hello виртуальных машин в отдельных процессах набор масштабирования toomonitor hello.

> [!NOTE]
> Полный REST API для получения информации о масштабируемых наборах можно найти на странице [Масштабируемые наборы виртуальных машин](https://msdn.microsoft.com/library/mt589023.aspx).

## <a name="step-6-remove-hello-resources"></a>Шаг 6: Удаление ресурсов hello
Поскольку вы оплачивать ресурсы, используемые в Azure, это всегда ресурсов toodelete рекомендаций, которые больше не нужны. Не нужно toodelete каждого ресурса, отдельно от группы ресурсов. Можно удалить группу ресурсов hello и автоматически удаляются все ее ресурсы.

```cli
azure group delete vmsstestrg1
```

## <a name="next-steps"></a>Дальнейшие действия
* Просмотрите примеры функций мониторинга Azure Monitor в статье [Шаблоны для быстрого начала работы с межплатформенным интерфейсом командной строки Azure Monitor](../monitoring-and-diagnostics/insights-cli-samples.md).
* Дополнительные сведения о функции уведомлений в [используйте автомасштабирования действия toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-autoscale-to-webhook-email.md)
* Узнайте, каким образом слишком[журналы аудита используйте toosend электронной почты и веб-перехватчика уведомлений о предупреждениях в мониторе Azure](../monitoring-and-diagnostics/insights-auditlog-to-webhook-email.md)
* Извлечение hello [автомасштабирования нашего примера приложения на Ubuntu 16.04](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) шаблон, который настраивает hello tooexercise приложения Python и Фляга для автоматического масштабирования функциональность наборы масштабирования виртуальной машины.

