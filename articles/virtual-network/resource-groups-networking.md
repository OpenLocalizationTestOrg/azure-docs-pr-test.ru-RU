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
# <a name="network-resource-provider"></a><span data-ttu-id="7fb10-103">Поставщик сетевых ресурсов</span><span class="sxs-lookup"><span data-stu-id="7fb10-103">Network Resource Provider</span></span>
<span data-ttu-id="7fb10-104">Является основой в современных успешности бизнеса, связано hello toobuild возможности приложений и управление ими крупномасштабных сети виду образом agile, гибким, безопасным и repeatable.</span><span class="sxs-lookup"><span data-stu-id="7fb10-104">An underpinning need in today’s business success, is hello ability toobuild and manage large scale network aware applications in an agile, flexible, secure and repeatable way.</span></span> <span data-ttu-id="7fb10-105">Диспетчер ресурсов Azure позволяет вам toocreate таких приложений в виде единой коллекции ресурсов в группах ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-105">Azure Resource Manager enables you toocreate such applications, as a single collection of resources in resource groups.</span></span> <span data-ttu-id="7fb10-106">Для управления такими ресурсами используются различные поставщики ресурсов в Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="7fb10-106">Such resources are managed through various resource providers under Resource Manager.</span></span>

<span data-ttu-id="7fb10-107">Диспетчер ресурсов Azure использует доступ к ресурсам другого ресурса поставщики tooprovide tooyour.</span><span class="sxs-lookup"><span data-stu-id="7fb10-107">Azure Resource Manager relies on different resource providers tooprovide access tooyour resources.</span></span> <span data-ttu-id="7fb10-108">Существует три основных поставщика ресурсов: сеть, хранилище и вычисления.</span><span class="sxs-lookup"><span data-stu-id="7fb10-108">There are three main resource providers: Network, Storage and Compute.</span></span> <span data-ttu-id="7fb10-109">В этом документе рассматриваются hello характеристики и преимущества hello поставщика сетевых ресурсов, включая:</span><span class="sxs-lookup"><span data-stu-id="7fb10-109">This document discusses hello characteristics and benefits of hello Network Resource Provider, including:</span></span>

