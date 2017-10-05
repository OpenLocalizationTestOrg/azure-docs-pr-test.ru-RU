---
title: "Элемент пользовательского интерфейса PublicIpAddressCombo управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="d199b-103">Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="d199b-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="d199b-104">Группа элементов управления для выбора нового или имеющегося общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d199b-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="d199b-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="d199b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d199b-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="d199b-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="d199b-108">Если для общедоступного IP-адреса выбрано значение "Нет", текстовое поле метки доменного имени будет скрыто.</span><span class="sxs-lookup"><span data-stu-id="d199b-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="d199b-109">Если выбран имеющийся общедоступный IP-адрес, текстовое поле метки доменного имени будет отключено.</span><span class="sxs-lookup"><span data-stu-id="d199b-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="d199b-110">Его значение является меткой доменного имени выбранного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d199b-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="d199b-111">Суффикс доменного имени (например, westus.cloudapp.azure.com) обновляется автоматически на основе выбранного расположения.</span><span class="sxs-lookup"><span data-stu-id="d199b-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="d199b-112">Схема</span><span class="sxs-lookup"><span data-stu-id="d199b-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d199b-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="d199b-113">Remarks</span></span>
- <span data-ttu-id="d199b-114">Если для параметра `constraints.required.domainNameLabel` задано значение **true**, пользователю необходимо указать метку доменного имени при создании общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="d199b-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="d199b-115">Имеющиеся общедоступные IP-адреса без метки недоступны для выбора.</span><span class="sxs-lookup"><span data-stu-id="d199b-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="d199b-116">Если для параметра `options.hideNone` задано значение **true**, значение **Нет** для общедоступного IP-адреса будет скрыто.</span><span class="sxs-lookup"><span data-stu-id="d199b-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="d199b-117">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="d199b-117">The default value is **false**.</span></span>
- <span data-ttu-id="d199b-118">Если для параметра `options.hideDomainNameLabel` задано значение **true**, текстовое поле для метки доменного имени будет скрыто.</span><span class="sxs-lookup"><span data-stu-id="d199b-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="d199b-119">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="d199b-119">The default value is **false**.</span></span>
- <span data-ttu-id="d199b-120">Если для параметра `options.hideExisting` задано значение true, пользователь не сможет выбрать имеющийся общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="d199b-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="d199b-121">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="d199b-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d199b-122">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="d199b-122">Sample output</span></span>
<span data-ttu-id="d199b-123">Если общедоступный IP-адрес не выбран, ожидаются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d199b-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="d199b-124">Если выбран новый или имеющийся IP-адрес, ожидаются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="d199b-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="d199b-125">При указании `options.hideNone` `newOrExistingOrNone` всегда возвращает значение **none**.</span><span class="sxs-lookup"><span data-stu-id="d199b-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="d199b-126">При указании `options.hideDomainNameLabel` `domainNameLabel` не объявляется.</span><span class="sxs-lookup"><span data-stu-id="d199b-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d199b-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d199b-127">Next steps</span></span>
* <span data-ttu-id="d199b-128">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d199b-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d199b-129">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d199b-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d199b-130">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="d199b-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
