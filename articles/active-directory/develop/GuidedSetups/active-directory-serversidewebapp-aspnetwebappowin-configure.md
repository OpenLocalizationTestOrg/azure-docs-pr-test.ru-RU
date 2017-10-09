---
title: "aaaAzure AD v2 ASP.NET Web Server Приступая к работе - Config | Документы Microsoft"
description: "Реализация входа Майкрософт в решении ASP.NET с традиционным браузерным приложением с использованием стандарта OpenID Connect"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>Создание приложения (экспресс)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  Введите имя для приложения и адрес электронной почты.
3.  Убедитесь, что установлен параметр hello для интерактивной установки
4.  Следуйте инструкциям hello tooadd приложении tooyour URL-адрес перенаправления

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>Добавить решение tooyour сведения о регистрации приложения (Дополнительно)
Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:
1. Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения
2. Введите имя для приложения и адрес электронной почты. 
3.  Убедитесь, что hello для интерактивной программы установки не установлен
4.  Щелкните `Add Platform`, а затем выберите `Web`.
5.  Вернитесь к предыдущему окну tooVisual Studio, в обозревателе решений выберите проект hello и посмотрите на окно "Свойства" hello (Если вы не видите окно «Свойства», нажмите клавишу F4)
6.  Слишком изменить протокол SSL включен`True`
7.  Скопируйте URL-адрес SSL hello и добавьте этот список toohello URL-адрес перенаправления URL-адресов в список URL-адреса перенаправления портала регистрации hello:<br/><br/>![Свойства проекта](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  Добавьте следующее hello в `web.config` расположенный в корневой папке hello в разделе "hello" `configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
Замените `ClientId` с только что зарегистрирован идентификатор приложения hello
</li>
<li>
Замените `redirectUri` с hello URL-адрес SSL проекта
</li>
</ol>
<!-- End Docs -->
