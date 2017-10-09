---
title: "назначение приложений самообслуживания tooconfigure aaaHow | Документы Microsoft"
description: "Включить toofind пользователей tooallow доступа к приложению самообслуживания своих приложений"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: d25a0146c4c8cebf9c2ae8c516f094a8eccb4570
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-self-service-application-assignment"></a><span data-ttu-id="3aca0-103">Как назначение tooconfigure самообслуживания приложений</span><span class="sxs-lookup"><span data-stu-id="3aca0-103">How tooconfigure self-service application assignment</span></span>

<span data-ttu-id="3aca0-104">Прежде чем пользователи могут самостоятельно обнаруживать приложений из панели доступа, необходимые tooenable **доступа к приложению самообслуживания** обратиться в tooself tooallow пользователей приложений tooany-находить и запрашивать доступ к.</span><span class="sxs-lookup"><span data-stu-id="3aca0-104">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

<span data-ttu-id="3aca0-105">Эта функция является хорошим способом для вас toosave время и деньги, как ИТ-отдел и настоятельно рекомендуется в качестве части развертывания современных приложений с Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="3aca0-105">This feature is a great way for you toosave time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="3aca0-106">Это позволит вам:</span><span class="sxs-lookup"><span data-stu-id="3aca0-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="3aca0-107">Разрешить пользователям самостоятельно обнаруживать приложения из hello [панели доступа приложений](https://myapps.microsoft.com/) корпорацию hello ИТ группы.</span><span class="sxs-lookup"><span data-stu-id="3aca0-107">Let users self-discover applications from hello [Application Access Panel](https://myapps.microsoft.com/) without bothering hello IT group.</span></span>

-   <span data-ttu-id="3aca0-108">Добавьте этих пользователей tooa предварительно настроенных группу, в разделе, который запросил доступ, удалить доступ и управление ролями hello, назначенный toothem.</span><span class="sxs-lookup"><span data-stu-id="3aca0-108">Add those users tooa pre-configured group so you can see who has requested access, remove access, and manage hello roles assigned toothem.</span></span>

-   <span data-ttu-id="3aca0-109">При необходимости допускает утверждающий business tooapprove запросы на доступ приложения hello ИТ-отдел не нужно.</span><span class="sxs-lookup"><span data-stu-id="3aca0-109">Optionally allow a business approver tooapprove application access requests so hello IT group doesn’t have to.</span></span>

-   <span data-ttu-id="3aca0-110">При необходимости настройте too10 лиц, которые могут разрешать доступ toothis приложения.</span><span class="sxs-lookup"><span data-stu-id="3aca0-110">Optionally configure up too10 individuals who may approve access toothis application.</span></span>