* <span data-ttu-id="7fb10-110">**Метаданные** — можно добавить с помощью тегов tooresources сведения.</span><span class="sxs-lookup"><span data-stu-id="7fb10-110">**Metadata** – you can add information tooresources using tags.</span></span> <span data-ttu-id="7fb10-111">Эти теги можно используется tootrack использования ресурсов в группах ресурсов и подписок.</span><span class="sxs-lookup"><span data-stu-id="7fb10-111">These tags can be used tootrack resource utilization across resource groups and subscriptions.</span></span>
* <span data-ttu-id="7fb10-112">**Повышенный контроль над сетью** : сетевые ресурсы нежестко связаны, и ими можно управлять более детально.</span><span class="sxs-lookup"><span data-stu-id="7fb10-112">**Greater control of your network** - network resources are loosely coupled and you can control them in a more granular fashion.</span></span> <span data-ttu-id="7fb10-113">Это означает, что у вас есть большую гибкость в управлении hello сетевых ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-113">This means you have more flexibility in managing hello networking resources.</span></span>
* <span data-ttu-id="7fb10-114">**Ускоренная настройка** : так как сетевые ресурсы нежестко связаны, вы можете создавать и организовывать сетевые ресурсы в параллельном режиме.</span><span class="sxs-lookup"><span data-stu-id="7fb10-114">**Faster configuration** - because network resources are loosely coupled, you can create and orchestrate network resources in parallel.</span></span> <span data-ttu-id="7fb10-115">Это значительно сокращает время настройки.</span><span class="sxs-lookup"><span data-stu-id="7fb10-115">This has drastically reduced configuration time.</span></span>
* <span data-ttu-id="7fb10-116">**Управление доступом на основе ролей** -RBAC предоставляет роли по умолчанию, в области безопасности, в дополнение tooallowing hello Создание пользовательских ролей для управления защитой.</span><span class="sxs-lookup"><span data-stu-id="7fb10-116">**Role Based Access Control** - RBAC provides default roles, with specific security scope, in addition tooallowing hello creation of custom roles for secure management.</span></span>
* <span data-ttu-id="7fb10-117">**Упрощение управления и развертывания** -он проще toodeploy и управлять приложениями, так как стек всего приложения можно можно создавать как единую коллекцию ресурсов в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-117">**Easier management and deployment** - it’s easier toodeploy and manage applications since you can can create an entire application stack as a single collection of resources in a resource group.</span></span> <span data-ttu-id="7fb10-118">И toodeploy быстрее, так как можно развернуть, просто указав полезные данные JSON шаблона.</span><span class="sxs-lookup"><span data-stu-id="7fb10-118">And faster toodeploy, since you can deploy by simply providing a template JSON payload.</span></span>
* <span data-ttu-id="7fb10-119">**Быстрой настройки** -можно использовать шаблоны в декларативном стиле tooenable repeatable быстрой настройки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="7fb10-119">**Rapid customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="7fb10-120">**REPEATABLE настройки** -можно использовать шаблоны в декларативном стиле tooenable repeatable быстрой настройки и развертывания.</span><span class="sxs-lookup"><span data-stu-id="7fb10-120">**Repeatable customization** - you can use declarative-style templates tooenable repeatable and rapid customization of deployments.</span></span>
* <span data-ttu-id="7fb10-121">**Интерфейсы управления** -можно использовать любой из следующих интерфейсов toomanage hello ресурсы:</span><span class="sxs-lookup"><span data-stu-id="7fb10-121">**Management interfaces** - you can use any of hello following interfaces toomanage your resources:</span></span>
  * <span data-ttu-id="7fb10-122">API на основе REST</span><span class="sxs-lookup"><span data-stu-id="7fb10-122">REST based API</span></span>
  * <span data-ttu-id="7fb10-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb10-123">PowerShell</span></span>
  * <span data-ttu-id="7fb10-124">ПАКЕТ SDK .NET</span><span class="sxs-lookup"><span data-stu-id="7fb10-124">.NET SDK</span></span>
  * <span data-ttu-id="7fb10-125">Пакет SDK для Node.js</span><span class="sxs-lookup"><span data-stu-id="7fb10-125">Node.JS SDK</span></span>
  * <span data-ttu-id="7fb10-126">Пакет SDK для Java</span><span class="sxs-lookup"><span data-stu-id="7fb10-126">Java SDK</span></span>
  * <span data-ttu-id="7fb10-127">Инфраструктура CLI Azure</span><span class="sxs-lookup"><span data-stu-id="7fb10-127">Azure CLI</span></span>
  * <span data-ttu-id="7fb10-128">Портал предварительной версии</span><span class="sxs-lookup"><span data-stu-id="7fb10-128">Preview Portal</span></span>
  * <span data-ttu-id="7fb10-129">Язык шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7fb10-129">Resource Manager template language</span></span>

## <a name="network-resources"></a><span data-ttu-id="7fb10-130">Сетевые ресурсы</span><span class="sxs-lookup"><span data-stu-id="7fb10-130">Network resources</span></span>
<span data-ttu-id="7fb10-131">Теперь вы можете управлять сетевыми ресурсам независимо друг от друга, а не через один вычислительный ресурс (виртуальную машину).</span><span class="sxs-lookup"><span data-stu-id="7fb10-131">You can now manage network resources independently, instead of having them all managed through a single compute resource (a virtual machine).</span></span> <span data-ttu-id="7fb10-132">Это обеспечивает более высокую степень гибкости и динамичности при создании сложной крупномасштабной инфраструктуры в группе ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-132">This ensures a higher degree of flexibility and agility in composing a complex and large scale infrastructure in a resource group.</span></span>

<span data-ttu-id="7fb10-133">Ниже показано концептуальное представление примера развертывания, включающего многоуровневое приложение.</span><span class="sxs-lookup"><span data-stu-id="7fb10-133">A conceptual view of a sample deployment involving a multi-tiered application is presented below.</span></span> <span data-ttu-id="7fb10-134">Всеми ресурсами, например сетевыми адаптерами, общедоступными IP-адресами и виртуальными машинами, можно управлять независимо друг от друга.</span><span class="sxs-lookup"><span data-stu-id="7fb10-134">Each resource you see, such as NICs, public IP addresses, and VMs, can be managed independently.</span></span>

![Модель сетевых ресурсов](./media/resource-groups-networking/Figure2.png)

