---
title: "Руководство по настройке ThousandEyes для автоматической подготовки пользователей с помощью Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как tooconfigure Azure Active Directory tooautomatically подготовки и Отмена подготовки учетных записей пользователей tooThousandEyes."
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
ms.openlocfilehash: f31883ab685d0ffcd9a830aa4a7d43c056f5f4cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-configuring-thousandeyes-for-automatic-user-provisioning"></a><span data-ttu-id="f4800-103">Руководство по настройке ThousandEyes для автоматической подготовки пользователей</span><span class="sxs-lookup"><span data-stu-id="f4800-103">Tutorial: Configuring ThousandEyes for Automatic User Provisioning</span></span>


<span data-ttu-id="f4800-104">Цель этого учебника Hello — hello шаги требуются tooperform в ThousandEyes и Azure AD tooautomatically подготовки и отменять подготовки учетных записей пользователей из Azure AD tooThousandEyes tooshow.</span><span class="sxs-lookup"><span data-stu-id="f4800-104">hello objective of this tutorial is tooshow you hello steps you need tooperform in ThousandEyes and Azure AD tooautomatically provision and de-provision user accounts from Azure AD tooThousandEyes.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="f4800-105">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="f4800-105">Prerequisites</span></span>

<span data-ttu-id="f4800-106">Hello сценарий, описанный в этом руководстве предполагается, что уже hello следующих элементов:</span><span class="sxs-lookup"><span data-stu-id="f4800-106">hello scenario outlined in this tutorial assumes that you already have hello following items:</span></span>

