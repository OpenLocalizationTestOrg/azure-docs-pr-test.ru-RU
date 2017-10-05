---
title: "Azure AD Connect: дальнейшие действия и управление Azure AD Connect | Документация Майкрософт"
description: "Узнайте, как расширить конфигурацию по умолчанию и операционные задачи для Azure AD Connect."
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
ms.openlocfilehash: beace24fa00c85a5038a3c39ae8f76af5fd12111
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="next-steps-and-how-to-manage-azure-ad-connect"></a><span data-ttu-id="0084d-103">Дальнейшие действия и управление Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0084d-103">Next steps and how to manage Azure AD Connect</span></span>
<span data-ttu-id="0084d-104">Используйте рабочие процедуры, приведенные в этой статье, для настройки Azure Active Directory (Azure AD) Connect в соответствии с потребностями вашей организации.</span><span class="sxs-lookup"><span data-stu-id="0084d-104">Use the operational procedures in this article to customize Azure Active Directory (Azure AD) Connect to meet your organization's needs and requirements.</span></span>  

## <a name="add-additional-sync-admins"></a><span data-ttu-id="0084d-105">Добавление дополнительных администраторов синхронизации</span><span class="sxs-lookup"><span data-stu-id="0084d-105">Add additional sync admins</span></span>
<span data-ttu-id="0084d-106">По умолчанию только пользователь, выполнивший установку, и локальные администраторы могут управлять установленным модулем синхронизации.</span><span class="sxs-lookup"><span data-stu-id="0084d-106">By default, only the user who did the installation and local admins are able to manage the installed sync engine.</span></span> <span data-ttu-id="0084d-107">Чтобы предоставить дополнительным пользователям доступ к модулю синхронизации и возможность управлять им, найдите группу ADSyncAdmins на локальном сервере и добавьте их в эту группу.</span><span class="sxs-lookup"><span data-stu-id="0084d-107">For additional people to be able to access and manage the sync engine, locate the group named ADSyncAdmins on the local server and add them to this group.</span></span>

## <a name="assign-licenses-to-azure-ad-premium-and-enterprise-mobility-suite-users"></a><span data-ttu-id="0084d-108">Назначение пользователям лицензий Azure AD Premium и Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="0084d-108">Assign licenses to Azure AD Premium and Enterprise Mobility Suite users</span></span>
<span data-ttu-id="0084d-109">После синхронизации данных о пользователях с облаком необходимо назначить им лицензию, чтобы они могли приступить к работе с облачными приложениями, такими как Office 365.</span><span class="sxs-lookup"><span data-stu-id="0084d-109">Now that your users have been synchronized to the cloud, you need to assign them a license so they can get going with cloud apps such as Office 365.</span></span>

### <a name="to-assign-an-azure-ad-premium-or-enterprise-mobility-suite-license"></a><span data-ttu-id="0084d-110">Назначение лицензии Azure AD Premium или Enterprise Mobility Suite</span><span class="sxs-lookup"><span data-stu-id="0084d-110">To assign an Azure AD Premium or Enterprise Mobility Suite License</span></span>

1. <span data-ttu-id="0084d-111">Войдите на портал Azure с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="0084d-111">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="0084d-112">Выберите **Active Directory**слева.</span><span class="sxs-lookup"><span data-stu-id="0084d-112">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0084d-113">На странице **Active Directory** дважды щелкните каталог с пользователями для настройки.</span><span class="sxs-lookup"><span data-stu-id="0084d-113">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="0084d-114">В верхней части страницы каталога выберите **Лицензии**.</span><span class="sxs-lookup"><span data-stu-id="0084d-114">At the top of the directory page, select **Licenses**.</span></span>
5. <span data-ttu-id="0084d-115">На странице **Лицензии** выберите **Active Directory Premium** или **Enterprise Mobility Suite**, а затем щелкните **Назначить**.</span><span class="sxs-lookup"><span data-stu-id="0084d-115">On the **Licenses** page, select **Active Directory Premium** or **Enterprise Mobility Suite**, and then click **Assign**.</span></span>
6. <span data-ttu-id="0084d-116">В диалоговом окне выберите пользователей, которым требуется назначить лицензии, и щелкните значок галочки, чтобы сохранить изменения.</span><span class="sxs-lookup"><span data-stu-id="0084d-116">In the dialog box, select the users you want to assign licenses to, and then click the check mark icon to save the changes.</span></span>

