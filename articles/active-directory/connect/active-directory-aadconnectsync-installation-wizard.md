---
title: "Повторное выполнение мастера установки Azure AD Connect | Документация Майкрософт"
description: "Объясняется, как работает мастер установки при повторном запуске."
keywords: "При повторном запуске мастера установки Azure AD Connect он позволяет настроить параметры обслуживания."
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
ms.openlocfilehash: 42855b785c0ab334e33a622c8db912ce2438c627
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-running-the-installation-wizard-a-second-time"></a><span data-ttu-id="4dba5-104">Синхронизация Azure AD Connect sync: повторный запуск мастера установки</span><span class="sxs-lookup"><span data-stu-id="4dba5-104">Azure AD Connect sync: Running the installation wizard a second time</span></span>
<span data-ttu-id="4dba5-105">При первом запуске мастера установки Azure AD Connect выполняется пошаговая настройка установки.</span><span class="sxs-lookup"><span data-stu-id="4dba5-105">The first time you run the Azure AD Connect installation wizard, it walks you through how to configure your installation.</span></span> <span data-ttu-id="4dba5-106">При повторном запуске мастера установки предлагается настроить параметры обслуживания.</span><span class="sxs-lookup"><span data-stu-id="4dba5-106">If you run the installation wizard again, it offers options for maintenance.</span></span>

<span data-ttu-id="4dba5-107">Мастер установки можно найти в меню "Пуск" с именем **Azure AD Connect**.</span><span class="sxs-lookup"><span data-stu-id="4dba5-107">You can find the installation wizard in the start menu named **Azure AD Connect**.</span></span>

![Меню "Пуск"](./media/active-directory-aadconnectsync-installation-wizard/startmenu.png)

<span data-ttu-id="4dba5-109">При запуске мастера установки появится страница со следующими параметрами:</span><span class="sxs-lookup"><span data-stu-id="4dba5-109">When you start the installation wizard, you see a page with these options:</span></span>

![Страница со списком дополнительных задач](./media/active-directory-aadconnectsync-installation-wizard/additionaltasks.png)

