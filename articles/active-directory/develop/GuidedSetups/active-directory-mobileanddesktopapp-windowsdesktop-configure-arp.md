---
title: "Приступая к работе с Azure AD версии 2 для классического приложения для Windows. Настройка | Документация Майкрософт"
description: "Здесь описывается, как классическое приложение для Windows .NET (XAML) может получить маркер доступа и вызвать API, защищенный конечной точкой Azure Active Directory версии 2."
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 5e83171846517496e221f0a84565cdf7b77514df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="add-the-applications-registration-information-to-your-app"></a><span data-ttu-id="78588-103">Добавление в приложение сведений о его регистрации</span><span class="sxs-lookup"><span data-stu-id="78588-103">Add the application’s registration information to your app</span></span>
<span data-ttu-id="78588-104">На этом шаге вам нужно добавить идентификатор приложения в свой проект.</span><span class="sxs-lookup"><span data-stu-id="78588-104">In this step, you need to add the Application Id to your project.</span></span>

1.  <span data-ttu-id="78588-105">Откройте файл `App.xaml.cs` и замените строку, содержащую `ClientId`, на:</span><span class="sxs-lookup"><span data-stu-id="78588-105">Open `App.xaml.cs` and replace the line containing the `ClientId` with:</span></span>

```csharp
private static string ClientId = "[Enter the application Id here]";
```

### <a name="what-is-next"></a><span data-ttu-id="78588-106">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="78588-106">What is Next</span></span>

[<span data-ttu-id="78588-107">Тестирование кода</span><span class="sxs-lookup"><span data-stu-id="78588-107">Test and Validate</span></span>](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
