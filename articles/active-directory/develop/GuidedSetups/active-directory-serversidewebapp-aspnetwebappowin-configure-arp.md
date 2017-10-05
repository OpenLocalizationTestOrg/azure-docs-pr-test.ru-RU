---
title: "Приступая к работе с Azure AD версии 2 для веб-сервера ASP.NET. Настройка | Документация Майкрософт"
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
ms.openlocfilehash: 8a1650a65e7980f4a13fa4edc7918b0099bb5464
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
## <a name="configure-your-aspnet-web-app-with-the-applications-registration-information"></a><span data-ttu-id="15e51-103">Настройка веб-приложения ASP.NET с помощью сведений о регистрации приложения</span><span class="sxs-lookup"><span data-stu-id="15e51-103">Configure your ASP.NET Web App with the application's registration information</span></span>

<span data-ttu-id="15e51-104">На этом шаге вам предстоит настроить проект для использования SSL, а затем использовать URL-адрес SSL для настройки сведений о регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="15e51-104">In this step, you will configure your project to use SSL, and then use the SSL URL to configure your application’s registration information.</span></span> <span data-ttu-id="15e51-105">После этого вы добавите сведения о регистрации приложения в свое решение, используя файл *web.config*.</span><span class="sxs-lookup"><span data-stu-id="15e51-105">After this, add the application’ registration information to your solution via *web.config*.</span></span>

1.  <span data-ttu-id="15e51-106">В обозревателе решений выберите проект и просмотрите окно `Properties` (если окно свойств не отображается, нажмите клавишу F4).</span><span class="sxs-lookup"><span data-stu-id="15e51-106">In Solution Explorer, select the project and look at the `Properties` window (if you don’t see a Properties window, press F4)</span></span>
2.  <span data-ttu-id="15e51-107">Измените `SSL Enabled` на `True`.</span><span class="sxs-lookup"><span data-stu-id="15e51-107">Change `SSL Enabled` to `True`</span></span>
3.  <span data-ttu-id="15e51-108">Скопируйте значение указанного выше `SSL URL` и вставьте его в поле `Redirect URL` в верхней части этой страницы, а затем щелкните *Обновление*:</span><span class="sxs-lookup"><span data-stu-id="15e51-108">Copy the value from `SSL URL` above and paste it in the `Redirect URL` field on the top of this page, then click *Update*:</span></span><br/><br/><span data-ttu-id="15e51-109">![Свойства проекта](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span><span class="sxs-lookup"><span data-stu-id="15e51-109">![Project properties](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)</span></span><br />
4.  <span data-ttu-id="15e51-110">Добавьте следующий код в файл `web.config`, расположенный в корневой папке в разделе `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="15e51-110">Add the following in `web.config` file located in root’s folder, under section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="[Enter the application Id here]" />
<add key="RedirectUri" value="[Enter the Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
