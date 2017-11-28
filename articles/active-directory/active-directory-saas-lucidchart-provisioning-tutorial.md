---
title: "Руководство по настройке LucidChart для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooLucidChart."
services: active-directory
documentationcenter: 
author: asmalser-msft
writer: asmalser-msft
manager: stevenpo
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/14/2017
ms.author: asmalser-msft
ms.openlocfilehash: d3af45141731215f2edc8942ad21b016468c1e38
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-lucidchart-for-automatic-user-provisioning"></a><span data-ttu-id="0614d-103">Руководство по настройке LucidChart для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="0614d-103">Tutorial: Configuring LucidChart for Automatic User Provisioning</span></span>


<span data-ttu-id="0614d-104">Цель этого учебника Hello — hello действия, которые следует tooperform в LucidChart и Azure AD tooautomatically подготовки и Отмена подготовки учетных записей пользователей из Azure AD tooLucidChart tooshow.</span><span class="sxs-lookup"><span data-stu-id="0614d-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in LucidChart and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooLucidChart.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="0614d-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="0614d-105">Prerequisites</span></span>

<span data-ttu-id="0614d-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="0614d-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="0614d-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="0614d-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="0614d-108">Клиент LucidChart с hello [плана корпоративного](https://www.lucidchart.com/user/117598685#/subscriptionLevel) или лучше включена</span><span class="sxs-lookup"><span data-stu-id="0614d-108">A LucidChart tenant with hello [Enterprise plan](https://www.lucidchart.com/user/117598685#/subscriptionLevel) or better enabled</span></span> 
*   <span data-ttu-id="0614d-109">учетная запись пользователя в LucidChart с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="0614d-109">A user account in LucidChart with Admin permissions</span></span> 

## <a name="assigning-users-toolucidchart"></a><span data-ttu-id="0614d-110">Назначение пользователей tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="0614d-110">Assigning users tooLucidChart</span></span>

<span data-ttu-id="0614d-111">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="0614d-111">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="0614d-112">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0614d-112">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="0614d-113">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="0614d-113">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour LucidChart app.</span></span> <span data-ttu-id="0614d-114">После приняла решение, можно назначить эти приложения LucidChart tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="0614d-114">Once decided, you can assign these users tooyour LucidChart app by following hello instructions here:</span></span>

[<span data-ttu-id="0614d-115">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="0614d-115">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toolucidchart"></a><span data-ttu-id="0614d-116">Важные советы для назначения пользователей tooLucidChart</span><span class="sxs-lookup"><span data-stu-id="0614d-116">Important tips for assigning users tooLucidChart</span></span>

*   <span data-ttu-id="0614d-117">Рекомендуется один назначенный hello tootest tooLucidChart настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0614d-117">It is recommended that a single Azure AD user is assigned tooLucidChart tootest hello provisioning configuration.</span></span> <span data-ttu-id="0614d-118">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="0614d-118">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="0614d-119">При назначении tooLucidChart пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="0614d-119">When assigning a user tooLucidChart, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="0614d-120">Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="0614d-120">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toolucidchart"></a><span data-ttu-id="0614d-121">Настройка подготовки tooLucidChart пользователей</span><span class="sxs-lookup"><span data-stu-id="0614d-121">Configuring user provisioning tooLucidChart</span></span> 

<span data-ttu-id="0614d-122">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooLucidChart подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в LucidChart, в зависимости от назначения пользователей и групп в Azure AD .</span><span class="sxs-lookup"><span data-stu-id="0614d-122">This section guides you through connecting your Azure AD tooLucidChart's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in LucidChart based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="0614d-123">Можно также выбрать tooenabled на основе SAML Single Sign-On для LucidChart, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="0614d-123">You may also choose tooenabled SAML-based Single Sign-On for LucidChart, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="0614d-124">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="0614d-124">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toolucidchart-in-azure-ad"></a><span data-ttu-id="0614d-125">Настройка учетной записи автоматического пользователя подготовки tooLucidChart в Azure AD</span><span class="sxs-lookup"><span data-stu-id="0614d-125">Configure automatic user account provisioning tooLucidChart in Azure AD</span></span>


1. <span data-ttu-id="0614d-126">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="0614d-126">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="0614d-127">Если вы уже настроили LucidChart для единого входа, поиск экземпляра LucidChart с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="0614d-127">If you have already configured LucidChart for single sign-on, search for your instance of LucidChart using hello search field.</span></span> <span data-ttu-id="0614d-128">В противном случае выберите **добавить** и выполните поиск **LucidChart** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="0614d-128">Otherwise, select **Add** and search for **LucidChart** in hello application gallery.</span></span> <span data-ttu-id="0614d-129">Выберите LucidChart из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="0614d-129">Select LucidChart from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="0614d-130">Выберите свой экземпляр LucidChart, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="0614d-130">Select your instance of LucidChart, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="0614d-131">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="0614d-131">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Подготовка LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart1.png)

5. <span data-ttu-id="0614d-133">В разделе hello **учетные данные администратора** раздел, входной hello **секрет маркера** созданные вашей LucidChart учетной записи (hello токен можно найти под учетной записью: **Team**  >  **Интеграции приложения** > **SCIM**).</span><span class="sxs-lookup"><span data-stu-id="0614d-133">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your LucidChart's account (you can find hello token under your account: **Team** > **App Integration** > **SCIM**).</span></span> 

    ![Подготовка LucidChart](./media/active-directory-saas-lucidchart-provisioning-tutorial/LucidChart2.png)

6. <span data-ttu-id="0614d-135">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение LucidChart tooyour.</span><span class="sxs-lookup"><span data-stu-id="0614d-135">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour LucidChart app.</span></span> <span data-ttu-id="0614d-136">При сбое подключения hello, убедитесь, что ваша учетная запись LucidChart имеет разрешения администратора и повторите шаг 5.</span><span class="sxs-lookup"><span data-stu-id="0614d-136">If hello connection fails, ensure your LucidChart account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="0614d-137">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».</span><span class="sxs-lookup"><span data-stu-id="0614d-137">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="0614d-138">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0614d-138">Click **Save**.</span></span> 

9. <span data-ttu-id="0614d-139">Установите hello сопоставлений **tooLucidChart синхронизации Azure Active Directory — пользователи**.</span><span class="sxs-lookup"><span data-stu-id="0614d-139">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooLucidChart**.</span></span>

10. <span data-ttu-id="0614d-140">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooLucidChart Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0614d-140">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooLucidChart.</span></span> <span data-ttu-id="0614d-141">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в LucidChart для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="0614d-141">hello attributes selected as **Matching** properties are used toomatch hello user accounts in LucidChart for update operations.</span></span> <span data-ttu-id="0614d-142">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="0614d-142">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="0614d-143">tooenable hello подготовки службы Azure AD для LucidChart, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="0614d-143">tooenable hello Azure AD provisioning service for LucidChart, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="0614d-144">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="0614d-144">Click **Save**.</span></span> 

<span data-ttu-id="0614d-145">Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooLucidChart в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="0614d-145">This operation starts hello initial synchronization of any users and/or groups assigned tooLucidChart in hello Users and Groups section.</span></span> <span data-ttu-id="0614d-146">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="0614d-146">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="0614d-147">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.</span><span class="sxs-lookup"><span data-stu-id="0614d-147">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="0614d-148">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="0614d-148">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0614d-149">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="0614d-149">Additional resources</span></span>

* [<span data-ttu-id="0614d-150">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="0614d-150">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="0614d-151">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="0614d-151">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="0614d-152">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0614d-152">Next steps</span></span>

* [<span data-ttu-id="0614d-153">Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="0614d-153">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
