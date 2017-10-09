---
title: "элемент управляемого пользовательского интерфейса приложения PublicIpAddressCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="197d5-103">Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo</span><span class="sxs-lookup"><span data-stu-id="197d5-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="197d5-104">Группа элементов управления для выбора нового или имеющегося общедоступного IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="197d5-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="197d5-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="197d5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="197d5-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="197d5-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="197d5-108">Если пользователь hello выбирает «None» для общедоступного IP-адреса, hello домена имя метки текстовое поле будет скрыта.</span><span class="sxs-lookup"><span data-stu-id="197d5-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="197d5-109">Если пользователь hello выбирает существующий общедоступный IP-адрес, hello домена имя метки текстовое поле будет отключено.</span><span class="sxs-lookup"><span data-stu-id="197d5-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="197d5-110">Его значением является метка доменного имени hello hello выбранных IP-адреса.</span><span class="sxs-lookup"><span data-stu-id="197d5-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="197d5-111">Здравствуйте обновлений суффикс (например, westus.cloudapp.azure.com) имя домена, автоматически на основе hello выбранного расположения.</span><span class="sxs-lookup"><span data-stu-id="197d5-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="197d5-112">Схема</span><span class="sxs-lookup"><span data-stu-id="197d5-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="197d5-113">Примечания</span><span class="sxs-lookup"><span data-stu-id="197d5-113">Remarks</span></span>
- <span data-ttu-id="197d5-114">Если `constraints.required.domainNameLabel` задано слишком**true**, hello пользователь должен предоставить метку имени домена, создавая новый общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="197d5-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="197d5-115">Имеющиеся общедоступные IP-адреса без метки недоступны для выбора.</span><span class="sxs-lookup"><span data-stu-id="197d5-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="197d5-116">Если `options.hideNone` задано слишком**true**, затем hello параметр tooselect **нет** hello открытый IP-адрес скрыт.</span><span class="sxs-lookup"><span data-stu-id="197d5-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="197d5-117">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="197d5-117">hello default value is **false**.</span></span>
- <span data-ttu-id="197d5-118">Если `options.hideDomainNameLabel` задано слишком**true**, скрыта hello текстовое поле для метка доменного имени.</span><span class="sxs-lookup"><span data-stu-id="197d5-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="197d5-119">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="197d5-119">hello default value is **false**.</span></span>
- <span data-ttu-id="197d5-120">Если `options.hideExisting` имеет значение true, то пользователь hello не может toochoose существующий общедоступный IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="197d5-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="197d5-121">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="197d5-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="197d5-122">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="197d5-122">Sample output</span></span>
<span data-ttu-id="197d5-123">Если hello пользователь выбирает не общедоступный IP-адрес, hello следующий результат является ожидаемым:</span><span class="sxs-lookup"><span data-stu-id="197d5-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="197d5-124">Если hello пользователь выбирает новый или существующий IP-адрес, hello следующий результат является ожидаемым:</span><span class="sxs-lookup"><span data-stu-id="197d5-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="197d5-125">При указании `options.hideNone` `newOrExistingOrNone` всегда возвращает значение **none**.</span><span class="sxs-lookup"><span data-stu-id="197d5-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="197d5-126">При указании `options.hideDomainNameLabel` `domainNameLabel` не объявляется.</span><span class="sxs-lookup"><span data-stu-id="197d5-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="197d5-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="197d5-127">Next steps</span></span>
* <span data-ttu-id="197d5-128">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="197d5-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="197d5-129">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="197d5-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="197d5-130">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="197d5-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
