---
title: "Повторным запуском мастера установки hello Azure AD Connect | Документы Microsoft"
description: "Объясняет, как мастер установки hello работает hello во второй раз при запуске."
keywords: "Мастер установки Hello Azure AD Connect позволяет настраивать параметры hello обслуживания второй раз при запуске"
services: active-directory
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: d800214e-e591-4297-b9b5-d0b1581cc36a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 83cc74aca471ef9b4f65f7f3582e3e48d3d81cfe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-running-hello-installation-wizard-a-second-time"></a><span data-ttu-id="4f5ea-104">Синхронизация Azure AD Connect: запуск мастера установки hello еще раз</span><span class="sxs-lookup"><span data-stu-id="4f5ea-104">Azure AD Connect sync: Running hello installation wizard a second time</span></span>
<span data-ttu-id="4f5ea-105">Hello первом запуске мастера установки hello Azure AD Connect, оно описано, как tooconfigure установки.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-105">hello first time you run hello Azure AD Connect installation wizard, it walks you through how tooconfigure your installation.</span></span> <span data-ttu-id="4f5ea-106">При запуске мастера установки hello, он предлагает варианты для обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-106">If you run hello installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="4f5ea-107">Приветствия мастера установки можно найти в меню "Пуск" hello с именем **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-107">You can find hello installation wizard in hello start menu named **Azure AD Connect**.</span></span>

