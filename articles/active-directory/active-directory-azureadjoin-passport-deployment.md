---
title: "Включение Microsoft Windows Hello для бизнеса в организации | Документация Майкрософт"
description: "Инструкции по развертыванию для включения в организации службы Microsoft Passport."
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
ms.openlocfilehash: 58943e1e29755c983e55c675dd4fe7b75ac47b34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-microsoft-windows-hello-for-business-in-your-organization"></a><span data-ttu-id="a8f5d-104">Включение Microsoft Windows Hello для бизнеса в организации</span><span class="sxs-lookup"><span data-stu-id="a8f5d-104">Enable Microsoft Windows Hello for Business in your organization</span></span>
<span data-ttu-id="a8f5d-105">После [подключения присоединенных к домену устройств Windows 10 к Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md) выполните следующую процедуру, чтобы включить Microsoft Windows Hello для бизнеса в организации:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-105">After [connecting Windows 10 domain-joined devices with Azure Active Directory](active-directory-azureadjoin-devices-group-policy.md), do the following to enable Microsoft Windows Hello for Business in your organization:</span></span>

1. <span data-ttu-id="a8f5d-106">Развертывание System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a8f5d-106">Deploy System Center Configuration Manager</span></span>  
2. <span data-ttu-id="a8f5d-107">Настройка параметров политики</span><span class="sxs-lookup"><span data-stu-id="a8f5d-107">Configure policy settings</span></span>
3. <span data-ttu-id="a8f5d-108">Настройка профиля сертификата</span><span class="sxs-lookup"><span data-stu-id="a8f5d-108">Configure the certificate profile</span></span>  

## <a name="deploy-system-center-configuration-manager"></a><span data-ttu-id="a8f5d-109">Развертывание System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a8f5d-109">Deploy System Center Configuration Manager</span></span>
<span data-ttu-id="a8f5d-110">Для развертывания сертификатов пользователей на основе ключей Windows Hello для бизнеса необходимо следующее:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-110">To deploy user certificates based on Windows Hello for Business keys, you need the following:</span></span>