<span data-ttu-id="7fb10-136">Каждый ресурс содержит как общий, так и собственный набор свойств.</span><span class="sxs-lookup"><span data-stu-id="7fb10-136">Every resource contains a common set of properties, and their individual property set.</span></span> <span data-ttu-id="7fb10-137">Hello распространенными свойствами являются:</span><span class="sxs-lookup"><span data-stu-id="7fb10-137">hello common properties are:</span></span>

| <span data-ttu-id="7fb10-138">Свойство</span><span class="sxs-lookup"><span data-stu-id="7fb10-138">Property</span></span> | <span data-ttu-id="7fb10-139">Описание</span><span class="sxs-lookup"><span data-stu-id="7fb10-139">Description</span></span> | <span data-ttu-id="7fb10-140">Примеры значений</span><span class="sxs-lookup"><span data-stu-id="7fb10-140">Sample values</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7fb10-141">**name**</span><span class="sxs-lookup"><span data-stu-id="7fb10-141">**name**</span></span> |<span data-ttu-id="7fb10-142">Уникальное имя ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fb10-142">Unique resource name.</span></span> <span data-ttu-id="7fb10-143">Для каждого типа ресурсов действуют свои ограничения на имена.</span><span class="sxs-lookup"><span data-stu-id="7fb10-143">Each resource type has its own naming restrictions.</span></span> |<span data-ttu-id="7fb10-144">PIP01, VM01, NIC01</span><span class="sxs-lookup"><span data-stu-id="7fb10-144">PIP01, VM01, NIC01</span></span> |
| <span data-ttu-id="7fb10-145">**расположение**</span><span class="sxs-lookup"><span data-stu-id="7fb10-145">**location**</span></span> |<span data-ttu-id="7fb10-146">Регион Azure, в которой hello находится ресурс</span><span class="sxs-lookup"><span data-stu-id="7fb10-146">Azure region in which hello resource resides</span></span> |<span data-ttu-id="7fb10-147">westus, eastus</span><span class="sxs-lookup"><span data-stu-id="7fb10-147">westus, eastus</span></span> |
| <span data-ttu-id="7fb10-148">**id**</span><span class="sxs-lookup"><span data-stu-id="7fb10-148">**id**</span></span> |<span data-ttu-id="7fb10-149">Уникальный идентификатор на основе универсального кода ресурса (URI)</span><span class="sxs-lookup"><span data-stu-id="7fb10-149">Unique URI based identification</span></span> |<span data-ttu-id="7fb10-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span><span class="sxs-lookup"><span data-stu-id="7fb10-150">/subscriptions/<subGUID>/resourceGroups/TestRG/providers/Microsoft.Network/publicIPAddresses/TestPIP</span></span> |

<span data-ttu-id="7fb10-151">Можно проверить hello отдельные свойства ресурсов в следующих разделах hello.</span><span class="sxs-lookup"><span data-stu-id="7fb10-151">You can check hello individual properties of resources in hello sections below.</span></span>

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

## <a name="management-interfaces"></a><span data-ttu-id="7fb10-152">Интерфейсы управления</span><span class="sxs-lookup"><span data-stu-id="7fb10-152">Management interfaces</span></span>
<span data-ttu-id="7fb10-153">Вы можете управлять сетевыми ресурсами Azure с помощью различных интерфейсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-153">You can manage your Azure networking resources using different interfaces.</span></span> <span data-ttu-id="7fb10-154">В этом документе основное внимание уделяется двум из этих интерфейсов: интерфейсу REST API и шаблонам.</span><span class="sxs-lookup"><span data-stu-id="7fb10-154">In this document we will focus on tow of those interfaces: REST API, and templates.</span></span>

### <a name="rest-api"></a><span data-ttu-id="7fb10-155">Интерфейс REST API</span><span class="sxs-lookup"><span data-stu-id="7fb10-155">REST API</span></span>
<span data-ttu-id="7fb10-156">Как упоминалось ранее, сетевыми ресурсами можно управлять через разнообразные интерфейсы, включая API REST, пакет SDK для .NET, пакет SDK для Node.JS, пакет SDK для Java, PowerShell, CLI, портал Azure и шаблоны.</span><span class="sxs-lookup"><span data-stu-id="7fb10-156">As mentioned earlier, network resources can be managed via a variety of interfaces, including REST API,.NET SDK, Node.JS SDK, Java SDK, PowerShell, CLI, Azure Portal and templates.</span></span>

