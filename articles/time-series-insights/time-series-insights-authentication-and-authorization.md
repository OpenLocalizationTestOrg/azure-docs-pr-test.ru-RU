---
title: "aaaConfigure проверки подлинности и авторизации в пользовательское приложение, которое вызывает hello API аналитики ряда времени Azure | Документы Microsoft"
description: "В этом учебнике описано, как tooconfigure проверки подлинности и авторизации в пользовательское приложение, которое вызывает hello API аналитики ряда времени Azure"
keywords: 
services: time-series-insights
documentationcenter: 
author: dmdenmsft
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: time-series-insights
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/24/2017
ms.author: dmden
ms.openlocfilehash: 5043468bfc2af3c0d27e8602508d92ba2848409e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-for-azure-time-series-insights-api"></a><span data-ttu-id="b1670-103">Проверка подлинности и авторизация для API Azure Time Series Insights</span><span class="sxs-lookup"><span data-stu-id="b1670-103">Authentication and authorization for Azure Time Series Insights API</span></span>

<span data-ttu-id="b1670-104">В этой статье объясняется, как пользовательское приложение, которое вызывает tooconfigure hello Azure времени серии аналитики API.</span><span class="sxs-lookup"><span data-stu-id="b1670-104">This article explains how tooconfigure a custom application that calls hello Azure Time Series Insights API.</span></span>

## <a name="service-principal"></a><span data-ttu-id="b1670-105">Субъект-служба</span><span class="sxs-lookup"><span data-stu-id="b1670-105">Service principal</span></span>

<span data-ttu-id="b1670-106">В этом разделе объясняется, как tooconfigure tooaccess приложения hello времени серии аналитики API от имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b1670-106">This section explains how tooconfigure an application tooaccess hello Time Series Insights API on behalf of hello application.</span></span> <span data-ttu-id="b1670-107">приложение Hello можно запрашивать данные или публикация ссылочных данных в среде времени серии аналитики hello с учетными данными приложения и не hello учетные данные.</span><span class="sxs-lookup"><span data-stu-id="b1670-107">hello application can then query data or publish reference data in hello Time Series Insights environment with application credentials and not hello user credentials.</span></span>

<span data-ttu-id="b1670-108">При наличии в приложение, работающее tooaccess аналитики ряда времени, необходимо установить приложение Azure Active Directory и назначить политики доступа hello данных в среде времени серии аналитики hello.</span><span class="sxs-lookup"><span data-stu-id="b1670-108">When you have an application that needs tooaccess Time Series Insights, you must set up an Azure Active Directory application and assign hello data access policies in hello Time Series Insights environment.</span></span> <span data-ttu-id="b1670-109">Этот подход является более предпочтительным, чем toorunning приложение hello в своих собственных учетных данных, так как:</span><span class="sxs-lookup"><span data-stu-id="b1670-109">This approach is preferable toorunning hello app under your own credentials because:</span></span>

* <span data-ttu-id="b1670-110">Можно назначить разрешения toohello удостоверения приложения, которые отличаются от собственных разрешений.</span><span class="sxs-lookup"><span data-stu-id="b1670-110">You can assign permissions toohello app identity that are different from your own permissions.</span></span> <span data-ttu-id="b1670-111">Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.</span><span class="sxs-lookup"><span data-stu-id="b1670-111">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span> <span data-ttu-id="b1670-112">Например можно разрешить tooonly приложения hello чтения данных в конкретной среде аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="b1670-112">For example, you can allow hello app tooonly read data in a particular Time Series Insights environment.</span></span>
* <span data-ttu-id="b1670-113">Если изменить ваши обязанности приложение hello toochange учетные данные, вам не нужно.</span><span class="sxs-lookup"><span data-stu-id="b1670-113">You don't have toochange hello app's credentials if your responsibilities change.</span></span>
* <span data-ttu-id="b1670-114">При запуске сценария автоматической установки можно использовать сертификата или ключа tooautomate проверки подлинности приложения.</span><span class="sxs-lookup"><span data-stu-id="b1670-114">You can use a certificate or an application key tooautomate authentication when you're running an unattended script.</span></span>

