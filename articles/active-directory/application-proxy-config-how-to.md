---
title: "aaaHow tooconfigure приложение прокси приложения | Документы Microsoft"
description: "Узнайте, как toocreate Настройка приложения прокси приложения в рамках простой процедуры"
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
ms.openlocfilehash: c64019098fc124e4fe10b8288830bcd2b7239d3d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-an-application-proxy-application"></a><span data-ttu-id="c0d37-103">Как tooconfigure приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="c0d37-103">How tooconfigure an Application Proxy application</span></span>

<span data-ttu-id="c0d37-104">В этой статье помогут toounderstand как tooconfigure приложение прокси приложения в Azure AD tooexpose toohello приложений вашей локальной облака.</span><span class="sxs-lookup"><span data-stu-id="c0d37-104">This article help you toounderstand how tooconfigure an Application Proxy application within Azure AD tooexpose your on-premises applications toohello cloud.</span></span>

## <a name="recommended-documents"></a><span data-ttu-id="c0d37-105">Рекомендуемые документы</span><span class="sxs-lookup"><span data-stu-id="c0d37-105">Recommended documents</span></span> 

<span data-ttu-id="c0d37-106">toolearn о начальной конфигурации hello и создание приложения прокси приложения с помощью портала администрирования hello выполните hello [публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span><span class="sxs-lookup"><span data-stu-id="c0d37-106">toolearn about hello initial configurations and creation of an Application Proxy application through hello Admin Portal, follow hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal).</span></span>

<span data-ttu-id="c0d37-107">Дополнительные сведения о настройке соединителей см. в разделе [включить прокси приложения в Azure portal hello](active-directory-application-proxy-enable.md).</span><span class="sxs-lookup"><span data-stu-id="c0d37-107">For details on configuring Connectors, see [Enable Application Proxy in hello Azure portal](active-directory-application-proxy-enable.md).</span></span>

<span data-ttu-id="c0d37-108">Сведения об отправке сертификатов и пользовательских доменах см. в разделе [Работа с пользовательскими доменами в прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="c0d37-108">For information on uploading certificates and using custom domains, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span>

## <a name="create-hello-applicationsetting-hello-urls"></a><span data-ttu-id="c0d37-109">Создание URL-адреса для параметра/приложения hello hello</span><span class="sxs-lookup"><span data-stu-id="c0d37-109">Create hello Application/Setting hello URLs</span></span>

<span data-ttu-id="c0d37-110">Если вы следуете hello шагов в hello [публикация приложений с помощью прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) документация и являются сообщение об ошибке, создание приложения hello см. сведения об ошибке hello сведения и предложения по приложение hello toofix.</span><span class="sxs-lookup"><span data-stu-id="c0d37-110">If you are following hello steps in hello [Publish applications using Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/application-proxy-publish-azure-portal) documentation and are getting an error creating hello application, see hello error details for information and suggestions for how toofix hello application.</span></span> <span data-ttu-id="c0d37-111">Большинство сообщений об ошибках включают в себя предлагаемое исправление.</span><span class="sxs-lookup"><span data-stu-id="c0d37-111">Most error messages include a suggested fix.</span></span> <span data-ttu-id="c0d37-112">tooavoid распространенные ошибки, проверьте:</span><span class="sxs-lookup"><span data-stu-id="c0d37-112">tooavoid common errors, verify:</span></span>

-   <span data-ttu-id="c0d37-113">Вы являетесь администратором с toocreate разрешений приложения прокси приложения</span><span class="sxs-lookup"><span data-stu-id="c0d37-113">You are an administrator with permission toocreate an Application Proxy application</span></span>

-   <span data-ttu-id="c0d37-114">Hello внутренний URL-адрес является уникальным</span><span class="sxs-lookup"><span data-stu-id="c0d37-114">hello internal URL is unique</span></span>

-   <span data-ttu-id="c0d37-115">Hello внешний URL-адрес является уникальным</span><span class="sxs-lookup"><span data-stu-id="c0d37-115">hello external URL is unique</span></span>

-   <span data-ttu-id="c0d37-116">Здравствуйте, URL-адреса, начинающиеся с http или https, а заканчивают комментарий сочетанием «/»</span><span class="sxs-lookup"><span data-stu-id="c0d37-116">hello URLs start with http or https, and end with a “/”</span></span>

-   <span data-ttu-id="c0d37-117">Hello URL-адрес должен быть имени домена, а не IP-адрес</span><span class="sxs-lookup"><span data-stu-id="c0d37-117">hello URL should be a domain name, not an IP address</span></span>

<span data-ttu-id="c0d37-118">сообщение об ошибке Hello должны отображаться в правом верхнем углу hello, при создании приложения hello.</span><span class="sxs-lookup"><span data-stu-id="c0d37-118">hello error message should display in hello top right corner when you create hello application.</span></span> <span data-ttu-id="c0d37-119">Можно также выбрать hello уведомления значок toosee hello сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="c0d37-119">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Уведомление](./media/application-proxy-config-how-to/error-message.png)

## <a name="configure-connectorsconnector-groups"></a><span data-ttu-id="c0d37-121">Настройка соединителей и групп соединителей</span><span class="sxs-lookup"><span data-stu-id="c0d37-121">Configure connectors/connector groups</span></span>

