---
title: "Проблема при создании приложения прокси приложения | Документы Майкрософт"
description: "Сведения об устранении неполадок при создании приложений прокси приложения на портале администрирования Azure AD."
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
ms.openlocfilehash: fe56f56162ba7186f1b660a5b44fcef38f1dee9d
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="problem-creating-an-application-proxy-application"></a><span data-ttu-id="20655-103">Проблема при создании приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="20655-103">Problem creating an Application Proxy application</span></span> 

<span data-ttu-id="20655-104">Ниже приведены некоторые наиболее распространенные проблемы, возникающие при создании приложения прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="20655-104">Below are some of the common issues people face when creating a new application proxy application.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="20655-105">Рекомендуемые документы</span><span class="sxs-lookup"><span data-stu-id="20655-105">Recommended documents</span></span> 

<span data-ttu-id="20655-106">Дополнительные сведения о создании приложения прокси приложения на портале администрирования см. в статье [Публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="20655-106">To learn more about creating an Application Proxy application through the Admin Portal, see [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="20655-107">Если при создании приложения по инструкциям из этого документа возникает ошибка, см. описание ошибки для получения сведений о ее исправлении.</span><span class="sxs-lookup"><span data-stu-id="20655-107">If you are following the steps in that document and are getting an error creating the application, see the error details for information and suggestions for how to fix the application.</span></span> <span data-ttu-id="20655-108">Большинство сообщений об ошибках включают в себя предлагаемое исправление.</span><span class="sxs-lookup"><span data-stu-id="20655-108">Most error messages include a suggested fix.</span></span> 

## <a name="specific-things-to-check"></a><span data-ttu-id="20655-109">Что нужно проверить</span><span class="sxs-lookup"><span data-stu-id="20655-109">Specific things to check</span></span>

<span data-ttu-id="20655-110">Чтобы избежать распространенных ошибок, проверьте следующее:</span><span class="sxs-lookup"><span data-stu-id="20655-110">To avoid common errors, verify:</span></span>

-   <span data-ttu-id="20655-111">Используется учетная запись администратора с разрешением на создание приложения прокси приложения.</span><span class="sxs-lookup"><span data-stu-id="20655-111">You are an administrator with permission to create an Application Proxy application</span></span>

-   <span data-ttu-id="20655-112">Внутренний URL-адрес является уникальным.</span><span class="sxs-lookup"><span data-stu-id="20655-112">The internal URL is unique</span></span>

-   <span data-ttu-id="20655-113">Внешний URL-адрес является уникальным.</span><span class="sxs-lookup"><span data-stu-id="20655-113">The external URL is unique</span></span>

-   <span data-ttu-id="20655-114">URL-адрес начинается с http или https и заканчивается на "/".</span><span class="sxs-lookup"><span data-stu-id="20655-114">The URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="20655-115">URL-адрес должен включать имя домена, а не IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="20655-115">The URL should be a domain name and not an IP address</span></span>

<span data-ttu-id="20655-116">Сообщение об ошибке при создании приложения должно отображаться в правом верхнем углу.</span><span class="sxs-lookup"><span data-stu-id="20655-116">The error message should display in the top right corner when you create the application.</span></span> <span data-ttu-id="20655-117">Для просмотра сообщений об ошибках также можно выбрать значок уведомления.</span><span class="sxs-lookup"><span data-stu-id="20655-117">You can also select the notification icon to see the error messages.</span></span>

   ![Уведомление](./media/application-proxy-config-problem/error-message.png)

## <a name="next-steps"></a><span data-ttu-id="20655-119">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="20655-119">Next steps</span></span>
[<span data-ttu-id="20655-120">Включение прокси приложения на портале Azure</span><span class="sxs-lookup"><span data-stu-id="20655-120">Enable Application Proxy in the Azure portal</span></span>](active-directory-application-proxy-enable.md)
