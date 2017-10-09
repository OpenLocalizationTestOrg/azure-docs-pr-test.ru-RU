---
title: "Доменные службы Azure Active Directory: включение поддержки службы профилей пользователей SharePoint | Документация Майкрософт"
description: "Настроить синхронизацию доменных служб Active Directory Azure управляемые домены toosupport профиль для сервера SharePoint"
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
ms.openlocfilehash: 9de4f810380309e8f6436fc24412701645978f1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-managed-domain-toosupport-profile-synchronization-for-sharepoint-server"></a><span data-ttu-id="cbdd2-103">Настройка синхронизации профиля toosupport управляемый домен для сервера SharePoint</span><span class="sxs-lookup"><span data-stu-id="cbdd2-103">Configure a managed domain toosupport profile synchronization for SharePoint Server</span></span>
<span data-ttu-id="cbdd2-104">Сервер SharePoint содержит службу профилей пользователей, которая используется для синхронизации профилей пользователей.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-104">SharePoint Server includes a User Profile Service that is used for user profile synchronization.</span></span> <span data-ttu-id="cbdd2-105">tooset копирование hello службой профилей пользователей, соответствующие разрешения должны toobe, предоставленные в домене Active Directory.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-105">tooset up hello User Profile Service, appropriate permissions need toobe granted on an Active Directory domain.</span></span> <span data-ttu-id="cbdd2-106">Дополнительные сведения см. в статье [Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span><span class="sxs-lookup"><span data-stu-id="cbdd2-106">For more information, see [grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx).</span></span>

<span data-ttu-id="cbdd2-107">В этой статье объясняется, как доменные службы Azure AD управляемые домены toodeploy hello синхронизации профилей пользователей SharePoint Server службу можно настроить.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-107">This article explains how you can configure Azure AD Domain Services managed domains toodeploy hello SharePoint Server User Profile Sync service.</span></span>

## <a name="hello-aad-dc-service-accounts-group"></a><span data-ttu-id="cbdd2-108">Группа «Учетные записи службы контроллера домена AAD» Hello</span><span class="sxs-lookup"><span data-stu-id="cbdd2-108">hello 'AAD DC Service Accounts' group</span></span>
<span data-ttu-id="cbdd2-109">Группа безопасности с именем "**учетных записей служб контроллер домена AAD**" можно использовать в организационную единицу hello «Пользователи» на управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-109">A security group called '**AAD DC Service Accounts**' is available within hello 'Users' organizational unit on your managed domain.</span></span> <span data-ttu-id="cbdd2-110">Можно найти эту группу в hello **Active Directory — пользователи и компьютеры** оснастки MMC на управляемый домен.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-110">You can see this group in hello **Active Directory Users and Computers** MMC snap-in on your managed domain.</span></span>

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts.png)

<span data-ttu-id="cbdd2-112">Члены этой группы безопасности, делегированные hello следующие права:</span><span class="sxs-lookup"><span data-stu-id="cbdd2-112">Members of this security group are delegated hello following privileges:</span></span>
- <span data-ttu-id="cbdd2-113">Привилегия «Репликация изменений каталога» Hello в корневом каталоге hello DSE из hello управляемого домена.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-113">hello 'Replicate Directory Changes' privilege on hello root DSE of hello managed domain.</span></span>
- <span data-ttu-id="cbdd2-114">Hello права «Репликация изменений каталога» в контексте именования конфигурации hello (cn = контейнера конфигурации) домена с управляемыми hello.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-114">hello 'Replicate Directory Changes' privilege on hello Configuration naming context (cn=configuration container) of hello managed domain.</span></span>

<span data-ttu-id="cbdd2-115">Эта группа безопасности также является членом встроенной группы «hello» **пред-Windows 2000 доступ**.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-115">This security group is also a member of hello built-in group **Pre-Windows 2000 Compatible Access**.</span></span>

![Группа безопасности "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-properties.png)


## <a name="enable-your-managed-domain-toosupport-sharepoint-server-user-profile-sync"></a><span data-ttu-id="cbdd2-117">Включить к управляемому домену toosupport синхронизации профиля пользователя на сервере SharePoint</span><span class="sxs-lookup"><span data-stu-id="cbdd2-117">Enable your managed domain toosupport SharePoint Server user profile sync</span></span>
<span data-ttu-id="cbdd2-118">Можно добавить hello учетная запись, используемая для toohello синхронизации профиля пользователя SharePoint **учетных записей служб контроллер домена AAD** группы.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-118">You can add hello service account used for SharePoint user profile synchronization toohello **AAD DC Service Accounts** group.</span></span> <span data-ttu-id="cbdd2-119">В результате учетная запись синхронизации hello получает соответствующие права доступа tooreplicate изменения toohello каталог.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-119">As a result, hello synchronization account gets adequate privileges tooreplicate changes toohello directory.</span></span> <span data-ttu-id="cbdd2-120">Это действие позволяет toowork синхронизации профиля пользователя SharePoint Server правильно.</span><span class="sxs-lookup"><span data-stu-id="cbdd2-120">This configuration step enables SharePoint Server user profile sync toowork correctly.</span></span>

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member.png)

![Добавление участников в группу "Учетные записи службы контроллера домена AAD"](./media/active-directory-domain-services-admin-guide/aad-dc-service-accounts-add-member2.png)

## <a name="related-content"></a><span data-ttu-id="cbdd2-123">Похожий контент</span><span class="sxs-lookup"><span data-stu-id="cbdd2-123">Related Content</span></span>
* [<span data-ttu-id="cbdd2-124">Предоставление доменным службам Active Directory разрешений для синхронизации профилей в SharePoint Server 2013</span><span class="sxs-lookup"><span data-stu-id="cbdd2-124">Technical Reference - Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013</span></span>](https://technet.microsoft.com/library/hh296982.aspx)
