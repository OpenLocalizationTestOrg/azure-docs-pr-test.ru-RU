---
title: "Часто задаваемые вопросы по Azure Active Directory Connect | Документация Майкрософт"
description: "На этой странице изложены часто задаваемые вопросы об Azure AD Connect."
services: active-directory
documentationcenter: 
author: billmath
manager: femila
ms.assetid: 4e47a087-ebcd-4b63-9574-0c31907a39a3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: billmath
ms.openlocfilehash: 39c0b127d3dcf6f45607ad8b4647a9ad79dfc732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="d8ca2-103">Часто задаваемые вопросы по Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="d8ca2-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="d8ca2-104">Общая установка</span><span class="sxs-lookup"><span data-stu-id="d8ca2-104">General installation</span></span>
<span data-ttu-id="d8ca2-105">**Вопрос установки работает, если hello Azure AD глобального администратора имеет 2FA включено?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-105">**Q: Will installation work if hello Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="d8ca2-106">Со сборками hello с февраля 2016 г. Эта функция поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-106">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="d8ca2-107">**Вопрос. есть ли способ tooinstall автоматической Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-107">**Q: Is there a way tooinstall Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="d8ca2-108">Это только поддерживаемые tooinstall Azure AD Connect с помощью мастера установки hello.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-108">It is only supported tooinstall Azure AD Connect using hello installation wizard.</span></span> <span data-ttu-id="d8ca2-109">Автоматическая и "тихая" установка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="d8ca2-110">**Вопрос. В лесу есть один домен, с которым нельзя связаться. Как я могу установить Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="d8ca2-111">Со сборками hello с февраля 2016 г. Эта функция поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-111">With hello builds from February 2016, this is supported.</span></span>

<span data-ttu-id="d8ca2-112">**Вопрос выполняет hello AD DS работу агента работоспособности на server core?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-112">**Q: Does hello AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="d8ca2-113">Да.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-113">Yes.</span></span> <span data-ttu-id="d8ca2-114">После установки агента hello, необходимо выполнить процесс регистрации hello, используя hello, выполнив командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-114">After installing hello agent, you can complete hello registration process using hello following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="d8ca2-115">Сеть</span><span class="sxs-lookup"><span data-stu-id="d8ca2-115">Network</span></span>
<span data-ttu-id="d8ca2-116">**Вопрос. у меня брандмауэр, сетевое устройство или то, что ограничивает максимальное время подключения hello может оставаться открытым в моей сети. Каким должно быть пороговое значение времени ожидания на стороне клиента при использовании Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-116">**Q: I have a firewall, network device, or something else that limits hello maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="d8ca2-117">Все сетевое программное обеспечение, физических устройств или все, что ограничения соединения могут оставаться открытым hello максимальное время следует использовать пороговое значение хотя бы 5 минут (300 секунд) для связи между hello сервера, где hello Azure AD Connect установки клиента и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-117">All networking software, physical devices, or anything else that limits hello maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between hello server where hello Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="d8ca2-118">Это также касается средства синхронизации Microsoft Identity tooall ранее были выпущены.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-118">This also applies tooall previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="d8ca2-119">**Вопрос. Поддерживаются ли одноуровневые домены (SLD)?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="d8ca2-120">Нет. Azure AD Connect не поддерживает локальные леса и домены, использующие SLD.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="d8ca2-121">**Вопрос. Поддерживаются ли имена NetBIOS "с точками"?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="d8ca2-122">"Нет", "Azure AD Connect не поддерживает локального леса и домены где hello NetBIOS-имя содержит точку «.» в имени hello.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-122">No, Azure AD Connect does not support on-premises forests/domains where hello NetBios name contains a period "." in hello name.</span></span>

## <a name="federation"></a><span data-ttu-id="d8ca2-123">Федерация</span><span class="sxs-lookup"><span data-stu-id="d8ca2-123">Federation</span></span>
<span data-ttu-id="d8ca2-124">**Вопрос. что делать, если я получаю сообщение электронной почты, спрашивать меня toorenew сертификатов Office 365**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-124">**Q: What do I do if I receive an email that asking me toorenew my Office 365 certificate**</span></span>  
<span data-ttu-id="d8ca2-125">С помощью руководства по hello, описанных в hello [обновить сертификаты](active-directory-aadconnect-o365-certs.md) раздела справки по как toorenew hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-125">Use hello guidance that is outlined in hello [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how toorenew hello certificate.</span></span>

