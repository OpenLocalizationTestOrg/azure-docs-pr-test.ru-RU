---
title: "Синхронизация Azure AD Connect: изменение учетной записи службы синхронизации подключения hello Azure AD | Документы Microsoft"
description: "В этом разделе документе описываются hello ключ шифрования, а как tooabandon его после hello пароль изменен."
services: active-directory
keywords: "учетная запись службы синхронизации Azure AD, пароль"
documentationcenter: 
author: cychua
manager: femila
editor: 
ms.assetid: 76b19162-8b16-4960-9e22-bd64e6675ecc
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 11948ac4662f722e4f684ef6c9b9ccdc6387e60f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="changing-hello-azure-ad-connect-sync-service-account-password"></a><span data-ttu-id="c15c9-104">Изменение пароля учетной записи службы синхронизации Azure AD Connect hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-104">Changing hello Azure AD Connect sync service account password</span></span>
<span data-ttu-id="c15c9-105">При изменении пароля учетной записи службы синхронизации Azure AD Connect hello hello службы синхронизации будут начала может неверно до прервана hello ключ шифрования и пароль учетной записи службы синхронизации Azure AD Connect hello повторной инициализации.</span><span class="sxs-lookup"><span data-stu-id="c15c9-105">If you change hello  Azure AD Connect sync service account password, hello Synchronization Service will not be able start correctly until you have abandoned hello encryption key and reinitialized hello Azure AD Connect sync service account password.</span></span> 

<span data-ttu-id="c15c9-106">Azure AD Connect, как часть hello служб синхронизации использует шифрование ключа toostore hello пароли hello AD DS и учетные записи служб Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-106">Azure AD Connect, as part of hello Synchronization Services uses an encryption key toostore hello passwords of hello AD DS and Azure AD service accounts.</span></span>  <span data-ttu-id="c15c9-107">Эти учетные записи, шифруются перед сохранением в базе данных hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-107">These accounts are encrypted before they are stored in hello database.</span></span> 