<span data-ttu-id="b1670-115">В этой статье показано, как их по очереди перебирает tooperform hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="b1670-115">This article shows you how tooperform those steps through hello Azure portal.</span></span> <span data-ttu-id="b1670-116">Этот раздел посвящен приложения одного клиента, где приложение hello предполагаемого toorun в организации только один.</span><span class="sxs-lookup"><span data-stu-id="b1670-116">It focuses on a single-tenant application where hello application is intended toorun in only one organization.</span></span> <span data-ttu-id="b1670-117">Обычно однотенантная архитектура используется для создания бизнес-приложений в рамках организации.</span><span class="sxs-lookup"><span data-stu-id="b1670-117">You typically use single-tenant applications for line-of-business applications that run in your organization.</span></span>

<span data-ttu-id="b1670-118">поток Hello установки состоит из трех шагов высокого уровня.</span><span class="sxs-lookup"><span data-stu-id="b1670-118">hello setup flow consists of three high-level steps:</span></span>

1. <span data-ttu-id="b1670-119">Создайте приложение в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="b1670-119">Create an application in Azure Active Directory.</span></span>
2. <span data-ttu-id="b1670-120">Разрешить этой среды аналитики ряда времени приложения hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b1670-120">Authorize this application tooaccess hello Time Series Insights environment.</span></span>
3. <span data-ttu-id="b1670-121">Идентификатор приложения hello и ключа tooacquire маркера toohello `"https://api.timeseries.azure.com/"` аудитории или ресурса.</span><span class="sxs-lookup"><span data-stu-id="b1670-121">Use hello application ID and key tooacquire a token toohello `"https://api.timeseries.azure.com/"` audience or resource.</span></span> <span data-ttu-id="b1670-122">маркер Hello можно затем используется toocall hello API аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="b1670-122">hello token can then be used toocall hello Time Series Insights API.</span></span>

<span data-ttu-id="b1670-123">Ниже приведены hello подробное описание действий:</span><span class="sxs-lookup"><span data-stu-id="b1670-123">Here are hello detailed steps:</span></span>

1. <span data-ttu-id="b1670-124">В hello портал Azure, выберите **Azure Active Directory** > **регистрации приложения** > **Регистрация нового приложения**.</span><span class="sxs-lookup"><span data-stu-id="b1670-124">In hello Azure portal, select **Azure Active Directory** > **App registrations** > **New application registration**.</span></span>

   ![Регистрация нового приложения в Azure Active Directory](media/authentication-and-authorization/active-directory-new-application-registration.png)  

2. <span data-ttu-id="b1670-126">Присвойте toobe hello имя, выберите тип приложения hello **веб-приложения и API**, выберите любой допустимый URI для **URL-адрес входа**и нажмите кнопку **создать**.</span><span class="sxs-lookup"><span data-stu-id="b1670-126">Give hello application a name, select hello type toobe **Web app / API**, select any valid URI for **Sign-on URL**, and click **Create**.</span></span>

   ![Создание приложения hello в Azure Active Directory](media/authentication-and-authorization/active-directory-create-web-api-application.png)

3. <span data-ttu-id="b1670-128">Выберите только что созданный приложения и скопируйте его приложения tooyour идентификатор любого текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="b1670-128">Select your newly created application and copy its application ID tooyour favorite text editor.</span></span>

   ![Скопируйте идентификатор приложения hello](media/authentication-and-authorization/active-directory-copy-application-id.png)

4. <span data-ttu-id="b1670-130">Выберите **ключей**, введите имя ключа hello, выберите hello истечения срока действия и нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b1670-130">Select **Keys**, enter hello key name, select hello expiration, and click **Save**.</span></span>

   ![Выбор ключей приложения](media/authentication-and-authorization/active-directory-application-keys.png)

   ![Введите имя ключа hello и истечения срока действия и нажмите кнопку Сохранить](media/authentication-and-authorization/active-directory-application-keys-save.png)

5. <span data-ttu-id="b1670-133">Скопируйте hello ключа tooyour любого текстового редактора.</span><span class="sxs-lookup"><span data-stu-id="b1670-133">Copy hello key tooyour favorite text editor.</span></span>

   ![Скопируйте ключ приложения hello](media/authentication-and-authorization/active-directory-copy-application-key.png)

6. <span data-ttu-id="b1670-135">Среда времени серии Insights hello, выберите **политикам доступа** и нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="b1670-135">For hello Time Series Insights environment, select **Data Access Policies** and click **Add**.</span></span>

   ![Добавить новый среда доступа к данным политики toohello аналитики ряда времени](media/authentication-and-authorization/time-series-insights-data-access-policies-add.png)

