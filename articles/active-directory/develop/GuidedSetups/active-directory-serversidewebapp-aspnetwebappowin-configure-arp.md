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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Настройка веб-приложения ASP.NET с сведения о регистрации приложения hello

На этом шаге будет настройка вашего проекта toouse SSL и воспользуйтесь tooconfigure URL-адрес SSL hello сведения о регистрации приложения. После этого добавить приложение hello "решение tooyour для регистрации информации через *web.config*.

1.  В обозревателе решений выберите проект hello и посмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу F4)
2.  Изменение `SSL Enabled` слишком`True`
3.  Скопируйте значение hello из `SSL URL` выше и вставьте его в hello `Redirect URL` поле на hello верхней части этой страницы, а затем нажмите кнопку *обновление*:<br/><br/>![Свойства проекта](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  Добавьте следующее hello в `web.config` файл, расположенный в корневой папке, в разделе `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
