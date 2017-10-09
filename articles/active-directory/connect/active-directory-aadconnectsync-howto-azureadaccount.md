---
title: "Синхронизация Azure AD Connect: как учетная запись службы toomanage hello Azure AD | Документы Microsoft"
description: "В этом разделе описываются, как учетная запись службы toorestore hello Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054, как tooreset hello пароль для hello Azure AD Connect sync учетная запись службы соединителя"
documentationcenter: 
author: andkjell
manager: femila
editor: 
ms.assetid: 6077043a-27f1-4304-a44b-81dc46620f24
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: e563518eae173de42a1d40bb5a76e63f29f9da42
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-how-toomanage-hello-azure-ad-service-account"></a><span data-ttu-id="484de-104">Синхронизация Azure AD Connect: как учетная запись службы toomanage hello Azure AD</span><span class="sxs-lookup"><span data-stu-id="484de-104">Azure AD Connect sync: How toomanage hello Azure AD service account</span></span>
<span data-ttu-id="484de-105">бесплатные службы toobe должен Hello учетной записи службы hello соединителя Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484de-105">hello service account used by hello Azure AD Connector is supposed toobe service free.</span></span> <span data-ttu-id="484de-106">Если вам требуется tooreset свои учетные данные, этот раздел предназначен для вас.</span><span class="sxs-lookup"><span data-stu-id="484de-106">If you need tooreset its credentials, then this topic is for you.</span></span> <span data-ttu-id="484de-107">Например, если по ошибке сброс пароля hello hello учетной записи службы с помощью PowerShell имеет глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="484de-107">For example, if a Global Administrator has by mistake reset hello password on hello service account using PowerShell.</span></span>

## <a name="reset-hello-credentials"></a><span data-ttu-id="484de-108">Сброс учетных данных hello</span><span class="sxs-lookup"><span data-stu-id="484de-108">Reset hello credentials</span></span>
<span data-ttu-id="484de-109">Если учетная запись службы hello, определенные для hello соединителя Azure AD не удается связаться с Azure AD из-за проблем tooauthentication, можно сбросить пароль hello.</span><span class="sxs-lookup"><span data-stu-id="484de-109">If hello service account defined on hello Azure AD Connector cannot contact Azure AD due tooauthentication problems, hello password can be reset.</span></span>

1. <span data-ttu-id="484de-110">Войдите в сервер синхронизации Azure AD Connect toohello и запустите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="484de-110">Sign in toohello Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="484de-111">Запустите `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="484de-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="484de-112">![Командлет PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="484de-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="484de-113">Введите учетные данные глобального администратора Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484de-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="484de-114">Этот командлет сбрасывает hello пароль для учетной записи службы hello и обновить его в Azure AD и в модуле синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="484de-114">This cmdlet resets hello password for hello service account and update it both in Azure AD and in hello sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="484de-115">Известные проблемы, которые можно решить с помощью описанных действий</span><span class="sxs-lookup"><span data-stu-id="484de-115">Known issues these steps can solve</span></span>
<span data-ttu-id="484de-116">В этом разделе приведен список ошибок, обнаруженных командой клиентов, которые были исправлены при помощи учетных данных, сброс hello учетной записи службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="484de-116">This section is a list of errors reported by customers that were fixed by a credentials reset on hello Azure AD service account.</span></span>

- - -
<span data-ttu-id="484de-117">Событие 6900</span><span class="sxs-lookup"><span data-stu-id="484de-117">Event 6900</span></span>  
<span data-ttu-id="484de-118">Hello сервер обнаружил непредвиденную ошибку при обработке уведомления об изменении пароля:</span><span class="sxs-lookup"><span data-stu-id="484de-118">hello server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="484de-119">AADSTS70002: ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="484de-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="484de-120">AADSTS50054: старый пароль используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="484de-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="484de-121">Событие 659</span><span class="sxs-lookup"><span data-stu-id="484de-121">Event 659</span></span>  
<span data-ttu-id="484de-122">Произошла ошибка при получении конфигурации синхронизации политики паролей.</span><span class="sxs-lookup"><span data-stu-id="484de-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="484de-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException.</span><span class="sxs-lookup"><span data-stu-id="484de-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="484de-124">AADSTS70002: ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="484de-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="484de-125">AADSTS50054: старый пароль используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="484de-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="484de-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="484de-126">Next steps</span></span>
<span data-ttu-id="484de-127">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="484de-127">**Overview topics**</span></span>

* [<span data-ttu-id="484de-128">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="484de-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="484de-129">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="484de-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

