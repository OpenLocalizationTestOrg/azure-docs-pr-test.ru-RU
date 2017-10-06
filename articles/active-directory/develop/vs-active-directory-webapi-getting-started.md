---
title: "aaaGet работы с Azure AD в проектах Visual Studio WebApi | Документы Microsoft"
description: "Запуск с помощью Azure Active Directory в проектах WebApi после подключения tooor создания Azure AD с помощью Visual Studio tooget подключенные службы"
services: active-directory
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: bf1eb32d-25cd-4abf-8679-2ead299fedaa
ms.service: active-directory
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 03/19/2017
ms.author: kraigb
ms.custom: aaddev
ms.openlocfilehash: 21413a71a2fd61f31268bf6d5e4d86b8be5bd16a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="ec644-103">Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты WebApi)</span><span class="sxs-lookup"><span data-stu-id="ec644-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ec644-104">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="ec644-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="ec644-105">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="ec644-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-tooaccess-controllers"></a><span data-ttu-id="ec644-106">Требование проверки подлинности tooaccess контроллеров</span><span class="sxs-lookup"><span data-stu-id="ec644-106">Requiring authentication tooaccess controllers</span></span>
<span data-ttu-id="ec644-107">Все контроллеры в проекте были снабженных hello **авторизовать** атрибута.</span><span class="sxs-lookup"><span data-stu-id="ec644-107">All controllers in your project were adorned with hello **Authorize** attribute.</span></span> <span data-ttu-id="ec644-108">Этот атрибут требуется hello toobe пользователя, доступ к API-интерфейсы hello определяются эти контроллеры только после проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="ec644-108">This attribute requires hello user toobe authenticated before accessing hello APIs defined by these controllers.</span></span> <span data-ttu-id="ec644-109">tooallow hello контроллера toobe доступна анонимно, удалите этот атрибут из контроллера hello.</span><span class="sxs-lookup"><span data-stu-id="ec644-109">tooallow hello controller toobe accessed anonymously, remove this attribute from hello controller.</span></span> <span data-ttu-id="ec644-110">Tooset hello разрешения на более детальном уровне, применить метод tooeach атрибут hello, требующей авторизации вместо применения его toohello класс контроллера.</span><span class="sxs-lookup"><span data-stu-id="ec644-110">If you want tooset hello permissions at a more granular level, apply hello attribute tooeach method that requires authorization instead of applying it toohello controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ec644-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ec644-111">Next steps</span></span>
[<span data-ttu-id="ec644-112">Дополнительная информация о службе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ec644-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

