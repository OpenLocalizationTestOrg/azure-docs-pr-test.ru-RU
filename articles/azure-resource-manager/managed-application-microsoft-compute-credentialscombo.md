---
title: "элемент управляемого пользовательского интерфейса приложения CredentialsCombo aaaAzure | Документы Microsoft"
description: "Описывает hello элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo для управляемых приложений Azure"
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
ms.openlocfilehash: d44a3929ebb7a5ff78b72f9eaeb6e52b098e266f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputecredentialscombo-ui-element"></a><span data-ttu-id="4d512-103">Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo</span><span class="sxs-lookup"><span data-stu-id="4d512-103">Microsoft.Compute.CredentialsCombo UI element</span></span>
<span data-ttu-id="4d512-104">Группа элементов управления со встроенной проверкой паролей и открытых ключей SSH для Windows и Linux.</span><span class="sxs-lookup"><span data-stu-id="4d512-104">A group of controls with built-in validation for Windows and Linux passwords and SSH public keys.</span></span> <span data-ttu-id="4d512-105">Этот элемент используется при [создании управляемого приложения Azure](managed-application-publishing.md).</span><span class="sxs-lookup"><span data-stu-id="4d512-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="4d512-106">Пример элемента пользовательского интерфейса</span><span class="sxs-lookup"><span data-stu-id="4d512-106">UI sample</span></span>
![Элемент пользовательского интерфейса Microsoft.Compute.CredentialsCombo](./media/managed-application-elements/microsoft.compute.credentialscombo.png)

## <a name="schema"></a><span data-ttu-id="4d512-108">Схема</span><span class="sxs-lookup"><span data-stu-id="4d512-108">Schema</span></span>
<span data-ttu-id="4d512-109">Если `osPlatform` — **Windows**, а затем hello используется следующая схема:</span><span class="sxs-lookup"><span data-stu-id="4d512-109">If `osPlatform` is **Windows**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false
  },
  "osPlatform": "Windows",
  "visible": true
}
```

<span data-ttu-id="4d512-110">Если `osPlatform` — **Linux**, а затем hello используется следующая схема:</span><span class="sxs-lookup"><span data-stu-id="4d512-110">If `osPlatform` is **Linux**, then hello following schema is used:</span></span>
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
    "customValidationMessage": "hello password must contain at least 8 characters, with at least 1 letter and 1 number."
  },
  "options": {
    "hideConfirmation": false,
    "hidePassword": false
  },
  "osPlatform": "Linux",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="4d512-111">Примечания</span><span class="sxs-lookup"><span data-stu-id="4d512-111">Remarks</span></span>
- <span data-ttu-id="4d512-112">Необходимо задать значение для параметра `osPlatform` (**Windows** или **Linux**).</span><span class="sxs-lookup"><span data-stu-id="4d512-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="4d512-113">Если `constraints.required` задано слишком**true**, затем hello пароль или SSH открытого ключа текстовые поля должны содержать значения toovalidate успешно.</span><span class="sxs-lookup"><span data-stu-id="4d512-113">If `constraints.required` is set too**true**, then hello password or SSH public key text boxes must contain values toovalidate successfully.</span></span> <span data-ttu-id="4d512-114">значение по умолчанию Hello — **true**.</span><span class="sxs-lookup"><span data-stu-id="4d512-114">hello default value is **true**.</span></span>
- <span data-ttu-id="4d512-115">Если `options.hideConfirmation` задано слишком**true**, скрыта hello второе текстовое поле для подтверждения пароля пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="4d512-115">If `options.hideConfirmation` is set too**true**, then hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="4d512-116">значение по умолчанию Hello — **false**.</span><span class="sxs-lookup"><span data-stu-id="4d512-116">hello default value is **false**.</span></span>
- <span data-ttu-id="4d512-117">Если `options.hidePassword` задано слишком**true**, скрыта hello параметр toouse пароля.</span><span class="sxs-lookup"><span data-stu-id="4d512-117">If `options.hidePassword` is set too**true**, then hello option toouse password authentication is hidden.</span></span> <span data-ttu-id="4d512-118">Его можно использовать только тогда, когда параметр `osPlatform` имеет значение **Linux**.</span><span class="sxs-lookup"><span data-stu-id="4d512-118">It can be used only when `osPlatform` is **Linux**.</span></span> <span data-ttu-id="4d512-119">Значение по умолчанию — **false**.</span><span class="sxs-lookup"><span data-stu-id="4d512-119">The default value is **false**.</span></span>
- <span data-ttu-id="4d512-120">Дополнительные ограничения на hello допускается пароли можно реализовать с помощью hello `customPasswordRegex` свойство.</span><span class="sxs-lookup"><span data-stu-id="4d512-120">Additional constraints on hello allowed passwords can be implemented by using hello `customPasswordRegex` property.</span></span> <span data-ttu-id="4d512-121">Здравствуйте, строки в `customValidationMessage` отображается, если пароль не соответствует пользовательской проверки.</span><span class="sxs-lookup"><span data-stu-id="4d512-121">hello string in `customValidationMessage` is displayed when a password fails custom validation.</span></span> <span data-ttu-id="4d512-122">Hello значение по умолчанию для обоих свойств — **null**.</span><span class="sxs-lookup"><span data-stu-id="4d512-122">hello default value for both properties is **null**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="4d512-123">Пример выходных данных</span><span class="sxs-lookup"><span data-stu-id="4d512-123">Sample output</span></span>
<span data-ttu-id="4d512-124">Если `osPlatform` — **Windows**, или предоставляемое hello пользователем пароля вместо открытого ключа SSH, а затем hello следующие ожидаются выходные данные:</span><span class="sxs-lookup"><span data-stu-id="4d512-124">If `osPlatform` is **Windows**, or hello user provided a password instead of an SSH public key, then hello following output is expected:</span></span>

```json
{
  "authenticationType": "password",
  "password": "p4ssw0rd",
}
```

<span data-ttu-id="4d512-125">Если пользователь hello открытый ключ SSH, затем hello следующие выходные данные ожидается:</span><span class="sxs-lookup"><span data-stu-id="4d512-125">If hello user provided an SSH public key, then hello following output is expected:</span></span>
```json
{
  "authenticationType": "sshPublicKey",
  "sshPublicKey": "AAAAB3NzaC1yc2EAAAABIwAAAIEA1on8gxCGJJWSRT4uOrR13mUaUk0hRf4RzxSZ1zRbYYFw8pfGesIFoEuVth4HKyF8k1y4mRUnYHP1XNMNMJl1JcEArC2asV8sHf6zSPVffozZ5TT4SfsUu/iKy9lUcCfXzwre4WWZSXXcPff+EHtWshahu3WzBdnGxm5Xoi89zcE=",
}
```

## <a name="next-steps"></a><span data-ttu-id="4d512-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4d512-126">Next steps</span></span>
* <span data-ttu-id="4d512-127">Введение toomanaged приложений, в разделе [Обзор управляемого приложения Azure](managed-application-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d512-127">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="4d512-128">Для определения пользовательского интерфейса toocreating Общие сведения см. в разделе [Приступая к работе с CreateUiDefinition](managed-application-createuidefinition-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4d512-128">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="4d512-129">Дополнительные сведения об общих свойствах элементов пользовательского интерфейса см. в статье [Элементы CreateUiDefinition](managed-application-createuidefinition-elements.md).</span><span class="sxs-lookup"><span data-stu-id="4d512-129">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