## <a name="verify-the-scheduled-synchronization-task"></a><span data-ttu-id="0084d-117">Проверка выполнения запланированной задачи синхронизации</span><span class="sxs-lookup"><span data-stu-id="0084d-117">Verify the scheduled synchronization task</span></span>
<span data-ttu-id="0084d-118">Используйте портал Azure, чтобы проверить состояние синхронизации.</span><span class="sxs-lookup"><span data-stu-id="0084d-118">Use the Azure portal to check the status of a synchronization.</span></span>

### <a name="to-verify-the-scheduled-synchronization-task"></a><span data-ttu-id="0084d-119">Чтобы проверить выполнение запланированной задачи синхронизации:</span><span class="sxs-lookup"><span data-stu-id="0084d-119">To verify the scheduled synchronization task</span></span>
1. <span data-ttu-id="0084d-120">Войдите на портал Azure с учетной записью администратора.</span><span class="sxs-lookup"><span data-stu-id="0084d-120">Sign in to the Azure portal as an admin.</span></span>
2. <span data-ttu-id="0084d-121">Выберите **Active Directory**слева.</span><span class="sxs-lookup"><span data-stu-id="0084d-121">On the left, select **Active Directory**.</span></span>
3. <span data-ttu-id="0084d-122">На странице **Active Directory** дважды щелкните каталог с пользователями для настройки.</span><span class="sxs-lookup"><span data-stu-id="0084d-122">On the **Active Directory** page, double-click the directory that has the users you want to set up.</span></span>
4. <span data-ttu-id="0084d-123">В верхней части страницы каталога выберите вкладку **Интеграция каталогов**.</span><span class="sxs-lookup"><span data-stu-id="0084d-123">At the top of the directory page, select **Directory Integration**.</span></span>
5. <span data-ttu-id="0084d-124">В разделе **integration with local active directory** (Интеграция с активным локальным каталогом Active Directory) просмотрите время последней синхронизации.</span><span class="sxs-lookup"><span data-stu-id="0084d-124">Under **integration with local active directory**, note the last sync time.</span></span>

<span data-ttu-id="0084d-125"><center>![Время синхронизации каталога](./media/active-directory-aadconnect-whats-next/verify.png)</center></span><span class="sxs-lookup"><span data-stu-id="0084d-125"><center>![Directory sync time](./media/active-directory-aadconnect-whats-next/verify.png)</center></span></span>

## <a name="start-a-scheduled-synchronization-task"></a><span data-ttu-id="0084d-126">Запуск запланированной задачи синхронизации</span><span class="sxs-lookup"><span data-stu-id="0084d-126">Start a scheduled synchronization task</span></span>
<span data-ttu-id="0084d-127">Чтобы выполнить задачу синхронизации, можно снова запустить мастер Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0084d-127">If you need to run a synchronization task, you can do this by running through the Azure AD Connect wizard again.</span></span>  <span data-ttu-id="0084d-128">Для этого требуется указать учетные данные Azure AD.</span><span class="sxs-lookup"><span data-stu-id="0084d-128">You need to provide your Azure AD credentials.</span></span>  <span data-ttu-id="0084d-129">В мастере выберите задачу **Настроить параметры синхронизации** и нажмите кнопку **Далее** для перехода к следующим страницам мастера.</span><span class="sxs-lookup"><span data-stu-id="0084d-129">In the wizard, select the **Customize synchronization options** task, and click **Next** to move through the wizard.</span></span> <span data-ttu-id="0084d-130">Убедитесь, что на последней странице установлен флажок **Запустить синхронизацию сразу после завершения начальной настройки**.</span><span class="sxs-lookup"><span data-stu-id="0084d-130">At the end, ensure that the **Start the synchronization process as soon as the initial configuration completes** box is selected.</span></span>

