---
title: "Общие сведения о поставщике ресурсов aaaNetwork | Документы Microsoft"
description: "Дополнительные сведения о hello новый поставщик ресурсов сети в диспетчере ресурсов Azure"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: 79bf09da-4809-45cb-8d21-705616ef24dc
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: 81b8f51fe8ee180d8f7885c6e04eb953904d7be5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="network-resource-provider"></a>Поставщик сетевых ресурсов
Является основой в современных успешности бизнеса, связано hello toobuild возможности приложений и управление ими крупномасштабных сети виду образом agile, гибким, безопасным и repeatable. Диспетчер ресурсов Azure позволяет вам toocreate таких приложений в виде единой коллекции ресурсов в группах ресурсов. Для управления такими ресурсами используются различные поставщики ресурсов в Azure Resource Manager.

Диспетчер ресурсов Azure использует доступ к ресурсам другого ресурса поставщики tooprovide tooyour. Существует три основных поставщика ресурсов: сеть, хранилище и вычисления. В этом документе рассматриваются hello характеристики и преимущества hello поставщика сетевых ресурсов, включая:

* **Метаданные** — можно добавить с помощью тегов tooresources сведения. Эти теги можно используется tootrack использования ресурсов в группах ресурсов и подписок.
* **Повышенный контроль над сетью** : сетевые ресурсы нежестко связаны, и ими можно управлять более детально. Это означает, что у вас есть большую гибкость в управлении hello сетевых ресурсов.
* **Ускоренная настройка** : так как сетевые ресурсы нежестко связаны, вы можете создавать и организовывать сетевые ресурсы в параллельном режиме. Это значительно сокращает время настройки.
* **Управление доступом на основе ролей** -RBAC предоставляет роли по умолчанию, в области безопасности, в дополнение tooallowing hello Создание пользовательских ролей для управления защитой.
* **Упрощение управления и развертывания** -он проще toodeploy и управлять приложениями, так как стек всего приложения можно можно создавать как единую коллекцию ресурсов в группе ресурсов. И toodeploy быстрее, так как можно развернуть, просто указав полезные данные JSON шаблона.
* **Быстрой настройки** -можно использовать шаблоны в декларативном стиле tooenable repeatable быстрой настройки и развертывания.
* **REPEATABLE настройки** -можно использовать шаблоны в декларативном стиле tooenable repeatable быстрой настройки и развертывания.
* **Интерфейсы управления** -можно использовать любой из следующих интерфейсов toomanage hello ресурсы:
  * API на основе REST
  * PowerShell
  * ПАКЕТ SDK .NET
  * Пакет SDK для Node.js
  * Пакет SDK для Java
  * Инфраструктура CLI Azure
  * Портал предварительной версии
  * Язык шаблонов Resource Manager

## <a name="network-resources"></a>Сетевые ресурсы
Теперь вы можете управлять сетевыми ресурсам независимо друг от друга, а не через один вычислительный ресурс (виртуальную машину). Это обеспечивает более высокую степень гибкости и динамичности при создании сложной крупномасштабной инфраструктуры в группе ресурсов.

Ниже показано концептуальное представление примера развертывания, включающего многоуровневое приложение. Всеми ресурсами, например сетевыми адаптерами, общедоступными IP-адресами и виртуальными машинами, можно управлять независимо друг от друга.

![Модель сетевых ресурсов](./media/resource-groups-networking/Figure2.png)

Каждый ресурс содержит как общий, так и собственный набор свойств. Hello распространенными свойствами являются:

| Свойство | Описание | Примеры значений |
| --- | --- | --- |
| **name** |Уникальное имя ресурса. Для каждого типа ресурсов действуют свои ограничения на имена. |PIP01, VM01, NIC01 |
| **расположение** |Регион Azure, в которой hello находится ресурс |westus, eastus |
| **id** |Уникальный идентификатор на основе универсального кода ресурса (URI) |/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP |

Можно проверить hello отдельные свойства ресурсов в следующих разделах hello.

[!INCLUDE [virtual-networks-nrp-pip-include](../../includes/virtual-networks-nrp-pip-include.md)]

[!INCLUDE [virtual-networks-nrp-nic-include](../../includes/virtual-networks-nrp-nic-include.md)]

