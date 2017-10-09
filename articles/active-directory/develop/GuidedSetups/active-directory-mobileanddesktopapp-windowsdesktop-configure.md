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
## <a name="create-an-application-express"></a><span data-ttu-id="2569b-104">Создание приложения (экспресс)</span><span class="sxs-lookup"><span data-stu-id="2569b-104">Create an application (Express)</span></span>
<span data-ttu-id="2569b-105">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="2569b-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2569b-106">Зарегистрировать приложение через hello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="2569b-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="2569b-107">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2569b-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="2569b-108">Убедитесь, что установлен параметр hello для интерактивной установки</span><span class="sxs-lookup"><span data-stu-id="2569b-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="2569b-109">Выполните код приложения hello tooobtain инструкции hello и вставьте его в коде</span><span class="sxs-lookup"><span data-stu-id="2569b-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="2569b-110">Добавить решение tooyour сведения о регистрации приложения (Дополнительно)</span><span class="sxs-lookup"><span data-stu-id="2569b-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="2569b-111">Теперь необходимо приложение hello tooregister *портала регистрации приложения Microsoft*:</span><span class="sxs-lookup"><span data-stu-id="2569b-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="2569b-112">Go toohello [портала регистрации приложения Microsoft](https://apps.dev.microsoft.com/portal/register-app) tooregister приложения</span><span class="sxs-lookup"><span data-stu-id="2569b-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="2569b-113">Введите имя для приложения и адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="2569b-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="2569b-114">Убедитесь, что hello для интерактивной программы установки не установлен</span><span class="sxs-lookup"><span data-stu-id="2569b-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="2569b-115">Щелкните `Add Platform`, а затем — `Native Application` и нажмите кнопку "Сохранить".</span><span class="sxs-lookup"><span data-stu-id="2569b-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="2569b-116">Скопируйте hello GUID в код приложения, вернитесь к предыдущему окну tooVisual Studio откройте `App.xaml.cs` и замените `your_client_id_here` с hello вы зарегистрировали идентификатор приложения:</span><span class="sxs-lookup"><span data-stu-id="2569b-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
