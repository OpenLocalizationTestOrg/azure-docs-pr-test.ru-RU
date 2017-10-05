---
title: "Доменные службы Azure Active Directory: включение поддержки службы профилей пользователей SharePoint | Документация Майкрософт"
description: "Настройте управляемые домены доменных служб Azure Active Directory для поддержки синхронизации профилей для сервера SharePoint"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: c3c923b5c9cd652f0c5b0ec98c1cda740f180122
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="configure-a-managed-domain-to-support-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="474bd-103">Настройка управляемого домена для поддержки синхронизации профилей для сервера SharePoint</span><span class="sxs-lookup"><span data-stu-id="474bd-103">Configure a managed domain to support profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="474bd-104">Сервер SharePoint содержит службу профилей пользователей, которая используется для синхронизации профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="474bd-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="474bd-105">Для настройки службы профилей пользователей необходимо иметь соответствующее разрешение домена Active Directory.</span><span class="sxs-lookup"><span data-stu-id="474bd-105">To set up the User Profile Service, appropriate permissions need to be granted on an Active Directory domain.</span></span> <span data-ttu-id="474bd-106">Дополнительные сведения см. в статье [Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="474bd-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="474bd-107">В этой статье описывается настройка управляемых доменов доменных служб Azure AD для развертывания службы синхронизации профилей пользователей для сервера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="474bd-107">This article explains how you can configure Azure AD Domain Services managed domains to deploy the SharePoint Server User Profile Sync service.</span></span>

## <a name="the-aad-dc-service-accounts-group"></a><span data-ttu-id="474bd-108">Группа "Учетные записи службы контроллера домена AAD"</span><span class="sxs-lookup"><span data-stu-id="474bd-108">The 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="474bd-109">Группа безопасности **Учетные записи службы контроллера домена AAD** доступна в подразделении "Пользователи" на управляемом домене.</span><span class="sxs-lookup"><span data-stu-id="474bd-109">A security group called '**AAD DC Service Accounts**' is available within the 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="474bd-110">Эту группу можно найти в оснастке MMC **Пользователи и компьютеры Active Directory** на управляемом домене.</span><span class="sxs-lookup"><span data-stu-id="474bd-110">You can see this group in the **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="474bd-112">Участникам этой группы безопасности делегируются следующие привилегии доступа:</span><span class="sxs-lookup"><span data-stu-id="474bd-112">Members of this security group are delegated the following privileges:</span></span>
- <span data-ttu-id="474bd-113">Репликация изменений каталога в атрибуте Root DSE управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="474bd-113">The 'Replicate Directory Changes' privilege on the root DSE of the managed domain.</span></span>
- <span data-ttu-id="474bd-114">Репликация изменений каталога в контексте именования конфигураций (cn = контейнер конфигурации) управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="474bd-114">The 'Replicate Directory Changes' privilege on the Configuration naming context (cn=configuration container) of the managed domain.</span></span>

<span data-ttu-id="474bd-115">Эта группа безопасности также входит во встроенную группу **Пред-Windows 2000 доступ**.</span><span class="sxs-lookup"><span data-stu-id="474bd-115">This security group is also a member of the built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-to-support-sharepoint-server-user-profile-sync"></a><span data-ttu-id="474bd-117">Включение управляемого домена для поддержки синхронизации профилей пользователей SharePoint Server</span><span class="sxs-lookup"><span data-stu-id="474bd-117">Enable your managed domain to support SharePoint Server user profile sync</span></span>
<span data-ttu-id="474bd-118">Учетную запись службы, используемую для синхронизации профилей пользователей SharePoint, можно добавить в группу **Учетные записи службы контроллера домена AAD**.</span><span class="sxs-lookup"><span data-stu-id="474bd-118">You can add the service account used for SharePoint user profile synchronization to the **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="474bd-119">В результате синхронизированная учетная запись получает достаточные привилегии доступа для репликации изменений в каталог.</span><span class="sxs-lookup"><span data-stu-id="474bd-119">As a result, the synchronization account gets adequate privileges to replicate changes to the directory.</span></span> <span data-ttu-id="474bd-120">На этом этапе настраивается правильная работа синхронизации профилей пользователей сервера SharePoint.</span><span class="sxs-lookup"><span data-stu-id="474bd-120">This configuration step enables SharePoint Server user profile sync to work correctly.</span></span>

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="474bd-123">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="474bd-123">Related Content</span></span>
* [<span data-ttu-id="474bd-124">Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="474bd-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
