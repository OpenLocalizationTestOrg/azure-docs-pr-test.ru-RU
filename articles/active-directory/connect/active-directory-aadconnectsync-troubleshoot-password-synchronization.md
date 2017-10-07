---
title: "Синхронизация паролей aaaTroubleshoot с Azure AD Connect sync | Документы Microsoft"
description: "Эта статья содержит сведения о том, как tootroubleshoot проблем с синхронизацией паролей."
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
ms.openlocfilehash: 390eafec792cb39251627c14cb754f8bb30035b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-password-synchronization-with-azure-ad-connect-sync"></a><span data-ttu-id="64aa4-103">Устранение неполадок синхронизации паролей с помощью службы синхронизации Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="64aa4-103">Troubleshoot password synchronization with Azure AD Connect sync</span></span>
<span data-ttu-id="64aa4-104">В этом разделе шаги как tootroubleshoot проблемы с синхронизацией паролей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-104">This topic provides steps for how tootroubleshoot issues with password synchronization.</span></span> <span data-ttu-id="64aa4-105">Неполадки синхронизации паролей могут возникать либо в подмножестве пользователей, либо у всех.</span><span class="sxs-lookup"><span data-stu-id="64aa4-105">If passwords are not synchronizing as expected, it can be either for a subset of users or for all users.</span></span> <span data-ttu-id="64aa4-106">Для Azure Active Directory (Azure AD) подключения развертывания к версии 1.1.524.0 или более поздней версии, теперь есть командлет диагностики, которые можно использовать tootroubleshoot проблем синхронизации паролей:</span><span class="sxs-lookup"><span data-stu-id="64aa4-106">For Azure Active Directory (Azure AD) Connect deployment with version 1.1.524.0 or later, there is now a diagnostic cmdlet that you can use tootroubleshoot password synchronization issues:</span></span>

