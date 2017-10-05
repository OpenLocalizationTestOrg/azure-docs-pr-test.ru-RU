---
title: "Приступая к работе с Azure AD в проектах WebApi в Visual Studio | Документация Майкрософт"
description: "Как начать использовать Azure Active Directory в проектах WebApi после подключения или создания Azure AD с помощью подключенных служб Visual Studio"
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
ms.openlocfilehash: a756316054dd3bb63f3b0a9f59621bb1345bc693
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="get-started-with-azure-active-directory-and-visual-studio-connected-services-webapi-projects"></a><span data-ttu-id="1dc7c-103">Начало работы с Azure Active Directory и подключенными службами Visual Studio (проекты WebApi)</span><span class="sxs-lookup"><span data-stu-id="1dc7c-103">Get Started with Azure Active Directory and Visual Studio connected services (WebApi projects)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="1dc7c-104">Приступая к работе</span><span class="sxs-lookup"><span data-stu-id="1dc7c-104">Getting Started</span></span>](vs-active-directory-webapi-getting-started.md)
> * [<span data-ttu-id="1dc7c-105">Что произошло?</span><span class="sxs-lookup"><span data-stu-id="1dc7c-105">What Happened</span></span>](vs-active-directory-webapi-what-happened.md)
> 
> 

## <a name="requiring-authentication-to-access-controllers"></a><span data-ttu-id="1dc7c-106">Требование проверки подлинности для доступа к контроллерам</span><span class="sxs-lookup"><span data-stu-id="1dc7c-106">Requiring authentication to access controllers</span></span>
<span data-ttu-id="1dc7c-107">Ко всем контроллерам в проекте добавлен атрибут **Authorize** .</span><span class="sxs-lookup"><span data-stu-id="1dc7c-107">All controllers in your project were adorned with the **Authorize** attribute.</span></span> <span data-ttu-id="1dc7c-108">Этот атрибут обеспечивает аутентификацию пользователей перед доступом к интерфейсам API, определяемым этими контроллерами.</span><span class="sxs-lookup"><span data-stu-id="1dc7c-108">This attribute requires the user to be authenticated before accessing the APIs defined by these controllers.</span></span> <span data-ttu-id="1dc7c-109">Для анонимного доступа к контроллеру удалить с него этот атрибут.</span><span class="sxs-lookup"><span data-stu-id="1dc7c-109">To allow the controller to be accessed anonymously, remove this attribute from the controller.</span></span> <span data-ttu-id="1dc7c-110">Если необходимо задать разрешения на более детальном уровне, примените атрибут к каждому методу, требующему проверки подлинности, а не к классу контроллера.</span><span class="sxs-lookup"><span data-stu-id="1dc7c-110">If you want to set the permissions at a more granular level, apply the attribute to each method that requires authorization instead of applying it to the controller class.</span></span>

## <a name="next-steps"></a><span data-ttu-id="1dc7c-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="1dc7c-111">Next steps</span></span>
[<span data-ttu-id="1dc7c-112">Дополнительная информация о службе Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1dc7c-112">Learn more about Azure Active Directory</span></span>](https://azure.microsoft.com/services/active-directory/)

