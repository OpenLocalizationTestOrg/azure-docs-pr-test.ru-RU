---
title: "с помощью доступа к приложению самообслуживания aaaProblem | Документы Microsoft"
description: "Устранение неполадок доступа связанные приложения-службы tooself проблем"
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
ms.reviewer: japere
ms.openlocfilehash: 2487be1df191a4e7fd0bcc0ebbe4ea62fae0fd5d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="problem-using-self-service-application-access"></a><span data-ttu-id="a694b-103">Проблемы при использовании самостоятельного доступа к приложениям</span><span class="sxs-lookup"><span data-stu-id="a694b-103">Problem using self-service application access</span></span>

<span data-ttu-id="a694b-104">Доступ к приложению самообслуживания является хорошим способом tooallow пользователей tooself-обнаружение приложений, при необходимости разрешить hello бизнес группы tooapprove доступ toothose приложений.</span><span class="sxs-lookup"><span data-stu-id="a694b-104">Self-service application access is a great way tooallow users tooself-discover applications, optionally allow hello business group tooapprove access toothose applications.</span></span> <span data-ttu-id="a694b-105">Вы можете разрешить hello бизнес группы toomanage hello учетные данные назначены пользователи toothose для пароля единого входа в приложения непосредственно из своей панели доступа.</span><span class="sxs-lookup"><span data-stu-id="a694b-105">You can allow hello business group toomanage hello credentials assigned toothose users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="a694b-106">Прежде чем пользователи могут самостоятельно обнаруживать приложений из панели доступа, необходимые tooenable **доступа к приложению самообслуживания** обратиться в tooself tooallow пользователей приложений tooany-находить и запрашивать доступ к.</span><span class="sxs-lookup"><span data-stu-id="a694b-106">Before your users can self-discover applications from their access panel, you need tooenable **Self-service application access** tooany applications that you wish tooallow users tooself-discover and request access to.</span></span>

## <a name="general-issues-toocheck-first"></a><span data-ttu-id="a694b-107">Общие проблемы toocheck сначала</span><span class="sxs-lookup"><span data-stu-id="a694b-107">General issues toocheck first</span></span>

-   <span data-ttu-id="a694b-108">Убедитесь, что самостоятельный доступ к приложению настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="a694b-108">Make sure self-service application access is configured correctly.</span></span> <span data-ttu-id="a694b-109">См. в разделе «Как tooconfigure приложению самообслуживания доступ к».</span><span class="sxs-lookup"><span data-stu-id="a694b-109">See “How tooconfigure self-service application access”.</span></span>

-   <span data-ttu-id="a694b-110">Убедитесь, что hello пользователя или группы был включен toorequest доступа к приложению самообслуживания.</span><span class="sxs-lookup"><span data-stu-id="a694b-110">Make sure hello user or group has been enabled toorequest self-service application access.</span></span>