<span data-ttu-id="7fb10-157">Hello Rest API соответствует toohello спецификации протокола HTTP 1.1.</span><span class="sxs-lookup"><span data-stu-id="7fb10-157">hello Rest API’s conform toohello HTTP 1.1 protocol specification.</span></span> <span data-ttu-id="7fb10-158">Общая структура URI Hello из hello API приведено ниже:</span><span class="sxs-lookup"><span data-stu-id="7fb10-158">hello general URI structure of hello API is presented below:</span></span>

    https://management.azure.com/subscriptions/{subscription-id}/providers/{resource-provider-namespace}/locations/{region-location}/register?api-version={api-version}

<span data-ttu-id="7fb10-159">И параметров hello в фигурных скобках представляют Привет следующие элементы:</span><span class="sxs-lookup"><span data-stu-id="7fb10-159">And hello parameters in braces represent hello following elements:</span></span>

* <span data-ttu-id="7fb10-160">**subscription-id** : идентификатор вашей подписки на Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb10-160">**subscription-id** - your Azure subscription id.</span></span>
* <span data-ttu-id="7fb10-161">**пространство имен поставщика ресурсов** -пространство имен для используемого поставщика hello.</span><span class="sxs-lookup"><span data-stu-id="7fb10-161">**resource-provider-namespace** - namespace for hello provider being used.</span></span> <span data-ttu-id="7fb10-162">Hello для поставщика сетевых ресурсов hello значение *Microsoft.Network*.</span><span class="sxs-lookup"><span data-stu-id="7fb10-162">hello value for hello network resource provider is *Microsoft.Network*.</span></span>
* <span data-ttu-id="7fb10-163">**имя региона** — имя региона Azure hello</span><span class="sxs-lookup"><span data-stu-id="7fb10-163">**region-name** - hello Azure region name</span></span>

<span data-ttu-id="7fb10-164">Hello следующие методы HTTP, поддерживаются при выполнении toohello вызовы REST API:</span><span class="sxs-lookup"><span data-stu-id="7fb10-164">hello following HTTP methods are supported when making calls toohello REST API:</span></span>

* <span data-ttu-id="7fb10-165">**ПОМЕСТИТЕ** — служат toocreate ресурсов данного типа, измените свойства ресурса или изменить связь между ресурсами.</span><span class="sxs-lookup"><span data-stu-id="7fb10-165">**PUT** - used toocreate a resource of a given type, modify a resource property or change an association between resources.</span></span>
* <span data-ttu-id="7fb10-166">**ПОЛУЧИТЬ** -использовала tooretrieve сведения для предоставленного ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fb10-166">**GET** - used tooretrieve information for a provisioned resource.</span></span>
* <span data-ttu-id="7fb10-167">**Удалить** -использовать toodelete существующего ресурса.</span><span class="sxs-lookup"><span data-stu-id="7fb10-167">**DELETE** - used toodelete an existing resource.</span></span>