-   <span data-ttu-id="3aca0-111">При необходимости разрешить утверждающего business tooset hello паролей пользователи сети могут использовать в приложении toohello прямо из hello бизнеса утверждающий toosign [панели доступа приложения](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3aca0-111">Optionally allow a business approver tooset hello passwords those users can use toosign in toohello application, right from hello business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="3aca0-112">При необходимости автоматически назначьте роли приложения tooan самообслуживания назначенных пользователей напрямую.</span><span class="sxs-lookup"><span data-stu-id="3aca0-112">Optionally automatically assign self-service assigned users tooan application role directly.</span></span>

## <a name="enable-self-service-application-access-tooallow-users-toofind-their-own-applications"></a><span data-ttu-id="3aca0-113">Включить toofind пользователей tooallow доступа к приложению самообслуживания своих приложений</span><span class="sxs-lookup"><span data-stu-id="3aca0-113">Enable self-service application access tooallow users toofind their own applications</span></span>

<span data-ttu-id="3aca0-114">Доступ к приложению самообслуживания является хорошим способом tooallow пользователей tooself-обнаружение приложений, при необходимости разрешить hello бизнес группы tooapprove доступ toothose приложений.</span><span class="sxs-lookup"><span data-stu-id="3aca0-114">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="3aca0-115">Вы можете разрешить hello бизнес группы toomanage hello учетные данные назначены пользователи toothose для пароля единого входа в приложения непосредственно из своей панели доступа.</span><span class="sxs-lookup"><span data-stu-id="3aca0-115">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="3aca0-116">приложение tooan доступа к приложению самообслуживания tooenable, выполните следующие действия hello</span><span class="sxs-lookup"><span data-stu-id="3aca0-116">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="3aca0-117">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="3aca0-117">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="3aca0-118">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="3aca0-118">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="3aca0-119">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="3aca0-119">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="3aca0-120">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3aca0-120">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="3aca0-121">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="3aca0-121">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="3aca0-122">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="3aca0-122">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="3aca0-123">Выберите приложение hello hello toofrom список будет tooenable самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="3aca0-123">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="3aca0-124">После загрузки приложения hello щелкните **самообслуживания** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="3aca0-124">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="3aca0-125">tooenable доступа к приложению самообслуживания для этого приложения, включите hello **пользователи приложения toothis toorequest доступ?** переключения слишком**Да.**</span><span class="sxs-lookup"><span data-stu-id="3aca0-125">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="3aca0-126">Затем toowhich tooselect hello группы пользователей, запрашивающих доступ toothis приложения должны быть добавлены, нажмите кнопку Далее метка toohello hello селектор **toowhich группы должны быть назначены пользователи будут добавлены?** и выберите группу.</span><span class="sxs-lookup"><span data-stu-id="3aca0-126">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="3aca0-127">**Необязательно:** желанию toorequire утверждения business до разрешения доступа пользователей, задайте hello **перед предоставлением доступа toothis приложения требуется утверждение?** переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="3aca0-127">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="3aca0-128">**Необязательно: для приложений, только с помощью пароля единого входа на** желанию tooallow тех бизнес утверждающих toospecify hello паролей, которые отправляются toothis приложения для утвержденных пользователей, задайте hello **разрешить утверждающим tooset пароль пользователя для этого приложения?**  переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="3aca0-128">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="3aca0-129">**Необязательно:** toospecify hello бизнеса утверждающие разрешены приложение toothis tooapprove access, щелкните надпись Далее toohello hello селектор **разрешениями приложения toothis tooapprove доступ?** tooselect вверх утверждающие too10 отдельных бизнеса.</span><span class="sxs-lookup"><span data-stu-id="3aca0-129">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

   >[!NOTE]
   ><span data-ttu-id="3aca0-130">Группы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="3aca0-130">Groups are not supported.</span></span>
   >
   >

13. <span data-ttu-id="3aca0-131">**Необязательно:** **для приложений, которые предоставляют роли**, при желании tooassign утвержденные пользователи tooa роли, нажмите кнопку Далее toohello селектор hello **toowhich роль следует назначить пользователей в этом приложения?**  tooselect hello роли toowhich этих пользователей следует назначить.</span><span class="sxs-lookup"><span data-stu-id="3aca0-131">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="3aca0-132">Нажмите кнопку hello **Сохранить** кнопку hello верхней части колонки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="3aca0-132">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="3aca0-133">После завершения конфигурации самостоятельного приложения пользователи могут перейти tootheir [панели доступа приложения](https://myapps.microsoft.com/) и нажмите кнопку hello **+ добавить** кнопку toofind hello приложений toowhich включен Самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="3aca0-133">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="3aca0-134">Чтобы просмотреть уведомления для бизнес-утверждений, [используйте панель доступа к приложениям](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="3aca0-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="3aca0-135">Вы можете включить электронное сообщение о том, когда пользователь запрашивает доступ tooan приложения, которое требует утверждения.</span><span class="sxs-lookup"><span data-stu-id="3aca0-135">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="3aca0-136">Это утверждение поддерживает один бизнес-правила утверждения, то есть, если указать несколько утверждающих лиц любой один утверждающий может утверждающий доступа toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="3aca0-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approver access toohello application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3aca0-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="3aca0-137">Next steps</span></span>
[<span data-ttu-id="3aca0-138">Настройка Azure Active Directory для самостоятельного управления группами</span><span class="sxs-lookup"><span data-stu-id="3aca0-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
