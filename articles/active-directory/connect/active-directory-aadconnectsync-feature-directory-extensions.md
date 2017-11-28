---
title: "Синхронизация Azure AD Connect: расширения каталогов | Документация Майкрософт"
description: "В этом разделе описывается функция расширения hello каталог в Azure AD Connect."
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
ms.openlocfilehash: 31525ae914aa4d9e047ea1515b460a8311d5c815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-ad-connect-sync-directory-extensions"></a><span data-ttu-id="686e9-103">Синхронизация Azure AD Connect: расширения каталогов</span><span class="sxs-lookup"><span data-stu-id="686e9-103">Azure AD Connect sync: Directory extensions</span></span>
<span data-ttu-id="686e9-104">Расширения каталогов позволяет tooextend hello схемы в Azure AD с помощью собственных атрибутов из локальной службы Active Directory.</span><span class="sxs-lookup"><span data-stu-id="686e9-104">Directory extensions allows you tooextend hello schema in Azure AD with your own attributes from on-premises Active Directory.</span></span> <span data-ttu-id="686e9-105">Эта функция позволяет toobuild бизнес-приложения, использование атрибутов продолжить toomanage в локальной среде.</span><span class="sxs-lookup"><span data-stu-id="686e9-105">This feature allows you toobuild LOB apps consuming attributes you continue toomanage on-premises.</span></span> <span data-ttu-id="686e9-106">Эти атрибуты могут быть использованы через [расширения каталогов Azure AD Graph](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) или [Microsoft Graph](https://graph.microsoft.io/).</span><span class="sxs-lookup"><span data-stu-id="686e9-106">These attributes can be consumed through [Azure AD Graph directory extensions](https://msdn.microsoft.com/Library/Azure/Ad/Graph/howto/azure-ad-graph-api-directory-schema-extensions) or [Microsoft Graph](https://graph.microsoft.io/).</span></span> <span data-ttu-id="686e9-107">Вы увидите hello атрибуты доступны с помощью [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) и [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) соответственно.</span><span class="sxs-lookup"><span data-stu-id="686e9-107">You can see hello attributes available using [Azure AD Graph explorer](https://graphexplorer.cloudapp.net) and [Microsoft Graph explorer](https://graphexplorer2.azurewebsites.net/) respectively.</span></span>

<span data-ttu-id="686e9-108">В настоящее время рабочие нагрузки Office 365 не используют эти атрибуты.</span><span class="sxs-lookup"><span data-stu-id="686e9-108">At present no Office 365 workload consumes these attributes.</span></span>

<span data-ttu-id="686e9-109">Настройка дополнительных атрибутов требуется toosynchronize пути hello пользовательские параметры в мастере установки hello.</span><span class="sxs-lookup"><span data-stu-id="686e9-109">You configure which additional attributes you want toosynchronize in hello custom settings path in hello installation wizard.</span></span>
<span data-ttu-id="686e9-110">![Мастер расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span><span class="sxs-lookup"><span data-stu-id="686e9-110">![Schema Extension Wizard](./media/active-directory-aadconnectsync-feature-directory-extensions/extension2.png)</span></span>  
<span data-ttu-id="686e9-111">Hello установки показаны следующие атрибуты, которые являются допустимыми кандидатами hello.</span><span class="sxs-lookup"><span data-stu-id="686e9-111">hello installation shows hello following attributes, which are valid candidates:</span></span>

* <span data-ttu-id="686e9-112">Типы объектов пользователей и групп</span><span class="sxs-lookup"><span data-stu-id="686e9-112">User and Group object types</span></span>
* <span data-ttu-id="686e9-113">Однозначные атрибуты: строка, логическое значение, целое число, двоичное значение.</span><span class="sxs-lookup"><span data-stu-id="686e9-113">Single-valued attributes: String, Boolean, Integer, Binary</span></span>
* <span data-ttu-id="686e9-114">Многозначные атрибуты: строка, двоичное значение.</span><span class="sxs-lookup"><span data-stu-id="686e9-114">Multi-valued attributes: String, Binary</span></span>

<span data-ttu-id="686e9-115">Список атрибутов Hello считывается из кэша схем hello создается во время установки Azure AD Connect.</span><span class="sxs-lookup"><span data-stu-id="686e9-115">hello list of attributes is read from hello schema cache created during installation of Azure AD Connect.</span></span> <span data-ttu-id="686e9-116">Если расширения схемы Active Directory hello с дополнительные атрибуты, затем hello [схема должна быть обновлена](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) перед эти новые атрибуты являются видимыми.</span><span class="sxs-lookup"><span data-stu-id="686e9-116">If you have extended hello Active Directory schema with additional attributes, then hello [schema must be refreshed](active-directory-aadconnectsync-installation-wizard.md#refresh-directory-schema) before these new attributes are visible.</span></span>

<span data-ttu-id="686e9-117">Объект в Azure AD может иметь атрибутов расширений каталога too100.</span><span class="sxs-lookup"><span data-stu-id="686e9-117">An object in Azure AD can have up too100 directory extensions attributes.</span></span> <span data-ttu-id="686e9-118">Максимальная длина Hello-250 знаков.</span><span class="sxs-lookup"><span data-stu-id="686e9-118">hello max length is 250 characters.</span></span> <span data-ttu-id="686e9-119">Если значение атрибута длиннее, оно усекается обработчиком синхронизации hello.</span><span class="sxs-lookup"><span data-stu-id="686e9-119">If an attribute value is longer, then it is truncated by hello sync engine.</span></span>

<span data-ttu-id="686e9-120">Во время установки Azure AD Connect приложение регистрируется при условии наличия этих атрибутов.</span><span class="sxs-lookup"><span data-stu-id="686e9-120">During installation of Azure AD Connect, an application is registered where these attributes are available.</span></span> <span data-ttu-id="686e9-121">Можно видеть это приложение в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="686e9-121">You can see this application in hello Azure portal.</span></span>  
![Приложение расширения схемы](./media/active-directory-aadconnectsync-feature-directory-extensions/extension3new.png)

<span data-ttu-id="686e9-123">Теперь эти атрибуты доступны в Graph: </span><span class="sxs-lookup"><span data-stu-id="686e9-123">These attributes are now available through Graph:</span></span>  
![График](./media/active-directory-aadconnectsync-feature-directory-extensions/extension4.png)

<span data-ttu-id="686e9-125">Hello атрибуты имеют префикс с расширением\_{AppClientId}\_.</span><span class="sxs-lookup"><span data-stu-id="686e9-125">hello attributes are prefixed with extension\_{AppClientId}\_.</span></span> <span data-ttu-id="686e9-126">Hello AppClientId имеет одинаковое значение для всех атрибутов в клиенте Azure AD hello.</span><span class="sxs-lookup"><span data-stu-id="686e9-126">hello AppClientId has hello same value for all attributes in your Azure AD tenant.</span></span>

## <a name="next-steps"></a><span data-ttu-id="686e9-127">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="686e9-127">Next steps</span></span>
<span data-ttu-id="686e9-128">Дополнительные сведения о hello [синхронизации Azure AD Connect](active-directory-aadconnectsync-whatis.md) конфигурации.</span><span class="sxs-lookup"><span data-stu-id="686e9-128">Learn more about hello [Azure AD Connect sync](active-directory-aadconnectsync-whatis.md) configuration.</span></span>

<span data-ttu-id="686e9-129">Узнайте больше об [интеграции локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).</span><span class="sxs-lookup"><span data-stu-id="686e9-129">Learn more about [Integrating your on-premises identities with Azure Active Directory](active-directory-aadconnect.md).</span></span>
