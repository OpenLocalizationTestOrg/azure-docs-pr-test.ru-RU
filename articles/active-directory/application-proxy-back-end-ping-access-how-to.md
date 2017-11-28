---
title: "Настройка приложения прокси приложения для использования PingAccess | Документы Майкрософт"
description: "Сведения об использовании PingAccess для предоставления преимуществ прокси приложения в приложениях, использующих проверку подлинности на основе заголовков."
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
ms.openlocfilehash: a9da67373465cebbdbecae5c8fb8bd0a0ee3c171
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-an-application-proxy-application-to-use-pingaccess"></a><span data-ttu-id="1859f-103">Настройка приложения прокси приложения для использования PingAccess</span><span class="sxs-lookup"><span data-stu-id="1859f-103">How to configure an Application Proxy application to use PingAccess</span></span>

<span data-ttu-id="1859f-104">Наше сотрудничество с PingAccess позволило предоставить преимущества прокси приложения в приложениях, использующих проверку подлинности на основе заголовков.</span><span class="sxs-lookup"><span data-stu-id="1859f-104">Our collaboration with PingAccess now allows you to extend the benefits of Application Proxy to applications using header-based authentication.</span></span> <span data-ttu-id="1859f-105">Если ваши приложения не используют заголовки, см. нашу [документацию по единому входу](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) для получения сведений о других возможностях.</span><span class="sxs-lookup"><span data-stu-id="1859f-105">If your applications do not use headers, see our [Single Sign-On documentation](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-sso-using-kcd) for details on other options.</span></span>

## <a name="overview-of-steps-and-recommended-documents"></a><span data-ttu-id="1859f-106">Обзор шагов и рекомендуемые документы</span><span class="sxs-lookup"><span data-stu-id="1859f-106">Overview of steps and recommended documents</span></span>

<span data-ttu-id="1859f-107">Чтобы настроить приложение для использования PingAccess, нужно выполнить четыре шага:</span><span class="sxs-lookup"><span data-stu-id="1859f-107">To configure an application with PingAccess, there are four steps:</span></span>

1.  <span data-ttu-id="1859f-108">Настройка соединителей прокси приложения</span><span class="sxs-lookup"><span data-stu-id="1859f-108">Configure Application Proxy Connectors</span></span>

2.  <span data-ttu-id="1859f-109">Создание приложения прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="1859f-109">Create an Azure AD Application Proxy Application</span></span>

3.  <span data-ttu-id="1859f-110">Скачивание и настройка PingAccess</span><span class="sxs-lookup"><span data-stu-id="1859f-110">Download & Configure PingAccess</span></span>

4.  <span data-ttu-id="1859f-111">Настройка приложений в PingAccess</span><span class="sxs-lookup"><span data-stu-id="1859f-111">Configure Applications in PingAccess</span></span>

<span data-ttu-id="1859f-112">Сведения о каждом из этих шагов см. в нашей [документации по единому входу с использованием заголовков](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span><span class="sxs-lookup"><span data-stu-id="1859f-112">For details on each of these steps, see our [Single Sign-On with Headers documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-ping-access).</span></span>
