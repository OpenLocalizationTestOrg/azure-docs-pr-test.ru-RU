---
title: "Доменные службы Azure AD. Включение синхронизации паролей | Документация Майкрософт"
description: "Приступая к работе с доменными службами Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 8731f2b2-661c-4f3d-adba-2c9e06344537
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/30/2017
ms.author: maheshu
ms.openlocfilehash: a7a6ee0f83d3d9bdaf236717efb39155a26934e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-password-synchronization-tooazure-active-directory-domain-services"></a><span data-ttu-id="19d38-103">Включение синхронизации паролей tooAzure доменных служб Active Directory</span><span class="sxs-lookup"><span data-stu-id="19d38-103">Enable password synchronization tooAzure Active Directory Domain Services</span></span>
<span data-ttu-id="19d38-104">Выполняя предыдущие задачи, вы включили доменные службы Azure Active Directory для клиента Azure Active Directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="19d38-104">In preceding tasks, you enabled Azure Active Directory Domain Services for your Azure Active Directory (Azure AD) tenant.</span></span> <span data-ttu-id="19d38-105">Следующая задача Hello-tooenable синхронизации хэшей учетные данные, необходимые для tooAzure проверки подлинности NT LAN Manager (NTLM) и Kerberos доменные службы AD.</span><span class="sxs-lookup"><span data-stu-id="19d38-105">hello next task is tooenable synchronization of credential hashes required for NT LAN Manager (NTLM) and Kerberos authentication tooAzure AD Domain Services.</span></span> <span data-ttu-id="19d38-106">После настройки синхронизации учетных данных, пользователи могут входить в управляемый домен toohello со своими корпоративными учетными данными.</span><span class="sxs-lookup"><span data-stu-id="19d38-106">After you've set up credential synchronization, users can sign in toohello managed domain with their corporate credentials.</span></span>

<span data-ttu-id="19d38-107">этапы Hello отличаются для учетных записей пользователя только для облака учетные записи vs, которые синхронизируются из вашего локального каталога с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="19d38-107">hello steps involved are different for cloud-only user accounts vs user accounts that are synchronized from your on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="19d38-108">Если клиент Azure AD имеет сочетание облако только пользователей и пользователей из локальной AD, необходимо tooperform оба шага.</span><span class="sxs-lookup"><span data-stu-id="19d38-108">If your Azure AD tenant has a combination of cloud only users and users from your on-premises AD, you need tooperform both steps.</span></span>

<br>

