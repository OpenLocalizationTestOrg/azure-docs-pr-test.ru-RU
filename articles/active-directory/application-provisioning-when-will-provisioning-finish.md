---
title: "Подготовка пользователей для приложения в коллекции Azure AD выполняется час и более | Документация Майкрософт"
description: "Как узнать, почему подготовка для приложения может выполняться дольше, чем ожидалось"
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
ms.openlocfilehash: 183d60cbbbc8d02f7cd3cacc160453c45717ef0d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="user-provisioning-to-an-azure-ad-gallery-application-is-taking-hours-or-more"></a><span data-ttu-id="590fd-103">Подготовка пользователей для приложения в коллекции Azure AD выполняется час и более</span><span class="sxs-lookup"><span data-stu-id="590fd-103">User provisioning to an Azure AD Gallery application is taking hours or more</span></span>

<span data-ttu-id="590fd-104">При первом включении автоматической подготовки для приложения начальная синхронизация может выполняться от 20 минут до нескольких часов в зависимости от размера каталога Azure AD и количества подготавливаемых пользователей.</span><span class="sxs-lookup"><span data-stu-id="590fd-104">When first enabling automatic provisioning for an application, the initial sync can take anywhere from 20 minutes to several hours, depending on the size of the Azure AD directory and the number of users in scope for provisioning.</span></span> 

<span data-ttu-id="590fd-105">Последующие операции синхронизации занимают меньше времени, так как служба подготовки сохраняет "водяные знаки", которые представляют состояние обеих систем после начальной синхронизации. Это позволяет повысить скорость последующих операций синхронизации.</span><span class="sxs-lookup"><span data-stu-id="590fd-105">Subsequent syncs after the initial sync be faster, as the provisioning service stores watermarks that represent the state of both systems after the initial sync, improving performance of subsequent syncs.</span></span>

## <a name="how-to-improve-provisioning-performance"></a><span data-ttu-id="590fd-106">Как улучшить производительность подготовки</span><span class="sxs-lookup"><span data-stu-id="590fd-106">How to improve provisioning performance</span></span>

<span data-ttu-id="590fd-107">Если начальная синхронизация занимает несколько часов, повысить производительность можно только одним способом:</span><span class="sxs-lookup"><span data-stu-id="590fd-107">If the initial sync is taking more than a few hours, there is one thing you can do to improve performance:</span></span>

-   <span data-ttu-id="590fd-108">**Фильтры области.**</span><span class="sxs-lookup"><span data-stu-id="590fd-108">**User scoping filters.**</span></span> <span data-ttu-id="590fd-109">Фильтры области позволяют точно настроить данные, которые служба подготовки получает из Azure AD, за счет фильтрации пользователей по значению конкретного атрибута.</span><span class="sxs-lookup"><span data-stu-id="590fd-109">Scoping filters allow you to fine tune the data that the provisioning service extracts from Azure AD by filtering out users based on specific attribute values.</span></span> <span data-ttu-id="590fd-110">Дополнительные сведения о фильтрах области см. в статье [Подготовка приложений на основе атрибутов с использованием фильтров области](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span><span class="sxs-lookup"><span data-stu-id="590fd-110">For more information on scoping filters, see [Attribute-based application provisioning with scoping filters](https://docs.microsoft.com/azure/active-directory/active-directory-saas-scoping-filters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="590fd-111">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="590fd-111">Next steps</span></span>
[<span data-ttu-id="590fd-112">Автоматическая подготовка пользователей и ее отзыв для приложений SaaS в Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="590fd-112">Automate User Provisioning and Deprovisioning to SaaS Applications with Azure Active Directory</span></span>](active-directory-saas-app-provisioning.md)