<span data-ttu-id="c0d37-122">Если возникают неполадки при настройке приложения из-за предупреждения о соединители hello и группы соединителей см. инструкции о включении прокси приложения для сведений о том, как toodownload соединители.</span><span class="sxs-lookup"><span data-stu-id="c0d37-122">If you are having difficulty configuring your application because of warning about hello connectors and connector groups, see instructions on enabling Application Proxy for details on how toodownload connectors.</span></span> <span data-ttu-id="c0d37-123">Следует toolearn больше о соединителях см hello [соединители документации](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span><span class="sxs-lookup"><span data-stu-id="c0d37-123">If you want toolearn more about connectors, see hello [connectors documentation](https://docs.microsoft.com/azure/active-directory/application-proxy-understand-connectors).</span></span>

<span data-ttu-id="c0d37-124">Если соединителях находятся в неактивном состоянии, это означает, которых не удается tooreach hello службы.</span><span class="sxs-lookup"><span data-stu-id="c0d37-124">If your connectors are inactive, this means that they are unable tooreach hello service.</span></span> <span data-ttu-id="c0d37-125">Часто это потому, что все необходимые hello порты не открыты.</span><span class="sxs-lookup"><span data-stu-id="c0d37-125">This is often because all hello required ports are not open.</span></span> <span data-ttu-id="c0d37-126">toosee список необходимых портах разделе hello предварительным hello включении документации по прокси-сервера приложения.</span><span class="sxs-lookup"><span data-stu-id="c0d37-126">toosee a list of required ports, see hello pre-requisites section of hello enabling Application Proxy documentation.</span></span>

## <a name="upload-certificates-for-custom-domains"></a><span data-ttu-id="c0d37-127">Отправка сертификатов для пользовательских доменов</span><span class="sxs-lookup"><span data-stu-id="c0d37-127">Upload certificates for custom domains</span></span>

<span data-ttu-id="c0d37-128">Пользовательские домены позволяют toospecify hello домен вашей внешние URL-адреса.</span><span class="sxs-lookup"><span data-stu-id="c0d37-128">Custom Domains allow you toospecify hello domain of your external URLs.</span></span> <span data-ttu-id="c0d37-129">пользовательские домены toouse, потребуется tooupload hello сертификат для этого домена.</span><span class="sxs-lookup"><span data-stu-id="c0d37-129">toouse custom domains, you need tooupload hello certificate for that domain.</span></span> <span data-ttu-id="c0d37-130">Сведения об использовании сертификатов и пользовательских доменов см. в разделе [Работа с пользовательскими доменами в прокси приложения Azure AD](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span><span class="sxs-lookup"><span data-stu-id="c0d37-130">For information on using custom domains and certificates, see [Working with custom domains in Azure AD Application Proxy](https://docs.microsoft.com/azure/active-directory/active-directory-application-proxy-custom-domains).</span></span> 

<span data-ttu-id="c0d37-131">При возникновении проблем при загрузке сертификата, найдите сообщения об ошибке hello в портал hello Дополнительные сведения о hello проблема с сертификатом hello.</span><span class="sxs-lookup"><span data-stu-id="c0d37-131">If you are encountering issues uploading your certificate, look for hello error messages in hello portal for additional information on hello problem with hello certificate.</span></span> <span data-ttu-id="c0d37-132">Распространенные проблемы, связанные с сертификатами, включают следующие:</span><span class="sxs-lookup"><span data-stu-id="c0d37-132">Common certificate problems include:</span></span>

-   <span data-ttu-id="c0d37-133">Срок действия сертификата истек.</span><span class="sxs-lookup"><span data-stu-id="c0d37-133">Expired certificate</span></span>

-   <span data-ttu-id="c0d37-134">Сертификат является самозаверяющим.</span><span class="sxs-lookup"><span data-stu-id="c0d37-134">Certificate is self-signed</span></span>

-   <span data-ttu-id="c0d37-135">В сертификате отсутствует закрытый ключ hello</span><span class="sxs-lookup"><span data-stu-id="c0d37-135">Certificate is missing hello private key</span></span>

<span data-ttu-id="c0d37-136">Отображение сообщений об ошибках Hello в hello правом верхнем углу попытке tooupload hello сертификата.</span><span class="sxs-lookup"><span data-stu-id="c0d37-136">hello error message display in hello top right corner as you try tooupload hello certificate.</span></span> <span data-ttu-id="c0d37-137">Можно также выбрать hello уведомления значок toosee hello сообщения об ошибках.</span><span class="sxs-lookup"><span data-stu-id="c0d37-137">You can also select hello notification icon toosee hello error messages.</span></span>

   ![Уведомление](./media/application-proxy-config-how-to/error-message2.png)

## <a name="next-steps"></a><span data-ttu-id="c0d37-139">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c0d37-139">Next steps</span></span>
[<span data-ttu-id="c0d37-140">Публикация приложений с помощью прокси приложения Azure AD</span><span class="sxs-lookup"><span data-stu-id="c0d37-140">Publish applications using Azure AD Application Proxy</span></span>](application-proxy-publish-azure-portal.md)
