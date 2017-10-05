---
title: "Отчет о нелицензированном использовании | Документация Майкрософт"
description: "Отчет о нелицензированном использовании помогает выявить пользователей, которые используют платные функции Azure AD без лицензии."
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
ms.openlocfilehash: c0b4f455f067e825362bdecc02ea62d7984f0d31
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="unlicensed-usage-report"></a><span data-ttu-id="c64d3-103">Отчет о нелицензированном использовании</span><span class="sxs-lookup"><span data-stu-id="c64d3-103">Unlicensed usage report</span></span>
<span data-ttu-id="c64d3-104">Отчет о нелицензированном использовании помогает выявить пользователей, которые используют платные функции Azure AD без лицензии.</span><span class="sxs-lookup"><span data-stu-id="c64d3-104">The unlicensed usage report helps you identify unlicensed users that are using paid Azure AD features.</span></span> <span data-ttu-id="c64d3-105">Благодаря этому вы сможете эффективнее использовать приобретенные лицензии и вовремя узнавать о необходимости купить новые.</span><span class="sxs-lookup"><span data-stu-id="c64d3-105">This allows you to make better use of licenses that you have purchased and to identify you know when you may need additional licenses.</span></span> 

<span data-ttu-id="c64d3-106">В отчете отображается активное использование платных функций за последние 30 дней.</span><span class="sxs-lookup"><span data-stu-id="c64d3-106">The report shows active usage of the paid features in the last 30 days.</span></span> 

## <a name="report-structure"></a><span data-ttu-id="c64d3-107">Структура отчета</span><span class="sxs-lookup"><span data-stu-id="c64d3-107">Report structure</span></span>
| <span data-ttu-id="c64d3-108">Имя столбца</span><span class="sxs-lookup"><span data-stu-id="c64d3-108">Column name</span></span> | <span data-ttu-id="c64d3-109">Описание</span><span class="sxs-lookup"><span data-stu-id="c64d3-109">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="c64d3-110">Пользователь без лицензии</span><span class="sxs-lookup"><span data-stu-id="c64d3-110">Unlicensed User</span></span> |<span data-ttu-id="c64d3-111">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="c64d3-111">Name of the user</span></span> |
| <span data-ttu-id="c64d3-112">Функция</span><span class="sxs-lookup"><span data-stu-id="c64d3-112">Feature</span></span> |<span data-ttu-id="c64d3-113">Название функции.</span><span class="sxs-lookup"><span data-stu-id="c64d3-113">The feature name.</span></span> <span data-ttu-id="c64d3-114">Например, условный доступ</span><span class="sxs-lookup"><span data-stu-id="c64d3-114">For example: conditional access</span></span> |
| <span data-ttu-id="c64d3-115">Приложение к которому осуществлялся доступ</span><span class="sxs-lookup"><span data-stu-id="c64d3-115">Application Accessed</span></span> |<span data-ttu-id="c64d3-116">Имя приложения, к которому осуществляется доступ с помощью функции.</span><span class="sxs-lookup"><span data-stu-id="c64d3-116">The name of the application that is being accessed with the feature.</span></span> <span data-ttu-id="c64d3-117">Например, Office 365 SharePoint Online</span><span class="sxs-lookup"><span data-stu-id="c64d3-117">For example: Office 365 SharePoint Online</span></span> |

> [!NOTE]
> <span data-ttu-id="c64d3-118">Если учетная запись пользователя удалена, столбец "Пользователь без лицензии" будет заполнен идентификатором, таким как 1003000090D8B285</span><span class="sxs-lookup"><span data-stu-id="c64d3-118">If a user account has been deleted the ‘Unlicensed User’ column will be populated with an ID, like 1003000090D8B285</span></span>
> 
> 

## <a name="conditional-access-feature"></a><span data-ttu-id="c64d3-119">Функция условного доступа</span><span class="sxs-lookup"><span data-stu-id="c64d3-119">Conditional access feature</span></span>
<span data-ttu-id="c64d3-120">При доступе к службе, для которой применяется политика условного доступа, пользователи без лицензии будут помечены, если у них нет лицензии Azure AD Premium.</span><span class="sxs-lookup"><span data-stu-id="c64d3-120">Unlicensed users will be flagged when they access a service that has conditional access policy applied if they do not have an Azure AD Premium license.</span></span> 

<span data-ttu-id="c64d3-121">Это относится к MFA (многофакторной проверке подлинности) и политикам расположения, а также политикам устройств, которые используют Intune.</span><span class="sxs-lookup"><span data-stu-id="c64d3-121">This applies to MFA / Location policies as well as device polices that use Intune.</span></span>

## <a name="see-also"></a><span data-ttu-id="c64d3-122">Дополнительные материалы</span><span class="sxs-lookup"><span data-stu-id="c64d3-122">See also</span></span>
* [<span data-ttu-id="c64d3-123">Защита доступа к Office 365 и другим приложениям, подключенным к Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="c64d3-123">Using Conditional Access with Office 365 and other Azure Active Directory connected apps</span></span>](active-directory-conditional-access.md)
* [<span data-ttu-id="c64d3-124">Основные сведения об условном доступе к Azure AD</span><span class="sxs-lookup"><span data-stu-id="c64d3-124">Getting started with conditional access to Azure AD</span></span>](active-directory-conditional-access-azuread-connected-apps.md) 

