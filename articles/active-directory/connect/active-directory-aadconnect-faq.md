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
ms.openlocfilehash: fd5988b2d4170166902bb5cc39603d4a0f83be59
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="frequently-asked-questions-for-azure-active-directory-connect"></a><span data-ttu-id="279eb-103">Часто задаваемые вопросы по Azure Active Directory Connect</span><span class="sxs-lookup"><span data-stu-id="279eb-103">Frequently asked questions for Azure Active Directory Connect</span></span>

## <a name="general-installation"></a><span data-ttu-id="279eb-104">Общая установка</span><span class="sxs-lookup"><span data-stu-id="279eb-104">General installation</span></span>
<span data-ttu-id="279eb-105">**Вопрос. Будет ли установка выполнена корректно, если глобальный администратор Azure AD включил 2FA?**</span><span class="sxs-lookup"><span data-stu-id="279eb-105">**Q: Will installation work if the Azure AD Global Admin has 2FA enabled?**</span></span>  
<span data-ttu-id="279eb-106">Это поддерживается в сборках от февраля 2016 года.</span><span class="sxs-lookup"><span data-stu-id="279eb-106">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="279eb-107">**Вопрос. Есть ли способ автоматической установки Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-107">**Q: Is there a way to install Azure AD Connect unattended?**</span></span>  
<span data-ttu-id="279eb-108">Установка Azure AD Connect может быть выполнена только с помощью мастера установки.</span><span class="sxs-lookup"><span data-stu-id="279eb-108">It is only supported to install Azure AD Connect using the installation wizard.</span></span> <span data-ttu-id="279eb-109">Автоматическая и "тихая" установка не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="279eb-109">An unattended and silent installation is not supported.</span></span>

<span data-ttu-id="279eb-110">**Вопрос. В лесу есть один домен, с которым нельзя связаться. Как я могу установить Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-110">**Q: I have a forest where one domain cannot be contacted. How do I install Azure AD Connect?**</span></span>  
<span data-ttu-id="279eb-111">Это поддерживается в сборках от февраля 2016 года.</span><span class="sxs-lookup"><span data-stu-id="279eb-111">With the builds from February 2016, this is supported.</span></span>

<span data-ttu-id="279eb-112">**Вопрос. Работает ли агент работоспособности AD DS на основных серверных компонентах?**</span><span class="sxs-lookup"><span data-stu-id="279eb-112">**Q: Does the AD DS health agent work on server core?**</span></span>  
<span data-ttu-id="279eb-113">Да.</span><span class="sxs-lookup"><span data-stu-id="279eb-113">Yes.</span></span> <span data-ttu-id="279eb-114">После установки агента можно выполнить регистрацию, используя следующий командлет PowerShell.</span><span class="sxs-lookup"><span data-stu-id="279eb-114">After installing the agent, you can complete the registration process using the following PowerShell cmdlet:</span></span> 

`Register-AzureADConnectHealthADDSAgent -Credentials $cred`

## <a name="network"></a><span data-ttu-id="279eb-115">Сеть</span><span class="sxs-lookup"><span data-stu-id="279eb-115">Network</span></span>
<span data-ttu-id="279eb-116">**Вопрос. У меня есть брандмауэр, сетевое устройство или иное средство, ограничивающее максимальное время, в течение которого подключения могут оставаться открытыми в моей сети. Каким должно быть пороговое значение времени ожидания на стороне клиента при использовании Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-116">**Q: I have a firewall, network device, or something else that limits the maximum time connections can stay open on my network. How long should my client side timeout threshold be when using Azure AD Connect?**</span></span>  
<span data-ttu-id="279eb-117">Всему сетевому программному обеспечению, физическим устройствам или прочим средствам, ограничивающим максимальное время, в течение которого подключение может оставаться открытым, следует использовать пороговое значение в 5 минут (300 секунд) для подключений между сервером, на который установлен клиент Azure AD Connect, и Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="279eb-117">All networking software, physical devices, or anything else that limits the maximum time connections can remain open should use a threshold of at least 5 minutes (300 seconds) for connectivity between the server where the Azure AD Connect client is installed and Azure Active Directory.</span></span> <span data-ttu-id="279eb-118">Это также относится ко всем ранее выпущенным инструментам синхронизации Microsoft Identity.</span><span class="sxs-lookup"><span data-stu-id="279eb-118">This also applies to all previously released Microsoft Identity synchronization tools.</span></span>

