---
title: "Azure AD Connect. Обновление SSL-сертификата для фермы служб федерации Active Directory (AD FS) | Документы Майкрософт"
description: "В этом документе описаны действия по обновлению SSL-сертификата фермы AD FS с помощью Azure AD Connect."
services: active-directory
keywords: "azure ad connect, обновление ssl adfs, обновление сертификата adfs, изменение сертификата adfs, новый сертификат adfs, сертификат adfs, обновление ssl-сертификата adfs, обновление ssl-сертификата adfs, настройка ssl-сертификата adfs, adfs, ssl, сертификат, сертификат взаимодействия со службой adfs, обновление федерации, настройка федерации, aad connect"
authors: anandyadavmsft
manager: femila
editor: billmath
ms.assetid: 7c781f61-848a-48ad-9863-eb29da78f53c
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: anandy
ms.openlocfilehash: 87807a203d71b3abfe3e93132eb7d0b82b14b4ee
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="update-the-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="00b39-104">Обновление SSL-сертификата для фермы служб федерации Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="00b39-104">Update the SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="00b39-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="00b39-105">Overview</span></span>
<span data-ttu-id="00b39-106">В этой статье описывается обновление SSL-сертификата для фермы служб федерации Active Directory (AD FS) с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="00b39-106">This article describes how you can use Azure AD Connect to update the SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="00b39-107">С помощью инструмента Azure AD Connect можно легко обновить SSL-сертификат для фермы AD FS, даже если заданный метод входа пользователей отличается от AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-107">You can use the Azure AD Connect tool to easily update the SSL certificate for the AD FS farm even if the user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="00b39-108">Операцию обновления SSL-сертификата для фермы AD FS во всей федерации и на серверах прокси-службы веб-приложения (WAP) можно полностью выполнить за три простых шага.</span><span class="sxs-lookup"><span data-stu-id="00b39-108">You can perform the whole operation of updating SSL certificate for the AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Три шага](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="00b39-110">Дополнительные сведения о сертификатах, используемых службами AD FS, см. в статье [Общее представление о сертификатах, используемых службами федерации Active Directory](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="00b39-110">To learn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00b39-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="00b39-111">Prerequisites</span></span>

* <span data-ttu-id="00b39-112">**Ферма AD FS.** Убедитесь, что ферма AD FS работает под управлением Windows Server 2012 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="00b39-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="00b39-113">**Azure AD Connect.** Инструмент Azure AD Connect должен иметь версию 1.1.443.0 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="00b39-113">**Azure AD Connect**: Ensure that the version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="00b39-114">Вы используете задачу **Обновление SSL-сертификата AD FS**.</span><span class="sxs-lookup"><span data-stu-id="00b39-114">You'll use the task **Update AD FS SSL certificate**.</span></span>

