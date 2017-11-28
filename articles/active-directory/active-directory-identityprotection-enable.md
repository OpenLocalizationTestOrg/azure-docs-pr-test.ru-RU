---
title: "Включение защиты идентификации Azure Active Directory | Документация Майкрософт"
description: "Узнайте, как включить защиту идентификации Azure Active Directory."
services: active-directory
keywords: "защита удостоверений Azure Active Directory, Cloud App Discovery, управление приложениями, безопасность, риск, уровень риска, уязвимость, политика безопасности"
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: f7a7ffaf-76bf-4cc7-96a1-86c944275c82
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.reviewer: nigu
ms.openlocfilehash: e0683e837086ca08f4b4b3f49695bdd2b4063ea4
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="enabling-azure-active-directory-identity-protection"></a><span data-ttu-id="d475d-104">Включение защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d475d-104">Enabling Azure Active Directory Identity Protection</span></span>
<span data-ttu-id="d475d-105">Защита идентификации Azure Active Directory — это новая возможность, которая обеспечивает единое представление подозрительных операций входа в систему и потенциальных уязвимостей. В этой службе реализованы уведомления, рекомендации по исправлению и политики на основе рисков, помогающие защитить организацию.</span><span class="sxs-lookup"><span data-stu-id="d475d-105">Azure Active Directory Identity Protection is a new capability that provides a consolidated view into suspicious sign-in activities and potential vulnerabilities and with notifications, remediation recommendations and risk-based policies helps you protect your business.</span></span> 

<span data-ttu-id="d475d-106">Данная служба обнаруживает подозрительные операции входа в систему по пользовательским и привилегированным (администраторы) удостоверениям по таким признакам, как атаки методом подбора, раскрытые учетные данные, попытки входа в систему из неизвестных расположений и зараженные устройства, чтобы обеспечить защиту в реальном времени.</span><span class="sxs-lookup"><span data-stu-id="d475d-106">The service detects suspicious activities for end user and privileged (admin) identities based on signals like brute force attacks, leaked credentials, sign ins from unfamiliar locations, infected devices, to protect against these activities in real-time.</span></span> <span data-ttu-id="d475d-107">Что более важно, на основе этих подозрительных операций вычисляется серьезность риска пользователя, и можно настроить политики на основе рисков, чтобы обеспечить автоматическую защиту удостоверений своей организации.</span><span class="sxs-lookup"><span data-stu-id="d475d-107">More importantly, based on these suspicious activities, a user risk severity is computed and risk-based policies can be configured and automatically protect the identities of your organization.</span></span> <span data-ttu-id="d475d-108">Дополнительные сведения см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).</span><span class="sxs-lookup"><span data-stu-id="d475d-108">For more details, see [Azure Active Directory Identity Protection](active-directory-identityprotection.md).</span></span>

<span data-ttu-id="d475d-109">В этом разделе показано, как включить защиту идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d475d-109">This topics shows how to enable Azure Active Directory Identity Protection.</span></span>

## <a name="steps-to-enable-azure-active-directory-identity-protection"></a><span data-ttu-id="d475d-110">Инструкции по включению защиты идентификации Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="d475d-110">Steps to enable Azure Active Directory Identity Protection</span></span>
1. <span data-ttu-id="d475d-111">[Войдите](https://ms.portal.azure.com/) на портал Azure с правами глобального администратора.</span><span class="sxs-lookup"><span data-stu-id="d475d-111">[Sign-on](https://ms.portal.azure.com/) to your Azure portal as global administrator.</span></span> 
2. <span data-ttu-id="d475d-112">На портале Azure щелкните **Marketplace**.</span><span class="sxs-lookup"><span data-stu-id="d475d-112">In the Azure portal, click **Marketplace**.</span></span>
   
    <span data-ttu-id="d475d-113">![Создание](./media/active-directory-identityprotection-enable/01.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="d475d-113">![Create](./media/active-directory-identityprotection-enable/01.png "Create")</span></span>
3. <span data-ttu-id="d475d-114">В списке приложений щелкните **Безопасность+идентификация**.</span><span class="sxs-lookup"><span data-stu-id="d475d-114">In the applications list, click **Security + Identity**.</span></span>
   
    <span data-ttu-id="d475d-115">![Создание](./media/active-directory-identityprotection-enable/02.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="d475d-115">![Create](./media/active-directory-identityprotection-enable/02.png "Create")</span></span>
4. <span data-ttu-id="d475d-116">Щелкните **Azure AD Identity Protection**(Защита идентификации Azure AD).</span><span class="sxs-lookup"><span data-stu-id="d475d-116">Click **Azure AD Identity Protection**.</span></span>
   
    <span data-ttu-id="d475d-117">![Создание](./media/active-directory-identityprotection-enable/03.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="d475d-117">![Create](./media/active-directory-identityprotection-enable/03.png "Create")</span></span>
5. <span data-ttu-id="d475d-118">В колонке **Azure AD Identity Protection** (Защита идентификации Azure AD) щелкните **Создать**.</span><span class="sxs-lookup"><span data-stu-id="d475d-118">On the **Azure AD Identity Protection** blade, click **Create**.</span></span>
   
    <span data-ttu-id="d475d-119">![Создание](./media/active-directory-identityprotection-enable/04.png "Создание")</span><span class="sxs-lookup"><span data-stu-id="d475d-119">![Create](./media/active-directory-identityprotection-enable/04.png "Create")</span></span>

## <a name="next-steps"></a><span data-ttu-id="d475d-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d475d-120">Next Steps</span></span>
* [<span data-ttu-id="d475d-121">Защита идентификации Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d475d-121">Azure Active Directory Identity Protection</span></span>](active-directory-identityprotection.md)

