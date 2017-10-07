---
title: "политики проверки подлинности API Management aaaAzure | Документы Microsoft"
description: "Дополнительные сведения о hello политики проверки подлинности, доступные для использования в службе управления API Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 061702a7-3a78-472b-a54a-f3b1e332490d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ce93cced66cb67520e97c7c15f3685bffb08e1f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="2de50-103">Политики аутентификации в службе управления API</span><span class="sxs-lookup"><span data-stu-id="2de50-103">API Management authentication policies</span></span>
<span data-ttu-id="2de50-104">Здесь вы найдете ссылку для hello следующих политиках управления интерфейсами API.</span><span class="sxs-lookup"><span data-stu-id="2de50-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="2de50-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="2de50-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="2de50-106"><a name="AuthenticationPolicies"></a> Политики аутентификации</span><span class="sxs-lookup"><span data-stu-id="2de50-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="2de50-107">[Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="2de50-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="2de50-108">[Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="2de50-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="2de50-109"><a name="Basic"></a> Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="2de50-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="2de50-110">Используйте hello `authentication-basic` tooauthenticate политики с помощью серверной службы с использованием обычной проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="2de50-110">Use hello `authentication-basic` policy tooauthenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="2de50-111">Эта политика фактически устанавливает toohello заголовок авторизации HTTP hello значение соответствующего toohello учетные данные, указанные в политике hello.</span><span class="sxs-lookup"><span data-stu-id="2de50-111">This policy effectively sets hello HTTP Authorization header toohello value corresponding toohello credentials provided in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2de50-112">Правило политики</span><span class="sxs-lookup"><span data-stu-id="2de50-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="2de50-113">Пример</span><span class="sxs-lookup"><span data-stu-id="2de50-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="2de50-114">Элементы</span><span class="sxs-lookup"><span data-stu-id="2de50-114">Elements</span></span>  
  
|<span data-ttu-id="2de50-115">Имя</span><span class="sxs-lookup"><span data-stu-id="2de50-115">Name</span></span>|<span data-ttu-id="2de50-116">Описание</span><span class="sxs-lookup"><span data-stu-id="2de50-116">Description</span></span>|<span data-ttu-id="2de50-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2de50-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="2de50-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="2de50-118">authentication-basic</span></span>|<span data-ttu-id="2de50-119">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="2de50-119">Root element.</span></span>|<span data-ttu-id="2de50-120">Да</span><span class="sxs-lookup"><span data-stu-id="2de50-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2de50-121">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="2de50-121">Attributes</span></span>  
  
|<span data-ttu-id="2de50-122">Имя</span><span class="sxs-lookup"><span data-stu-id="2de50-122">Name</span></span>|<span data-ttu-id="2de50-123">Описание</span><span class="sxs-lookup"><span data-stu-id="2de50-123">Description</span></span>|<span data-ttu-id="2de50-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2de50-124">Required</span></span>|<span data-ttu-id="2de50-125">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2de50-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="2de50-126">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="2de50-126">username</span></span>|<span data-ttu-id="2de50-127">Указывает имя пользователя hello hello основных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="2de50-127">Specifies hello username of hello Basic credential.</span></span>|<span data-ttu-id="2de50-128">Да</span><span class="sxs-lookup"><span data-stu-id="2de50-128">Yes</span></span>|<span data-ttu-id="2de50-129">Недоступно</span><span class="sxs-lookup"><span data-stu-id="2de50-129">N/A</span></span>|  
|<span data-ttu-id="2de50-130">пароль</span><span class="sxs-lookup"><span data-stu-id="2de50-130">password</span></span>|<span data-ttu-id="2de50-131">Указывает пароль hello hello основных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="2de50-131">Specifies hello password of hello Basic credential.</span></span>|<span data-ttu-id="2de50-132">Да</span><span class="sxs-lookup"><span data-stu-id="2de50-132">Yes</span></span>|<span data-ttu-id="2de50-133">Недоступно</span><span class="sxs-lookup"><span data-stu-id="2de50-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2de50-134">Использование</span><span class="sxs-lookup"><span data-stu-id="2de50-134">Usage</span></span>  
 <span data-ttu-id="2de50-135">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2de50-135">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2de50-136">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="2de50-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="2de50-137">**Области политики:** API.</span><span class="sxs-lookup"><span data-stu-id="2de50-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="2de50-138"><a name="ClientCertificate"></a> Аутентификация с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="2de50-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="2de50-139">Используйте hello `authentication-certificate` tooauthenticate политики с помощью серверной службы с использованием клиентского сертификата.</span><span class="sxs-lookup"><span data-stu-id="2de50-139">Use hello `authentication-certificate` policy tooauthenticate with a backend service using client certificate.</span></span> <span data-ttu-id="2de50-140">Hello сертификат должен toobe [установлен в API Management](http://go.microsoft.com/fwlink/?LinkID=511599) первый и определяется его отпечатком.</span><span class="sxs-lookup"><span data-stu-id="2de50-140">hello certificate needs toobe [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="2de50-141">Правило политики</span><span class="sxs-lookup"><span data-stu-id="2de50-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="2de50-142">Пример</span><span class="sxs-lookup"><span data-stu-id="2de50-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="2de50-143">Элементы</span><span class="sxs-lookup"><span data-stu-id="2de50-143">Elements</span></span>  
  
|<span data-ttu-id="2de50-144">Имя</span><span class="sxs-lookup"><span data-stu-id="2de50-144">Name</span></span>|<span data-ttu-id="2de50-145">Описание</span><span class="sxs-lookup"><span data-stu-id="2de50-145">Description</span></span>|<span data-ttu-id="2de50-146">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2de50-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="2de50-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="2de50-147">authentication-certificate</span></span>|<span data-ttu-id="2de50-148">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="2de50-148">Root element.</span></span>|<span data-ttu-id="2de50-149">Да</span><span class="sxs-lookup"><span data-stu-id="2de50-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="2de50-150">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="2de50-150">Attributes</span></span>  
  
|<span data-ttu-id="2de50-151">Имя</span><span class="sxs-lookup"><span data-stu-id="2de50-151">Name</span></span>|<span data-ttu-id="2de50-152">Описание</span><span class="sxs-lookup"><span data-stu-id="2de50-152">Description</span></span>|<span data-ttu-id="2de50-153">Обязательно</span><span class="sxs-lookup"><span data-stu-id="2de50-153">Required</span></span>|<span data-ttu-id="2de50-154">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="2de50-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="2de50-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="2de50-155">thumbprint</span></span>|<span data-ttu-id="2de50-156">отпечаток сертификата клиента hello Hello.</span><span class="sxs-lookup"><span data-stu-id="2de50-156">hello thumbprint for hello client certificate.</span></span>|<span data-ttu-id="2de50-157">Да</span><span class="sxs-lookup"><span data-stu-id="2de50-157">Yes</span></span>|<span data-ttu-id="2de50-158">Недоступно</span><span class="sxs-lookup"><span data-stu-id="2de50-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="2de50-159">Использование</span><span class="sxs-lookup"><span data-stu-id="2de50-159">Usage</span></span>  
 <span data-ttu-id="2de50-160">Эта политика может использоваться в следующие политики hello [разделы](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областей](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="2de50-160">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="2de50-161">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="2de50-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="2de50-162">**Области политики:** API.</span><span class="sxs-lookup"><span data-stu-id="2de50-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="2de50-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="2de50-163">Next steps</span></span>
<span data-ttu-id="2de50-164">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="2de50-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  