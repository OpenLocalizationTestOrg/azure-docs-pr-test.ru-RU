---
title: "Использование самостоятельного доступа к приложениям | Документация Майкрософт"
description: "Включите самостоятельный доступ к приложениям, позволяющий пользователям найти свои приложения"
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
ms.openlocfilehash: 08a05a70d976104d4e0a37b0a0dd15042b0212d8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-self-service-application-access"></a><span data-ttu-id="7406d-103">Использование самостоятельного доступа к приложениям</span><span class="sxs-lookup"><span data-stu-id="7406d-103">How to use self-service application access</span></span>

<span data-ttu-id="7406d-104">Прежде чем пользователи смогут самостоятельно находить приложения на панели доступа, необходимо включить **самостоятельный доступ к приложениям**, чтобы пользователи либо искали их сами, либо запрашивали к ним доступ.</span><span class="sxs-lookup"><span data-stu-id="7406d-104">Before your users can self-discover applications from their access panel, you need to enable **Self-service application access** to any applications that you wish to allow users to self-discover and request access to.</span></span>

<span data-ttu-id="7406d-105">Эта функция представляет собой отличный способ сэкономить время и деньги в ИТ-подразделении. Мы настоятельно рекомендуем использовать ее в развертывании современных приложений с помощью Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7406d-105">This feature is a great way for you to save time and money as an IT group, and is highly recommended as part of a modern applications deployment with Azure Active Directory.</span></span>

<span data-ttu-id="7406d-106">Это позволит вам:</span><span class="sxs-lookup"><span data-stu-id="7406d-106">Using this feature, you can:</span></span>

