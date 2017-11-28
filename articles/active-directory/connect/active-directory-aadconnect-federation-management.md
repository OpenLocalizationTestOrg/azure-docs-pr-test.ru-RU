---
title: "Службы федерации Directory aaaActive управления и настройки с Azure AD Connect | Документы Microsoft"
description: "Управление службами AD FS с помощью Azure AD Connect и настройка пользовательского входа в AD FS с помощью Azure AD Connect и PowerShell."
keywords: "AD FS, ADFS, управление AD FS, AAD Connect, Connect, вход, настройка AD FS, восстановление доверия, Office 365, федерация, проверяющая сторона"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 2593b6c6-dc3f-46ef-8e02-a8e2dc4e9fb9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/18/2017
ms.author: billmath
ms.openlocfilehash: 361a2bfd6d7a6993dbe773d6ea039ad1afc6346a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="8c6f9-104">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8c6f9-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="8c6f9-105">В этой статье описывается как toomanage и настройте службы федерации Active Directory (AD FS), используя подключение Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-105">This article describes how toomanage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="8c6f9-106">Он также включает другие стандартные задачи AD FS, которые могут потребоваться toodo для завершения настройки фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-106">It also includes other common AD FS tasks that you might need toodo for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="8c6f9-107">Раздел</span><span class="sxs-lookup"><span data-stu-id="8c6f9-107">Topic</span></span> | <span data-ttu-id="8c6f9-108">Что описывает</span><span class="sxs-lookup"><span data-stu-id="8c6f9-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="8c6f9-109">**Управление AD FS**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="8c6f9-110">Восстановите доверие hello</span><span class="sxs-lookup"><span data-stu-id="8c6f9-110">Repair hello trust</span></span>](#repairthetrust) |<span data-ttu-id="8c6f9-111">Как федерации hello toorepair доверие с Office 365.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-111">How toorepair hello federation trust with Office 365.</span></span> |
| [<span data-ttu-id="8c6f9-112">Федерация с Azure AD с помощью альтернативного имени пользователя</span><span class="sxs-lookup"><span data-stu-id="8c6f9-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="8c6f9-113">Настройка федерации с использованием альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="8c6f9-114">Добавление сервера AD FS</span><span class="sxs-lookup"><span data-stu-id="8c6f9-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="8c6f9-115">Каким образом AD FS tooexpand фермы с дополнительного сервера AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-115">How tooexpand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="8c6f9-116">Добавление прокси-сервера веб-приложения AD FS</span><span class="sxs-lookup"><span data-stu-id="8c6f9-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="8c6f9-117">Каким образом AD FS tooexpand фермы с дополнительного сервера прокси-сервера веб-приложения (WAP).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-117">How tooexpand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="8c6f9-118">Добавление федеративного домена</span><span class="sxs-lookup"><span data-stu-id="8c6f9-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="8c6f9-119">Как tooadd федеративный домен.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-119">How tooadd a federated domain.</span></span> |
| [<span data-ttu-id="8c6f9-120">Обновить сертификат SSL hello</span><span class="sxs-lookup"><span data-stu-id="8c6f9-120">Update hello SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="8c6f9-121">Как tooupdate hello SSL сертификат для фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-121">How tooupdate hello SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="8c6f9-122">**Настройка AD FS**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="8c6f9-123">Добавление настраиваемого логотипа компании или иллюстрации</span><span class="sxs-lookup"><span data-stu-id="8c6f9-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="8c6f9-124">Как войти toocustomize AD FS страницы с эмблемой компании и иллюстрации.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-124">How toocustomize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="8c6f9-125">Добавление описания входа в систему</span><span class="sxs-lookup"><span data-stu-id="8c6f9-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="8c6f9-126">Как tooadd входа в странице описания.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-126">How tooadd a sign-in page description.</span></span> |
| [<span data-ttu-id="8c6f9-127">Изменение правил утверждений служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="8c6f9-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="8c6f9-128">Как toomodify AD FS утверждений для различных сценариев федерации.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-128">How toomodify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="8c6f9-129">Управление AD FS</span><span class="sxs-lookup"><span data-stu-id="8c6f9-129">Manage AD FS</span></span>
<span data-ttu-id="8c6f9-130">В Azure AD Connect с минимальным участием пользователя выполнять различные задачи AD FS связанные с помощью мастера hello Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using hello Azure AD Connect wizard.</span></span> <span data-ttu-id="8c6f9-131">После завершения установки Azure AD Connect выполнения мастером hello hello мастер можно запустить снова tooperform дополнительные задачи.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-131">After you've finished installing Azure AD Connect by running hello wizard, you can run hello wizard again tooperform additional tasks.</span></span>

## <span data-ttu-id="8c6f9-132">Восстановите доверие hello<a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-132">Repair hello trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="8c6f9-133">Можно использовать Azure AD Connect toocheck hello текущее состояние работоспособности hello AD FS и отношение доверия Azure AD и выполнить соответствующие действия toorepair hello доверия.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-133">You can use Azure AD Connect toocheck hello current health of hello AD FS and Azure AD trust and take appropriate actions toorepair hello trust.</span></span> <span data-ttu-id="8c6f9-134">Выполните эти шаги toorepair Azure AD и AD FS доверия.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-134">Follow these steps toorepair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="8c6f9-135">Выберите **AAD восстановления и доверия ADFS** списке hello дополнительные задачи.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-135">Select **Repair AAD and ADFS Trust** from hello list of additional tasks.</span></span>
   <span data-ttu-id="8c6f9-136">![Восстановление доверия AAD и ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="8c6f9-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="8c6f9-137">На hello **подключения tooAzure AD** , введите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-137">On hello **Connect tooAzure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="8c6f9-138">![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="8c6f9-138">![Connect tooAzure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="8c6f9-139">На hello **учетные данные для удаленного доступа** введите hello учетные данные администратора домена hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-139">On hello **Remote access credentials** page, enter hello credentials for hello domain administrator.</span></span>

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="8c6f9-141">Когда вы нажмете кнопку **Далее**, Azure AD Connect проверит работоспособность сертификата и отобразит возможные проблемы.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Состояние сертификатов](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="8c6f9-143">Hello **готовности tooconfigure** страница hello показан список действий, которые будут выполнены toorepair hello доверия.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-143">hello **Ready tooconfigure** page shows hello list of actions that will be performed toorepair hello trust.</span></span>

    ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="8c6f9-145">Нажмите кнопку **установить** toorepair hello доверия.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-145">Click **Install** toorepair hello trust.</span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-146">Azure AD Connect может выполнить восстановление или другие действия только для самозаверяющих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="8c6f9-147">С помощью Azure AD Connect нельзя восстановить сертификаты третьих сторон.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="8c6f9-148">Федерация с Azure AD с помощью альтернативного имени пользователя <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="8c6f9-149">Рекомендуется, hello локальной Name(UPN) участника-пользователя и облака hello, имя участника-пользователя хранятся hello таким же.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-149">It is recommended that hello on-premises User Principal Name(UPN) and hello cloud User Principal Name are kept hello same.</span></span> <span data-ttu-id="8c6f9-150">Если hello локального имени участника-пользователя используется немаршрутизируемый домена (например,).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-150">If hello on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="8c6f9-151">Contoso.local) или не может быть изменен из-за зависимостей приложения toolocal, рекомендуется настроить альтернативное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-151">Contoso.local) or cannot be changed due toolocal application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="8c6f9-152">Альтернативного идентификатора входа позволяет tooconfigure входа пользователей где пользователи могут войти под атрибут, отличный от их имени участника-пользователя, например, почту.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-152">Alternate login ID allows you tooconfigure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="8c6f9-153">Hello Выбор для имени участника-пользователя в Azure AD Connect атрибут userPrincipalName toohello значения по умолчанию в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-153">hello choice for User Principal Name in Azure AD Connect defaults toohello userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="8c6f9-154">Если выбрать для имени участника-пользователя любой другой атрибут и выполнить федерацию с помощью AD FS, то Azure AD Connect настроит AD FS на использование альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="8c6f9-155">В приведенном ниже примере показано, как выбрать другой атрибут для имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Выбор альтернативного атрибута имени пользователя](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="8c6f9-157">Настройка альтернативного имени пользователя для AD FS состоит из двух основных этапов:</span><span class="sxs-lookup"><span data-stu-id="8c6f9-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="8c6f9-158">**Настройка hello правильный набор утверждений для выдачи**: hello правил утверждений выдачи в проверяющей стороне hello Azure AD доверии toouse измененный атрибут UserPrincipalName hello выбран как hello альтернативного идентификатора пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-158">**Configure hello right set of issuance claims**: hello issuance claim rules in hello Azure AD relying party trust are modified toouse hello selected UserPrincipalName attribute as hello alternate ID of hello user.</span></span>
2. <span data-ttu-id="8c6f9-159">**Включение альтернативного идентификатора входа в конфигурации AD FS hello**: hello AD FS конфигурации обновляется, чтобы службы федерации Active Directory можно найти пользователей в соответствующие лесах hello, используя hello альтернативный идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-159">**Enable alternate login ID in hello AD FS configuration**: hello AD FS configuration is updated so that AD FS can look up users in hello appropriate forests using hello alternate ID.</span></span> <span data-ttu-id="8c6f9-160">Эта конфигурация поддерживается для службы AD FS, работающей под управлением Windows Server 2012 R2 (с обновлением KB2919355) и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="8c6f9-161">Если серверы hello AD FS 2012 R2, Azure AD Connect проверяет наличие hello hello требуется КБ.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-161">If hello AD FS servers are 2012 R2, Azure AD Connect checks for hello presence of hello required KB.</span></span> <span data-ttu-id="8c6f9-162">Если hello КБ не обнаруживается, предупреждение будет отображаться после завершения настройки, как показано ниже:</span><span class="sxs-lookup"><span data-stu-id="8c6f9-162">If hello KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Предупреждение об отсутствии обновления в версии 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="8c6f9-164">Конфигурация hello toorectify в случае отсутствующих КБ, установите необходимые hello [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) и затем восстановить с помощью доверия hello [восстановить AAD и отношение доверия AD FS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-164">toorectify hello configuration in case of missing KB, install hello required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair hello trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-165">Дополнительные сведения о toomanually alternateID и шаги настройки, чтение [настройка альтернативного идентификатора входа](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span><span class="sxs-lookup"><span data-stu-id="8c6f9-165">For more information on alternateID and steps toomanually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="8c6f9-166">Добавление сервера AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-167">сервер AD FS tooadd Azure AD Connect требуется hello PFX-сертификат.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-167">tooadd an AD FS server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="8c6f9-168">Таким образом можно выполнить эту операцию только в том случае, если вы настроили фермы hello AD FS с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-168">Therefore, you can perform this operation only if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="8c6f9-169">Выберите пункт **Развернуть дополнительный сервер федерации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Дополнительный сервер федерации](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="8c6f9-171">На hello **подключения tooAzure AD** введите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-171">On hello **Connect tooAzure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="8c6f9-173">Укажите учетные данные администратора домена hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-173">Provide hello domain administrator credentials.</span></span>

   ![Учетные данные администратора домена](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="8c6f9-175">Azure AD Connect запрашивает пароль hello hello PFX-файл, указанный при настройке новой ферме AD FS с Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-175">Azure AD Connect asks for hello password of hello PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="8c6f9-176">Нажмите кнопку **ввод пароля** tooprovide hello пароль для PFX-файла hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-176">Click **Enter Password** tooprovide hello password for hello PFX file.</span></span>

   ![Пароль сертификата](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="8c6f9-179">На hello **серверов AD FS** введите hello имя сервера или IP адрес toobe добавлены фермы toohello AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-179">On hello **AD FS Servers** page, enter hello server name or IP address toobe added toohello AD FS farm.</span></span>

   ![Серверы AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="8c6f9-181">Нажмите кнопку **Далее**и ознакомиться со статьей hello окончательного **Настройка** страницы.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-181">Click **Next**, and go through hello final **Configure** page.</span></span> <span data-ttu-id="8c6f9-182">После завершения добавления toohello AD FS hello серверы фермы Azure AD Connect будет предоставлена tooverify hello hello параметр подключения.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-182">After Azure AD Connect has finished adding hello servers toohello AD FS farm, you will be given hello option tooverify hello connectivity.</span></span>

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Установка завершена](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="8c6f9-185">Добавление WAP-сервера AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-186">tooadd WAP-сервера Azure AD Connect требуется hello PFX-сертификат.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-186">tooadd a WAP server, Azure AD Connect requires hello PFX certificate.</span></span> <span data-ttu-id="8c6f9-187">Таким образом можно выполнять только операции при настройке фермы hello AD FS с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-187">Therefore, you can only perform this operation if you configured hello AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="8c6f9-188">Выберите **развернуть прокси веб-приложения** hello списке доступных задач.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-188">Select **Deploy Web Application Proxy** from hello list of available tasks.</span></span>

   ![Развертывание прокси-службы веб-приложения](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="8c6f9-190">Укажите учетные данные глобальный администратор Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-190">Provide hello Azure global administrator credentials.</span></span>

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="8c6f9-192">На hello **укажите SSL-сертификат** укажите hello пароль для PFX-файла hello, указанный при настройке фермы hello AD FS с Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-192">On hello **Specify SSL certificate** page, provide hello password for hello PFX file that you provided when you configured hello AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="8c6f9-193">![Пароль сертификата](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="8c6f9-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="8c6f9-195">Добавьте сервер toobe hello, добавления в качестве сервера WAP.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-195">Add hello server toobe added as a WAP server.</span></span> <span data-ttu-id="8c6f9-196">Hello WAP-сервера могут быть присоединены к домену toohello домена, hello мастер запрашивает добавляемом сервере toohello учетные данные администратора.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-196">Because hello WAP server might not be joined toohello domain, hello wizard asks for administrative credentials toohello server being added.</span></span>

   ![Учетные данные администратора сервера](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="8c6f9-198">На hello **учетные данные прокси-сервера доверия** укажите учетные данные администратора tooconfigure hello прокси доверия и доступа hello основной сервер в ферме AD FS hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-198">On hello **Proxy trust credentials** page, provide administrative credentials tooconfigure hello proxy trust and access hello primary server in hello AD FS farm.</span></span>

   ![Учетные данные доверия прокси-сервера](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="8c6f9-200">На hello **готовности tooconfigure** странице приветствия мастера отображаются hello список действий, которые будут выполнены.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-200">On hello **Ready tooconfigure** page, hello wizard shows hello list of actions that will be performed.</span></span>

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="8c6f9-202">Нажмите кнопку **установить** toofinish hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-202">Click **Install** toofinish hello configuration.</span></span> <span data-ttu-id="8c6f9-203">После завершения настройки hello, предоставляет мастер hello hello tooverify параметр hello серверов toohello подключения.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-203">After hello configuration is complete, hello wizard gives you hello option tooverify hello connectivity toohello servers.</span></span> <span data-ttu-id="8c6f9-204">Нажмите кнопку **проверьте** toocheck подключения.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-204">Click **Verify** toocheck connectivity.</span></span>

   ![Установка завершена](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="8c6f9-206">Добавление федеративного домена <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="8c6f9-207">Это легко tooadd toobe домена в федерацию с Azure AD с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-207">It's easy tooadd a domain toobe federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="8c6f9-208">Azure AD Connect добавляет hello домен для федерации и изменяет hello утверждений, правила toocorrectly отражают hello издателя при наличии нескольких доменов в федерацию с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-208">Azure AD Connect adds hello domain for federation and modifies hello claim rules toocorrectly reflect hello issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="8c6f9-209">tooadd федеративный домен, выберите hello задач **добавить дополнительный домен Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-209">tooadd a federated domain, select hello task **Add an additional Azure AD domain**.</span></span>

   ![Дополнительный домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="8c6f9-211">На следующей странице приветствия мастера hello укажите учетные данные глобального администратора hello в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-211">On hello next page of hello wizard, provide hello global administrator credentials for Azure AD.</span></span>

   ![Подключение tooAzure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="8c6f9-213">На hello **учетные данные для удаленного доступа** укажите учетные данные администратора домена hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-213">On hello **Remote access credentials** page, provide hello domain administrator credentials.</span></span>

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="8c6f9-215">На следующей странице приветствия hello мастер предоставляет список доменов Azure AD, которые можно создать федерацию с вашего локального каталога.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-215">On hello next page, hello wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="8c6f9-216">Выберите домен hello из списка hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-216">Choose hello domain from hello list.</span></span>

   ![Домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="8c6f9-218">После выбора домена hello hello мастером вам соответствующую информацию о дальнейших действиях, которые мастер hello примет и влияние настроек hello hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-218">After you choose hello domain, hello wizard provides you with appropriate information about further actions that hello wizard will take and hello impact of hello configuration.</span></span> <span data-ttu-id="8c6f9-219">В некоторых случаях при выборе домена, не еще выполняется в Azure AD hello мастер предоставляет сведения о toohelp проверьте hello домена.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-219">In some cases, if you select a domain that isn't yet verified in Azure AD, hello wizard provides you with information toohelp you verify hello domain.</span></span> <span data-ttu-id="8c6f9-220">В разделе [добавить ваш tooAzure имя пользовательского домена Active Directory](../active-directory-add-domain.md) для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-220">See [Add your custom domain name tooAzure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="8c6f9-221">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-221">Click **Next**.</span></span> <span data-ttu-id="8c6f9-222">Hello **готовности tooconfigure** странице отображаются hello список действий, которые выполняют Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-222">hello **Ready tooconfigure** page shows hello list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="8c6f9-223">Нажмите кнопку **установить** toofinish hello конфигурации.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-223">Click **Install** toofinish hello configuration.</span></span>

   ![Все готово tooconfigure](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="8c6f9-225">Добавить пользователей из hello федеративного домена должна быть синхронизирована, прежде чем их можно будет toologin tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-225">Users from hello added federated domain must be synchronized before they will be able toologin tooAzure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="8c6f9-226">Пользовательская настройка AD FS</span><span class="sxs-lookup"><span data-stu-id="8c6f9-226">AD FS customization</span></span>
<span data-ttu-id="8c6f9-227">Hello следующие разделы содержат сведения о распространенных задач hello, возможно, tooperform во время настройки страницы входа AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-227">hello following sections provide details about some of hello common tasks that you might have tooperform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="8c6f9-228">Добавление настраиваемого логотипа компании или иллюстрации <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="8c6f9-229">Эмблема hello toochange hello компании, которая отображается на hello **входа** , используйте следующий командлет Windows PowerShell и синтаксисом hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-229">toochange hello logo of hello company that's displayed on hello **Sign-in** page, use hello following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-230">Здравствуйте, рекомендуется измерения для hello логотипа — 260 x 35 @ 96 точек на дюйм. размер файла не должен превышать 10 КБ.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-230">hello recommended dimensions for hello logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="8c6f9-231">Hello *TargetName* является обязательным.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-231">hello *TargetName* parameter is required.</span></span> <span data-ttu-id="8c6f9-232">имя по умолчанию — тема по умолчанию Hello, предоставляемая в AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-232">hello default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="8c6f9-233">Добавление описания входа в систему <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="8c6f9-234">tooadd toohello описание страницы входа **страницы входа**, используйте следующий командлет Windows PowerShell и синтаксисом hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-234">tooadd a sign-in page description toohello **Sign-in page**, use hello following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in tooContoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="8c6f9-235">Изменение правил утверждений служб федерации Active Directory <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="8c6f9-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="8c6f9-236">Службы федерации Active Directory поддерживает языка форматированного утверждений, который можно использовать toocreate пользовательские правила утверждений.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-236">AD FS supports a rich claim language that you can use toocreate custom claim rules.</span></span> <span data-ttu-id="8c6f9-237">Дополнительные сведения см. в разделе [hello роль языка правил утверждений hello](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-237">For more information, see [hello Role of hello Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="8c6f9-238">Hello следующих разделах описаны как можно создавать настраиваемые правила для некоторых сценариев, связывающие tooAzure AD и федерации AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-238">hello following sections describe how you can write custom rules for some scenarios that relate tooAzure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-hello-attribute"></a><span data-ttu-id="8c6f9-239">Неизменяемый идентификатор условного по значению их присутствия в атрибуте hello</span><span class="sxs-lookup"><span data-stu-id="8c6f9-239">Immutable ID conditional on a value being present in hello attribute</span></span>
<span data-ttu-id="8c6f9-240">Azure AD Connect позволяет указать атрибут toobe использовать привязку к источнику, если объекты — синхронизироваться tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-240">Azure AD Connect lets you specify an attribute toobe used as a source anchor when objects are synced tooAzure AD.</span></span> <span data-ttu-id="8c6f9-241">Если hello значения настраиваемого атрибута hello не пуст, вы можете tooissue утверждение неизменяемый идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-241">If hello value in hello custom attribute is not empty, you might want tooissue an immutable ID claim.</span></span>

<span data-ttu-id="8c6f9-242">Например, можно выбрать **ms-ds-consistencyguid** как атрибут hello для привязки источника hello и проблема **ImmutableID** как **ms-ds-consistencyguid** в вариантов hello атрибут имеет значение для нее.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-242">For example, you might select **ms-ds-consistencyguid** as hello attribute for hello source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case hello attribute has a value against it.</span></span> <span data-ttu-id="8c6f9-243">Если нет значения для атрибута hello, отправить **objectGuid** как hello неизменяемый идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-243">If there's no value against hello attribute, issue **objectGuid** as hello immutable ID.</span></span> <span data-ttu-id="8c6f9-244">Вы можете создать hello набор настраиваемых правил утверждений, как описано в следующем разделе hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-244">You can construct hello set of custom claim rules as described in hello following section.</span></span>

<span data-ttu-id="8c6f9-245">**Правило 1. Атрибуты запросов**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="8c6f9-246">В этом правиле выполняется запрос значения hello **ms-ds-consistencyguid** и **objectGuid** для hello пользователя из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-246">In this rule, you're querying hello values of **ms-ds-consistencyguid** and **objectGuid** for hello user from Active Directory.</span></span> <span data-ttu-id="8c6f9-247">Измените имя hello хранилища имя tooan соответствующее хранилище в развертывание AD FS.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-247">Change hello store name tooan appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="8c6f9-248">Также изменить тип утверждения, соответствующие tooa типа утверждений hello для федерации, согласно его определению **objectGuid** и **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-248">Also change hello claims type tooa proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="8c6f9-249">Кроме того, с помощью **добавить** и не **проблему**, следует избегать добавления исходящего проблемы для сущности hello и hello значения можно использовать как промежуточные значения.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for hello entity, and can use hello values as intermediate values.</span></span> <span data-ttu-id="8c6f9-250">Будет выдавать hello утверждения в правиле более поздней версии, после установления какие toouse значение как hello неизменяемый идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-250">You will issue hello claim in a later rule after you establish which value toouse as hello immutable ID.</span></span>

<span data-ttu-id="8c6f9-251">**Правило 2: Проверьте, существует ли ms-ds-consistencyguid для пользователя hello**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-251">**Rule 2: Check if ms-ds-consistencyguid exists for hello user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="8c6f9-252">Это правило определяет временной пометку **idflag** , задано слишком**useguid** при наличии не **ms-ds-consistencyguid** заполняется для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-252">This rule defines a temporary flag called **idflag** that is set too**useguid** if there's no **ms-ds-consistencyguid** populated for hello user.</span></span> <span data-ttu-id="8c6f9-253">Hello смысл этого заключается в hello тем, что службы федерации Active Directory не разрешают пустой утверждений.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-253">hello logic behind this is hello fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="8c6f9-254">Поэтому при добавлении утверждений http://contoso.com/ws/2016/02/identity/claims/objectguid и http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid правила 1, вы получаете **msdsconsistencyguid** только если утверждения значение Hello заполняется для пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if hello value is populated for hello user.</span></span> <span data-ttu-id="8c6f9-255">Если оно не заполнено, службы AD FS определяют, что значение окажется пустым, и немедленно его опускают.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="8c6f9-256">**objectGuid**имеют все объекты, поэтому такое утверждение всегда будет присутствовать после выполнения правила 1.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="8c6f9-257">**Правило 3. Выдача ms-ds-consistencyguid в качестве неизменяемого идентификатора, если он присутствует**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="8c6f9-258">Это неявная проверка **Exist** .</span><span class="sxs-lookup"><span data-stu-id="8c6f9-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="8c6f9-259">Если существует значение hello для утверждения hello, затем выполните, как hello неизменяемый идентификатор.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-259">If hello value for hello claim exists, then issue that as hello immutable ID.</span></span> <span data-ttu-id="8c6f9-260">Hello в предыдущем примере hello **nameidentifier** утверждения.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-260">hello previous example uses hello **nameidentifier** claim.</span></span> <span data-ttu-id="8c6f9-261">Вы получите toochange типа toohello соответствующие утверждения для hello неизменяемый идентификатор в вашей среде.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-261">You'll have toochange this toohello appropriate claim type for hello immutable ID in your environment.</span></span>

<span data-ttu-id="8c6f9-262">**Правило 4. Выдача objectGuid в качестве неизменяемого идентификатора при отсутствии ms-ds-consistencyGuid**</span><span class="sxs-lookup"><span data-stu-id="8c6f9-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="8c6f9-263">В этом правиле, просто выполняется проверка hello временные флаг **idflag**.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-263">In this rule, you're simply checking hello temporary flag **idflag**.</span></span> <span data-ttu-id="8c6f9-264">Принято, основаны ли tooissue hello утверждения на его значение.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-264">You decide whether tooissue hello claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="8c6f9-265">Важно соблюдать последовательность Hello этих правил.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-265">hello sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="8c6f9-266">Единый вход с помощью UPN поддомена</span><span class="sxs-lookup"><span data-stu-id="8c6f9-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="8c6f9-267">Можно добавить несколько toobe домена федерации с помощью Azure AD Connect, как описано в [добавьте новый федеративный домен](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-267">You can add more than one domain toobe federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="8c6f9-268">Утверждение имени участника (UPN) пользователя hello необходимо изменить, чтобы hello ИД издателя соответствует toohello корневого домена, а не hello дочерний домен, поскольку hello федеративной корневого домена также охватывает дочерний hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-268">You must modify hello user principal name (UPN) claim so that hello issuer ID corresponds toohello root domain and not hello subdomain, because hello federated root domain also covers hello child.</span></span>

<span data-ttu-id="8c6f9-269">По умолчанию hello правил утверждений для издателя, как будет задан ИД:</span><span class="sxs-lookup"><span data-stu-id="8c6f9-269">By default, hello claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Утверждение идентификатора издателя по умолчанию](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="8c6f9-271">правило по умолчанию Hello принимает суффикс UPN hello и использует его в утверждение идентификатора издателя hello.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-271">hello default rule simply takes hello UPN suffix and uses it in hello issuer ID claim.</span></span> <span data-ttu-id="8c6f9-272">Предположим, Григорий является пользователем в домене sub.contoso.com, а contoso.com включен в федерацию с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="8c6f9-273">Вводит Джон john@sub.contoso.com как hello имя пользователя при входе в tooAzure AD.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-273">John enters john@sub.contoso.com as hello username while signing in tooAzure AD.</span></span> <span data-ttu-id="8c6f9-274">правило утверждения идентификатор издателя по умолчанию Hello в AD FS обработает его в hello, следуя способом:</span><span class="sxs-lookup"><span data-stu-id="8c6f9-274">hello default issuer ID claim rule in AD FS handles it in hello following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="8c6f9-275">**Значение утверждения:** http://sub.contoso.com/adfs/services/trust/.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="8c6f9-276">toohave только hello корневого домена hello поставщиком значение утверждения, измените hello утверждения правило toomatch hello следующее.</span><span class="sxs-lookup"><span data-stu-id="8c6f9-276">toohave only hello root domain in hello issuer claim value, change hello claim rule toomatch hello following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="8c6f9-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="8c6f9-277">Next steps</span></span>
<span data-ttu-id="8c6f9-278">См. [дополнительные сведения о параметрах входа пользователя](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="8c6f9-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