<span data-ttu-id="279eb-119">**Вопрос. Поддерживаются ли одноуровневые домены (SLD)?**</span><span class="sxs-lookup"><span data-stu-id="279eb-119">**Q: Are SLDs (Single Label Domains) supported?**</span></span>  
<span data-ttu-id="279eb-120">Нет. Azure AD Connect не поддерживает локальные леса и домены, использующие SLD.</span><span class="sxs-lookup"><span data-stu-id="279eb-120">No, Azure AD Connect does not support on-premises forests/domains using SLDs.</span></span>

<span data-ttu-id="279eb-121">**Вопрос. Поддерживаются ли имена NetBIOS "с точками"?**</span><span class="sxs-lookup"><span data-stu-id="279eb-121">**Q: Are "dotted" NetBios named supported?**</span></span>  
<span data-ttu-id="279eb-122">Нет. Azure AD Connect не поддерживает локальные леса и домены, имя NetBIOS которых содержит точку (".").</span><span class="sxs-lookup"><span data-stu-id="279eb-122">No, Azure AD Connect does not support on-premises forests/domains where the NetBios name contains a period "." in the name.</span></span>

## <a name="federation"></a><span data-ttu-id="279eb-123">Федерация</span><span class="sxs-lookup"><span data-stu-id="279eb-123">Federation</span></span>
<span data-ttu-id="279eb-124">**Вопрос. Что делать, если мне на электронную почту пришло сообщение с требованием продлить срок действия сертификата Office 365?**</span><span class="sxs-lookup"><span data-stu-id="279eb-124">**Q: What do I do if I receive an email that asking me to renew my Office 365 certificate**</span></span>  
<span data-ttu-id="279eb-125">Используйте инструкции, описанные в статье [Обновление сертификатов федерации для Office 365 и Azure AD](active-directory-aadconnect-o365-certs.md) .</span><span class="sxs-lookup"><span data-stu-id="279eb-125">Use the guidance that is outlined in the [renew certificates](active-directory-aadconnect-o365-certs.md) topic on how to renew the certificate.</span></span>

<span data-ttu-id="279eb-126">**Вопрос. У меня задан параметр "Automatically update relying party" (Автоматически обновлять проверяющую сторону) для проверяющей стороны Office 365. Потребуется выполнить ли какое-либо действие при автоматической смене сертификата для подписи маркера?**</span><span class="sxs-lookup"><span data-stu-id="279eb-126">**Q: I have "Automatically update relying party" set for O365 relying party. Do I have to take any action when my token signing certificate automatically rolls over?**</span></span>  
<span data-ttu-id="279eb-127">Используйте инструкции, приведенные в статье [Обновление сертификатов федерации для Office 365 и Azure AD](active-directory-aadconnect-o365-certs.md).</span><span class="sxs-lookup"><span data-stu-id="279eb-127">Use the guidance that is outlined in the article [renew certificates](active-directory-aadconnect-o365-certs.md).</span></span>

## <a name="environment"></a><span data-ttu-id="279eb-128">Среда</span><span class="sxs-lookup"><span data-stu-id="279eb-128">Environment</span></span>
<span data-ttu-id="279eb-129">**Вопрос. Поддерживается ли переименование сервера после установки Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-129">**Q: Is it supported to rename the server after Azure AD Connect has been installed?**</span></span>  
<span data-ttu-id="279eb-130">Нет.</span><span class="sxs-lookup"><span data-stu-id="279eb-130">No.</span></span> <span data-ttu-id="279eb-131">Изменение имени сервера приведет к тому, что обработчик синхронизации не сможет подключиться к базе данных SQL и служба не запустится.</span><span class="sxs-lookup"><span data-stu-id="279eb-131">Changing the server name will cause the sync engine to not be able to connect to the SQL database and the service will not be able to start.</span></span>

## <a name="identity-data"></a><span data-ttu-id="279eb-132">Данные удостоверений</span><span class="sxs-lookup"><span data-stu-id="279eb-132">Identity data</span></span>
<span data-ttu-id="279eb-133">**Вопрос. Атрибут имени участника-пользователя (userPrincipalName) в Azure AD не совпадает с локальным именем участника. Почему?**</span><span class="sxs-lookup"><span data-stu-id="279eb-133">**Q: The UPN (userPrincipalName) attribute in Azure AD does not match the on-prem UPN - why?**</span></span>  
<span data-ttu-id="279eb-134">См. следующие статьи:</span><span class="sxs-lookup"><span data-stu-id="279eb-134">See these articles:</span></span>

