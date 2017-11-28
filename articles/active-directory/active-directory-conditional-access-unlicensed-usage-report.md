---
title: "Отчет об использовании aaaUnlicensed | Документы Microsoft"
description: "Здравствуйте Нелицензированное использование отчетов позволяет выявить Нелицензированные пользователи, использующие платные функции Azure AD."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: 92138f43-9528-4c8a-b834-66a47da476e3
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: markvi
ms.openlocfilehash: c44d1756b4641d7ca88434017eedb6c5e2567cb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="8ec47-103">Отчет о нелицензированном использовании</span><span class="sxs-lookup"><span data-stu-id="8ec47-103">Unlicensed usage report</span></span>
<span data-ttu-id="8ec47-104">Здравствуйте Нелицензированное использование отчетов позволяет выявить Нелицензированные пользователи, использующие платные функции Azure AD.</span><span class="sxs-lookup"><span data-stu-id="8ec47-104">hello unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="8ec47-105">Это позволяет лучше использовать toomake лицензий, приобретенных и tooidentify, вы знаете, когда может потребоваться дополнительные лицензии.</span><span class="sxs-lookup"><span data-stu-id="8ec47-105">This allows you toomake better use of licenses that you have purchased and tooidentify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="8ec47-106">Hello отчетов отображает активные использование hello платные функции hello последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="8ec47-106">hello report shows active usage of hello paid features in hello last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="8ec47-107">Структура отчета</span><span class="sxs-lookup"><span data-stu-id="8ec47-107">Report structure</span></span>
| <span data-ttu-id="8ec47-108">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="8ec47-108">Column name</span></span> | <span data-ttu-id="8ec47-109">Описание</span><span class="sxs-lookup"><span data-stu-id="8ec47-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="8ec47-110">Пользователь без лицензии</span><span class="sxs-lookup"><span data-stu-id="8ec47-110">Unlicensed User</span></span> |<span data-ttu-id="8ec47-111">Имя пользователя hello</span><span class="sxs-lookup"><span data-stu-id="8ec47-111">Name of hello user</span></span> |
| <span data-ttu-id="8ec47-112">Функция</span><span class="sxs-lookup"><span data-stu-id="8ec47-112">Feature</span></span> |<span data-ttu-id="8ec47-113">имя функции Hello.</span><span class="sxs-lookup"><span data-stu-id="8ec47-113">hello feature name.</span></span> <span data-ttu-id="8ec47-114">Например, условный доступ</span><span class="sxs-lookup"><span data-stu-id="8ec47-114">For example: conditional access</span></span> |
| <span data-ttu-id="8ec47-115">Приложение к которому осуществлялся доступ</span><span class="sxs-lookup"><span data-stu-id="8ec47-115">Application Accessed</span></span> |<span data-ttu-id="8ec47-116">Имя приложения hello, к которому осуществляется с помощью функции hello Hello.</span><span class="sxs-lookup"><span data-stu-id="8ec47-116">hello name of hello application that is being accessed with hello feature.</span></span> <span data-ttu-id="8ec47-117">Например, Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="8ec47-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="8ec47-118">Если учетная запись пользователя была удалена Здравствуйте, «Нелицензированные пользователя» будет заполнен столбец с Идентификатором, например 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="8ec47-118">If a user account has been deleted hello ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="8ec47-119">Функция условного доступа</span><span class="sxs-lookup"><span data-stu-id="8ec47-119">Conditional access feature</span></span>
<span data-ttu-id="8ec47-120">При доступе к службе, для которой применяется политика условного доступа, пользователи без лицензии будут помечены, если у них нет лицензии Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="8ec47-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="8ec47-121">Это относится tooMFA / расположение политики, а также устройств политики, использовать Intune.</span><span class="sxs-lookup"><span data-stu-id="8ec47-121">This applies tooMFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="8ec47-122">См. также</span><span class="sxs-lookup"><span data-stu-id="8ec47-122">See also</span></span>
* [<span data-ttu-id="8ec47-123">Защита доступа к Office 365 и другим приложениям, подключенным к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="8ec47-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="8ec47-124">Начало работы с условным доступом tooAzure AD</span><span class="sxs-lookup"><span data-stu-id="8ec47-124">Getting started with conditional access tooAzure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

