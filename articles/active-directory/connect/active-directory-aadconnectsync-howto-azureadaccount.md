---
title: "Синхронизация Azure AD Connect: управление учетной записью службы Azure AD | Документация Майкрософт"
description: "В этой статье описывается процедура восстановления учетной записи службы Azure AD."
services: active-directory
keywords: "AADSTS70002, AADSTS50054 Как сбросить пароль для учетной записи службы соединителя синхронизации Azure AD Connect"
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
ms.openlocfilehash: 8e9e8192ee4fcb636b5be91d2616acbc9120c8c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-how-to-manage-the-azure-ad-service-account"></a><span data-ttu-id="06165-104">Синхронизация Azure AD Connect: управление учетной записью службы Azure AD</span><span class="sxs-lookup"><span data-stu-id="06165-104">Azure AD Connect sync: How to manage the Azure AD service account</span></span>
<span data-ttu-id="06165-105">Учетная запись службы, используемая соединителем Azure AD, как правило, не нуждается в обслуживании.</span><span class="sxs-lookup"><span data-stu-id="06165-105">The service account used by the Azure AD Connector is supposed to be service free.</span></span> <span data-ttu-id="06165-106">Если требуется сбросить ее учетные данные, в этой статье вы найдете необходимые сведения.</span><span class="sxs-lookup"><span data-stu-id="06165-106">If you need to reset its credentials, then this topic is for you.</span></span> <span data-ttu-id="06165-107">Например, это потребуется, если глобальный администратор по ошибке сбросит пароль учетной записи службы с помощью PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06165-107">For example, if a Global Administrator has by mistake reset the password on the service account using PowerShell.</span></span>

## <a name="reset-the-credentials"></a><span data-ttu-id="06165-108">Сброс учетных данных</span><span class="sxs-lookup"><span data-stu-id="06165-108">Reset the credentials</span></span>
<span data-ttu-id="06165-109">Если учетная запись службы, определенная в соединителе Azure AD, не может связаться с Azure AD из-за проблем с проверкой подлинности, можно сбросить пароль.</span><span class="sxs-lookup"><span data-stu-id="06165-109">If the service account defined on the Azure AD Connector cannot contact Azure AD due to authentication problems, the password can be reset.</span></span>

1. <span data-ttu-id="06165-110">Войдите на сервер синхронизации Azure AD Connect и запустите PowerShell.</span><span class="sxs-lookup"><span data-stu-id="06165-110">Sign in to the Azure AD Connect sync server and start PowerShell.</span></span>
2. <span data-ttu-id="06165-111">Запустите `Add-ADSyncAADServiceAccount`.</span><span class="sxs-lookup"><span data-stu-id="06165-111">Run `Add-ADSyncAADServiceAccount`.</span></span>  
   <span data-ttu-id="06165-112">![Командлет PowerShell addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span><span class="sxs-lookup"><span data-stu-id="06165-112">![PowerShell cmdlet addadsyncaadserviceaccount](./media/active-directory-aadconnectsync-howto-azureadaccount/addadsyncaadserviceaccount.png)</span></span>
3. <span data-ttu-id="06165-113">Введите учетные данные глобального администратора Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06165-113">Provide Azure AD Global admin credentials.</span></span>

<span data-ttu-id="06165-114">Этот командлет сбрасывает пароль для учетной записи службы и обновляет его в Azure AD и в модуле синхронизации.</span><span class="sxs-lookup"><span data-stu-id="06165-114">This cmdlet resets the password for the service account and update it both in Azure AD and in the sync engine.</span></span>

## <a name="known-issues-these-steps-can-solve"></a><span data-ttu-id="06165-115">Известные проблемы, которые можно решить с помощью описанных действий</span><span class="sxs-lookup"><span data-stu-id="06165-115">Known issues these steps can solve</span></span>
<span data-ttu-id="06165-116">Ниже представлен список обнаруженных пользователями ошибок, которые можно исправить путем сброса учетных данных учетной записи службы Azure AD.</span><span class="sxs-lookup"><span data-stu-id="06165-116">This section is a list of errors reported by customers that were fixed by a credentials reset on the Azure AD service account.</span></span>

- - -
<span data-ttu-id="06165-117">Событие 6900</span><span class="sxs-lookup"><span data-stu-id="06165-117">Event 6900</span></span>  
<span data-ttu-id="06165-118">Сервер обнаружил непредвиденную ошибку при обработке уведомления об изменении пароля.</span><span class="sxs-lookup"><span data-stu-id="06165-118">The server encountered an unexpected error while processing a password change notification:</span></span>  
<span data-ttu-id="06165-119">AADSTS70002: ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="06165-119">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="06165-120">AADSTS50054: старый пароль используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="06165-120">AADSTS50054: Old password is used for authentication.</span></span>

- - -
<span data-ttu-id="06165-121">Событие 659</span><span class="sxs-lookup"><span data-stu-id="06165-121">Event 659</span></span>  
<span data-ttu-id="06165-122">Произошла ошибка при получении конфигурации синхронизации политики паролей.</span><span class="sxs-lookup"><span data-stu-id="06165-122">Error while retrieving password policy sync configuration.</span></span> <span data-ttu-id="06165-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException.</span><span class="sxs-lookup"><span data-stu-id="06165-123">Microsoft.IdentityModel.Clients.ActiveDirectory.AdalServiceException:</span></span>  
<span data-ttu-id="06165-124">AADSTS70002: ошибка при проверке учетных данных.</span><span class="sxs-lookup"><span data-stu-id="06165-124">AADSTS70002: Error validating credentials.</span></span> <span data-ttu-id="06165-125">AADSTS50054: старый пароль используется для проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="06165-125">AADSTS50054: Old password is used for authentication.</span></span>

## <a name="next-steps"></a><span data-ttu-id="06165-126">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="06165-126">Next steps</span></span>
<span data-ttu-id="06165-127">**Обзорные статьи**</span><span class="sxs-lookup"><span data-stu-id="06165-127">**Overview topics**</span></span>

* [<span data-ttu-id="06165-128">Службы синхронизации Azure AD Connect: общие сведений о синхронизации и ее настройка</span><span class="sxs-lookup"><span data-stu-id="06165-128">Azure AD Connect sync: Understand and customize synchronization</span></span>](active-directory-aadconnectsync-whatis.md)
* [<span data-ttu-id="06165-129">Интеграция локальных удостоверений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="06165-129">Integrating your on-premises identities with Azure Active Directory</span></span>](active-directory-aadconnect.md)