<span data-ttu-id="0084d-131"><center>![Запуск синхронизации](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span><span class="sxs-lookup"><span data-stu-id="0084d-131"><center>![Start synchronization](./media/active-directory-aadconnect-whats-next/startsynch.png)</center></span></span>

<span data-ttu-id="0084d-132">Дополнительные сведения о планировщике синхронизации Azure AD Connect см. в статье [Синхронизация Azure AD Connect: планировщик](active-directory-aadconnectsync-feature-scheduler.md).</span><span class="sxs-lookup"><span data-stu-id="0084d-132">For more information on the Azure AD Connect sync Scheduler, see [Azure AD Connect Scheduler](active-directory-aadconnectsync-feature-scheduler.md).</span></span>

## <a name="additional-tasks-available-in-azure-ad-connect"></a><span data-ttu-id="0084d-133">Дополнительные задачи в Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="0084d-133">Additional tasks available in Azure AD Connect</span></span>
<span data-ttu-id="0084d-134">После установки Azure AD Connect вы можете повторно запускать мастер с начальной страницы Azure AD Connect или используя ярлык на рабочем столе.</span><span class="sxs-lookup"><span data-stu-id="0084d-134">After your initial installation of Azure AD Connect, you can always start the wizard again from the Azure AD Connect start page or desktop shortcut.</span></span>  <span data-ttu-id="0084d-135">При повторном запуске мастера будут доступны дополнительные задачи.</span><span class="sxs-lookup"><span data-stu-id="0084d-135">You will notice that going through the wizard again provides some new options in the form of additional tasks.</span></span>  

<span data-ttu-id="0084d-136">Список задач и их краткое описание см. в следующей таблице.</span><span class="sxs-lookup"><span data-stu-id="0084d-136">The following table provides a summary of these tasks and a brief description of each task.</span></span>

![Список дополнительных задач](./media/active-directory-aadconnect-whats-next/addtasks.png)

| <span data-ttu-id="0084d-138">Дополнительная задача</span><span class="sxs-lookup"><span data-stu-id="0084d-138">Additional task</span></span> | <span data-ttu-id="0084d-139">Описание</span><span class="sxs-lookup"><span data-stu-id="0084d-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0084d-140">**Просмотреть выбранный сценарий**</span><span class="sxs-lookup"><span data-stu-id="0084d-140">**View the selected scenario**</span></span> |<span data-ttu-id="0084d-141">Просмотр текущего решения Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="0084d-141">View your current Azure AD Connect solution.</span></span>  <span data-ttu-id="0084d-142">Включает общие параметры, синхронизированные каталоги и параметры синхронизации.</span><span class="sxs-lookup"><span data-stu-id="0084d-142">This includes general settings, synchronized directories, and sync settings.</span></span> |
| <span data-ttu-id="0084d-143">**Настроить параметры синхронизации**</span><span class="sxs-lookup"><span data-stu-id="0084d-143">**Customize synchronization options**</span></span> |<span data-ttu-id="0084d-144">Изменение текущей конфигурации, например добавление в нее дополнительных лесов Active Directory или активация параметров синхронизации, таких как обратная запись для пользователей, групп, устройств или паролей.</span><span class="sxs-lookup"><span data-stu-id="0084d-144">Change the current configuration like adding additional Active Directory forests to the configuration, or enabling sync options such as user, group, device, or password write-back.</span></span> |
| <span data-ttu-id="0084d-145">**Включить промежуточный режим**</span><span class="sxs-lookup"><span data-stu-id="0084d-145">**Enable Staging Mode**</span></span> |<span data-ttu-id="0084d-146">Промежуточные сведения, которые сразу не синхронизируются и не экспортируются в Azure AD или локальной каталог Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0084d-146">Stage information that is not immediately synchronized and is not exported to Azure AD or on-premises Active Directory.</span></span>  <span data-ttu-id="0084d-147">Эта функция позволяет просмотреть результаты синхронизации до ее выполнения.</span><span class="sxs-lookup"><span data-stu-id="0084d-147">With this feature, you can preview the synchronizations before they occur.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="0084d-148">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="0084d-148">Next steps</span></span>
<span data-ttu-id="0084d-149">Дополнительные сведения об интеграции локальных удостоверений см. в статье [Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="0084d-149">Learn more about [integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