[!INCLUDE [virtual-networks-nrp-nsg-include](../../includes/virtual-networks-nrp-nsg-include.md)]

[!INCLUDE [virtual-networks-nrp-udr-include](../../includes/virtual-networks-nrp-udr-include.md)]

[!INCLUDE [virtual-networks-nrp-vnet-include](../../includes/virtual-networks-nrp-vnet-include.md)]

[!INCLUDE [virtual-networks-nrp-dns-include](../../includes/virtual-networks-nrp-dns-include.md)]

[!INCLUDE [virtual-networks-nrp-lb-include](../../includes/virtual-networks-nrp-lb-include.md)]

[!INCLUDE [virtual-networks-nrp-appgw-include](../../includes/virtual-networks-nrp-appgw-include.md)]

[!INCLUDE [virtual-networks-nrp-vpn-include](../../includes/virtual-networks-nrp-vpn-include.md)]

[!INCLUDE [virtual-networks-nrp-tm-include](../../includes/virtual-networks-nrp-tm-include.md)]

## <a name="management-interfaces"></a>Интерфейсы управления
Вы можете управлять сетевыми ресурсами Azure с помощью различных интерфейсов. В этом документе основное внимание уделяется двум из этих интерфейсов: интерфейсу REST API и шаблонам.

### <a name="rest-api"></a>Интерфейс REST API
Как упоминалось ранее, сетевыми ресурсами можно управлять через разнообразные интерфейсы, включая API REST, пакет SDK для .NET, пакет SDK для Node.JS, пакет SDK для Java, PowerShell, CLI, портал Azure и шаблоны.

Hello Rest API соответствует toohello спецификации протокола HTTP 1.1. Общая структура URI Hello из hello API приведено ниже:

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

И параметров hello в фигурных скобках представляют Привет следующие элементы:

* **subscription-id** : идентификатор вашей подписки на Azure.
* **пространство имен поставщика ресурсов** -пространство имен для используемого поставщика hello. Hello для поставщика сетевых ресурсов hello значение *Microsoft.Network*.
* **имя региона** — имя региона Azure hello

Hello следующие методы HTTP, поддерживаются при выполнении toohello вызовы REST API:

* **ПОМЕСТИТЕ** — служат toocreate ресурсов данного типа, измените свойства ресурса или изменить связь между ресурсами.
* **ПОЛУЧИТЬ** -использовала tooretrieve сведения для предоставленного ресурса.
* **Удалить** -использовать toodelete существующего ресурса.

Hello запроса и ответа соответствует tooa формат полезных данных JSON. Дополнительные сведения см. в статье [API управления ресурсами Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).

### <a name="resource-manager-template-language"></a>Язык шаблонов Resource Manager
В добавление ресурсов toomanaging принудительно (через API-интерфейсы или SDK) можно также использовать декларативного программирования toobuild стиль и управлять сетевым ресурсам с помощью hello язык шаблонов диспетчера ресурсов.

Ниже приведен пример такого шаблона.

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

шаблон Hello — в первую очередь JSON-Описание ресурсов hello и значения экземпляров hello введенного через параметры. пример Hello может быть toocreate используется виртуальная сеть с 2 подсетей.

    {
        "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/VNET.json",
        "contentVersion": "1.0.0.0",
        "parameters" : {
          "location": {
            "type": "String",
            "allowedValues": ["East US", "West US", "West Europe", "East Asia", "South East Asia"],
            "metadata" : {
              "Description" : "Deployment location"
            }
          },
          "virtualNetworkName":{
            "type" : "string",
            "defaultValue":"myVNET",
            "metadata" : {
              "Description" : "VNET name"
            }
          },
          "addressPrefix":{
            "type" : "string",
            "defaultValue" : "10.0.0.0/16",
            "metadata" : {
              "Description" : "Address prefix"
            }

          },
          "subnet1Name": {
            "type" : "string",
            "defaultValue" : "Subnet-1",
            "metadata" : {
              "Description" : "Subnet 1 Name"
            }
          },
          "subnet2Name": {
            "type" : "string",
            "defaultValue" : "Subnet-2",
            "metadata" : {
              "Description" : "Subnet 2 name"
            }
          },
          "subnet1Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.0.0/24",
            "metadata" : {
              "Description" : "Subnet 1 Prefix"
            }
          },
          "subnet2Prefix" : {
            "type" : "string",
            "defaultValue" : "10.0.1.0/24",
            "metadata" : {
              "Description" : "Subnet 2 Prefix"
            }
          }
        },
        "resources": [
        {
          "apiVersion": "2015-05-01-preview",
          "type": "Microsoft.Network/virtualNetworks",
          "name": "[parameters('virtualNetworkName')]",
          "location": "[parameters('location')]",
          "properties": {
            "addressSpace": {
              "addressPrefixes": [
                "[parameters('addressPrefix')]"
              ]
            },
            "subnets": [
              {
                "name": "[parameters('subnet1Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet1Prefix')]"
                }
              },
              {
                "name": "[parameters('subnet2Name')]",
                "properties" : {
                  "addressPrefix": "[parameters('subnet2Prefix')]"
                }
              }
            ]
          }
        }
        ]
    }

