---
title: "Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect | Документация Майкрософт"
description: "Эта статья содержит сведения по устранению неполадок синхронизации паролей."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 33fa6a8867764975a57b8727e7705529d1d7506a
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="ebbe9-103">Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="ebbe9-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="ebbe9-104">В этой статье приводятся пошаговые инструкции для устранения неполадок, связанных с синхронизацией паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-104">This topic provides steps for how to troubleshoot issues with password synchronization.</span></span> <span data-ttu-id="ebbe9-105">Неполадки синхронизации паролей могут возникать либо в подмножестве пользователей, либо у всех.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="ebbe9-106">Для развертывания Azure Active Directory (Azure AD) Connect версии 1.1.524.0 или более поздних теперь есть командлет диагностики, который вы можете использовать для устранения неполадок синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use to troubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="ebbe9-107">Если пароли не синхронизируются, перейдите к разделу [Пароли не синхронизируются: устранение неполадок с помощью командлета диагностики](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-107">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: troubleshoot by using the diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="ebbe9-108">Если возникла проблема с отдельными объектами, перейдите к разделу [Пароли не синхронизируются одним объектом: устранение неполадок с помощью командлета диагностики](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-108">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="ebbe9-109">Для ранних версий развертывания Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="ebbe9-110">Если пароли не синхронизируются, перейдите к разделу [Пароли не синхронизируются: шаги по устранению неполадок вручную](#no-passwords-are-synchronized-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-110">If you have an issue where no passwords are synchronized, refer to the [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="ebbe9-111">Если возникла проблема с отдельными объектами, перейдите к разделу [Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-111">If you have an issue with individual objects, refer to the [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="ebbe9-112">Пароли не синхронизируются: устранение неполадок с помощью командлета диагностики</span><span class="sxs-lookup"><span data-stu-id="ebbe9-112">No passwords are synchronized: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="ebbe9-113">Вы можете использовать командлет `Invoke-ADSyncDiagnostics`, чтобы выяснить, почему не происходит синхронизация паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-113">You can use the `Invoke-ADSyncDiagnostics` cmdlet to figure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbe9-114">Командлет `Invoke-ADSyncDiagnostics` доступен только для Azure AD Connect версии 1.1.524.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-114">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="ebbe9-115">Запуск командлета диагностики</span><span class="sxs-lookup"><span data-stu-id="ebbe9-115">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="ebbe9-116">Чтобы устранить неполадки, связанные с синхронизацией паролей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-116">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="ebbe9-117">Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-117">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="ebbe9-118">Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="ebbe9-119">Запустите `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="ebbe9-120">Запустите `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="ebbe9-121">Изучение результатов выполнения командлета</span><span class="sxs-lookup"><span data-stu-id="ebbe9-121">Understand the results of the cmdlet</span></span>
<span data-ttu-id="ebbe9-122">Командлет диагностики выполняет следующие проверки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-122">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="ebbe9-123">Проверяет, чтобы для вашего клиента Azure AD была включена функция синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-123">Validates that the password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="ebbe9-124">Проверяет, чтобы сервер Azure AD Connect не находился в промежуточном режиме.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-124">Validates that the Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="ebbe9-125">Для каждого существующего локального соединителя Active Directory (который соответствует существующему лесу Active Directory):</span><span class="sxs-lookup"><span data-stu-id="ebbe9-125">For each existing on-premises Active Directory connector (which corresponds to an existing Active Directory forest):</span></span>

   * <span data-ttu-id="ebbe9-126">Проверяет, чтобы была включена функция синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-126">Validates that the password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="ebbe9-127">Ищет события пульса синхронизации паролей в журнале событий приложений Windows.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-127">Searches for password synchronization heartbeat events in the Windows Application Event logs.</span></span>

   * <span data-ttu-id="ebbe9-128">Для каждого домена Active Directory в локальном соединителе Active Directory:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-128">For each Active Directory domain under the on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="ebbe9-129">Проверяет, чтобы из сервера Azure AD Connect можно было получить доступ к домену.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-129">Validates that the domain is reachable from the Azure AD Connect server.</span></span>

      * <span data-ttu-id="ebbe9-130">Проверяет, чтобы учетные записи доменных служб Active Directory (AD DS), используемые локальным соединителем Active Directory, имели правильные имя пользователя, пароль и разрешения, необходимые для синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-130">Validates that the Active Directory Domain Services (AD DS) accounts used by the on-premises Active Directory connector has the correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="ebbe9-131">На схеме ниже отображаются результаты командлета для локальной топологии Active Directory с одним доменом:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-131">The following diagram illustrates the results of the cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Диагностические выходные данные для синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="ebbe9-133">В оставшейся части этого раздела описываются определенные результаты, возвращенные командлетом, и соответствующие неполадки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-133">The rest of this section describes specific results that are returned by the cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="ebbe9-134">Отключена функция синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="ebbe9-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="ebbe9-135">Если вы не включили синхронизацию паролей с помощью мастера Azure AD Connect, возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-135">If you haven't enabled password synchronization by using the Azure AD Connect wizard, the following error is returned:</span></span>

![Отключена функция синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="ebbe9-137">Сервер Azure AD Connect находится в промежуточном режиме</span><span class="sxs-lookup"><span data-stu-id="ebbe9-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="ebbe9-138">Если сервер Azure AD Connect находится в промежуточном режиме, синхронизация паролей временно отключена и возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-138">If the Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and the following error is returned:</span></span>

![Сервер Azure AD Connect находится в промежуточном режиме](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="ebbe9-140">Отсутствуют события пульса синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="ebbe9-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="ebbe9-141">У каждого локального соединителя Active Directory есть свой собственный канал синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="ebbe9-142">Если установлен канал синхронизации паролей и нет необходимости синхронизировать какие-либо изменения пароля, в журнале событий приложений Windows каждые 30 минут создается событие пульса (EventId 654).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-142">When the password synchronization channel is established and there aren't any password changes to be synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under the Windows Application Event Log.</span></span> <span data-ttu-id="ebbe9-143">Для каждого локального соединителя Active Directory командлет ищет соответствующие события пульса за последние три часа.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-143">For each on-premises Active Directory connector, the cmdlet searches for corresponding heartbeat events in the past three hours.</span></span> <span data-ttu-id="ebbe9-144">Если событие пульса не найдено, возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-144">If no heartbeat event is found, the following error is returned:</span></span>

![Отсутствует событие пульса синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="ebbe9-146">Учетная запись AD DS не имеет необходимых разрешений</span><span class="sxs-lookup"><span data-stu-id="ebbe9-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="ebbe9-147">Если учетная запись AD DS, используемая локальным соединителем Active Directory для синхронизации хэшей паролей, не содержит соответствующих разрешений, возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-147">If the AD DS account that's used by the on-premises Active Directory connector to synchronize password hashes does not have the appropriate permissions, the following error is returned:</span></span>

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="ebbe9-149">Неправильный пароль или имя пользователя учетной записи AD DS</span><span class="sxs-lookup"><span data-stu-id="ebbe9-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="ebbe9-150">Если учетная запись AD DS, используемая локальным соединителем Active Directory для синхронизации хэшей паролей, содержит неправильный пароль или имя пользователя, возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-150">If the AD DS account used by the on-premises Active Directory connector to synchronize password hashes has an incorrect username or password, the following error is returned:</span></span>

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet"></a><span data-ttu-id="ebbe9-152">Пароли не синхронизируются одним объектом: устранение неполадок с помощью командлета диагностики</span><span class="sxs-lookup"><span data-stu-id="ebbe9-152">One object is not synchronizing passwords: troubleshoot by using the diagnostic cmdlet</span></span>
<span data-ttu-id="ebbe9-153">Вы можете использовать командлет `Invoke-ADSyncDiagnostics`, чтобы определить, почему пароли не синхронизируются одним объектом.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-153">You can use the `Invoke-ADSyncDiagnostics` cmdlet to determine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="ebbe9-154">Командлет `Invoke-ADSyncDiagnostics` доступен только для Azure AD Connect версии 1.1.524.0 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-154">The `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-the-diagnostics-cmdlet"></a><span data-ttu-id="ebbe9-155">Запуск командлета диагностики</span><span class="sxs-lookup"><span data-stu-id="ebbe9-155">Run the diagnostics cmdlet</span></span>
<span data-ttu-id="ebbe9-156">Чтобы устранить неполадки, связанные с синхронизацией паролей, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-156">To troubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="ebbe9-157">Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с помощью параметра **Запуск от имени администратора**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-157">Open a new Windows PowerShell session on your Azure AD Connect server with the **Run as Administrator** option.</span></span>

2. <span data-ttu-id="ebbe9-158">Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="ebbe9-159">Запустите `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="ebbe9-160">Выполните следующий командлет:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-160">Run the following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="ebbe9-161">Например:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-the-results-of-the-cmdlet"></a><span data-ttu-id="ebbe9-162">Изучение результатов выполнения командлета</span><span class="sxs-lookup"><span data-stu-id="ebbe9-162">Understand the results of the cmdlet</span></span>
<span data-ttu-id="ebbe9-163">Командлет диагностики выполняет следующие проверки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-163">The diagnostic cmdlet performs the following checks:</span></span>

* <span data-ttu-id="ebbe9-164">Проверяет состояние объекта Active Directory в пространстве соединителя Active Directory, метавселенной и пространстве соединителя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-164">Examines the state of the Active Directory object in the Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="ebbe9-165">Проверяет, чтобы с синхронизацией паролей были включены правила синхронизации, и чтобы они были применены к объекту Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-165">Validates that there are synchronization rules with password synchronization enabled and applied to the Active Directory object.</span></span>

* <span data-ttu-id="ebbe9-166">Пытается извлечь и отобразить результаты последней попытки синхронизации паролей для объекта.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-166">Attempts to retrieve and display the results of the last attempt to synchronize the password for the object.</span></span>

<span data-ttu-id="ebbe9-167">На схеме ниже отображаются результаты командлета при устранении неполадок синхронизации паролей для одного объекта:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-167">The following diagram illustrates the results of the cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Диагностические выходные данные для синхронизации паролей для одного объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="ebbe9-169">В оставшейся части этого раздела описываются определенные результаты, возвращенные командлетом, и соответствующие неполадки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-169">The rest of this section describes specific results returned by the cmdlet and corresponding issues.</span></span>

#### <a name="the-active-directory-object-isnt-exported-to-azure-ad"></a><span data-ttu-id="ebbe9-170">Невозможно экспортировать в Azure AD объект Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebbe9-170">The Active Directory object isn't exported to Azure AD</span></span>
<span data-ttu-id="ebbe9-171">Синхронизация паролей для этой локальной учетной записи Active Directory завершается сбоем, так как в клиенте Azure AD отсутствует соответствующий объект.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in the Azure AD tenant.</span></span> <span data-ttu-id="ebbe9-172">Возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-172">The following error is returned:</span></span>

![Отсутствует объект Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="ebbe9-174">У пользователя временный пароль</span><span class="sxs-lookup"><span data-stu-id="ebbe9-174">User has a temporary password</span></span>
<span data-ttu-id="ebbe9-175">В настоящее время Azure AD Connect не поддерживает синхронизацию временных паролей с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="ebbe9-176">Пароль может рассматриваться как временный, если для локального пользователя Active Directory установлен параметр **смены пароля при следующем входе в систему**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-176">A password is considered to be temporary if the **Change password at next logon** option is set on the on-premises Active Directory user.</span></span> <span data-ttu-id="ebbe9-177">Возвращается следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-177">The following error is returned:</span></span>

![Временный пароль не экспортируется](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-to-synchronize-password-arent-available"></a><span data-ttu-id="ebbe9-179">Результаты последней попытки синхронизации пароля недоступны</span><span class="sxs-lookup"><span data-stu-id="ebbe9-179">Results of last attempt to synchronize password aren't available</span></span>
<span data-ttu-id="ebbe9-180">По умолчанию Azure AD Connect хранит результаты синхронизации паролей семь дней.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-180">By default, Azure AD Connect stores the results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="ebbe9-181">Если для выбранного объекта Active Directory результаты недоступны, возвращается следующее предупреждение:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-181">If there are no results available for the selected Active Directory object, the following warning is returned:</span></span>

![Диагностические выходные данные для одного объекта: отсутствует история синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="ebbe9-183">Пароли не синхронизируются: шаги по устранению неполадок вручную</span><span class="sxs-lookup"><span data-stu-id="ebbe9-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="ebbe9-184">Чтобы выяснить, почему не происходит синхронизация паролей, выполните следующие действия:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-184">Follow these steps to determine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="ebbe9-185">Переведен ли сервер Connect в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="ebbe9-185">Is the Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="ebbe9-186">Сервер, находящийся в промежуточном режиме, не синхронизирует пароли.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="ebbe9-187">Выполните сценарий, приведенный в разделе [Получение состояния параметров синхронизации паролей](#get-the-status-of-password-sync-settings).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-187">Run the script in the [Get the status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="ebbe9-188">В этом разделе рассматривается конфигурация синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-188">It gives you an overview of the password sync configuration.</span></span>  

    ![Выходные данные сценария PowerShell из параметров синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="ebbe9-190">Если в Azure AD не включена функция синхронизации паролей или не добавлено состояние канала синхронизации, запустите мастер установки Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-190">If the feature is not enabled in Azure AD or if the sync channel status is not enabled, run the Connect installation wizard.</span></span> <span data-ttu-id="ebbe9-191">Выберите **Настроить параметры синхронизации** и снимите флажок синхронизации паролей. Это позволит временно отключить функцию.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables the feature.</span></span> <span data-ttu-id="ebbe9-192">Затем снова запустите мастер установки и включите синхронизацию паролей. Запустите скрипт снова и проверьте правильность конфигурации.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-192">Then run the wizard again and re-enable password sync. Run the script again to verify that the configuration is correct.</span></span>

4. <span data-ttu-id="ebbe9-193">Проверьте журнал событий на наличие ошибок.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-193">Look in the event log for errors.</span></span> <span data-ttu-id="ebbe9-194">Найдите следующие события, которые могут указывать на проблему:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-194">Look for the following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="ebbe9-195">Источник: "Directory synchronization" ID: 0, 611, 652, 655. Если вы видите эти события, то это свидетельствует о проблеме с подключением.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="ebbe9-196">Сообщение в журнале событий содержит сведения о лесе, в котором возникла проблема.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-196">The event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="ebbe9-197">Дополнительные сведения см. в разделе о [проблеме с подключением](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="ebbe9-198">Если нет пульса или не сработали другие методы, то [запустите полную синхронизацию всех паролей](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="ebbe9-199">Этот сценарий необходимо выполнить только один раз.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-199">Run the script only once.</span></span>

6. <span data-ttu-id="ebbe9-200">Ознакомьтесь с разделом [Пароли не синхронизируются одним объектом](#one-object-is-not-synchronizing-passwords).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-200">See the [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="ebbe9-201">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="ebbe9-201">Connectivity problems</span></span>

<span data-ttu-id="ebbe9-202">Проверьте, есть ли подключение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="ebbe9-203">Имеет ли учетная запись необходимые разрешения для чтения хэшей паролей во всех доменах?</span><span class="sxs-lookup"><span data-stu-id="ebbe9-203">Does the account have required permissions to read the password hashes in all domains?</span></span> <span data-ttu-id="ebbe9-204">Если при установке Connect вы использовали стандартные параметры, то у вас уже должны быть необходимые разрешения.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-204">If you installed Connect by using Express settings, the permissions should already be correct.</span></span> 

<span data-ttu-id="ebbe9-205">Если вы использовали выборочную установку, задайте разрешения вручную следующим образом:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-205">If you used custom installation, set the permissions manually by doing the following:</span></span>
    
1. <span data-ttu-id="ebbe9-206">Чтобы найти учетную запись, используемую соединителем Active Directory, запустите **Synchronization Service Manager**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-206">To find the account used by the Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="ebbe9-207">Перейдите в раздел **Connectors** (Соединители), а затем найдите локальный лес Active Directory, в котором устраняются неполадки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-207">Go to **Connectors**, and then search for the on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="ebbe9-208">Выберите соединитель и щелкните **Properties** (Свойства).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-208">Select the connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="ebbe9-209">Выберите **Подключиться к лесу Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-209">Go to **Connect to Active Directory Forest**.</span></span>  
    
    ![Учетная запись, используемая соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="ebbe9-211">Запишите имя пользователя и домен, в котором размещена учетная запись.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-211">Note the username and the domain where the account is located.</span></span>
    
5. <span data-ttu-id="ebbe9-212">Запустите **Пользователи и компьютеры Active Directory** и проверьте, чтобы для учетной записи, найденной на предыдущем шаге, в корне всех доменов в лесу были заданы следующие разрешения:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-212">Start **Active Directory Users and Computers**, and then verify that the account you found earlier has the follow permissions set at the root of all domains in your forest:</span></span>
    * <span data-ttu-id="ebbe9-213">Репликация изменений каталога</span><span class="sxs-lookup"><span data-stu-id="ebbe9-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="ebbe9-214">Репликация всех изменений каталога</span><span class="sxs-lookup"><span data-stu-id="ebbe9-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="ebbe9-215">Доступны ли контроллеры домена для Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="ebbe9-215">Are the domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="ebbe9-216">Если серверу Connect не удается подключиться ко всем контроллерам домена, настройте параметр **Only use preferred domain controller** (Использовать только предпочтительные контроллеры домена).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-216">If the Connect server cannot connect to all domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Контроллер домена, используемый соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="ebbe9-218">Вернитесь в меню **Synchronization Service Manager** и выберите **Configure Directory Partitions** (Настройка разделов каталога).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-218">Go back to **Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="ebbe9-219">В списке **Select directory partitions** (Выбор разделов каталога) выберите свой домен, установите флажок **Only use preferred domain controllers** (Использовать только предпочтительные контроллеры домена), а затем щелкните **Configure** (Настроить).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-219">Select your domain in **Select directory partitions**, select the **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="ebbe9-220">В списке введите контроллеры домена, которые будет использовать Connect для синхронизации паролей. Этот же список используется для импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-220">In the list, enter the domain controllers that Connect should use for password sync. The same list is used for import and export as well.</span></span> <span data-ttu-id="ebbe9-221">Выполните эти действия для всех доменов.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="ebbe9-222">Если в сценарии отображается отсутствие пульса, тогда запустите сценарий, приведенный в разделе [Запуск полной синхронизации всех паролей](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-222">If the script shows that there is no heartbeat, run the script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="ebbe9-223">Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную</span><span class="sxs-lookup"><span data-stu-id="ebbe9-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="ebbe9-224">Проблемы, связанные с синхронизацией паролей, можно легко устранить, просмотрев состояние объекта.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-224">You can easily troubleshoot password synchronization issues by reviewing the status of an object.</span></span>

1. <span data-ttu-id="ebbe9-225">В средстве **Пользователи и компьютеры Active Directory** найдите пользователя, а затем убедитесь в отсутствии флажка для параметра **Требовать смены пароля при следующем входе в систему**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-225">In **Active Directory Users and Computers**, search for the user, and then verify that the **User must change password at next logon** check box is cleared.</span></span>  

    ![Повышение производительности в Active Directory с помощью синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="ebbe9-227">Если флажок установлен, пользователь должен войти в систему и сменить пароль.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-227">If the check box is selected, ask the user to sign in and change the password.</span></span> <span data-ttu-id="ebbe9-228">Временные пароли не синхронизируются с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="ebbe9-229">Если с паролем в Active Directory все в порядке, отследите пользователя в модуле синхронизации.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-229">If the password looks correct in Active Directory, follow the user in the sync engine.</span></span> <span data-ttu-id="ebbe9-230">Отследив пользователя от локального Active Directory до Azure AD, вы сможете убедиться в отсутствии ошибок в объекте.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-230">By following the user from on-premises Active Directory to Azure AD, you can see whether there is a descriptive error on the object.</span></span>

    <span data-ttu-id="ebbe9-231">а.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-231">a.</span></span> <span data-ttu-id="ebbe9-232">Запустите [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-232">Start the [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="ebbe9-233">b.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-233">b.</span></span> <span data-ttu-id="ebbe9-234">Щелкните **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-234">Click **Connectors**.</span></span>

    <span data-ttu-id="ebbe9-235">c.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-235">c.</span></span> <span data-ttu-id="ebbe9-236">Выберите **соединитель Active Directory**, к которому относится пользователь.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-236">Select the **Active Directory Connector** where the user is located.</span></span>

    <span data-ttu-id="ebbe9-237">г)</span><span class="sxs-lookup"><span data-stu-id="ebbe9-237">d.</span></span> <span data-ttu-id="ebbe9-238">Выберите **Search Connector Space**(Поиск пространства соединителя).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="ebbe9-239">д.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-239">e.</span></span> <span data-ttu-id="ebbe9-240">В поле **Scope** (Область) выберите **DN or Anchor** (Различающееся имя или привязка), а затем введите полное различающееся имя пользователя, для которого требуется устранить неполадки.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-240">In the **Scope** box, select **DN or Anchor**, and then enter the full DN of the user you are troubleshooting.</span></span>

    ![Поиск пользователя в пространстве соединителя с различающимся именем](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="ebbe9-242">f.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-242">f.</span></span> <span data-ttu-id="ebbe9-243">Найдите нужного пользователя и нажмите кнопку **Properties** (Свойства), чтобы просмотреть все атрибуты.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-243">Locate the user you are looking for, and then click **Properties** to see all the attributes.</span></span> <span data-ttu-id="ebbe9-244">Если в результатах поиска нет нужного пользователя, то проверьте [правила фильтрации](active-directory-aadconnectsync-configure-filtering.md) и выполните действия, описанные в разделе [Примените и проверьте изменения](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes). После этого пользователь должен отобразиться в Connect.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-244">If the user is not in the search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for the user to appear in Connect.</span></span>

    <span data-ttu-id="ebbe9-245">ж.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-245">g.</span></span> <span data-ttu-id="ebbe9-246">Чтобы просмотреть сведения о синхронизации паролей объекта за прошедшую неделю, щелкните **Log** (Журнал).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-246">To see the password sync details of the object for the past week, click **Log**.</span></span>  

    ![Сведения журнала для объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="ebbe9-248">Если журнал объекта пуст, то Azure AD Connect не сможет считать хэш паролей из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-248">If the object log is empty, Azure AD Connect has been unable to read the password hash from Active Directory.</span></span> <span data-ttu-id="ebbe9-249">Перейдите к устранению неполадок, описанных в разделе [Проблема подключения](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="ebbe9-250">Если состояние имеет значение, отличное от **успешного**, то воспользуйтесь таблицей в разделе [Журнал синхронизации паролей](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="ebbe9-250">If you see any other value than **success**, refer to the table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="ebbe9-251">h.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-251">h.</span></span> <span data-ttu-id="ebbe9-252">Выберите вкладку **Lineage** (Журнал обращений и преобразований) и убедитесь, что по крайней мере для одного правила синхронизации в колонке **PasswordSync** задано значение **True**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-252">Select the **lineage** tab, and make sure that at least one sync rule in the **PasswordSync** column is **True**.</span></span> <span data-ttu-id="ebbe9-253">В конфигурации по умолчанию правило синхронизации имеет имя **In from AD - User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-253">In the default configuration, the name of the sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Сведения о пользователе в журнале обращений и преобразований](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="ebbe9-255">i.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-255">i.</span></span> <span data-ttu-id="ebbe9-256">Щелкните **Metaverse Object Properties** (Свойства объекта метавселенной), чтобы показать список атрибутов пользователя.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-256">Click **Metaverse Object Properties** to display a list of user attributes.</span></span>  

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="ebbe9-258">Атрибут **cloudFiltered** должен отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="ebbe9-259">Убедитесь, что атрибуты домена (domainFQDN и domainNetBios) имеют ожидаемые значения.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-259">Make sure that the domain attributes (domainFQDN and domainNetBios) have the expected values.</span></span>

    <span data-ttu-id="ebbe9-260">j.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-260">j.</span></span> <span data-ttu-id="ebbe9-261">Щелкните вкладку **Connectors** (Соединители). Вы должны увидеть соединители для локального Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-261">Click the **Connectors** tab. Make sure that you see connectors to both on-premises Active Directory and Azure AD.</span></span>

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="ebbe9-263">k.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-263">k.</span></span> <span data-ttu-id="ebbe9-264">Выберите строку, которая представляет Azure AD, щелкните **Properties** (Свойства), а затем щелкните вкладку **Lineage** (Журнал обращений и преобразований). Объект пространства соединителя должен содержать правило исходящих подключений в колонке **синхронизации паролей** с заданным значением **True**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-264">Select the row that represents Azure AD, click **Properties**, and then click the **Lineage** tab. The connector space object should have an outbound rule in the **PasswordSync** column set to **True**.</span></span> <span data-ttu-id="ebbe9-265">В конфигурации по умолчанию это будет правило синхронизации с именем **Out to AAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-265">In the default configuration, the name of the sync rule is **Out to AAD - User Join**.</span></span>  

    ![Диалоговое окно свойств объекта пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="ebbe9-267">Журнал синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="ebbe9-267">Password sync log</span></span>
<span data-ttu-id="ebbe9-268">В столбце "Состояние" могут содержаться перечисленные ниже значения.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-268">The status column can have the following values:</span></span>

| <span data-ttu-id="ebbe9-269">Состояние</span><span class="sxs-lookup"><span data-stu-id="ebbe9-269">Status</span></span> | <span data-ttu-id="ebbe9-270">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="ebbe9-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ebbe9-271">Успешно</span><span class="sxs-lookup"><span data-stu-id="ebbe9-271">Success</span></span> |<span data-ttu-id="ebbe9-272">Пароль успешно синхронизирован</span><span class="sxs-lookup"><span data-stu-id="ebbe9-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="ebbe9-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="ebbe9-273">FilteredByTarget</span></span> |<span data-ttu-id="ebbe9-274">Для пароля установлено значение **Пользователь должен изменить пароль при следующем входе**.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-274">Password is set to **User must change password at next logon**.</span></span> <span data-ttu-id="ebbe9-275">Пароль не синхронизирован.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="ebbe9-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="ebbe9-276">NoTargetConnection</span></span> |<span data-ttu-id="ebbe9-277">Объект отсутствует в метавселенной или в пространстве соединителя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-277">No object in the metaverse or in the Azure AD connector space.</span></span> |
| <span data-ttu-id="ebbe9-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="ebbe9-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="ebbe9-279">Объект не найден в локальном пространстве соединителя Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-279">No object found in the on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="ebbe9-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="ebbe9-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="ebbe9-281">Объект в пространстве соединителя Azure AD еще не экспортирован.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-281">The object in the Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="ebbe9-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="ebbe9-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="ebbe9-283">Запись журнала создана до выхода версии 1.0.9125.0 и отображается в исходном состоянии.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="ebbe9-284">Ошибка</span><span class="sxs-lookup"><span data-stu-id="ebbe9-284">Error</span></span> |<span data-ttu-id="ebbe9-285">Служба вернула неизвестную ошибку.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="ebbe9-286">Unknown</span><span class="sxs-lookup"><span data-stu-id="ebbe9-286">Unknown</span></span> |<span data-ttu-id="ebbe9-287">Произошла ошибка при попытке обработать пакет хэшей паролей.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-287">An error occurred while trying to process a batch of password hashes.</span></span>  |
| <span data-ttu-id="ebbe9-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="ebbe9-288">MissingAttribute</span></span> |<span data-ttu-id="ebbe9-289">Недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="ebbe9-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="ebbe9-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="ebbe9-291">Ранее были недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="ebbe9-292">Предпринята попытка повторно синхронизировать хэш пароля пользователя.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-292">An attempt to resynchronize the user's password hash is made.</span></span> |

## <a name="scripts-to-help-troubleshooting"></a><span data-ttu-id="ebbe9-293">Сценарии, помогающие при устранении неполадок</span><span class="sxs-lookup"><span data-stu-id="ebbe9-293">Scripts to help troubleshooting</span></span>

### <a name="get-the-status-of-password-sync-settings"></a><span data-ttu-id="ebbe9-294">Получение состояния параметров синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="ebbe9-294">Get the status of password sync settings</span></span>
```
Import-Module ADSync
$connectors = Get-ADSyncConnector
$aadConnectors = $connectors | Where-Object {$_.SubType -eq "Windows Azure Active Directory (Microsoft)"}
$adConnectors = $connectors | Where-Object {$_.ConnectorTypeName -eq "AD"}
if ($aadConnectors -ne $null -and $adConnectors -ne $null)
{
    if ($aadConnectors.Count -eq 1)
    {
        $features = Get-ADSyncAADCompanyFeature -ConnectorName $aadConnectors[0].Name
        Write-Host
        Write-Host "Password sync feature enabled in your Azure AD directory: "  $features.PasswordHashSync
        foreach ($adConnector in $adConnectors)
        {
            Write-Host
            Write-Host "Password sync channel status BEGIN ------------------------------------------------------- "
            Write-Host
            Get-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector.Name
            Write-Host
            $pingEvents =
                Get-EventLog -LogName "Application" -Source "Directory Synchronization" -InstanceId 654  -After (Get-Date).AddHours(-3) |
                    Where-Object { $_.Message.ToUpperInvariant().Contains($adConnector.Identifier.ToString("D").ToUpperInvariant()) } |
                    Sort-Object { $_.Time } -Descending
            if ($pingEvents -ne $null)
            {
                Write-Host "Latest heart beat event (within last 3 hours). Time " $pingEvents[0].TimeWritten
            }
            else
            {
                Write-Warning "No ping event found within last 3 hours."
            }
            Write-Host
            Write-Host "Password sync channel status END ------------------------------------------------------- "
            Write-Host
        }
    }
    else
    {
        Write-Warning "More than one Azure AD Connectors found. Please update the script to use the appropriate Connector."
    }
}
Write-Host
if ($aadConnectors -eq $null)
{
    Write-Warning "No Azure AD Connector was found."
}
if ($adConnectors -eq $null)
{
    Write-Warning "No AD DS Connector was found."
}
Write-Host
```

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="ebbe9-295">Запуск полной синхронизации всех паролей</span><span class="sxs-lookup"><span data-stu-id="ebbe9-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="ebbe9-296">Запустите этот сценарий только один раз.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-296">Run this script only once.</span></span> <span data-ttu-id="ebbe9-297">Если одного раза мало, то это значит, что проблема в чем-то другом.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-297">If you need to run it more than once, something else is the problem.</span></span> <span data-ttu-id="ebbe9-298">Для устранения этой проблемы обратитесь в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="ebbe9-298">To troubleshoot the problem, contact Microsoft support.</span></span>

<span data-ttu-id="ebbe9-299">Полную синхронизацию всех паролей можно активировать с помощью следующего сценария:</span><span class="sxs-lookup"><span data-stu-id="ebbe9-299">You can trigger a full sync of all passwords by using the following script:</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"
$aadConnector = "<CASE SENSITIVE AAD CONNECTOR NAME>"
Import-Module adsync
$c = Get-ADSyncConnector -Name $adConnector
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1
$c.GlobalParameters.Remove($p.Name)
$c.GlobalParameters.Add($p)
$c = Add-ADSyncConnector -Connector $c
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $false
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $aadConnector -Enable $true
```

## <a name="next-steps"></a><span data-ttu-id="ebbe9-300">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ebbe9-300">Next steps</span></span>
* [<span data-ttu-id="ebbe9-301">Реализация синхронизации паролей с помощью службы Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="ebbe9-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="ebbe9-302">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="ebbe9-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="ebbe9-303">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ebbe9-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
