---
title: "Автоматическая подготовка пользователей и групп из Azure Active Directory tooapplications aaaUsing системы для управления удостоверениями междоменной | Документы Microsoft"
description: "Azure Active Directory автоматически подготавливать пользователей и групп tooany приложения или идентификатор магазина, аппаратные веб-службой с hello интерфейс, определенный в спецификации протокола SCIM hello"
services: active-directory
documentationcenter: 
author: asmalser-msft
manager: femila
editor: 
ms.assetid: 4d86f3dc-e2d3-4bde-81a3-4a0e092551c0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/28/2017
ms.author: asmalser
ms.reviewer: asmalser
ms.custom: aaddev;it-pro;oldportal
ms.openlocfilehash: 43045c97e68d0d22db598dcb5ec23481c4e97718
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-system-for-cross-domain-identity-management-tooautomatically-provision-users-and-groups-from-azure-active-directory-tooapplications"></a><span data-ttu-id="4b095-103">При использовании системы для подготовки tooautomatically между доменами удостоверений пользователей и группы из tooapplications Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b095-103">Using System for Cross-Domain Identity Management tooautomatically provision users and groups from Azure Active Directory tooapplications</span></span>

## <a name="overview"></a><span data-ttu-id="4b095-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="4b095-104">Overview</span></span>
<span data-ttu-id="4b095-105">Azure Active Directory (Azure AD) автоматически подготавливать пользователей и групп tooany приложения или идентификатор магазина, аппаратные веб-службой с hello интерфейс, определенный в hello [система для идентификации управления доменами (SCIM) 2.0 Спецификация протокола](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="4b095-105">Azure Active Directory (Azure AD) can automatically provision users and groups tooany application or identity store that is fronted by a web service with hello interface defined in hello [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="4b095-106">Azure Active Directory можно отправлять запросы toocreate, изменение или удаление назначенных пользователей и групп toohello веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4b095-106">Azure Active Directory can send requests toocreate, modify, or delete assigned users and groups toohello web service.</span></span> <span data-ttu-id="4b095-107">Hello веб-службы можно преобразовать эти запросы в операции над hello целевого хранилища удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4b095-107">hello web service can then translate those requests into operations on hello target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="4b095-108">Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье.</span><span class="sxs-lookup"><span data-stu-id="4b095-108">Microsoft recommends that you manage Azure AD using hello [Azure AD admin center](https://aad.portal.azure.com) in hello Azure portal instead of using hello Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="4b095-109">![][0]
*Рисунок 1: Подготовка из хранилища удостоверений Azure Active Directory tooan через веб-службу*</span><span class="sxs-lookup"><span data-stu-id="4b095-109">![][0]
*Figure 1: Provisioning from Azure Active Directory tooan identity store via a web service*</span></span>

<span data-ttu-id="4b095-110">Эту возможность можно использовать в сочетании с возможностью «принеси свое приложение» hello в Azure AD tooenable-единого входа и автоматической подготовки пользователей для приложений, предоставляющих или аппаратные веб-службой SCIM.</span><span class="sxs-lookup"><span data-stu-id="4b095-110">This capability can be used in conjunction with hello “bring your own app” capability in Azure AD tooenable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="4b095-111">Существуют два варианта использования SCIM в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b095-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="4b095-112">**Подготовка tooapplications пользователей и групп, которые поддерживают SCIM** приложений, которые поддерживают SCIM 2.0 и проверка подлинности работает в Azure AD без настройки применения маркеров носителя OAuth.</span><span class="sxs-lookup"><span data-stu-id="4b095-112">**Provisioning users and groups tooapplications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="4b095-113">**Построение подготовки решения для приложений, поддерживающих другие API-инициализации на основе** для приложений, не являющихся SCIM, можно создать tootranslate конечная точка SCIM между конечной точкой Azure AD SCIM hello и поддерживает приложения hello любого API для подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="4b095-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint tootranslate between hello Azure AD SCIM endpoint and any API hello application supports for user provisioning.</span></span> <span data-ttu-id="4b095-114">Разработка конечную точку SCIM toohelp, мы предоставляем библиотеки Common Language Infrastructure (CLI), а также примеры кода, которые показывают, как указать конечную точку SCIM и преобразования сообщений SCIM toodo.</span><span class="sxs-lookup"><span data-stu-id="4b095-114">toohelp you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how toodo provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-tooapplications-that-support-scim"></a><span data-ttu-id="4b095-115">Подготовка пользователей и групп tooapplications, который поддерживает SCIM</span><span class="sxs-lookup"><span data-stu-id="4b095-115">Provisioning users and groups tooapplications that support SCIM</span></span>
<span data-ttu-id="4b095-116">Azure AD может быть настроенный tooautomatically назначенный подготовки пользователей и групп tooapplications, реализовать [системы для управления удостоверениями междоменной 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) веб-службы и принять маркеров носителя OAuth для проверки подлинности .</span><span class="sxs-lookup"><span data-stu-id="4b095-116">Azure AD can be configured tooautomatically provision assigned users and groups tooapplications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="4b095-117">Согласно спецификации hello SCIM 2.0 приложений должно соответствовать следующим требованиям:</span><span class="sxs-lookup"><span data-stu-id="4b095-117">Within hello SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="4b095-118">Поддерживает создание пользователей и/или групп, согласно разделе 3.3 hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-118">Supports creating users and/or groups, as per section 3.3 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="4b095-119">Поддерживает изменение пользователей и/или групп, имеющих запросы patch согласно раздел 3.5.2 hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="4b095-120">Поддерживает извлечение известному ресурсу согласно раздел 3.4.1 hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-120">Supports retrieving a known resource as per section 3.4.1 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="4b095-121">Поддерживает запросы пользователей и/или групп, как описано в разделе 3.4.2 из hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-121">Supports querying users and/or groups, as per section 3.4.2 of hello SCIM protocol.</span></span>  <span data-ttu-id="4b095-122">(по умолчанию пользователи запрашиваются по атрибуту externalI, а группы по атрибуту displayName).</span><span class="sxs-lookup"><span data-stu-id="4b095-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="4b095-123">Поддерживает запросы пользователя по Идентификатору и диспетчером, как описано в разделе 3.4.2 из hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-123">Supports querying user by ID and by manager as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="4b095-124">Поддерживает группы по Идентификатору и для элементов, как описано в разделе 3.4.2 из hello SCIM протокол запросов.</span><span class="sxs-lookup"><span data-stu-id="4b095-124">Supports querying groups by ID and by member as per section 3.4.2 of hello SCIM protocol.</span></span>  
* <span data-ttu-id="4b095-125">Принимает маркеров носителя OAuth для авторизации, как описано в разделе 2.1 hello SCIM протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of hello SCIM protocol.</span></span>

<span data-ttu-id="4b095-126">Рекомендуется связаться с поставщиком приложения или ознакомиться с документацией поставщика для получения подтверждения соответствия этим требованиям.</span><span class="sxs-lookup"><span data-stu-id="4b095-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="4b095-127">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4b095-127">Getting started</span></span>
<span data-ttu-id="4b095-128">Приложения, поддерживающие профиль SCIM hello описанные в этой статье может быть подключенным tooAzure Active Directory с помощью функции hello «приложение не галереи» в галерее приложения hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-128">Applications that support hello SCIM profile described in this article can be connected tooAzure Active Directory using hello "non-gallery application" feature in hello Azure AD application gallery.</span></span> <span data-ttu-id="4b095-129">После подключена, Azure AD запускает процесс синхронизации каждые 20 минут, где он запрашивает конечную точку SCIM приложения hello для назначенных пользователей и групп и создает или изменяет их в соответствии с toohello сведения о назначении.</span><span class="sxs-lookup"><span data-stu-id="4b095-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries hello application's SCIM endpoint for assigned users and groups, and creates or modifies them according toohello assignment details.</span></span>

<span data-ttu-id="4b095-130">**tooconnect приложение, поддерживающее SCIM:**</span><span class="sxs-lookup"><span data-stu-id="4b095-130">**tooconnect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="4b095-131">Войдите в слишком[hello портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b095-131">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="4b095-132">Обзор слишком ** Azure Active Directory > корпоративных приложений и выберите **нового приложения > все > приложения без коллекции**.</span><span class="sxs-lookup"><span data-stu-id="4b095-132">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="4b095-133">Введите имя для вашего приложения и нажмите кнопку **добавить** toocreate значок объекта приложения.</span><span class="sxs-lookup"><span data-stu-id="4b095-133">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span>
    
  <span data-ttu-id="4b095-134">![][1]
  *Рисунок 2. Использование коллекции приложений Azure AD*</span><span class="sxs-lookup"><span data-stu-id="4b095-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="4b095-135">На экране полученный hello выберите hello **Provisioning** вкладку в левом столбце hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-135">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="4b095-136">В hello **режим подготовки** последовательно выберите пункты **автоматического**.</span><span class="sxs-lookup"><span data-stu-id="4b095-136">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="4b095-137">![][2]
  *Рисунок 3: Настройка подготовки в hello портал Azure*</span><span class="sxs-lookup"><span data-stu-id="4b095-137">![][2]
*Figure 3: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="4b095-138">В hello **URL-адрес клиента** введите hello URL-адрес конечной точки SCIM приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-138">In hello **Tenant URL** field, enter hello URL of hello application's SCIM endpoint.</span></span> <span data-ttu-id="4b095-139">Пример: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="4b095-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="4b095-140">Если конечная точка SCIM hello требует токена носителя OAuth от издателя, отличные от Azure AD, то копирование hello required токена носителя OAuth в hello необязательно **секрет маркера** поля.</span><span class="sxs-lookup"><span data-stu-id="4b095-140">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="4b095-141">Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="4b095-142">Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.</span><span class="sxs-lookup"><span data-stu-id="4b095-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="4b095-143">Нажмите кнопку hello **проверить подключение** кнопку toohave Azure Active Directory попытки tooconnect toohello SCIM конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4b095-143">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="4b095-144">Если hello попытки не удались, отображаются сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4b095-144">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="4b095-145">Если приложение toohello tooconnect попыток hello выполняются успешно, нажмите кнопку **Сохранить** toosave учетные данные администратора hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-145">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="4b095-146">В hello **сопоставления** статьи, два набора можно выбрать сопоставлений атрибутов: для пользовательских объектов и объектов групп.</span><span class="sxs-lookup"><span data-stu-id="4b095-146">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="4b095-147">Выберите каждый один атрибуты tooreview hello, которые синхронизируются из tooyour приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b095-147">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="4b095-148">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello пользователей и групп в приложении для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="4b095-148">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="4b095-149">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="4b095-149">Select hello Save button toocommit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="4b095-150">При необходимости можно отключить синхронизации группы объектов, отключив hello «groups» сопоставления.</span><span class="sxs-lookup"><span data-stu-id="4b095-150">You can optionally disable syncing of group objects by disabling hello "groups" mapping.</span></span> 

11. <span data-ttu-id="4b095-151">В разделе **параметры**, hello **область** поле определяет, какие пользователи и группы синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4b095-151">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="4b095-152">При выборе «Синхронизации только назначенные пользователи и группы» (рекомендуется) будет синхронизировать только пользователей и группы, назначенные в hello **пользователей и групп** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4b095-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="4b095-153">После завершения настройки изменить hello **состояние подготовки** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="4b095-153">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="4b095-154">Нажмите кнопку **Сохранить** toostart hello подготовки службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-154">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="4b095-155">Если синхронизация только назначены пользователи и группы (рекомендуется), быть убедиться, что hello tooselect **пользователей и групп** и назначьте hello пользователей или групп, которые нужно toosync.</span><span class="sxs-lookup"><span data-stu-id="4b095-155">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="4b095-156">После запуска начальной синхронизации hello, можно использовать hello **журналы аудита** вкладке toomonitor хода выполнения, показывающий все действия, выполняемые hello подготовки службы в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b095-156">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="4b095-157">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4b095-157">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="4b095-158">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-158">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="4b095-159">Создание собственного решения подготовки для любого приложения</span><span class="sxs-lookup"><span data-stu-id="4b095-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="4b095-160">Создав веб-службу SCIM, взаимодействующую с Azure Active Directory, можно включить единый вход и автоматическую подготовку пользователей практически для любого приложения, которое предоставляет API подготовки пользователей REST или SOAP.</span><span class="sxs-lookup"><span data-stu-id="4b095-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="4b095-161">Вот как это работает</span><span class="sxs-lookup"><span data-stu-id="4b095-161">Here’s how it works:</span></span>

1. <span data-ttu-id="4b095-162">Azure AD предоставляет библиотеку CLI с именем [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="4b095-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="4b095-163">Системные интеграторы и разработчиков можно использовать этот toocreate библиотеки и развернуть веб-SCIM конечной точки службы можно подключаться хранилище удостоверений tooany приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-163">System integrators and developers can use this library toocreate and deploy a SCIM-based web service endpoint capable of connecting Azure AD tooany application’s identity store.</span></span>
2. <span data-ttu-id="4b095-164">Сопоставления реализованы в hello web service toomap hello унифицировать toohello пользователя схемы и необходимые приложения hello протокола.</span><span class="sxs-lookup"><span data-stu-id="4b095-164">Mappings are implemented in hello web service toomap hello standardized user schema toohello user schema and protocol required by hello application.</span></span>
3. <span data-ttu-id="4b095-165">URL-адрес конечной точки Hello регистрируется в Azure AD в рамках пользовательского приложения в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-165">hello endpoint URL is registered in Azure AD as part of a custom application in hello application gallery.</span></span>
4. <span data-ttu-id="4b095-166">Пользователи и группы назначаются toothis приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-166">Users and groups are assigned toothis application in Azure AD.</span></span> <span data-ttu-id="4b095-167">После назначения они помещаются в очередь toobe синхронизированы toohello целевое приложение.</span><span class="sxs-lookup"><span data-stu-id="4b095-167">Upon assignment, they are put into a queue toobe synchronized toohello target application.</span></span> <span data-ttu-id="4b095-168">процесс синхронизации Hello обработки hello очереди выполняется каждые 20 минут.</span><span class="sxs-lookup"><span data-stu-id="4b095-168">hello synchronization process handling hello queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="4b095-169">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="4b095-169">Code Samples</span></span>
<span data-ttu-id="4b095-170">toomake это удобным процесс, набор [примеры кода](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) предоставляются, создайте конечную точку службы web SCIM и демонстрируют автоматическую подготовку к работе.</span><span class="sxs-lookup"><span data-stu-id="4b095-170">toomake this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="4b095-171">В одном примере поставщик службы использует файл, в котором пользователи и группы представлены строками значений, разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="4b095-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="4b095-172">Hello других — поставщика, который работает со службой hello Amazon Web Services удостоверений и управления доступом.</span><span class="sxs-lookup"><span data-stu-id="4b095-172">hello other is of a provider that operates on hello Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="4b095-173">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="4b095-173">**Prerequisites**</span></span>

* <span data-ttu-id="4b095-174">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="4b095-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="4b095-175">Пакет Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="4b095-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="4b095-176">Компьютере Windows, который поддерживает toobe framework 4.5 hello ASP.NET используется в качестве hello SCIM конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4b095-176">Windows machine that supports hello ASP.NET framework 4.5 toobe used as hello SCIM endpoint.</span></span> <span data-ttu-id="4b095-177">Этот компьютер должен быть доступен из облака hello</span><span class="sxs-lookup"><span data-stu-id="4b095-177">This machine must be accessible from hello cloud</span></span>
* [<span data-ttu-id="4b095-178">Подписка Azure с пробной или лицензированной версией Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="4b095-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="4b095-179">Образец Hello Amazon AWS требует библиотек из не hello [AWS набор средств для Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="4b095-179">hello Amazon AWS sample requires libraries from hello [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="4b095-180">Дополнительные сведения см. в разделе hello README файл, входящий в состав образца hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-180">For more information, see hello README file included with hello sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="4b095-181">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="4b095-181">Getting Started</span></span>
<span data-ttu-id="4b095-182">Самый простой способ tooimplement Hello SCIM конечной точки, которое может принять подготовки запросов из Azure AD toobuild и разверните образец кода hello, выводит файл значений с разделителями запятыми (CSV) tooa подготовленные пользователи hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-182">hello easiest way tooimplement a SCIM endpoint that can accept provisioning requests from Azure AD is toobuild and deploy hello code sample that outputs hello provisioned users tooa comma-separated value (CSV) file.</span></span>

<span data-ttu-id="4b095-183">**toocreate конечную точку SCIM образца:**</span><span class="sxs-lookup"><span data-stu-id="4b095-183">**toocreate a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="4b095-184">Загрузите пакет образца кода hello в [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="4b095-184">Download hello code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="4b095-185">Распакуйте пакет hello и поместите его на компьютере Windows в расположении, например C:\AzureAD-BYOA-Provisioning-Samples\.</span><span class="sxs-lookup"><span data-stu-id="4b095-185">Unzip hello package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="4b095-186">В этой папке запустите hello FileProvisioningAgent решения в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="4b095-186">In this folder, launch hello FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="4b095-187">Выберите **Сервис > Диспетчер пакетов библиотеки > консоль диспетчера пакетов**и выполните следующие команды для ссылки на решение hello tooresolve в проект FileProvisioningAgent hello hello:</span><span class="sxs-lookup"><span data-stu-id="4b095-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute hello following commands for hello FileProvisioningAgent project tooresolve hello solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="4b095-188">Построение проекта FileProvisioningAgent hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-188">Build hello FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="4b095-189">Запустите приложение hello командной строки в Windows (с правами администратора) и использовать hello **cd** hello directory команда toochange tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** папки.</span><span class="sxs-lookup"><span data-stu-id="4b095-189">Launch hello Command Prompt application in Windows (as an Administrator), and use hello **cd** command toochange hello directory tooyour **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="4b095-190">Выполните hello следующую команду, заменив < ip адрес > hello IP-адрес или домен, имя компьютера Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-190">Run hello following command, replacing <ip-address> with hello IP address or domain name of hello Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="4b095-191">В Windows, под **параметры Windows > сети и Интернету параметров**выберите hello **брандмауэра Windows > Дополнительные параметры**и создать **правила входящего подключения** , Разрешает доступ входящего трафика tooport 9000.</span><span class="sxs-lookup"><span data-stu-id="4b095-191">In Windows under **Windows Settings > Network & Internet Settings**, select hello **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access tooport 9000.</span></span>
9. <span data-ttu-id="4b095-192">Если компьютер Windows hello за маршрутизатором, hello маршрутизатора потребностей toobe настроен tooperform перевод доступа к сети между его порта 9000, предоставляемый toohello Интернета и порта 9000 на компьютере Windows hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-192">If hello Windows machine is behind a router, hello router needs toobe configured tooperform Network Access Translation between its port 9000 that is exposed toohello internet, and port 9000 on hello Windows machine.</span></span> <span data-ttu-id="4b095-193">Это необходимо для возможности tooaccess toobe Azure AD эту конечную точку в облаке hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-193">This is required for Azure AD toobe able tooaccess this endpoint in hello cloud.</span></span>

<span data-ttu-id="4b095-194">**tooregister hello образец SCIM конечной точки в Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="4b095-194">**tooregister hello sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="4b095-195">Войдите в слишком[hello портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="4b095-195">Sign in too[hello Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="4b095-196">Обзор слишком ** Azure Active Directory > корпоративных приложений и выберите **нового приложения > все > приложения без коллекции**.</span><span class="sxs-lookup"><span data-stu-id="4b095-196">Browse too**Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="4b095-197">Введите имя для вашего приложения и нажмите кнопку **добавить** toocreate значок объекта приложения.</span><span class="sxs-lookup"><span data-stu-id="4b095-197">Enter a name for your application, and click **Add** icon toocreate an app object.</span></span> <span data-ttu-id="4b095-198">создать объект приложения Hello — предполагаемого toorepresent hello целевого приложения будет подготовки tooand реализации единого входа, а не просто hello SCIM endpoint.</span><span class="sxs-lookup"><span data-stu-id="4b095-198">hello application object created is intended toorepresent hello target app you would be provisioning tooand implementing single sign-on for, and not just hello SCIM endpoint.</span></span>
4. <span data-ttu-id="4b095-199">На экране полученный hello выберите hello **Provisioning** вкладку в левом столбце hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-199">In hello resulting screen, select hello **Provisioning** tab in hello left column.</span></span>
5. <span data-ttu-id="4b095-200">В hello **режим подготовки** последовательно выберите пункты **автоматического**.</span><span class="sxs-lookup"><span data-stu-id="4b095-200">In hello **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="4b095-201">![][2]
  *Рисунок 4: Настройка подготовки в hello портал Azure*</span><span class="sxs-lookup"><span data-stu-id="4b095-201">![][2]
*Figure 4: Configuring provisioning in hello Azure portal*</span></span>
    
6. <span data-ttu-id="4b095-202">В hello **URL-адрес клиента** введите hello предоставляется Интернет URL-адрес и порт SCIM конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4b095-202">In hello **Tenant URL** field, enter hello internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="4b095-203">Это может быть что-то, как http://testmachine.contoso.com:9000 или http://<ip-address>:9000/, где < ip адрес > является hello Интернета, предоставляемым IP адрес.</span><span class="sxs-lookup"><span data-stu-id="4b095-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is hello internet exposed IP address.</span></span>  
7. <span data-ttu-id="4b095-204">Если конечная точка SCIM hello требует токена носителя OAuth от издателя, отличные от Azure AD, то копирование hello required токена носителя OAuth в hello необязательно **секрет маркера** поля.</span><span class="sxs-lookup"><span data-stu-id="4b095-204">If hello SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy hello required OAuth bearer token into hello optional **Secret Token** field.</span></span> <span data-ttu-id="4b095-205">Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="4b095-206">Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.</span><span class="sxs-lookup"><span data-stu-id="4b095-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="4b095-207">Нажмите кнопку hello **проверить подключение** кнопку toohave Azure Active Directory попытки tooconnect toohello SCIM конечной точки.</span><span class="sxs-lookup"><span data-stu-id="4b095-207">Click hello **Test Connection** button toohave Azure Active Directory attempt tooconnect toohello SCIM endpoint.</span></span> <span data-ttu-id="4b095-208">Если hello попытки не удались, отображаются сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="4b095-208">If hello attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="4b095-209">Если приложение toohello tooconnect попыток hello выполняются успешно, нажмите кнопку **Сохранить** toosave учетные данные администратора hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-209">If hello attempts tooconnect toohello application succeed, then click **Save** toosave hello admin credentials.</span></span>
10. <span data-ttu-id="4b095-210">В hello **сопоставления** статьи, два набора можно выбрать сопоставлений атрибутов: для пользовательских объектов и объектов групп.</span><span class="sxs-lookup"><span data-stu-id="4b095-210">In hello **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="4b095-211">Выберите каждый один атрибуты tooreview hello, которые синхронизируются из tooyour приложения Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b095-211">Select each one tooreview hello attributes that are synchronized from Azure Active Directory tooyour app.</span></span> <span data-ttu-id="4b095-212">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello пользователей и групп в приложении для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="4b095-212">hello attributes selected as **Matching** properties are used toomatch hello users and groups in your app for update operations.</span></span> <span data-ttu-id="4b095-213">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="4b095-213">Select hello Save button toocommit any changes.</span></span>
11. <span data-ttu-id="4b095-214">В разделе **параметры**, hello **область** поле определяет, какие пользователи и группы синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4b095-214">Under **Settings**, hello **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="4b095-215">При выборе «Синхронизации только назначенные пользователи и группы» (рекомендуется) будет синхронизировать только пользователей и группы, назначенные в hello **пользователей и групп** вкладки.</span><span class="sxs-lookup"><span data-stu-id="4b095-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in hello **Users and groups** tab.</span></span>
12. <span data-ttu-id="4b095-216">После завершения настройки изменить hello **состояние подготовки** слишком**на**.</span><span class="sxs-lookup"><span data-stu-id="4b095-216">Once your configuration is complete, change hello **Provisioning Status** too**On**.</span></span>
13. <span data-ttu-id="4b095-217">Нажмите кнопку **Сохранить** toostart hello подготовки службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-217">Click **Save** toostart hello Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="4b095-218">Если синхронизация только назначены пользователи и группы (рекомендуется), быть убедиться, что hello tooselect **пользователей и групп** и назначьте hello пользователей или групп, которые нужно toosync.</span><span class="sxs-lookup"><span data-stu-id="4b095-218">If syncing only assigned users and groups (recommended), be sure tooselect hello **Users and groups** tab and assign hello users and/or groups you wish toosync.</span></span>

<span data-ttu-id="4b095-219">После запуска начальной синхронизации hello, можно использовать hello **журналы аудита** вкладке toomonitor хода выполнения, показывающий все действия, выполняемые hello подготовки службы в приложении.</span><span class="sxs-lookup"><span data-stu-id="4b095-219">Once hello initial synchronization has started, you can use hello **Audit logs** tab toomonitor progress, which shows all actions performed by hello provisioning service on your app.</span></span> <span data-ttu-id="4b095-220">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="4b095-220">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="4b095-221">Последний шаг Hello Проверка образца hello — hello tooopen TargetFile.csv файл в папке \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug hello на компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="4b095-221">hello final step in verifying hello sample is tooopen hello TargetFile.csv file in hello \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="4b095-222">После выполнения процесса подготовки hello в этом файле отображаются сведения hello всех назначенных и подготовить пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="4b095-222">Once hello provisioning process is run, this file shows hello details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="4b095-223">Библиотеки для разработчика</span><span class="sxs-lookup"><span data-stu-id="4b095-223">Development libraries</span></span>
<span data-ttu-id="4b095-224">toodevelop собственной веб-службы, который соответствует спецификации SCIM toohello, сначала ознакомьтесь с hello следующих библиотек, предоставляемых корпорацией Майкрософт toohelp ускорить процесс разработки hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-224">toodevelop your own web service that conforms toohello SCIM specification, first familiarize yourself with hello following libraries provided by Microsoft toohelp accelerate hello development process:</span></span> 

1. <span data-ttu-id="4b095-225">Библиотеки Common Language Infrastructure (CLI) для использования с языками, основанными на этой инфраструктуре, например C#.</span><span class="sxs-lookup"><span data-stu-id="4b095-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="4b095-226">Одно из этих библиотек [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), объявляет интерфейс, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, показано в следующих рисунке hello: A разработчик, использующий hello библиотеки будет реализовывать этот интерфейс с классом, который может ссылаться, универсальной поставщика.</span><span class="sxs-lookup"><span data-stu-id="4b095-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in hello following illustration:  A developer using hello libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="4b095-227">Hello библиотеки позволяют toodeploy developer Привет веб-службы, который соответствует спецификации SCIM toohello.</span><span class="sxs-lookup"><span data-stu-id="4b095-227">hello libraries enable hello developer toodeploy a web service that conforms toohello SCIM specification.</span></span> <span data-ttu-id="4b095-228">Hello веб-служба может размещаться либо в службах IIS или любой исполняемая сборка Общеязыковая инфраструктура.</span><span class="sxs-lookup"><span data-stu-id="4b095-228">hello web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="4b095-229">Запрос преобразуется в поставщик toohello вызовы методов, которые может быть запрограммировано toooperate developer Привет на некоторых хранилище удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4b095-229">Request is translated into calls toohello provider’s methods, which would be programmed by hello developer toooperate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="4b095-230">[Express обработчики маршрутов](http://expressjs.com/guide/routing.html) доступны для синтаксического анализа node.js запрос объектов, представляющих вызовы (в соответствии с hello спецификации SCIM), tooa node.js веб-службы.</span><span class="sxs-lookup"><span data-stu-id="4b095-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by hello SCIM specification), made tooa node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="4b095-231">Создание пользовательской конечной точки SCIM</span><span class="sxs-lookup"><span data-stu-id="4b095-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="4b095-232">Использование библиотек CLI hello, разработчики, использующие эти библиотеки можно размещать свои службы в любой исполняемая сборка Общеязыковая инфраструктура или в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="4b095-232">Using hello CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="4b095-233">Ниже приведен пример кода для размещения службы в исполняемую сборку, по адресу hello http://localhost:9000:</span><span class="sxs-lookup"><span data-stu-id="4b095-233">Here is sample code for hosting a service within an executable assembly, at hello address http://localhost:9000:</span></span> 

    private static void Main(string[] arguments)
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IProvider and 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
      new DevelopersMonitor();
    Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
      new DevelopersProvider(arguments[1]);
    Microsoft.SystemForCrossDomainIdentityManagement.Service webService = null;
    try
    {
        webService = new WebService(monitor, provider);
        webService.Start("http://localhost:9000");

        Console.ReadKey(true);
    }
    finally
    {
        if (webService != null)
        {
            webService.Dispose();
            webService = null;
        }
    }
    }

    public class WebService : Microsoft.SystemForCrossDomainIdentityManagement.Service
    {
    private Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor;
    private Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider;

    public WebService(
      Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitoringBehavior, 
      Microsoft.SystemForCrossDomainIdentityManagement.IProvider providerBehavior)
    {
        this.monitor = monitoringBehavior;
        this.provider = providerBehavior;
    }

    public override IMonitor MonitoringBehavior
    {
        get
        {
            return this.monitor;
        }

        set
        {
            this.monitor = value;
        }
    }

    public override IProvider ProviderBehavior
    {
        get
        {
            return this.provider;
        }

        set
        {
            this.provider = value;
        }
    }
    }

<span data-ttu-id="4b095-234">Эту службу необходимо иметь HTTP адреса и сервера проверки подлинности сертификат какие hello корневого центра сертификации — одно из следующих hello:</span><span class="sxs-lookup"><span data-stu-id="4b095-234">This service must have an HTTP address and server authentication certificate of which hello root certification authority is one of hello following:</span></span> 

* <span data-ttu-id="4b095-235">CNNIC;</span><span class="sxs-lookup"><span data-stu-id="4b095-235">CNNIC</span></span>
* <span data-ttu-id="4b095-236">Comodo;</span><span class="sxs-lookup"><span data-stu-id="4b095-236">Comodo</span></span>
* <span data-ttu-id="4b095-237">CyberTrust;</span><span class="sxs-lookup"><span data-stu-id="4b095-237">CyberTrust</span></span>
* <span data-ttu-id="4b095-238">DigiCert;</span><span class="sxs-lookup"><span data-stu-id="4b095-238">DigiCert</span></span>
* <span data-ttu-id="4b095-239">GeoTrust;</span><span class="sxs-lookup"><span data-stu-id="4b095-239">GeoTrust</span></span>
* <span data-ttu-id="4b095-240">GlobalSign;</span><span class="sxs-lookup"><span data-stu-id="4b095-240">GlobalSign</span></span>
* <span data-ttu-id="4b095-241">Go Daddy;</span><span class="sxs-lookup"><span data-stu-id="4b095-241">Go Daddy</span></span>
* <span data-ttu-id="4b095-242">VeriSign;</span><span class="sxs-lookup"><span data-stu-id="4b095-242">Verisign</span></span>
* <span data-ttu-id="4b095-243">WoSign.</span><span class="sxs-lookup"><span data-stu-id="4b095-243">WoSign</span></span>

<span data-ttu-id="4b095-244">Сертификат проверки подлинности сервера может быть привязанного tooa-порту на узле Windows с помощью служебной программы оболочки сети hello:</span><span class="sxs-lookup"><span data-stu-id="4b095-244">A server authentication certificate can be bound tooa port on a Windows host using hello network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="4b095-245">Здесь hello значение аргумента certhash hello — hello отпечаток сертификата hello, пока значение hello аргумента appid hello произвольный глобальный уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="4b095-245">Here, hello value provided for hello certhash argument is hello thumbprint of hello certificate, while hello value provided for hello appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="4b095-246">Служба toohost hello в службах IIS, разработчик построение будет осуществляться библиотечная сборка кодом CLA на класс с именем запуска в пространстве имен по умолчанию hello сборки hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-246">toohost hello service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in hello default namespace of hello assembly.</span></span>  <span data-ttu-id="4b095-247">Ниже приведен пример такого класса.</span><span class="sxs-lookup"><span data-stu-id="4b095-247">Here is a sample of such a class:</span></span> 

    public class Startup
    {
    // Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IMonitor and  
    // Microsoft.SystemForCrossDomainIdentityManagement.Service are all defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Service.dll.  

    Microsoft.SystemForCrossDomainIdentityManagement.IWebApplicationStarter starter;

    public Startup()
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IMonitor monitor = 
          new DevelopersMonitor();
        Microsoft.SystemForCrossDomainIdentityManagement.IProvider provider = 
          new DevelopersProvider();
        this.starter = 
          new Microsoft.SystemForCrossDomainIdentityManagement.WebApplicationStarter(
            provider, 
            monitor);
    }

    public void Configuration(
      Owin.IAppBuilder builder) // Defined in in Owin.dll.  
    {
        this.starter.ConfigureApplication(builder);
    }
    }

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="4b095-248">Обработка аутентификации на конечной точке</span><span class="sxs-lookup"><span data-stu-id="4b095-248">Handling endpoint authentication</span></span>
<span data-ttu-id="4b095-249">Запросы от Azure Active Directory содержат токен носителя OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="4b095-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="4b095-250">Любой запрос службы принимающей hello должен проверить подлинность издателя hello как Azure Active Directory от имени клиента Azure Active Directory hello ожидалось, для доступа toohello веб-службы Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="4b095-250">Any service receiving hello request should authenticate hello issuer as being Azure Active Directory on behalf of hello expected Azure Active Directory tenant, for access toohello Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="4b095-251">В токене hello hello издателя идентифицируется утверждение iss, такие как «iss»: «https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/».</span><span class="sxs-lookup"><span data-stu-id="4b095-251">In hello token, hello issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="4b095-252">В этом примере базовый адрес hello hello значение утверждения, https://sts.windows.net, определяет Azure Active Directory, как hello издателя, пока hello относительный адрес сегмента, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, уникальный идентификатор hello Azure Active Клиент каталога, от имени которой hello выдачи токена.</span><span class="sxs-lookup"><span data-stu-id="4b095-252">In this example, hello base address of hello claim value, https://sts.windows.net, identifies Azure Active Directory as hello issuer, while hello relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of hello Azure Active Directory tenant on behalf of which hello token was issued.</span></span>  <span data-ttu-id="4b095-253">Если токен hello был выдан для доступа к веб-службы для Azure Active Directory Graph hello, затем hello идентификатор этой службы, 00000002-0000-0000-c000-000000000000, должны быть в значение hello aud hello токен утверждений.</span><span class="sxs-lookup"><span data-stu-id="4b095-253">If hello token was issued for accessing hello Azure Active Directory Graph web service, then hello identifier of that service, 00000002-0000-0000-c000-000000000000, should be in hello value of hello token’s aud claim.</span></span>  

<span data-ttu-id="4b095-254">Разработчики, использующие hello CLA библиотек, предоставляемых корпорацией Майкрософт для построения службы SCIM могут проходить проверку подлинности запросы от Azure Active Directory с помощью пакета Microsoft.Owin.Security.ActiveDirectory hello, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="4b095-254">Developers using hello CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using hello Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="4b095-255">В поставщике реализация свойства Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior hello наличием возвращать метод toobe, вызывается при каждом запуске службы hello:</span><span class="sxs-lookup"><span data-stu-id="4b095-255">In a provider, implement hello Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method toobe called whenever hello service is started:</span></span> 

  ````
    public override Action\<Owin.IAppBuilder, System.Web.Http.HttpConfiguration.HttpConfiguration\> StartupBehavior
    {
      get
      {
        return this.OnServiceStartup;
      }
    }

    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder,  // Defined in Owin.dll.  
      System.Web.Http.HttpConfiguration configuration)  // Defined in System.Web.Http.dll.  
    {
    }
  ````

2. <span data-ttu-id="4b095-256">Добавьте следующий код toothat метод toohave hello любой запрос tooany конечных точек службы hello, проверку подлинности как подшипника маркер, выданный службой Azure Active Directory от имени указанного клиента, для toohello доступа Azure AD Graph веб-службы:</span><span class="sxs-lookup"><span data-stu-id="4b095-256">Add hello following code toothat method toohave any request tooany of hello service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access toohello Azure AD Graph web service:</span></span> 

  ````
    private void OnServiceStartup(
      Owin.IAppBuilder applicationBuilder IAppBuilder applicationBuilder, 
      System.Web.Http.HttpConfiguration HttpConfiguration configuration)
    {
      // IFilter is defined in System.Web.Http.dll.  
      System.Web.Http.Filters.IFilter authorizationFilter = 
        new System.Web.Http.AuthorizeAttribute(); // Defined in System.Web.Http.dll.configuration.Filters.Add(authorizationFilter);

      // SystemIdentityModel.Tokens.TokenValidationParameters is defined in    
      // System.IdentityModel.Token.Jwt.dll.
      SystemIdentityModel.Tokens.TokenValidationParameters tokenValidationParameters =     
        new TokenValidationParameters()
        {
          ValidAudience = "00000002-0000-0000-c000-000000000000"
        };

      // WindowsAzureActiveDirectoryBearerAuthenticationOptions is defined in 
      // Microsoft.Owin.Security.ActiveDirectory.dll
      Microsoft.Owin.Security.ActiveDirectory.
      WindowsAzureActiveDirectoryBearerAuthenticationOptions authenticationOptions =
        new WindowsAzureActiveDirectoryBearerAuthenticationOptions()    {
        TokenValidationParameters = tokenValidationParameters,
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute hello appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="4b095-257">Схема пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="4b095-257">User and group schema</span></span>
<span data-ttu-id="4b095-258">Azure Active Directory можно подготовить два типа ресурсов tooSCIM веб-служб.</span><span class="sxs-lookup"><span data-stu-id="4b095-258">Azure Active Directory can provision two types of resources tooSCIM web services.</span></span>  <span data-ttu-id="4b095-259">Этими типами являются пользователи и группы.</span><span class="sxs-lookup"><span data-stu-id="4b095-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="4b095-260">Ресурсы пользовательского идентифицируются идентификатор схемы hello, urn: ietf:params:scim:schemas:extension:enterprise:2.0:User, который входит в данную спецификацию протокола: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="4b095-260">User resources are identified by hello schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="4b095-261">сопоставление по умолчанию Hello hello атрибутов пользователей в Azure Active Directory атрибуты toohello urn: ietf:params:scim:schemas:extension:enterprise:2.0:User ресурсов приведены в таблице 1, ниже.</span><span class="sxs-lookup"><span data-stu-id="4b095-261">hello default mapping of hello attributes of users in Azure Active Directory toohello attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="4b095-262">Ресурсы группы определяются hello идентификатор схемы, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="4b095-262">Group resources are identified by hello schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="4b095-263">В таблице 2 ниже показано сопоставление по умолчанию hello hello атрибутов групп в Azure Active Directory toohello атрибуты http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group ресурсов.</span><span class="sxs-lookup"><span data-stu-id="4b095-263">Table 2, below, shows hello default mapping of hello attributes of groups in Azure Active Directory toohello attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="4b095-264">Таблица 1. Сопоставление атрибутов пользователя по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4b095-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="4b095-265">Пользователь Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b095-265">Azure Active Directory user</span></span> | <span data-ttu-id="4b095-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="4b095-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="4b095-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="4b095-267">IsSoftDeleted</span></span> |<span data-ttu-id="4b095-268">активно</span><span class="sxs-lookup"><span data-stu-id="4b095-268">active</span></span> |
| <span data-ttu-id="4b095-269">displayName</span><span class="sxs-lookup"><span data-stu-id="4b095-269">displayName</span></span> |<span data-ttu-id="4b095-270">displayName</span><span class="sxs-lookup"><span data-stu-id="4b095-270">displayName</span></span> |
| <span data-ttu-id="4b095-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="4b095-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="4b095-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="4b095-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="4b095-273">givenName</span><span class="sxs-lookup"><span data-stu-id="4b095-273">givenName</span></span> |<span data-ttu-id="4b095-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="4b095-274">name.givenName</span></span> |
| <span data-ttu-id="4b095-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="4b095-275">jobTitle</span></span> |<span data-ttu-id="4b095-276">title</span><span class="sxs-lookup"><span data-stu-id="4b095-276">title</span></span> |
| <span data-ttu-id="4b095-277">mail</span><span class="sxs-lookup"><span data-stu-id="4b095-277">mail</span></span> |<span data-ttu-id="4b095-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="4b095-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="4b095-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="4b095-279">mailNickname</span></span> |<span data-ttu-id="4b095-280">externalId</span><span class="sxs-lookup"><span data-stu-id="4b095-280">externalId</span></span> |
| <span data-ttu-id="4b095-281">manager</span><span class="sxs-lookup"><span data-stu-id="4b095-281">manager</span></span> |<span data-ttu-id="4b095-282">manager</span><span class="sxs-lookup"><span data-stu-id="4b095-282">manager</span></span> |
| <span data-ttu-id="4b095-283">mobile</span><span class="sxs-lookup"><span data-stu-id="4b095-283">mobile</span></span> |<span data-ttu-id="4b095-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="4b095-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="4b095-285">objectId</span><span class="sxs-lookup"><span data-stu-id="4b095-285">objectId</span></span> |<span data-ttu-id="4b095-286">id</span><span class="sxs-lookup"><span data-stu-id="4b095-286">id</span></span> |
| <span data-ttu-id="4b095-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="4b095-287">postalCode</span></span> |<span data-ttu-id="4b095-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="4b095-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="4b095-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="4b095-289">proxy-Addresses</span></span> |<span data-ttu-id="4b095-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="4b095-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="4b095-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="4b095-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="4b095-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="4b095-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="4b095-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="4b095-293">streetAddress</span></span> |<span data-ttu-id="4b095-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="4b095-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="4b095-295">surname</span><span class="sxs-lookup"><span data-stu-id="4b095-295">surname</span></span> |<span data-ttu-id="4b095-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="4b095-296">name.familyName</span></span> |
| <span data-ttu-id="4b095-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="4b095-297">telephone-Number</span></span> |<span data-ttu-id="4b095-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="4b095-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="4b095-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="4b095-299">user-PrincipalName</span></span> |<span data-ttu-id="4b095-300">userName</span><span class="sxs-lookup"><span data-stu-id="4b095-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="4b095-301">Таблица 2. Сопоставление атрибутов группы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="4b095-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="4b095-302">Группа Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b095-302">Azure Active Directory group</span></span> | <span data-ttu-id="4b095-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="4b095-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="4b095-304">displayName</span><span class="sxs-lookup"><span data-stu-id="4b095-304">displayName</span></span> |<span data-ttu-id="4b095-305">externalId</span><span class="sxs-lookup"><span data-stu-id="4b095-305">externalId</span></span> |
| <span data-ttu-id="4b095-306">mail</span><span class="sxs-lookup"><span data-stu-id="4b095-306">mail</span></span> |<span data-ttu-id="4b095-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="4b095-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="4b095-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="4b095-308">mailNickname</span></span> |<span data-ttu-id="4b095-309">displayName</span><span class="sxs-lookup"><span data-stu-id="4b095-309">displayName</span></span> |
| <span data-ttu-id="4b095-310">members</span><span class="sxs-lookup"><span data-stu-id="4b095-310">members</span></span> |<span data-ttu-id="4b095-311">members</span><span class="sxs-lookup"><span data-stu-id="4b095-311">members</span></span> |
| <span data-ttu-id="4b095-312">objectId</span><span class="sxs-lookup"><span data-stu-id="4b095-312">objectId</span></span> |<span data-ttu-id="4b095-313">id</span><span class="sxs-lookup"><span data-stu-id="4b095-313">id</span></span> |
| <span data-ttu-id="4b095-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="4b095-314">proxyAddresses</span></span> |<span data-ttu-id="4b095-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="4b095-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="4b095-316">Подготовка и отзыв пользователей</span><span class="sxs-lookup"><span data-stu-id="4b095-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="4b095-317">Здравствуйте, следуя сообщений hello иллюстрации показано, что Azure Active Directory отправляет tooa службы SCIM toomanage жизненного цикла hello пользователя в другом хранилище удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4b095-317">hello following illustration shows hello messages that Azure Active Directory sends tooa SCIM service toomanage hello lifecycle of a user in another identity store.</span></span> <span data-ttu-id="4b095-318">Hello схема также показывает, как службы SCIM, реализовано с помощью библиотеки CLI hello предоставленная корпорацией Майкрософт для разработки, такие службы преобразования этих запросов в вызовы методов toohello поставщика.</span><span class="sxs-lookup"><span data-stu-id="4b095-318">hello diagram also shows how a SCIM service implemented using hello CLI libraries provided by Microsoft for building such services translate those requests into calls toohello methods of a provider.</span></span>  

<span data-ttu-id="4b095-319">![][4]
*Рисунок 5. Последовательность действий при подготовке и отзыве пользователя*</span><span class="sxs-lookup"><span data-stu-id="4b095-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="4b095-320">Запросы Azure Active Directory hello службу для пользователя со значением атрибута externalId сопоставления значения атрибута mailNickname hello пользователя в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="4b095-320">Azure Active Directory queries hello service for a user with an externalId attribute value matching hello mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="4b095-321">запрос Hello выражается как запрос протокола передачи гипертекста (HTTP), как показано в примере, при котором jyoung приводится образец mailNickname пользователя в Azure Active Directory:</span><span class="sxs-lookup"><span data-stu-id="4b095-321">hello query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="4b095-322">Если служба hello строится с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в toohello вызова метода запроса поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-322">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span>  <span data-ttu-id="4b095-323">Вот hello подпись этого метода.</span><span class="sxs-lookup"><span data-stu-id="4b095-323">Here is hello signature of that method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Protocol.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource[]> Query(
      Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters parameters, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="4b095-324">Вот hello определение интерфейса Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-324">Here is hello definition of hello Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
  ````
    public interface IQueryParameters: 
      Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
        System.Collections.Generic.IReadOnlyCollection <Microsoft.SystemForCrossDomainIdentityManagement.IFilter> AlternateFilters 
        { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IRetrievalParameters
    {
      system.Collections.Generic.IReadOnlyCollection<string> ExcludedAttributePaths 
      { get; }
      System.Collections.Generic.IReadOnlyCollection<string> RequestedAttributePaths 
      { get; }
      string SchemaIdentifier 
      { get; }
    }

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IFilter
    {
        Microsoft.SystemForCrossDomainIdentityManagement.IFilter AdditionalFilter 
          { get; set; }
        string AttributePath 
          { get; } 
        Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator FilterOperator 
          { get; }
        string ComparisonValue 
          { get; }
    }

    public enum Microsoft.SystemForCrossDomainIdentityManagement.ComparisonOperator
    {
        Equals
    }
  ````
  <span data-ttu-id="4b095-325">В следующий образец запроса для пользователя с указанным значением для атрибута externalId hello hello доступны следующие значения hello аргументов, передаваемых toohello метод запроса:</span><span class="sxs-lookup"><span data-stu-id="4b095-325">In hello following sample of a query for a user with a given value for hello externalId attribute, values of hello arguments passed toohello Query method are:</span></span> 
  * <span data-ttu-id="4b095-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="4b095-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="4b095-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="4b095-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="4b095-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="4b095-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="4b095-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="4b095-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="4b095-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="4b095-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="4b095-331">Если hello ответа tooa запроса toohello веб-службу для пользователя, имеющего значение атрибута externalId, соответствующее значению атрибута mailNickname hello пользователь возвращает всех пользователей, Azure Active Directory запрашивает, hello службы подготовки пользователя соответствующий toohello один в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b095-331">If hello response tooa query toohello web service for a user with an externalId attribute value that matches hello mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that hello service provision a user corresponding toohello one in Azure Active Directory.</span></span>  <span data-ttu-id="4b095-332">Ниже приведен пример такого запроса.</span><span class="sxs-lookup"><span data-stu-id="4b095-332">Here is an example of such a request:</span></span> 
  ````
    POST https://.../scim/Users HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas":
      [
        "urn:ietf:params:scim:schemas:core:2.0:User",
        "urn:ietf:params:scim:schemas:extension:enterprise:2.0User"],
      "externalId":"jyoung",
      "userName":"jyoung",
      "active":true,
      "addresses":null,
      "displayName":"Joy Young",
      "emails": [
        {
          "type":"work",
          "value":"jyoung@Contoso.com",
          "primary":true}],
      "meta": {
        "resourceType":"User"},
       "name":{
        "familyName":"Young",
        "givenName":"Joy"},
      "phoneNumbers":null,
      "preferredLanguage":null,
      "title":null,
      "department":null,
      "manager":null}
  ````
  <span data-ttu-id="4b095-333">Hello Общеязыковая инфраструктура библиотек, предоставляемых корпорацией Майкрософт для реализации службы SCIM преобразует этот запрос в toohello вызов метода Create поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-333">hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call toohello Create method of hello service’s provider.</span></span>  <span data-ttu-id="4b095-334">Метод Create Hello имеет следующую сигнатуру:</span><span class="sxs-lookup"><span data-stu-id="4b095-334">hello Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="4b095-335">В запрос tooprovision пользователя значение hello hello ресурсов аргумент является экземпляром hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="4b095-335">In a request tooprovision a user, hello value of hello resource argument is an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="4b095-336">Класс Core2EnterpriseUser, определенные в библиотеке Microsoft.SystemForCrossDomainIdentityManagement.Schemas hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-336">Core2EnterpriseUser class, defined in hello Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="4b095-337">Если tooprovision hello hello запрос пользователя завершается успешно, то hello реализация метода hello является ожидаемой tooreturn экземпляр hello Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="4b095-337">If hello request tooprovision hello user succeeds, then hello implementation of hello method is expected tooreturn an instance of hello Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="4b095-338">Класс Core2EnterpriseUser, со значением hello свойство идентификатора hello установить toohello уникальный идентификатор hello нового пользователя.</span><span class="sxs-lookup"><span data-stu-id="4b095-338">Core2EnterpriseUser class, with hello value of hello Identifier property set toohello unique identifier of hello newly provisioned user.</span></span>  

3. <span data-ttu-id="4b095-339">SCIM Azure Active Directory продолжается с помощью запроса службы hello hello текущее состояние этого пользователя с помощью запроса, таких как аппаратные tooupdate известные tooexist в хранилище удостоверение пользователя:</span><span class="sxs-lookup"><span data-stu-id="4b095-339">tooupdate a user known tooexist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting hello current state of that user from hello service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="4b095-340">В службе, построенных с использованием предоставленных корпорацией Майкрософт для реализации службы SCIM библиотеки Общеязыковая инфраструктура hello hello запрос преобразуется в вызов toohello метод получения поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-340">In a service built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, hello request is translated into a call toohello Retrieve method of hello service’s provider.</span></span>  <span data-ttu-id="4b095-341">Вот hello сигнатура метода извлечения hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-341">Here is hello signature of hello Retrieve method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource and 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
    // are defined in Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  
    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> 
       Retrieve(
         Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters 
           parameters, 
           string correlationIdentifier);

    public interface 
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceRetrievalParameters:   
        IRetrievalParameters
        {
          Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
            ResourceIdentifier 
              { get; }
    }
    public interface Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier
    {
        string Identifier 
          { get; set; }
        string Microsoft.SystemForCrossDomainIdentityManagement.SchemaIdentifier 
          { get; set; }
    }
  ````
  <span data-ttu-id="4b095-342">В примере hello запроса tooretrieve hello текущего состояния пользователя hello значения свойств hello hello объекта, предоставленных в качестве значения hello аргумента параметров hello определяются следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b095-342">In hello example of a request tooretrieve hello current state of a user, hello values of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="4b095-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="4b095-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="4b095-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="4b095-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="4b095-345">Если ссылочный атрибут toobe обновлена, затем Azure Active Directory запросы hello службы toodetermine ли hello текущее значение атрибута ссылки hello в хранилище удостоверений hello аппаратные hello службы уже соответствует значению hello этого атрибута в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="4b095-345">If a reference attribute is toobe updated, then Azure Active Directory queries hello service toodetermine whether or not hello current value of hello reference attribute in hello identity store fronted by hello service already matches hello value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="4b095-346">Для пользователей, из какой hello запрашивается текущее значение в этом случае единственным атрибутом hello является атрибутом диспетчер hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-346">For users, hello only attribute of which hello current value is queried in this way is hello manager attribute.</span></span> <span data-ttu-id="4b095-347">Ниже приведен пример toodetermine запрос ли атрибут manager hello объекта конкретного пользователя в настоящее время имеет определенное значение:</span><span class="sxs-lookup"><span data-stu-id="4b095-347">Here is an example of a request toodetermine whether hello manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="4b095-348">Здравствуйте, значение параметра запроса атрибуты hello, идентификатор, обозначает, удовлетворяющую hello выражение, предоставленное в качестве значения параметра запроса фильтра hello hello, если объект пользователя существует, то служба hello является ожидаемым toorespond с urn: ietf:params:scim:schemas: основной: 2.0:User или urn: ietf:params:scim:schemas:extension:enterprise:2.0:User ресурсов, включая только hello значение атрибута id этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="4b095-348">hello value of hello attributes query parameter, id, signifies that if a user object exists that satisfies hello expression provided as hello value of hello filter query parameter, then hello service is expected toorespond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only hello value of that resource’s id attribute.</span></span>  <span data-ttu-id="4b095-349">Здравствуйте, значение hello **идентификатор** атрибут известен toohello запрашивающей стороны.</span><span class="sxs-lookup"><span data-stu-id="4b095-349">hello value of hello **id** attribute is known toohello requestor.</span></span> <span data-ttu-id="4b095-350">Он включен в hello значение параметра запроса фильтра hello; Hello запрашиваются он предназначен фактически toorequest минимальное представление ресурса, удовлетворяющие hello критерий фильтра, как показатель того, является ли этих объекта существует.</span><span class="sxs-lookup"><span data-stu-id="4b095-350">It is included in hello value of hello filter query parameter; hello purpose of asking for it is actually toorequest a minimal representation of a resource that satisfying hello filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="4b095-351">Если служба hello строится с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в toohello вызова метода запроса поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-351">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Query method of hello service’s provider.</span></span> <span data-ttu-id="4b095-352">Hello значение свойства hello объекта hello, предоставленных в качестве значения hello аргумента параметров hello выглядят следующим образом:</span><span class="sxs-lookup"><span data-stu-id="4b095-352">hello value of hello properties of hello object provided as hello value of hello parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="4b095-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="4b095-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="4b095-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="4b095-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="4b095-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="4b095-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="4b095-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="4b095-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="4b095-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="4b095-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="4b095-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="4b095-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="4b095-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="4b095-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="4b095-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="4b095-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="4b095-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="4b095-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="4b095-362">Здесь hello значение индекса hello x может быть равно 0 и hello значение y hello индекс может быть 1, или значение hello x может быть 1 и hello значение y может быть равно 0, в зависимости от порядка hello hello выражений параметр запроса фильтра hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-362">Here, hello value of hello index x may be 0 and hello value of hello index y may be 1, or hello value of x may be 1 and hello value of y may be 0, depending on hello order of hello expressions of hello filter query parameter.</span></span>   

5. <span data-ttu-id="4b095-363">Ниже приведен пример запроса из Azure Active Directory tooan SCIM службы tooupdate пользователь:</span><span class="sxs-lookup"><span data-stu-id="4b095-363">Here is an example of a request from Azure Active Directory tooan SCIM service tooupdate a user:</span></span> 
  ````
    PATCH ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
    Content-type: application/json
    {
      "schemas": 
      [
        "urn:ietf:params:scim:api:messages:2.0:PatchOp"],
      "Operations":
      [
        {
          "op":"Add",
          "path":"manager",
          "value":
            [
              {
                "$ref":"http://.../scim/Users/2819c223-7f76-453a-919d-413861904646",
                "value":"2819c223-7f76-453a-919d-413861904646"}]}]}
  ````
  <span data-ttu-id="4b095-364">библиотеки Microsoft Общеязыковая инфраструктура Hello для реализации службы SCIM будут переводиться hello запроса toohello вызова метода Update поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-364">hello Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate hello request into a call toohello Update method of hello service’s provider.</span></span> <span data-ttu-id="4b095-365">Вот подпись hello hello метод обновления:</span><span class="sxs-lookup"><span data-stu-id="4b095-365">Here is hello signature of hello Update method:</span></span> 
  ````
    // System.Threading.Tasks.Tasks and 
    // System.Collections.Generic.IReadOnlyCollection<T>
    // are defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IPatch, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation, 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationName, 
    // Microsoft.SystemForCrossDomainIdentityManagement.IPath and 
    // Microsoft.SystemForCrossDomainIdentityManagement.OperationValue 
    // are all defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 

    System.Threading.Tasks.Task Update(
      Microsoft.SystemForCrossDomainIdentityManagement.IPatch patch, 
      string correlationIdentifier);

    public interface Microsoft.SystemForCrossDomainIdentityManagement.IPatch
    {
    Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase 
      PatchRequest 
        { get; set; }
    Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier 
      ResourceIdentifier 
        { get; set; }        
    }

    public class PatchRequest2: 
      Microsoft.SystemForCrossDomainIdentityManagement.PatchRequestBase
    {
    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation> 
        Operations
        { get;}

    public void AddOperation(
      Microsoft.SystemForCrossDomainIdentityManagement.PatchOperation operation);
    }

    public class PatchOperation
    {
    public Microsoft.SystemForCrossDomainIdentityManagement.OperationName 
      Name
      { get; set; }

    public Microsoft.SystemForCrossDomainIdentityManagement.IPath 
      Path
      { get; set; }

    public System.Collections.Generic.IReadOnlyCollection
      <Microsoft.SystemForCrossDomainIdentityManagement.OperationValue> Value
      { get; }

    public void AddValue(
      Microsoft.SystemForCrossDomainIdentityManagement.OperationValue value);
    }

    public enum OperationName
    {
      Add,
      Remove,
      Replace
    }

    public interface IPath
    {
      string AttributePath { get; }
      System.Collections.Generic.IReadOnlyCollection<IFilter> SubAttributes { get; }
      Microsoft.SystemForCrossDomainIdentityManagement.IPath ValuePath { get; }
    }

    public class OperationValue
    {
      public string Reference
      { get; set; }

      public string Value
      { get; set; }
    }
  ````
    <span data-ttu-id="4b095-366">В примере hello tooupdate запрос пользователя hello объекта, предоставленных в качестве значения hello аргумента исправление hello имеет значения этих свойств:</span><span class="sxs-lookup"><span data-stu-id="4b095-366">In hello example of a request tooupdate a user, hello object provided as hello value of hello patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="4b095-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="4b095-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="4b095-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="4b095-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="4b095-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="4b095-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="4b095-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="4b095-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="4b095-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="4b095-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="4b095-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="4b095-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="4b095-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="4b095-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="4b095-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="4b095-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="4b095-375">toode Подготовка пользователя из хранилища удостоверений аппаратные службой SCIM, Azure AD отправляет запрос, например:</span><span class="sxs-lookup"><span data-stu-id="4b095-375">toode-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="4b095-376">Если hello служба была создана с помощью библиотек Общеязыковая инфраструктура hello, предоставляемых корпорацией Майкрософт для реализации службы SCIM, hello запрос преобразуется в вызов toohello метод удаления поставщика услуг hello.</span><span class="sxs-lookup"><span data-stu-id="4b095-376">If hello service was built using hello Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then hello request is translated into a call toohello Delete method of hello service’s provider.</span></span>   <span data-ttu-id="4b095-377">Подпись метода Delete будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="4b095-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="4b095-378">значения этих свойств имеет Hello объекта, предоставленных в качестве значения hello аргумента resourceIdentifier hello в пример hello запроса toode подготовки пользователя:</span><span class="sxs-lookup"><span data-stu-id="4b095-378">hello object provided as hello value of hello resourceIdentifier argument has these property values in hello example of a request toode-provision a user:</span></span> 
  
  * <span data-ttu-id="4b095-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="4b095-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="4b095-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="4b095-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="4b095-381">Подготовка и отзыв групп</span><span class="sxs-lookup"><span data-stu-id="4b095-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="4b095-382">Здравствуйте, следуя сообщений hello иллюстрации показано, что Azure AcD отправляет tooa SCIM toomanage hello на протяжении срока службы группы в другом хранилище удостоверений.</span><span class="sxs-lookup"><span data-stu-id="4b095-382">hello following illustration shows hello messages that Azure AcD sends tooa SCIM service toomanage hello lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="4b095-383">Эти сообщения отличаются от hello относится toousers тремя способами:</span><span class="sxs-lookup"><span data-stu-id="4b095-383">Those messages differ from hello messages pertaining toousers in three ways:</span></span> 

* <span data-ttu-id="4b095-384">Схема Hello ресурс группы определяется как http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="4b095-384">hello schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="4b095-385">Запросы групп tooretrieve указания этого атрибута элементы hello — toobe, исключенные из любой ресурс, указанный в запросе toohello ответа.</span><span class="sxs-lookup"><span data-stu-id="4b095-385">Requests tooretrieve groups stipulate that hello members attribute is toobe excluded from any resource provided in response toohello request.</span></span>  
* <span data-ttu-id="4b095-386">Запросы toodetermine ли ссылочный атрибут имеет определенное значение — это запросы о hello элементов атрибута.</span><span class="sxs-lookup"><span data-stu-id="4b095-386">Requests toodetermine whether a reference attribute has a certain value are requests about hello members attribute.</span></span>  

<span data-ttu-id="4b095-387">![][5]
*Рисунок 6. Последовательность действий при подготовке и отзыве группы*</span><span class="sxs-lookup"><span data-stu-id="4b095-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="4b095-388">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="4b095-388">Related articles</span></span>
* [<span data-ttu-id="4b095-389">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4b095-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="4b095-390">Автоматизация пользователя подготовки и отзыва tooSaaS приложений</span><span class="sxs-lookup"><span data-stu-id="4b095-390">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="4b095-391">Настройка сопоставления атрибутов для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="4b095-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="4b095-392">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="4b095-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="4b095-393">Фильтры области для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="4b095-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="4b095-394">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="4b095-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="4b095-395">Список учебников по tooIntegrate приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="4b095-395">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