> [!div class="op_single_selector"]
> * <span data-ttu-id="19d38-109">**Учетные записи пользователей только для облака**: [синхронизации паролей для облачных учетных записей пользователей tooyour управляемого домена](active-directory-ds-getting-started-password-sync.md)</span><span class="sxs-lookup"><span data-stu-id="19d38-109">**Cloud-only user accounts**: [Synchronize passwords for cloud-only user accounts tooyour managed domain](active-directory-ds-getting-started-password-sync.md)</span></span>
> * <span data-ttu-id="19d38-110">**Локальные учетные записи пользователей**: [синхронизировать пароли для учетных записей пользователей, синхронизированных из локальной AD tooyour управляемого домена](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="19d38-110">**On-premises user accounts**: [Synchronize passwords for user accounts synced from your on-premises AD tooyour managed domain](active-directory-ds-getting-started-password-sync-synced-tenant.md)</span></span>
>
>

<br>

## <a name="task-5-enable-password-synchronization-tooyour-managed-domain-for-user-accounts-synced-with-your-on-premises-ad"></a><span data-ttu-id="19d38-111">Задача 5: Включение пароль tooyour управляемого домена синхронизации учетных записей пользователей, синхронизированные с локальным AD</span><span class="sxs-lookup"><span data-stu-id="19d38-111">Task 5: enable password synchronization tooyour managed domain for user accounts synced with your on-premises AD</span></span>
<span data-ttu-id="19d38-112">Объект синхронизации Azure AD клиента задается toosynchronize с локального каталога вашей организации с помощью Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="19d38-112">A synced Azure AD tenant is set toosynchronize with your organization's on-premises directory using Azure AD Connect.</span></span> <span data-ttu-id="19d38-113">По умолчанию Azure AD Connect не выполняет синхронизацию, NTLM и Kerberos tooAzure хэши учетных данных AD.</span><span class="sxs-lookup"><span data-stu-id="19d38-113">By default, Azure AD Connect does not synchronize NTLM and Kerberos credential hashes tooAzure AD.</span></span> <span data-ttu-id="19d38-114">toouse доменные службы Azure AD необходимо хэш tooconfigure Azure AD Connect toosynchronize учетные данные, которые требуются для проверки подлинности NTLM и Kerberos.</span><span class="sxs-lookup"><span data-stu-id="19d38-114">toouse Azure AD Domain Services, you need tooconfigure Azure AD Connect toosynchronize credential hashes required for NTLM and Kerberos authentication.</span></span> <span data-ttu-id="19d38-115">следующие шаги Hello включить синхронизацию хэши hello необходимых учетных данных из клиента Azure AD tooyour локального каталога.</span><span class="sxs-lookup"><span data-stu-id="19d38-115">hello following steps enable synchronization of hello required credential hashes from your on-premises directory tooyour Azure AD tenant.</span></span>

> [!NOTE]
> <span data-ttu-id="19d38-116">Если ваша организация использует учетные записи пользователей, которые синхронизируются из вашего локального каталога, необходимо включить синхронизацию хэшей NTLM и Kerberos в порядке toouse hello управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="19d38-116">If your organization has user accounts that are synchronized from your on-premises directory, your must enable synchronization of NTLM and Kerberos hashes in order toouse hello managed domain.</span></span> <span data-ttu-id="19d38-117">Синхронизированные учетная запись расположена синхронизированную учетную запись, которая была создана в ваш локальный каталог и является tooyour клиента Azure AD, используя Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="19d38-117">A synced user account is an account that was created in your on-premises directory and is synchronized tooyour Azure AD tenant using Azure AD Connect.</span></span>
>
>

### <a name="install-or-update-azure-ad-connect"></a><span data-ttu-id="19d38-118">Установка или обновление Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="19d38-118">Install or update Azure AD Connect</span></span>
<span data-ttu-id="19d38-119">Установить последние рекомендуется hello выпуска Azure AD Connect на домен присоединен компьютер.</span><span class="sxs-lookup"><span data-stu-id="19d38-119">Install hello latest recommended release of Azure AD Connect on a domain joined computer.</span></span> <span data-ttu-id="19d38-120">Если у вас есть существующий экземпляр программы установки Azure AD Connect, необходимо tooupdate его toouse hello последнюю версию Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="19d38-120">If you have an existing instance of Azure AD Connect setup, you need tooupdate it toouse hello latest version of Azure AD Connect.</span></span> <span data-ttu-id="19d38-121">Известные проблемы и ошибки, которые могут уже была исправлена, tooavoid убедитесь, что всегда использовать последнюю версию Azure AD Connect hello.</span><span class="sxs-lookup"><span data-stu-id="19d38-121">tooavoid known issues/bugs that may have already been fixed, ensure you always use hello latest version of Azure AD Connect.</span></span>

<span data-ttu-id="19d38-122">**[Загрузка Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span><span class="sxs-lookup"><span data-stu-id="19d38-122">**[Download Azure AD Connect](http://www.microsoft.com/download/details.aspx?id=47594)**</span></span>

<span data-ttu-id="19d38-123">Рекомендуемая версия: **1.1.553.0** (опубликована 27 июня 2017 г.).</span><span class="sxs-lookup"><span data-stu-id="19d38-123">Recommended version: **1.1.553.0** - published on June 27, 2017.</span></span>

> [!WARNING]
> <span data-ttu-id="19d38-124">НЕОБХОДИМО установить hello выпуска Azure AD Connect tooenable hello устаревший пароль учетных данных (требуется для проверки подлинности NTLM и Kerberos) toosynchronize tooyour Azure AD клиента, рекомендуется использовать последнюю версию.</span><span class="sxs-lookup"><span data-stu-id="19d38-124">You MUST install hello latest recommended release of Azure AD Connect tooenable hello legacy password credentials (required for NTLM and Kerberos authentication) toosynchronize tooyour Azure AD tenant.</span></span> <span data-ttu-id="19d38-125">Эта функция недоступна в предыдущих версиях Azure AD Connect, или с устаревшего средства DirSync hello</span><span class="sxs-lookup"><span data-stu-id="19d38-125">This functionality is not available in prior releases of Azure AD Connect or with hello legacy DirSync tool.</span></span>
>
>

<span data-ttu-id="19d38-126">Инструкции по установке для Azure AD Connect доступны в следующих hello статьи базы знаний - [Приступая к работе с Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span><span class="sxs-lookup"><span data-stu-id="19d38-126">Installation instructions for Azure AD Connect are available in hello following article - [Getting started with Azure AD Connect](../active-directory/active-directory-aadconnect.md)</span></span>

### <a name="enable-synchronization-of-ntlm-and-kerberos-credential-hashes-tooazure-ad"></a><span data-ttu-id="19d38-127">Включение синхронизации NTLM и Kerberos tooAzure хэши учетных данных AD</span><span class="sxs-lookup"><span data-stu-id="19d38-127">Enable synchronization of NTLM and Kerberos credential hashes tooAzure AD</span></span>
<span data-ttu-id="19d38-128">Выполните следующий сценарий PowerShell в каждом лесу, синхронизация паролей полного tooforce hello и включить клиент хэши toosync tooyour Azure AD для всех пользователей в локальной учетных данных.</span><span class="sxs-lookup"><span data-stu-id="19d38-128">Execute hello following PowerShell script on each AD forest, tooforce full password synchronization, and enable all on-premises users’ credential hashes toosync tooyour Azure AD tenant.</span></span> <span data-ttu-id="19d38-129">Этот сценарий включает hello хэши учетных данных, необходимых для клиента синхронизированные tooyour Azure AD toobe проверки подлинности NTLM или Kerberos.</span><span class="sxs-lookup"><span data-stu-id="19d38-129">This script enables hello credential hashes required for NTLM/Kerberos authentication toobe synchronized tooyour Azure AD tenant.</span></span>

```
$adConnector = "<CASE SENSITIVE AD CONNECTOR NAME>"  
$azureadConnector = "<CASE SENSITIVE AZURE AD CONNECTOR NAME>"  
Import-Module adsync  
$c = Get-ADSyncConnector -Name $adConnector  
$p = New-Object Microsoft.IdentityManagement.PowerShell.ObjectModel.ConfigurationParameter "Microsoft.Synchronize.ForceFullPasswordSync", String, ConnectorGlobal, $null, $null, $null
$p.Value = 1  
$c.GlobalParameters.Remove($p.Name)  
$c.GlobalParameters.Add($p)  
$c = Add-ADSyncConnector -Connector $c  
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $false   
Set-ADSyncAADPasswordSyncConfiguration -SourceConnector $adConnector -TargetConnector $azureadConnector -Enable $true  
```

<span data-ttu-id="19d38-130">В зависимости от размера каталога hello (число пользователей, групп и т.д.), синхронизации учетных данных хэширует tooAzure AD занимает время.</span><span class="sxs-lookup"><span data-stu-id="19d38-130">Depending on hello size of your directory (number of users, groups etc.), synchronization of credential hashes tooAzure AD takes time.</span></span> <span data-ttu-id="19d38-131">пароли Hello будет использовать на управляемый домен доменные службы Azure AD hello вскоре после синхронизации tooAzure AD hello хэши учетных данных.</span><span class="sxs-lookup"><span data-stu-id="19d38-131">hello passwords will be usable on hello Azure AD Domain Services managed domain shortly after hello credential hashes have synchronized tooAzure AD.</span></span>

<br>

## <a name="related-content"></a><span data-ttu-id="19d38-132">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="19d38-132">Related Content</span></span>
* [<span data-ttu-id="19d38-133">Включение синхронизации паролей tooAAD только для облака Azure в доменных службах AD directory</span><span class="sxs-lookup"><span data-stu-id="19d38-133">Enable password synchronization tooAAD Domain Services for a cloud-only Azure AD directory</span></span>](active-directory-ds-getting-started-password-sync.md)
* [<span data-ttu-id="19d38-134">Administer an Azure AD Domain Services managed domain (Администрирование управляемого домена доменных служб Azure AD)</span><span class="sxs-lookup"><span data-stu-id="19d38-134">Administer an Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-administer-domain.md)
* [<span data-ttu-id="19d38-135">Присоединение виртуальной машины tooan доменные службы Azure AD управляемого домена Windows</span><span class="sxs-lookup"><span data-stu-id="19d38-135">Join a Windows virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-windows-vm.md)
* [<span data-ttu-id="19d38-136">К домену Red Hat Enterprise Linux виртуальной машины tooan доменные службы Azure AD управляемого</span><span class="sxs-lookup"><span data-stu-id="19d38-136">Join a Red Hat Enterprise Linux virtual machine tooan Azure AD Domain Services managed domain</span></span>](active-directory-ds-admin-guide-join-rhel-linux-vm.md)