<span data-ttu-id="d8ca2-126">**Вопрос. У меня задан параметр "Automatically update relying party" (Автоматически обновлять проверяющую сторону) для проверяющей стороны Office 365. Нужно ли tootake какие-либо действия при перейдет my автоматически сертификат для подписи маркера?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have tootake any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="d8ca2-127">С помощью руководства по hello, описанные в статье hello [обновить сертификаты](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="d8ca2-127">Use hello guidance that is outlined in hello article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="d8ca2-128">Среда</span><span class="sxs-lookup"><span data-stu-id="d8ca2-128">Environment</span></span>
<span data-ttu-id="d8ca2-129">**Вопрос. есть ИТ поддерживается toorename hello server после установки Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-129">**Q: Is it supported toorename hello server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="d8ca2-130">Нет.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-130">No.</span></span> <span data-ttu-id="d8ca2-131">Изменение имени сервера hello toonot механизм синхронизации hello причина будет базы данных SQL может tooconnect toohello и hello службы не будет возможности toostart.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-131">Changing hello server name will cause hello sync engine toonot be able tooconnect toohello SQL database and hello service will not be able toostart.</span></span>

## <a name="identity-data"></a><span data-ttu-id="d8ca2-132">Данные удостоверений</span><span class="sxs-lookup"><span data-stu-id="d8ca2-132">Identity data</span></span>
<span data-ttu-id="d8ca2-133">**Вопрос атрибут имени участника-пользователя (userPrincipalName) hello в Azure AD не соответствует hello локального имени участника-пользователя — почему?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-133">**Q: hello UPN (userPrincipalName) attribute in Azure AD does not match hello on-prem UPN - why?**</span></span>  
<span data-ttu-id="d8ca2-134">См. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="d8ca2-134">See these articles:</span></span>

* [<span data-ttu-id="d8ca2-135">Имена пользователей не совпадают в Office 365, Azure или Intune hello локального имени участника-пользователя или альтернативному имени пользователя</span><span class="sxs-lookup"><span data-stu-id="d8ca2-135">User names in Office 365, Azure, or Intune don't match hello on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="d8ca2-136">Изменения не синхронизированы hello средство синхронизации Azure Active Directory после изменения hello UPN toouse учетной записи пользователя другой федеративный домен</span><span class="sxs-lookup"><span data-stu-id="d8ca2-136">Changes aren't synced by hello Azure Active Directory Sync tool after you change hello UPN of a user account toouse a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="d8ca2-137">Можно также настроить Azure AD tooallow hello синхронизации ядра tooupdate hello userPrincipalName, как описано в [функции службы синхронизации Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="d8ca2-137">You can also configure Azure AD tooallow hello sync engine tooupdate hello userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="d8ca2-138">**Вопрос. есть ИТ поддерживается toosoft соответствия локальных объектов AD группы или контакта с существующими объектами Azure AD группы или контакта?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-138">**Q: Is it supported toosoft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="d8ca2-139">Нет, в настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-139">No, this is currently not supported.</span></span>

<span data-ttu-id="d8ca2-140">**Вопрос. есть toomanually ИТ поддерживается атрибуту ImmutableId на существующего Azure AD группы или контакта toohard объекты соответствующим образом tooon локальные объекты "Контакт" / группы AD?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-140">**Q: Is it supported toomanually set ImmutableId attribute on existing Azure AD Group/Contact objects toohard match it tooon-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="d8ca2-141">Нет, в настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="d8ca2-142">Настраиваемая конфигурация</span><span class="sxs-lookup"><span data-stu-id="d8ca2-142">Custom configuration</span></span>
<span data-ttu-id="d8ca2-143">**Вопрос. где являются hello командлеты PowerShell для Azure AD Connect задокументированы?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-143">**Q: Where are hello PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="d8ca2-144">За исключением hello hello командлетов, описанных на этом сайте другие командлеты PowerShell в Azure AD Connect не поддерживается для пользователей.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-144">With hello exception of hello cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="d8ca2-145">**Вопрос. можно ли использовать сервер или сервер экспорта «Импорт» в *Synchronization Service Manager* toomove конфигурации между серверами?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* toomove configuration between servers?**</span></span>  
<span data-ttu-id="d8ca2-146">Нет.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-146">No.</span></span> <span data-ttu-id="d8ca2-147">Этот параметр не получает все параметры конфигурации; его использование не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="d8ca2-148">Вместо этого следует использовать приветствия мастера toocreate hello базовой конфигурации на втором сервере hello и использовать любое настраиваемое правило, между серверами hello редактор правил синхронизации toogenerate toomove сценариев PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-148">You should instead use hello wizard toocreate hello base configuration on hello second server and use hello sync rule editor toogenerate PowerShell scripts toomove any custom rule between servers.</span></span> <span data-ttu-id="d8ca2-149">Дополнительные сведения см. в разделе [Обновление со сменой сервера](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="d8ca2-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="d8ca2-150">**Вопрос. можно кэшировать пароли для hello Azure вход страницы и можно это не так как в нем элемент ввода пароля с помощью автозаполнения hello = «false» атрибут?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-150">**Q: Can passwords be cached for hello Azure sign-in page and can this be prevented since it contains a password input element with hello autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="d8ca2-151">Изменение атрибутов HTML hello hello пароль поля ввода, включая hello автозаполнения тег в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-151">We currently do not support modifying hello HTML attributes of hello Password input field, including hello autocomplete tag.</span></span> <span data-ttu-id="d8ca2-152">Настоящий момент мы работаем на функцию, которая позволит пользовательским кодом Javascript, которая допускает tooadd любое поле атрибута toohello пароль.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-152">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="d8ca2-153">Она должна быть доступна к концу 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="d8ca2-154">**Вопрос на hello Azure на странице входа отображаются имена пользователей для пользователей, которые ранее успешного входа.  Можно ли отключить эту функцию?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-154">**Q: On hello Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="d8ca2-155">Изменение атрибутов hello HTML страницы входа hello в настоящее время не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-155">We currently do not support modifying hello HTML attributes of hello sign-in page.</span></span> <span data-ttu-id="d8ca2-156">Настоящий момент мы работаем на функцию, которая позволит пользовательским кодом Javascript, которая допускает tooadd любое поле атрибута toohello пароль.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-156">We are currently working on a feature that will allow for custom Javascript which will allow you tooadd any attribute toohello password field.</span></span> <span data-ttu-id="d8ca2-157">Она должна быть доступна к концу 2017 года.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="d8ca2-158">**Вопрос. есть ли способ tooprevent одновременных сеансов?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-158">**Q: Is there a way tooprevent concurrent sessions?**</span></span></br>
<span data-ttu-id="d8ca2-159">Нет.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="d8ca2-160">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="d8ca2-160">Troubleshooting</span></span>
<span data-ttu-id="d8ca2-161">**Вопрос. Как получить справку по Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="d8ca2-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="d8ca2-162">Поиск hello базы знаний Майкрософт (KB)</span><span class="sxs-lookup"><span data-stu-id="d8ca2-162">Search hello Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="d8ca2-163">Поиск hello базы знаний Майкрософт (KB) для технические решения toocommon устранения неполадок о поддержке Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-163">Search hello Microsoft Knowledge Base (KB) for technical solutions toocommon break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="d8ca2-164">Форумы по Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d8ca2-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="d8ca2-165">Можно выполнять поиск и просмотр для технические вопросы и ответы от сообщества hello или задать собственный вопрос, щелкнув [здесь](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span><span class="sxs-lookup"><span data-stu-id="d8ca2-165">You can search and browse for technical questions and answers from hello community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="d8ca2-166">Служба поддержки клиентов Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="d8ca2-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="d8ca2-167">Использование этой поддержки tooget связь через портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d8ca2-167">Use this link tooget support through hello Azure portal.</span></span>

