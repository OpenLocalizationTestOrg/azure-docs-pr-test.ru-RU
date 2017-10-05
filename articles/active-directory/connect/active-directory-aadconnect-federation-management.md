---
title: "Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect | Документация Майкрософт"
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
ms.openlocfilehash: 14f03542a6553c5bb697192828368ffe6b96441c
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/18/2017
---
# <a name="manage-and-customize-active-directory-federation-services-by-using-azure-ad-connect"></a><span data-ttu-id="9dd33-104">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="9dd33-104">Manage and customize Active Directory Federation Services by using Azure AD Connect</span></span>
<span data-ttu-id="9dd33-105">В этой статье описывается управление службами федерации Active Directory (AD FS) и их настройка с помощью Azure Active Directory (Azure AD) Connect,</span><span class="sxs-lookup"><span data-stu-id="9dd33-105">This article describes how to manage and customize Active Directory Federation Services (AD FS) by using Azure Active Directory (Azure AD) Connect.</span></span> <span data-ttu-id="9dd33-106">а также рассматриваются другие стандартные задачи AD FS, которые может потребоваться выполнить для полной настройки фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-106">It also includes other common AD FS tasks that you might need to do for a complete configuration of an AD FS farm.</span></span>

| <span data-ttu-id="9dd33-107">Раздел</span><span class="sxs-lookup"><span data-stu-id="9dd33-107">Topic</span></span> | <span data-ttu-id="9dd33-108">Что описывает</span><span class="sxs-lookup"><span data-stu-id="9dd33-108">What it covers</span></span> |
|:--- |:--- |
| <span data-ttu-id="9dd33-109">**Управление AD FS**</span><span class="sxs-lookup"><span data-stu-id="9dd33-109">**Manage AD FS**</span></span> | |
| [<span data-ttu-id="9dd33-110">Восстановление доверия</span><span class="sxs-lookup"><span data-stu-id="9dd33-110">Repair the trust</span></span>](#repairthetrust) |<span data-ttu-id="9dd33-111">Восстановление доверия федерации с Office 365.</span><span class="sxs-lookup"><span data-stu-id="9dd33-111">How to repair the federation trust with Office 365.</span></span> |
| [<span data-ttu-id="9dd33-112">Федерация с Azure AD с помощью альтернативного имени пользователя</span><span class="sxs-lookup"><span data-stu-id="9dd33-112">Federate with Azure AD using alternate login ID </span></span>](#alternateid) | <span data-ttu-id="9dd33-113">Настройка федерации с использованием альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-113">Configure federation using alternate login ID</span></span>  |
| [<span data-ttu-id="9dd33-114">Добавление сервера AD FS</span><span class="sxs-lookup"><span data-stu-id="9dd33-114">Add an AD FS server</span></span>](#addadfsserver) |<span data-ttu-id="9dd33-115">Расширение фермы AD FS с использованием дополнительного сервера AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-115">How to expand an AD FS farm with an additional AD FS server.</span></span> |
| [<span data-ttu-id="9dd33-116">Добавление прокси-сервера веб-приложения AD FS</span><span class="sxs-lookup"><span data-stu-id="9dd33-116">Add an AD FS Web Application Proxy server</span></span>](#addwapserver) |<span data-ttu-id="9dd33-117">Добавление к ферме AD FS дополнительного сервера прокси-службы веб-приложения (WAP).</span><span class="sxs-lookup"><span data-stu-id="9dd33-117">How to expand an AD FS farm with an additional Web Application Proxy (WAP) server.</span></span> |
| [<span data-ttu-id="9dd33-118">Добавление федеративного домена</span><span class="sxs-lookup"><span data-stu-id="9dd33-118">Add a federated domain</span></span>](#addfeddomain) |<span data-ttu-id="9dd33-119">Добавление федеративного домена.</span><span class="sxs-lookup"><span data-stu-id="9dd33-119">How to add a federated domain.</span></span> |
| [<span data-ttu-id="9dd33-120">Обновление SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="9dd33-120">Update the SSL certificate</span></span>](active-directory-aadconnectfed-ssl-update.md)| <span data-ttu-id="9dd33-121">Обновление SSL-сертификата для фермы AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-121">How to update the SSL certificate for an AD FS farm.</span></span> |
| <span data-ttu-id="9dd33-122">**Настройка AD FS**</span><span class="sxs-lookup"><span data-stu-id="9dd33-122">**Customize AD FS**</span></span> | |
| [<span data-ttu-id="9dd33-123">Добавление настраиваемого логотипа компании или иллюстрации</span><span class="sxs-lookup"><span data-stu-id="9dd33-123">Add a custom company logo or illustration</span></span>](#customlogo) |<span data-ttu-id="9dd33-124">Настройка логотипа компании и иллюстрации для страницы входа AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-124">How to customize an AD FS sign-in page with a company logo and illustration.</span></span> |
| [<span data-ttu-id="9dd33-125">Добавление описания входа в систему</span><span class="sxs-lookup"><span data-stu-id="9dd33-125">Add a sign-in description</span></span>](#addsignindescription) |<span data-ttu-id="9dd33-126">Добавление описания страницы входа в систему.</span><span class="sxs-lookup"><span data-stu-id="9dd33-126">How to add a sign-in page description.</span></span> |
| [<span data-ttu-id="9dd33-127">Изменение правил утверждений служб федерации Active Directory</span><span class="sxs-lookup"><span data-stu-id="9dd33-127">Modify AD FS claim rules</span></span>](#modclaims) |<span data-ttu-id="9dd33-128">Изменение утверждений AD FS для различных сценариев федерации.</span><span class="sxs-lookup"><span data-stu-id="9dd33-128">How to modify AD FS claims for various federation scenarios.</span></span> |

## <a name="manage-ad-fs"></a><span data-ttu-id="9dd33-129">Управление AD FS</span><span class="sxs-lookup"><span data-stu-id="9dd33-129">Manage AD FS</span></span>
<span data-ttu-id="9dd33-130">В Azure AD Connect можно выполнять разные связанные с AD FS задачи с помощью мастера Azure AD Connect с минимальным участием пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-130">You can perform various AD FS-related tasks in Azure AD Connect with minimal user intervention by using the Azure AD Connect wizard.</span></span> <span data-ttu-id="9dd33-131">Завершив установку Azure AD Connect с помощью мастера, вы можете снова запустить этот мастер, чтобы выполнить дополнительные задачи.</span><span class="sxs-lookup"><span data-stu-id="9dd33-131">After you've finished installing Azure AD Connect by running the wizard, you can run the wizard again to perform additional tasks.</span></span>

## <span data-ttu-id="9dd33-132">Восстановление доверия <a name=repairthetrust></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-132">Repair the trust <a name=repairthetrust></a></span></span>
<span data-ttu-id="9dd33-133">Azure AD Connect может проверить текущую работоспособность AD FS и доверие Azure AD и предпринять соответствующие действия для восстановления доверия.</span><span class="sxs-lookup"><span data-stu-id="9dd33-133">You can use Azure AD Connect to check the current health of the AD FS and Azure AD trust and take appropriate actions to repair the trust.</span></span> <span data-ttu-id="9dd33-134">Выполните приведенные ниже действия для восстановления доверия Azure AD и AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-134">Follow these steps to repair your Azure AD and AD FS trust.</span></span>

1. <span data-ttu-id="9dd33-135">Выберите в списке дополнительных задач пункт **Восстановление доверия AAD и ADFS** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-135">Select **Repair AAD and ADFS Trust** from the list of additional tasks.</span></span>
   <span data-ttu-id="9dd33-136">![Восстановление доверия AAD и ADFS](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span><span class="sxs-lookup"><span data-stu-id="9dd33-136">![Repair AAD and ADFS Trust](media/active-directory-aadconnect-federation-management/RepairADTrust1.PNG)</span></span>

2. <span data-ttu-id="9dd33-137">На странице **Подключение к Azure AD** укажите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-137">On the **Connect to Azure AD** page, provide your global administrator credentials for Azure AD, and click **Next**.</span></span>
   <span data-ttu-id="9dd33-138">![Подключение к Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span><span class="sxs-lookup"><span data-stu-id="9dd33-138">![Connect to Azure AD](media/active-directory-aadconnect-federation-management/RepairADTrust2.PNG)</span></span>

3. <span data-ttu-id="9dd33-139">На странице **Учетные данные для удаленного доступа** введите учетные данные администратора домена.</span><span class="sxs-lookup"><span data-stu-id="9dd33-139">On the **Remote access credentials** page, enter the credentials for the domain administrator.</span></span>

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/RepairADTrust3.PNG)

    <span data-ttu-id="9dd33-141">Когда вы нажмете кнопку **Далее**, Azure AD Connect проверит работоспособность сертификата и отобразит возможные проблемы.</span><span class="sxs-lookup"><span data-stu-id="9dd33-141">After you click **Next**, Azure AD Connect checks for certificate health and shows any issues.</span></span>

    ![Состояние сертификатов](media/active-directory-aadconnect-federation-management/RepairADTrust4.PNG)

    <span data-ttu-id="9dd33-143">На странице **Готово к настройке** отобразится список действий, которые будут выполнены для восстановления доверия.</span><span class="sxs-lookup"><span data-stu-id="9dd33-143">The **Ready to configure** page shows the list of actions that will be performed to repair the trust.</span></span>

    ![Готово к настройке](media/active-directory-aadconnect-federation-management/RepairADTrust5.PNG)

4. <span data-ttu-id="9dd33-145">Чтобы восстановить доверие, нажмите кнопку **Установить** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-145">Click **Install** to repair the trust.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-146">Azure AD Connect может выполнить восстановление или другие действия только для самозаверяющих сертификатов.</span><span class="sxs-lookup"><span data-stu-id="9dd33-146">Azure AD Connect can only repair or act on certificates that are self-signed.</span></span> <span data-ttu-id="9dd33-147">С помощью Azure AD Connect нельзя восстановить сертификаты третьих сторон.</span><span class="sxs-lookup"><span data-stu-id="9dd33-147">Azure AD Connect can't repair third-party certificates.</span></span>

## <span data-ttu-id="9dd33-148">Федерация с Azure AD с помощью альтернативного имени пользователя <a name=alternateid></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-148">Federate with Azure AD using AlternateID <a name=alternateid></a></span></span>
<span data-ttu-id="9dd33-149">Рекомендуется, чтобы локальное имя участника-пользователя (UPN) и имя участника-пользователя в облаке были одинаковыми.</span><span class="sxs-lookup"><span data-stu-id="9dd33-149">It is recommended that the on-premises User Principal Name(UPN) and the cloud User Principal Name are kept the same.</span></span> <span data-ttu-id="9dd33-150">Если в локальном имени участника-пользователя используется не поддерживающий маршрутизацию домен (например,</span><span class="sxs-lookup"><span data-stu-id="9dd33-150">If the on-premises UPN uses a non-routable domain (ex.</span></span> <span data-ttu-id="9dd33-151">Contoso.local), или если его невозможно изменить из-за зависимостей локального приложения, то рекомендуется настроить альтернативное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-151">Contoso.local) or cannot be changed due to local application dependencies, we recommend setting up alternate login ID.</span></span> <span data-ttu-id="9dd33-152">Альтернативное имя пользователя позволяет настроить процедуру входа таким образом, что пользователи смогут использовать для входа атрибут, отличный от имени участника-пользователя, например адрес электронной почты.</span><span class="sxs-lookup"><span data-stu-id="9dd33-152">Alternate login ID allows you to configure a sign-in experience where users can sign in with an attribute other than their UPN, such as mail.</span></span> <span data-ttu-id="9dd33-153">По умолчанию для имени участника-пользователя в Azure AD Connect используется атрибут userPrincipalName в Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9dd33-153">The choice for User Principal Name in Azure AD Connect defaults to the userPrincipalName attribute in Active Directory.</span></span> <span data-ttu-id="9dd33-154">Если выбрать для имени участника-пользователя любой другой атрибут и выполнить федерацию с помощью AD FS, то Azure AD Connect настроит AD FS на использование альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-154">If you choose any other attribute for User Principal Name and are federating using AD FS, then Azure AD Connect will configure AD FS for alternate login ID.</span></span> <span data-ttu-id="9dd33-155">В приведенном ниже примере показано, как выбрать другой атрибут для имени участника-пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-155">An example of choosing a different attribute for User Principal Name is shown below:</span></span>

![Выбор альтернативного атрибута имени пользователя](media/active-directory-aadconnect-federation-management/attributeselection.png)

<span data-ttu-id="9dd33-157">Настройка альтернативного имени пользователя для AD FS состоит из двух основных этапов:</span><span class="sxs-lookup"><span data-stu-id="9dd33-157">Configuring alternate login ID for AD FS consists of two main steps:</span></span>
1. <span data-ttu-id="9dd33-158">**Настройка правильного набора утверждений выдачи**. Изменяются правила утверждений выдачи в отношениях доверия с проверяющей стороной Azure AD, чтобы использовать выбранный атрибут UserPrincipalName в качестве альтернативного имени пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-158">**Configure the right set of issuance claims**: The issuance claim rules in the Azure AD relying party trust are modified to use the selected UserPrincipalName attribute as the alternate ID of the user.</span></span>
2. <span data-ttu-id="9dd33-159">**Включение альтернативного имени пользователя в конфигурации AD FS**. Обновляется конфигурация AD FS, чтобы служба AD FS могла выполнять поиск пользователей в соответствующих лесах, используя альтернативное имя пользователя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-159">**Enable alternate login ID in the AD FS configuration**: The AD FS configuration is updated so that AD FS can look up users in the appropriate forests using the alternate ID.</span></span> <span data-ttu-id="9dd33-160">Эта конфигурация поддерживается для службы AD FS, работающей под управлением Windows Server 2012 R2 (с обновлением KB2919355) и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="9dd33-160">This configuration is supported for AD FS on Windows Server 2012 R2 (with KB2919355) or later.</span></span> <span data-ttu-id="9dd33-161">Если серверы AD FS работают под управлением версии 2012 R2, то Azure AD Connect проверяет наличие необходимого обновления.</span><span class="sxs-lookup"><span data-stu-id="9dd33-161">If the AD FS servers are 2012 R2, Azure AD Connect checks for the presence of the required KB.</span></span> <span data-ttu-id="9dd33-162">Если обновление не удается обнаружить, то после выполнения настройки отображается предупреждение, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="9dd33-162">If the KB is not detected, a warning will be displayed after configuration completes, as shown below:</span></span>

    ![Предупреждение об отсутствии обновления в версии 2012 R2](media/active-directory-aadconnect-federation-management/kbwarning.png)

    <span data-ttu-id="9dd33-164">При обнаружении такой проблемы необходимо исправить конфигурацию, установив обязательное обновление [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) и восстановив доверие с помощью действия [Восстановление доверия AAD и ADFS](#repairthetrust).</span><span class="sxs-lookup"><span data-stu-id="9dd33-164">To rectify the configuration in case of missing KB, install the required [KB2919355](http://go.microsoft.com/fwlink/?LinkID=396590) and then repair the trust using [Repair AAD and AD FS Trust](#repairthetrust).</span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-165">Дополнительные сведения об альтернативном имени пользователя и о его настройке вручную см. в статье [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id) (Настройка альтернативного имени пользователя).</span><span class="sxs-lookup"><span data-stu-id="9dd33-165">For more information on alternateID and steps to manually configure, read [Configuring Alternate Login ID](https://technet.microsoft.com/windows-server-docs/identity/ad-fs/operations/configuring-alternate-login-id)</span></span>

## <span data-ttu-id="9dd33-166">Добавление сервера AD FS <a name=addadfsserver></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-166">Add an AD FS server <a name=addadfsserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-167">Для добавления сервера AD FS Azure AD Connect требует PFX-файл сертификата.</span><span class="sxs-lookup"><span data-stu-id="9dd33-167">To add an AD FS server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="9dd33-168">Таким образом, эту операцию можно выполнить, только если ферма AD FS настроена с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-168">Therefore, you can perform this operation only if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="9dd33-169">Выберите пункт **Развернуть дополнительный сервер федерации** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-169">Select **Deploy an additional Federation Server**, and click **Next**.</span></span>

   ![Дополнительный сервер федерации](media/active-directory-aadconnect-federation-management/AddNewADFSServer1.PNG)

2. <span data-ttu-id="9dd33-171">На странице **Подключение к Azure AD** укажите учетные данные глобального администратора для Azure AD и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-171">On the **Connect to Azure AD** page, enter your global administrator credentials for Azure AD, and click **Next**.</span></span>

   ![Подключение к Azure AD](media/active-directory-aadconnect-federation-management/AddNewADFSServer2.PNG)

3. <span data-ttu-id="9dd33-173">Введите учетные данные администратора домена.</span><span class="sxs-lookup"><span data-stu-id="9dd33-173">Provide the domain administrator credentials.</span></span>

   ![Учетные данные администратора домена](media/active-directory-aadconnect-federation-management/AddNewADFSServer3.PNG)

4. <span data-ttu-id="9dd33-175">Azure AD Connect запросит пароль PFX-файла, который был указан при настройке новой фермы AD FS с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-175">Azure AD Connect asks for the password of the PFX file that you provided while configuring your new AD FS farm with Azure AD Connect.</span></span> <span data-ttu-id="9dd33-176">Щелкните **Введите пароль** , чтобы указать пароль для PFX-файла.</span><span class="sxs-lookup"><span data-stu-id="9dd33-176">Click **Enter Password** to provide the password for the PFX file.</span></span>

   ![Пароль сертификата](media/active-directory-aadconnect-federation-management/AddNewADFSServer4.PNG)

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/AddNewADFSServer5.PNG)

5. <span data-ttu-id="9dd33-179">На странице **Серверы AD FS** введите имя сервера или IP-адрес, который нужно добавить к ферме AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-179">On the **AD FS Servers** page, enter the server name or IP address to be added to the AD FS farm.</span></span>

   ![Серверы AD FS](media/active-directory-aadconnect-federation-management/AddNewADFSServer6.PNG)

6. <span data-ttu-id="9dd33-181">Нажмите кнопку **Далее** и выполните инструкции на последней странице **Настройка**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-181">Click **Next**, and go through the final **Configure** page.</span></span> <span data-ttu-id="9dd33-182">После того как Azure AD Connect завершит добавление серверов в ферму AD FS, у вас будет возможность проверить подключение.</span><span class="sxs-lookup"><span data-stu-id="9dd33-182">After Azure AD Connect has finished adding the servers to the AD FS farm, you will be given the option to verify the connectivity.</span></span>

   ![Готово к настройке](media/active-directory-aadconnect-federation-management/AddNewADFSServer7.PNG)

    ![Установка завершена](media/active-directory-aadconnect-federation-management/AddNewADFSServer8.PNG)

## <span data-ttu-id="9dd33-185">Добавление WAP-сервера AD FS <a name=addwapserver></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-185">Add an AD FS WAP server <a name=addwapserver></a></span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-186">Для добавления WAP-сервера Azure AD Connect требует PFX-файл сертификата.</span><span class="sxs-lookup"><span data-stu-id="9dd33-186">To add a WAP server, Azure AD Connect requires the PFX certificate.</span></span> <span data-ttu-id="9dd33-187">Таким образом, эту операцию можно выполнить, только если ферма AD FS настроена с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-187">Therefore, you can only perform this operation if you configured the AD FS farm by using Azure AD Connect.</span></span>

1. <span data-ttu-id="9dd33-188">Выберите пункт **Развертывание прокси-службы веб-приложения** в списке доступных задач.</span><span class="sxs-lookup"><span data-stu-id="9dd33-188">Select **Deploy Web Application Proxy** from the list of available tasks.</span></span>

   ![Развертывание прокси-службы веб-приложения](media/active-directory-aadconnect-federation-management/WapServer1.PNG)

2. <span data-ttu-id="9dd33-190">Введите учетные данные глобального администратора Azure.</span><span class="sxs-lookup"><span data-stu-id="9dd33-190">Provide the Azure global administrator credentials.</span></span>

   ![Подключение к Azure AD](media/active-directory-aadconnect-federation-management/wapserver2.PNG)

3. <span data-ttu-id="9dd33-192">На странице **Укажите SSL-сертификат** введите пароль для PFX-файла, который использовался при настройке фермы AD FS с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-192">On the **Specify SSL certificate** page, provide the password for the PFX file that you provided when you configured the AD FS farm with Azure AD Connect.</span></span>
   <span data-ttu-id="9dd33-193">![Пароль сертификата](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span><span class="sxs-lookup"><span data-stu-id="9dd33-193">![Certificate password](media/active-directory-aadconnect-federation-management/WapServer3.PNG)</span></span>

    ![Укажите SSL-сертификат](media/active-directory-aadconnect-federation-management/WapServer4.PNG)

4. <span data-ttu-id="9dd33-195">Добавьте сервер в качестве WAP-сервера.</span><span class="sxs-lookup"><span data-stu-id="9dd33-195">Add the server to be added as a WAP server.</span></span> <span data-ttu-id="9dd33-196">Так как WAP-сервер может быть не присоединен к домену, мастер запросит учетные данные администратора для добавляемого сервера.</span><span class="sxs-lookup"><span data-stu-id="9dd33-196">Because the WAP server might not be joined to the domain, the wizard asks for administrative credentials to the server being added.</span></span>

   ![Учетные данные администратора сервера](media/active-directory-aadconnect-federation-management/WapServer5.PNG)

5. <span data-ttu-id="9dd33-198">На странице **Учетные данные доверия прокси-сервера** введите учетные данные администратора, чтобы настроить доверие прокси-сервера и доступ к основному серверу в ферме AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-198">On the **Proxy trust credentials** page, provide administrative credentials to configure the proxy trust and access the primary server in the AD FS farm.</span></span>

   ![Учетные данные доверия прокси-сервера](media/active-directory-aadconnect-federation-management/WapServer6.PNG)

6. <span data-ttu-id="9dd33-200">В мастере на странице **Готово к настройке** отображается список действий, которые будут выполнены.</span><span class="sxs-lookup"><span data-stu-id="9dd33-200">On the **Ready to configure** page, the wizard shows the list of actions that will be performed.</span></span>

   ![Готово к настройке](media/active-directory-aadconnect-federation-management/WapServer7.PNG)

7. <span data-ttu-id="9dd33-202">Чтобы завершить настройку, нажмите кнопку **Установить** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-202">Click **Install** to finish the configuration.</span></span> <span data-ttu-id="9dd33-203">По завершении настройки мастер предоставляет возможность проверить подключение к серверам.</span><span class="sxs-lookup"><span data-stu-id="9dd33-203">After the configuration is complete, the wizard gives you the option to verify the connectivity to the servers.</span></span> <span data-ttu-id="9dd33-204">Чтобы проверить подключение, щелкните **Проверить** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-204">Click **Verify** to check connectivity.</span></span>

   ![Установка завершена](media/active-directory-aadconnect-federation-management/WapServer8.PNG)

## <span data-ttu-id="9dd33-206">Добавление федеративного домена <a name=addfeddomain></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-206">Add a federated domain <a name=addfeddomain></a></span></span>

<span data-ttu-id="9dd33-207">Вы можете быстро добавить домен в федерацию с Azure AD с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-207">It's easy to add a domain to be federated with Azure AD by using Azure AD Connect.</span></span> <span data-ttu-id="9dd33-208">Azure AD Connect добавляет домен для федерации, а также изменяет правила утверждения, чтобы правильно отражать издателя при наличии нескольких доменов в федерации с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dd33-208">Azure AD Connect adds the domain for federation and modifies the claim rules to correctly reflect the issuer when you have multiple domains federated with Azure AD.</span></span>

1. <span data-ttu-id="9dd33-209">Чтобы добавить федеративный домен, выберите задачу **Добавить дополнительный домен Azure AD**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-209">To add a federated domain, select the task **Add an additional Azure AD domain**.</span></span>

   ![Дополнительный домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain1.PNG)

2. <span data-ttu-id="9dd33-211">На следующей странице мастера введите учетные данные глобального администратора для Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dd33-211">On the next page of the wizard, provide the global administrator credentials for Azure AD.</span></span>

   ![Подключение к Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain2.PNG)

3. <span data-ttu-id="9dd33-213">На странице **Учетные данные для удаленного доступа** введите учетные данные администратора домена.</span><span class="sxs-lookup"><span data-stu-id="9dd33-213">On the **Remote access credentials** page, provide the domain administrator credentials.</span></span>

   ![Учетные данные удаленного доступа](media/active-directory-aadconnect-federation-management/additionaldomain3.PNG)

4. <span data-ttu-id="9dd33-215">На следующей странице мастера будет предоставлен список доменов Azure AD, которые можно использовать для федерации вашего локального каталога.</span><span class="sxs-lookup"><span data-stu-id="9dd33-215">On the next page, the wizard provides a list of Azure AD domains that you can federate your on-premises directory with.</span></span> <span data-ttu-id="9dd33-216">Выберите домен из списка.</span><span class="sxs-lookup"><span data-stu-id="9dd33-216">Choose the domain from the list.</span></span>

   ![Домен Azure AD](media/active-directory-aadconnect-federation-management/AdditionalDomain4.PNG)

    <span data-ttu-id="9dd33-218">Когда вы выберете домен, мастер предоставит соответствующие сведения о дальнейших действиях, которые будут выполнены мастером, а также о результатах настроек.</span><span class="sxs-lookup"><span data-stu-id="9dd33-218">After you choose the domain, the wizard provides you with appropriate information about further actions that the wizard will take and the impact of the configuration.</span></span> <span data-ttu-id="9dd33-219">В некоторых случаях при выборе домена, еще не проверенного в Azure AD, мастер предоставит сведения, которые помогут проверить домен.</span><span class="sxs-lookup"><span data-stu-id="9dd33-219">In some cases, if you select a domain that isn't yet verified in Azure AD, the wizard provides you with information to help you verify the domain.</span></span> <span data-ttu-id="9dd33-220">Дополнительные сведения см. в разделе [Добавление имени личного домена в Azure Active Directory](../active-directory-add-domain.md).</span><span class="sxs-lookup"><span data-stu-id="9dd33-220">See [Add your custom domain name to Azure Active Directory](../active-directory-add-domain.md) for more details.</span></span>

5. <span data-ttu-id="9dd33-221">Щелкните **Далее**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-221">Click **Next**.</span></span> <span data-ttu-id="9dd33-222">На странице **Готово к настройке** отображается список действий, которые выполнит Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="9dd33-222">The **Ready to configure** page shows the list of actions that Azure AD Connect will perform.</span></span> <span data-ttu-id="9dd33-223">Чтобы завершить настройку, нажмите кнопку **Установить** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-223">Click **Install** to finish the configuration.</span></span>

   ![Теперь все готово для настройки.](media/active-directory-aadconnect-federation-management/AdditionalDomain5.PNG)

> [!NOTE]
> <span data-ttu-id="9dd33-225">Пользователи из добавленного федеративного домена должна быть синхронизированы, прежде чем они смогут войти в Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dd33-225">Users from the added federated domain must be synchronized before they will be able to login to Azure AD.</span></span>

## <a name="ad-fs-customization"></a><span data-ttu-id="9dd33-226">Пользовательская настройка AD FS</span><span class="sxs-lookup"><span data-stu-id="9dd33-226">AD FS customization</span></span>
<span data-ttu-id="9dd33-227">Ниже приведены сведения о некоторых стандартных задачах, связанных с пользовательской настройкой страницы входа AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-227">The following sections provide details about some of the common tasks that you might have to perform when you customize your AD FS sign-in page.</span></span>

## <span data-ttu-id="9dd33-228">Добавление настраиваемого логотипа компании или иллюстрации <a name=customlogo></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-228">Add a custom company logo or illustration <a name=customlogo></a></span></span>
<span data-ttu-id="9dd33-229">Чтобы изменить логотип компании, который отображается на странице **входа**, используйте приведенный ниже командлет Windows PowerShell и синтаксис.</span><span class="sxs-lookup"><span data-stu-id="9dd33-229">To change the logo of the company that's displayed on the **Sign-in** page, use the following Windows PowerShell cmdlet and syntax.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-230">Рекомендуемые размеры логотипа — 260 x 35, 96 точек на дюйм. Размер файла не должен превышать 10 КБ.</span><span class="sxs-lookup"><span data-stu-id="9dd33-230">The recommended dimensions for the logo are 260 x 35 @ 96 dpi with a file size no greater than 10 KB.</span></span>

    Set-AdfsWebTheme -TargetName default -Logo @{path="c:\Contoso\logo.PNG"}

> [!NOTE]
> <span data-ttu-id="9dd33-231">Параметр *TargetName* является обязательным.</span><span class="sxs-lookup"><span data-stu-id="9dd33-231">The *TargetName* parameter is required.</span></span> <span data-ttu-id="9dd33-232">Стандартная тема для AD FS называется темой по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="9dd33-232">The default theme that's released with AD FS is named Default.</span></span>

## <span data-ttu-id="9dd33-233">Добавление описания входа в систему <a name=addsignindescription></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-233">Add a sign-in description <a name=addsignindescription></a></span></span>
<span data-ttu-id="9dd33-234">Чтобы добавить на **страницу входа**описание страницы входа, используйте следующий командлет Windows PowerShell и синтаксис.</span><span class="sxs-lookup"><span data-stu-id="9dd33-234">To add a sign-in page description to the **Sign-in page**, use the following Windows PowerShell cmdlet and syntax.</span></span>

    Set-AdfsGlobalWebContent -SignInPageDescriptionText "<p>Sign-in to Contoso requires device registration. Click <A href='http://fs1.contoso.com/deviceregistration/'>here</A> for more information.</p>"

## <span data-ttu-id="9dd33-235">Изменение правил утверждений служб федерации Active Directory <a name=modclaims></a></span><span class="sxs-lookup"><span data-stu-id="9dd33-235">Modify AD FS claim rules <a name=modclaims></a></span></span>
<span data-ttu-id="9dd33-236">Службы AD FS поддерживают обширный язык утверждений, с помощью которого можно создавать настраиваемые правила утверждений.</span><span class="sxs-lookup"><span data-stu-id="9dd33-236">AD FS supports a rich claim language that you can use to create custom claim rules.</span></span> <span data-ttu-id="9dd33-237">Дополнительные сведения см. в разделе [Роль языка правил утверждений](https://technet.microsoft.com/library/dd807118.aspx).</span><span class="sxs-lookup"><span data-stu-id="9dd33-237">For more information, see [The Role of the Claim Rule Language](https://technet.microsoft.com/library/dd807118.aspx).</span></span>

<span data-ttu-id="9dd33-238">Далее рассматривается, как можно создавать пользовательские правила для некоторых сценариев, связанных с использованием Azure AD и федерации AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-238">The following sections describe how you can write custom rules for some scenarios that relate to Azure AD and AD FS federation.</span></span>

### <a name="immutable-id-conditional-on-a-value-being-present-in-the-attribute"></a><span data-ttu-id="9dd33-239">Неизменяемый идентификатор, зависящий от наличия значения в атрибуте</span><span class="sxs-lookup"><span data-stu-id="9dd33-239">Immutable ID conditional on a value being present in the attribute</span></span>
<span data-ttu-id="9dd33-240">Azure AD Connect позволяет указывать атрибут, используемый в качестве привязки к источнику, когда объекты синхронизируются с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dd33-240">Azure AD Connect lets you specify an attribute to be used as a source anchor when objects are synced to Azure AD.</span></span> <span data-ttu-id="9dd33-241">Если значение в настраиваемом атрибуте не пустое, можно выдать утверждение неизменяемого идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9dd33-241">If the value in the custom attribute is not empty, you might want to issue an immutable ID claim.</span></span>

<span data-ttu-id="9dd33-242">Например, можно выбрать в качестве привязки к источнику атрибут **ms-ds-consistencyguid** и настроить выдачу **ImmutableID** как **ms-ds-consistencyguid** в случае наличия у атрибута значения.</span><span class="sxs-lookup"><span data-stu-id="9dd33-242">For example, you might select **ms-ds-consistencyguid** as the attribute for the source anchor and issue **ImmutableID** as **ms-ds-consistencyguid** in case the attribute has a value against it.</span></span> <span data-ttu-id="9dd33-243">Если у атрибута нет значения, в качестве неизменяемого идентификатора следует выдать **objectGuid**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-243">If there's no value against the attribute, issue **objectGuid** as the immutable ID.</span></span> <span data-ttu-id="9dd33-244">Можно создать набор пользовательских правил утверждения, как описано ниже.</span><span class="sxs-lookup"><span data-stu-id="9dd33-244">You can construct the set of custom claim rules as described in the following section.</span></span>

<span data-ttu-id="9dd33-245">**Правило 1. Атрибуты запросов**</span><span class="sxs-lookup"><span data-stu-id="9dd33-245">**Rule 1: Query attributes**</span></span>

    c:[Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname"]
    => add(store = "Active Directory", types = ("http://contoso.com/ws/2016/02/identity/claims/objectguid", "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"), query = "; objectGuid,ms-ds-consistencyguid;{0}", param = c.Value);

<span data-ttu-id="9dd33-246">В этом правиле запрашиваются значения **ms-ds-consistencyguid** и **objectGuid** для пользователя из Active Directory.</span><span class="sxs-lookup"><span data-stu-id="9dd33-246">In this rule, you're querying the values of **ms-ds-consistencyguid** and **objectGuid** for the user from Active Directory.</span></span> <span data-ttu-id="9dd33-247">Измените имя хранилища на имя соответствующего хранилища в развертывании AD FS.</span><span class="sxs-lookup"><span data-stu-id="9dd33-247">Change the store name to an appropriate store name in your AD FS deployment.</span></span> <span data-ttu-id="9dd33-248">Измените тип утверждений на определенный в федерации для **objectGuid** и **ms-ds-consistencyguid**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-248">Also change the claims type to a proper claims type for your federation, as defined for **objectGuid** and **ms-ds-consistencyguid**.</span></span>

<span data-ttu-id="9dd33-249">Кроме того, используя параметр **add** вместо **issue**, можно предотвратить добавление исходящей выдачи для сущности и использовать значения в качестве промежуточных.</span><span class="sxs-lookup"><span data-stu-id="9dd33-249">Also, by using **add** and not **issue**, you avoid adding an outgoing issue for the entity, and can use the values as intermediate values.</span></span> <span data-ttu-id="9dd33-250">Утверждение будет выдано в последующем правиле после того, как будет установлено, какое значение следует использовать в качестве неизменяемого идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9dd33-250">You will issue the claim in a later rule after you establish which value to use as the immutable ID.</span></span>

<span data-ttu-id="9dd33-251">**Правило 2. Проверка наличия ms-ds-consistencyguid для пользователя**</span><span class="sxs-lookup"><span data-stu-id="9dd33-251">**Rule 2: Check if ms-ds-consistencyguid exists for the user**</span></span>

    NOT EXISTS([Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"])
    => add(Type = "urn:anandmsft:tmp/idflag", Value = "useguid");

<span data-ttu-id="9dd33-252">Это правило определяет временный флаг с именем **idflag**, который получает значение **useguid**, если **ms-ds-concistencyguid** для пользователя не заполнен.</span><span class="sxs-lookup"><span data-stu-id="9dd33-252">This rule defines a temporary flag called **idflag** that is set to **useguid** if there's no **ms-ds-consistencyguid** populated for the user.</span></span> <span data-ttu-id="9dd33-253">Логика такого решения в том, что службы AD FS запрещают пустые утверждения.</span><span class="sxs-lookup"><span data-stu-id="9dd33-253">The logic behind this is the fact that AD FS doesn't allow empty claims.</span></span> <span data-ttu-id="9dd33-254">Поэтому при добавлении утверждений http://contoso.com/ws/2016/02/identity/claims/objectguid и http://contoso.com/ws/2016/02/identity/claims/msdsconcistencyguid в правиле 1 результатом будет утверждение **msdsconsistencyguid** только в том случае, если значение для пользователя заполнено.</span><span class="sxs-lookup"><span data-stu-id="9dd33-254">So when you add claims http://contoso.com/ws/2016/02/identity/claims/objectguid and http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid in Rule 1, you end up with an **msdsconsistencyguid** claim only if the value is populated for the user.</span></span> <span data-ttu-id="9dd33-255">Если оно не заполнено, службы AD FS определяют, что значение окажется пустым, и немедленно его опускают.</span><span class="sxs-lookup"><span data-stu-id="9dd33-255">If it isn't populated, AD FS sees that it will have an empty value and drops it immediately.</span></span> <span data-ttu-id="9dd33-256">**objectGuid**имеют все объекты, поэтому такое утверждение всегда будет присутствовать после выполнения правила 1.</span><span class="sxs-lookup"><span data-stu-id="9dd33-256">All objects will have **objectGuid**, so that claim will always be there after Rule 1 is executed.</span></span>

<span data-ttu-id="9dd33-257">**Правило 3. Выдача ms-ds-consistencyguid в качестве неизменяемого идентификатора, если он присутствует**</span><span class="sxs-lookup"><span data-stu-id="9dd33-257">**Rule 3: Issue ms-ds-consistencyguid as immutable ID if it's present**</span></span>

    c:[Type == "http://contoso.com/ws/2016/02/identity/claims/msdsconsistencyguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c.Value);

<span data-ttu-id="9dd33-258">Это неявная проверка **Exist** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-258">This is an implicit **Exist** check.</span></span> <span data-ttu-id="9dd33-259">Если значение для утверждения существует, выполняется его выдача в качестве неизменяемого идентификатора.</span><span class="sxs-lookup"><span data-stu-id="9dd33-259">If the value for the claim exists, then issue that as the immutable ID.</span></span> <span data-ttu-id="9dd33-260">В предыдущем примере используется утверждение **nameidentifier** .</span><span class="sxs-lookup"><span data-stu-id="9dd33-260">The previous example uses the **nameidentifier** claim.</span></span> <span data-ttu-id="9dd33-261">Его потребуется заменить соответствующим типом утверждения для неизменяемого идентификатора в конкретной среде.</span><span class="sxs-lookup"><span data-stu-id="9dd33-261">You'll have to change this to the appropriate claim type for the immutable ID in your environment.</span></span>

<span data-ttu-id="9dd33-262">**Правило 4. Выдача objectGuid в качестве неизменяемого идентификатора при отсутствии ms-ds-consistencyGuid**</span><span class="sxs-lookup"><span data-stu-id="9dd33-262">**Rule 4: Issue objectGuid as immutable ID if ms-ds-consistencyGuid is not present**</span></span>

    c1:[Type == "urn:anandmsft:tmp/idflag", Value =~ "useguid"]
    && c2:[Type == "http://contoso.com/ws/2016/02/identity/claims/objectguid"]
    => issue(Type = "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier", Value = c2.Value);

<span data-ttu-id="9dd33-263">В этом правиле просто выполняется проверка временного флага **idflag**.</span><span class="sxs-lookup"><span data-stu-id="9dd33-263">In this rule, you're simply checking the temporary flag **idflag**.</span></span> <span data-ttu-id="9dd33-264">На основе его значения определяется, следует ли выдавать утверждение.</span><span class="sxs-lookup"><span data-stu-id="9dd33-264">You decide whether to issue the claim based on its value.</span></span>

> [!NOTE]
> <span data-ttu-id="9dd33-265">Последовательность этих правил важна.</span><span class="sxs-lookup"><span data-stu-id="9dd33-265">The sequence of these rules is important.</span></span>

### <a name="sso-with-a-subdomain-upn"></a><span data-ttu-id="9dd33-266">Единый вход с помощью UPN поддомена</span><span class="sxs-lookup"><span data-stu-id="9dd33-266">SSO with a subdomain UPN</span></span>
<span data-ttu-id="9dd33-267">Можно включить несколько доменов в федерацию с помощью Azure AD Connect, как описано в разделе [Добавление нового федеративного домена](active-directory-aadconnect-federation-management.md#addfeddomain).</span><span class="sxs-lookup"><span data-stu-id="9dd33-267">You can add more than one domain to be federated by using Azure AD Connect, as described in [Add a new federated domain](active-directory-aadconnect-federation-management.md#addfeddomain).</span></span> <span data-ttu-id="9dd33-268">Следует изменить утверждение имени участника-пользователя (UPN) так, чтобы идентификатор издателя соответствовал корневому домену, а не поддомену, так как федеративный корневой домен включает и дочерние домены.</span><span class="sxs-lookup"><span data-stu-id="9dd33-268">You must modify the user principal name (UPN) claim so that the issuer ID corresponds to the root domain and not the subdomain, because the federated root domain also covers the child.</span></span>

<span data-ttu-id="9dd33-269">По умолчанию для идентификатора издателя установлено следующее правило утверждения:</span><span class="sxs-lookup"><span data-stu-id="9dd33-269">By default, the claim rule for issuer ID is set as:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

![Утверждение идентификатора издателя по умолчанию](media/active-directory-aadconnect-federation-management/issuer_id_default.png)

<span data-ttu-id="9dd33-271">Правило по умолчанию принимает суффикс UPN и использует его в утверждении идентификатора издателя.</span><span class="sxs-lookup"><span data-stu-id="9dd33-271">The default rule simply takes the UPN suffix and uses it in the issuer ID claim.</span></span> <span data-ttu-id="9dd33-272">Предположим, Григорий является пользователем в домене sub.contoso.com, а contoso.com включен в федерацию с Azure AD.</span><span class="sxs-lookup"><span data-stu-id="9dd33-272">For example, John is a user in sub.contoso.com, and contoso.com is federated with Azure AD.</span></span> <span data-ttu-id="9dd33-273">При входе в Azure AD Григорий вводит имя пользователя john@sub.contoso.com,</span><span class="sxs-lookup"><span data-stu-id="9dd33-273">John enters john@sub.contoso.com as the username while signing in to Azure AD.</span></span> <span data-ttu-id="9dd33-274">и правило по умолчанию для утверждения идентификатора издателя в AD FS обрабатывает его следующим образом:</span><span class="sxs-lookup"><span data-stu-id="9dd33-274">The default issuer ID claim rule in AD FS handles it in the following manner:</span></span>

    c:[Type
    == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(john@sub.contoso.com, “.+@(?<domain>.+)“, “http://${domain}/adfs/services/trust/“));

<span data-ttu-id="9dd33-275">**Значение утверждения:** http://sub.contoso.com/adfs/services/trust/.</span><span class="sxs-lookup"><span data-stu-id="9dd33-275">**Claim value:**  http://sub.contoso.com/adfs/services/trust/</span></span>

<span data-ttu-id="9dd33-276">Чтобы включить в значение утверждения издателя только корневой домен, измените правило утверждения так:</span><span class="sxs-lookup"><span data-stu-id="9dd33-276">To have only the root domain in the issuer claim value, change the claim rule to match the following:</span></span>

    c:[Type == “http://schemas.xmlsoap.org/claims/UPN“]

    => issue(Type = “http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid“, Value = regexreplace(c.Value, “^((.*)([.|@]))?(?<domain>[^.]*[.].*)$”, “http://${domain}/adfs/services/trust/“));

## <a name="next-steps"></a><span data-ttu-id="9dd33-277">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9dd33-277">Next steps</span></span>
<span data-ttu-id="9dd33-278">См. [дополнительные сведения о параметрах входа пользователя](active-directory-aadconnect-user-signin.md).</span><span class="sxs-lookup"><span data-stu-id="9dd33-278">Learn more about [user sign-in options](active-directory-aadconnect-user-signin.md).</span></span>
