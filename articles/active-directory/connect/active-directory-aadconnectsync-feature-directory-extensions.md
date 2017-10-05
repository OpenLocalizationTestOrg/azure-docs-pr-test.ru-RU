---
title: "Синхронизация Azure AD Connect: расширения каталогов | Документация Майкрософт"
description: "В этой статье описывается функция расширений каталогов в Azure AD Connect."
services: active-directory
documentationcenter: 
author: AndKjell
manager: femila
editor: 
ms.assetid: 995ee876-4415-4bb0-a258-cca3cbb02193
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/12/2017
ms.author: billmath
ms.openlocfilehash: 8ab9944437443a6d796345782f4f798aec96a0f6
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="ac84a-103">Синхронизация Azure AD Connect: расширения каталогов</span><span class="sxs-lookup"><span data-stu-id="ac84a-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="ac84a-104">Расширения каталогов позволяет расширять схему в Azure AD с помощью собственных атрибутов из локального каталога Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ac84a-104">Directory extensions allows you to extend the schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="ac84a-105">Эта функция позволяет создавать бизнес-приложения, использующие атрибуты, которыми вы по-прежнему можете управлять локально.</span><span class="sxs-lookup"><span data-stu-id="ac84a-105">This feature allows you to build LOB apps consuming attributes you continue to manage on-premises.</span></span> <span data-ttu-id="ac84a-106">Эти атрибуты могут быть использованы через [расширения каталогов Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) или [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="ac84a-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="ac84a-107">Просмотреть доступные атрибуты можно с помощью [проводника Azure AD Graph](https://graphexplorer.cloudapp.net) и [проводника Microsoft Graph](https://graphexplorer2.azurewebsites.net/) соответственно.</span><span class="sxs-lookup"><span data-stu-id="ac84a-107">You can see the attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="ac84a-108">В настоящее время рабочие нагрузки Office 365 не используют эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="ac84a-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="ac84a-109">Дополнительные атрибуты для синхронизации выбираются в разделе пользовательских параметров мастера установки.</span><span class="sxs-lookup"><span data-stu-id="ac84a-109">You configure which additional attributes you want to synchronize in the custom settings path in the installation wizard.</span></span>
<span data-ttu-id="ac84a-110">![Мастер расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="ac84a-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="ac84a-111">При установке отображаются следующие допустимые атрибуты:</span><span class="sxs-lookup"><span data-stu-id="ac84a-111">The installation shows the following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="ac84a-112">Типы объектов пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="ac84a-112">User and Group object types</span></span>
* <span data-ttu-id="ac84a-113">Однозначные атрибуты: строка, логическое значение, целое число, двоичное значение.</span><span class="sxs-lookup"><span data-stu-id="ac84a-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="ac84a-114">Многозначные атрибуты: строка, двоичное значение.</span><span class="sxs-lookup"><span data-stu-id="ac84a-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="ac84a-115">Список атрибутов считывается из кэша схемы, созданного во время установки Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="ac84a-115">The list of attributes is read from the schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="ac84a-116">Если в схему Active Directory добавлены дополнительные атрибуты, они будут отображаться только после [обновления схемы](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema).</span><span class="sxs-lookup"><span data-stu-id="ac84a-116">If you have extended the Active Directory schema with additional attributes, then the [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="ac84a-117">Объект в Azure AD может иметь до 100 атрибутов расширений каталога.</span><span class="sxs-lookup"><span data-stu-id="ac84a-117">An object in Azure AD can have up to 100 directory extensions attributes.</span></span> <span data-ttu-id="ac84a-118">Максимальная длина составляет 250 символов.</span><span class="sxs-lookup"><span data-stu-id="ac84a-118">The max length is 250 characters.</span></span> <span data-ttu-id="ac84a-119">Если значение атрибута больше, он будет усечен модулем синхронизации.</span><span class="sxs-lookup"><span data-stu-id="ac84a-119">If an attribute value is longer, then it is truncated by the sync engine.</span></span>

<span data-ttu-id="ac84a-120">Во время установки Azure AD Connect приложение регистрируется при условии наличия этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="ac84a-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="ac84a-121">Это приложение отображается на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="ac84a-121">You can see this application in the Azure portal.</span></span>  
![Приложение расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="ac84a-123">Теперь эти атрибуты доступны в Graph: </span><span class="sxs-lookup"><span data-stu-id="ac84a-123">These attributes are now available through Graph:</span></span>  
![График](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="ac84a-125">Атрибуты имеют префикс extension\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="ac84a-125">The attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="ac84a-126">AppClientId имеет одно значение для всех атрибутов в вашем клиенте Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ac84a-126">The AppClientId has the same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ac84a-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac84a-127">Next steps</span></span>
<span data-ttu-id="ac84a-128">Узнайте больше о настройке [службы синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) .</span><span class="sxs-lookup"><span data-stu-id="ac84a-128">Learn more about the [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="ac84a-129">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="ac84a-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