*   <span data-ttu-id="f4800-107">клиент Azure Active Directory;</span><span class="sxs-lookup"><span data-stu-id="f4800-107">An Azure Active directory tenant</span></span>
*   <span data-ttu-id="f4800-108">Клиент ThousandEyes с hello [стандартного плана](https://www.thousandeyes.com/pricing) или лучше включена</span><span class="sxs-lookup"><span data-stu-id="f4800-108">A ThousandEyes tenant with hello [Standard plan](https://www.thousandeyes.com/pricing) or better enabled</span></span> 
*   <span data-ttu-id="f4800-109">учетная запись пользователя ThousandEyes с разрешениями администратора.</span><span class="sxs-lookup"><span data-stu-id="f4800-109">A user account in ThousandEyes with Admin permissions</span></span> 

> [!NOTE]
> <span data-ttu-id="f4800-110">Hello подготовки интеграции Azure AD использует hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), являющийся tooThousandEyes доступные команды на плана Standard hello и более.</span><span class="sxs-lookup"><span data-stu-id="f4800-110">hello Azure AD provisioning integration relies on hello [ThousandEyes SCIM API](https://success.thousandeyes.com/PublicArticlePage?articleIdParam=kA044000000CnWrCAK), which is available tooThousandEyes teams on hello Standard plan or better.</span></span>

## <a name="assigning-users-toothousandeyes"></a><span data-ttu-id="f4800-111">Назначение пользователей tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="f4800-111">Assigning users tooThousandEyes</span></span>

<span data-ttu-id="f4800-112">Azure Active Directory использует называемый «назначения» toodetermine пользователей, которые должны получать доступ tooselected приложений.</span><span class="sxs-lookup"><span data-stu-id="f4800-112">Azure Active Directory uses a concept called "assignments" toodetermine which users should receive access tooselected apps.</span></span> <span data-ttu-id="f4800-113">В контексте hello автоматический подготовки пользователей. учетной записи синхронизируются только hello пользователей и групп, назначенных» «tooan приложения в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4800-113">In hello context of automatic user account provisioning, only hello users and groups that have been "assigned" tooan application in Azure AD is synchronized.</span></span> 

<span data-ttu-id="f4800-114">Для настройки и включения hello подготовки службы, требуется toodecide какие пользователи или группы в Azure AD представляют Привет пользователям требуется доступ к приложению ThousandEyes tooyour.</span><span class="sxs-lookup"><span data-stu-id="f4800-114">Before configuring and enabling hello provisioning service, you need toodecide what users and/or groups in Azure AD represent hello users who need access tooyour ThousandEyes app.</span></span> <span data-ttu-id="f4800-115">После приняла решение, можно назначить эти приложения ThousandEyes tooyour пользователей в соответствии с инструкциями hello здесь:</span><span class="sxs-lookup"><span data-stu-id="f4800-115">Once decided, you can assign these users tooyour ThousandEyes app by following hello instructions here:</span></span>

[<span data-ttu-id="f4800-116">Назначить пользователю или группе tooan корпоративного приложения</span><span class="sxs-lookup"><span data-stu-id="f4800-116">Assign a user or group tooan enterprise app</span></span>](active-directory-coreapps-assign-user-azure-portal.md)

### <a name="important-tips-for-assigning-users-toothousandeyes"></a><span data-ttu-id="f4800-117">Важные советы для назначения пользователей tooThousandEyes</span><span class="sxs-lookup"><span data-stu-id="f4800-117">Important tips for assigning users tooThousandEyes</span></span>

*   <span data-ttu-id="f4800-118">Рекомендуется один назначенный hello tootest tooThousandEyes настройки подготовки пользователя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4800-118">It is recommended that a single Azure AD user is assigned tooThousandEyes tootest hello provisioning configuration.</span></span> <span data-ttu-id="f4800-119">Дополнительные пользователи и/или группы можно назначить позднее.</span><span class="sxs-lookup"><span data-stu-id="f4800-119">Additional users and/or groups may be assigned later.</span></span>

*   <span data-ttu-id="f4800-120">При назначении tooThousandEyes пользователя, необходимо выбрать либо hello **пользователя** роли или другой допустимый конкретного приложения (если доступно) в диалоговом окне приветствия назначения.</span><span class="sxs-lookup"><span data-stu-id="f4800-120">When assigning a user tooThousandEyes, you must select either hello **User** role, or another valid application-specific role (if available) in hello assignment dialog.</span></span> <span data-ttu-id="f4800-121">Hello **доступа по умолчанию** роль не будет работать для подготовки, и эти пользователи будут пропускаться.</span><span class="sxs-lookup"><span data-stu-id="f4800-121">hello **Default Access** role does not work for provisioning, and these users are skipped.</span></span>


## <a name="configuring-user-provisioning-toothousandeyes"></a><span data-ttu-id="f4800-122">Настройка подготовки tooThousandEyes пользователей</span><span class="sxs-lookup"><span data-stu-id="f4800-122">Configuring user provisioning tooThousandEyes</span></span> 

<span data-ttu-id="f4800-123">Этот раздел поможет выполнить подключение учетной записи пользователя в Azure AD tooThousandEyes подготовки API и настройке подготовки службы toocreate hello, обновления и отключить учетные записи пользователей, назначенные в зависимости от назначения пользователей и групп в ThousandEyes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4800-123">This section guides you through connecting your Azure AD tooThousandEyes's user account provisioning API, and configuring hello provisioning service toocreate, update, and disable assigned user accounts in ThousandEyes based on user and group assignment in Azure AD.</span></span>

> [!TIP]
> <span data-ttu-id="f4800-124">Можно также выбрать tooenabled на основе SAML Single Sign-On для ThousandEyes, следуя инструкциям hello в [портал Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="f4800-124">You may also choose tooenabled SAML-based Single Sign-On for ThousandEyes, following hello instructions provided in [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="f4800-125">Единый вход можно настроить независимо от автоматической подготовки, хотя эти две возможности дополняют друг друга.</span><span class="sxs-lookup"><span data-stu-id="f4800-125">Single sign-on can be configured independently of automatic provisioning, though these two features compliment each other.</span></span>


### <a name="configure-automatic-user-account-provisioning-toothousandeyes-in-azure-ad"></a><span data-ttu-id="f4800-126">Настройка учетной записи автоматического пользователя подготовки tooThousandEyes в Azure AD</span><span class="sxs-lookup"><span data-stu-id="f4800-126">Configure automatic user account provisioning tooThousandEyes in Azure AD</span></span>


1. <span data-ttu-id="f4800-127">В hello [портал Azure](https://portal.azure.com), Обзор toohello **Azure Active Directory > корпоративных приложений > все приложения** раздела.</span><span class="sxs-lookup"><span data-stu-id="f4800-127">In hello [Azure portal](https://portal.azure.com), browse toohello **Azure Active Directory > Enterprise Apps > All applications**  section.</span></span>

2. <span data-ttu-id="f4800-128">Если вы уже настроили ThousandEyes для единого входа, поиск экземпляра ThousandEyes, с помощью поля поиска hello.</span><span class="sxs-lookup"><span data-stu-id="f4800-128">If you have already configured ThousandEyes for single sign-on, search for your instance of ThousandEyes using hello search field.</span></span> <span data-ttu-id="f4800-129">В противном случае выберите **добавить** и выполните поиск **ThousandEyes** в галерее приложения hello.</span><span class="sxs-lookup"><span data-stu-id="f4800-129">Otherwise, select **Add** and search for **ThousandEyes** in hello application gallery.</span></span> <span data-ttu-id="f4800-130">Выберите ThousandEyes из результатов поиска hello и добавить его в список tooyour приложений.</span><span class="sxs-lookup"><span data-stu-id="f4800-130">Select ThousandEyes from hello search results, and add it tooyour list of applications.</span></span>

3. <span data-ttu-id="f4800-131">Выберите свой экземпляр ThousandEyes, а затем выберите hello **Provisioning** вкладки.</span><span class="sxs-lookup"><span data-stu-id="f4800-131">Select your instance of ThousandEyes, then select hello **Provisioning** tab.</span></span>

4. <span data-ttu-id="f4800-132">Набор hello **режим подготовки** слишком**автоматического**.</span><span class="sxs-lookup"><span data-stu-id="f4800-132">Set hello **Provisioning Mode** too**Automatic**.</span></span>

    ![Подготовка ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes1.png)

5. <span data-ttu-id="f4800-134">В разделе hello **учетные данные администратора** раздел, входной hello **секрет маркера** созданные вашей ThousandEyes учетной записи (hello токен можно найти под учетной записью ThousandEyes: **безопасности & Проверка подлинности**).</span><span class="sxs-lookup"><span data-stu-id="f4800-134">Under hello **Admin Credentials** section, input hello **Secret Token** generated by your ThousandEyes's account (you can find hello token under your ThousandEyes account: **Security & Authentication**).</span></span> 

    ![Подготовка ThousandEyes](./media/active-directory-saas-thousandeyes-provisioning-tutorial/ThousandEyes2.png)

6. <span data-ttu-id="f4800-136">В hello портал Azure, щелкните **проверить подключение** tooensure Azure AD можно подключить приложение ThousandEyes tooyour.</span><span class="sxs-lookup"><span data-stu-id="f4800-136">In hello Azure portal, click **Test Connection** tooensure Azure AD can connect tooyour ThousandEyes app.</span></span> <span data-ttu-id="f4800-137">При сбое подключения hello, убедитесь, что ваша учетная запись ThousandEyes имеет разрешения администратора и повторите шаг 5.</span><span class="sxs-lookup"><span data-stu-id="f4800-137">If hello connection fails, ensure your ThousandEyes account has Admin permissions and try step 5 again.</span></span>

7. <span data-ttu-id="f4800-138">Введите адрес электронной почты hello пользователя или группы, которые должны получить уведомления о подготовке ошибки в hello **уведомление по электронной почте** поле и проверьте hello флажок «Отправить уведомление по электронной почте при возникновении сбоя».</span><span class="sxs-lookup"><span data-stu-id="f4800-138">Enter hello email address of a person or group who should receive provisioning error notifications in hello **Notification Email** field, and check hello checkbox "Send an email notification when a failure occurs."</span></span>

8. <span data-ttu-id="f4800-139">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f4800-139">Click **Save**.</span></span> 

9. <span data-ttu-id="f4800-140">Установите hello сопоставлений **tooThousandEyes синхронизации Azure Active Directory — пользователи**.</span><span class="sxs-lookup"><span data-stu-id="f4800-140">Under hello Mappings section, select **Synchronize Azure Active Directory Users tooThousandEyes**.</span></span>

10. <span data-ttu-id="f4800-141">В hello **сопоставления атрибутов** просмотрите hello атрибутов пользователей, которые синхронизируются из tooThousandEyes Azure AD.</span><span class="sxs-lookup"><span data-stu-id="f4800-141">In hello **Attribute Mappings** section, review hello user attributes that are synchronized from Azure AD tooThousandEyes.</span></span> <span data-ttu-id="f4800-142">Здравствуйте, атрибуты, выбранные в качестве **сопоставление** свойства, используемые toomatch hello учетных записей пользователей в ThousandEyes для операций обновления.</span><span class="sxs-lookup"><span data-stu-id="f4800-142">hello attributes selected as **Matching** properties are used toomatch hello user accounts in ThousandEyes for update operations.</span></span> <span data-ttu-id="f4800-143">Выберите toocommit кнопку hello сохранить все изменения.</span><span class="sxs-lookup"><span data-stu-id="f4800-143">Select hello Save button toocommit any changes.</span></span>

11. <span data-ttu-id="f4800-144">tooenable hello подготовки службы Azure AD для ThousandEyes, изменение hello **состояние подготовки** слишком**на** в hello **параметры** раздела</span><span class="sxs-lookup"><span data-stu-id="f4800-144">tooenable hello Azure AD provisioning service for ThousandEyes, change hello **Provisioning Status** too**On** in hello **Settings** section</span></span>

12. <span data-ttu-id="f4800-145">Щелкните **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="f4800-145">Click **Save**.</span></span> 

<span data-ttu-id="f4800-146">Эта операция запускает hello первоначальной синхронизации все пользователи и группы, назначенные tooThousandEyes в hello пользователей и группы раздела.</span><span class="sxs-lookup"><span data-stu-id="f4800-146">This operation starts hello initial synchronization of any users and/or groups assigned tooThousandEyes in hello Users and Groups section.</span></span> <span data-ttu-id="f4800-147">Начальная синхронизация Hello принимает tooperform больше времени, чем последующие синхронизации, которые происходят примерно каждые 20 минут при условии, что запущена служба hello.</span><span class="sxs-lookup"><span data-stu-id="f4800-147">hello initial sync takes longer tooperform than subsequent syncs, which occur approximately every 20 minutes as long as hello service is running.</span></span> <span data-ttu-id="f4800-148">Можно использовать hello **сведения о синхронизации** статьи toomonitor хода выполнения и следуйте ссылки tooprovisioning отчеты о действиях, которые описывают все действия, выполняемые hello подготовки службы.</span><span class="sxs-lookup"><span data-stu-id="f4800-148">You can use hello **Synchronization Details** section toomonitor progress and follow links tooprovisioning activity reports, which describe all actions performed by hello provisioning service.</span></span>

<span data-ttu-id="f4800-149">Дополнительные сведения о способ подготовки tooread hello Azure AD использует для входа см. в разделе [отчеты о автоматический подготовки пользователей. учетной записи](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span><span class="sxs-lookup"><span data-stu-id="f4800-149">For more information on how tooread hello Azure AD provisioning logs, see [Reporting on automatic user account provisioning](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-saas-provisioning-reporting).</span></span>


## <a name="additional-resources"></a><span data-ttu-id="f4800-150">Дополнительные ресурсы</span><span class="sxs-lookup"><span data-stu-id="f4800-150">Additional resources</span></span>

* [<span data-ttu-id="f4800-151">Управление подготовкой учетных записей пользователей для корпоративных приложений</span><span class="sxs-lookup"><span data-stu-id="f4800-151">Managing user account provisioning for Enterprise Apps</span></span>](active-directory-enterprise-apps-manage-provisioning.md)
* [<span data-ttu-id="f4800-152">Что такое доступ к приложениям и единый вход с помощью Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="f4800-152">What is application access and single sign-on with Azure Active Directory?</span></span>](active-directory-appssoaccess-whatis.md)

## <a name="next-steps"></a><span data-ttu-id="f4800-153">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4800-153">Next steps</span></span>

* [<span data-ttu-id="f4800-154">Узнайте, каким образом ведет журнал tooreview и получать отчеты о действиях по подготовке</span><span class="sxs-lookup"><span data-stu-id="f4800-154">Learn how tooreview logs and get reports on provisioning activity</span></span>](active-directory-saas-provisioning-reporting.md)