<span data-ttu-id="7fb10-168">Hello запроса и ответа соответствует tooa формат полезных данных JSON.</span><span class="sxs-lookup"><span data-stu-id="7fb10-168">Both hello request and response conform tooa JSON payload format.</span></span> <span data-ttu-id="7fb10-169">Дополнительные сведения см. в статье [API управления ресурсами Azure](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span><span class="sxs-lookup"><span data-stu-id="7fb10-169">For more details, see [Azure Resource Management APIs](https://msdn.microsoft.com/library/azure/dn948464.aspx).</span></span>

### <a name="resource-manager-template-language"></a><span data-ttu-id="7fb10-170">Язык шаблонов Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7fb10-170">Resource Manager template language</span></span>
<span data-ttu-id="7fb10-171">В добавление ресурсов toomanaging принудительно (через API-интерфейсы или SDK) можно также использовать декларативного программирования toobuild стиль и управлять сетевым ресурсам с помощью hello язык шаблонов диспетчера ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-171">In addition toomanaging resources imperatively (via APIs or SDK), you can also use a declarative programming style toobuild and manage network resources by using hello Resource Manager Template Language.</span></span>

<span data-ttu-id="7fb10-172">Ниже приведен пример такого шаблона.</span><span class="sxs-lookup"><span data-stu-id="7fb10-172">A sample representation of a template is provided below –</span></span>

    {
      "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json",
      "contentVersion": "<version-number-of-template>",
      "parameters": { <parameter-definitions-of-template> },
      "variables": { <variable-definitions-of-template> },
      "resources": [ { <definition-of-resource-to-deploy> } ],
      "outputs": { <output-of-template> }    
    }

<span data-ttu-id="7fb10-173">шаблон Hello — в первую очередь JSON-Описание ресурсов hello и значения экземпляров hello введенного через параметры.</span><span class="sxs-lookup"><span data-stu-id="7fb10-173">hello template is primarily a JSON description of hello resources and hello instance values injected via parameters.</span></span> <span data-ttu-id="7fb10-174">пример Hello может быть toocreate используется виртуальная сеть с 2 подсетей.</span><span class="sxs-lookup"><span data-stu-id="7fb10-174">hello example below can be used toocreate a virtual network with 2 subnets.</span></span>

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

<span data-ttu-id="7fb10-175">У вас есть возможность hello вручную указать значения параметров hello, при использовании шаблона, или можно использовать файл параметров.</span><span class="sxs-lookup"><span data-stu-id="7fb10-175">You have hello option of providing hello parameter values manually when using a template, or you can use a parameter file.</span></span> <span data-ttu-id="7fb10-176">Hello приведенном ниже примере показан возможный набор toobe значения параметра, при использовании шаблона hello выше:</span><span class="sxs-lookup"><span data-stu-id="7fb10-176">hello example below shows a possible set of parameter values toobe used with hello template above:</span></span>

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


<span data-ttu-id="7fb10-177">Основные преимущества Hello с помощью шаблонов являются:</span><span class="sxs-lookup"><span data-stu-id="7fb10-177">hello main advantages of using templates are:</span></span>

* <span data-ttu-id="7fb10-178">Вы можете создать сложную инфраструктуру в группе ресурсов, используя декларативный стиль.</span><span class="sxs-lookup"><span data-stu-id="7fb10-178">You can build a complex infrastructure in a resource group in a declarative style.</span></span> <span data-ttu-id="7fb10-179">Hello orchestration создания hello ресурсы, включая управление зависимостями, обрабатываются диспетчером ресурсов.</span><span class="sxs-lookup"><span data-stu-id="7fb10-179">hello orchestration of creating hello resources, including dependency management, is handled by Resource Manager.</span></span>
* <span data-ttu-id="7fb10-180">Hello инфраструктуры могут создаваться repeatable образом в различных регионах и в пределах области, просто изменив параметры.</span><span class="sxs-lookup"><span data-stu-id="7fb10-180">hello infrastructure can be created in a repeatable way across various regions and within a region by simply changing parameters.</span></span>
* <span data-ttu-id="7fb10-181">декларативном стиле Hello приводит tooshorter периоду в построении шаблонов hello и развертывание инфраструктуры hello.</span><span class="sxs-lookup"><span data-stu-id="7fb10-181">hello declarative style leads tooshorter lead time in building hello templates and rolling out hello infrastructure.</span></span>

<span data-ttu-id="7fb10-182">Примеры шаблонов см. в разделе [шаблонов быстрого запуска Azure](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="7fb10-182">For sample templates, see [Azure quickstart templates](https://github.com/Azure/azure-quickstart-templates).</span></span>

<span data-ttu-id="7fb10-183">Дополнительные сведения о hello язык шаблонов диспетчера ресурсов см. в разделе [язык шаблонов диспетчера ресурсов Azure](../azure-resource-manager/resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="7fb10-183">For more information on hello Resource Manager Template Language, see [Azure Resource Manager Template Language](../azure-resource-manager/resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="7fb10-184">Образец Hello шаблона выше использует hello виртуальной сети и подсети ресурсы.</span><span class="sxs-lookup"><span data-stu-id="7fb10-184">hello sample template above uses hello virtual network and subnet resources.</span></span> <span data-ttu-id="7fb10-185">Существует и другие сетевые ресурсы, которые вы можете использовать. Они перечислены ниже.</span><span class="sxs-lookup"><span data-stu-id="7fb10-185">There are other network resources you can use as listed below:</span></span>

### <a name="using-a-template"></a><span data-ttu-id="7fb10-186">Использование шаблона</span><span class="sxs-lookup"><span data-stu-id="7fb10-186">Using a template</span></span>
<span data-ttu-id="7fb10-187">Можно развернуть tooAzure службы из шаблона с помощью PowerShell, AzureCLI, или путем выполнения toodeploy щелкните из GitHub.</span><span class="sxs-lookup"><span data-stu-id="7fb10-187">You can deploy services tooAzure from a template by using PowerShell, AzureCLI, or by performing a click toodeploy from GitHub.</span></span> <span data-ttu-id="7fb10-188">toodeploy службы из шаблона в GitHub, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="7fb10-188">toodeploy services from a template in GitHub, execute hello following steps:</span></span>

1. <span data-ttu-id="7fb10-189">Откройте файл template3 hello из GitHub.</span><span class="sxs-lookup"><span data-stu-id="7fb10-189">Open hello template3 file from GitHub.</span></span> <span data-ttu-id="7fb10-190">В качестве примера откройте страницу с шаблоном [Виртуальная сеть с двумя подсетями](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span><span class="sxs-lookup"><span data-stu-id="7fb10-190">As an example, open [Virtual network with two subnets](https://github.com/Azure/azure-quickstart-templates/tree/master/101-virtual-network).</span></span>
2. <span data-ttu-id="7fb10-191">Щелкните **развертывание tooAzure**, а затем войдите на toohello портал Azure с помощью учетных данных.</span><span class="sxs-lookup"><span data-stu-id="7fb10-191">Click on **Deploy tooAzure**, and then sign in on toohello Azure portal with your credentials.</span></span>
3. <span data-ttu-id="7fb10-192">Проверьте шаблон hello и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="7fb10-192">Verify hello template, and then click **Save**.</span></span>
4. <span data-ttu-id="7fb10-193">Нажмите кнопку **изменить параметры** и выберите расположение, например *Запад США*, hello виртуальной сети и подсетей.</span><span class="sxs-lookup"><span data-stu-id="7fb10-193">Click **Edit parameters** and select a location, such as *West US*, for hello vnet and subnets.</span></span>
5. <span data-ttu-id="7fb10-194">При необходимости измените hello **ADDRESSPREFIX** и **SUBNETPREFIX** параметры и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="7fb10-194">If necessary, change hello **ADDRESSPREFIX** and **SUBNETPREFIX** parameters, and then click **OK**.</span></span>
6. <span data-ttu-id="7fb10-195">Нажмите кнопку **выбрать группу ресурсов** и выберите в группе ресурсов hello виртуальной сети tooadd hello и подсетей.</span><span class="sxs-lookup"><span data-stu-id="7fb10-195">Click **Select a resource group** and then click on hello resource group you want tooadd hello vnet and subnets to.</span></span> <span data-ttu-id="7fb10-196">Кроме того, можно создать новую группу ресурсов, щелкнув **Создать новую**.</span><span class="sxs-lookup"><span data-stu-id="7fb10-196">Alternatively, you can create a new resource group by clicking **Or create new**.</span></span>
7. <span data-ttu-id="7fb10-197">Щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="7fb10-197">Click **Create**.</span></span> <span data-ttu-id="7fb10-198">Обратите внимание, hello отображение плитку **подготовки шаблона-развертывания**.</span><span class="sxs-lookup"><span data-stu-id="7fb10-198">Notice hello tile displaying **Provisioning Template deployment**.</span></span> <span data-ttu-id="7fb10-199">После завершения развертывания hello, вы увидите ниже tooone аналогичные экрана.</span><span class="sxs-lookup"><span data-stu-id="7fb10-199">Once hello deployment is done, you will see a screen similar tooone below.</span></span>

![Пример развертывания шаблона](./media/resource-groups-networking/Figure6.png)

## <a name="next-steps"></a><span data-ttu-id="7fb10-201">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7fb10-201">Next steps</span></span>
[<span data-ttu-id="7fb10-202">Язык шаблонов в диспетчере ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="7fb10-202">Azure Resource Manager Template Language</span></span>](../azure-resource-manager/resource-group-authoring-templates.md)

[<span data-ttu-id="7fb10-203">Сеть Azure: часто используемые шаблоны</span><span class="sxs-lookup"><span data-stu-id="7fb10-203">Azure Networking – commonly used templates</span></span>](https://github.com/Azure/azure-quickstart-templates)

[<span data-ttu-id="7fb10-204">Azure Resource Manager и классическое развертывание</span><span class="sxs-lookup"><span data-stu-id="7fb10-204">Azure Resource Manager vs. classic deployment</span></span>](../azure-resource-manager/resource-manager-deployment-model.md)

[<span data-ttu-id="7fb10-205">Общие сведения об Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="7fb10-205">Azure Resource Manager Overview</span></span>](../azure-resource-manager/resource-group-overview.md)

