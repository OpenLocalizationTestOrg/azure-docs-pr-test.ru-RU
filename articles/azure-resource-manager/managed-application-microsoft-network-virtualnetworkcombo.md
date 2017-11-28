---
title: "элемент управляемого пользовательского интерфейса приложения VirtualNetworkCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="57ee7-103">Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo</span><span class="sxs-lookup"><span data-stu-id="57ee7-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="57ee7-104">Группа элементов управления для выбора новой или имеющейся виртуальной сети.</span><span class="sxs-lookup"><span data-stu-id="57ee7-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="57ee7-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="57ee7-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="57ee7-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="57ee7-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="57ee7-108">В верхней каркаса hello пользователь hello выбравший новую виртуальную сеть, поэтому hello пользователь может настроить префикса имя и адрес каждой подсети.</span><span class="sxs-lookup"><span data-stu-id="57ee7-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="57ee7-109">Настройка подсетей в этом случае является необязательной.</span><span class="sxs-lookup"><span data-stu-id="57ee7-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="57ee7-110">В каркас нижней hello hello пользователь, выбравший существующей виртуальной сети, поэтому hello пользователя необходимо сопоставить каждой подсети hello развертывания шаблона требуется tooan существующей подсети.</span><span class="sxs-lookup"><span data-stu-id="57ee7-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="57ee7-111">Настройка подсетей в этом случае является обязательной.</span><span class="sxs-lookup"><span data-stu-id="57ee7-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="57ee7-112">Схема</span><span class="sxs-lookup"><span data-stu-id="57ee7-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="57ee7-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="57ee7-113">Remarks</span></span>
- <span data-ttu-id="57ee7-114">Если указано, hello первый неперекрывающиеся префикс адреса размер `defaultValue.addressPrefixSize` определяется автоматически на основании существующих виртуальных сетей в подписке hello пользователя.</span><span class="sxs-lookup"><span data-stu-id="57ee7-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="57ee7-115">Здравствуйте, значение по умолчанию для `defaultValue.name` и `defaultValue.addressPrefixSize` — **null**.</span><span class="sxs-lookup"><span data-stu-id="57ee7-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="57ee7-116">Обязательно должен быть указан параметр `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="57ee7-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="57ee7-117">Все существующие виртуальные сети с адресным пространством меньше, чем hello указанное значение, становятся недоступными для выбора.</span><span class="sxs-lookup"><span data-stu-id="57ee7-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="57ee7-118">Для каждой подсети должны быть определены `subnets` и `constraints.minAddressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="57ee7-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="57ee7-119">При создании новой виртуальной сети, префикс адреса для каждой подсети вычисляется автоматически на основе префикса адреса hello виртуальной сети, а соответствующее `addressPrefixSize`.</span><span class="sxs-lookup"><span data-stu-id="57ee7-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="57ee7-120">При использовании имеющейся виртуальной сети любые подсети со значением меньше, чем у `constraints.minAddressPrefixSize`, — недоступны.</span><span class="sxs-lookup"><span data-stu-id="57ee7-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="57ee7-121">Кроме того (если указано), подсети, которые не содержат минимальное число доступных адресов (`minAddressCount`), — недоступны.</span><span class="sxs-lookup"><span data-stu-id="57ee7-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="57ee7-122">значение по умолчанию Hello — **0**.</span><span class="sxs-lookup"><span data-stu-id="57ee7-122">hello default value is **0**.</span></span> <span data-ttu-id="57ee7-123">tooensure, hello доступных адресов являются смежными, укажите **true** для `requireContiguousAddresses`.</span><span class="sxs-lookup"><span data-stu-id="57ee7-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="57ee7-124">значение по умолчанию Hello — **true**.</span><span class="sxs-lookup"><span data-stu-id="57ee7-124">hello default value is **true**.</span></span>
- <span data-ttu-id="57ee7-125">Создание подсетей в имеющейся виртуальной сети не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="57ee7-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="57ee7-126">Если `options.hideExisting` — **true**, hello пользователь не может выбрать существующую виртуальную сеть.</span><span class="sxs-lookup"><span data-stu-id="57ee7-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="57ee7-127">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="57ee7-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="57ee7-128">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="57ee7-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="57ee7-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="57ee7-129">Next steps</span></span>
* <span data-ttu-id="57ee7-130">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57ee7-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="57ee7-131">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="57ee7-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="57ee7-132">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="57ee7-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
