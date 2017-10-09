---
title: "Подготовка приложения Azure AD tooan коллекции aaaUser — ведения часа или более | Документы Microsoft"
description: "Как toofind out почему подготовки tooyour приложения может выполняться дольше, чем ожидалось"
services: active-directory
documentationcenter: 
author: ajamess
manager: femila
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/11/2017
ms.author: asteen
ms.openlocfilehash: 0658f041724c91ddd1997cc7759393b46680f13a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="user-provisioning-tooan-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="22f24-103">Подготовка приложения Azure AD tooan коллекции пользователей — ведения часов или более</span><span class="sxs-lookup"><span data-stu-id="22f24-103">User provisioning tooan Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="22f24-104">При первом включении автоматической инициализации приложения, hello начальной синхронизации может занять от tooseveral часов 20 минут, в зависимости от размера каталога Azure AD hello и hello количество пользователей в области для подготовки hello.</span><span class="sxs-lookup"><span data-stu-id="22f24-104">When first enabling automatic provisioning for an application, hello initial sync can take anywhere from 20 minutes tooseveral hours, depending on hello size of hello Azure AD directory and hello number of users in scope for provisioning.</span></span> 

<span data-ttu-id="22f24-105">Последующие синхронизации после начальной синхронизации hello выполняться быстрее, как hello подготовки службы хранит водяных знаков, которые представляют Привет состояние обеих систем после начальной синхронизации hello, повышая производительность последующих синхронизаций.</span><span class="sxs-lookup"><span data-stu-id="22f24-105">Subsequent syncs after hello initial sync be faster, as hello provisioning service stores watermarks that represent hello state of both systems after hello initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-tooimprove-provisioning-performance"></a><span data-ttu-id="22f24-106">Как tooimprove подготовки производительности</span><span class="sxs-lookup"><span data-stu-id="22f24-106">How tooimprove provisioning performance</span></span>

<span data-ttu-id="22f24-107">Если начальная синхронизация hello занимает несколько часов, есть один вопрос, можно сделать tooimprove производительности:</span><span class="sxs-lookup"><span data-stu-id="22f24-107">If hello initial sync is taking more than a few hours, there is one thing you can do tooimprove performance:</span></span>

-   <span data-ttu-id="22f24-108">**Фильтры области.**</span><span class="sxs-lookup"><span data-stu-id="22f24-108">**User scoping filters.**</span></span> <span data-ttu-id="22f24-109">Фильтры области позволяют toofine настраивать hello данные, которые hello подготовки служба извлекает из Azure AD с помощью фильтрации пользователей на основе значений конкретного атрибута.</span><span class="sxs-lookup"><span data-stu-id="22f24-109">Scoping filters allow you toofine tune hello data that hello provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="22f24-110">Дополнительные сведения о фильтрах области см. в статье [Подготовка приложений на основе атрибутов с использованием фильтров области](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="22f24-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="22f24-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="22f24-111">Next steps</span></span>
[<span data-ttu-id="22f24-112">Автоматизировать подготовку пользователей и их отзыва tooSaaS приложений с Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="22f24-112">Automate User Provisioning and Deprovisioning tooSaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

