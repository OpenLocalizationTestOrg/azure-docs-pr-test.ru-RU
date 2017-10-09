---
title: "Azure AD Connect: Дальнейшие действия и каким образом Azure AD Connect toomanage | Документы Microsoft"
description: "Узнайте, как tooextend hello задачи и конфигурация по умолчанию для Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
editor: curtand
ms.assetid: c18bee36-aebf-4281-b8fc-3fe14116f1a5
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 4404aaff24d54d76b83baca3b331a6a250ba4c03
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="next-steps-and-how-toomanage-azure-ad-connect"></a><span data-ttu-id="10301-103">Дальнейшие действия и как toomanage Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="10301-103">Next steps and how toomanage Azure AD Connect</span></span>
<span data-ttu-id="10301-104">Используйте hello операционные процедуры в этой статье toocustomize подключение Azure Active Directory (Azure AD) toomeet требованиями и требованиями к вашей организации.</span><span class="sxs-lookup"><span data-stu-id="10301-104">Use hello operational procedures in this article toocustomize Azure Active Directory (Azure AD) Connect toomeet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="10301-105">Добавление дополнительных администраторов синхронизации</span><span class="sxs-lookup"><span data-stu-id="10301-105">Add additional sync admins</span></span>
<span data-ttu-id="10301-106">По умолчанию только hello этот пользователь hello установки и локальных администраторов, модуль синхронизации может toomanage hello установлен.</span><span class="sxs-lookup"><span data-stu-id="10301-106">By default, only hello user who did hello installation and local admins are able toomanage hello installed sync engine.</span></span> <span data-ttu-id="10301-107">Для возможности tooaccess toobe другим пользователям и управлять подсистема синхронизации hello, hello группы с именем ADSyncAdmins на локальном сервере hello и добавьте их toothis группы.</span><span class="sxs-lookup"><span data-stu-id="10301-107">For additional people toobe able tooaccess and manage hello sync engine, locate hello group named ADSyncAdmins on hello local server and add them toothis group.</span></span>

## <a name="assign-licenses-tooazure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="10301-108">Назначить лицензии tooAzure пользователей AD Premium и Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="10301-108">Assign licenses tooAzure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="10301-109">Теперь, когда пользователи были синхронизированы облака toohello необходимо tooassign их лицензии, поэтому они могут начать работу с облачных приложений, таких как Office 365.</span><span class="sxs-lookup"><span data-stu-id="10301-109">Now that your users have been synchronized toohello cloud, you need tooassign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="tooassign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="10301-110">tooassign Azure AD Premium или Enterprise Mobility Suite лицензии</span><span class="sxs-lookup"><span data-stu-id="10301-110">tooassign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="10301-111">Войдите в toohello портал Azure от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="10301-111">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="10301-112">В левой части экрана приветствия выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10301-112">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="10301-113">На hello **Active Directory** дважды щелкните каталог hello hello пользователей необходимо tooset.</span><span class="sxs-lookup"><span data-stu-id="10301-113">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="10301-114">В начале hello hello каталог страницы, выберите **лицензий**.</span><span class="sxs-lookup"><span data-stu-id="10301-114">At hello top of hello directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="10301-115">На hello **лицензий** выберите **Active Directory Premium** или **Enterprise Mobility Suite**, а затем нажмите кнопку **назначить**.</span><span class="sxs-lookup"><span data-stu-id="10301-115">On hello **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="10301-116">В диалоговом окне приветствия выберите пользователей hello tooassign лицензии и нажмите кнопку hello флажок значок toosave hello изменения.</span><span class="sxs-lookup"><span data-stu-id="10301-116">In hello dialog box, select hello users you want tooassign licenses to, and then click hello check mark icon toosave hello changes.</span></span>

## <a name="verify-hello-scheduled-synchronization-task"></a><span data-ttu-id="10301-117">Проверить синхронизацию по расписанию задачу hello</span><span class="sxs-lookup"><span data-stu-id="10301-117">Verify hello scheduled synchronization task</span></span>
<span data-ttu-id="10301-118">Использование hello Azure портала toocheck hello состояния процесса синхронизации.</span><span class="sxs-lookup"><span data-stu-id="10301-118">Use hello Azure portal toocheck hello status of a synchronization.</span></span>

### <a name="tooverify-hello-scheduled-synchronization-task"></a><span data-ttu-id="10301-119">tooverify hello запланированная задача синхронизации</span><span class="sxs-lookup"><span data-stu-id="10301-119">tooverify hello scheduled synchronization task</span></span>
1. <span data-ttu-id="10301-120">Войдите в toohello портал Azure от имени администратора.</span><span class="sxs-lookup"><span data-stu-id="10301-120">Sign in toohello Azure portal as an admin.</span></span>
2. <span data-ttu-id="10301-121">В левой части экрана приветствия выберите **Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="10301-121">On hello left, select **Active Directory**.</span></span>
3. <span data-ttu-id="10301-122">На hello **Active Directory** дважды щелкните каталог hello hello пользователей необходимо tooset.</span><span class="sxs-lookup"><span data-stu-id="10301-122">On hello **Active Directory** page, double-click hello directory that has hello users you want tooset up.</span></span>
4. <span data-ttu-id="10301-123">В начале hello hello каталог страницы, выберите **Интеграция каталогов**.</span><span class="sxs-lookup"><span data-stu-id="10301-123">At hello top of hello directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="10301-124">В разделе **интеграции с локальной службой active directory**, Примечание hello время последней синхронизации.</span><span class="sxs-lookup"><span data-stu-id="10301-124">Under **integration with local active directory**, note hello last sync time.</span></span>