![Меню "Пуск"](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="4f5ea-109">При запуске мастера установки hello, отображается страница с этими параметрами.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-109">When you start hello installation wizard, you see a page with these options:</span></span>

![Страница со списком дополнительных задач](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="4f5ea-111">Если вы установили службы AD FS с Azure AD Connect, вам будет доступно еще больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="4f5ea-112">Здравствуйте, дополнительные параметры, у вас есть по ADFS описаны в [управления ADFS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-112">hello additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="4f5ea-113">Выберите одну из задач hello и нажмите кнопку **Далее** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-113">Select one of hello tasks and click **Next** toocontinue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4f5ea-114">При наличии откройте мастер установки hello приостанавливаются все операции в модуль синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-114">While you have hello installation wizard open, all operations in hello sync engine are suspended.</span></span> <span data-ttu-id="4f5ea-115">Убедитесь, что сразу после завершения изменения конфигурации, закройте мастер установки hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-115">Make sure you close hello installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="4f5ea-116">Просмотр текущей конфигурации</span><span class="sxs-lookup"><span data-stu-id="4f5ea-116">View current configuration</span></span>
<span data-ttu-id="4f5ea-117">Этот параметр позволяет быстро просмотреть текущие настройки параметров.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-117">This option gives you a quick view of your currently configured options.</span></span>

![Страница со списком всех параметров и их состоянием](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="4f5ea-119">Нажмите кнопку **Назад** toogo назад.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-119">Click **Previous** toogo back.</span></span> <span data-ttu-id="4f5ea-120">При выборе **выхода**, закройте мастер установки hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-120">If you select **Exit**, you close hello installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="4f5ea-121">Настройка параметров синхронизации</span><span class="sxs-lookup"><span data-stu-id="4f5ea-121">Customize synchronization options</span></span>
<span data-ttu-id="4f5ea-122">Этот параметр является toohello синхронизации используется toomake изменения конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-122">This option is used toomake changes toohello sync configuration.</span></span> <span data-ttu-id="4f5ea-123">Вы увидите подмножество параметров hello пути установки пользовательской конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-123">You see a subset of options from hello custom configuration installation path.</span></span> <span data-ttu-id="4f5ea-124">Они отобразятся, даже если изначально использовались параметры экспресс-установки.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="4f5ea-125">[Добавить дополнительные каталоги](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="4f5ea-126">Сведения об удалении каталога см. [здесь](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="4f5ea-127">[Изменить фильтрацию доменов и подразделений](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="4f5ea-128">Удалить групповую фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-128">Remove Group filtering.</span></span>
* <span data-ttu-id="4f5ea-129">[Изменить дополнительные возможности](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="4f5ea-130">Hello другие параметры из первоначальной установки hello не может быть изменено и не доступны.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-130">hello other options from hello initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="4f5ea-131">Доступны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="4f5ea-131">These options are:</span></span>

* <span data-ttu-id="4f5ea-132">Изменить toouse hello атрибут userPrincipalName и sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-132">Change hello attribute toouse for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="4f5ea-133">Изменить hello присоединение метод для объектов из другого леса.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-133">Change hello joining method for objects from different forest.</span></span>
* <span data-ttu-id="4f5ea-134">Включить фильтрацию на основе группы.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="4f5ea-135">Обновление схемы каталога</span><span class="sxs-lookup"><span data-stu-id="4f5ea-135">Refresh directory schema</span></span>
<span data-ttu-id="4f5ea-136">Этот параметр используется при изменении схемы hello в одном из локальных лесов AD DS.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-136">This option is used if you have changed hello schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="4f5ea-137">Например мог установить Exchange или обновления схемы tooa Windows Server 2012 с объектами устройства.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-137">For example, you might have installed Exchange or upgraded tooa Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="4f5ea-138">В этом случае требуется tooinstruct Azure AD Connect tooread hello схемы из AD DS и обновляет свой кэш.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-138">In this case, you need tooinstruct Azure AD Connect tooread hello schema again from AD DS and update its cache.</span></span> <span data-ttu-id="4f5ea-139">Это действие также выполняется повторное создание правила синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-139">This action also regenerates hello Sync Rules.</span></span> <span data-ttu-id="4f5ea-140">При добавлении схемы Exchange hello, например hello правила синхронизации для Exchange добавляются toohello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-140">If you add hello Exchange schema, as an example, hello Sync Rules for Exchange are added toohello configuration.</span></span>

<span data-ttu-id="4f5ea-141">При выборе этого параметра отображаются все каталоги hello в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-141">When you select this option, all hello directories in your configuration are listed.</span></span> <span data-ttu-id="4f5ea-142">Можно сохранить значение по умолчанию hello и обновление всех лесах или отменить выбор некоторых из них.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-142">You can keep hello default setting and refresh all forests or unselect some of them.</span></span>

![Страница со списком всех каталогов в среде hello](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="4f5ea-144">Настройка промежуточного режима</span><span class="sxs-lookup"><span data-stu-id="4f5ea-144">Configure staging mode</span></span>
<span data-ttu-id="4f5ea-145">Этот параметр позволяет вам tooenable и отключить промежуточный режим на сервере hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-145">This option allows you tooenable and disable staging mode on hello server.</span></span> <span data-ttu-id="4f5ea-146">Дополнительные сведения о промежуточном режиме и его использовании см. [здесь](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="4f5ea-147">При выборе параметра Hello отображаются, если промежуточной включено или отключено:</span><span class="sxs-lookup"><span data-stu-id="4f5ea-147">hello option shows if staging is currently enabled or disabled:</span></span>  
![Параметр, который отображается текущее состояние промежуточного режима hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="4f5ea-149">toochange Здравствуйте состояния, выберите этот параметр и выберите или отмените выбор hello флажок.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-149">toochange hello state, select this option and select or unselect hello checkbox.</span></span>  
![Параметр, который отображается текущее состояние промежуточного режима hello](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="4f5ea-151">Изменение параметров входа пользователя</span><span class="sxs-lookup"><span data-stu-id="4f5ea-151">Change user sign-in</span></span>
<span data-ttu-id="4f5ea-152">Этот параметр позволяет toochange из toofederation синхронизации пароля или наоборот hello.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-152">This option allows you toochange from password sync toofederation or hello other way around.</span></span> <span data-ttu-id="4f5ea-153">Невозможно изменить слишком**не задан**.</span><span class="sxs-lookup"><span data-stu-id="4f5ea-153">You cannot change too**do not configure**.</span></span>

<span data-ttu-id="4f5ea-154">Дополнительные сведения о входе пользователя см. [здесь](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f5ea-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4f5ea-155">Next steps</span></span>
* <span data-ttu-id="4f5ea-156">Дополнительные сведения о модели конфигурации hello, используемой службой Azure AD Connect sync в [декларативной подготовки основные сведения о](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4f5ea-156">Learn more about hello configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="4f5ea-157">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="4f5ea-157">**Overview topics**</span></span>

* [<span data-ttu-id="4f5ea-158">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="4f5ea-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4f5ea-159">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4f5ea-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