-   <span data-ttu-id="7406d-107">Разрешить пользователям самостоятельно находить приложения на [панели доступа к приложениям](https://myapps.microsoft.com/) без обращения к специалистам ИТ-подразделения.</span><span class="sxs-lookup"><span data-stu-id="7406d-107">Let users self-discover applications from the [Application Access Panel](https://myapps.microsoft.com/) without bothering the IT group.</span></span>

-   <span data-ttu-id="7406d-108">Добавьте этих пользователей к предварительно настроенным группам, чтобы видеть, кто запросил доступ, удалять доступ и управлять назначенными ролями.</span><span class="sxs-lookup"><span data-stu-id="7406d-108">Add those users to a pre-configured group so you can see who has requested access, remove access, and manage the roles assigned to them.</span></span>

-   <span data-ttu-id="7406d-109">При необходимости разрешать корпоративному утверждающему подтверждать запросы на доступ к приложениям без привлечения ИТ-подразделения.</span><span class="sxs-lookup"><span data-stu-id="7406d-109">Optionally allow a business approver to approve application access requests so the IT group doesn’t have to.</span></span>

-   <span data-ttu-id="7406d-110">При необходимости настраивать для не более 10 сотрудников возможность разрешать доступ к этому приложению.</span><span class="sxs-lookup"><span data-stu-id="7406d-110">Optionally configure up to 10 individuals who may approve access to this application.</span></span>

-   <span data-ttu-id="7406d-111">При необходимости разрешать корпоративному утверждающему задавать пароли пользователей для входа в приложение прямо с [панели доступа к приложению](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7406d-111">Optionally allow a business approver to set the passwords those users can use to sign in to the application, right from the business approver’s [Application Access Panel](https://myapps.microsoft.com/).</span></span>

-   <span data-ttu-id="7406d-112">При необходимости автоматически назначать пользователей, находящихся на самообслуживании, роли приложения напрямую.</span><span class="sxs-lookup"><span data-stu-id="7406d-112">Optionally automatically assign self-service assigned users to an application role directly.</span></span>

## <a name="enable-self-service-application-access-to-allow-users-to-find-their-own-applications"></a><span data-ttu-id="7406d-113">Включите самостоятельный доступ к приложениям, позволяющий пользователям найти свои приложения</span><span class="sxs-lookup"><span data-stu-id="7406d-113">Enable self-service application access to allow users to find their own applications</span></span>

<span data-ttu-id="7406d-114">Самостоятельный доступ к приложениям — это отличный способ разрешить пользователям самим находить приложения и при необходимости позволять бизнес-группе утверждать доступ к этим приложениям.</span><span class="sxs-lookup"><span data-stu-id="7406d-114">Self-service application access is a great way to allow users to self-discover applications, optionally allow the business group to approve access to those applications.</span></span> <span data-ttu-id="7406d-115">Вы можете разрешить бизнес-группе управлять учетными данными пользователей для приложений, использующих единый вход по паролю, прямо на панелях доступа.</span><span class="sxs-lookup"><span data-stu-id="7406d-115">You can allow the business group to manage the credentials assigned to those users for Password Single-Sign On Applications right from their access panels.</span></span>

<span data-ttu-id="7406d-116">Чтобы включить для приложения самостоятельный доступ к приложениям, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="7406d-116">To enable self-service application access to an application, follow the steps below:</span></span>

1.  <span data-ttu-id="7406d-117">Откройте [**портал Azure**](https://portal.azure.com/) и войдите в систему как **глобальный администратор**.</span><span class="sxs-lookup"><span data-stu-id="7406d-117">Open the [**Azure Portal**](https://portal.azure.com/) and sign in as a **Global Administrator.**</span></span>

2.  <span data-ttu-id="7406d-118">Откройте **расширение Azure Active Directory**, щелкнув **Больше служб** в нижней части расположенного слева главного меню навигации.</span><span class="sxs-lookup"><span data-stu-id="7406d-118">Open the **Azure Active Directory Extension** by clicking **More services** at the bottom of the main left hand navigation menu.</span></span>

3.  <span data-ttu-id="7406d-119">В поле фильтра поиска введите **Azure Active Directory** и выберите элемент **Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="7406d-119">Type in **“Azure Active Directory**” in the filter search box and select the **Azure Active Directory** item.</span></span>

4.  <span data-ttu-id="7406d-120">В меню навигации Azure Active Directory слева щелкните **Корпоративные приложения**.</span><span class="sxs-lookup"><span data-stu-id="7406d-120">click **Enterprise Applications** from the Azure Active Directory left hand navigation menu.</span></span>

5.  <span data-ttu-id="7406d-121">Щелкните **Все приложения**, чтобы открыть полный список приложений.</span><span class="sxs-lookup"><span data-stu-id="7406d-121">click **All Applications** to view a list of all your applications.</span></span>

  * <span data-ttu-id="7406d-122">Если нужное приложение отсутствует в списке, в верхней части списка **Все приложения** воспользуйтесь элементом управления **Фильтр**, указав в нем для параметра **Показать** значение **Все приложения**.</span><span class="sxs-lookup"><span data-stu-id="7406d-122">If you do not see the application you want show up here, use the **Filter** control at the top of the **All Applications List** and set the **Show** option to **All Applications.**</span></span>

6.  <span data-ttu-id="7406d-123">Выберите из списка приложение, для которого необходимо включить функцию самостоятельного доступа.</span><span class="sxs-lookup"><span data-stu-id="7406d-123">Select the application you want to enable Self-service access to from the list.</span></span>

7.  <span data-ttu-id="7406d-124">После загрузки приложения щелкните **Самообслуживание** в меню навигации слева.</span><span class="sxs-lookup"><span data-stu-id="7406d-124">Once the application loads, click **Self-service** from the application’s left hand navigation menu.</span></span>

8.  <span data-ttu-id="7406d-125">Чтобы включить самостоятельный доступ к приложениям для этого приложения, установите переключатель **Разрешить пользователям запрашивать доступ к этому приложению?** в состояние **Да**.</span><span class="sxs-lookup"><span data-stu-id="7406d-125">To enable Self-service application access for this application, turn the **Allow users to request access to this application?** toggle to **Yes.**</span></span>

9.  <span data-ttu-id="7406d-126">Затем выберите группу, в которую необходимо добавить пользователей, запрашивающих доступ к этому приложению, щелкните селектор рядом с меткой **К какой группе следует добавить назначенных пользователей?** и выберите группу.</span><span class="sxs-lookup"><span data-stu-id="7406d-126">Next, to select the group to which users who request access to this application should be added, click the selector next to the label **To which group should assigned users be added?** and select a group.</span></span>

10. <span data-ttu-id="7406d-127">**Необязательно.** Если вы хотите запрашивать бизнес-утверждение для предоставления пользователям доступа, установите переключатель **Требовать утверждение перед предоставлением доступа к этому приложению?** в состояние **Да**.</span><span class="sxs-lookup"><span data-stu-id="7406d-127">**Optional:** If you wish to require a business approval before users are allowed access, set the **Require approval before granting access to this application?** toggle to **Yes**.</span></span>

11. <span data-ttu-id="7406d-128">**(Необязательно.) В приложениях, использующих единый вход по паролю,** при необходимости можно разрешить бизнес-утверждениям указывать пароли, которые отправляются приложению для утвержденных пользователей. Для этого установите переключатель **Разрешить утверждающим лицам задавать пароли пользователей для этого приложения?** в положение **Да**.</span><span class="sxs-lookup"><span data-stu-id="7406d-128">**Optional: For applications using password single-sign on only,** if you wish to allow those business approvers to specify the passwords that are sent to this application for approved users, set the **Allow approvers to set user’s passwords for this application?** toggle to **Yes**.</span></span>

12. <span data-ttu-id="7406d-129">**Необязательно.** Чтобы указать утверждающие лица, которым разрешено утверждать доступ к этому приложению, щелкните селектор рядом с меткой **Кому разрешено утверждать доступ к этому приложению?** и выберите до 10 отдельных утверждающих лиц.</span><span class="sxs-lookup"><span data-stu-id="7406d-129">**Optional:** To specify the business approvers who are allowed to approve access to this application, click the selector next to the label **Who is allowed to approve access to this application?** to select up to 10 individual business approvers.</span></span>

   * <span data-ttu-id="7406d-130">Группы не поддерживаются.</span><span class="sxs-lookup"><span data-stu-id="7406d-130">Groups are not supported.</span></span>

13. <span data-ttu-id="7406d-131">**Необязательно.** **В приложениях, предоставляющих роли,** при необходимости можно назначить самостоятельно утвержденных пользователей для роли, щелкнув селектор рядом с меткой **Какую роль следует назначить пользователям в этом приложении?** и выбрав нужную роль.</span><span class="sxs-lookup"><span data-stu-id="7406d-131">**Optional:** **For applications which expose roles**, if you wish to assign self-service approved users to a role, click the selector next to the **To which role should users be assigned in this application?** to select the role to which these users should be assigned.</span></span>

14. <span data-ttu-id="7406d-132">Нажмите кнопку **Сохранить** в верхней части колонки, чтобы завершить процедуру.</span><span class="sxs-lookup"><span data-stu-id="7406d-132">Click the **Save** button at the top of the blade to finish.</span></span>

<span data-ttu-id="7406d-133">После завершения настройки самостоятельного доступа к приложению пользователи могут перейти на [панель доступа к приложениям](https://myapps.microsoft.com/) и нажать кнопку **Добавить**, чтобы найти приложения, для которых включен самостоятельный доступ.</span><span class="sxs-lookup"><span data-stu-id="7406d-133">Once you complete Self-service application configuration, users can navigate to their [Application Access Panel](https://myapps.microsoft.com/) and click the **+Add** button to find the apps to which you have enabled Self-service access.</span></span> <span data-ttu-id="7406d-134">Чтобы просмотреть уведомления для бизнес-утверждений, [используйте панель доступа к приложениям](https://myapps.microsoft.com/).</span><span class="sxs-lookup"><span data-stu-id="7406d-134">Business approvers also see a notification in their [Application Access Panel](https://myapps.microsoft.com/).</span></span> <span data-ttu-id="7406d-135">Вы можете получать уведомления по электронной почте, когда пользователь запрашивает доступ к приложению, требующему утверждения.</span><span class="sxs-lookup"><span data-stu-id="7406d-135">You can enable an email notifying them when a user has requested access to an application that requires their approval.</span></span> 

<span data-ttu-id="7406d-136">Эти утверждения поддерживают только отдельные рабочие процессы, то есть если вы зададите несколько утверждающих лиц, отдельное утверждающее лицо может подтвердить доступ к приложению.</span><span class="sxs-lookup"><span data-stu-id="7406d-136">These approvals support single approval workflows only, meaning that if you specify multiple approvers, any single approver may approve access to the application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7406d-137">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="7406d-137">Next steps</span></span>
[<span data-ttu-id="7406d-138">Настройка Azure Active Directory для самостоятельного управления группами</span><span class="sxs-lookup"><span data-stu-id="7406d-138">Setting up Azure Active Directory for self-service group management</span></span>](active-directory-accessmanagement-self-service-group-management.md)
