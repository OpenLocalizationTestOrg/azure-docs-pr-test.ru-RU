---
title: "aaaEnable Microsoft Windows Hello для бизнеса в вашей организации | Документы Microsoft"
description: "Развертывание инструкции tooenable Microsoft Passport в вашей организации."
services: active-directory
documentationcenter: 
keywords: "настройка Microsoft Passport, развертывание Microsoft Windows Hello для бизнеса"
author: MarkusVi
manager: femila
tags: azure-classic-portal
ms.assetid: 7dbbe3c6-1cd7-429c-a9b2-115fcbc02416
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: 6041f5916f606752bc55844b1b2d0a423b913cd3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="44415-104">Включение Microsoft Windows Hello для бизнеса в организации</span><span class="sxs-lookup"><span data-stu-id="44415-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="44415-105">После [подключение устройств, присоединенных к домену Windows 10 с Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), hello следующие tooenable Microsoft Windows Hello для бизнеса в вашей организации:</span><span class="sxs-lookup"><span data-stu-id="44415-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do hello following tooenable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="44415-106">Развертывание System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="44415-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="44415-107">Настройка параметров политики</span><span class="sxs-lookup"><span data-stu-id="44415-107">Configure policy settings</span></span>
3. <span data-ttu-id="44415-108">Настройка профиля сертификата hello</span><span class="sxs-lookup"><span data-stu-id="44415-108">Configure hello certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="44415-109">Развертывание System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="44415-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="44415-110">toodeploy пользователя сертификаты на основе Windows Hello для бизнес-ключи, необходимы следующие hello.</span><span class="sxs-lookup"><span data-stu-id="44415-110">toodeploy user certificates based on Windows Hello for Business keys, you need hello following:</span></span>