<span data-ttu-id="10301-125"><center>![Время синхронизации каталога](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="10301-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="10301-126">Запуск запланированной задачи синхронизации</span><span class="sxs-lookup"><span data-stu-id="10301-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="10301-127">Если вам требуется toorun задачу синхронизации, это можно сделать путем повторного запуска мастера Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="10301-127">If you need toorun a synchronization task, you can do this by running through hello Azure AD Connect wizard again.</span></span>  <span data-ttu-id="10301-128">Необходимо tooprovide учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="10301-128">You need tooprovide your Azure AD credentials.</span></span>  <span data-ttu-id="10301-129">В мастере приветствия выберите hello **настроить параметры синхронизации** задач и нажмите кнопку **Далее** toomove мастером hello.</span><span class="sxs-lookup"><span data-stu-id="10301-129">In hello wizard, select hello **Customize synchronization options** task, and click **Next** toomove through hello wizard.</span></span> <span data-ttu-id="10301-130">В конце hello, убедитесь, что hello **запуск процесса синхронизации hello сразу же после завершения начальной настройки hello** флажок.</span><span class="sxs-lookup"><span data-stu-id="10301-130">At hello end, ensure that hello **Start hello synchronization process as soon as hello initial configuration completes** box is selected.</span></span>

<span data-ttu-id="10301-131"><center>![Запуск синхронизации](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="10301-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="10301-132">Дополнительные сведения о синхронизации hello Azure AD Connect планировщика см. в разделе [планировщик подключения Azure AD](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="10301-132">For more information on hello Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="10301-133">Дополнительные задачи в Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="10301-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="10301-134">После первоначальной установки Azure AD Connect всегда мастер можно запустить hello снова из hello Azure AD Connect Пуск страницы или рабочего стола с помощью ярлыка.</span><span class="sxs-lookup"><span data-stu-id="10301-134">After your initial installation of Azure AD Connect, you can always start hello wizard again from hello Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="10301-135">Обратите внимание, что снова перейти в мастере hello предоставляет некоторые новые параметры в форме hello дополнительные задачи.</span><span class="sxs-lookup"><span data-stu-id="10301-135">You will notice that going through hello wizard again provides some new options in hello form of additional tasks.</span></span>  

<span data-ttu-id="10301-136">Hello ниже приводится сводка этих задач и краткое описание каждой задачи.</span><span class="sxs-lookup"><span data-stu-id="10301-136">hello following table provides a summary of these tasks and a brief description of each task.</span></span>

![Список дополнительных задач](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="10301-138">Дополнительная задача</span><span class="sxs-lookup"><span data-stu-id="10301-138">Additional task</span></span> | <span data-ttu-id="10301-139">Описание</span><span class="sxs-lookup"><span data-stu-id="10301-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="10301-140">**Представление hello выбранного сценария**</span><span class="sxs-lookup"><span data-stu-id="10301-140">**View hello selected scenario**</span></span> |<span data-ttu-id="10301-141">Просмотр текущего решения Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="10301-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="10301-142">Включает общие параметры, синхронизированные каталоги и параметры синхронизации.</span><span class="sxs-lookup"><span data-stu-id="10301-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="10301-143">**Настроить параметры синхронизации**</span><span class="sxs-lookup"><span data-stu-id="10301-143">**Customize synchronization options**</span></span> |<span data-ttu-id="10301-144">Изменить текущую конфигурацию hello как добавление дополнительная настройка toohello лесов Active Directory или включение параметров синхронизации, например пользователь, группа, устройства или обратная запись пароля.</span><span class="sxs-lookup"><span data-stu-id="10301-144">Change hello current configuration like adding additional Active Directory forests toohello configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="10301-145">**Включить промежуточный режим**</span><span class="sxs-lookup"><span data-stu-id="10301-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="10301-146">Сведения о рабочей области, не синхронизирована немедленно и не экспортируются tooAzure AD или локальной Active Directory.</span><span class="sxs-lookup"><span data-stu-id="10301-146">Stage information that is not immediately synchronized and is not exported tooAzure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="10301-147">С помощью этой функции можно просмотреть синхронизаций hello прежде, чем они возникнут.</span><span class="sxs-lookup"><span data-stu-id="10301-147">With this feature, you can preview hello synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="10301-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="10301-148">Next steps</span></span>
<span data-ttu-id="10301-149">Дополнительные сведения об интеграции локальных удостоверений см. в статье [Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="10301-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