-   <span data-ttu-id="a694b-111">Убедитесь, что hello находится посетитель hello нужное место для доступа к приложению самообслуживания.</span><span class="sxs-lookup"><span data-stu-id="a694b-111">Make sure hello user is visiting hello correct place for self-service application access.</span></span> <span data-ttu-id="a694b-112">Пользователи могут перейти tootheir [панели доступа приложения](https://myapps.microsoft.com/) и нажмите кнопку hello **+ добавить** кнопку toofind hello приложений toowhich включен самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="a694b-112">users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled self-service access.</span></span>

-   <span data-ttu-id="a694b-113">Если доступа к приложению самообслуживания совсем недавно был настроен, повторите toosign и выхода из системы в hello пользовательской панели доступа после нескольких минут toosee Если возникающих изменения hello самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="a694b-113">If self-service application access was just recently configured, try toosign in and out again into hello user’s Access Panel after a few minutes toosee if hello self-service access changes have appeared.</span></span>

## <a name="how-tooconfigure-self-service-application-access"></a><span data-ttu-id="a694b-114">Способ доступа к приложению самообслуживания tooconfigure</span><span class="sxs-lookup"><span data-stu-id="a694b-114">How tooconfigure self-service application access</span></span>

<span data-ttu-id="a694b-115">приложение tooan доступа к приложению самообслуживания tooenable, выполните следующие действия hello</span><span class="sxs-lookup"><span data-stu-id="a694b-115">tooenable self-service application access tooan application, follow hello steps below:</span></span>

1.  <span data-ttu-id="a694b-116">Откройте hello [ **портала Azure** ](https://portal.azure.com/) и войдите как **глобального администратора.**</span><span class="sxs-lookup"><span data-stu-id="a694b-116">Open hello [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="a694b-117">Привет открыть **расширение Active Directory Azure** , щелкнув **дополнительные службы** hello нижней части меню навигации hello основной левой руки.</span><span class="sxs-lookup"><span data-stu-id="a694b-117">Open hello **Azure Active Directory Extension** by clicking **More services** at hello bottom of hello main left hand navigation menu.</span></span>

3.  <span data-ttu-id="a694b-118">Введите в **«Azure Active Directory**» в поле поиска hello фильтр и выберите hello **Azure Active Directory** элемента.</span><span class="sxs-lookup"><span data-stu-id="a694b-118">Type in **“Azure Active Directory**” in hello filter search box and select hello **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="a694b-119">Нажмите кнопку **корпоративных приложений** из Azure Active Directory hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="a694b-119">click **Enterprise Applications** from hello Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="a694b-120">Нажмите кнопку **все приложения** tooview список всех приложений.</span><span class="sxs-lookup"><span data-stu-id="a694b-120">click **All Applications** tooview a list of all your applications.</span></span>

  * <span data-ttu-id="a694b-121">Используйте hello, если нужно показать здесь приложения hello не отображается, **фильтра** управления вверху hello hello **список всех приложений** и набор hello **Показать** параметр слишком **Все приложения.**</span><span class="sxs-lookup"><span data-stu-id="a694b-121">If you do not see hello application you want show up here, use hello **Filter** control at hello top of hello **All Applications List** and set hello **Show** option too**All Applications.**</span></span>

6.  <span data-ttu-id="a694b-122">Выберите приложение hello hello toofrom список будет tooenable самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="a694b-122">Select hello application you want tooenable Self-service access toofrom hello list.</span></span>

7.  <span data-ttu-id="a694b-123">После загрузки приложения hello щелкните **самообслуживания** из приложения hello левого меню навигации.</span><span class="sxs-lookup"><span data-stu-id="a694b-123">Once hello application loads, click **Self-service** from hello application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="a694b-124">tooenable доступа к приложению самообслуживания для этого приложения, включите hello **пользователи приложения toothis toorequest доступ?** переключения слишком**Да.**</span><span class="sxs-lookup"><span data-stu-id="a694b-124">tooenable Self-service application access for this application, turn hello **Allow users toorequest access toothis application?** toggle too**Yes.**</span></span>

9.  <span data-ttu-id="a694b-125">Затем toowhich tooselect hello группы пользователей, запрашивающих доступ toothis приложения должны быть добавлены, нажмите кнопку Далее метка toohello hello селектор **toowhich группы должны быть назначены пользователи будут добавлены?** и выберите группу.</span><span class="sxs-lookup"><span data-stu-id="a694b-125">Next, tooselect hello group toowhich users who request access toothis application should be added, click hello selector next toohello label **toowhich group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="a694b-126">**Необязательно:** желанию toorequire утверждения business до разрешения доступа пользователей, задайте hello **перед предоставлением доступа toothis приложения требуется утверждение?** переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="a694b-126">**Optional:** If you wish toorequire a business approval before users are allowed access, set hello **Require approval before granting access toothis application?** toggle too**Yes**.</span></span>

11. <span data-ttu-id="a694b-127">**Необязательно: для приложений, только с помощью пароля единого входа на** желанию tooallow тех бизнес утверждающих toospecify hello паролей, которые отправляются toothis приложения для утвержденных пользователей, задайте hello **разрешить утверждающим tooset пароль пользователя для этого приложения?**  переключения слишком**Да**.</span><span class="sxs-lookup"><span data-stu-id="a694b-127">**Optional: For applications using password single-sign on only,** if you wish tooallow those business approvers toospecify hello passwords that are sent toothis application for approved users, set hello **Allow approvers tooset user’s passwords for this application?** toggle too**Yes**.</span></span>

12. <span data-ttu-id="a694b-128">**Необязательно:** toospecify hello бизнеса утверждающие разрешены приложение toothis tooapprove access, щелкните надпись Далее toohello hello селектор **разрешениями приложения toothis tooapprove доступ?** tooselect вверх утверждающие too10 отдельных бизнеса.</span><span class="sxs-lookup"><span data-stu-id="a694b-128">**Optional:** toospecify hello business approvers who are allowed tooapprove access toothis application, click hello selector next toohello label **Who is allowed tooapprove access toothis application?** tooselect up too10 individual business approvers.</span></span>

 >[!NOTE]
 > <span data-ttu-id="a694b-129">Группы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="a694b-129">Groups are not supported.</span></span>
 >
 >

13. <span data-ttu-id="a694b-130">**Необязательно:** **для приложений, которые предоставляют роли**, при желании tooassign утвержденные пользователи tooa роли, нажмите кнопку Далее toohello селектор hello **toowhich роль следует назначить пользователей в этом приложения?**  tooselect hello роли toowhich этих пользователей следует назначить.</span><span class="sxs-lookup"><span data-stu-id="a694b-130">**Optional:** **For applications which expose roles**, if you wish tooassign self-service approved users tooa role, click hello selector next toohello **toowhich role should users be assigned in this application?** tooselect hello role toowhich these users should be assigned.</span></span>

14. <span data-ttu-id="a694b-131">Нажмите кнопку hello **Сохранить** кнопку hello верхней части колонки toofinish hello.</span><span class="sxs-lookup"><span data-stu-id="a694b-131">Click hello **Save** button at hello top of hello blade toofinish.</span></span>

<span data-ttu-id="a694b-132">После завершения конфигурации самостоятельного приложения пользователи могут перейти tootheir [панели доступа приложения](https://myapps.microsoft.com/) и нажмите кнопку hello **+ добавить** кнопку toofind hello приложений toowhich включен Самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="a694b-132">Once you complete Self-service application configuration, users can navigate tootheir [Application Access Panel](https://myapps.microsoft.com/) and click hello **+Add** button toofind hello apps toowhich you have enabled Self-service access.</span></span> <span data-ttu-id="a694b-133">Чтобы просмотреть уведомления для бизнес-утверждений, [используйте панель доступа к приложениям](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="a694b-133">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="a694b-134">Вы можете включить электронное сообщение о том, когда пользователь запрашивает доступ tooan приложения, которое требует утверждения.</span><span class="sxs-lookup"><span data-stu-id="a694b-134">You can enable an email notifying them when a user has requested access tooan application that requires their approval.</span></span> 

<span data-ttu-id="a694b-135">Это утверждение поддерживает единичное утверждение рабочих процессов, то есть, если указываются несколько утверждающих лиц, любой один утверждающий могут разрешать доступ toohello приложения.</span><span class="sxs-lookup"><span data-stu-id="a694b-135">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access toohello application.</span></span>

## <a name="if-these-troubleshooting-steps-do-not-resolve-hello-issue"></a><span data-ttu-id="a694b-136">Если эти шаги по устранению неполадок не решат проблему hello</span><span class="sxs-lookup"><span data-stu-id="a694b-136">If these troubleshooting steps do not resolve hello issue</span></span> 

<span data-ttu-id="a694b-137">Откройте запрос в службу поддержки с hello следующую информацию, если они доступны:</span><span class="sxs-lookup"><span data-stu-id="a694b-137">open a support ticket with hello following information if available:</span></span>

-   <span data-ttu-id="a694b-138">идентификатор ошибки корреляции;</span><span class="sxs-lookup"><span data-stu-id="a694b-138">Correlation error ID</span></span>

-   <span data-ttu-id="a694b-139">имя участника-пользователя (адрес электронной почты пользователя);</span><span class="sxs-lookup"><span data-stu-id="a694b-139">UPN (user email address)</span></span>

-   <span data-ttu-id="a694b-140">идентификатор клиента;</span><span class="sxs-lookup"><span data-stu-id="a694b-140">TenantID</span></span>

-   <span data-ttu-id="a694b-141">тип браузера;</span><span class="sxs-lookup"><span data-stu-id="a694b-141">Browser type</span></span>

-   <span data-ttu-id="a694b-142">часовой пояс и время или отрезок времени возникновения ошибки;</span><span class="sxs-lookup"><span data-stu-id="a694b-142">Time zone and time/timeframe during error occurs</span></span>

-   <span data-ttu-id="a694b-143">трассировки Fiddler.</span><span class="sxs-lookup"><span data-stu-id="a694b-143">Fiddler traces</span></span>

## <a name="next-steps"></a><span data-ttu-id="a694b-144">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a694b-144">Next steps</span></span>
[<span data-ttu-id="a694b-145">Настройка Azure Active Directory для самостоятельного управления группами</span><span class="sxs-lookup"><span data-stu-id="a694b-145">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