![Задача обновления SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="00b39-116">Шаг 1. Предоставление сведений о ферме AD FS</span><span class="sxs-lookup"><span data-stu-id="00b39-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="00b39-117">Azure AD Connect попытается автоматически получить сведения о ферме AD FS следующими способами:</span><span class="sxs-lookup"><span data-stu-id="00b39-117">Azure AD Connect attempts to obtain information about the AD FS farm automatically by:</span></span>
1. <span data-ttu-id="00b39-118">Запросив сведения о ферме из AD FS (Windows Server 2016 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="00b39-118">Querying the farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="00b39-119">Просмотрев сведения из предыдущих выполнений (сохраненных локально с Azure AD Connect).</span><span class="sxs-lookup"><span data-stu-id="00b39-119">Referencing the information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="00b39-120">Отображаемый список серверов можно изменить путем добавления или изменения серверов в соответствии с текущей конфигурацией фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-120">You can modify the list of servers that are displayed by adding or removing the servers to reflect the current configuration of the AD FS farm.</span></span> <span data-ttu-id="00b39-121">После предоставления сведений о сервере Azure AD Connect отображает состояние подключения и текущее состояние SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="00b39-121">As soon as the server information is provided, Azure AD Connect displays the connectivity and current SSL certificate status.</span></span>

![Сведения о сервере AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="00b39-123">Если в списке содержится сервер, который больше не является частью фермы AD FS, щелкните **Удалить**, чтобы удалить его из списка серверов в ферме AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-123">If the list contains a server that's no longer part of the AD FS farm, click **Remove** to delete the server from the list of servers in your AD FS farm.</span></span>

![Автономный сервер в списке](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="00b39-125">Удаление сервера из списка серверов в ферме AD FS в Azure AD Connect является локальной операцией, которая обновляет данные для фермы AD FS, обслуживаемой Azure AD Connect в локальном режиме.</span><span class="sxs-lookup"><span data-stu-id="00b39-125">Removing a server from the list of servers for an AD FS farm in Azure AD Connect is a local operation and updates the information for the AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="00b39-126">Для отображения изменений Azure AD Connect не изменит конфигурацию в AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-126">Azure AD Connect doesn't modify the configuration on AD FS to reflect the change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="00b39-127">Шаг 2. Указание нового SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="00b39-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="00b39-128">После подтверждения сведений о серверах фермы AD FS Azure AD Connect запросит новый SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="00b39-128">After you've confirmed the information about AD FS farm servers, Azure AD Connect asks for the new SSL certificate.</span></span> <span data-ttu-id="00b39-129">Чтобы продолжить установку, укажите защищенный паролем PFX-сертификат.</span><span class="sxs-lookup"><span data-stu-id="00b39-129">Provide a password-protected PFX certificate to continue the installation.</span></span>

![SSL-сертификат](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="00b39-131">После предоставления сертификата Azure AD Connect выполнит необходимые процедуры.</span><span class="sxs-lookup"><span data-stu-id="00b39-131">After you provide the certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="00b39-132">Проверьте, что указан правильный сертификат для фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-132">Verify the certificate to ensure that the certificate is correct for the AD FS farm:</span></span>

-   <span data-ttu-id="00b39-133">Имя субъекта или альтернативное имя субъекта сертификата совпадает с именем службы федерации или является именем группового сертификата.</span><span class="sxs-lookup"><span data-stu-id="00b39-133">The subject name/alternate subject name for the certificate is either the same as the federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="00b39-134">Сертификат действителен в течение более чем 30 дней.</span><span class="sxs-lookup"><span data-stu-id="00b39-134">The certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="00b39-135">Цепь доверия сертификатов является допустимой.</span><span class="sxs-lookup"><span data-stu-id="00b39-135">The certificate trust chain is valid.</span></span>
-   <span data-ttu-id="00b39-136">Сертификат защищен паролем.</span><span class="sxs-lookup"><span data-stu-id="00b39-136">The certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-the-update"></a><span data-ttu-id="00b39-137">Шаг 3. Выбор серверов для обновления</span><span class="sxs-lookup"><span data-stu-id="00b39-137">Step 3: Select servers for the update</span></span>

<span data-ttu-id="00b39-138">На следующем шаге выберите серверы, для которых необходимо обновить SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="00b39-138">In the next step, select the servers that need to have the SSL certificate updated.</span></span> <span data-ttu-id="00b39-139">Серверы, которые находятся в автономном режиме, выбирать нельзя.</span><span class="sxs-lookup"><span data-stu-id="00b39-139">Servers that are offline can't be selected for the update.</span></span>

![Выбор серверов для обновления](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="00b39-141">По завершении настройки Azure AD Connect отобразит сообщение, указывающее состояние обновления, и предоставит возможность проверки входа в AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-141">After you complete the configuration, Azure AD Connect displays the message that indicates the status of the update and provides an option to verify the AD FS sign-in.</span></span>

![Завершение настройки](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="00b39-143">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="00b39-143">FAQs</span></span>

* <span data-ttu-id="00b39-144">**Что должно собой представлять имя субъекта сертификата для нового SSL-сертификата AD FS?**</span><span class="sxs-lookup"><span data-stu-id="00b39-144">**What should be the subject name of the certificate for the new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="00b39-145">Azure AD Connect проверяет, содержит ли имя субъекта или альтернативное имя субъекта сертификата имя службы федерации.</span><span class="sxs-lookup"><span data-stu-id="00b39-145">Azure AD Connect checks if the subject name/alternate subject name of the certificate contains the federation service name.</span></span> <span data-ttu-id="00b39-146">Например, если имя службы федерации — fs.contoso.com, именем субъекта или альтернативным именем субъекта должно быть fs.contoso.com.</span><span class="sxs-lookup"><span data-stu-id="00b39-146">For example, if your federation service name is fs.contoso.com, the subject name/alternate subject name must be fs.contoso.com.</span></span>  <span data-ttu-id="00b39-147">Поддерживаются также групповые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="00b39-147">Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="00b39-148">**Почему на странице сервера WAP появляется повторный запрос на ввод учетных данных?**</span><span class="sxs-lookup"><span data-stu-id="00b39-148">**Why am I asked for credentials again on the WAP server page?**</span></span>

    <span data-ttu-id="00b39-149">Если указанные учетные данные для подключения к серверам AD FS не имеют прав на управление серверами WAP, Azure AD Connect выведет запрос на ввод учетных данных с административными привилегиями на WAP-серверах.</span><span class="sxs-lookup"><span data-stu-id="00b39-149">If the credentials you provide for connecting to AD FS servers don't also have the privilege to manage the WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on the WAP servers.</span></span>

* <span data-ttu-id="00b39-150">**Сервер находится в автономном режиме. Что делать?**</span><span class="sxs-lookup"><span data-stu-id="00b39-150">**The server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="00b39-151">Если сервер находится вне сети, Azure AD Connect не может выполнять никаких операций.</span><span class="sxs-lookup"><span data-stu-id="00b39-151">Azure AD Connect can't perform any operation if the server is offline.</span></span> <span data-ttu-id="00b39-152">Если сервер является частью фермы AD FS, проверьте подключение к нему.</span><span class="sxs-lookup"><span data-stu-id="00b39-152">If the server is part of the AD FS farm, then check the connectivity to the server.</span></span> <span data-ttu-id="00b39-153">Устранив проблему, щелкните значок обновления, чтобы изменить состояние в мастере.</span><span class="sxs-lookup"><span data-stu-id="00b39-153">After you've resolved the issue, press the refresh icon to update the status in the wizard.</span></span> <span data-ttu-id="00b39-154">Если сервер ранее входил в ферму, но уже не существует, щелкните **Удалить**, чтобы удалить его из списка серверов, поддерживаемых Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="00b39-154">If the server was part of the farm earlier but now no longer exists, click **Remove** to delete it from the list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="00b39-155">Удаление сервера из списка в Azure AD Connect не приводит к изменению самой конфигурации AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-155">Removing the server from the list in Azure AD Connect doesn't alter the AD FS configuration itself.</span></span> <span data-ttu-id="00b39-156">При использовании AD FS в Windows Server 2016 или более поздней версии сервер останется в параметрах конфигурации и отобразится при следующем запуске задачи.</span><span class="sxs-lookup"><span data-stu-id="00b39-156">If you're using AD FS in Windows Server 2016 or later, the server remains in the configuration settings and will be shown again the next time the task is run.</span></span>

* <span data-ttu-id="00b39-157">**Можно ли обновить подмножество серверов фермы с помощью нового SSL-сертификата?**</span><span class="sxs-lookup"><span data-stu-id="00b39-157">**Can I update a subset of my farm servers with the new SSL certificate?**</span></span>

    <span data-ttu-id="00b39-158">Да.</span><span class="sxs-lookup"><span data-stu-id="00b39-158">Yes.</span></span> <span data-ttu-id="00b39-159">Задачу **Обновить SSL-сертификат** можно запускать повторно, чтобы обновить оставшиеся серверы.</span><span class="sxs-lookup"><span data-stu-id="00b39-159">You can always run the task **Update SSL Certificate** again to update the remaining servers.</span></span> <span data-ttu-id="00b39-160">На странице **Выберите серверы, на которых нужно обновить SSL-сертификат** можно отсортировать список серверов на странице **Срок действия SSL**, чтобы без труда обращаться к серверам, которые пока не обновлены.</span><span class="sxs-lookup"><span data-stu-id="00b39-160">On the **Select servers for SSL certificate update** page, you can sort the list of servers on **SSL Expiry date** to easily access the servers that aren't updated yet.</span></span>

* <span data-ttu-id="00b39-161">**Сервер был удален во время предыдущего запуска, но он по-прежнему отображается как находящийся вне сети и указан на странице серверов AD FS. Почему этот автономный сервер по-прежнему существует даже после удаления?**</span><span class="sxs-lookup"><span data-stu-id="00b39-161">**I removed the server in the previous run, but it's still being shown as offline and listed on the AD FS Servers page. Why is the offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="00b39-162">Удаление сервера из списка в Azure AD Connect не приводит к его удалению из конфигурации AD FS.</span><span class="sxs-lookup"><span data-stu-id="00b39-162">Removing the server from the list in Azure AD Connect doesn't remove it in the AD FS configuration.</span></span> <span data-ttu-id="00b39-163">Azure AD Connect обращается к AD FS (Windows Server 2016 или более поздней версии) для получения сведений о ферме.</span><span class="sxs-lookup"><span data-stu-id="00b39-163">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about the farm.</span></span> <span data-ttu-id="00b39-164">Если сервер по-прежнему присутствует в конфигурации AD FS, он будет указан в списке.</span><span class="sxs-lookup"><span data-stu-id="00b39-164">If the server is still present in the AD FS configuration, it will be listed back in the list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="00b39-165">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="00b39-165">Next steps</span></span>

- [<span data-ttu-id="00b39-166">Azure AD Connect и федерация</span><span class="sxs-lookup"><span data-stu-id="00b39-166">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="00b39-167">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="00b39-167">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
