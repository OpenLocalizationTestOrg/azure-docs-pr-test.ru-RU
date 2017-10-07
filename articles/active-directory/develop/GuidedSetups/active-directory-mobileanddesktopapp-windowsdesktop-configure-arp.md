---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - Config | Документы Microsoft"
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
ms.openlocfilehash: d96d9eded200824a6f7ee234009dd0bb11b18b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="add-hello-applications-registration-information-tooyour-app"></a>Добавить приложение tooyour сведения о регистрации приложения hello
На этом шаге требуется идентификатор приложения tooyour tooadd hello проекта.

1.  Откройте `App.xaml.cs` и замените строку hello, содержащий hello `ClientId` с:

```csharp
private static string ClientId = "[Enter hello application Id here]";
```

### <a name="what-is-next"></a>Дальнейшие действия

[Тестирование кода](active-directory-mobileanddesktopapp-windowsdesktop-test.md)