7. <span data-ttu-id="b1670-137">В hello **Выбор пользователя** диалоговое окно, имя приложения hello вставить (из шага 2) или идентификатор приложения (из шага 3).</span><span class="sxs-lookup"><span data-stu-id="b1670-137">In hello **Select User** dialog box, paste hello application name (from step 2) or application ID (from step 3).</span></span>

   ![Поиск приложений в диалоговом окне Выбор пользователя hello](media/authentication-and-authorization/time-series-insights-data-access-policies-select-user.png)

8. <span data-ttu-id="b1670-139">Выберите hello роли (**чтения** для запроса данных, **участника** для запроса данных и изменения эталонных данных) и нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1670-139">Select hello role (**Reader** for querying data, **Contributor** for querying data and changing reference data) and click **Ok**.</span></span>

   ![В диалоговом окне выберите роль hello выбирает читателя или участника](media/authentication-and-authorization/time-series-insights-data-access-policies-select-role.png)

9. <span data-ttu-id="b1670-141">Сохранить политику hello, щелкнув **ОК**.</span><span class="sxs-lookup"><span data-stu-id="b1670-141">Save hello policy by clicking **Ok**.</span></span>

10. <span data-ttu-id="b1670-142">Используйте идентификатор приложения hello (из шага 3) и маркер hello tooacquire ключа (из шага 5) приложения от имени приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b1670-142">Use hello application ID (from step 3) and application key (from step 5) tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="b1670-143">Hello маркера затем можно передать в hello `Authorization` заголовка, когда приложение вызывает hello hello API аналитики ряда времени.</span><span class="sxs-lookup"><span data-stu-id="b1670-143">hello token can then be passed in hello `Authorization` header when hello application calls hello Time Series Insights API.</span></span>

    <span data-ttu-id="b1670-144">При использовании C# можно использовать следующий код tooacquire hello токен имени приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="b1670-144">If you're using C#, you can use hello following code tooacquire hello token on behalf of hello application.</span></span> <span data-ttu-id="b1670-145">Полный пример см. в статье [Запрос данных из среды Azure Time Series Insights с помощью C##](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b1670-145">For a complete sample, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

    ```csharp
    var authenticationContext = new AuthenticationContext(
        "https://login.microsoftonline.com/common",
        TokenCache.DefaultShared);

    AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
        // Set hello resource URI toohello Azure Time Series Insights API
        resource: "https://api.timeseries.azure.com/", 
        clientCredential: new ClientCredential(
            // Application ID of application registered in Azure Active Directory
            clientId: "1bc3af48-7e2f-4845-880a-c7649a6470b8", 
            // Application key of hello application that's registered in Azure Active Directory
            clientSecret: "aBcdEffs4XYxoAXzLB1n3R2meNCYdGpIGBc2YC5D6L2="));

    string accessToken = token.AccessToken;
    ```

## <a name="next-steps"></a><span data-ttu-id="b1670-146">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b1670-146">Next steps</span></span>

<span data-ttu-id="b1670-147">Используйте идентификатор приложения hello и ключ в приложении.</span><span class="sxs-lookup"><span data-stu-id="b1670-147">Use hello application ID and key in your application.</span></span> <span data-ttu-id="b1670-148">Пример кода, вызывает hello API аналитики ряда времени, в разделе [запрос данных с помощью C#](time-series-insights-query-data-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b1670-148">For sample code that calls hello Time Series Insights API, see [Query data using C#](time-series-insights-query-data-csharp.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="b1670-149">См. также</span><span class="sxs-lookup"><span data-stu-id="b1670-149">See also</span></span>

* <span data-ttu-id="b1670-150">[Запрос API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) для hello полный Справочник по API-Интерфейс запросов</span><span class="sxs-lookup"><span data-stu-id="b1670-150">[Query API](/rest/api/time-series-insights/time-series-insights-reference-queryapi) for hello full Query API reference</span></span>
* [<span data-ttu-id="b1670-151">Создание службы субъекта в hello портал Azure</span><span class="sxs-lookup"><span data-stu-id="b1670-151">Create a service principal in hello Azure portal</span></span>](../azure-resource-manager/resource-group-create-service-principal-portal.md)
