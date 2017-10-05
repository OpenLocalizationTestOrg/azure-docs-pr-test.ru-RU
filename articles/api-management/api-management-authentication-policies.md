---
title: "Политики аутентификации в службе управления API Azure | Документация Майкрософт"
description: "Сведения о политиках аутентификации, доступных для использования в службе управления API Azure."
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
ms.openlocfilehash: 63ef20a56ab7721f9ecc7025d05963cc4b0c27a0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-authentication-policies"></a><span data-ttu-id="d4f35-103">Политики аутентификации в службе управления API</span><span class="sxs-lookup"><span data-stu-id="d4f35-103">API Management authentication policies</span></span>
<span data-ttu-id="d4f35-104">В этой статье рассматриваются приведенные ниже политики управления API.</span><span class="sxs-lookup"><span data-stu-id="d4f35-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="d4f35-105">Дополнительные сведения о добавлении и настройке политик см. в статье о [политиках в управлении API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d4f35-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d4f35-106"><a name="AuthenticationPolicies"></a> Политики аутентификации</span><span class="sxs-lookup"><span data-stu-id="d4f35-106"><a name="AuthenticationPolicies"></a> Authentication policies</span></span>  
  
-   <span data-ttu-id="d4f35-107">[Обычная проверка подлинности](api-management-authentication-policies.md#Basic) – обычная проверка подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="d4f35-107">[Authenticate with Basic](api-management-authentication-policies.md#Basic) - Authenticate with a backend service using Basic authentication.</span></span>  
  
-   <span data-ttu-id="d4f35-108">[Аутентификация с помощью сертификата клиента](api-management-authentication-policies.md#ClientCertificate) – аутентификация внутренней службы с помощью сертификатов клиентов.</span><span class="sxs-lookup"><span data-stu-id="d4f35-108">[Authenticate with client certificate](api-management-authentication-policies.md#ClientCertificate) - Authenticate with a backend service using client certificates.</span></span>  
  
##  <span data-ttu-id="d4f35-109"><a name="Basic"></a> Обычная проверка подлинности</span><span class="sxs-lookup"><span data-stu-id="d4f35-109"><a name="Basic"></a> Authenticate with Basic</span></span>  
 <span data-ttu-id="d4f35-110">Используйте политику `authentication-basic` для обычной проверки подлинности внутренней службы.</span><span class="sxs-lookup"><span data-stu-id="d4f35-110">Use the `authentication-basic` policy to authenticate with a backend service using Basic authentication.</span></span> <span data-ttu-id="d4f35-111">Эта политика задает для заголовка авторизации HTTP значение, соответствующее учетным данным, предоставленным в политике.</span><span class="sxs-lookup"><span data-stu-id="d4f35-111">This policy effectively sets the HTTP Authorization header to the value corresponding to the credentials provided in the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d4f35-112">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d4f35-112">Policy statement</span></span>  
  
```xml  
<authentication-basic username="username" password="password" />  
```  
  
### <a name="example"></a><span data-ttu-id="d4f35-113">Пример</span><span class="sxs-lookup"><span data-stu-id="d4f35-113">Example</span></span>  
  
```xml  
<authentication-basic username="testuser" password="testpassword" />  
```  
  
### <a name="elements"></a><span data-ttu-id="d4f35-114">Элементы</span><span class="sxs-lookup"><span data-stu-id="d4f35-114">Elements</span></span>  
  
|<span data-ttu-id="d4f35-115">Имя</span><span class="sxs-lookup"><span data-stu-id="d4f35-115">Name</span></span>|<span data-ttu-id="d4f35-116">Описание</span><span class="sxs-lookup"><span data-stu-id="d4f35-116">Description</span></span>|<span data-ttu-id="d4f35-117">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d4f35-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d4f35-118">authentication-basic</span><span class="sxs-lookup"><span data-stu-id="d4f35-118">authentication-basic</span></span>|<span data-ttu-id="d4f35-119">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d4f35-119">Root element.</span></span>|<span data-ttu-id="d4f35-120">Да</span><span class="sxs-lookup"><span data-stu-id="d4f35-120">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d4f35-121">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d4f35-121">Attributes</span></span>  
  
|<span data-ttu-id="d4f35-122">Имя</span><span class="sxs-lookup"><span data-stu-id="d4f35-122">Name</span></span>|<span data-ttu-id="d4f35-123">Описание</span><span class="sxs-lookup"><span data-stu-id="d4f35-123">Description</span></span>|<span data-ttu-id="d4f35-124">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d4f35-124">Required</span></span>|<span data-ttu-id="d4f35-125">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d4f35-125">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d4f35-126">Имя пользователя</span><span class="sxs-lookup"><span data-stu-id="d4f35-126">username</span></span>|<span data-ttu-id="d4f35-127">Задает имя пользователя для обычных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d4f35-127">Specifies the username of the Basic credential.</span></span>|<span data-ttu-id="d4f35-128">Да</span><span class="sxs-lookup"><span data-stu-id="d4f35-128">Yes</span></span>|<span data-ttu-id="d4f35-129">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d4f35-129">N/A</span></span>|  
|<span data-ttu-id="d4f35-130">пароль</span><span class="sxs-lookup"><span data-stu-id="d4f35-130">password</span></span>|<span data-ttu-id="d4f35-131">Задает пароль для обычных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d4f35-131">Specifies the password of the Basic credential.</span></span>|<span data-ttu-id="d4f35-132">Да</span><span class="sxs-lookup"><span data-stu-id="d4f35-132">Yes</span></span>|<span data-ttu-id="d4f35-133">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d4f35-133">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d4f35-134">Использование</span><span class="sxs-lookup"><span data-stu-id="d4f35-134">Usage</span></span>  
 <span data-ttu-id="d4f35-135">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d4f35-135">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d4f35-136">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d4f35-136">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d4f35-137">**Области политики:** API.</span><span class="sxs-lookup"><span data-stu-id="d4f35-137">**Policy scopes:** API</span></span>  
  
##  <span data-ttu-id="d4f35-138"><a name="ClientCertificate"></a> Аутентификация с помощью сертификата клиента</span><span class="sxs-lookup"><span data-stu-id="d4f35-138"><a name="ClientCertificate"></a> Authenticate with client certificate</span></span>  
 <span data-ttu-id="d4f35-139">Используйте политику `authentication-certificate` для аутентификации внутренней службы с помощью сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="d4f35-139">Use the `authentication-certificate` policy to authenticate with a backend service using client certificate.</span></span> <span data-ttu-id="d4f35-140">Сертификат сначала должен быть [установлен в службу управления API](http://go.microsoft.com/fwlink/?LinkID=511599) и идентифицирован по его отпечатку.</span><span class="sxs-lookup"><span data-stu-id="d4f35-140">The certificate needs to be [installed into API Management](http://go.microsoft.com/fwlink/?LinkID=511599) first and is identified by its thumbprint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d4f35-141">Правило политики</span><span class="sxs-lookup"><span data-stu-id="d4f35-141">Policy statement</span></span>  
  
```xml  
<authentication-certificate thumbprint="thumbprint" />  
```  
  
### <a name="example"></a><span data-ttu-id="d4f35-142">Пример</span><span class="sxs-lookup"><span data-stu-id="d4f35-142">Example</span></span>  
  
```xml  
<authentication-certificate thumbprint="....." />  
```  
  
### <a name="elements"></a><span data-ttu-id="d4f35-143">Элементы</span><span class="sxs-lookup"><span data-stu-id="d4f35-143">Elements</span></span>  
  
|<span data-ttu-id="d4f35-144">Имя</span><span class="sxs-lookup"><span data-stu-id="d4f35-144">Name</span></span>|<span data-ttu-id="d4f35-145">Описание</span><span class="sxs-lookup"><span data-stu-id="d4f35-145">Description</span></span>|<span data-ttu-id="d4f35-146">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d4f35-146">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d4f35-147">authentication-certificate</span><span class="sxs-lookup"><span data-stu-id="d4f35-147">authentication-certificate</span></span>|<span data-ttu-id="d4f35-148">Корневой элемент.</span><span class="sxs-lookup"><span data-stu-id="d4f35-148">Root element.</span></span>|<span data-ttu-id="d4f35-149">Да</span><span class="sxs-lookup"><span data-stu-id="d4f35-149">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d4f35-150">Атрибуты</span><span class="sxs-lookup"><span data-stu-id="d4f35-150">Attributes</span></span>  
  
|<span data-ttu-id="d4f35-151">Имя</span><span class="sxs-lookup"><span data-stu-id="d4f35-151">Name</span></span>|<span data-ttu-id="d4f35-152">Описание</span><span class="sxs-lookup"><span data-stu-id="d4f35-152">Description</span></span>|<span data-ttu-id="d4f35-153">Обязательно</span><span class="sxs-lookup"><span data-stu-id="d4f35-153">Required</span></span>|<span data-ttu-id="d4f35-154">значение по умолчанию</span><span class="sxs-lookup"><span data-stu-id="d4f35-154">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d4f35-155">thumbprint</span><span class="sxs-lookup"><span data-stu-id="d4f35-155">thumbprint</span></span>|<span data-ttu-id="d4f35-156">Отпечаток для сертификата клиента.</span><span class="sxs-lookup"><span data-stu-id="d4f35-156">The thumbprint for the client certificate.</span></span>|<span data-ttu-id="d4f35-157">Да</span><span class="sxs-lookup"><span data-stu-id="d4f35-157">Yes</span></span>|<span data-ttu-id="d4f35-158">Недоступно</span><span class="sxs-lookup"><span data-stu-id="d4f35-158">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d4f35-159">Использование</span><span class="sxs-lookup"><span data-stu-id="d4f35-159">Usage</span></span>  
 <span data-ttu-id="d4f35-160">Эта политика может использоваться в следующих [разделах](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) и [областях](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="d4f35-160">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d4f35-161">**Разделы политики:** inbound.</span><span class="sxs-lookup"><span data-stu-id="d4f35-161">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d4f35-162">**Области политики:** API.</span><span class="sxs-lookup"><span data-stu-id="d4f35-162">**Policy scopes:** API</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="d4f35-163">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d4f35-163">Next steps</span></span>
<span data-ttu-id="d4f35-164">Дополнительные сведения о работе с политиками см. в статье со справочными материалами по [политикам в службе управления API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d4f35-164">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  