<span data-ttu-id="4dba5-111">Если вы установили службы AD FS с Azure AD Connect, вам будет доступно еще больше возможностей.</span><span class="sxs-lookup"><span data-stu-id="4dba5-111">If you have installed ADFS with Azure AD Connect, you have even more options.</span></span> <span data-ttu-id="4dba5-112">Дополнительные возможности служб AD FS описаны в разделе [Управление AD FS](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span><span class="sxs-lookup"><span data-stu-id="4dba5-112">The additional options you have for ADFS are documented in [ADFS management](active-directory-aadconnect-federation-management.md#manage-ad-fs).</span></span>

<span data-ttu-id="4dba5-113">Чтобы продолжить, выберите одну из задач и нажмите кнопку **Далее** .</span><span class="sxs-lookup"><span data-stu-id="4dba5-113">Select one of the tasks and click **Next** to continue.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4dba5-114">Когда открыт мастер установки, приостанавливаются все операции в модуле синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4dba5-114">While you have the installation wizard open, all operations in the sync engine are suspended.</span></span> <span data-ttu-id="4dba5-115">Убедитесь, что сразу после внесения изменений в конфигурацию вы завершили работу мастера установки.</span><span class="sxs-lookup"><span data-stu-id="4dba5-115">Make sure you close the installation wizard as soon as you have completed your configuration changes.</span></span>
>
>

## <a name="view-current-configuration"></a><span data-ttu-id="4dba5-116">Просмотр текущей конфигурации</span><span class="sxs-lookup"><span data-stu-id="4dba5-116">View current configuration</span></span>
<span data-ttu-id="4dba5-117">Этот параметр позволяет быстро просмотреть текущие настройки параметров.</span><span class="sxs-lookup"><span data-stu-id="4dba5-117">This option gives you a quick view of your currently configured options.</span></span>

![Страница со списком всех параметров и их состоянием](./media/active-directory-aadconnectsync-installation-wizard/viewconfig.png)

<span data-ttu-id="4dba5-119">Чтобы вернуться, нажмите кнопку **Назад** .</span><span class="sxs-lookup"><span data-stu-id="4dba5-119">Click **Previous** to go back.</span></span> <span data-ttu-id="4dba5-120">Если выбрать **Выход**, окно мастера установки закроется.</span><span class="sxs-lookup"><span data-stu-id="4dba5-120">If you select **Exit**, you close the installation wizard.</span></span>

## <a name="customize-synchronization-options"></a><span data-ttu-id="4dba5-121">Настройка параметров синхронизации</span><span class="sxs-lookup"><span data-stu-id="4dba5-121">Customize synchronization options</span></span>
<span data-ttu-id="4dba5-122">Этот параметр используется для изменения конфигурации синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4dba5-122">This option is used to make changes to the sync configuration.</span></span> <span data-ttu-id="4dba5-123">Вы увидите набор параметров из пути установки пользовательской конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4dba5-123">You see a subset of options from the custom configuration installation path.</span></span> <span data-ttu-id="4dba5-124">Они отобразятся, даже если изначально использовались параметры экспресс-установки.</span><span class="sxs-lookup"><span data-stu-id="4dba5-124">You see this option even if you used express installation initially.</span></span>

* <span data-ttu-id="4dba5-125">[Добавить дополнительные каталоги](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span><span class="sxs-lookup"><span data-stu-id="4dba5-125">[Add more directories](active-directory-aadconnect-get-started-custom.md#connect-your-directories).</span></span> <span data-ttu-id="4dba5-126">Сведения об удалении каталога см. [здесь](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span><span class="sxs-lookup"><span data-stu-id="4dba5-126">For removing a directory, see [Delete a Connector](active-directory-aadconnectsync-service-manager-ui-connectors.md#delete).</span></span>
* <span data-ttu-id="4dba5-127">[Изменить фильтрацию доменов и подразделений](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span><span class="sxs-lookup"><span data-stu-id="4dba5-127">[Change Domain and OU filtering](active-directory-aadconnect-get-started-custom.md#domain-and-ou-filtering).</span></span>
* <span data-ttu-id="4dba5-128">Удалить групповую фильтрацию.</span><span class="sxs-lookup"><span data-stu-id="4dba5-128">Remove Group filtering.</span></span>
* <span data-ttu-id="4dba5-129">[Изменить дополнительные возможности](active-directory-aadconnect-get-started-custom.md#optional-features).</span><span class="sxs-lookup"><span data-stu-id="4dba5-129">[Change optional features](active-directory-aadconnect-get-started-custom.md#optional-features).</span></span>

<span data-ttu-id="4dba5-130">Другие параметры из начальной установки нельзя изменить, поэтому они недоступны.</span><span class="sxs-lookup"><span data-stu-id="4dba5-130">The other options from the initial installation cannot be changed and are not available.</span></span> <span data-ttu-id="4dba5-131">Доступны следующие параметры:</span><span class="sxs-lookup"><span data-stu-id="4dba5-131">These options are:</span></span>

* <span data-ttu-id="4dba5-132">Изменить атрибут, используемый для userPrincipalName и sourceAnchor.</span><span class="sxs-lookup"><span data-stu-id="4dba5-132">Change the attribute to use for userPrincipalName and sourceAnchor.</span></span>
* <span data-ttu-id="4dba5-133">Изменить метод соединения для объектов из другого леса.</span><span class="sxs-lookup"><span data-stu-id="4dba5-133">Change the joining method for objects from different forest.</span></span>
* <span data-ttu-id="4dba5-134">Включить фильтрацию на основе группы.</span><span class="sxs-lookup"><span data-stu-id="4dba5-134">Enable group-based filtering.</span></span>

## <a name="refresh-directory-schema"></a><span data-ttu-id="4dba5-135">Обновление схемы каталога</span><span class="sxs-lookup"><span data-stu-id="4dba5-135">Refresh directory schema</span></span>
<span data-ttu-id="4dba5-136">Этот параметр используется при изменении схемы в одном из локальных лесов AD DS.</span><span class="sxs-lookup"><span data-stu-id="4dba5-136">This option is used if you have changed the schema in one of your on-premises AD DS forests.</span></span> <span data-ttu-id="4dba5-137">Например, когда выполнена установка Exchange или обновление до схемы Windows Server 2012 с объектами устройства.</span><span class="sxs-lookup"><span data-stu-id="4dba5-137">For example, you might have installed Exchange or upgraded to a Windows Server 2012 schema with device objects.</span></span> <span data-ttu-id="4dba5-138">В этом случае необходимо настроить Azure AD Connect на повторное чтение схемы из AD DS и обновление кэша.</span><span class="sxs-lookup"><span data-stu-id="4dba5-138">In this case, you need to instruct Azure AD Connect to read the schema again from AD DS and update its cache.</span></span> <span data-ttu-id="4dba5-139">Это действие также повторно создает правила синхронизации.</span><span class="sxs-lookup"><span data-stu-id="4dba5-139">This action also regenerates the Sync Rules.</span></span> <span data-ttu-id="4dba5-140">Если добавить, например, схему Exchange, то правила синхронизации для Exchange добавятся в конфигурацию.</span><span class="sxs-lookup"><span data-stu-id="4dba5-140">If you add the Exchange schema, as an example, the Sync Rules for Exchange are added to the configuration.</span></span>

<span data-ttu-id="4dba5-141">При выборе этого параметра отобразятся все каталоги в конфигурации.</span><span class="sxs-lookup"><span data-stu-id="4dba5-141">When you select this option, all the directories in your configuration are listed.</span></span> <span data-ttu-id="4dba5-142">Можно оставить значение по умолчанию и обновить все леса или отменить выбор некоторых из них.</span><span class="sxs-lookup"><span data-stu-id="4dba5-142">You can keep the default setting and refresh all forests or unselect some of them.</span></span>

![Страница со списком всех каталогов в среде](./media/active-directory-aadconnectsync-installation-wizard/refreshschema.png)

## <a name="configure-staging-mode"></a><span data-ttu-id="4dba5-144">Настройка промежуточного режима</span><span class="sxs-lookup"><span data-stu-id="4dba5-144">Configure staging mode</span></span>
<span data-ttu-id="4dba5-145">Этот параметр позволяет включить и отключить на сервере промежуточный режим.</span><span class="sxs-lookup"><span data-stu-id="4dba5-145">This option allows you to enable and disable staging mode on the server.</span></span> <span data-ttu-id="4dba5-146">Дополнительные сведения о промежуточном режиме и его использовании см. [здесь](active-directory-aadconnectsync-operations.md#staging-mode).</span><span class="sxs-lookup"><span data-stu-id="4dba5-146">More information about staging mode and how it is used can be found in [Operations](active-directory-aadconnectsync-operations.md#staging-mode).</span></span>

<span data-ttu-id="4dba5-147">Рядом с параметром будет показано, включен или отключен промежуточный режим в данный момент: </span><span class="sxs-lookup"><span data-stu-id="4dba5-147">The option shows if staging is currently enabled or disabled:</span></span>  
![Параметр, который также отображает текущее состояние промежуточного режима](./media/active-directory-aadconnectsync-installation-wizard/stagingmodecurrentstate.png)

<span data-ttu-id="4dba5-149">Для изменения состояния выберите этот параметр и установите или снимите флажок.</span><span class="sxs-lookup"><span data-stu-id="4dba5-149">To change the state, select this option and select or unselect the checkbox.</span></span>  
![Параметр, который также отображает текущее состояние промежуточного режима](./media/active-directory-aadconnectsync-installation-wizard/stagingmodeenable.png)

## <a name="change-user-sign-in"></a><span data-ttu-id="4dba5-151">Изменение параметров входа пользователя</span><span class="sxs-lookup"><span data-stu-id="4dba5-151">Change user sign-in</span></span>
<span data-ttu-id="4dba5-152">Этот параметр позволяет заменить синхронизацию паролей на федерацию или наоборот.</span><span class="sxs-lookup"><span data-stu-id="4dba5-152">This option allows you to change from password sync to federation or the other way around.</span></span> <span data-ttu-id="4dba5-153">Нельзя изменить на значение **Не настраивать**.</span><span class="sxs-lookup"><span data-stu-id="4dba5-153">You cannot change to **do not configure**.</span></span>

<span data-ttu-id="4dba5-154">Дополнительные сведения о входе пользователя см. [здесь](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span><span class="sxs-lookup"><span data-stu-id="4dba5-154">For more information on this option, see [user sign-in](active-directory-aadconnect-user-signin.md#changing-the-user-sign-in-method).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4dba5-155">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4dba5-155">Next steps</span></span>
* <span data-ttu-id="4dba5-156">Дополнительные сведения о модели конфигурации, используемой в синхронизации Azure AD Connect, см. в статье о [принципах декларативной подготовки](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span><span class="sxs-lookup"><span data-stu-id="4dba5-156">Learn more about the configuration model used by Azure AD Connect sync in [Understanding Declarative Provisioning](active-directory-aadconnectsync-understanding-declarative-provisioning.md).</span></span>

<span data-ttu-id="4dba5-157">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="4dba5-157">**Overview topics**</span></span>

* [<span data-ttu-id="4dba5-158">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="4dba5-158">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="4dba5-159">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="4dba5-159">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