* <span data-ttu-id="a8f5d-111">**System Center Configuration Manager (текущая версия)**. Необходимо установить версию 1606 или более позднюю.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-111">**System Center Configuration Manager Current Branch** - You need to install version 1606 or better.</span></span> <span data-ttu-id="a8f5d-112">Дополнительные сведения см. в [документации по System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) и [блоге рабочей группы по System Center Configuration Manager](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8f5d-112">For more information, see the [Documentation for System Center Configuration Manager](https://technet.microsoft.com/library/mt346023.aspx) and [System Center Configuration Manager Team Blog](http://blogs.technet.com/b/configmgrteam/archive/2015/09/23/now-available-update-for-system-center-config-manager-tp3.aspx).</span></span>
* <span data-ttu-id="a8f5d-113">**Инфраструктура открытых ключей (PKI)**. Для поддержки использования сертификатов пользователей службой Microsoft Windows Hello для бизнеса необходима инфраструктура PKI.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-113">**Public key infrastructure (PKI)** - To enable Microsoft Windows Hello for Business by using user certificates, you must have a PKI in place.</span></span> <span data-ttu-id="a8f5d-114">Если она отсутствует или вы не хотите использовать ее для сертификатов пользователей, то вы можете развернуть новый контроллер домена с установленной сборкой 10551 (или более поздней версии) Windows Server 2016.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-114">If you don’t have one, or you don’t want to use it for user certificates, you can deploy a new domain controller that has Windows Server 2016 build 10551 (or better) installed.</span></span> <span data-ttu-id="a8f5d-115">Выполните процедуру по [установке реплики контроллера домена в существующем домене](https://technet.microsoft.com/library/jj574134.aspx) или [установке нового леса Active Directory при создании новой среды](https://technet.microsoft.com/library/jj574166).</span><span class="sxs-lookup"><span data-stu-id="a8f5d-115">Follow the steps to [install a replica domain controller in an existing domain](https://technet.microsoft.com/library/jj574134.aspx) or to [install a new Active Directory forest, if you're creating a new environment](https://technet.microsoft.com/library/jj574166).</span></span> <span data-ttu-id="a8f5d-116">(Образы ISO доступны для скачивания на странице [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span><span class="sxs-lookup"><span data-stu-id="a8f5d-116">(The ISOs are available for download on [Signiant Media Exchange](https://datatransfer.microsoft.com/signiant_media_exchange/spring/main?sdkAccessible=true).)</span></span>

## <a name="configure-policy-settings"></a><span data-ttu-id="a8f5d-117">Настройка параметров политики</span><span class="sxs-lookup"><span data-stu-id="a8f5d-117">Configure policy settings</span></span>
<span data-ttu-id="a8f5d-118">Существует два варианта настройки параметров политики Microsoft Windows Hello для бизнеса:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-118">To configure the Microsoft Windows Hello for Business policy settings, you have two options:</span></span>

* <span data-ttu-id="a8f5d-119">групповая политика в Active Directory;</span><span class="sxs-lookup"><span data-stu-id="a8f5d-119">Group Policy in Active Directory</span></span> 
* <span data-ttu-id="a8f5d-120">System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-120">The System Center Configuration Manager</span></span> 

<span data-ttu-id="a8f5d-121">Для настройки параметров политики Microsoft Windows Hello для бизнеса рекомендуется использовать групповую политику в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-121">Using Group Policy in Active Directory is the recommended method to configure Microsoft Windows Hello for Business policy settings.</span></span> 

<span data-ttu-id="a8f5d-122">Использование System Center Configuration Manager также является предпочтительным методом при развертывании сертификатов.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-122">Using System Center Configuration Manager is the preferred method when you also use it to deploy certificates.</span></span> <span data-ttu-id="a8f5d-123">Данный сценарий:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-123">This scenario:</span></span>

* <span data-ttu-id="a8f5d-124">обеспечивает совместимость с более новыми сценариями развертывания;</span><span class="sxs-lookup"><span data-stu-id="a8f5d-124">Ensures compatibility with the newer deployment scenarios</span></span>
* <span data-ttu-id="a8f5d-125">требует на стороне клиента наличие Windows 10 версии 1607 или более новой.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-125">Requires on the client side Windows 10 Version 1607 or better.</span></span>

### <a name="configure-microsoft-windows-hello-for-business-via-group-policy-in-active-directory"></a><span data-ttu-id="a8f5d-126">Настройка Microsoft Windows Hello для бизнеса с помощью групповой политики в Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8f5d-126">Configure Microsoft Windows Hello for Business via group policy in Active Directory</span></span>
<span data-ttu-id="a8f5d-127">**Шаги**:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-127">**Steps**:</span></span>

1. <span data-ttu-id="a8f5d-128">Откройте диспетчер серверов и выберите **Инструменты** > **Управление групповой политикой**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-128">Open Server Manager, and navigate to **Tools** > **Group Policy Management**.</span></span>
2. <span data-ttu-id="a8f5d-129">В разделе "Управление групповой политикой" перейдите к узлу, соответствующему домену, для которого необходимо включить присоединение к Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-129">From Group Policy Management, navigate to the domain node that corresponds to the domain in which you want to enable Azure AD Join.</span></span>
3. <span data-ttu-id="a8f5d-130">Щелкните правой кнопкой мыши **Объекты групповой политики** и выберите **Создать**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-130">Right-click **Group Policy Objects**, and select **New**.</span></span> <span data-ttu-id="a8f5d-131">Укажите имя объекта групповой политики, например "Включение Windows Hello для бизнеса".</span><span class="sxs-lookup"><span data-stu-id="a8f5d-131">Give your Group Policy Object a name, for example, Enable Windows Hello for Business.</span></span> <span data-ttu-id="a8f5d-132">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-132">Click **OK**.</span></span>
4. <span data-ttu-id="a8f5d-133">Щелкните правой кнопкой мыши новый объект групповой политики и выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-133">Right-click your new Group Policy Object, and then select **Edit**.</span></span>
5. <span data-ttu-id="a8f5d-134">Последовательно выберите **Конфигурация компьютера** > **Политики** > **Административные шаблоны** > **Компоненты Windows** > **Windows Hello для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-134">Navigate to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Windows Hello for Business**.</span></span>
6. <span data-ttu-id="a8f5d-135">Щелкните правой кнопкой мыши **Enable Windows Hello for Business** (Включить Windows Hello для бизнеса), а затем выберите пункт **Изменить**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-135">Right-click **Enable Windows Hello for Business**, and then select **Edit**.</span></span>
7. <span data-ttu-id="a8f5d-136">Установите переключатель в положение **Включено**, а затем щелкните **Применить**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-136">Select the **Enabled** option button, and then click **Apply**.</span></span> <span data-ttu-id="a8f5d-137">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-137">Click **OK**.</span></span>
8. <span data-ttu-id="a8f5d-138">Теперь вы можете связать объект групповой политики с выбранным расположением.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-138">You can now link the Group Policy Object to a location of your choice.</span></span> <span data-ttu-id="a8f5d-139">Чтобы включить эту политику для всех присоединенных к домену устройств Windows 10 в организации, свяжите групповую политику с доменом.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-139">To enable this policy for all of the domain-joined Windows 10 devices in your organization, link the Group Policy to the domain.</span></span> <span data-ttu-id="a8f5d-140">Например:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-140">For example:</span></span>
   * <span data-ttu-id="a8f5d-141">с определенным подразделением в Active Directory, в котором будут размещаться компьютеры Windows 10, присоединенные к домену;</span><span class="sxs-lookup"><span data-stu-id="a8f5d-141">A specific organizational unit (OU) in Active Directory where Windows 10 domain-joined computers will be located</span></span>
   * <span data-ttu-id="a8f5d-142">с определенной группой безопасности, содержащей присоединенные к домену компьютеры Windows 10, для которых будет выполняться автоматическая регистрация в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-142">A specific security group that contains Windows 10 domain-joined computers that will be automatically registered with Azure AD</span></span>

### <a name="configure-windows-hello-for-business-using-system-center-configuration-manager"></a><span data-ttu-id="a8f5d-143">Настройка Windows Hello для бизнеса с помощью System Center Configuration Manager</span><span class="sxs-lookup"><span data-stu-id="a8f5d-143">Configure Windows Hello for Business using System Center Configuration Manager</span></span>
<span data-ttu-id="a8f5d-144">**Шаги**:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-144">**Steps**:</span></span>

1. <span data-ttu-id="a8f5d-145">Откройте **System Center Configuration Manager** и перейдите к разделу **Assets & Compliance > Параметры соответствия > Доступ к ресурсам компании > Профили Windows Hello для бизнеса** (Ресурсы и соответствие).</span><span class="sxs-lookup"><span data-stu-id="a8f5d-145">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Windows Hello for Business Profiles**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/01.png)
2. <span data-ttu-id="a8f5d-147">На панели инструментов в верхней части щелкните **Создать профиль Windows Hello для бизнеса**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-147">In the toolbar on the top, click **Create Windows Hello for business Profile**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/02.png)
3. <span data-ttu-id="a8f5d-149">В диалоговом окне **Общие** выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-149">On the **General** dialog, perform the following steps:</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/03.png)
   
    <span data-ttu-id="a8f5d-151">а.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-151">a.</span></span> <span data-ttu-id="a8f5d-152">В текстовом поле **Имя** введите имя профиля, например **Мой профиль WHfB**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-152">In the **Name** textbox, type a name for your profile, for example, **My WHfB Profile**.</span></span>
   
    <span data-ttu-id="a8f5d-153">b.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-153">b.</span></span> <span data-ttu-id="a8f5d-154">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-154">Click **Next**.</span></span>
4. <span data-ttu-id="a8f5d-155">В диалоговом окне **Поддерживаемые платформы** выберите платформы, которые будут подготовлены с помощью этого профиля Windows Hello для бизнеса, и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-155">On the **Supported Platforms** dialog, select the platforms that will be provisioned with this Windows Hello for business profile, and then click **Next**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/04.png)
5. <span data-ttu-id="a8f5d-157">В диалоговом окне **Параметры** выполните следующее:</span><span class="sxs-lookup"><span data-stu-id="a8f5d-157">On the **Settings** dialog, perform the following steps:</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/05.png)
   
    <span data-ttu-id="a8f5d-159">а.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-159">a.</span></span> <span data-ttu-id="a8f5d-160">Для параметра **Настройка Windows Hello для бизнеса** выберите значение **Включено**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-160">As **Configure Windows Hello for Business**, select **Enabled**.</span></span>
   
    <span data-ttu-id="a8f5d-161">b.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-161">b.</span></span> <span data-ttu-id="a8f5d-162">Для параметра **Использовать доверенный платформенный модуль (TPM)** выберите **Требуется**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-162">As **Use a Trusted Platform Module (TPM)**, select **Required**.</span></span> 
   
    <span data-ttu-id="a8f5d-163">c.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-163">c.</span></span> <span data-ttu-id="a8f5d-164">Для параметра **Способ проверки подлинности** выберите значение **На основе сертификата**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-164">As **Authentication method**, select **Certificate-based**.</span></span>
   
    <span data-ttu-id="a8f5d-165">d.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-165">d.</span></span> <span data-ttu-id="a8f5d-166">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-166">Click **Next**.</span></span>
