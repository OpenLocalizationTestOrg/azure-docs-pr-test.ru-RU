---
title: "хэш-алгоритм подписи aaaChange для доверия с проверяющей стороной Office 365 | Документы Microsoft"
description: "Эта страница содержит рекомендации по изменению алгоритма SHA для доверия федерации с Office 365"
keywords: "SHA1,SHA256,O365,федерация,aadconnect,adfs,ad fs,изменение sha,доверие федерации,отношение доверия с проверяющей стороной"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: samueld
editor: 
ms.assetid: cf6880e2-af78-4cc9-91bc-b64de4428bbd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: anandy
ms.openlocfilehash: 3333d1384aff8bdf6b3bcc894f8c633fd9ccc3a0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="8b686-104">Изменение хэш-алгоритма подписи для отношения доверия с проверяющей стороной Office 365</span><span class="sxs-lookup"><span data-stu-id="8b686-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="8b686-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="8b686-105">Overview</span></span>
<span data-ttu-id="8b686-106">Службы федерации Active Directory (AD FS) подписывает его tooensure Azure Active Directory tooMicrosoft маркеры, они не подделаны.</span><span class="sxs-lookup"><span data-stu-id="8b686-106">Active Directory Federation Services (AD FS) signs its tokens tooMicrosoft Azure Active Directory tooensure that they cannot be tampered with.</span></span> <span data-ttu-id="8b686-107">Подпись основывается на алгоритме SHA1 или SHA256.</span><span class="sxs-lookup"><span data-stu-id="8b686-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="8b686-108">Azure Active Directory теперь поддерживает маркеров, подписанных с помощью алгоритма SHA256, а рекомендуется задать для подписи токена алгоритм tooSHA256 hello для hello высокого уровня безопасности.</span><span class="sxs-lookup"><span data-stu-id="8b686-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting hello token-signing algorithm tooSHA256 for hello highest level of security.</span></span> <span data-ttu-id="8b686-109">В этой статье описывается hello необходимости toohello алгоритм подписи маркера hello tooset более безопасный уровень SHA256.</span><span class="sxs-lookup"><span data-stu-id="8b686-109">This article describes hello steps needed tooset hello token-signing algorithm toohello more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="8b686-110">Корпорация Майкрософт рекомендует использование SHA256 hello-алгоритма для подписи маркеров, как это более безопасно, чем SHA1, но SHA1 по-прежнему остается поддерживаемый параметр.</span><span class="sxs-lookup"><span data-stu-id="8b686-110">Microsoft recommends usage of SHA256 as hello algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-hello-token-signing-algorithm"></a><span data-ttu-id="8b686-111">Измените алгоритм подписи маркера hello</span><span class="sxs-lookup"><span data-stu-id="8b686-111">Change hello token-signing algorithm</span></span>
<span data-ttu-id="8b686-112">После выбора алгоритма подписи hello с одним hello две следующие процедуры, службы федерации Active Directory подписывает маркеры hello для Office 365 с проверяющей стороной с помощью SHA256.</span><span class="sxs-lookup"><span data-stu-id="8b686-112">After you have set hello signature algorithm with one of hello two processes below, AD FS signs hello tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="8b686-113">Не требуется toomake изменения дополнительные конфигурации, а это изменение не оказывает влияния на вашей возможности tooaccess Office 365 или другие приложения Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8b686-113">You don't need toomake any extra configuration changes, and this change has no impact on your ability tooaccess Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="8b686-114">Консоль управления AD FS</span><span class="sxs-lookup"><span data-stu-id="8b686-114">AD FS management console</span></span>
1. <span data-ttu-id="8b686-115">Откройте консоль управления hello AD FS на сервере hello основной AD FS.</span><span class="sxs-lookup"><span data-stu-id="8b686-115">Open hello AD FS management console on hello primary AD FS server.</span></span>
2. <span data-ttu-id="8b686-116">Разверните узел hello AD FS и щелкните **доверия с проверяющей стороной**.</span><span class="sxs-lookup"><span data-stu-id="8b686-116">Expand hello AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="8b686-117">Щелкните правой кнопкой мыши нужный объект отношений доверия с проверяющей стороной Office 365 или Azure и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="8b686-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="8b686-118">Выберите hello **Дополнительно** вкладку и выберите hello безопасного хэш-алгоритм SHA256.</span><span class="sxs-lookup"><span data-stu-id="8b686-118">Select hello **Advanced** tab and select hello secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="8b686-119">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="8b686-119">Click **OK**.</span></span>

![Алгоритм подписи SHA256 — MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="8b686-121">Командлеты AD FS PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b686-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="8b686-122">На любом сервере AD FS откройте PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="8b686-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="8b686-123">Набор hello безопасного хэш-алгоритм с помощью hello **AdfsRelyingPartyTrust набор** командлета.</span><span class="sxs-lookup"><span data-stu-id="8b686-123">Set hello secure hash algorithm by using hello **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="8b686-124">Также ознакомьтесь</span><span class="sxs-lookup"><span data-stu-id="8b686-124">Also read</span></span>
* [<span data-ttu-id="8b686-125">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="8b686-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

