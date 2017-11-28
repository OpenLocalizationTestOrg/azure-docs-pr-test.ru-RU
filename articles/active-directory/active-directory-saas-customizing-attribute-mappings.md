---
title: "aaaCustomizing сопоставления атрибутов Azure AD | Документы Microsoft"
description: "Узнать, какие сопоставления атрибутов для приложений SaaS в Azure Active Directory как их можно изменить tooaddress бизнеса требуется."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 549e0b8c-87ce-4c9b-b487-b7bf0155dc77
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: markvi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 14db5303f06fc8df3b07a0a8b75713312e71bbfd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="customizing-user-provisioning-attribute-mappings-for-saas-applications-in-azure-active-directory"></a><span data-ttu-id="fd4b2-103">Настройка сопоставлений атрибутов для подготовки пользователей для приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd4b2-103">Customizing User Provisioning Attribute Mappings for SaaS Applications in Azure Active Directory</span></span>
<span data-ttu-id="fd4b2-104">Microsoft Azure AD обеспечивает поддержку для приложений SaaS сторонних toothird Salesforce, Google Apps и другие подготовки пользователей.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-104">Microsoft Azure AD provides support for user provisioning toothird-party SaaS applications such as Salesforce, Google Apps and others.</span></span> <span data-ttu-id="fd4b2-105">Если у вас есть подготовки пользователей для приложений SaaS сторонних разработчиков, hello портала управления Azure определяет значения его атрибутов в форме конфигурации, называемой «сопоставление атрибутов».</span><span class="sxs-lookup"><span data-stu-id="fd4b2-105">If you have user provisioning for a third-party SaaS application enabled, hello Azure Management Portal controls its attribute values in form of a configuration called “attribute mapping.”</span></span>

<span data-ttu-id="fd4b2-106">Существует набор предварительно настроенных сопоставлений атрибутов между объектами пользователей Azure AD и каждого приложения SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-106">There is a preconfigured set of attribute mappings between Azure AD user objects and each SaaS app’s user objects.</span></span> <span data-ttu-id="fd4b2-107">Некоторые приложения управляют другими типами объектов, такими как группы или контакты.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-107">Some apps manage other types of objects, such as Groups or Contacts.</span></span> <br> 
 <span data-ttu-id="fd4b2-108">Можно настроить в соответствии с потребностями бизнеса tooyour сопоставления атрибута по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-108">You can customize hello default attribute mappings according tooyour business needs.</span></span> <span data-ttu-id="fd4b2-109">Это означает, что можно изменить или удалить существующие сопоставления атрибутов или создать новые.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-109">This means, you can change or delete existing attribute mappings or create new attribute mappings.</span></span>

<span data-ttu-id="fd4b2-110">На портале hello Azure AD, эту функцию можно открыть, щелкнув **сопоставления** конфигурации в разделе **Provisioning** в hello **управление** раздел  **Корпоративное приложение**.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-110">In hello Azure AD portal, you can access this feature by clicking a **Mappings** configuration under **Provisioning** in hello **Manage** section of an **Enterprise application**.</span></span>


![Salesforce][5] 

<span data-ttu-id="fd4b2-112">Щелкнув **сопоставления** конфигурации, открывается hello связанные **сопоставление атрибута** колонку.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-112">Clicking a **Mappings** configuration, opens hello related **Attribute Mapping** blade.</span></span>  
<span data-ttu-id="fd4b2-113">Существуют сопоставления атрибутов, необходимых для приложения SaaS toofunction правильно.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-113">There are attribute mappings that are required by a SaaS application toofunction correctly.</span></span> <span data-ttu-id="fd4b2-114">Обязательные атрибуты hello **удалить** компонент недоступен.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-114">For required attributes, hello **Delete** feature is unavailable.</span></span>


![Salesforce][6]  

<span data-ttu-id="fd4b2-116">В приведенном выше примере hello, вы увидите, что hello **Username** атрибут управляемого объекта в Salesforce заполняется hello **userPrincipalName** значение hello связанный объект Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-116">In hello example above, you can see that hello **Username** attribute of a managed object in Salesforce is populated with hello **userPrincipalName** value of hello linked Azure Active Directory Object.</span></span>

<span data-ttu-id="fd4b2-117">Щелкнув сопоставление, вы можете настроить **Сопоставления атрибутов**.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-117">You can customize existing **Attribute Mappings** by clicking a mapping.</span></span> <span data-ttu-id="fd4b2-118">При этом откроется hello **изменение атрибута** колонку.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-118">This opens hello **Edit Attribute** blade.</span></span>

![Salesforce][7]  


  

## <a name="understanding-attribute-mapping-types"></a><span data-ttu-id="fd4b2-120">Основные сведения о типах сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="fd4b2-120">Understanding attribute mapping types</span></span>
<span data-ttu-id="fd4b2-121">С помощью сопоставлений атрибутов можно управлять заполнением атрибутов в сторонних приложениях SaaS.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-121">With attribute mappings, you control how attributes are populated in a third-party SaaS application.</span></span> <span data-ttu-id="fd4b2-122">Поддерживаются четыре типа сопоставлений.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-122">There are four different mapping types supported:</span></span>