<span data-ttu-id="c15c9-108">Hello ключ шифрования, используемый защищается с помощью [защиты данных Windows (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span><span class="sxs-lookup"><span data-stu-id="c15c9-108">hello encryption key used is secured using [Windows Data Protection (DPAPI)](https://msdn.microsoft.com/library/ms995355.aspx).</span></span> <span data-ttu-id="c15c9-109">DPAPI защищает ключ шифрования hello, с помощью hello **пароль учетной записи службы hello Azure AD Connect sync**.</span><span class="sxs-lookup"><span data-stu-id="c15c9-109">DPAPI protects hello encryption key using hello **password of hello Azure AD Connect sync service account**.</span></span> 

<span data-ttu-id="c15c9-110">Если вам требуется пароль учетной записи службы hello toochange можно использовать процедуры hello в [ключ шифрования Abandoning hello Azure AD Sync подключения](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish это.</span><span class="sxs-lookup"><span data-stu-id="c15c9-110">If you need toochange hello service account password you can use hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) tooaccomplish this.</span></span>  <span data-ttu-id="c15c9-111">Эти процедуры также следует использовать, если требуется ключ шифрования hello tooabandon по любой причине.</span><span class="sxs-lookup"><span data-stu-id="c15c9-111">These procedures should also be used if you need tooabandon hello encryption key for any reason.</span></span>

##<a name="issues-that-arise-from-changing-hello-password"></a><span data-ttu-id="c15c9-112">Проблемы, которые возникают вследствие изменения пароля hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-112">Issues that arise from changing hello password</span></span>
<span data-ttu-id="c15c9-113">Есть две вещи, которые должны производиться при изменении пароля учетной записи службы hello toobe.</span><span class="sxs-lookup"><span data-stu-id="c15c9-113">There are two things that need toobe done when you change hello service account password.</span></span>

<span data-ttu-id="c15c9-114">Во-первых необходимо в диспетчер управления службами Windows hello пароль toochange hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-114">First, you need toochange hello password under hello Windows Service Control Manager.</span></span>  <span data-ttu-id="c15c9-115">Пока вы не устраните эту проблему, будут появляться следующие ошибки.</span><span class="sxs-lookup"><span data-stu-id="c15c9-115">Until this issue is resolved you will see following errors:</span></span>


- <span data-ttu-id="c15c9-116">При попытке hello toostart службы синхронизации в диспетчере управления службами Windows, возникает ошибка hello»**Windows не удалось запустить службу Microsoft Azure AD Sync hello на локальном компьютере**».</span><span class="sxs-lookup"><span data-stu-id="c15c9-116">If you try toostart hello Synchronization Service in Windows Service Control Manager, you receive hello error "**Windows could not start hello Microsoft Azure AD Sync service on Local Computer**".</span></span> <span data-ttu-id="c15c9-117">**Ошибка 1069: hello не запустилась из-за ошибки tooa входа в систему.** "</span><span class="sxs-lookup"><span data-stu-id="c15c9-117">**Error 1069: hello service did not start due tooa logon failure.**"</span></span>
- <span data-ttu-id="c15c9-118">В области просмотра событий Windows журнал системных событий hello содержит ошибку с **7038 идентификатор события** и сообщение «**hello службы ADSync было невозможно toolog на как и в настоящее время настроен hello пароль из-за следующих toohello ошибка: Hello имя пользователя или пароль неправильный.** "</span><span class="sxs-lookup"><span data-stu-id="c15c9-118">Under Windows Event Viewer, hello system event log contains an error with **Event ID 7038** and message “**hello ADSync service was unable toolog on as with hello currently configured password due toohello following error: hello user name or password is incorrect.**"</span></span>

<span data-ttu-id="c15c9-119">Во-вторых при определенных условиях, при обновлении пароля hello hello служба синхронизации больше не можем извлечь ключ шифрования hello посредством DPAPI.</span><span class="sxs-lookup"><span data-stu-id="c15c9-119">Second, under specific conditions, if hello password is updated, hello Synchronization Service can no longer retrieve hello encryption key via DPAPI.</span></span> <span data-ttu-id="c15c9-120">Без ключа шифрования hello приветствия служба синхронизации не удается расшифровать hello toosynchronize необходимые пароли из локальной AD и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-120">Without hello encryption key, hello Synchronization Service cannot decrypt hello passwords required toosynchronize to/from on-premises AD and Azure AD.</span></span>
<span data-ttu-id="c15c9-121">Вы этом случае вы увидите такие ошибки.</span><span class="sxs-lookup"><span data-stu-id="c15c9-121">You will see errors such as:</span></span>

- <span data-ttu-id="c15c9-122">В разделе диспетчера управления службами, если при toostart hello службы синхронизации, не удалось получить ключ шифрования hello, он завершается с ошибкой «** hello Microsoft Azure AD Sync не удается запустить Windows на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="c15c9-122">Under Windows Service Control Manager, if you try toostart hello Synchronization Service and it cannot retrieve hello encryption key, it fails with error “**Windows could not start hello Microsoft Azure AD Sync on Local Computer.</span></span> <span data-ttu-id="c15c9-123">Дополнительные сведения просмотрите журнал событий системы hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-123">For more information, review hello System Event log.</span></span> <span data-ttu-id="c15c9-124">Если это служба не корпорации Майкрософт, обратитесь к поставщику службы hello и см. код ошибки tooservice **-21451857952 ***.»</span><span class="sxs-lookup"><span data-stu-id="c15c9-124">If this is a non-Microsoft service, contact hello service vendor, and refer tooservice-specific error code **-21451857952****.”</span></span>
- <span data-ttu-id="c15c9-125">В средстве просмотра событий Windows, журнал событий приложения hello содержит ошибку с **6028 идентификатор события** и сообщение об ошибке *»**ключа шифрования сервера hello невозможен.* *»*</span><span class="sxs-lookup"><span data-stu-id="c15c9-125">Under Windows Event Viewer, hello application event log contains an error with **Event ID 6028** and error message *“**hello server encryption key cannot be accessed.**”*</span></span>

<span data-ttu-id="c15c9-126">tooensure, не получают эти ошибки, выполните процедуры hello в [ключ шифрования Abandoning hello Azure AD Sync подключения](#abandoning-the-azure-ad-connect-sync-encryption-key) при изменении пароля hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-126">tooensure that you do not receive these errors, follow hello procedures in [Abandoning hello Azure AD Connect Sync encryption key](#abandoning-the-azure-ad-connect-sync-encryption-key) when changing hello password.</span></span>
 
## <a name="abandoning-hello-azure-ad-connect-sync-encryption-key"></a><span data-ttu-id="c15c9-127">Ключ шифрования подключения службу синхронизации Azure AD прерывающее hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-127">Abandoning hello Azure AD Connect Sync encryption key</span></span>
>[!IMPORTANT]
><span data-ttu-id="c15c9-128">Hello следующие процедуры применяются только tooAzure AD Connect сборки 1.1.443.0 или более ранних версий.</span><span class="sxs-lookup"><span data-stu-id="c15c9-128">hello following procedures only apply tooAzure AD Connect build 1.1.443.0 or older.</span></span>

<span data-ttu-id="c15c9-129">Используйте следующий ключ шифрования hello tooabandon процедуры hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-129">Use hello following procedures tooabandon hello encryption key.</span></span>

### <a name="what-toodo-if-you-need-tooabandon-hello-encryption-key"></a><span data-ttu-id="c15c9-130">Какие toodo, если требуется ключ шифрования tooabandon hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-130">What toodo if you need tooabandon hello encryption key</span></span>

<span data-ttu-id="c15c9-131">Если требуется ключ шифрования hello tooabandon используйте следующие процедуры tooaccomplish hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-131">If you need tooabandon hello encryption key, use hello following procedures tooaccomplish this.</span></span>

1. [<span data-ttu-id="c15c9-132">Прервать hello существующий ключ шифрования</span><span class="sxs-lookup"><span data-stu-id="c15c9-132">Abandon hello existing encryption key</span></span>](#abandon-the-existing-encryption-key)

2. [<span data-ttu-id="c15c9-133">Указывать пароль учетной записи hello hello учетной записи службы AD DS</span><span class="sxs-lookup"><span data-stu-id="c15c9-133">Provide hello password of hello AD DS account</span></span>](#provide-the-password-of-the-ad-ds-account)

3. [<span data-ttu-id="c15c9-134">Повторная инициализация hello пароль учетной записи Azure AD sync hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-134">Reinitialize hello password of hello Azure AD sync account</span></span>](#reinitialize-the-password-of-the-azure-ad-sync-account)

4. [<span data-ttu-id="c15c9-135">Запуск службы синхронизации hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-135">Start hello Synchronization Service</span></span>](#start-the-synchronization-service)

#### <a name="abandon-hello-existing-encryption-key"></a><span data-ttu-id="c15c9-136">Прервать hello существующий ключ шифрования</span><span class="sxs-lookup"><span data-stu-id="c15c9-136">Abandon hello existing encryption key</span></span>
<span data-ttu-id="c15c9-137">Отказаться от hello существующий ключ шифрования, поэтому могут создаваться этого нового ключа шифрования:</span><span class="sxs-lookup"><span data-stu-id="c15c9-137">Abandon hello existing encryption key so that new encryption key can be created:</span></span>

1. <span data-ttu-id="c15c9-138">Войдите в систему tooyour подключения сервера Azure AD как администратор.</span><span class="sxs-lookup"><span data-stu-id="c15c9-138">Log in tooyour Azure AD Connect Server as administrator.</span></span>

2. <span data-ttu-id="c15c9-139">Запустите сеанс PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c15c9-139">Start a new PowerShell session.</span></span>

3. <span data-ttu-id="c15c9-140">Найдите toofolder:`$env:Program Files\Microsoft Azure AD Sync\bin\`</span><span class="sxs-lookup"><span data-stu-id="c15c9-140">Navigate toofolder: `$env:Program Files\Microsoft Azure AD Sync\bin\`</span></span>

4. <span data-ttu-id="c15c9-141">Выполните команду hello.`./miiskmu.exe /a`</span><span class="sxs-lookup"><span data-stu-id="c15c9-141">Run hello command: `./miiskmu.exe /a`</span></span>

![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key5.png)

#### <a name="provide-hello-password-of-hello-ad-ds-account"></a><span data-ttu-id="c15c9-143">Указывать пароль учетной записи hello hello учетной записи службы AD DS</span><span class="sxs-lookup"><span data-stu-id="c15c9-143">Provide hello password of hello AD DS account</span></span>
<span data-ttu-id="c15c9-144">Как больше не могут быть расшифрованы hello существующие пароли, хранящийся в базе данных hello, необходимо tooprovide hello служба синхронизации с hello пароль учетной записи hello AD DS.</span><span class="sxs-lookup"><span data-stu-id="c15c9-144">As hello existing passwords stored inside hello database can no longer be decrypted, you need tooprovide hello Synchronization Service with hello password of hello AD DS account.</span></span> <span data-ttu-id="c15c9-145">Служба синхронизации Hello шифрует hello пароли, с помощью нового ключа шифрования hello:</span><span class="sxs-lookup"><span data-stu-id="c15c9-145">hello Synchronization Service encrypts hello passwords using hello new encryption key:</span></span>

1. <span data-ttu-id="c15c9-146">Запустите hello Synchronization Service Manager (служба → НАЧАЛА синхронизации).</span><span class="sxs-lookup"><span data-stu-id="c15c9-146">Start hello Synchronization Service Manager (START → Synchronization Service).</span></span>
</br><span data-ttu-id="c15c9-147">![Synchronization Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span><span class="sxs-lookup"><span data-stu-id="c15c9-147">![Sync Service Manager](./media/active-directory-aadconnectsync-service-manager-ui/startmenu.png)</span></span>  
2. <span data-ttu-id="c15c9-148">Go toohello **соединители** вкладки.</span><span class="sxs-lookup"><span data-stu-id="c15c9-148">Go toohello **Connectors** tab.</span></span>
3. <span data-ttu-id="c15c9-149">Выберите hello **соединителя AD** , соответствующий tooyour локальной AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-149">Select hello **AD Connector** that corresponds tooyour on-premises AD.</span></span> <span data-ttu-id="c15c9-150">При наличии более одного соединителя AD, повторите указанные действия для каждого из них hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-150">If you have more than one AD connector, repeat hello following steps for each of them.</span></span>
4. <span data-ttu-id="c15c9-151">В разделе **Действия** выберите **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="c15c9-151">Under **Actions**, select **Properties**.</span></span>
5. <span data-ttu-id="c15c9-152">В всплывающем диалоговом окне приветствия выберите **подключения леса tooActive**:</span><span class="sxs-lookup"><span data-stu-id="c15c9-152">In hello pop-up dialog, select **Connect tooActive Directory Forest**:</span></span>
6. <span data-ttu-id="c15c9-153">Введите пароль hello учетной записи hello AD DS в hello **пароль** текстового поля.</span><span class="sxs-lookup"><span data-stu-id="c15c9-153">Enter hello password of hello AD DS account in hello **Password** textbox.</span></span> <span data-ttu-id="c15c9-154">Если вы не знаете пароль, необходимо задать tooa известно значение перед выполнением этого шага.</span><span class="sxs-lookup"><span data-stu-id="c15c9-154">If you do not know its password, you must set it tooa known value before performing this step.</span></span>
7. <span data-ttu-id="c15c9-155">Нажмите кнопку **ОК** toosave hello новый пароль и закрыть hello всплывающем диалоговом окне.</span><span class="sxs-lookup"><span data-stu-id="c15c9-155">Click **OK** toosave hello new password and close hello pop-up dialog.</span></span>
<span data-ttu-id="c15c9-156">![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key6.png)</span><span class="sxs-lookup"><span data-stu-id="c15c9-156">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key6.png)</span></span>

#### <a name="reinitialize-hello-password-of-hello-azure-ad-sync-account"></a><span data-ttu-id="c15c9-157">Повторная инициализация hello пароль учетной записи Azure AD sync hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-157">Reinitialize hello password of hello Azure AD sync account</span></span>
<span data-ttu-id="c15c9-158">Нельзя напрямую предоставить hello пароль учетной записи службы toohello службы синхронизации для hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-158">You cannot directly provide hello password of hello Azure AD service account toohello Synchronization Service.</span></span> <span data-ttu-id="c15c9-159">Вместо этого необходим командлет hello toouse **ADSyncAADServiceAccount добавить** tooreinitialize hello учетной записи службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-159">Instead, you need toouse hello cmdlet **Add-ADSyncAADServiceAccount** tooreinitialize hello Azure AD service account.</span></span> <span data-ttu-id="c15c9-160">Hello командлет сбрасывает пароль учетной записи hello и делает доступными toohello служба синхронизации:</span><span class="sxs-lookup"><span data-stu-id="c15c9-160">hello cmdlet resets hello account password and makes it available toohello Synchronization Service:</span></span>

1. <span data-ttu-id="c15c9-161">Запустите новый сеанс PowerShell на сервере hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="c15c9-161">Start a new PowerShell session on hello Azure AD Connect server.</span></span>
2. <span data-ttu-id="c15c9-162">Выполните командлет `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="c15c9-162">Run cmdlet `Add-ADSyncAADServiceAccount`.</span></span>
3. <span data-ttu-id="c15c9-163">В диалоговом окне всплывающих hello учетные данные hello Azure AD глобального администратора для вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c15c9-163">In hello pop-up dialog, provide hello Azure AD Global admin credentials for your Azure AD tenant.</span></span>
<span data-ttu-id="c15c9-164">![Служебная программа для ключа шифрования в службе синхронизации Azure AD Connect](media/active-directory-aadconnectsync-encryption-key/key7.png)</span><span class="sxs-lookup"><span data-stu-id="c15c9-164">![Azure AD Connect Sync Encryption Key Utility](media/active-directory-aadconnectsync-encryption-key/key7.png)</span></span>
4. <span data-ttu-id="c15c9-165">Если успешна, вы увидите командную строку PowerShell hello.</span><span class="sxs-lookup"><span data-stu-id="c15c9-165">If it is successful, you will see hello PowerShell command prompt.</span></span>

#### <a name="start-hello-synchronization-service"></a><span data-ttu-id="c15c9-166">Запуск службы синхронизации hello</span><span class="sxs-lookup"><span data-stu-id="c15c9-166">Start hello Synchronization Service</span></span>
<span data-ttu-id="c15c9-167">Теперь, когда hello служба синхронизации имеет ключ шифрования toohello доступа и все hello пароли ему, можно перезапустить службу hello в диспетчер управления службами Windows hello:</span><span class="sxs-lookup"><span data-stu-id="c15c9-167">Now that hello Synchronization Service has access toohello encryption key and all hello passwords it needs, you can restart hello service in hello Windows Service Control Manager:</span></span>


1. <span data-ttu-id="c15c9-168">Go tooWindows диспетчера управления службами (Пуск → службы).</span><span class="sxs-lookup"><span data-stu-id="c15c9-168">Go tooWindows Service Control Manager (START → Services).</span></span>
2. <span data-ttu-id="c15c9-169">Выберите **службу синхронизации Microsoft Azure AD** и нажмите кнопку "Перезапустить".</span><span class="sxs-lookup"><span data-stu-id="c15c9-169">Select **Microsoft Azure AD Sync** and click Restart.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c15c9-170">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c15c9-170">Next steps</span></span>
<span data-ttu-id="c15c9-171">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="c15c9-171">**Overview topics**</span></span>

* [<span data-ttu-id="c15c9-172">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="c15c9-172">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)

* [<span data-ttu-id="c15c9-173">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c15c9-173">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