* [<span data-ttu-id="279eb-135">Имена пользователей в Office 365, Azure или Intune не совпадают с локальным именем участника-пользователя или альтернативным именем для входа</span><span class="sxs-lookup"><span data-stu-id="279eb-135">User names in Office 365, Azure, or Intune don't match the on-premises UPN or alternate login ID</span></span>](https://support.microsoft.com/en-us/kb/2523192)
* [<span data-ttu-id="279eb-136">Изменения не синхронизируются с помощью инструмента синхронизации Azure Active Directory после изменения имени участника-пользователя или учетной записи пользователя для использования другого федеративного домена</span><span class="sxs-lookup"><span data-stu-id="279eb-136">Changes aren't synced by the Azure Active Directory Sync tool after you change the UPN of a user account to use a different federated domain</span></span>](https://support.microsoft.com/en-us/kb/2669550)

<span data-ttu-id="279eb-137">Можно также настроить Azure AD так, чтобы модуль синхронизации обновлял userPrincipalName, как описано в статье [Функции службы синхронизации Azure AD Connect](active-directory-aadconnectsyncservice-features.md).</span><span class="sxs-lookup"><span data-stu-id="279eb-137">You can also configure Azure AD to allow the sync engine to update the userPrincipalName as described in [Azure AD Connect sync service features](active-directory-aadconnectsyncservice-features.md).</span></span>

<span data-ttu-id="279eb-138">**Вопрос. Поддерживается ли мягкое сопоставление локальных объектов группы или контактных объектов Azure AD с существующими объектами группы или контактными объектами Azure AD?**</span><span class="sxs-lookup"><span data-stu-id="279eb-138">**Q: Is it supported to soft match on-premises AD Group/Contact objects with existing Azure AD Group/Contact objects?**</span></span>  
<span data-ttu-id="279eb-139">Нет, в настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="279eb-139">No, this is currently not supported.</span></span>

<span data-ttu-id="279eb-140">**Вопрос. Поддерживается ли возможность настройки вручную атрибута ImmutableId в существующих объектах группы или контактных объектах Azure AD для их жесткого сопоставления с аналогичными локальными объектами?**</span><span class="sxs-lookup"><span data-stu-id="279eb-140">**Q: Is it supported to manually set ImmutableId attribute on existing Azure AD Group/Contact objects to hard match it to on-premises AD Group/Contact objects?**</span></span>  
<span data-ttu-id="279eb-141">Нет, в настоящее время такая возможность не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="279eb-141">No, this is currently not supported.</span></span>



## <a name="custom-configuration"></a><span data-ttu-id="279eb-142">Настраиваемая конфигурация</span><span class="sxs-lookup"><span data-stu-id="279eb-142">Custom configuration</span></span>
<span data-ttu-id="279eb-143">**Вопрос. Где можно найти документацию по командлетам PowerShell для Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-143">**Q: Where are the PowerShell cmdlets for Azure AD Connect documented?**</span></span>  
<span data-ttu-id="279eb-144">За исключением командлетов, описанных на этом сайте, другие командлеты PowerShell, используемые в Azure AD Connect, не предназначены для использования клиентами.</span><span class="sxs-lookup"><span data-stu-id="279eb-144">With the exception of the cmdlets documented on this site, other PowerShell cmdlets found in Azure AD Connect are not supported for customer use.</span></span>

<span data-ttu-id="279eb-145">**Вопрос. Можно ли использовать функцию "Server export/server import" (Импорт или экспорт сервера) в *Synchronization Service Manager* для перемещения конфигурации между серверами?**</span><span class="sxs-lookup"><span data-stu-id="279eb-145">**Q: Can I use "Server export/server import" found in *Synchronization Service Manager* to move configuration between servers?**</span></span>  
<span data-ttu-id="279eb-146">Нет.</span><span class="sxs-lookup"><span data-stu-id="279eb-146">No.</span></span> <span data-ttu-id="279eb-147">Этот параметр не получает все параметры конфигурации; его использование не рекомендуется.</span><span class="sxs-lookup"><span data-stu-id="279eb-147">This option will not retrieve all configuration settings and should not be used.</span></span> <span data-ttu-id="279eb-148">Вместо этого следует использовать мастер, чтобы создать базовую конфигурацию на втором сервере, и редактор правил синхронизации, чтобы создать сценарии PowerShell для перемещения настраиваемых правил между серверами.</span><span class="sxs-lookup"><span data-stu-id="279eb-148">You should instead use the wizard to create the base configuration on the second server and use the sync rule editor to generate PowerShell scripts to move any custom rule between servers.</span></span> <span data-ttu-id="279eb-149">Дополнительные сведения см. в разделе [Обновление со сменой сервера](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span><span class="sxs-lookup"><span data-stu-id="279eb-149">See [Swing migration](active-directory-aadconnect-upgrade-previous-version.md#swing-migration).</span></span>

<span data-ttu-id="279eb-150">**Вопрос. Могут ли сохраняться пароли в кэше для страницы входа Azure? Можно ли этого избежать, задав для элемента ввода пароля атрибут autocomplete со значением false?**</span><span class="sxs-lookup"><span data-stu-id="279eb-150">**Q: Can passwords be cached for the Azure sign-in page and can this be prevented since it contains a password input element with the autocomplete = "false" attribute?**</span></span></br>
<span data-ttu-id="279eb-151">В настоящее время изменение атрибутов HTML для поля ввода пароля, в том числе тега автозаполнения, не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="279eb-151">We currently do not support modifying the HTML attributes of the Password input field, including the autocomplete tag.</span></span> <span data-ttu-id="279eb-152">Мы работаем над функцией, которая позволит добавлять любой атрибут в поле пароля, используя пользовательский код Javascript.</span><span class="sxs-lookup"><span data-stu-id="279eb-152">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="279eb-153">Она должна быть доступна к концу 2017 года.</span><span class="sxs-lookup"><span data-stu-id="279eb-153">This should be available later part of 2017.</span></span>

<span data-ttu-id="279eb-154">**Вопрос. На странице входа Azure отображаются имена пользователей, которые уже выполнили вход.  Можно ли отключить эту функцию?**</span><span class="sxs-lookup"><span data-stu-id="279eb-154">**Q: On the Azure sign-in page, usernames for users who have previously signed in successfully are shown.  Can this behavior be turned off?**</span></span></br>
<span data-ttu-id="279eb-155">В настоящее время изменение атрибутов HTML страницы входа не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="279eb-155">We currently do not support modifying the HTML attributes of the sign-in page.</span></span> <span data-ttu-id="279eb-156">Мы работаем над функцией, которая позволит добавлять любой атрибут в поле пароля, используя пользовательский код Javascript.</span><span class="sxs-lookup"><span data-stu-id="279eb-156">We are currently working on a feature that will allow for custom Javascript which will allow you to add any attribute to the password field.</span></span> <span data-ttu-id="279eb-157">Она должна быть доступна к концу 2017 года.</span><span class="sxs-lookup"><span data-stu-id="279eb-157">This should be available later part of 2017.</span></span>

<span data-ttu-id="279eb-158">**Вопрос. Можно ли предотвратить параллельные сеансы?**</span><span class="sxs-lookup"><span data-stu-id="279eb-158">**Q: Is there a way to prevent concurrent sessions?**</span></span></br>
<span data-ttu-id="279eb-159">Нет.</span><span class="sxs-lookup"><span data-stu-id="279eb-159">No.</span></span>



## <a name="troubleshooting"></a><span data-ttu-id="279eb-160">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="279eb-160">Troubleshooting</span></span>
<span data-ttu-id="279eb-161">**Вопрос. Как получить справку по Azure AD Connect?**</span><span class="sxs-lookup"><span data-stu-id="279eb-161">**Q: How can I get help with Azure AD Connect?**</span></span>

[<span data-ttu-id="279eb-162">Поиск в базе знаний Майкрософт</span><span class="sxs-lookup"><span data-stu-id="279eb-162">Search the Microsoft Knowledge Base (KB)</span></span>](https://www.microsoft.com/en-us/Search/result.aspx?q=azure%20active%20directory%20connect&form=mssupport)

* <span data-ttu-id="279eb-163">В базе знаний Майкрософт можно найти технические решения распространенных проблем, связанные с поддержкой Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="279eb-163">Search the Microsoft Knowledge Base (KB) for technical solutions to common break-fix issues about Support for Azure AD Connect.</span></span>

[<span data-ttu-id="279eb-164">Форумы по Microsoft Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="279eb-164">Microsoft Azure Active Directory Forums</span></span>](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=WindowsAzureAD)

* <span data-ttu-id="279eb-165">[Здесь](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required)вы можете искать и просматривать ответы членов сообщества на технические вопросы, а также задавать собственные.</span><span class="sxs-lookup"><span data-stu-id="279eb-165">You can search and browse for technical questions and answers from the community or ask your own question by clicking [here](https://social.msdn.microsoft.com/Forums/azure/en-US/newthread?category=windowsazureplatform&forum=WindowsAzureAD&prof=required).</span></span>

[<span data-ttu-id="279eb-166">Служба поддержки клиентов Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="279eb-166">Azure AD Connect customer support</span></span>](https://manage.windowsazure.com/?getsupport=true)

* <span data-ttu-id="279eb-167">Перейдите по этой ссылке, чтобы получить поддержку на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="279eb-167">Use this link to get support through the Azure portal.</span></span>

