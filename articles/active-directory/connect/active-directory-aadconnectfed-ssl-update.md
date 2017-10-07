---
title: "Azure AD Connect: Hello обновления SSL-сертификат для фермы службы федерации Active Directory (AD FS) | Документы Microsoft"
description: "Этот документ сведения hello действия tooupdate hello SSL-сертификат фермы AD FS с помощью Azure AD Connect."
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
ms.openlocfilehash: bce7f75aab83b6abacb8472a6895054d137e10e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="update-hello-ssl-certificate-for-an-active-directory-federation-services-ad-fs-farm"></a><span data-ttu-id="2291a-104">Обновить сертификат SSL hello для фермы службы федерации Active Directory (AD FS)</span><span class="sxs-lookup"><span data-stu-id="2291a-104">Update hello SSL certificate for an Active Directory Federation Services (AD FS) farm</span></span>

## <a name="overview"></a><span data-ttu-id="2291a-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="2291a-105">Overview</span></span>
<span data-ttu-id="2291a-106">В этой статье описывается, как можно использовать Azure AD Connect tooupdate hello SSL-сертификат для фермы службы федерации Active Directory (AD FS).</span><span class="sxs-lookup"><span data-stu-id="2291a-106">This article describes how you can use Azure AD Connect tooupdate hello SSL certificate for an Active Directory Federation Services (AD FS) farm.</span></span> <span data-ttu-id="2291a-107">Можно использовать hello Azure AD Connect tooeasily средство обновления hello SSL-сертификат для фермы hello AD FS, даже если hello пользователя войти выбранного метода не AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-107">You can use hello Azure AD Connect tool tooeasily update hello SSL certificate for hello AD FS farm even if hello user sign-in method selected is not AD FS.</span></span>

<span data-ttu-id="2291a-108">Можно выполнить hello всей операции обновления SSL-сертификат для фермы hello AD FS для всех федерации и прокси-сервера веб-приложения (WAP) серверов три простых шагов.</span><span class="sxs-lookup"><span data-stu-id="2291a-108">You can perform hello whole operation of updating SSL certificate for hello AD FS farm across all federation and Web Application Proxy (WAP) servers in three simple steps:</span></span>

![Три шага](./media/active-directory-aadconnectfed-ssl-update/threesteps.png)