* <span data-ttu-id="64aa4-107">Если имеется проблема, где нет пароли синхронизируются, см. toohello [не пароли синхронизируются: Устранение неполадок с помощью командлета диагностики hello](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-107">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet](#no-passwords-are-synchronized-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

* <span data-ttu-id="64aa4-108">Если имеется проблема с отдельными объектами ссылаются toohello [одного объекта не выполняют синхронизацию паролей: Устранение неполадок с помощью командлета диагностики hello](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-108">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet](#one-object-is-not-synchronizing-passwords-troubleshoot-by-using-the-diagnostic-cmdlet) section.</span></span>

<span data-ttu-id="64aa4-109">Для ранних версий развертывания Azure AD Connect:</span><span class="sxs-lookup"><span data-stu-id="64aa4-109">For older versions of Azure AD Connect deployment:</span></span>

* <span data-ttu-id="64aa4-110">Если имеется проблема, где нет пароли синхронизируются, см. toohello [не пароли синхронизируются: вручную шаги по устранению неполадок](#no-passwords-are-synchronized-manual-troubleshooting-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-110">If you have an issue where no passwords are synchronized, refer toohello [No passwords are synchronized: manual troubleshooting steps](#no-passwords-are-synchronized-manual-troubleshooting-steps) section.</span></span>

* <span data-ttu-id="64aa4-111">Если имеется проблема с отдельными объектами ссылаются toohello [одного объекта не выполняют синхронизацию паролей: вручную шаги по устранению неполадок](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-111">If you have an issue with individual objects, refer toohello [One object is not synchronizing passwords: manual troubleshooting steps](#one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps) section.</span></span>

## <a name="no-passwords-are-synchronized-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="64aa4-112">Выполняется синхронизация паролей не: Устранение неполадок с помощью командлета диагностики hello</span><span class="sxs-lookup"><span data-stu-id="64aa4-112">No passwords are synchronized: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="64aa4-113">Можно использовать hello `Invoke-ADSyncDiagnostics` toofigure командлет out почему не пароли синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="64aa4-113">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toofigure out why no passwords are synchronized.</span></span>

> [!NOTE]
> <span data-ttu-id="64aa4-114">Hello `Invoke-ADSyncDiagnostics` командлет доступен только для Azure AD Connect версии 1.1.524.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="64aa4-114">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="64aa4-115">Запустите командлет диагностики hello</span><span class="sxs-lookup"><span data-stu-id="64aa4-115">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="64aa4-116">проблемы tootroubleshoot, где нет пароли синхронизируются:</span><span class="sxs-lookup"><span data-stu-id="64aa4-116">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="64aa4-117">Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с hello **Запуск от имени администратора** параметр.</span><span class="sxs-lookup"><span data-stu-id="64aa4-117">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="64aa4-118">Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="64aa4-118">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="64aa4-119">Запустите `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="64aa4-119">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="64aa4-120">Запустите `Invoke-ADSyncDiagnostics -PasswordSync`.</span><span class="sxs-lookup"><span data-stu-id="64aa4-120">Run `Invoke-ADSyncDiagnostics -PasswordSync`.</span></span>

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="64aa4-121">Изучите результаты hello hello командлета</span><span class="sxs-lookup"><span data-stu-id="64aa4-121">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="64aa4-122">Hello диагностики командлет выполняет следующие проверки hello:</span><span class="sxs-lookup"><span data-stu-id="64aa4-122">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="64aa4-123">Проверяет, hello включена функция синхронизации паролей для вашего клиента Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-123">Validates that hello password synchronization feature is enabled for your Azure AD tenant.</span></span>

* <span data-ttu-id="64aa4-124">Проверяет, hello Azure AD Connect, сервер не находится в промежуточный режим.</span><span class="sxs-lookup"><span data-stu-id="64aa4-124">Validates that hello Azure AD Connect server is not in staging mode.</span></span>

* <span data-ttu-id="64aa4-125">Для каждой существующей локальной Active Directory connector (которая соответствует tooan существующий лес Active Directory):</span><span class="sxs-lookup"><span data-stu-id="64aa4-125">For each existing on-premises Active Directory connector (which corresponds tooan existing Active Directory forest):</span></span>

   * <span data-ttu-id="64aa4-126">Проверяет, hello включена функция синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-126">Validates that hello password synchronization feature is enabled.</span></span>
   
   * <span data-ttu-id="64aa4-127">Выполняет поиск событий пульса синхронизации паролей в hello журналы событий приложений Windows.</span><span class="sxs-lookup"><span data-stu-id="64aa4-127">Searches for password synchronization heartbeat events in hello Windows Application Event logs.</span></span>

   * <span data-ttu-id="64aa4-128">Для каждого домена Active Directory под hello локальный Соединитель Active Directory:</span><span class="sxs-lookup"><span data-stu-id="64aa4-128">For each Active Directory domain under hello on-premises Active Directory connector:</span></span>

      * <span data-ttu-id="64aa4-129">Проверяет, hello домен доступен с сервера hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="64aa4-129">Validates that hello domain is reachable from hello Azure AD Connect server.</span></span>

      * <span data-ttu-id="64aa4-130">Проверяет наличие hello правильное имя пользователя, пароль и разрешения, необходимые для синхронизации паролей учетных записей доменных служб Active Directory (AD DS) hello, используемых hello локальный Соединитель Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64aa4-130">Validates that hello Active Directory Domain Services (AD DS) accounts used by hello on-premises Active Directory connector has hello correct username, password, and permissions required for password synchronization.</span></span>

<span data-ttu-id="64aa4-131">Привет, следующая схема иллюстрирует hello результаты командлета hello топологии одного домена в локальной среде Active Directory:</span><span class="sxs-lookup"><span data-stu-id="64aa4-131">hello following diagram illustrates hello results of hello cmdlet for a single-domain, on-premises Active Directory topology:</span></span>

![Диагностические выходные данные для синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalgeneral.png)

<span data-ttu-id="64aa4-133">Hello оставшейся части этого раздела описываются определенные результаты, возвращаемые командлетом hello и соответствующих проблем.</span><span class="sxs-lookup"><span data-stu-id="64aa4-133">hello rest of this section describes specific results that are returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="password-synchronization-feature-isnt-enabled"></a><span data-ttu-id="64aa4-134">Отключена функция синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="64aa4-134">Password synchronization feature isn't enabled</span></span>
<span data-ttu-id="64aa4-135">Если вы не включили синхронизации паролей с помощью мастера hello Azure AD Connect, возвращается hello следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="64aa4-135">If you haven't enabled password synchronization by using hello Azure AD Connect wizard, hello following error is returned:</span></span>

![Отключена функция синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobaldisabled.png)

#### <a name="azure-ad-connect-server-is-in-staging-mode"></a><span data-ttu-id="64aa4-137">Сервер Azure AD Connect находится в промежуточном режиме</span><span class="sxs-lookup"><span data-stu-id="64aa4-137">Azure AD Connect server is in staging mode</span></span>
<span data-ttu-id="64aa4-138">В случае сервера Azure AD Connect hello в промежуточный режим синхронизации паролей временно отключена и hello будет возвращена следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="64aa4-138">If hello Azure AD Connect server is in staging mode, password synchronization is temporarily disabled, and hello following error is returned:</span></span>

![Сервер Azure AD Connect находится в промежуточном режиме](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalstaging.png)

#### <a name="no-password-synchronization-heartbeat-events"></a><span data-ttu-id="64aa4-140">Отсутствуют события пульса синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="64aa4-140">No password synchronization heartbeat events</span></span>
<span data-ttu-id="64aa4-141">У каждого локального соединителя Active Directory есть свой собственный канал синхронизации паролей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-141">Each on-premises Active Directory connector has its own password synchronization channel.</span></span> <span data-ttu-id="64aa4-142">Если не синхронизировать изменения toobe любой пароль система устанавливается канал синхронизации пароля hello, событие пульса (EventId 654) создается один раз каждые 30 минут в журнале событий приложений Windows hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-142">When hello password synchronization channel is established and there aren't any password changes toobe synchronized, a heartbeat event (EventId 654) is generated once every 30 minutes under hello Windows Application Event Log.</span></span> <span data-ttu-id="64aa4-143">Для каждого локального соединителя Active Directory, hello командлет ищет соответствующие события пульса в hello последние три часа.</span><span class="sxs-lookup"><span data-stu-id="64aa4-143">For each on-premises Active Directory connector, hello cmdlet searches for corresponding heartbeat events in hello past three hours.</span></span> <span data-ttu-id="64aa4-144">Если событие пульса не найден, hello будет возвращена следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="64aa4-144">If no heartbeat event is found, hello following error is returned:</span></span>

![Отсутствует событие пульса синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalnoheartbeat.png)

#### <a name="ad-ds-account-does-not-have-correct-permissions"></a><span data-ttu-id="64aa4-146">Учетная запись AD DS не имеет необходимых разрешений</span><span class="sxs-lookup"><span data-stu-id="64aa4-146">AD DS account does not have correct permissions</span></span>
<span data-ttu-id="64aa4-147">Если учетная запись hello AD DS, используемый hello в локальной среде хэши паролей toosynchronize Соединитель Active Directory не имеет соответствующих разрешений hello hello будет возвращена следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="64aa4-147">If hello AD DS account that's used by hello on-premises Active Directory connector toosynchronize password hashes does not have hello appropriate permissions, hello following error is returned:</span></span>

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectpermission.png)

#### <a name="incorrect-ad-ds-account-username-or-password"></a><span data-ttu-id="64aa4-149">Неправильный пароль или имя пользователя учетной записи AD DS</span><span class="sxs-lookup"><span data-stu-id="64aa4-149">Incorrect AD DS account username or password</span></span>
<span data-ttu-id="64aa4-150">Если hello Доменных службах Active Directory учетная запись используется hello хэши паролей toosynchronize Соединитель Active Directory в локальной среде имеет неправильное имя пользователя или пароль, hello будет возвращена следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="64aa4-150">If hello AD DS account used by hello on-premises Active Directory connector toosynchronize password hashes has an incorrect username or password, hello following error is returned:</span></span>

![Неверные учетные данные](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phsglobalaccountincorrectcredential.png)

## <a name="one-object-is-not-synchronizing-passwords-troubleshoot-by-using-hello-diagnostic-cmdlet"></a><span data-ttu-id="64aa4-152">Один объект не выполняют синхронизацию паролей: Устранение неполадок с помощью командлета диагностики hello</span><span class="sxs-lookup"><span data-stu-id="64aa4-152">One object is not synchronizing passwords: troubleshoot by using hello diagnostic cmdlet</span></span>
<span data-ttu-id="64aa4-153">Можно использовать hello `Invoke-ADSyncDiagnostics` toodetermine командлета, почему один объект не выполняется синхронизация паролей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-153">You can use hello `Invoke-ADSyncDiagnostics` cmdlet toodetermine why one object is not synchronizing passwords.</span></span>

> [!NOTE]
> <span data-ttu-id="64aa4-154">Hello `Invoke-ADSyncDiagnostics` командлет доступен только для Azure AD Connect версии 1.1.524.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="64aa4-154">hello `Invoke-ADSyncDiagnostics` cmdlet is available only for Azure AD Connect version 1.1.524.0 or later.</span></span>

### <a name="run-hello-diagnostics-cmdlet"></a><span data-ttu-id="64aa4-155">Запустите командлет диагностики hello</span><span class="sxs-lookup"><span data-stu-id="64aa4-155">Run hello diagnostics cmdlet</span></span>
<span data-ttu-id="64aa4-156">проблемы tootroubleshoot, где нет пароли синхронизируются:</span><span class="sxs-lookup"><span data-stu-id="64aa4-156">tootroubleshoot issues where no passwords are synchronized:</span></span>

1. <span data-ttu-id="64aa4-157">Откройте новый сеанс Windows PowerShell на сервере Azure AD Connect с hello **Запуск от имени администратора** параметр.</span><span class="sxs-lookup"><span data-stu-id="64aa4-157">Open a new Windows PowerShell session on your Azure AD Connect server with hello **Run as Administrator** option.</span></span>

2. <span data-ttu-id="64aa4-158">Запустите `Set-ExecutionPolicy RemoteSigned` или `Set-ExecutionPolicy Unrestricted`.</span><span class="sxs-lookup"><span data-stu-id="64aa4-158">Run `Set-ExecutionPolicy RemoteSigned` or `Set-ExecutionPolicy Unrestricted`.</span></span>

3. <span data-ttu-id="64aa4-159">Запустите `Import-Module ADSyncDiagnostics`.</span><span class="sxs-lookup"><span data-stu-id="64aa4-159">Run `Import-Module ADSyncDiagnostics`.</span></span>

4. <span data-ttu-id="64aa4-160">Выполните следующий командлет hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-160">Run hello following cmdlet:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName <Name-of-AD-Connector> -DistinguishedName <DistinguishedName-of-AD-object>
   ```
   <span data-ttu-id="64aa4-161">Например:</span><span class="sxs-lookup"><span data-stu-id="64aa4-161">For example:</span></span>
   ```
   Invoke-ADSyncDiagnostics -PasswordSync -ADConnectorName "contoso.com" -DistinguishedName "CN=TestUserCN=Users,DC=contoso,DC=com"
   ```

### <a name="understand-hello-results-of-hello-cmdlet"></a><span data-ttu-id="64aa4-162">Изучите результаты hello hello командлета</span><span class="sxs-lookup"><span data-stu-id="64aa4-162">Understand hello results of hello cmdlet</span></span>
<span data-ttu-id="64aa4-163">Hello диагностики командлет выполняет следующие проверки hello:</span><span class="sxs-lookup"><span data-stu-id="64aa4-163">hello diagnostic cmdlet performs hello following checks:</span></span>

* <span data-ttu-id="64aa4-164">Проверяет состояние hello объекта Active Directory hello в пространство соединителя Active Directory hello, метавселенной и Azure AD пространством соединителя.</span><span class="sxs-lookup"><span data-stu-id="64aa4-164">Examines hello state of hello Active Directory object in hello Active Directory connector space, Metaverse, and Azure AD connector space.</span></span>

* <span data-ttu-id="64aa4-165">Проверяет, что отсутствуют правила синхронизации с синхронизацией паролей включен и применяется toohello объекта Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64aa4-165">Validates that there are synchronization rules with password synchronization enabled and applied toohello Active Directory object.</span></span>

* <span data-ttu-id="64aa4-166">Пытается tooretrieve и отображение результатов hello hello последней попытки toosynchronize hello пароля для hello объекта.</span><span class="sxs-lookup"><span data-stu-id="64aa4-166">Attempts tooretrieve and display hello results of hello last attempt toosynchronize hello password for hello object.</span></span>

<span data-ttu-id="64aa4-167">Привет, следующая схема иллюстрирует hello результаты командлета hello при устранении неполадок синхронизации паролей для одного объекта:</span><span class="sxs-lookup"><span data-stu-id="64aa4-167">hello following diagram illustrates hello results of hello cmdlet when troubleshooting password synchronization for a single object:</span></span>

![Диагностические выходные данные для синхронизации паролей для одного объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectgeneral.png)

<span data-ttu-id="64aa4-169">Hello оставшейся части этого раздела описываются определенных результатов, возвращаемых командлетом hello и соответствующих проблем.</span><span class="sxs-lookup"><span data-stu-id="64aa4-169">hello rest of this section describes specific results returned by hello cmdlet and corresponding issues.</span></span>

#### <a name="hello-active-directory-object-isnt-exported-tooazure-ad"></a><span data-ttu-id="64aa4-170">объект Active Directory Hello не экспортированного tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="64aa4-170">hello Active Directory object isn't exported tooAzure AD</span></span>
<span data-ttu-id="64aa4-171">Синхронизация паролей для этой учетной записи локальной службы каталогов Active Directory завершается ошибкой, так как отсутствует соответствующий объект в клиенте Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-171">Password synchronization for this on-premises Active Directory account fails because there is no corresponding object in hello Azure AD tenant.</span></span> <span data-ttu-id="64aa4-172">возвращается следующая ошибка Hello:</span><span class="sxs-lookup"><span data-stu-id="64aa4-172">hello following error is returned:</span></span>

![Отсутствует объект Azure AD](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnotexported.png)

#### <a name="user-has-a-temporary-password"></a><span data-ttu-id="64aa4-174">У пользователя временный пароль</span><span class="sxs-lookup"><span data-stu-id="64aa4-174">User has a temporary password</span></span>
<span data-ttu-id="64aa4-175">В настоящее время Azure AD Connect не поддерживает синхронизацию временных паролей с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-175">Currently, Azure AD Connect does not support synchronizing temporary passwords with Azure AD.</span></span> <span data-ttu-id="64aa4-176">Пароль считается toobe временные Если hello **смену пароля при следующем входе в систему** был установлен на hello локального пользователя Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64aa4-176">A password is considered toobe temporary if hello **Change password at next logon** option is set on hello on-premises Active Directory user.</span></span> <span data-ttu-id="64aa4-177">возвращается следующая ошибка Hello:</span><span class="sxs-lookup"><span data-stu-id="64aa4-177">hello following error is returned:</span></span>

![Временный пароль не экспортируется](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjecttemporarypassword.png)

#### <a name="results-of-last-attempt-toosynchronize-password-arent-available"></a><span data-ttu-id="64aa4-179">Результаты выполнения последней попытки toosynchronize пароль недоступны</span><span class="sxs-lookup"><span data-stu-id="64aa4-179">Results of last attempt toosynchronize password aren't available</span></span>
<span data-ttu-id="64aa4-180">По умолчанию Azure AD Connect сохраняются результаты hello попыток синхронизации паролей на семь дней.</span><span class="sxs-lookup"><span data-stu-id="64aa4-180">By default, Azure AD Connect stores hello results of password synchronization attempts for seven days.</span></span> <span data-ttu-id="64aa4-181">Если нет результатов для выбранного hello объекта Active Directory, возвращается hello следующие предупреждения:</span><span class="sxs-lookup"><span data-stu-id="64aa4-181">If there are no results available for hello selected Active Directory object, hello following warning is returned:</span></span>

![Диагностические выходные данные для одного объекта: отсутствует история синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/phssingleobjectnohistory.png)


## <a name="no-passwords-are-synchronized-manual-troubleshooting-steps"></a><span data-ttu-id="64aa4-183">Пароли не синхронизируются: шаги по устранению неполадок вручную</span><span class="sxs-lookup"><span data-stu-id="64aa4-183">No passwords are synchronized: manual troubleshooting steps</span></span>
<span data-ttu-id="64aa4-184">Выполните эти шаги toodetermine, почему не пароли синхронизируются.</span><span class="sxs-lookup"><span data-stu-id="64aa4-184">Follow these steps toodetermine why no passwords are synchronized:</span></span>

1. <span data-ttu-id="64aa4-185">— Сервер Connect hello в [промежуточный режим](active-directory-aadconnectsync-operations.md#staging-mode)?</span><span class="sxs-lookup"><span data-stu-id="64aa4-185">Is hello Connect server in [staging mode](active-directory-aadconnectsync-operations.md#staging-mode)?</span></span> <span data-ttu-id="64aa4-186">Сервер, находящийся в промежуточном режиме, не синхронизирует пароли.</span><span class="sxs-lookup"><span data-stu-id="64aa4-186">A server in staging mode does not synchronize any passwords.</span></span>

2. <span data-ttu-id="64aa4-187">Выполнение скрипта hello hello [получить состояние hello синхронизации паролей](#get-the-status-of-password-sync-settings) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-187">Run hello script in hello [Get hello status of password sync settings](#get-the-status-of-password-sync-settings) section.</span></span> <span data-ttu-id="64aa4-188">Он предоставляет общие сведения о конфигурации синхронизации пароля hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-188">It gives you an overview of hello password sync configuration.</span></span>  

    ![Выходные данные сценария PowerShell из параметров синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/psverifyconfig.png)  

3. <span data-ttu-id="64aa4-190">Если функция hello не включена в Azure AD или состояние канала синхронизации hello не включена, запустите мастер установки Connect hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-190">If hello feature is not enabled in Azure AD or if hello sync channel status is not enabled, run hello Connect installation wizard.</span></span> <span data-ttu-id="64aa4-191">Выберите **Настроить параметры синхронизации** и снимите флажок синхронизации паролей. Это изменение временно отключает функцию «hello».</span><span class="sxs-lookup"><span data-stu-id="64aa4-191">Select **Customize synchronization options**, and unselect password sync. This change temporarily disables hello feature.</span></span> <span data-ttu-id="64aa4-192">Затем снова запустите мастер hello и повторное включение синхронизации паролей. Запустите сценарий hello снова tooverify, hello конфигурации указано правильно.</span><span class="sxs-lookup"><span data-stu-id="64aa4-192">Then run hello wizard again and re-enable password sync. Run hello script again tooverify that hello configuration is correct.</span></span>

4. <span data-ttu-id="64aa4-193">Просмотрите журнал ошибок hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-193">Look in hello event log for errors.</span></span> <span data-ttu-id="64aa4-194">Найдите следующие события, указывающие на проблему hello:</span><span class="sxs-lookup"><span data-stu-id="64aa4-194">Look for hello following events, which would indicate a problem:</span></span>
    * <span data-ttu-id="64aa4-195">Источник: "Directory synchronization" ID: 0, 611, 652, 655. Если вы видите эти события, то это свидетельствует о проблеме с подключением.</span><span class="sxs-lookup"><span data-stu-id="64aa4-195">Source: "Directory synchronization" ID: 0, 611, 652, 655 If you see these events, you have a connectivity problem.</span></span> <span data-ttu-id="64aa4-196">сообщения журнала событий Hello содержит сведения лесу, где возникла проблема.</span><span class="sxs-lookup"><span data-stu-id="64aa4-196">hello event log message contains forest information where you have a problem.</span></span> <span data-ttu-id="64aa4-197">Дополнительные сведения см. в разделе о [проблеме с подключением](#connectivity problem).</span><span class="sxs-lookup"><span data-stu-id="64aa4-197">For more information, see [Connectivity problem](#connectivity problem).</span></span>

5. <span data-ttu-id="64aa4-198">Если нет пульса или не сработали другие методы, то [запустите полную синхронизацию всех паролей](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="64aa4-198">If you see no heartbeat or if nothing else worked, run [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span> <span data-ttu-id="64aa4-199">Запустите сценарий hello только один раз.</span><span class="sxs-lookup"><span data-stu-id="64aa4-199">Run hello script only once.</span></span>

6. <span data-ttu-id="64aa4-200">В разделе hello [Устранение один объект, который не выполняют синхронизацию паролей](#one-object-is-not-synchronizing-passwords) раздела.</span><span class="sxs-lookup"><span data-stu-id="64aa4-200">See hello [Troubleshoot one object that is not synchronizing passwords](#one-object-is-not-synchronizing-passwords) section.</span></span>

### <a name="connectivity-problems"></a><span data-ttu-id="64aa4-201">Проблемы с подключением</span><span class="sxs-lookup"><span data-stu-id="64aa4-201">Connectivity problems</span></span>

<span data-ttu-id="64aa4-202">Проверьте, есть ли подключение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-202">Do you have connectivity with Azure AD?</span></span>

<span data-ttu-id="64aa4-203">Требуется хэши паролей hello tooread разрешения во всех доменах hello учетная запись?</span><span class="sxs-lookup"><span data-stu-id="64aa4-203">Does hello account have required permissions tooread hello password hashes in all domains?</span></span> <span data-ttu-id="64aa4-204">Если вы установили подключение с помощью экспресс-параметры, разрешения hello уже должен быть правильно.</span><span class="sxs-lookup"><span data-stu-id="64aa4-204">If you installed Connect by using Express settings, hello permissions should already be correct.</span></span> 

<span data-ttu-id="64aa4-205">Если вы использовали выборочную установку, разрешения hello вручную, выполнив hello ниже:</span><span class="sxs-lookup"><span data-stu-id="64aa4-205">If you used custom installation, set hello permissions manually by doing hello following:</span></span>
    
1. <span data-ttu-id="64aa4-206">hello toofind учетная запись, используемая службой соединителя Active Directory hello, start **диспетчер службы синхронизации**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-206">toofind hello account used by hello Active Directory connector, start **Synchronization Service Manager**.</span></span> 
 
2. <span data-ttu-id="64aa4-207">Go слишком**соединители**и выполните поиск в лесу Active Directory локальной hello, устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="64aa4-207">Go too**Connectors**, and then search for hello on-premises Active Directory forest you are troubleshooting.</span></span> 
 
3. <span data-ttu-id="64aa4-208">Выберите соединитель hello и нажмите кнопку **свойства**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-208">Select hello connector, and then click **Properties**.</span></span> 
 
4. <span data-ttu-id="64aa4-209">Go слишком**подключения леса tooActive**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-209">Go too**Connect tooActive Directory Forest**.</span></span>  
    
    ![Учетная запись, используемая соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/connectoraccount.png)  
    <span data-ttu-id="64aa4-211">Обратите внимание, hello имя пользователя и домен hello, где расположена учетная запись hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-211">Note hello username and hello domain where hello account is located.</span></span>
    
5. <span data-ttu-id="64aa4-212">Запуск **Active Directory — пользователи и компьютеры**и убедитесь, что учетная запись hello, найденные ранее имеет разрешения выполните hello в корне hello всех доменов в лесу:</span><span class="sxs-lookup"><span data-stu-id="64aa4-212">Start **Active Directory Users and Computers**, and then verify that hello account you found earlier has hello follow permissions set at hello root of all domains in your forest:</span></span>
    * <span data-ttu-id="64aa4-213">Репликация изменений каталога</span><span class="sxs-lookup"><span data-stu-id="64aa4-213">Replicate Directory Changes</span></span>
    * <span data-ttu-id="64aa4-214">Репликация всех изменений каталога</span><span class="sxs-lookup"><span data-stu-id="64aa4-214">Replicate Directory Changes All</span></span>

6. <span data-ttu-id="64aa4-215">Являются hello контроллерами домена, которые доступны для Azure AD Connect?</span><span class="sxs-lookup"><span data-stu-id="64aa4-215">Are hello domain controllers reachable by Azure AD Connect?</span></span> <span data-ttu-id="64aa4-216">Если подключение сервера hello не может подключаться tooall контроллеров домена, настройте **использовать предпочтительный контроллер домена только**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-216">If hello Connect server cannot connect tooall domain controllers, configure **Only use preferred domain controller**.</span></span>  
    
    ![Контроллер домена, используемый соединителем Active Directory](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/preferreddc.png)  
    
7. <span data-ttu-id="64aa4-218">Возврат слишком**Synchronization Service Manager** и **Настройка раздела каталога**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-218">Go back too**Synchronization Service Manager** and **Configure Directory Partition**.</span></span> 
 
8. <span data-ttu-id="64aa4-219">Выберите домен в **выберите разделы каталога**выберите hello **использовать только контроллеры домена предпочтительный** флажок и нажмите кнопку **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-219">Select your domain in **Select directory partitions**, select hello **Only use preferred domain controllers** check box, and then click **Configure**.</span></span> 

9. <span data-ttu-id="64aa4-220">В списке hello введите hello контроллеры домена, подключение следует использовать для синхронизации паролей. Hello один список используется для импорта и экспорта также.</span><span class="sxs-lookup"><span data-stu-id="64aa4-220">In hello list, enter hello domain controllers that Connect should use for password sync. hello same list is used for import and export as well.</span></span> <span data-ttu-id="64aa4-221">Выполните эти действия для всех доменов.</span><span class="sxs-lookup"><span data-stu-id="64aa4-221">Do these steps for all your domains.</span></span>

10. <span data-ttu-id="64aa4-222">Если hello сценарий показывает, что не пакетов пульса, выполните сценарий hello в [запуска полной синхронизации всех паролей](#trigger-a-full-sync-of-all-passwords).</span><span class="sxs-lookup"><span data-stu-id="64aa4-222">If hello script shows that there is no heartbeat, run hello script in [Trigger a full sync of all passwords](#trigger-a-full-sync-of-all-passwords).</span></span>

## <a name="one-object-is-not-synchronizing-passwords-manual-troubleshooting-steps"></a><span data-ttu-id="64aa4-223">Пароли не синхронизируются одним объектом: шаги по устранению неполадок вручную</span><span class="sxs-lookup"><span data-stu-id="64aa4-223">One object is not synchronizing passwords: manual troubleshooting steps</span></span>
<span data-ttu-id="64aa4-224">Можно легко устранения неполадок синхронизации паролей, проверив состояние hello объекта.</span><span class="sxs-lookup"><span data-stu-id="64aa4-224">You can easily troubleshoot password synchronization issues by reviewing hello status of an object.</span></span>

1. <span data-ttu-id="64aa4-225">В **Active Directory — пользователи и компьютеры**, поиск пользователя hello и убедитесь, что hello **пользователь должен сменить пароль при следующем входе в систему** флажок снят.</span><span class="sxs-lookup"><span data-stu-id="64aa4-225">In **Active Directory Users and Computers**, search for hello user, and then verify that hello **User must change password at next logon** check box is cleared.</span></span>  

    ![Повышение производительности в Active Directory с помощью синхронизации паролей](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/adprodpassword.png)  

    <span data-ttu-id="64aa4-227">Если установлен флажок "hello", попросите toosign пользователя hello в и смену пароля hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-227">If hello check box is selected, ask hello user toosign in and change hello password.</span></span> <span data-ttu-id="64aa4-228">Временные пароли не синхронизируются с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-228">Temporary passwords are not synchronized with Azure AD.</span></span>

2. <span data-ttu-id="64aa4-229">Если пароль hello верны в Active Directory, выполните пользователя hello в модуль синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-229">If hello password looks correct in Active Directory, follow hello user in hello sync engine.</span></span> <span data-ttu-id="64aa4-230">Следующие hello пользователя из локальной Active Directory tooAzure AD вы увидите, имеются ли описательное сообщение об ошибке hello объекта.</span><span class="sxs-lookup"><span data-stu-id="64aa4-230">By following hello user from on-premises Active Directory tooAzure AD, you can see whether there is a descriptive error on hello object.</span></span>

    <span data-ttu-id="64aa4-231">а.</span><span class="sxs-lookup"><span data-stu-id="64aa4-231">a.</span></span> <span data-ttu-id="64aa4-232">Запуск hello [диспетчер службы синхронизации](active-directory-aadconnectsync-service-manager-ui.md).</span><span class="sxs-lookup"><span data-stu-id="64aa4-232">Start hello [Synchronization Service Manager](active-directory-aadconnectsync-service-manager-ui.md).</span></span>

    <span data-ttu-id="64aa4-233">b.</span><span class="sxs-lookup"><span data-stu-id="64aa4-233">b.</span></span> <span data-ttu-id="64aa4-234">Щелкните **Соединители**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-234">Click **Connectors**.</span></span>

    <span data-ttu-id="64aa4-235">c.</span><span class="sxs-lookup"><span data-stu-id="64aa4-235">c.</span></span> <span data-ttu-id="64aa4-236">Выберите hello **Соединитель Active Directory** где находится пользователь hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-236">Select hello **Active Directory Connector** where hello user is located.</span></span>

    <span data-ttu-id="64aa4-237">d.</span><span class="sxs-lookup"><span data-stu-id="64aa4-237">d.</span></span> <span data-ttu-id="64aa4-238">Выберите **Search Connector Space**(Поиск пространства соединителя).</span><span class="sxs-lookup"><span data-stu-id="64aa4-238">Select **Search Connector Space**.</span></span>

    <span data-ttu-id="64aa4-239">д.</span><span class="sxs-lookup"><span data-stu-id="64aa4-239">e.</span></span> <span data-ttu-id="64aa4-240">В hello **область** выберите **DN или привязки**и введите полное имя DN hello пользователя hello, устранении неполадок.</span><span class="sxs-lookup"><span data-stu-id="64aa4-240">In hello **Scope** box, select **DN or Anchor**, and then enter hello full DN of hello user you are troubleshooting.</span></span>

    ![Поиск пользователя в пространстве соединителя с различающимся именем](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/searchcs.png)  

    <span data-ttu-id="64aa4-242">f.</span><span class="sxs-lookup"><span data-stu-id="64aa4-242">f.</span></span> <span data-ttu-id="64aa4-243">Найдите hello пользователя ищете и нажмите кнопку **свойства** toosee все hello атрибуты.</span><span class="sxs-lookup"><span data-stu-id="64aa4-243">Locate hello user you are looking for, and then click **Properties** toosee all hello attributes.</span></span> <span data-ttu-id="64aa4-244">Если пользователь hello не hello результат поиска, проверьте вашей [правила фильтрации](active-directory-aadconnectsync-configure-filtering.md) и убедитесь, что запускается [применить и проверка изменений](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) для tooappear пользователя hello в соединение.</span><span class="sxs-lookup"><span data-stu-id="64aa4-244">If hello user is not in hello search result, verify your [filtering rules](active-directory-aadconnectsync-configure-filtering.md) and make sure that you run [Apply and verify changes](active-directory-aadconnectsync-configure-filtering.md#apply-and-verify-changes) for hello user tooappear in Connect.</span></span>

    <span data-ttu-id="64aa4-245">ж.</span><span class="sxs-lookup"><span data-stu-id="64aa4-245">g.</span></span> <span data-ttu-id="64aa4-246">щелкните последнюю неделю toosee пароль hello синхронизации сведений hello объекта для hello **журнала**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-246">toosee hello password sync details of hello object for hello past week, click **Log**.</span></span>  

    ![Сведения журнала для объекта](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/csobjectlog.png)  

    <span data-ttu-id="64aa4-248">Если журнал hello объекта пуст, Azure AD Connect был хэш пароля невозможно tooread hello из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64aa4-248">If hello object log is empty, Azure AD Connect has been unable tooread hello password hash from Active Directory.</span></span> <span data-ttu-id="64aa4-249">Перейдите к устранению неполадок, описанных в разделе [Проблема подключения](#connectivity-errors).</span><span class="sxs-lookup"><span data-stu-id="64aa4-249">Continue your troubleshooting with [Connectivity Errors](#connectivity-errors).</span></span> <span data-ttu-id="64aa4-250">Если вы видите любое другое значение, чем **успех**, см. таблицу toohello в [журнал синхронизации паролей](#password-sync-log).</span><span class="sxs-lookup"><span data-stu-id="64aa4-250">If you see any other value than **success**, refer toohello table in [Password sync log](#password-sync-log).</span></span>

    <span data-ttu-id="64aa4-251">h.</span><span class="sxs-lookup"><span data-stu-id="64aa4-251">h.</span></span> <span data-ttu-id="64aa4-252">Выберите hello **журнала обращений и преобразований** вкладку и убедитесь, что это правило синхронизации по крайней мере один в hello **PasswordSync** столбец **True**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-252">Select hello **lineage** tab, and make sure that at least one sync rule in hello **PasswordSync** column is **True**.</span></span> <span data-ttu-id="64aa4-253">В конфигурации по умолчанию hello hello правило синхронизации hello называется **в из AD — User AccountEnabled**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-253">In hello default configuration, hello name of hello sync rule is **In from AD - User AccountEnabled**.</span></span>  

    ![Сведения о пользователе в журнале обращений и преобразований](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync.png)  

    <span data-ttu-id="64aa4-255">i.</span><span class="sxs-lookup"><span data-stu-id="64aa4-255">i.</span></span> <span data-ttu-id="64aa4-256">Нажмите кнопку **свойства объекта метавселенной** toodisplay список атрибутов пользователей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-256">Click **Metaverse Object Properties** toodisplay a list of user attributes.</span></span>  

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvpasswordsync.png)  

    <span data-ttu-id="64aa4-258">Атрибут **cloudFiltered** должен отсутствовать.</span><span class="sxs-lookup"><span data-stu-id="64aa4-258">Verify that there is no **cloudFiltered** attribute present.</span></span> <span data-ttu-id="64aa4-259">Убедитесь, что атрибуты домена hello (domainFQDN и domainNetBios) hello ожидаемые значения.</span><span class="sxs-lookup"><span data-stu-id="64aa4-259">Make sure that hello domain attributes (domainFQDN and domainNetBios) have hello expected values.</span></span>

    <span data-ttu-id="64aa4-260">j.</span><span class="sxs-lookup"><span data-stu-id="64aa4-260">j.</span></span> <span data-ttu-id="64aa4-261">Нажмите кнопку hello **соединители** вкладки. Убедитесь, что вы видите tooboth соединители локальной Active Directory и Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-261">Click hello **Connectors** tab. Make sure that you see connectors tooboth on-premises Active Directory and Azure AD.</span></span>

    ![Сведения метавселенной](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/mvconnectors.png)  

    <span data-ttu-id="64aa4-263">k.</span><span class="sxs-lookup"><span data-stu-id="64aa4-263">k.</span></span> <span data-ttu-id="64aa4-264">Выберите hello строку, представляющую Azure AD щелкните **свойства**и нажмите кнопку hello **журнала обращений и преобразований** объект пространства соединителя hello вкладку должны иметь исходящего правила в hello **PasswordSync** столбец установлен слишком**True**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-264">Select hello row that represents Azure AD, click **Properties**, and then click hello **Lineage** tab. hello connector space object should have an outbound rule in hello **PasswordSync** column set too**True**.</span></span> <span data-ttu-id="64aa4-265">В конфигурации по умолчанию hello hello правило синхронизации hello называется **Out tooAAD - User Join**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-265">In hello default configuration, hello name of hello sync rule is **Out tooAAD - User Join**.</span></span>  

    ![Диалоговое окно свойств объекта пространства соединителя](./media/active-directory-aadconnectsync-troubleshoot-password-synchronization/cspasswordsync2.png)  

### <a name="password-sync-log"></a><span data-ttu-id="64aa4-267">Журнал синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="64aa4-267">Password sync log</span></span>
<span data-ttu-id="64aa4-268">Hello Status может содержать hello следующие значения:</span><span class="sxs-lookup"><span data-stu-id="64aa4-268">hello status column can have hello following values:</span></span>

| <span data-ttu-id="64aa4-269">Состояние</span><span class="sxs-lookup"><span data-stu-id="64aa4-269">Status</span></span> | <span data-ttu-id="64aa4-270">Description (Описание)</span><span class="sxs-lookup"><span data-stu-id="64aa4-270">Description</span></span> |
| --- | --- |
| <span data-ttu-id="64aa4-271">Успешно</span><span class="sxs-lookup"><span data-stu-id="64aa4-271">Success</span></span> |<span data-ttu-id="64aa4-272">Пароль успешно синхронизирован</span><span class="sxs-lookup"><span data-stu-id="64aa4-272">Password has been successfully synchronized.</span></span> |
| <span data-ttu-id="64aa4-273">FilteredByTarget</span><span class="sxs-lookup"><span data-stu-id="64aa4-273">FilteredByTarget</span></span> |<span data-ttu-id="64aa4-274">Задать пароль слишком**пользователь должен сменить пароль при следующем входе в систему**.</span><span class="sxs-lookup"><span data-stu-id="64aa4-274">Password is set too**User must change password at next logon**.</span></span> <span data-ttu-id="64aa4-275">Пароль не синхронизирован.</span><span class="sxs-lookup"><span data-stu-id="64aa4-275">Password has not been synchronized.</span></span> |
| <span data-ttu-id="64aa4-276">NoTargetConnection</span><span class="sxs-lookup"><span data-stu-id="64aa4-276">NoTargetConnection</span></span> |<span data-ttu-id="64aa4-277">Ни один из объектов в метавселенной hello или в пространство соединителя hello Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-277">No object in hello metaverse or in hello Azure AD connector space.</span></span> |
| <span data-ttu-id="64aa4-278">SourceConnectorNotPresent</span><span class="sxs-lookup"><span data-stu-id="64aa4-278">SourceConnectorNotPresent</span></span> |<span data-ttu-id="64aa4-279">Объект не найден в пространство соединителя hello в локальной среде Active Directory.</span><span class="sxs-lookup"><span data-stu-id="64aa4-279">No object found in hello on-premises Active Directory connector space.</span></span> |
| <span data-ttu-id="64aa4-280">TargetNotExportedToDirectory</span><span class="sxs-lookup"><span data-stu-id="64aa4-280">TargetNotExportedToDirectory</span></span> |<span data-ttu-id="64aa4-281">Hello объекта в hello пространство соединителя Azure AD не экспортированы.</span><span class="sxs-lookup"><span data-stu-id="64aa4-281">hello object in hello Azure AD connector space has not yet been exported.</span></span> |
| <span data-ttu-id="64aa4-282">MigratedCheckDetailsForMoreInfo</span><span class="sxs-lookup"><span data-stu-id="64aa4-282">MigratedCheckDetailsForMoreInfo</span></span> |<span data-ttu-id="64aa4-283">Запись журнала создана до выхода версии 1.0.9125.0 и отображается в исходном состоянии.</span><span class="sxs-lookup"><span data-stu-id="64aa4-283">Log entry was created before build 1.0.9125.0 and is shown in its legacy state.</span></span> |
| <span data-ttu-id="64aa4-284">Ошибка</span><span class="sxs-lookup"><span data-stu-id="64aa4-284">Error</span></span> |<span data-ttu-id="64aa4-285">Служба вернула неизвестную ошибку.</span><span class="sxs-lookup"><span data-stu-id="64aa4-285">Service returned an unknown error.</span></span> |
| <span data-ttu-id="64aa4-286">Unknown</span><span class="sxs-lookup"><span data-stu-id="64aa4-286">Unknown</span></span> |<span data-ttu-id="64aa4-287">Произошла ошибка при попытке tooprocess пакет хэши паролей.</span><span class="sxs-lookup"><span data-stu-id="64aa4-287">An error occurred while trying tooprocess a batch of password hashes.</span></span>  |
| <span data-ttu-id="64aa4-288">MissingAttribute</span><span class="sxs-lookup"><span data-stu-id="64aa4-288">MissingAttribute</span></span> |<span data-ttu-id="64aa4-289">Недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-289">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services are not available.</span></span> |
| <span data-ttu-id="64aa4-290">RetryRequestedByTarget</span><span class="sxs-lookup"><span data-stu-id="64aa4-290">RetryRequestedByTarget</span></span> |<span data-ttu-id="64aa4-291">Ранее были недоступны определенные атрибуты (например, хэш Kerberos), необходимые доменным службам Azure AD.</span><span class="sxs-lookup"><span data-stu-id="64aa4-291">Specific attributes (for example, Kerberos hash) required by Azure AD Domain Services were not available previously.</span></span> <span data-ttu-id="64aa4-292">Выполняется попытка tooresynchronize hello хэш пароля пользователя.</span><span class="sxs-lookup"><span data-stu-id="64aa4-292">An attempt tooresynchronize hello user's password hash is made.</span></span> |

## <a name="scripts-toohelp-troubleshooting"></a><span data-ttu-id="64aa4-293">Устранение неполадок toohelp сценариев</span><span class="sxs-lookup"><span data-stu-id="64aa4-293">Scripts toohelp troubleshooting</span></span>

### <a name="get-hello-status-of-password-sync-settings"></a><span data-ttu-id="64aa4-294">Получить состояние hello синхронизации паролей</span><span class="sxs-lookup"><span data-stu-id="64aa4-294">Get hello status of password sync settings</span></span>
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
        Write-Warning "More than one Azure AD Connectors found. Please update hello script toouse hello appropriate Connector."
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

#### <a name="trigger-a-full-sync-of-all-passwords"></a><span data-ttu-id="64aa4-295">Запуск полной синхронизации всех паролей</span><span class="sxs-lookup"><span data-stu-id="64aa4-295">Trigger a full sync of all passwords</span></span>
> [!NOTE]
> <span data-ttu-id="64aa4-296">Запустите этот сценарий только один раз.</span><span class="sxs-lookup"><span data-stu-id="64aa4-296">Run this script only once.</span></span> <span data-ttu-id="64aa4-297">Если вам требуется toorun его несколько раз, либо является проблема hello.</span><span class="sxs-lookup"><span data-stu-id="64aa4-297">If you need toorun it more than once, something else is hello problem.</span></span> <span data-ttu-id="64aa4-298">tootroubleshoot hello проблему, обратитесь в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="64aa4-298">tootroubleshoot hello problem, contact Microsoft support.</span></span>

<span data-ttu-id="64aa4-299">Полная синхронизация всех паролей можно запускать с помощью hello следующий скрипт:</span><span class="sxs-lookup"><span data-stu-id="64aa4-299">You can trigger a full sync of all passwords by using hello following script:</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="64aa4-300">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="64aa4-300">Next steps</span></span>
* [<span data-ttu-id="64aa4-301">Реализация синхронизации паролей с помощью службы Azure AD Connect Sync</span><span class="sxs-lookup"><span data-stu-id="64aa4-301">Implementing password synchronization with Azure AD Connect sync</span></span>](active-directory-aadconnectsync-implement-password-synchronization.md)
* [<span data-ttu-id="64aa4-302">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="64aa4-302">Azure AD Connect Sync: Customizing synchronization options</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="64aa4-303">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="64aa4-303">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)
