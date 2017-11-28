---
title: "Изменение хэш-алгоритма подписи для отношения доверия с проверяющей стороной Office 365 | Документация Майкрософт"
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
ms.openlocfilehash: c581b1468630a9f28204592c936360b72f42f0d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="change-signature-hash-algorithm-for-office-365-relying-party-trust"></a><span data-ttu-id="a1775-104">Изменение хэш-алгоритма подписи для отношения доверия с проверяющей стороной Office 365</span><span class="sxs-lookup"><span data-stu-id="a1775-104">Change signature hash algorithm for Office 365 relying party trust</span></span>
## <a name="overview"></a><span data-ttu-id="a1775-105">Обзор</span><span class="sxs-lookup"><span data-stu-id="a1775-105">Overview</span></span>
<span data-ttu-id="a1775-106">Службы федерации Active Directory (AD FS) подписывают маркеры для Microsoft Azure Active Directory, чтобы защитить их от незаконного изменения.</span><span class="sxs-lookup"><span data-stu-id="a1775-106">Active Directory Federation Services (AD FS) signs its tokens to Microsoft Azure Active Directory to ensure that they cannot be tampered with.</span></span> <span data-ttu-id="a1775-107">Подпись основывается на алгоритме SHA1 или SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1775-107">This signature can be based on SHA1 or SHA256.</span></span> <span data-ttu-id="a1775-108">Теперь Azure Active Directory поддерживает маркеры, подписанные с помощью алгоритма SHA256. Мы рекомендуем выбирать этот алгоритм подписи маркера для обеспечения максимальной защиты.</span><span class="sxs-lookup"><span data-stu-id="a1775-108">Azure Active Directory now supports tokens signed with an SHA256 algorithm, and we recommend setting the token-signing algorithm to SHA256 for the highest level of security.</span></span> <span data-ttu-id="a1775-109">В этой статье описывается процедура замены алгоритма подписи маркера на алгоритм с более высоким уровнем защиты — SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1775-109">This article describes the steps needed to set the token-signing algorithm to the more secure SHA256 level.</span></span>

>[!NOTE]
><span data-ttu-id="a1775-110">Корпорация Майкрософт рекомендует использовать алгоритм SHA256 для подписания маркеров, так как он защищеннее, чем SHA1, но SHA1 по-прежнему поддерживается.</span><span class="sxs-lookup"><span data-stu-id="a1775-110">Microsoft recommends usage of SHA256 as the algorithm for signing tokens as it is more secure than SHA1 but SHA1 still remains a supported option.</span></span>

## <a name="change-the-token-signing-algorithm"></a><span data-ttu-id="a1775-111">Изменение алгоритма подписи маркера</span><span class="sxs-lookup"><span data-stu-id="a1775-111">Change the token-signing algorithm</span></span>
<span data-ttu-id="a1775-112">После того как алгоритм подписи будет выбран с помощью одного из указанных ниже способов, службы AD FS будут подписывать маркеры для отношения доверия с проверяющей стороной Office 365 с помощью SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1775-112">After you have set the signature algorithm with one of the two processes below, AD FS signs the tokens for Office 365 relying party trust with SHA256.</span></span> <span data-ttu-id="a1775-113">В конфигурацию не требуется вносить никакие дополнительные изменения. Кроме того, это изменение никак не влияет на возможность доступа к Office 365 или другим приложениям Azure AD.</span><span class="sxs-lookup"><span data-stu-id="a1775-113">You don't need to make any extra configuration changes, and this change has no impact on your ability to access Office 365 or other Azure AD applications.</span></span>

### <a name="ad-fs-management-console"></a><span data-ttu-id="a1775-114">Консоль управления AD FS</span><span class="sxs-lookup"><span data-stu-id="a1775-114">AD FS management console</span></span>
1. <span data-ttu-id="a1775-115">Откройте консоль управления AD FS на сервере-источнике AD FS.</span><span class="sxs-lookup"><span data-stu-id="a1775-115">Open the AD FS management console on the primary AD FS server.</span></span>
2. <span data-ttu-id="a1775-116">Разверните узел AD FS и выберите **Relying party trusts**(Отношения доверия с проверяющей стороной).</span><span class="sxs-lookup"><span data-stu-id="a1775-116">Expand the AD FS node and click **Relying Party Trusts**.</span></span>
3. <span data-ttu-id="a1775-117">Щелкните правой кнопкой мыши нужный объект отношений доверия с проверяющей стороной Office 365 или Azure и выберите пункт **Свойства**.</span><span class="sxs-lookup"><span data-stu-id="a1775-117">Right-click your Office 365/Azure relying party trust and select **Properties**.</span></span>
4. <span data-ttu-id="a1775-118">Перейдите на вкладку **Дополнительно** и в поле "Secure hash algorithm" (Алгоритм SHA) выберите значение SHA256.</span><span class="sxs-lookup"><span data-stu-id="a1775-118">Select the **Advanced** tab and select the secure hash algorithm SHA256.</span></span>
5. <span data-ttu-id="a1775-119">Нажмите кнопку **ОК**.</span><span class="sxs-lookup"><span data-stu-id="a1775-119">Click **OK**.</span></span>

![Алгоритм подписи SHA256 — MMC](./media/active-directory-aadconnectfed-sha256guidance/mmc.png)

### <a name="ad-fs-powershell-cmdlets"></a><span data-ttu-id="a1775-121">Командлеты AD FS PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1775-121">AD FS PowerShell cmdlets</span></span>
1. <span data-ttu-id="a1775-122">На любом сервере AD FS откройте PowerShell с правами администратора.</span><span class="sxs-lookup"><span data-stu-id="a1775-122">On any AD FS server, open PowerShell under administrator privileges.</span></span>
2. <span data-ttu-id="a1775-123">Задайте алгоритм SHA с помощью командлета **Set-AdfsRelyingPartyTrust** .</span><span class="sxs-lookup"><span data-stu-id="a1775-123">Set the secure hash algorithm by using the **Set-AdfsRelyingPartyTrust** cmdlet.</span></span>
   
   <code>Set-AdfsRelyingPartyTrust -TargetName 'Microsoft Office 365 Identity Platform' -SignatureAlgorithm 'http://www.w3.org/2001/04/xmldsig-more#rsa-sha256'</code>

## <a name="also-read"></a><span data-ttu-id="a1775-124">Также ознакомьтесь</span><span class="sxs-lookup"><span data-stu-id="a1775-124">Also read</span></span>
* [<span data-ttu-id="a1775-125">Управление службами федерации Active Directory и их настройка с помощью Azure AD Connect</span><span class="sxs-lookup"><span data-stu-id="a1775-125">Repair Office 365 trust with Azure AD Connect</span></span>](connect/active-directory-aadconnect-federation-management.md#repairthetrust)

