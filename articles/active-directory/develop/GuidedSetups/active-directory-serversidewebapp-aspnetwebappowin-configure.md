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
## <a name="create-an-application-express"></a><span data-ttu-id="63f69-103">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="63f69-103">Create an application (Express)</span></span>
<span data-ttu-id="63f69-104">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="63f69-104">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="63f69-105">Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span><span class="sxs-lookup"><span data-stu-id="63f69-105">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)</span></span>
2.  <span data-ttu-id="63f69-106">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="63f69-106">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="63f69-107">Убедитесь, что установлен параметр hello для интерактивной установки</span><span class="sxs-lookup"><span data-stu-id="63f69-107">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="63f69-108">Следуйте инструкциям hello tooadd приложении tooyour URL-адрес перенаправления</span><span class="sxs-lookup"><span data-stu-id="63f69-108">Follow hello instructions tooadd a Redirect URL tooyour application</span></span>

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="63f69-109">Добавить решение tooyour сведения о регистрации приложения (Дополнительно)</span><span class="sxs-lookup"><span data-stu-id="63f69-109">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="63f69-110">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="63f69-110">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="63f69-111">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения</span><span class="sxs-lookup"><span data-stu-id="63f69-111">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="63f69-112">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="63f69-112">Enter a name for your application and your email</span></span> 
3.  <span data-ttu-id="63f69-113">Убедитесь, что hello для интерактивной программы установки не установлен</span><span class="sxs-lookup"><span data-stu-id="63f69-113">Make sure hello option for Guided Setup is unchecked</span></span>
4.  <span data-ttu-id="63f69-114">Щелкните `Add Platform`, а затем выберите `Web`.</span><span class="sxs-lookup"><span data-stu-id="63f69-114">Click `Add Platform`, then select `Web`</span></span>
5.  <span data-ttu-id="63f69-115">Вернитесь к предыдущему окну tooVisual Studio, в обозревателе решений выберите проект hello и посмотрите на окно "Свойства" hello (Если вы не видите окно «Свойства», нажмите клавишу F4)</span><span class="sxs-lookup"><span data-stu-id="63f69-115">Go back tooVisual Studio and, in Solution Explorer, select hello project and look at hello Properties window (if you don’t see a Properties window, press F4)</span></span>
6.  <span data-ttu-id="63f69-116">Слишком изменить протокол SSL включен`True`</span><span class="sxs-lookup"><span data-stu-id="63f69-116">Change SSL Enabled too`True`</span></span>
7.  <span data-ttu-id="63f69-117">Скопируйте URL-адрес SSL hello и добавьте этот список toohello URL-адрес перенаправления URL-адресов в список URL-адреса перенаправления портала регистрации hello:</span><span class="sxs-lookup"><span data-stu-id="63f69-117">Copy hello SSL URL and add this URL toohello list of Redirect URLs in hello Registration Portal’s list of Redirect URLs:</span></span><br/><br/>![Свойства проекта](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  <span data-ttu-id="63f69-119">Добавьте следующее hello в `web.config` расположенный в корневой папке hello в разделе "hello" `configuration\appSettings`:</span><span class="sxs-lookup"><span data-stu-id="63f69-119">Add hello following in `web.config` located in hello root folder under hello section `configuration\appSettings`:</span></span>

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
<span data-ttu-id="63f69-120">Замените `ClientId` с только что зарегистрирован идентификатор приложения hello</span><span class="sxs-lookup"><span data-stu-id="63f69-120">Replace `ClientId` with hello Application Id you just registered</span></span>
</li>
<li>
<span data-ttu-id="63f69-121">Замените `redirectUri` с hello URL-адрес SSL проекта</span><span class="sxs-lookup"><span data-stu-id="63f69-121">Replace `redirectUri` with hello SSL URL of your project</span></span>
</li>
</ol>
<!-- End Docs -->
