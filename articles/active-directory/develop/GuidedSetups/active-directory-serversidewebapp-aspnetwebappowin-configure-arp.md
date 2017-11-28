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
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a><span data-ttu-id="0ec07-103">Настройка веб-приложения ASP.NET с сведения о регистрации приложения hello</span><span class="sxs-lookup"><span data-stu-id="0ec07-103">Configure your ASP.NET Web App with hello application's registration information</span></span>

<span data-ttu-id="0ec07-104">На этом шаге будет настройка вашего проекта toouse SSL и воспользуйтесь tooconfigure URL-адрес SSL hello сведения о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="0ec07-104">In this step, you will configure your project toouse SSL, and then use hello SSL URL tooconfigure your application’s registration information.</span></span> <span data-ttu-id="0ec07-105">После этого добавить приложение hello "решение tooyour для регистрации информации через *web.config*.</span><span class="sxs-lookup"><span data-stu-id="0ec07-105">After this, add hello application’ registration information tooyour solution via *web.config*.</span></span>

1.  <span data-ttu-id="0ec07-106">В обозревателе решений выберите проект hello и посмотрите hello `Properties` окна (Если вы не видите окно «Свойства», нажмите клавишу F4)</span><span class="sxs-lookup"><span data-stu-id="0ec07-106">In Solution Explorer, select hello project and look at hello `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="0ec07-107">Изменение `SSL Enabled` слишком`True`</span><span class="sxs-lookup"><span data-stu-id="0ec07-107">Change `SSL Enabled` too`True`</span></span>
3.  <span data-ttu-id="0ec07-108">Скопируйте значение hello из `SSL URL` выше и вставьте его в hello `Redirect URL` поле на hello верхней части этой страницы, а затем нажмите кнопку *обновление*:</span><span class="sxs-lookup"><span data-stu-id="0ec07-108">Copy hello value from `SSL URL` above and paste it in hello `Redirect URL` field on hello top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="0ec07-109">![Свойства проекта](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="0ec07-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="0ec07-110">Добавьте следующее hello в `web.config` файл, расположенный в корневой папке, в разделе `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="0ec07-110">Add hello following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
