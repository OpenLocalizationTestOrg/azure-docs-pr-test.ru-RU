---
title: "aaaAzure AD v2 Windows Desktop Приступая к работе - Config | Документы Microsoft"
description: "Здесь описывается, как классическое приложение для Windows .NET (XAML) может получить маркер доступа и вызвать API, защищенный конечной точкой Azure Active Directory версии 2. | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Создание приложения (экспресс)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что установлен параметр hello для интерактивной установки
4.  Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Добавить решение tooyour сведения о регистрации приложения (Дополнительно)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения
2. Введите имя для приложения и адрес электронной почты. 
3. Убедитесь, что hello для интерактивной программы установки не установлен
4. Щелкните `Add Platform`, а затем — `Native Application` и нажмите кнопку "Сохранить".
5. Скопируйте hello GUID в код приложения, вернитесь к предыдущему окну tooVisual Studio откройте `App.xaml.cs` и замените `your_client_id_here` с hello вы зарегистрировали идентификатор приложения:

```csharp
private static string ClientId = "your_application_id_here";
```
