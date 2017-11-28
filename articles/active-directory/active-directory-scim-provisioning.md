---
title: "Использование SCIM для автоматической подготовки пользователей и групп Azure Active Directory для приложений | Документация Майкрософт"
description: "Azure Active Directory может выполнять автоматическую подготовку пользователей и групп для любого приложения или хранилища удостоверений, представляющим собой веб-службу с интерфейсом, определенным в спецификации протокола SCIM."
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
ms.openlocfilehash: 91978cee88d55c99bcb63c63cdaf01581ae84668
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="using-system-for-cross-domain-identity-management-to-automatically-provision-users-and-groups-from-azure-active-directory-to-applications"></a><span data-ttu-id="7a1ac-103">Использование SCIM для автоматической подготовки пользователей и групп Azure Active Directory для приложений</span><span class="sxs-lookup"><span data-stu-id="7a1ac-103">Using System for Cross-Domain Identity Management to automatically provision users and groups from Azure Active Directory to applications</span></span>

## <a name="overview"></a><span data-ttu-id="7a1ac-104">Обзор</span><span class="sxs-lookup"><span data-stu-id="7a1ac-104">Overview</span></span>
<span data-ttu-id="7a1ac-105">Azure Active Directory (Azure AD) может выполнять автоматическую подготовку пользователей и групп для любого приложения или хранилища удостоверений, представляющего собой веб-службу с интерфейсом, определенным в [спецификации протокола SCIM 2.0](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-105">Azure Active Directory (Azure AD) can automatically provision users and groups to any application or identity store that is fronted by a web service with the interface defined in the [System for Cross-Domain Identity Management (SCIM) 2.0 protocol specification](https://tools.ietf.org/html/draft-ietf-scim-api-19).</span></span> <span data-ttu-id="7a1ac-106">Azure Active Directory может отправлять веб-службе запросы на создание, изменение или удаление назначенных пользователей и групп.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-106">Azure Active Directory can send requests to create, modify, or delete assigned users and groups to the web service.</span></span> <span data-ttu-id="7a1ac-107">Веб-служба может преобразовывать эти запросы в операции с целевым хранилищем удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-107">The web service can then translate those requests into operations on the target identity store.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="7a1ac-108">Для управления службой Azure AD мы рекомендуем использовать [Центр администрирования Azure AD](https://aad.portal.azure.com) на портале Azure, а не классический портал Azure, который упоминается в этой статье.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-108">Microsoft recommends that you manage Azure AD using the [Azure AD admin center](https://aad.portal.azure.com) in the Azure portal instead of using the Azure classic portal referenced in this article.</span></span> 



<span data-ttu-id="7a1ac-109">![][0]
*Рисунок 1. Подготовка из Azure Active Directory в хранилище удостоверений через веб-службу*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-109">![][0]
*Figure 1: Provisioning from Azure Active Directory to an identity store via a web service*</span></span>

<span data-ttu-id="7a1ac-110">Эта функция в сочетании с возможностью использовать сторонние приложения (BYOA) в Azure AD позволяет организовать режим единого входа и автоматической подготовки пользователей для приложений, которые предоставляют веб-службу SCIM или используют интерфейс на ее основе.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-110">This capability can be used in conjunction with the “bring your own app” capability in Azure AD to enable single sign-on and automatic user provisioning for applications that provide or are fronted by a SCIM web service.</span></span>

<span data-ttu-id="7a1ac-111">Существуют два варианта использования SCIM в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-111">There are two use cases for using SCIM in Azure Active Directory:</span></span>

* <span data-ttu-id="7a1ac-112">**Подготовка пользователей и групп в приложениях, поддерживающих SCIM**. Приложения, которые поддерживают SCIM 2.0 и используют токены носителя OAuth для аутентификации, работают с Azure AD без дополнительной настройки.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-112">**Provisioning users and groups to applications that support SCIM** Applications that support SCIM 2.0 and use OAuth bearer tokens for authentication works with Azure AD without configuration.</span></span>
* <span data-ttu-id="7a1ac-113">**Сборка собственного решения подготовки для приложений, поддерживающих другую подготовку на основе API**. Для приложений, не поддерживающих SCIM, можно создать конечную точку SCIM для преобразования данных между конечной точкой SCIM Azure AD и любым API, поддерживаемым приложением для подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-113">**Build your own provisioning solution for applications that support other API-based provisioning** For non-SCIM applications, you can create a SCIM endpoint to translate between the Azure AD SCIM endpoint and any API the application supports for user provisioning.</span></span> <span data-ttu-id="7a1ac-114">Чтобы помочь вам в разработке конечной точки SCIM, мы предоставляем библиотеки Common Language Infrastructure (CLI), а также примеры кода, демонстрирующие подготовку конечной точки SCIM и преобразование сообщений SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-114">To help you develop a SCIM endpoint, we provide Common Language Infrastructure (CLI) libraries along with code samples that show you how to do provide a SCIM endpoint and translate SCIM messages.</span></span>  

## <a name="provisioning-users-and-groups-to-applications-that-support-scim"></a><span data-ttu-id="7a1ac-115">Подготовка пользователей и групп для приложений, поддерживающих SCIM</span><span class="sxs-lookup"><span data-stu-id="7a1ac-115">Provisioning users and groups to applications that support SCIM</span></span>
<span data-ttu-id="7a1ac-116">В Azure AD можно настроить автоматическую подготовку назначенных пользователей и групп для приложений, реализующих веб-службу [SCIM 2](https://tools.ietf.org/html/draft-ietf-scim-api-19) и принимающих токены носителя OAuth для аутентификации.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-116">Azure AD can be configured to automatically provision assigned users and groups to applications that implement a [System for Cross-domain Identity Management 2 (SCIM)](https://tools.ietf.org/html/draft-ietf-scim-api-19) web service and accept OAuth bearer tokens for authentication.</span></span> <span data-ttu-id="7a1ac-117">В спецификации SCIM 2.0 приложения должны удовлетворять следующим требованиям.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-117">Within the SCIM 2.0 specification, applications must meet these requirements:</span></span>

* <span data-ttu-id="7a1ac-118">Поддержка создания пользователей и групп, как описано в разделе 3.3 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-118">Supports creating users and/or groups, as per section 3.3 of the SCIM protocol.</span></span>  
* <span data-ttu-id="7a1ac-119">Поддержка изменения пользователей и групп с помощью запросов на исправление, как описано в разделе 3.5.2 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-119">Supports modifying users and/or groups with patch requests as per section 3.5.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="7a1ac-120">Поддержка получения известного ресурса, как описано в разделе 3.4.1 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-120">Supports retrieving a known resource as per section 3.4.1 of the SCIM protocol.</span></span>  
* <span data-ttu-id="7a1ac-121">Поддержка запросов пользователей и групп, как описано в разделе 3.4.2 протокола SCIM</span><span class="sxs-lookup"><span data-stu-id="7a1ac-121">Supports querying users and/or groups, as per section 3.4.2 of the SCIM protocol.</span></span>  <span data-ttu-id="7a1ac-122">(по умолчанию пользователи запрашиваются по атрибуту externalI, а группы по атрибуту displayName).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-122">By default, users are queried by externalId and groups are queried by displayName.</span></span>  
* <span data-ttu-id="7a1ac-123">Поддержка запросов пользователей по идентификатору и диспетчеру, как описано в разделе 3.4.2 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-123">Supports querying user by ID and by manager as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="7a1ac-124">Поддержка запросов групп по идентификатору и члену, как описано в разделе 3.4.2 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-124">Supports querying groups by ID and by member as per section 3.4.2 of the SCIM protocol.</span></span>  
* <span data-ttu-id="7a1ac-125">Принятие токенов носителя OAuth для авторизации, как описано в разделе 2.1 протокола SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-125">Accepts OAuth bearer tokens for authorization as per section 2.1 of the SCIM protocol.</span></span>

<span data-ttu-id="7a1ac-126">Рекомендуется связаться с поставщиком приложения или ознакомиться с документацией поставщика для получения подтверждения соответствия этим требованиям.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-126">Check with your application provider, or your application provider's documentation for statements of compatibility with these requirements.</span></span>

### <a name="getting-started"></a><span data-ttu-id="7a1ac-127">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="7a1ac-127">Getting started</span></span>
<span data-ttu-id="7a1ac-128">Описанные ранее в этой статье приложения, поддерживающие профиль SCIM, можно подключать к Azure Active Directory с помощью функции "Приложение не из коллекции", доступной в коллекции приложений Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-128">Applications that support the SCIM profile described in this article can be connected to Azure Active Directory using the "non-gallery application" feature in the Azure AD application gallery.</span></span> <span data-ttu-id="7a1ac-129">После подключения Azure AD запускает процесс синхронизации каждые 20 минут, запрашивая конечную точку SCIM приложения для получения назначенных пользователей и групп, и создает или изменяет их согласно сведениям о назначении.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-129">Once connected, Azure AD runs a synchronization process every 20 minutes where it queries the application's SCIM endpoint for assigned users and groups, and creates or modifies them according to the assignment details.</span></span>

<span data-ttu-id="7a1ac-130">**Подключение приложения, поддерживающего SCIM:**</span><span class="sxs-lookup"><span data-stu-id="7a1ac-130">**To connect an application that supports SCIM:**</span></span>

1. <span data-ttu-id="7a1ac-131">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-131">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="7a1ac-132">Выберите **"Azure Active Directory > Корпоративные приложения", затем выберите **Новое приложение > Все > Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-132">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="7a1ac-133">Введите имя приложения и щелкните значок **Добавить**, чтобы создать объект приложения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-133">Enter a name for your application, and click **Add** icon to create an app object.</span></span>
    
  <span data-ttu-id="7a1ac-134">![][1]
  *Рисунок 2. Использование коллекции приложений Azure AD*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-134">![][1]
*Figure 2: Azure AD application gallery*</span></span>
    
4. <span data-ttu-id="7a1ac-135">На отобразившемся экране выберите вкладку **Подготовка** в левом столбце.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-135">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="7a1ac-136">В меню **Режим подготовки к работе** выберите **Автоматический**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-136">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="7a1ac-137">![][2]
  *Рисунок 3. Настройка автоматической подготовки пользователей на портале Azure*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-137">![][2]
*Figure 3: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="7a1ac-138">В поле **URL-адрес клиента** введите URL-адрес конечной точки SCIM приложения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-138">In the **Tenant URL** field, enter the URL of the application's SCIM endpoint.</span></span> <span data-ttu-id="7a1ac-139">Пример: https://api.contoso.com/scim/v2/</span><span class="sxs-lookup"><span data-stu-id="7a1ac-139">Example: https://api.contoso.com/scim/v2/</span></span>
7. <span data-ttu-id="7a1ac-140">Если конечной точке SCIM требуется токен носителя OAuth от издателя, отличного от Azure AD, скопируйте необходимый токен носителя OAuth в необязательное для заполнения поле **Секретный токен**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-140">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="7a1ac-141">Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-141">If this field is left blank, then Azure AD included an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="7a1ac-142">Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-142">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="7a1ac-143">Нажмите кнопку **Проверить подключение**. Azure Active Directory попробует подключиться к конечной точке SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-143">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="7a1ac-144">Если подключиться не удастся, отобразятся сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-144">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="7a1ac-145">Если подключиться к приложению удалось, нажмите кнопку **Сохранить**, чтобы сохранить учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-145">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="7a1ac-146">В разделе **Сопоставления** доступны на выбор два набора сопоставлений атрибутов: для объектов-пользователей и для объектов групп.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-146">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="7a1ac-147">Выберите каждый из них, чтобы просмотреть атрибуты, которые синхронизируются из Azure Active Directory с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-147">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="7a1ac-148">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления пользователей и групп в вашем приложении для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-148">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="7a1ac-149">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-149">Select the Save button to commit any changes.</span></span>

    >[!NOTE]
    ><span data-ttu-id="7a1ac-150">При необходимости можно отключить синхронизацию объектов групп, отключив сопоставление групп.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-150">You can optionally disable syncing of group objects by disabling the "groups" mapping.</span></span> 

11. <span data-ttu-id="7a1ac-151">Поле **Область** в разделе **Параметры** определяет, какие пользователи или группы синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-151">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="7a1ac-152">Если выбрать параметр "Sync only assigned users and groups" (Синхронизировать только назначенных пользователей и группы) (рекомендуется), то будут синхронизированы только пользователи и группы, назначенные на вкладке **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-152">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="7a1ac-153">После завершения настройки измените значение параметра **Состояние подготовки** для **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-153">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="7a1ac-154">Нажмите кнопку **Сохранить**, чтобы запустить службу подготовки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-154">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="7a1ac-155">Если используется синхронизация только назначенных пользователей и групп (рекомендуется), не забудьте перейти на вкладку **Пользователи и группы** и назначить пользователей и (или) группы, которые требуется синхронизировать.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-155">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="7a1ac-156">После запуска начальной синхронизации для отслеживания хода выполнения можно использовать вкладку **Журналы аудита**. На ней отображаются все действия, выполняемые службой подготовки с приложением.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-156">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="7a1ac-157">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-157">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

>[!NOTE]
><span data-ttu-id="7a1ac-158">Начальная синхронизация занимает больше времени, чем последующие операции синхронизации. Последующие операции синхронизации выполняются примерно каждые 20 минут, при условии, что служба запущена.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-158">The initial sync takes longer to perform than subsequent syncs, which occur approximately every 20 minutes as long as the service is running.</span></span> 


## <a name="building-your-own-provisioning-solution-for-any-application"></a><span data-ttu-id="7a1ac-159">Создание собственного решения подготовки для любого приложения</span><span class="sxs-lookup"><span data-stu-id="7a1ac-159">Building your own provisioning solution for any application</span></span>
<span data-ttu-id="7a1ac-160">Создав веб-службу SCIM, взаимодействующую с Azure Active Directory, можно включить единый вход и автоматическую подготовку пользователей практически для любого приложения, которое предоставляет API подготовки пользователей REST или SOAP.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-160">By creating a SCIM web service that interfaces with Azure Active Directory, you can enable single sign-on and automatic user provisioning for virtually any application that provides a REST or SOAP user provisioning API.</span></span>

<span data-ttu-id="7a1ac-161">Вот как это работает</span><span class="sxs-lookup"><span data-stu-id="7a1ac-161">Here’s how it works:</span></span>

1. <span data-ttu-id="7a1ac-162">Azure AD предоставляет библиотеку CLI с именем [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-162">Azure AD provides a common language infrastructure library named [Microsoft.SystemForCrossDomainIdentityManagement](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/).</span></span> <span data-ttu-id="7a1ac-163">Системные интеграторы и разработчики на основе этой библиотеки могут создавать и развертывать SCIM-совместимые конечные точки, через которые Azure AD сможет подключаться к хранилищу удостоверений любого приложения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-163">System integrators and developers can use this library to create and deploy a SCIM-based web service endpoint capable of connecting Azure AD to any application’s identity store.</span></span>
2. <span data-ttu-id="7a1ac-164">Веб-служба реализует механизмы сопоставления стандартной пользовательской схемы c пользовательской схемой и протоколом, которые использует приложение.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-164">Mappings are implemented in the web service to map the standardized user schema to the user schema and protocol required by the application.</span></span>
3. <span data-ttu-id="7a1ac-165">Azure AD хранит URL-адрес конечной точки как часть информации о пользовательском приложении в коллекции приложений.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-165">The endpoint URL is registered in Azure AD as part of a custom application in the application gallery.</span></span>
4. <span data-ttu-id="7a1ac-166">Администратор назначает для этого приложения пользователей и группы в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-166">Users and groups are assigned to this application in Azure AD.</span></span> <span data-ttu-id="7a1ac-167">Azure AD помещает назначенных пользователей в очередь для синхронизации с целевым приложением.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-167">Upon assignment, they are put into a queue to be synchronized to the target application.</span></span> <span data-ttu-id="7a1ac-168">Процесс синхронизации каждые 20 минут выполняет задания из этой очереди.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-168">The synchronization process handling the queue runs every 20 minutes.</span></span>

### <a name="code-samples"></a><span data-ttu-id="7a1ac-169">Примеры кода</span><span class="sxs-lookup"><span data-stu-id="7a1ac-169">Code Samples</span></span>
<span data-ttu-id="7a1ac-170">Чтобы вам было проще разобраться, мы предлагаем [примеры кода](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) , которые создают конечную точку веб-службы SCIM и демонстрируют автоматическую подготовку пользователей.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-170">To make this process easier, a set of [code samples](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master) are provided that create a SCIM web service endpoint and demonstrate automatic provisioning.</span></span> <span data-ttu-id="7a1ac-171">В одном примере поставщик службы использует файл, в котором пользователи и группы представлены строками значений, разделенных запятыми.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-171">One sample is of a provider that maintains a file with rows of comma-separated values representing users and groups.</span></span>  <span data-ttu-id="7a1ac-172">Во втором примере поставщик использует службу идентификации и управления доступом Amazon Web Services.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-172">The other is of a provider that operates on the Amazon Web Services Identity and Access Management service.</span></span>  

<span data-ttu-id="7a1ac-173">**Предварительные требования**</span><span class="sxs-lookup"><span data-stu-id="7a1ac-173">**Prerequisites**</span></span>

* <span data-ttu-id="7a1ac-174">Visual Studio 2013 или более поздней версии</span><span class="sxs-lookup"><span data-stu-id="7a1ac-174">Visual Studio 2013 or later</span></span>
* [<span data-ttu-id="7a1ac-175">Пакет Azure SDK для .NET</span><span class="sxs-lookup"><span data-stu-id="7a1ac-175">Azure SDK for .NET</span></span>](https://azure.microsoft.com/downloads/)
* <span data-ttu-id="7a1ac-176">Компьютер под управлением Windows, поддерживающий платформу ASP.NET 4.5, на котором будет размещена конечная точка SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-176">Windows machine that supports the ASP.NET framework 4.5 to be used as the SCIM endpoint.</span></span> <span data-ttu-id="7a1ac-177">Этот компьютер должен быть доступен из облака.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-177">This machine must be accessible from the cloud</span></span>
* [<span data-ttu-id="7a1ac-178">Подписка Azure с пробной или лицензированной версией Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-178">An Azure subscription with a trial or licensed version of Azure AD Premium</span></span>](https://azure.microsoft.com/services/active-directory/)
* <span data-ttu-id="7a1ac-179">Для примера с Amazon AWS нужны библиотеки из [набора средств AWS для Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-179">The Amazon AWS sample requires libraries from the [AWS Toolkit for Visual Studio](http://docs.aws.amazon.com/AWSToolkitVS/latest/UserGuide/tkv_setup.html).</span></span> <span data-ttu-id="7a1ac-180">Дополнительная информация есть в файле сведений, включенном в пример.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-180">For more information, see the README file included with the sample.</span></span>

### <a name="getting-started"></a><span data-ttu-id="7a1ac-181">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="7a1ac-181">Getting Started</span></span>
<span data-ttu-id="7a1ac-182">Начнем с самого простого способа реализации конечной точки SCIM. Этот пример кода принимает запросы на подготовку от Azure AD и сохраняет пользователей в файл формата CSV (значения, разделенные запятыми).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-182">The easiest way to implement a SCIM endpoint that can accept provisioning requests from Azure AD is to build and deploy the code sample that outputs the provisioned users to a comma-separated value (CSV) file.</span></span>

<span data-ttu-id="7a1ac-183">**Создание конечной точки SCIM из этого примера:**</span><span class="sxs-lookup"><span data-stu-id="7a1ac-183">**To create a sample SCIM endpoint:**</span></span>

1. <span data-ttu-id="7a1ac-184">Загрузите пакет кода, расположенный по адресу [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span><span class="sxs-lookup"><span data-stu-id="7a1ac-184">Download the code sample package at [https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master](https://github.com/Azure/AzureAD-BYOA-Provisioning-Samples/tree/master)</span></span>
2. <span data-ttu-id="7a1ac-185">Распакуйте пакет и поместите его в любую удобную папку на компьютере Windows, например C:\AzureAD-BYOA-Provisioning-Samples.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-185">Unzip the package and place it on your Windows machine at a location such as C:\AzureAD-BYOA-Provisioning-Samples\.</span></span>
3. <span data-ttu-id="7a1ac-186">Запустите в Visual Studio решение FileProvisioningAgent из этой папки.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-186">In this folder, launch the FileProvisioningAgent solution in Visual Studio.</span></span>
4. <span data-ttu-id="7a1ac-187">Выберите **Инструменты > Library Package Manager (Диспетчер пакетов библиотеки) > Консоль диспетчера пакетов** и выполните приведенные ниже команды, чтобы разрешить ссылки на решения в проекте FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-187">Select **Tools > Library Package Manager > Package Manager Console**, and execute the following commands for the FileProvisioningAgent project to resolve the solution references:</span></span>
  ```` 
   Install-Package Microsoft.SystemForCrossDomainIdentityManagement
   Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory
   Install-Package Microsoft.Owin.Diagnostics
   Install-Package Microsoft.Owin.Host.SystemWeb
  ````
5. <span data-ttu-id="7a1ac-188">Соберите проект FileProvisioningAgent.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-188">Build the FileProvisioningAgent project.</span></span>
6. <span data-ttu-id="7a1ac-189">Запустите в Windows приложение командной строки (с правами администратора) и с помощью команды **cd** перейдите в каталог **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-189">Launch the Command Prompt application in Windows (as an Administrator), and use the **cd** command to change the directory to your **\AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug** folder.</span></span>
7. <span data-ttu-id="7a1ac-190">Выполните приведенную ниже команду, заменив <ip-address> IP-адресом или доменным именем компьютера Windows.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-190">Run the following command, replacing <ip-address> with the IP address or domain name of the Windows machine:</span></span>
  ````   
   FileAgnt.exe http://<ip-address>:9000 TargetFile.csv
  ````
8. <span data-ttu-id="7a1ac-191">В Windows откройте раздел **Параметры Windows > Параметры сети и Интернета**, выберите **Брандмауэр Windows > Дополнительные параметры** и создайте **правило для входящего трафика**, разрешающее входящий доступ к порту 9000.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-191">In Windows under **Windows Settings > Network & Internet Settings**, select the **Windows Firewall > Advanced Settings**, and create an **Inbound Rule** that allows inbound access to port 9000.</span></span>
9. <span data-ttu-id="7a1ac-192">Если компьютер Windows подключен через маршрутизатор, то на этом маршрутизаторе нужно настроить преобразование сетевых адресов между внешним портом 9000 и портом 9000 на компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-192">If the Windows machine is behind a router, the router needs to be configured to perform Network Access Translation between its port 9000 that is exposed to the internet, and port 9000 on the Windows machine.</span></span> <span data-ttu-id="7a1ac-193">Это необходимо, чтобы служба Azure AD могла получить доступ к этой конечной точке в облаке.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-193">This is required for Azure AD to be able to access this endpoint in the cloud.</span></span>

<span data-ttu-id="7a1ac-194">**Регистрация примера конечной точки SCIM в Azure AD:**</span><span class="sxs-lookup"><span data-stu-id="7a1ac-194">**To register the sample SCIM endpoint in Azure AD:**</span></span>

1. <span data-ttu-id="7a1ac-195">Войдите на [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-195">Sign in to [the Azure portal](https://portal.azure.com).</span></span> 
2. <span data-ttu-id="7a1ac-196">Выберите **"Azure Active Directory > Корпоративные приложения", затем выберите **Новое приложение > Все > Приложение не из коллекции**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-196">Browse to **Azure Active Directory > Enterprise Applications, and select **New application > All > Non-gallery application**.</span></span>
3. <span data-ttu-id="7a1ac-197">Введите имя приложения и щелкните значок **Добавить**, чтобы создать объект приложения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-197">Enter a name for your application, and click **Add** icon to create an app object.</span></span> <span data-ttu-id="7a1ac-198">Созданный объект приложения будет представлять не только конечную точку SCIM, но и все целевое приложение, для которого вы настраиваете подготовку пользователей и единый вход.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-198">The application object created is intended to represent the target app you would be provisioning to and implementing single sign-on for, and not just the SCIM endpoint.</span></span>
4. <span data-ttu-id="7a1ac-199">На отобразившемся экране выберите вкладку **Подготовка** в левом столбце.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-199">In the resulting screen, select the **Provisioning** tab in the left column.</span></span>
5. <span data-ttu-id="7a1ac-200">В меню **Режим подготовки к работе** выберите **Автоматический**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-200">In the **Provisioning Mode** menu, select **Automatic**.</span></span>
    
  <span data-ttu-id="7a1ac-201">![][2]
  *Рисунок 4. Настройка автоматической подготовки пользователей на портале Azure*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-201">![][2]
*Figure 4: Configuring provisioning in the Azure portal*</span></span>
    
6. <span data-ttu-id="7a1ac-202">В поле **URL-адрес клиента** введите доступные в Интернете URL-адрес и порт конечной точки SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-202">In the **Tenant URL** field, enter the internet-exposed URL and port of your SCIM endpoint.</span></span> <span data-ttu-id="7a1ac-203">Это будет строка типа http://testmachine.contoso.com:9000 или http://<IP-адрес>:9000 /, где <IP-адрес> является IP-адресом, доступным в Интернете.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-203">This would be something like http://testmachine.contoso.com:9000 or http://<ip-address>:9000/, where <ip-address> is the internet exposed IP address.</span></span>  
7. <span data-ttu-id="7a1ac-204">Если конечной точке SCIM требуется токен носителя OAuth от издателя, отличного от Azure AD, скопируйте необходимый токен носителя OAuth в необязательное для заполнения поле **Секретный токен**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-204">If the SCIM endpoint requires an OAuth bearer token from an issuer other than Azure AD, then copy the required OAuth bearer token into the optional **Secret Token** field.</span></span> <span data-ttu-id="7a1ac-205">Если оставить это поле пустым, то Azure AD будет добавлять в каждый запрос токен носителя OAuth, выданный Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-205">If this field is left blank, then Azure AD will include an OAuth bearer token issued from Azure AD with each request.</span></span> <span data-ttu-id="7a1ac-206">Приложения, использующие Azure AD в качестве поставщика удостоверений, могут проверить этот выданный Azure AD токен.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-206">Apps that use Azure AD as an identity provider can validate this Azure AD -issued token.</span></span>
8. <span data-ttu-id="7a1ac-207">Нажмите кнопку **Проверить подключение**. Azure Active Directory попробует подключиться к конечной точке SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-207">Click the **Test Connection** button to have Azure Active Directory attempt to connect to the SCIM endpoint.</span></span> <span data-ttu-id="7a1ac-208">Если подключиться не удастся, отобразятся сведения об ошибке.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-208">If the attempts fail, error information is displayed.</span></span>  
9. <span data-ttu-id="7a1ac-209">Если подключиться к приложению удалось, нажмите кнопку **Сохранить**, чтобы сохранить учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-209">If the attempts to connect to the application succeed, then click **Save** to save the admin credentials.</span></span>
10. <span data-ttu-id="7a1ac-210">В разделе **Сопоставления** доступны на выбор два набора сопоставлений атрибутов: для объектов-пользователей и для объектов групп.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-210">In the **Mappings** section, there are two selectable sets of attribute mappings: one for user objects and one for group objects.</span></span> <span data-ttu-id="7a1ac-211">Выберите каждый из них, чтобы просмотреть атрибуты, которые синхронизируются из Azure Active Directory с вашим приложением.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-211">Select each one to review the attributes that are synchronized from Azure Active Directory to your app.</span></span> <span data-ttu-id="7a1ac-212">Атрибуты, выбранные как свойства **Matching**, используются для сопоставления пользователей и групп в вашем приложении для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-212">The attributes selected as **Matching** properties are used to match the users and groups in your app for update operations.</span></span> <span data-ttu-id="7a1ac-213">Нажмите кнопку "Сохранить", чтобы подтвердить все изменения.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-213">Select the Save button to commit any changes.</span></span>
11. <span data-ttu-id="7a1ac-214">Поле **Область** в разделе **Параметры** определяет, какие пользователи или группы синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-214">Under **Settings**, the **Scope** field defines which users and or groups are synchronized.</span></span> <span data-ttu-id="7a1ac-215">Если выбрать параметр "Sync only assigned users and groups" (Синхронизировать только назначенных пользователей и группы) (рекомендуется), то будут синхронизированы только пользователи и группы, назначенные на вкладке **Пользователи и группы**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-215">Selecting "Sync only assigned users and groups" (recommended) will only sync users and groups assigned in the **Users and groups** tab.</span></span>
12. <span data-ttu-id="7a1ac-216">После завершения настройки измените значение параметра **Состояние подготовки** для **Включено**.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-216">Once your configuration is complete, change the **Provisioning Status** to **On**.</span></span>
13. <span data-ttu-id="7a1ac-217">Нажмите кнопку **Сохранить**, чтобы запустить службу подготовки Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-217">Click **Save** to start the Azure AD provisioning service.</span></span> 
14. <span data-ttu-id="7a1ac-218">Если используется синхронизация только назначенных пользователей и групп (рекомендуется), не забудьте перейти на вкладку **Пользователи и группы** и назначить пользователей и (или) группы, которые требуется синхронизировать.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-218">If syncing only assigned users and groups (recommended), be sure to select the **Users and groups** tab and assign the users and/or groups you wish to sync.</span></span>

<span data-ttu-id="7a1ac-219">После запуска начальной синхронизации для отслеживания хода выполнения можно использовать вкладку **Журналы аудита**. На ней отображаются все действия, выполняемые службой подготовки с приложением.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-219">Once the initial synchronization has started, you can use the **Audit logs** tab to monitor progress, which shows all actions performed by the provisioning service on your app.</span></span> <span data-ttu-id="7a1ac-220">Дополнительные сведения о чтении журналов подготовки Azure AD см. в руководстве по [отчетам об автоматической подготовке учетных записей](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="7a1ac-220">For more information on how to read the Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>

<span data-ttu-id="7a1ac-221">Наконец, последний этап проверки примера. Откройте файл TargetFile.csv в папке \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug на компьютере Windows.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-221">The final step in verifying the sample is to open the TargetFile.csv file in the \AzureAD-BYOA-Provisioning-Samples\ProvisioningAgent\bin\Debug folder on your Windows machine.</span></span> <span data-ttu-id="7a1ac-222">Когда процесс подготовки будет запущен, в этом файле отобразятся сведения обо всех пользователях и группах, которые были назначены и подготовлены.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-222">Once the provisioning process is run, this file shows the details of all assigned and provisioned users and groups.</span></span>

### <a name="development-libraries"></a><span data-ttu-id="7a1ac-223">Библиотеки для разработчика</span><span class="sxs-lookup"><span data-stu-id="7a1ac-223">Development libraries</span></span>
<span data-ttu-id="7a1ac-224">Чтобы разработать свою веб-службу, которая соответствует спецификации SCIM, ознакомьтесь с этими библиотеками Майкрософт, которые помогут ускорить процесс разработки.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-224">To develop your own web service that conforms to the SCIM specification, first familiarize yourself with the following libraries provided by Microsoft to help accelerate the development process:</span></span> 

1. <span data-ttu-id="7a1ac-225">Библиотеки Common Language Infrastructure (CLI) для использования с языками, основанными на этой инфраструктуре, например C#.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-225">Common Language Infrastructure (CLI) libraries are offered for use with languages based on that infrastructure, such as C#.</span></span> <span data-ttu-id="7a1ac-226">Одна из этих библиотек, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), объявляет интерфейс, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, показанный на следующем рисунке. Разработчик, использующий библиотеки, будет реализовывать этот интерфейс с помощью класса, на который в общем случае можно ссылаться как на поставщик.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-226">One of those libraries, [Microsoft.SystemForCrossDomainIdentityManagement.Service](https://www.nuget.org/packages/Microsoft.SystemForCrossDomainIdentityManagement/), declares an interface, Microsoft.SystemForCrossDomainIdentityManagement.IProvider, shown in the following illustration:  A developer using the libraries would implement that interface with a class that may be referred to, generically, as a provider.</span></span> <span data-ttu-id="7a1ac-227">Эти библиотеки позволяют разработчику развернуть веб-службу, которая соответствует спецификации SCIM.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-227">The libraries enable the developer to deploy a web service that conforms to the SCIM specification.</span></span> <span data-ttu-id="7a1ac-228">Эта веб-служба может размещаться в службах IIS или любой исполняемой сборке Common Language Infrastructure.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-228">The web service can be either hosted within Internet Information Services, or any executable Common Language Infrastructure assembly.</span></span> <span data-ttu-id="7a1ac-229">Запрос преобразовывается в вызовы методов поставщика, которые программирует разработчик для управления хранилищем удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-229">Request is translated into calls to the provider’s methods, which would be programmed by the developer to operate on some identity store.</span></span>
  
  ![][3]
  
2. <span data-ttu-id="7a1ac-230">[Обработчики ExpressRoute](http://expressjs.com/guide/routing.html) используются для анализа объектов запроса Node.js, которые представляют собой вызовы (как определено в спецификации SCIM), направленные к веб-службе Node.js.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-230">[Express route handlers](http://expressjs.com/guide/routing.html) are available for parsing node.js request objects representing calls (as defined by the SCIM specification), made to a node.js web service.</span></span>   

### <a name="building-a-custom-scim-endpoint"></a><span data-ttu-id="7a1ac-231">Создание пользовательской конечной точки SCIM</span><span class="sxs-lookup"><span data-stu-id="7a1ac-231">Building a Custom SCIM Endpoint</span></span>
<span data-ttu-id="7a1ac-232">Используя библиотеки CLI, разработчики могут размещать свои службы в любой исполняемой сборке Common Language Infrastructure или в службах IIS.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-232">Using the CLI libraries, developers using those libraries can host their services within any executable Common Language Infrastructure assembly, or within Internet Information Services.</span></span> <span data-ttu-id="7a1ac-233">Ниже приведен пример кода для размещения службы в исполняемой сборке по адресу http://localhost:9000.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-233">Here is sample code for hosting a service within an executable assembly, at the address http://localhost:9000:</span></span> 

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

<span data-ttu-id="7a1ac-234">Эта служба должна иметь HTTP-адрес и сертификат проверки подлинности сервера одного из следующих корневых центров сертификации:</span><span class="sxs-lookup"><span data-stu-id="7a1ac-234">This service must have an HTTP address and server authentication certificate of which the root certification authority is one of the following:</span></span> 

* <span data-ttu-id="7a1ac-235">CNNIC;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-235">CNNIC</span></span>
* <span data-ttu-id="7a1ac-236">Comodo;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-236">Comodo</span></span>
* <span data-ttu-id="7a1ac-237">CyberTrust;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-237">CyberTrust</span></span>
* <span data-ttu-id="7a1ac-238">DigiCert;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-238">DigiCert</span></span>
* <span data-ttu-id="7a1ac-239">GeoTrust;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-239">GeoTrust</span></span>
* <span data-ttu-id="7a1ac-240">GlobalSign;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-240">GlobalSign</span></span>
* <span data-ttu-id="7a1ac-241">Go Daddy;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-241">Go Daddy</span></span>
* <span data-ttu-id="7a1ac-242">VeriSign;</span><span class="sxs-lookup"><span data-stu-id="7a1ac-242">Verisign</span></span>
* <span data-ttu-id="7a1ac-243">WoSign.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-243">WoSign</span></span>

<span data-ttu-id="7a1ac-244">Сертификат проверки подлинности сервера можно привязать к порту на узле Windows с помощью служебной программы сетевой оболочки.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-244">A server authentication certificate can be bound to a port on a Windows host using the network shell utility:</span></span> 

    netsh http add sslcert ipport=0.0.0.0:443 certhash=0000000000003ed9cd0c315bbb6dc1c08da5e6 appid={00112233-4455-6677-8899-AABBCCDDEEFF}  

<span data-ttu-id="7a1ac-245">Здесь в качестве значения аргумента certhash предоставляется отпечаток сертификата, а в качестве значения аргумента appid — произвольный глобальный уникальный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-245">Here, the value provided for the certhash argument is the thumbprint of the certificate, while the value provided for the appid argument is an arbitrary globally unique identifier.</span></span>  

<span data-ttu-id="7a1ac-246">Чтобы разместить службу в службах IIS, разработчик должен создать сборку библиотеки кода CLA и определить класс Startup в пространстве имен по умолчанию для этой сборки.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-246">To host the service within Internet Information Services, a developer would build a CLA code library assembly with a class named Startup in the default namespace of the assembly.</span></span>  <span data-ttu-id="7a1ac-247">Ниже приведен пример такого класса.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-247">Here is a sample of such a class:</span></span> 

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

### <a name="handling-endpoint-authentication"></a><span data-ttu-id="7a1ac-248">Обработка аутентификации на конечной точке</span><span class="sxs-lookup"><span data-stu-id="7a1ac-248">Handling endpoint authentication</span></span>
<span data-ttu-id="7a1ac-249">Запросы от Azure Active Directory содержат токен носителя OAuth 2.0.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-249">Requests from Azure Active Directory include an OAuth 2.0 bearer token.</span></span>   <span data-ttu-id="7a1ac-250">Любая веб-служба, которая получит запрос, должна убедиться, что токен выдала служба Azure Active Directory от имени клиента Azure Active Directory для доступа к веб-службе Azure Active Directory Graph.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-250">Any service receiving the request should authenticate the issuer as being Azure Active Directory on behalf of the expected Azure Active Directory tenant, for access to the Azure Active Directory Graph web service.</span></span>  <span data-ttu-id="7a1ac-251">В токене издатель обозначается утверждением iss, которое имеет следующий вид: iss:https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-251">In the token, the issuer is identified by an iss claim, like, "iss":"https://sts.windows.net/cbb1a5ac-f33b-45fa-9bf5-f37db0fed422/".</span></span>  <span data-ttu-id="7a1ac-252">В этом примере базовый адрес утверждения со значением https://sts.windows.net подтверждает, что издателем является Azure Active Directory. Относительный адрес сегмента (cbb1a5ac-f33b-45fa-9bf5-f37db0fed422) — это уникальный идентификатор клиента Azure Active Directory, от имени которого выдан маркер.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-252">In this example, the base address of the claim value, https://sts.windows.net, identifies Azure Active Directory as the issuer, while the relative address segment, cbb1a5ac-f33b-45fa-9bf5-f37db0fed422, is a unique identifier of the Azure Active Directory tenant on behalf of which the token was issued.</span></span>  <span data-ttu-id="7a1ac-253">Если токен выпущен для доступа к веб-службе Azure Active Directory Graph, то утверждение aud такого токена должно иметь значение 00000002-0000-0000-c000-000000000000, то есть значение идентификатора этой веб-службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-253">If the token was issued for accessing the Azure Active Directory Graph web service, then the identifier of that service, 00000002-0000-0000-c000-000000000000, should be in the value of the token’s aud claim.</span></span>  

<span data-ttu-id="7a1ac-254">Разработчики, которые используют для создания службы SCIM предоставленные корпорацией Майкрософт библиотеки CLA, могут аутентифицировать запросы от Azure Active Directory с помощью пакета Microsoft.Owin.Security.ActiveDirectory. Для этого нужно выполнить следующие действия.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-254">Developers using the CLA libraries provided by Microsoft for building a SCIM service can authenticate requests from Azure Active Directory using the Microsoft.Owin.Security.ActiveDirectory package by following these steps:</span></span> 

1. <span data-ttu-id="7a1ac-255">Реализуйте в поставщике свойство Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior, которое будет возвращать метод, вызываемый при каждом запуске службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-255">In a provider, implement the Microsoft.SystemForCrossDomainIdentityManagement.IProvider.StartupBehavior property by having it return a method to be called whenever the service is started:</span></span> 

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

2. <span data-ttu-id="7a1ac-256">Добавьте в этот метод приведенный ниже код. Для всех запросов к любой из конечных точек службы этот метод будет проверять, является ли отправителем запроса служба Azure Active Directory, выпустившая токен от имени указанного клиента для доступа к веб-службе Azure AD Graph.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-256">Add the following code to that method to have any request to any of the service’s endpoints authenticated as bearing a token issued by Azure Active Directory on behalf of a specified tenant, for access to the Azure AD Graph web service:</span></span> 

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
        Tenant = "03F9FCBC-EA7B-46C2-8466-F81917F3C15E" // Substitute the appropriate tenant’s 
                                                      // identifier for this one.  
      };

      applicationBuilder.UseWindowsAzureActiveDirectoryBearerAuthentication(authenticationOptions);
    }
  ````


## <a name="user-and-group-schema"></a><span data-ttu-id="7a1ac-257">Схема пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="7a1ac-257">User and group schema</span></span>
<span data-ttu-id="7a1ac-258">Azure Active Directory может предоставлять веб-службе SCIM ресурсы двух типов.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-258">Azure Active Directory can provision two types of resources to SCIM web services.</span></span>  <span data-ttu-id="7a1ac-259">Этими типами являются пользователи и группы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-259">Those types of resources are users and groups.</span></span>  

<span data-ttu-id="7a1ac-260">Ресурс пользователя имеет идентификатор схемы urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, который включен в данную спецификацию протокола: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-260">User resources are identified by the schema identifier, urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, which is included in this protocol specification: http://tools.ietf.org/html/draft-ietf-scim-core-schema.</span></span>  <span data-ttu-id="7a1ac-261">Ниже в таблице 1 приводится используемое по умолчанию сопоставление атрибутов пользователей в Azure Active Directory и атрибутов ресурсов типа urn:ietf:params:scim:schemas:extension:enterprise:2.0:User.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-261">The default mapping of the attributes of users in Azure Active Directory to the attributes of urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resources is provided in table 1, below.</span></span>  

<span data-ttu-id="7a1ac-262">Ресурсы группы определяются по идентификатору схемы, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-262">Group resources are identified by the schema identifier, http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  <span data-ttu-id="7a1ac-263">Ниже в таблице 2 приводится используемое по умолчанию сопоставление атрибутов групп в Azure Active Directory и атрибутов ресурсов http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-263">Table 2, below, shows the default mapping of the attributes of groups in Azure Active Directory to the attributes of http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group resources.</span></span>  

### <a name="table-1-default-user-attribute-mapping"></a><span data-ttu-id="7a1ac-264">Таблица 1. Сопоставление атрибутов пользователя по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7a1ac-264">Table 1: Default user attribute mapping</span></span>
| <span data-ttu-id="7a1ac-265">Пользователь Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a1ac-265">Azure Active Directory user</span></span> | <span data-ttu-id="7a1ac-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span><span class="sxs-lookup"><span data-stu-id="7a1ac-266">urn:ietf:params:scim:schemas:extension:enterprise:2.0:User</span></span> |
| --- | --- |
| <span data-ttu-id="7a1ac-267">IsSoftDeleted</span><span class="sxs-lookup"><span data-stu-id="7a1ac-267">IsSoftDeleted</span></span> |<span data-ttu-id="7a1ac-268">активно</span><span class="sxs-lookup"><span data-stu-id="7a1ac-268">active</span></span> |
| <span data-ttu-id="7a1ac-269">displayName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-269">displayName</span></span> |<span data-ttu-id="7a1ac-270">displayName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-270">displayName</span></span> |
| <span data-ttu-id="7a1ac-271">Facsimile-TelephoneNumber</span><span class="sxs-lookup"><span data-stu-id="7a1ac-271">Facsimile-TelephoneNumber</span></span> |<span data-ttu-id="7a1ac-272">phoneNumbers[type eq "fax"].value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-272">phoneNumbers[type eq "fax"].value</span></span> |
| <span data-ttu-id="7a1ac-273">givenName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-273">givenName</span></span> |<span data-ttu-id="7a1ac-274">name.givenName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-274">name.givenName</span></span> |
| <span data-ttu-id="7a1ac-275">jobTitle</span><span class="sxs-lookup"><span data-stu-id="7a1ac-275">jobTitle</span></span> |<span data-ttu-id="7a1ac-276">title</span><span class="sxs-lookup"><span data-stu-id="7a1ac-276">title</span></span> |
| <span data-ttu-id="7a1ac-277">mail</span><span class="sxs-lookup"><span data-stu-id="7a1ac-277">mail</span></span> |<span data-ttu-id="7a1ac-278">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-278">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="7a1ac-279">mailNickname</span><span class="sxs-lookup"><span data-stu-id="7a1ac-279">mailNickname</span></span> |<span data-ttu-id="7a1ac-280">externalId</span><span class="sxs-lookup"><span data-stu-id="7a1ac-280">externalId</span></span> |
| <span data-ttu-id="7a1ac-281">manager</span><span class="sxs-lookup"><span data-stu-id="7a1ac-281">manager</span></span> |<span data-ttu-id="7a1ac-282">manager</span><span class="sxs-lookup"><span data-stu-id="7a1ac-282">manager</span></span> |
| <span data-ttu-id="7a1ac-283">mobile</span><span class="sxs-lookup"><span data-stu-id="7a1ac-283">mobile</span></span> |<span data-ttu-id="7a1ac-284">phoneNumbers[type eq "mobile"].value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-284">phoneNumbers[type eq "mobile"].value</span></span> |
| <span data-ttu-id="7a1ac-285">objectId</span><span class="sxs-lookup"><span data-stu-id="7a1ac-285">objectId</span></span> |<span data-ttu-id="7a1ac-286">id</span><span class="sxs-lookup"><span data-stu-id="7a1ac-286">id</span></span> |
| <span data-ttu-id="7a1ac-287">postalCode</span><span class="sxs-lookup"><span data-stu-id="7a1ac-287">postalCode</span></span> |<span data-ttu-id="7a1ac-288">addresses[type eq "work"].postalCode</span><span class="sxs-lookup"><span data-stu-id="7a1ac-288">addresses[type eq "work"].postalCode</span></span> |
| <span data-ttu-id="7a1ac-289">proxy-Addresses</span><span class="sxs-lookup"><span data-stu-id="7a1ac-289">proxy-Addresses</span></span> |<span data-ttu-id="7a1ac-290">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-290">emails[type eq "other"].Value</span></span> |
| <span data-ttu-id="7a1ac-291">physical-Delivery-OfficeName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-291">physical-Delivery-OfficeName</span></span> |<span data-ttu-id="7a1ac-292">addresses[type eq "other"].Formatted</span><span class="sxs-lookup"><span data-stu-id="7a1ac-292">addresses[type eq "other"].Formatted</span></span> |
| <span data-ttu-id="7a1ac-293">streetAddress</span><span class="sxs-lookup"><span data-stu-id="7a1ac-293">streetAddress</span></span> |<span data-ttu-id="7a1ac-294">addresses[type eq "work"].streetAddress</span><span class="sxs-lookup"><span data-stu-id="7a1ac-294">addresses[type eq "work"].streetAddress</span></span> |
| <span data-ttu-id="7a1ac-295">surname</span><span class="sxs-lookup"><span data-stu-id="7a1ac-295">surname</span></span> |<span data-ttu-id="7a1ac-296">name.familyName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-296">name.familyName</span></span> |
| <span data-ttu-id="7a1ac-297">telephone-Number</span><span class="sxs-lookup"><span data-stu-id="7a1ac-297">telephone-Number</span></span> |<span data-ttu-id="7a1ac-298">phoneNumbers[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-298">phoneNumbers[type eq "work"].value</span></span> |
| <span data-ttu-id="7a1ac-299">user-PrincipalName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-299">user-PrincipalName</span></span> |<span data-ttu-id="7a1ac-300">userName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-300">userName</span></span> |

### <a name="table-2-default-group-attribute-mapping"></a><span data-ttu-id="7a1ac-301">Таблица 2. Сопоставление атрибутов группы по умолчанию</span><span class="sxs-lookup"><span data-stu-id="7a1ac-301">Table 2: Default group attribute mapping</span></span>
| <span data-ttu-id="7a1ac-302">Группа Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a1ac-302">Azure Active Directory group</span></span> | <span data-ttu-id="7a1ac-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span><span class="sxs-lookup"><span data-stu-id="7a1ac-303">http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group</span></span> |
| --- | --- |
| <span data-ttu-id="7a1ac-304">displayName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-304">displayName</span></span> |<span data-ttu-id="7a1ac-305">externalId</span><span class="sxs-lookup"><span data-stu-id="7a1ac-305">externalId</span></span> |
| <span data-ttu-id="7a1ac-306">mail</span><span class="sxs-lookup"><span data-stu-id="7a1ac-306">mail</span></span> |<span data-ttu-id="7a1ac-307">emails[type eq "work"].value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-307">emails[type eq "work"].value</span></span> |
| <span data-ttu-id="7a1ac-308">mailNickname</span><span class="sxs-lookup"><span data-stu-id="7a1ac-308">mailNickname</span></span> |<span data-ttu-id="7a1ac-309">displayName</span><span class="sxs-lookup"><span data-stu-id="7a1ac-309">displayName</span></span> |
| <span data-ttu-id="7a1ac-310">members</span><span class="sxs-lookup"><span data-stu-id="7a1ac-310">members</span></span> |<span data-ttu-id="7a1ac-311">members</span><span class="sxs-lookup"><span data-stu-id="7a1ac-311">members</span></span> |
| <span data-ttu-id="7a1ac-312">objectId</span><span class="sxs-lookup"><span data-stu-id="7a1ac-312">objectId</span></span> |<span data-ttu-id="7a1ac-313">id</span><span class="sxs-lookup"><span data-stu-id="7a1ac-313">id</span></span> |
| <span data-ttu-id="7a1ac-314">proxyAddresses</span><span class="sxs-lookup"><span data-stu-id="7a1ac-314">proxyAddresses</span></span> |<span data-ttu-id="7a1ac-315">emails[type eq "other"].Value</span><span class="sxs-lookup"><span data-stu-id="7a1ac-315">emails[type eq "other"].Value</span></span> |

## <a name="user-provisioning-and-de-provisioning"></a><span data-ttu-id="7a1ac-316">Подготовка и отзыв пользователей</span><span class="sxs-lookup"><span data-stu-id="7a1ac-316">User provisioning and de-provisioning</span></span>
<span data-ttu-id="7a1ac-317">На рисунке ниже показаны сообщения, которые Azure Active Directory отправляет службе SCIM для управления жизненным циклом пользователя в стороннем хранилище удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-317">The following illustration shows the messages that Azure Active Directory sends to a SCIM service to manage the lifecycle of a user in another identity store.</span></span> <span data-ttu-id="7a1ac-318">Также схема демонстрирует, как служба SCIM, реализованная с помощью библиотек CLI корпорации Майкрософт для создания таких служб, преобразовывает эти запросы в вызовы методов поставщика.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-318">The diagram also shows how a SCIM service implemented using the CLI libraries provided by Microsoft for building such services translate those requests into calls to the methods of a provider.</span></span>  

<span data-ttu-id="7a1ac-319">![][4]
*Рисунок 5. Последовательность действий при подготовке и отзыве пользователя*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-319">![][4]
*Figure 5: User provisioning and de-provisioning sequence*</span></span>

1. <span data-ttu-id="7a1ac-320">Azure Active Directory запрашивает службу пользователя, у которого значение атрибута externalId совпадает со значением атрибута mailNickname пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-320">Azure Active Directory queries the service for a user with an externalId attribute value matching the mailNickname attribute value of a user in Azure AD.</span></span> <span data-ttu-id="7a1ac-321">Запрос имеет вид HTTP-запроса, пример которого приведен ниже. Значение jyoung в этом запросе обозначает идентификатор mailNickname пользователя Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-321">The query is expressed as a Hypertext Transfer Protocol (HTTP) request such as this example, wherein jyoung is a sample of a mailNickname of a user in Azure Active Directory:</span></span> 
  ````
    GET https://.../scim/Users?filter=externalId eq jyoung HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="7a1ac-322">Если служба создана с использованием библиотек Common Language Infrastructure корпорации Майкрософт для реализации служб SCIM, то такой запрос будет преобразован в вызов метода Query поставщика службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-322">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span>  <span data-ttu-id="7a1ac-323">Подпись этого метода будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="7a1ac-323">Here is the signature of that method:</span></span> 
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
  <span data-ttu-id="7a1ac-324">Ниже приводится определение интерфейса Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-324">Here is the definition of the Microsoft.SystemForCrossDomainIdentityManagement.IQueryParameters interface:</span></span> 
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
  <span data-ttu-id="7a1ac-325">В вышеприведенном примере запроса пользователя с определенным значением атрибута externalId в метод Query передаются следующие значения аргументов.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-325">In the following sample of a query for a user with a given value for the externalId attribute, values of the arguments passed to the Query method are:</span></span> 
  * <span data-ttu-id="7a1ac-326">parameters.AlternateFilters.Count: 1</span><span class="sxs-lookup"><span data-stu-id="7a1ac-326">parameters.AlternateFilters.Count: 1</span></span>
  * <span data-ttu-id="7a1ac-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-327">parameters.AlternateFilters.ElementAt(0).AttributePath: "externalId"</span></span>
  * <span data-ttu-id="7a1ac-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="7a1ac-328">parameters.AlternateFilters.ElementAt(0).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="7a1ac-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-329">parameters.AlternateFilter.ElementAt(0).ComparisonValue: "jyoung"</span></span>
  * <span data-ttu-id="7a1ac-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span><span class="sxs-lookup"><span data-stu-id="7a1ac-330">correlationIdentifier: System.Net.Http.HttpRequestMessage.GetOwinEnvironment["owin.RequestId"]</span></span> 

2. <span data-ttu-id="7a1ac-331">Если на запрос пользователя с определенным значением атрибута externalId, совпадающим со значением атрибута mailNickname пользователя, веб-служба вернет ответ, не содержащий пользователей, то Azure Active Directory отправит запрос к этой службе на подготовку пользователя, соответствующего пользователю в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-331">If the response to a query to the web service for a user with an externalId attribute value that matches the mailNickname attribute value of a user does not return any users, then Azure Active Directory requests that the service provision a user corresponding to the one in Azure Active Directory.</span></span>  <span data-ttu-id="7a1ac-332">Ниже приведен пример такого запроса.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-332">Here is an example of such a request:</span></span> 
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
  <span data-ttu-id="7a1ac-333">Библиотеки CLI, разработанные корпорацией Майкрософт для реализации служб SCIM, преобразуют этот запрос в вызов метода Create поставщика услуг.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-333">The Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services would translate that request into a call to the Create method of the service’s provider.</span></span>  <span data-ttu-id="7a1ac-334">Подпись метода Create будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="7a1ac-334">The Create method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.Resource is defined in 
    // Microsoft.SystemForCrossDomainIdentityManagement.Schemas.  

    System.Threading.Tasks.Task<Microsoft.SystemForCrossDomainIdentityManagement.Resource> Create(
      Microsoft.SystemForCrossDomainIdentityManagement.Resource resource, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="7a1ac-335">В запросе на подготовку пользователя в аргументе resource передается экземпляр класса Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-335">In a request to provision a user, the value of the resource argument is an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="7a1ac-336">Core2EnterpriseUser, определенного в библиотеке Microsoft.SystemForCrossDomainIdentityManagement.Schemas.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-336">Core2EnterpriseUser class, defined in the Microsoft.SystemForCrossDomainIdentityManagement.Schemas library.</span></span>  <span data-ttu-id="7a1ac-337">Если запрос на подготовку пользователя завершается успешно, реализованный в службе метод должен вернуть экземпляр класса Microsoft.SystemForCrossDomainIdentityManagement.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-337">If the request to provision the user succeeds, then the implementation of the method is expected to return an instance of the Microsoft.SystemForCrossDomainIdentityManagement.</span></span> <span data-ttu-id="7a1ac-338">Core2EnterpriseUser, в котором свойство Identifier имеет значение уникального идентификатора подготовленного пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-338">Core2EnterpriseUser class, with the value of the Identifier property set to the unique identifier of the newly provisioned user.</span></span>  

3. <span data-ttu-id="7a1ac-339">Для обновления пользователя, уже существующего в хранилище удостоверений с интерфейсом SCIM, Azure Active Directory запросит у службы текущее состояние этого пользователя, отправив запрос следующего вида.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-339">To update a user known to exist in an identity store fronted by an SCIM, Azure Active Directory proceeds by requesting the current state of that user from the service with a request such as:</span></span> 
  ````
    GET ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="7a1ac-340">Если служба создана с использованием библиотек CLI корпорации Майкрософт для реализации служб SCIM, то такой запрос будет преобразован в вызов метода Retrieve поставщика службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-340">In a service built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, the request is translated into a call to the Retrieve method of the service’s provider.</span></span>  <span data-ttu-id="7a1ac-341">Подпись метода Retrieve будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="7a1ac-341">Here is the signature of the Retrieve method:</span></span> 
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
  <span data-ttu-id="7a1ac-342">В приведенном выше примере запроса на получение текущего состояния пользователя в качестве значения аргумента parameters будет передан объект со следующими значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-342">In the example of a request to retrieve the current state of a user, the values of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="7a1ac-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-343">Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="7a1ac-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-344">SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

4. <span data-ttu-id="7a1ac-345">Если требуется обновить атрибут ссылки, Azure Active Directory передает службе запрос с требованием проверить, совпадает ли текущее значение атрибута ссылки в хранилище удостоверений с текущим значением этого атрибута в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-345">If a reference attribute is to be updated, then Azure Active Directory queries the service to determine whether or not the current value of the reference attribute in the identity store fronted by the service already matches the value of that attribute in Azure Active Directory.</span></span> <span data-ttu-id="7a1ac-346">Для пользователей таким способом запрашивается только значение атрибута manager.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-346">For users, the only attribute of which the current value is queried in this way is the manager attribute.</span></span> <span data-ttu-id="7a1ac-347">Ниже приведен пример запроса на проверку значения атрибута manager для определенного пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-347">Here is an example of a request to determine whether the manager attribute of a particular user object currently has a certain value:</span></span> 
  ````
    GET ~/scim/Users?filter=id eq 54D382A4-2050-4C03-94D1-E769F1D15682 and manager eq 2819c223-7f76-453a-919d-413861904646&attributes=id HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="7a1ac-348">Значение id для параметра attributes в запросе означает, что, если существует объект пользователя, который соответствует выражению, переданному в параметре filter запроса, служба должна вернуть ресурс urn:ietf:params:scim:schemas:core:2.0:User или urn:ietf:params:scim:schemas:extension:enterprise:2.0:User, в котором установлено только значение атрибута id.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-348">The value of the attributes query parameter, id, signifies that if a user object exists that satisfies the expression provided as the value of the filter query parameter, then the service is expected to respond with a urn:ietf:params:scim:schemas:core:2.0:User or urn:ietf:params:scim:schemas:extension:enterprise:2.0:User resource, including only the value of that resource’s id attribute.</span></span>  <span data-ttu-id="7a1ac-349">Значение атрибута **id** известно запросившей стороне.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-349">The value of the **id** attribute is known to the requestor.</span></span> <span data-ttu-id="7a1ac-350">Оно включено в параметр filter запроса. Фактически этот атрибут запрашивается, чтобы узнать, существует ли такой объект. В ответе будет представлен минимально определенный ресурс, отвечающий критериям фильтра.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-350">It is included in the value of the filter query parameter; the purpose of asking for it is actually to request a minimal representation of a resource that satisfying the filter expression as an indication of whether or not any such object exists.</span></span>   

  <span data-ttu-id="7a1ac-351">Если служба создана с использованием библиотек Common Language Infrastructure корпорации Майкрософт для реализации служб SCIM, то такой запрос будет преобразован в вызов метода Query поставщика службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-351">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Query method of the service’s provider.</span></span> <span data-ttu-id="7a1ac-352">В нем передается аргумент parameters, значением которого будет объект со следующими свойствами.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-352">The value of the properties of the object provided as the value of the parameters argument are as follows:</span></span> 
  
  * <span data-ttu-id="7a1ac-353">parameters.AlternateFilters.Count: 2</span><span class="sxs-lookup"><span data-stu-id="7a1ac-353">parameters.AlternateFilters.Count: 2</span></span>
  * <span data-ttu-id="7a1ac-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-354">parameters.AlternateFilters.ElementAt(x).AttributePath: "id"</span></span>
  * <span data-ttu-id="7a1ac-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="7a1ac-355">parameters.AlternateFilters.ElementAt(x).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="7a1ac-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-356">parameters.AlternateFilter.ElementAt(x).ComparisonValue: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="7a1ac-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-357">parameters.AlternateFilters.ElementAt(y).AttributePath: "manager"</span></span>
  * <span data-ttu-id="7a1ac-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span><span class="sxs-lookup"><span data-stu-id="7a1ac-358">parameters.AlternateFilters.ElementAt(y).ComparisonOperator: ComparisonOperator.Equals</span></span>
  * <span data-ttu-id="7a1ac-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-359">parameters.AlternateFilter.ElementAt(y).ComparisonValue: "2819c223-7f76-453a-919d-413861904646"</span></span>
  * <span data-ttu-id="7a1ac-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-360">parameters.RequestedAttributePaths.ElementAt(0): "id"</span></span>
  * <span data-ttu-id="7a1ac-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-361">parameters.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

  <span data-ttu-id="7a1ac-362">Здесь значение индекса «x» будет равно 0, а значение индекса «y» — 1 или наоборот, в зависимости от порядка выражений в параметре filter запроса.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-362">Here, the value of the index x may be 0 and the value of the index y may be 1, or the value of x may be 1 and the value of y may be 0, depending on the order of the expressions of the filter query parameter.</span></span>   

5. <span data-ttu-id="7a1ac-363">Ниже приведен пример запроса от Azure Active Directory к службе SCIM для обновления пользователя.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-363">Here is an example of a request from Azure Active Directory to an SCIM service to update a user:</span></span> 
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
  <span data-ttu-id="7a1ac-364">Библиотеки Microsoft CLI для реализации службы SCIM преобразуют такой запрос в вызов метода Update поставщика услуги.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-364">The Microsoft Common Language Infrastructure libraries for implementing SCIM services would translate the request into a call to the Update method of the service’s provider.</span></span> <span data-ttu-id="7a1ac-365">Подпись метода Update выглядит следующим образом.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-365">Here is the signature of the Update method:</span></span> 
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
    <span data-ttu-id="7a1ac-366">В примере запроса на обновление пользователя в качестве значения аргумента patch передается объект со следующими значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-366">In the example of a request to update a user, the object provided as the value of the patch argument has these property values:</span></span> 
  
  * <span data-ttu-id="7a1ac-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-367">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="7a1ac-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-368">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>
  * <span data-ttu-id="7a1ac-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span><span class="sxs-lookup"><span data-stu-id="7a1ac-369">(PatchRequest as PatchRequest2).Operations.Count: 1</span></span>
  * <span data-ttu-id="7a1ac-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span><span class="sxs-lookup"><span data-stu-id="7a1ac-370">(PatchRequest as PatchRequest2).Operations.ElementAt(0).OperationName: OperationName.Add</span></span>
  * <span data-ttu-id="7a1ac-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-371">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Path.AttributePath: "manager"</span></span>
  * <span data-ttu-id="7a1ac-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span><span class="sxs-lookup"><span data-stu-id="7a1ac-372">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.Count: 1</span></span>
  * <span data-ttu-id="7a1ac-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="7a1ac-373">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Reference: http://.../scim/Users/2819c223-7f76-453a-919d-413861904646</span></span>
  * <span data-ttu-id="7a1ac-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span><span class="sxs-lookup"><span data-stu-id="7a1ac-374">(PatchRequest as PatchRequest2).Operations.ElementAt(0).Value.ElementAt(0).Value: 2819c223-7f76-453a-919d-413861904646</span></span>

6. <span data-ttu-id="7a1ac-375">Для отзыва пользователя из хранилища удостоверений, интерфейсом для которого является служба SCIM, Azure AD отправляет запрос следующего вида.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-375">To de-provision a user from an identity store fronted by an SCIM service, Azure AD sends a request such as:</span></span> 
  ````
    DELETE ~/scim/Users/54D382A4-2050-4C03-94D1-E769F1D15682 HTTP/1.1
    Authorization: Bearer ...
  ````
  <span data-ttu-id="7a1ac-376">Если служба создана с использованием библиотек Common Language Infrastructure корпорации Майкрософт для реализации служб SCIM, то такой запрос будет преобразован в вызов метода Delete поставщика службы.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-376">If the service was built using the Common Language Infrastructure libraries provided by Microsoft for implementing SCIM services, then the request is translated into a call to the Delete method of the service’s provider.</span></span>   <span data-ttu-id="7a1ac-377">Подпись метода Delete будет выглядеть так:</span><span class="sxs-lookup"><span data-stu-id="7a1ac-377">That method has this signature:</span></span> 
  ````
    // System.Threading.Tasks.Tasks is defined in mscorlib.dll.  
    // Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier, 
    // is defined in Microsoft.SystemForCrossDomainIdentityManagement.Protocol. 
    System.Threading.Tasks.Task Delete(
      Microsoft.SystemForCrossDomainIdentityManagement.IResourceIdentifier  
        resourceIdentifier, 
      string correlationIdentifier);
  ````
  <span data-ttu-id="7a1ac-378">В примере запроса на отзыв пользователя в качестве значения аргумента resourceIdentifier передается объект со следующими значениями свойств.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-378">The object provided as the value of the resourceIdentifier argument has these property values in the example of a request to de-provision a user:</span></span> 
  
  * <span data-ttu-id="7a1ac-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-379">ResourceIdentifier.Identifier: "54D382A4-2050-4C03-94D1-E769F1D15682"</span></span>
  * <span data-ttu-id="7a1ac-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span><span class="sxs-lookup"><span data-stu-id="7a1ac-380">ResourceIdentifier.SchemaIdentifier: "urn:ietf:params:scim:schemas:extension:enterprise:2.0:User"</span></span>

## <a name="group-provisioning-and-de-provisioning"></a><span data-ttu-id="7a1ac-381">Подготовка и отзыв групп</span><span class="sxs-lookup"><span data-stu-id="7a1ac-381">Group provisioning and de-provisioning</span></span>
<span data-ttu-id="7a1ac-382">На рисунке ниже показаны сообщения, которые Azure AD отправляет службе SCIM для управления жизненным циклом группы в стороннем хранилище удостоверений.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-382">The following illustration shows the messages that Azure AcD sends to a SCIM service to manage the lifecycle of a group in another identity store.</span></span>  <span data-ttu-id="7a1ac-383">Эти сообщения имеют три отличия от сообщений, относящихся к пользователям.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-383">Those messages differ from the messages pertaining to users in three ways:</span></span> 

* <span data-ttu-id="7a1ac-384">Схема ресурса группы идентифицируется как http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-384">The schema of a group resource is identified as http://schemas.microsoft.com/2006/11/ResourceManagement/ADSCIM/Group.</span></span>  
* <span data-ttu-id="7a1ac-385">В запросах на получение групп по умолчанию предполагается, что из всех возвращаемых ресурсов исключается атрибут members.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-385">Requests to retrieve groups stipulate that the members attribute is to be excluded from any resource provided in response to the request.</span></span>  
* <span data-ttu-id="7a1ac-386">Запросы, которые должны определить, имеет ли ссылочный атрибут указанное значение, применяются в отношении атрибута members.</span><span class="sxs-lookup"><span data-stu-id="7a1ac-386">Requests to determine whether a reference attribute has a certain value are requests about the members attribute.</span></span>  

<span data-ttu-id="7a1ac-387">![][5]
*Рисунок 6. Последовательность действий при подготовке и отзыве группы*</span><span class="sxs-lookup"><span data-stu-id="7a1ac-387">![][5]
*Figure 6: Group provisioning and de-provisioning sequence*</span></span>

## <a name="related-articles"></a><span data-ttu-id="7a1ac-388">Связанные статьи</span><span class="sxs-lookup"><span data-stu-id="7a1ac-388">Related articles</span></span>
* [<span data-ttu-id="7a1ac-389">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a1ac-389">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="7a1ac-390">Автоматическая подготовка пользователей и ее отзыв для приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="7a1ac-390">Automate User Provisioning/Deprovisioning to SaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="7a1ac-391">Настройка сопоставления атрибутов для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7a1ac-391">Customizing Attribute Mappings for User Provisioning</span></span>](active-directory-saas-customizing-attribute-mappings.md)
* [<span data-ttu-id="7a1ac-392">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="7a1ac-392">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="7a1ac-393">Фильтры области для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="7a1ac-393">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="7a1ac-394">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="7a1ac-394">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="7a1ac-395">Список учебников по интеграции приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="7a1ac-395">List of Tutorials on How to Integrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[0]: ./media/active-directory-scim-provisioning/scim-figure-1.PNG
[1]: ./media/active-directory-scim-provisioning/scim-figure-2a.PNG
[2]: ./media/active-directory-scim-provisioning/scim-figure-2b.PNG
[3]: ./media/active-directory-scim-provisioning/scim-figure-3.PNG
[4]: ./media/active-directory-scim-provisioning/scim-figure-4.PNG
[5]: ./media/active-directory-scim-provisioning/scim-figure-5.PNG
