---
title: "Элемент пользовательского интерфейса VirtualNetworkCombo управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo для управляемых приложений Azure"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="159b6-103">Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="159b6-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="159b6-104">Группа элементов управления для выбора новой или имеющейся виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="159b6-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="159b6-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="159b6-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="159b6-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="159b6-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="159b6-108">В верхней области каркаса пользователь выбрал новую виртуальную сеть. Теперь он может настроить префикс адреса и имя каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="159b6-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="159b6-109">Настройка подсетей в этом случае является необязательной.</span><span class="sxs-lookup"><span data-stu-id="159b6-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="159b6-110">В нижней области каркаса пользователь выбрал имеющуюся виртуальную сеть. Теперь он должен сопоставить каждую подсеть, необходимую шаблону развертывания, с имеющейся подсетью.</span><span class="sxs-lookup"><span data-stu-id="159b6-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="159b6-111">Настройка подсетей в этом случае является обязательной.</span><span class="sxs-lookup"><span data-stu-id="159b6-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="159b6-112">Схема</span><span class="sxs-lookup"><span data-stu-id="159b6-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="159b6-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="159b6-113">Remarks</span></span>
- <span data-ttu-id="159b6-114">Если указан, первый префикс адреса размера `defaultValue.addressPrefixSize`, который не перекрывается, автоматически определяется на основе имеющихся виртуальных сетей в подписке пользователя.</span><span class="sxs-lookup"><span data-stu-id="159b6-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="159b6-115">Значение по умолчанию для параметров `defaultValue.name` и `defaultValue.addressPrefixSize` — **null**.</span><span class="sxs-lookup"><span data-stu-id="159b6-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="159b6-116">Обязательно должен быть указан параметр `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="159b6-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="159b6-117">Любые имеющиеся виртуальные сети с адресным пространством меньше указанного значения являются недоступными.</span><span class="sxs-lookup"><span data-stu-id="159b6-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="159b6-118">Для каждой подсети должны быть определены `subnets` и `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="159b6-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="159b6-119">При создании виртуальной сети префикс адреса каждой подсети определяется автоматически на основе префикса адреса виртуальной сети и `addressPrefixSize` соответственно.</span><span class="sxs-lookup"><span data-stu-id="159b6-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="159b6-120">При использовании имеющейся виртуальной сети любые подсети со значением меньше, чем у `constraints.minAddressPrefixSize`, — недоступны.</span><span class="sxs-lookup"><span data-stu-id="159b6-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="159b6-121">Кроме того (если указано), подсети, которые не содержат минимальное число доступных адресов (`minAddressCount`), — недоступны.</span><span class="sxs-lookup"><span data-stu-id="159b6-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="159b6-122">Значение по умолчанию — **0**.</span><span class="sxs-lookup"><span data-stu-id="159b6-122">The default value is **0**.</span></span> <span data-ttu-id="159b6-123">Чтобы адреса были связанными, задайте значение **true** для `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="159b6-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="159b6-124">Значение по умолчанию — **true**.</span><span class="sxs-lookup"><span data-stu-id="159b6-124">The default value is **true**.</span></span>
- <span data-ttu-id="159b6-125">Создание подсетей в имеющейся виртуальной сети не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="159b6-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="159b6-126">Если для параметра `options.hideExisting` задано значение **true**, пользователь не может выбрать имеющуюся виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="159b6-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="159b6-127">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="159b6-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="159b6-128">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="159b6-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="159b6-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="159b6-129">Next steps</span></span>
* <span data-ttu-id="159b6-130">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="159b6-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="159b6-131">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="159b6-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="159b6-132">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="159b6-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