* <span data-ttu-id="44415-111">**Текущей ветви System Center Configuration Manager** -требуется tooinstall версии 1606 или более поздней.</span><span class="sxs-lookup"><span data-stu-id="44415-111">**System Center Configuration Manager Current Branch** - You need tooinstall version 1606 or better.</span></span> <span data-ttu-id="44415-112">Дополнительные сведения см. в разделе hello [документации для System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) и [блог группы System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="44415-112">For more information, see hello [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="44415-113">**Инфраструктуры открытых ключей (PKI)** -tooenable Microsoft Windows Hello для бизнеса с помощью пользовательских сертификатов, необходимо иметь PKI на месте.</span><span class="sxs-lookup"><span data-stu-id="44415-113">**Public key infrastructure (PKI)** - tooenable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="44415-114">Если у вас его нет, или вы не хотите toouse его для сертификатов пользователей, можно развернуть новый контроллер домена с Windows Server 2016 построения 10551 (или выше) установлен.</span><span class="sxs-lookup"><span data-stu-id="44415-114">If you don’t have one, or you don’t want toouse it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="44415-115">Выполните действия hello слишком[Установка реплики контроллера домена в существующем домене](https://technet.microsoft.com/library/jj574134.aspx) или слишком[Установка нового леса Active Directory, если вы создаете новую среду](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="44415-115">Follow hello steps too[install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or too[install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="44415-116">(hello образы ISO доступны для загрузки на [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="44415-116">(hello ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="44415-117">Настройка параметров политики</span><span class="sxs-lookup"><span data-stu-id="44415-117">Configure policy settings</span></span>
<span data-ttu-id="44415-118">hello tooconfigure Microsoft Windows Hello для бизнеса параметров политики можно использовать два варианта:</span><span class="sxs-lookup"><span data-stu-id="44415-118">tooconfigure hello Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="44415-119">групповая политика в Active Directory;</span><span class="sxs-lookup"><span data-stu-id="44415-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="44415-120">Hello System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="44415-120">hello System Center Configuration Manager</span></span> 

<span data-ttu-id="44415-121">Благодаря использованию групповой политики в Active Directory — hello, рекомендуется использовать метод tooconfigure Microsoft Windows Hello для бизнеса параметров политики.</span><span class="sxs-lookup"><span data-stu-id="44415-121">Using Group Policy in Active Directory is hello recommended method tooconfigure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="44415-122">С помощью System Center Configuration Manager — hello предпочтительный метод, можно также использовать сертификаты toodeploy.</span><span class="sxs-lookup"><span data-stu-id="44415-122">Using System Center Configuration Manager is hello preferred method when you also use it toodeploy certificates.</span></span> <span data-ttu-id="44415-123">Данный сценарий:</span><span class="sxs-lookup"><span data-stu-id="44415-123">This scenario:</span></span>

* <span data-ttu-id="44415-124">Обеспечивает совместимость с более новые сценарии развертывания hello</span><span class="sxs-lookup"><span data-stu-id="44415-124">Ensures compatibility with hello newer deployment scenarios</span></span>
* <span data-ttu-id="44415-125">Требуется на стороне клиента hello Windows 10 версии 1607 или выше.</span><span class="sxs-lookup"><span data-stu-id="44415-125">Requires on hello client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="44415-126">Настройка Microsoft Windows Hello для бизнеса с помощью групповой политики в Active Directory</span><span class="sxs-lookup"><span data-stu-id="44415-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="44415-127">**Шаги**:</span><span class="sxs-lookup"><span data-stu-id="44415-127">**Steps**:</span></span>

1. <span data-ttu-id="44415-128">Откройте диспетчер сервера и перейдите слишком**средства** > **Управление групповой политикой**.</span><span class="sxs-lookup"><span data-stu-id="44415-128">Open Server Manager, and navigate too**Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="44415-129">Управление групповой политикой перейдите toohello узел домена, соответствующий toohello домен, в котором нужно tooenable присоединения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44415-129">From Group Policy Management, navigate toohello domain node that corresponds toohello domain in which you want tooenable Azure AD Join.</span></span>
3. <span data-ttu-id="44415-130">Щелкните правой кнопкой мыши **Объекты групповой политики** и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="44415-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="44415-131">Укажите имя объекта групповой политики, например "Включение Windows Hello для бизнеса".</span><span class="sxs-lookup"><span data-stu-id="44415-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="44415-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44415-132">Click **OK**.</span></span>
4. <span data-ttu-id="44415-133">Щелкните правой кнопкой мыши новый объект групповой политики и выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="44415-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="44415-134">Перейдите в слишком**Конфигурация компьютера** > **политики** > **административные шаблоны** > **Windows Компоненты** > **Windows Hello для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="44415-134">Navigate too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="44415-135">Щелкните правой кнопкой мыши **Enable Windows Hello for Business** (Включить Windows Hello для бизнеса), а затем выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="44415-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="44415-136">Выберите hello **включено** переключатель, а затем нажмите кнопку **применить**.</span><span class="sxs-lookup"><span data-stu-id="44415-136">Select hello **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="44415-137">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="44415-137">Click **OK**.</span></span>
8. <span data-ttu-id="44415-138">Теперь можно связать hello объекта групповой политики tooa местом по своему усмотрению.</span><span class="sxs-lookup"><span data-stu-id="44415-138">You can now link hello Group Policy Object tooa location of your choice.</span></span> <span data-ttu-id="44415-139">tooenable эту политику для всех hello присоединенных к домену устройств Windows 10 в вашей организации toohello групповой политики домена для связи hello.</span><span class="sxs-lookup"><span data-stu-id="44415-139">tooenable this policy for all of hello domain-joined Windows 10 devices in your organization, link hello Group Policy toohello domain.</span></span> <span data-ttu-id="44415-140">Например:</span><span class="sxs-lookup"><span data-stu-id="44415-140">For example:</span></span>
   * <span data-ttu-id="44415-141">с определенным подразделением в Active Directory, в котором будут размещаться компьютеры Windows 10, присоединенные к домену;</span><span class="sxs-lookup"><span data-stu-id="44415-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="44415-142">с определенной группой безопасности, содержащей присоединенные к домену компьютеры Windows 10, для которых будет выполняться автоматическая регистрация в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="44415-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="44415-143">Настройка Windows Hello для бизнеса с помощью System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="44415-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="44415-144">**Шаги**:</span><span class="sxs-lookup"><span data-stu-id="44415-144">**Steps**:</span></span>

1. <span data-ttu-id="44415-145">Откройте hello **System Center Configuration Manager**и перейдите слишком**активы и соответствие нормативным требованиям > Параметры соответствия > доступ к ресурсам компании > Windows Hello для бизнес-профили**.</span><span class="sxs-lookup"><span data-stu-id="44415-145">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="44415-147">Щелкните hello панели инструментов в верхней части hello **создать Windows Hello для бизнеса профиль**.</span><span class="sxs-lookup"><span data-stu-id="44415-147">In hello toolbar on hello top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="44415-149">На hello **Общие** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="44415-149">On hello **General** dialog, perform hello following steps:</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="44415-151">а.</span><span class="sxs-lookup"><span data-stu-id="44415-151">a.</span></span> <span data-ttu-id="44415-152">В hello **имя** текстовом поле введите имя для своего профиля, например, **Мой профиль WHfB**.</span><span class="sxs-lookup"><span data-stu-id="44415-152">In hello **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="44415-153">b.</span><span class="sxs-lookup"><span data-stu-id="44415-153">b.</span></span> <span data-ttu-id="44415-154">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44415-154">Click **Next**.</span></span>
4. <span data-ttu-id="44415-155">На hello **поддерживаемые платформы** диалоговое окно, выберите hello платформы, будет использован этот Windows Hello для бизнес-профиль и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44415-155">On hello **Supported Platforms** dialog, select hello platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="44415-157">На hello **параметры** диалоговое окно, выполните следующие шаги hello:</span><span class="sxs-lookup"><span data-stu-id="44415-157">On hello **Settings** dialog, perform hello following steps:</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="44415-159">а.</span><span class="sxs-lookup"><span data-stu-id="44415-159">a.</span></span> <span data-ttu-id="44415-160">Для параметра **Настройка Windows Hello для бизнеса** выберите значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="44415-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="44415-161">b.</span><span class="sxs-lookup"><span data-stu-id="44415-161">b.</span></span> <span data-ttu-id="44415-162">Для параметра **Использовать доверенный платформенный модуль (TPM)** выберите **Требуется**.</span><span class="sxs-lookup"><span data-stu-id="44415-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="44415-163">c.</span><span class="sxs-lookup"><span data-stu-id="44415-163">c.</span></span> <span data-ttu-id="44415-164">Для параметра **Способ проверки подлинности** выберите значение **На основе сертификата**.</span><span class="sxs-lookup"><span data-stu-id="44415-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="44415-165">d.</span><span class="sxs-lookup"><span data-stu-id="44415-165">d.</span></span> <span data-ttu-id="44415-166">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44415-166">Click **Next**.</span></span>
6. <span data-ttu-id="44415-167">На hello **Сводка** диалоговое окно, нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="44415-167">On hello **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="44415-168">На hello **завершения** диалоговое окно, нажмите кнопку **закрыть**.</span><span class="sxs-lookup"><span data-stu-id="44415-168">On hello **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="44415-169">Щелкните hello панели инструментов в верхней части hello **развернуть**.</span><span class="sxs-lookup"><span data-stu-id="44415-169">In hello toolbar on hello top, click **Deploy**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-hello-certificate-profile"></a><span data-ttu-id="44415-171">Настройка профиля сертификата hello</span><span class="sxs-lookup"><span data-stu-id="44415-171">Configure hello certificate profile</span></span>
<span data-ttu-id="44415-172">При использовании проверки подлинности на основе сертификатов для проверки подлинности в локальной среде требуется tooconfigure и развертывание профиля сертификата.</span><span class="sxs-lookup"><span data-stu-id="44415-172">If you are using certificate-based authentication for on-premises authentication, you need tooconfigure and deploy a certificate profile.</span></span> <span data-ttu-id="44415-173">Эта задача требует tooset NDES-сервер, и роли сайта точки регистрации сертификатов в System Center Configuration Manager hello.</span><span class="sxs-lookup"><span data-stu-id="44415-173">This task requires you tooset up an NDES server and Certificate Registration Point site role in hello System Center Configuration Manager.</span></span> <span data-ttu-id="44415-174">Дополнительные сведения см. в разделе hello [необходимые условия для профилей сертификатов в Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="44415-174">For more details, see hello [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="44415-175">Привет открыть **System Center Configuration Manager**, а затем переходить слишком**активы и соответствие нормативным требованиям > параметров соответствия требованиям > доступ к ресурсам компании > профилей сертификатов**.</span><span class="sxs-lookup"><span data-stu-id="44415-175">Open hello **System Center Configuration Manager**, and then navigate too**Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="44415-176">Выберите шаблон с EKU входа со смарт-картой.</span><span class="sxs-lookup"><span data-stu-id="44415-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="44415-177">На hello **регистрация SCEP** страницы приветствия профиль сертификата, вы должны toochoose **tooPassport для работы в противном случае сбой установки** как hello **поставщик хранилища ключей**.</span><span class="sxs-lookup"><span data-stu-id="44415-177">On hello **SCEP Enrollment** page of hello certificate profile, you need toochoose **Install tooPassport for Work otherwise fail** as hello **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44415-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44415-178">Next steps</span></span>
* [<span data-ttu-id="44415-179">Windows 10 для предприятия hello: способов toouse устройств для работы</span><span class="sxs-lookup"><span data-stu-id="44415-179">Windows 10 for hello enterprise: Ways toouse devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="44415-180">Расширение облака возможности tooWindows 10 устройствами с помощью присоединения Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="44415-180">Extending cloud capabilities tooWindows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="44415-181">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="44415-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="44415-182">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="44415-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="44415-183">Подключитесь к домену устройства tooAzure AD для Windows 10</span><span class="sxs-lookup"><span data-stu-id="44415-183">Connect domain-joined devices tooAzure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="44415-184">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="44415-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