>[!NOTE]
><span data-ttu-id="2291a-110">toolearn Дополнительные сведения о сертификаты, используемые службами AD FS в разделе [основные сведения о сертификатах, используемых службами AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span><span class="sxs-lookup"><span data-stu-id="2291a-110">toolearn more about certificates that are used by AD FS, see [Understanding certificates used by AD FS](https://technet.microsoft.com/library/cc730660.aspx).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2291a-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="2291a-111">Prerequisites</span></span>

* <span data-ttu-id="2291a-112">**Ферма AD FS.** Убедитесь, что ферма AD FS работает под управлением Windows Server 2012 R2 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2291a-112">**AD FS Farm**: Make sure that your AD FS farm is Windows Server 2012 R2-based or later.</span></span>
* <span data-ttu-id="2291a-113">**Azure AD Connect**: Убедитесь, что hello версия Azure AD Connect — 1.1.443.0 или более поздней версии.</span><span class="sxs-lookup"><span data-stu-id="2291a-113">**Azure AD Connect**: Ensure that hello version of Azure AD Connect is 1.1.443.0 or later.</span></span> <span data-ttu-id="2291a-114">Будем использовать задачу hello **обновления AD FS SSL-сертификат**.</span><span class="sxs-lookup"><span data-stu-id="2291a-114">You'll use hello task **Update AD FS SSL certificate**.</span></span>

![Задача обновления SSL](./media/active-directory-aadconnectfed-ssl-update/updatessltask.png)

## <a name="step-1-provide-ad-fs-farm-information"></a><span data-ttu-id="2291a-116">Шаг 1. Предоставление сведений о ферме AD FS</span><span class="sxs-lookup"><span data-stu-id="2291a-116">Step 1: Provide AD FS farm information</span></span>

<span data-ttu-id="2291a-117">Azure AD Connect автоматически предпримет tooobtain сведения о ферме hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-117">Azure AD Connect attempts tooobtain information about hello AD FS farm automatically by:</span></span>
1. <span data-ttu-id="2291a-118">Запроса сведений о ферме hello из службы федерации Active Directory (Windows Server 2016 или более поздней версии).</span><span class="sxs-lookup"><span data-stu-id="2291a-118">Querying hello farm information from AD FS (Windows Server 2016 or later).</span></span>
2. <span data-ttu-id="2291a-119">Ссылка на сведения hello из предыдущего выполнения, в котором хранятся локально с Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="2291a-119">Referencing hello information from previous runs, which are stored locally with Azure AD Connect.</span></span>

<span data-ttu-id="2291a-120">Вы можете изменить hello список серверов, которые отображаются, добавив или удалив hello серверов tooreflect hello текущей конфигурации фермы hello AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-120">You can modify hello list of servers that are displayed by adding or removing hello servers tooreflect hello current configuration of hello AD FS farm.</span></span> <span data-ttu-id="2291a-121">Как только сведения о сервере hello предоставляется, Azure AD Connect отображает hello подключения и текущее состояние сертификата SSL.</span><span class="sxs-lookup"><span data-stu-id="2291a-121">As soon as hello server information is provided, Azure AD Connect displays hello connectivity and current SSL certificate status.</span></span>

![Сведения о сервере AD FS](./media/active-directory-aadconnectfed-ssl-update/adfsserverinfo.png)

<span data-ttu-id="2291a-123">Если список hello содержит сервера, который больше не является частью фермы hello AD FS, щелкните **удалить** toodelete hello сервер из списка серверов в ферме AD FS hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-123">If hello list contains a server that's no longer part of hello AD FS farm, click **Remove** toodelete hello server from hello list of servers in your AD FS farm.</span></span>

![Автономный сервер в списке](./media/active-directory-aadconnectfed-ssl-update/offlineserverlist.png)

>[!NOTE]
> <span data-ttu-id="2291a-125">Удаление сервера из списка hello серверов AD FS фермы в Azure AD Connect локального операция и обновления hello сведения для hello фермы AD FS, который поддерживает Azure AD Connect, локально.</span><span class="sxs-lookup"><span data-stu-id="2291a-125">Removing a server from hello list of servers for an AD FS farm in Azure AD Connect is a local operation and updates hello information for hello AD FS farm that Azure AD Connect maintains locally.</span></span> <span data-ttu-id="2291a-126">Azure AD Connect не изменяет конфигурации hello при изменении hello tooreflect AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-126">Azure AD Connect doesn't modify hello configuration on AD FS tooreflect hello change.</span></span>    

## <a name="step-2-provide-a-new-ssl-certificate"></a><span data-ttu-id="2291a-127">Шаг 2. Указание нового SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="2291a-127">Step 2: Provide a new SSL certificate</span></span>

<span data-ttu-id="2291a-128">После подтверждения hello сведения о серверах фермы AD FS, Azure AD Connect запрашивает hello новый SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="2291a-128">After you've confirmed hello information about AD FS farm servers, Azure AD Connect asks for hello new SSL certificate.</span></span> <span data-ttu-id="2291a-129">Укажите защищенный паролем PFX toocontinue hello установки сертификата.</span><span class="sxs-lookup"><span data-stu-id="2291a-129">Provide a password-protected PFX certificate toocontinue hello installation.</span></span>

![SSL-сертификат](./media/active-directory-aadconnectfed-ssl-update/certificate.png)

<span data-ttu-id="2291a-131">После ввода hello сертификат Azure AD Connect проходит через ряд необходимых компонентов.</span><span class="sxs-lookup"><span data-stu-id="2291a-131">After you provide hello certificate, Azure AD Connect goes through a series of prerequisites.</span></span> <span data-ttu-id="2291a-132">Проверьте правильность tooensure сертификат hello, hello сертификат фермы hello AD FS:</span><span class="sxs-lookup"><span data-stu-id="2291a-132">Verify hello certificate tooensure that hello certificate is correct for hello AD FS farm:</span></span>

-   <span data-ttu-id="2291a-133">Hello субъекта имени или альтернативного имени субъекта для hello сертификат может быть Здравствуйте таким же, как имя службы федерации hello, или он представляет собой групповой сертификат.</span><span class="sxs-lookup"><span data-stu-id="2291a-133">hello subject name/alternate subject name for hello certificate is either hello same as hello federation service name, or it's a wildcard certificate.</span></span>
-   <span data-ttu-id="2291a-134">Hello сертификат действителен в течение более 30 дней.</span><span class="sxs-lookup"><span data-stu-id="2291a-134">hello certificate is valid for more than 30 days.</span></span>
-   <span data-ttu-id="2291a-135">цепь доверия сертификатов Hello является допустимым.</span><span class="sxs-lookup"><span data-stu-id="2291a-135">hello certificate trust chain is valid.</span></span>
-   <span data-ttu-id="2291a-136">Hello сертификат, защищен паролем.</span><span class="sxs-lookup"><span data-stu-id="2291a-136">hello certificate is password protected.</span></span>

## <a name="step-3-select-servers-for-hello-update"></a><span data-ttu-id="2291a-137">Шаг 3: Выбор серверов для обновления hello</span><span class="sxs-lookup"><span data-stu-id="2291a-137">Step 3: Select servers for hello update</span></span>

<span data-ttu-id="2291a-138">В следующем шаге hello выберите hello серверам, нуждающимся toohave hello SSL-сертификат обновлен.</span><span class="sxs-lookup"><span data-stu-id="2291a-138">In hello next step, select hello servers that need toohave hello SSL certificate updated.</span></span> <span data-ttu-id="2291a-139">Серверы, которые находятся в автономном режиме нельзя выбрать для обновления hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-139">Servers that are offline can't be selected for hello update.</span></span>

![Выберите серверы tooupdate](./media/active-directory-aadconnectfed-ssl-update/selectservers.png)

<span data-ttu-id="2291a-141">После завершения настройки hello Azure AD Connect отображает приветственное сообщение, указывающее состояние обновления hello hello и предоставляет параметр tooverify hello AD FS вход.</span><span class="sxs-lookup"><span data-stu-id="2291a-141">After you complete hello configuration, Azure AD Connect displays hello message that indicates hello status of hello update and provides an option tooverify hello AD FS sign-in.</span></span>

![Завершение настройки](./media/active-directory-aadconnectfed-ssl-update/configurecomplete.png)   

## <a name="faqs"></a><span data-ttu-id="2291a-143">Часто задаваемые вопросы</span><span class="sxs-lookup"><span data-stu-id="2291a-143">FAQs</span></span>

* <span data-ttu-id="2291a-144">**Что должны быть hello. имя субъекта сертификата hello hello новый сертификат AD FS SSL?**</span><span class="sxs-lookup"><span data-stu-id="2291a-144">**What should be hello subject name of hello certificate for hello new AD FS SSL certificate?**</span></span>

    <span data-ttu-id="2291a-145">Azure AD Connect проверяет, содержит ли имя субъекта имени или альтернативного hello субъекта сертификата hello hello имя службы федерации.</span><span class="sxs-lookup"><span data-stu-id="2291a-145">Azure AD Connect checks if hello subject name/alternate subject name of hello certificate contains hello federation service name.</span></span> <span data-ttu-id="2291a-146">Например если имя службы федерации fs.contoso.com, hello субъекта имени или альтернативного субъекта имя должно быть fs.contoso.com.  Поддерживаются также групповые сертификаты.</span><span class="sxs-lookup"><span data-stu-id="2291a-146">For example, if your federation service name is fs.contoso.com, hello subject name/alternate subject name must be fs.contoso.com.  Wildcard certificates are also accepted.</span></span>

* <span data-ttu-id="2291a-147">**Почему появляется учетные данные снова на странице сервера WAP hello?**</span><span class="sxs-lookup"><span data-stu-id="2291a-147">**Why am I asked for credentials again on hello WAP server page?**</span></span>

    <span data-ttu-id="2291a-148">Если hello учетные данные, предоставленные для подключения серверов федерации Active Directory tooAD также нет hello прав toomanage hello WAP-серверах, затем Azure AD Connect запрашивает учетные данные, имеющие административные привилегии на hello WAP-серверах.</span><span class="sxs-lookup"><span data-stu-id="2291a-148">If hello credentials you provide for connecting tooAD FS servers don't also have hello privilege toomanage hello WAP servers, then Azure AD Connect asks for credentials that have administrative privilege on hello WAP servers.</span></span>

* <span data-ttu-id="2291a-149">**Hello сервер отображается как отключенный. Что делать?**</span><span class="sxs-lookup"><span data-stu-id="2291a-149">**hello server is shown as offline. What should I do?**</span></span>

    <span data-ttu-id="2291a-150">Azure AD Connect не может выполнить любую операцию, если сервер hello отключен.</span><span class="sxs-lookup"><span data-stu-id="2291a-150">Azure AD Connect can't perform any operation if hello server is offline.</span></span> <span data-ttu-id="2291a-151">Если hello server является частью hello фермы AD FS, проверьте сервер toohello hello подключения.</span><span class="sxs-lookup"><span data-stu-id="2291a-151">If hello server is part of hello AD FS farm, then check hello connectivity toohello server.</span></span> <span data-ttu-id="2291a-152">После разрешения проблемы hello, нажмите клавишу состояние hello tooupdate значок обновления hello в мастере hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-152">After you've resolved hello issue, press hello refresh icon tooupdate hello status in hello wizard.</span></span> <span data-ttu-id="2291a-153">Если сервер hello входила в состав из hello фермы ранее, но теперь больше не существует, щелкните **удалить** toodelete поддерживает его из списка серверов, Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-153">If hello server was part of hello farm earlier but now no longer exists, click **Remove** toodelete it from hello list of servers that Azure AD Connect maintains.</span></span> <span data-ttu-id="2291a-154">Удаление сервера hello из списка hello в Azure AD Connect не изменяет hello сама конфигурация AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-154">Removing hello server from hello list in Azure AD Connect doesn't alter hello AD FS configuration itself.</span></span> <span data-ttu-id="2291a-155">Если вы используете службы федерации Active Directory в Windows Server 2016 или более поздней версии, hello server остается в параметрах конфигурации hello и отображается снова hello при очередном hello выполнения задачи.</span><span class="sxs-lookup"><span data-stu-id="2291a-155">If you're using AD FS in Windows Server 2016 or later, hello server remains in hello configuration settings and will be shown again hello next time hello task is run.</span></span>

* <span data-ttu-id="2291a-156">**Можно обновить подмножество моей ферме серверов с hello новый SSL-сертификат?**</span><span class="sxs-lookup"><span data-stu-id="2291a-156">**Can I update a subset of my farm servers with hello new SSL certificate?**</span></span>

    <span data-ttu-id="2291a-157">Да.</span><span class="sxs-lookup"><span data-stu-id="2291a-157">Yes.</span></span> <span data-ttu-id="2291a-158">Всегда иметь возможность выполнить задачу hello **обновления SSL-сертификат** снова tooupdate hello оставшихся серверов.</span><span class="sxs-lookup"><span data-stu-id="2291a-158">You can always run hello task **Update SSL Certificate** again tooupdate hello remaining servers.</span></span> <span data-ttu-id="2291a-159">На hello **обновления сертификатов выберите серверы для использования SSL** страницы, можно выполнить сортировку hello список серверов по **даты истечения срока действия SSL** tooeasily доступа hello серверы, которые еще не обновлены.</span><span class="sxs-lookup"><span data-stu-id="2291a-159">On hello **Select servers for SSL certificate update** page, you can sort hello list of servers on **SSL Expiry date** tooeasily access hello servers that aren't updated yet.</span></span>

* <span data-ttu-id="2291a-160">**Я удалил сервера hello в hello предыдущего запуска, но она по-прежнему показывается как вне сети и перечисленные на странице приветствия AD FS серверы. Почему необходимо hello автономный сервер по-прежнему существует, даже после того, она удалена?**</span><span class="sxs-lookup"><span data-stu-id="2291a-160">**I removed hello server in hello previous run, but it's still being shown as offline and listed on hello AD FS Servers page. Why is hello offline server still there even after I removed it?**</span></span>

    <span data-ttu-id="2291a-161">Удаление сервера hello из списка hello в Azure AD Connect не удаляет его в hello конфигурации AD FS.</span><span class="sxs-lookup"><span data-stu-id="2291a-161">Removing hello server from hello list in Azure AD Connect doesn't remove it in hello AD FS configuration.</span></span> <span data-ttu-id="2291a-162">Azure AD Connect ссылается на AD FS (Windows Server 2016 или более поздней версии), все сведения о ферме hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-162">Azure AD Connect references AD FS (Windows Server 2016 or higher) for any information about hello farm.</span></span> <span data-ttu-id="2291a-163">Если hello server по-прежнему присутствует в hello конфигурации AD FS, отображаются в списке hello.</span><span class="sxs-lookup"><span data-stu-id="2291a-163">If hello server is still present in hello AD FS configuration, it will be listed back in hello list.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="2291a-164">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2291a-164">Next steps</span></span>

- [<span data-ttu-id="2291a-165">Azure AD Connect и федерация</span><span class="sxs-lookup"><span data-stu-id="2291a-165">Azure AD Connect and federation</span></span>](active-directory-aadconnectfed-whatis.md)
- [<span data-ttu-id="2291a-166">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="2291a-166">Active Directory Federation Services management and customization with Azure AD Connect</span></span>](active-directory-aadconnect-federation-management.md)