У вас есть возможность hello вручную указать значения параметров hello, при использовании шаблона, или можно использовать файл параметров. Hello приведенном ниже примере показан возможный набор toobe значения параметра, при использовании шаблона hello выше:

    {
      "location": {
          "value": "East US"
      },
      "virtualNetworkName": {
          "value": "VNET1"
      },
      "subnet1Name": {
          "value": "Subnet1"
      },
      "subnet2Name": {
          "value": "Subnet2"
      },
      "addressPrefix": {
          "value": "192.168.0.0/16"
      },
      "subnet1Prefix": {
          "value": "192.168.1.0/24"
      },
      "subnet2Prefix": {
          "value": "192.168.2.0/24"
      }
    }


Основные преимущества Hello с помощью шаблонов являются:

* Вы можете создать сложную инфраструктуру в группе ресурсов, используя декларативный стиль. Hello orchestration создания hello ресурсы, включая управление зависимостями, обрабатываются диспетчером ресурсов.
* Hello инфраструктуры могут создаваться repeatable образом в различных регионах и в пределах области, просто изменив параметры.
* декларативном стиле Hello приводит tooshorter периоду в построении шаблонов hello и развертывание инфраструктуры hello.

Примеры шаблонов см. в разделе [шаблонов быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates).

Дополнительные сведения о hello язык шаблонов диспетчера ресурсов см. в разделе [язык шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Образец Hello шаблона выше использует hello виртуальной сети и подсети ресурсы. Существует и другие сетевые ресурсы, которые вы можете использовать. Они перечислены ниже.

### <a name="using-a-template"></a>Использование шаблона
Можно развернуть tooAzure службы из шаблона с помощью PowerShell, AzureCLI, или путем выполнения toodeploy щелкните из GitHub. toodeploy службы из шаблона в GitHub, выполните следующие шаги hello:

1. Откройте файл template3 hello из GitHub. В качестве примера откройте страницу с шаблоном [Виртуальная сеть с двумя подсетями](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).
2. Щелкните **развертывание tooAzure**, а затем войдите на toohello портал Azure с помощью учетных данных.
3. Проверьте шаблон hello и нажмите кнопку **Сохранить**.
4. Нажмите кнопку **изменить параметры** и выберите расположение, например *Запад США*, hello виртуальной сети и подсетей.
5. При необходимости измените hello **ADDRESSPREFIX** и **SUBNETPREFIX** параметры и нажмите кнопку **ОК**.
6. Нажмите кнопку **выбрать группу ресурсов** и выберите в группе ресурсов hello виртуальной сети tooadd hello и подсетей. Кроме того, можно создать новую группу ресурсов, щелкнув **Создать новую**.
7. Щелкните **Создать**. Обратите внимание, hello отображение плитку **подготовки шаблона-развертывания**. После завершения развертывания hello, вы увидите ниже tooone аналогичные экрана.

![Пример развертывания шаблона](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a>Дальнейшие действия
[Язык шаблонов в диспетчере ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Сеть Azure: часто используемые шаблоны](https://github.com/Azure/azure-quickstart-templates)

[Azure Resource Manager и классическое развертывание](../azure-resource-manager/resource-manager-deployment-model.md)

[Общие сведения об Azure Resource Manager](../azure-resource-manager/resource-group-overview.md)