* <span data-ttu-id="fd4b2-123">**Прямой** — hello целевой атрибут заполняется значением атрибута связанного объекта hello hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-123">**Direct** – hello target attribute is populated with hello value of an attribute of hello linked object in Azure AD.</span></span>
* <span data-ttu-id="fd4b2-124">**Константа** — hello целевой атрибут заполняется определенной строки были выбраны.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-124">**Constant** – hello target attribute is populated with a specific string you have specified.</span></span>
* <span data-ttu-id="fd4b2-125">**Выражение** -hello целевой атрибут заполняется на основе hello результата выражения like скрипта.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-125">**Expression** - hello target attribute is populated based on hello result of a script-like expression.</span></span> 
  <span data-ttu-id="fd4b2-126">Дополнительные сведения см. в статье [Запись выражений для сопоставления атрибутов в Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span><span class="sxs-lookup"><span data-stu-id="fd4b2-126">For more information, see [Writing Expressions for Attribute Mappings in Azure Active Directory](active-directory-saas-writing-expressions-for-attribute-mappings.md).</span></span>
* <span data-ttu-id="fd4b2-127">**Нет** -hello целевой атрибут оставляется без изменений.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-127">**None** - hello target attribute is left unmodified.</span></span> <span data-ttu-id="fd4b2-128">Однако hello целевой атрибут пуст, заполняется значением по умолчанию hello, указываемое.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-128">However, if hello target attribute is ever empty, it is populated with hello Default value that you specify.</span></span>

<span data-ttu-id="fd4b2-129">В дополнение toothese четырех основных типов сопоставлений атрибутов, настраиваемые сопоставления атрибутов поддерживают концепцию hello необязательный **по умолчанию** назначения значений.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-129">In addition toothese four basic attribute mapping types, custom attribute mappings support hello concept of an optional **default** value assignment.</span></span> <span data-ttu-id="fd4b2-130">значение по умолчанию Hello гарантирует, что целевой атрибут заполняется со значением, если нет значения ни в Azure AD, ни hello целевого объекта.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-130">hello default value assignment ensures that a target attribute is populated with a value if there is neither a value in Azure AD nor on hello target object.</span></span> <span data-ttu-id="fd4b2-131">Самая обычная конфигурация Hello — tooleave этом пустым.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-131">hello most common configuration is tooleave this blank.</span></span>


## <a name="understanding-attribute-mapping-properties"></a><span data-ttu-id="fd4b2-132">Основные сведения о свойствах сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="fd4b2-132">Understanding attribute mapping properties</span></span>

<span data-ttu-id="fd4b2-133">В предыдущем разделе hello уже были введено toohello атрибута сопоставления типа свойства.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-133">In hello previous section, you have already been introduced toohello attribute mapping type property.</span></span>
<span data-ttu-id="fd4b2-134">В свойстве toothis сложения сопоставления атрибутов также поддерживают hello следующие атрибуты:</span><span class="sxs-lookup"><span data-stu-id="fd4b2-134">In addition toothis property, attribute mappings do also support hello following attributes:</span></span>

- <span data-ttu-id="fd4b2-135">**Исходный атрибут** -атрибут пользователя hello из исходной системы hello (например: Azure Active Directory).</span><span class="sxs-lookup"><span data-stu-id="fd4b2-135">**Source attribute** - hello user attribute from hello source system (e.g.: Azure Active Directory).</span></span>
- <span data-ttu-id="fd4b2-136">**Целевой атрибут** — атрибут пользователя hello в целевой системе hello (например: ServiceNow).</span><span class="sxs-lookup"><span data-stu-id="fd4b2-136">**Target attribute** – hello user attribute in hello target system (e.g.: ServiceNow).</span></span>
- <span data-ttu-id="fd4b2-137">**Сопоставления объектов с помощью этого атрибута** — ли это сопоставление можно использовать toouniquely идентификации пользователей между исходной и целевой системами hello.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-137">**Match objects using this attribute** – Whether or not this mapping should be used toouniquely identify users between hello source and target systems.</span></span> <span data-ttu-id="fd4b2-138">Обычно устанавливается на hello userPrincipalName или атрибут mail в Azure AD, как правило, сопоставленного поля имени пользователя tooa в целевом приложении.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-138">This is typically set on hello userPrincipalName or mail attribute in Azure AD, which is typically mapped tooa username field in a target application.</span></span>
- <span data-ttu-id="fd4b2-139">**Приоритет сопоставления** — возможность указания нескольких атрибутов сопоставления.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-139">**Matching precedence** – Multiple matching attributes can be set.</span></span> <span data-ttu-id="fd4b2-140">Если существует несколько, они вычисляются в порядке hello, определенные по этому полю.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-140">When there are multiple, they are evaluated in hello order defined by this field.</span></span> <span data-ttu-id="fd4b2-141">Как только соответствие найдено, дальнейшие атрибуты сопоставления не вычисляются.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-141">As soon as a match is found, no further matching attributes are evaluated.</span></span>
- <span data-ttu-id="fd4b2-142">**Применить это сопоставление**</span><span class="sxs-lookup"><span data-stu-id="fd4b2-142">**Apply this mapping**</span></span>
    - <span data-ttu-id="fd4b2-143">**Всегда** — применить это сопоставление как при создании, так и при обновлении пользователей</span><span class="sxs-lookup"><span data-stu-id="fd4b2-143">**Always** – Apply this mapping on both user creation and update actions</span></span>
    - <span data-ttu-id="fd4b2-144">**Только при создании** — применить это сопоставление только при создании пользователей</span><span class="sxs-lookup"><span data-stu-id="fd4b2-144">**Only during creation** - Apply this mapping only on user creation actions</span></span>


## <a name="what-you-should-know"></a><span data-ttu-id="fd4b2-145">Необходимая информация</span><span class="sxs-lookup"><span data-stu-id="fd4b2-145">What you should know</span></span>

<span data-ttu-id="fd4b2-146">Процесс синхронизации в Microsoft Azure AD реализован очень эффективно.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-146">Microsoft Azure AD provides an efficient implementation of a synchronization process.</span></span> <span data-ttu-id="fd4b2-147">Во время цикла синхронизации в инициализированной среде обрабатываются только объекты, требующие обновления.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-147">In an initialized environment, only objects requiring updates are processed during a synchronization cycle.</span></span> <span data-ttu-id="fd4b2-148">Обновление сопоставлений атрибутов оказывает влияние на производительность hello цикла синхронизации.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-148">Updating attribute mappings has an impact on hello performance of a synchronization cycle.</span></span> <span data-ttu-id="fd4b2-149">Обновление настройки сопоставления атрибута toohello требует всех toobe управляемых объектов вычислены.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-149">An update toohello attribute mapping configuration requires all managed objects toobe reevaluated.</span></span> <span data-ttu-id="fd4b2-150">Это рекомендуемый лучший подход tookeep hello число последовательных изменений сопоставлений атрибутов tooyour как минимум.</span><span class="sxs-lookup"><span data-stu-id="fd4b2-150">It is a recommended best practice tookeep hello number of consecutive changes tooyour attribute mappings at a minimum.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fd4b2-151">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fd4b2-151">Next steps</span></span>

* [<span data-ttu-id="fd4b2-152">Указатель статьей по управлению приложениями в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="fd4b2-152">Article Index for Application Management in Azure Active Directory</span></span>](active-directory-apps-index.md)
* [<span data-ttu-id="fd4b2-153">Автоматизация пользователя подготовки и отзыва tooSaaS приложений</span><span class="sxs-lookup"><span data-stu-id="fd4b2-153">Automate User Provisioning/Deprovisioning tooSaaS Apps</span></span>](active-directory-saas-app-provisioning.md)
* [<span data-ttu-id="fd4b2-154">Запись выражений для сопоставления атрибутов</span><span class="sxs-lookup"><span data-stu-id="fd4b2-154">Writing Expressions for Attribute Mappings</span></span>](active-directory-saas-writing-expressions-for-attribute-mappings.md)
* [<span data-ttu-id="fd4b2-155">Фильтры области для подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="fd4b2-155">Scoping Filters for User Provisioning</span></span>](active-directory-saas-scoping-filters.md)
* [<span data-ttu-id="fd4b2-156">С помощью SCIM tooenable автоматическую подготовку пользователей и групп из Azure Active Directory tooapplications</span><span class="sxs-lookup"><span data-stu-id="fd4b2-156">Using SCIM tooenable automatic provisioning of users and groups from Azure Active Directory tooapplications</span></span>](active-directory-scim-provisioning.md)
* [<span data-ttu-id="fd4b2-157">Уведомления о подготовке учетных записей</span><span class="sxs-lookup"><span data-stu-id="fd4b2-157">Account Provisioning Notifications</span></span>](active-directory-saas-account-provisioning-notifications.md)
* [<span data-ttu-id="fd4b2-158">Список учебников по tooIntegrate приложений SaaS</span><span class="sxs-lookup"><span data-stu-id="fd4b2-158">List of Tutorials on How tooIntegrate SaaS Apps</span></span>](active-directory-saas-tutorial-list.md)

<!--Image references-->
[1]: ./media/active-directory-saas-customizing-attribute-mappings/ic765497.png
[2]: ./media/active-directory-saas-customizing-attribute-mappings/ic775419.png
[3]: ./media/active-directory-saas-customizing-attribute-mappings/ic775420.png
[4]: ./media/active-directory-saas-customizing-attribute-mappings/ic775421.png
[5]: ./media/active-directory-saas-customizing-attribute-mappings/21.png
[6]: ./media/active-directory-saas-customizing-attribute-mappings/22.png
[7]: ./media/active-directory-saas-customizing-attribute-mappings/23.png