6. <span data-ttu-id="a8f5d-167">В диалоговом окне **Сводка** нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-167">On the **Summary** dialog, click **Next**.</span></span>
7. <span data-ttu-id="a8f5d-168">В диалоговом окне **Завершение** нажмите кнопку **Закрыть**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-168">On the **Completion** dialog, click **Close**.</span></span>
8. <span data-ttu-id="a8f5d-169">На панели инструментов в верхней части экрана щелкните **Развернуть**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-169">In the toolbar on the top, click **Deploy**.</span></span>
   
    ![Настройка Windows Hello для бизнеса](./media/active-directory-azureadjoin-passport-deployment/06.png)

## <a name="configure-the-certificate-profile"></a><span data-ttu-id="a8f5d-171">Настройка профиля сертификата</span><span class="sxs-lookup"><span data-stu-id="a8f5d-171">Configure the certificate profile</span></span>
<span data-ttu-id="a8f5d-172">При использовании аутентификации на основе сертификатов для локальной аутентификации необходимо настроить и развернуть профиль сертификата.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-172">If you are using certificate-based authentication for on-premises authentication, you need to configure and deploy a certificate profile.</span></span> <span data-ttu-id="a8f5d-173">Для этого нужно настроить сервер NDES и роль сайта "Точка регистрации сертификатов" в System Center Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-173">This task requires you to set up an NDES server and Certificate Registration Point site role in the System Center Configuration Manager.</span></span> <span data-ttu-id="a8f5d-174">Дополнительные сведения см. в статье [Необходимые условия для профилей сертификатов в Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span><span class="sxs-lookup"><span data-stu-id="a8f5d-174">For more details, see the [Prerequisites for Certificate Profiles in Configuration Manager](https://technet.microsoft.com/library/dn261205.aspx).</span></span>

1. <span data-ttu-id="a8f5d-175">Откройте **System Center Configuration Manager** и перейдите к разделу **Assets & Compliance > Параметры соответствия > Доступ к ресурсам компании > Профили сертификатов** (Ресурсы и соответствие).</span><span class="sxs-lookup"><span data-stu-id="a8f5d-175">Open the **System Center Configuration Manager**, and then navigate to **Assets & Compliance > Compliance Settings > Company Resource Access > Certificate Profiles**.</span></span>
2. <span data-ttu-id="a8f5d-176">Выберите шаблон с EKU входа со смарт-картой.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-176">Select a template that has Smart Card sign-in extended key usage (EKU).</span></span>

<span data-ttu-id="a8f5d-177">На странице **Регистрация SCEP** профиля сертификата выберите для параметра **Поставщик хранилища ключей** значение **Установить в Passport for Work, в ином случае — выдать отказ**.</span><span class="sxs-lookup"><span data-stu-id="a8f5d-177">On the **SCEP Enrollment** page of the certificate profile, you need to choose **Install to Passport for Work otherwise fail** as the **Key Storage Provider**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a8f5d-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a8f5d-178">Next steps</span></span>
* [<span data-ttu-id="a8f5d-179">Windows 10 для предприятия: использование устройств для работы</span><span class="sxs-lookup"><span data-stu-id="a8f5d-179">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="a8f5d-180">Использование возможностей облачных служб на устройствах с Windows 10 с помощью присоединения к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="a8f5d-180">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="a8f5d-181">Проверка подлинности удостоверений без использования паролей с помощью службы Microsoft Passport</span><span class="sxs-lookup"><span data-stu-id="a8f5d-181">Authenticating identities without passwords through Microsoft Passport</span></span>](active-directory-azureadjoin-passport.md)
* [<span data-ttu-id="a8f5d-182">Сценарии использования для присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8f5d-182">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="a8f5d-183">Подключение присоединенных к домену устройств к Azure AD для работы в Windows 10</span><span class="sxs-lookup"><span data-stu-id="a8f5d-183">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="a8f5d-184">Настройка присоединения к Azure AD</span><span class="sxs-lookup"><span data-stu-id="a8f5d-184">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

