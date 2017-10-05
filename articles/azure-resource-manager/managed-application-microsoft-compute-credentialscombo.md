---
title: "Элемент пользовательского интерфейса CredentialsCombo управляемого приложения Azure | Документация Майкрософт"
description: "Сведения об элементе пользовательского интерфейса Microsoft.Compute.CredentialsCombo для управляемых приложений Azure"
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
ms.openlocfilehash: 254f383ee6f7cb9f7051fa135d85319a22c3c369
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="0fe56-103">Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="0fe56-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="0fe56-104">Группа элементов управления со встроенной проверкой паролей и открытых ключей SSH для Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="0fe56-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="0fe56-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="0fe56-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0fe56-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="0fe56-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="0fe56-108">Схема</span><span class="sxs-lookup"><span data-stu-id="0fe56-108">Schema</span></span>
<span data-ttu-id="0fe56-109">Если параметр `osPlatform` имеет значение **Windows**, используется следующая схема:</span><span class="sxs-lookup"><span data-stu-id="0fe56-109">If `osPlatform` is **Windows**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": {
    "password": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="0fe56-110">Если параметр `osPlatform` имеет значение **Linux**, используется следующая схема:</span><span class="sxs-lookup"><span data-stu-id="0fe56-110">If `osPlatform` is **Linux**, then the following schema is used:</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.CredentialsCombo",
  "label": {
    "authenticationType": "Authentication type",
    "password": "Password",
    "confirmPassword": "Confirm password",
    "sshPublicKey": "SSH public key"
  },
  "toolTip": {
    "authenticationType": "",
    "password": "",
    "sshPublicKey": ""
  },
  "constraints": {
    "required": true,
    "customPasswordRegex": "^(?=.*[A-Za-z])(?=.*\\d)[A-Za-z\\d]{8,}$",
    "customValidationMessage": "The password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0fe56-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="0fe56-111">Remarks</span></span>
- <span data-ttu-id="0fe56-112">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="0fe56-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="0fe56-113">Если для параметра `constraints.required` задано значение **true**, то текстовые поля для пароля и открытого ключа SSH должны содержать значения, чтобы пройти проверку.</span><span class="sxs-lookup"><span data-stu-id="0fe56-113">If `constraints.required` is set to **true**, then the password or SSH public key text boxes must contain values to validate successfully.</span></span> <span data-ttu-id="0fe56-114">Значение по умолчанию — **true**.</span><span class="sxs-lookup"><span data-stu-id="0fe56-114">The default value is **true**.</span></span>
- <span data-ttu-id="0fe56-115">Если для параметра `options.hideConfirmation` задано значение **true**, второе текстовое поле для подтверждения пароля скрыто.</span><span class="sxs-lookup"><span data-stu-id="0fe56-115">If `options.hideConfirmation` is set to **true**, then the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="0fe56-116">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="0fe56-116">The default value is **false**.</span></span>
- <span data-ttu-id="0fe56-117">Если для параметра `options.hidePassword` задано значение **true**, возможность использования проверки пароля скрыта.</span><span class="sxs-lookup"><span data-stu-id="0fe56-117">If `options.hidePassword` is set to **true**, then the option to use password authentication is hidden.</span></span> <span data-ttu-id="0fe56-118">Его можно использовать только тогда, когда параметр `osPlatform` имеет значение **Linux**.</span><span class="sxs-lookup"><span data-stu-id="0fe56-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="0fe56-119">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="0fe56-119">The default value is **false**.</span></span>
- <span data-ttu-id="0fe56-120">Дополнительные ограничения на разрешенные пароли можно реализовать с помощью свойства `customPasswordRegex`.</span><span class="sxs-lookup"><span data-stu-id="0fe56-120">Additional constraints on the allowed passwords can be implemented by using the `customPasswordRegex` property.</span></span> <span data-ttu-id="0fe56-121">Строка в `customValidationMessage` отображается, если пароль не прошел пользовательскую проверку.</span><span class="sxs-lookup"><span data-stu-id="0fe56-121">The string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="0fe56-122">Значение по умолчанию для обоих свойств — **null**.</span><span class="sxs-lookup"><span data-stu-id="0fe56-122">The default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0fe56-123">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="0fe56-123">Sample output</span></span>
<span data-ttu-id="0fe56-124">Если параметр `osPlatform` имеет значение **Windows** или пользователь указал пароль вместо открытого ключа SSH, ожидаются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0fe56-124">If `osPlatform` is **Windows**, or the user provided a password instead of an SSH public key, then the following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="0fe56-125">Если пользователь предоставил открытый ключ SSH, ожидаются следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="0fe56-125">If the user provided an SSH public key, then the following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="0fe56-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0fe56-126">Next steps</span></span>
* <span data-ttu-id="0fe56-127">Общие сведения об управляемых приложениях Azure см. в [этой статье](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0fe56-127">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0fe56-128">Общие сведения о создании определений пользовательского интерфейса см. в статье [Начало работы с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0fe56-128">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0fe56-129">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="0fe56-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
