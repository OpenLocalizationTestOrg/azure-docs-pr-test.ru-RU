---
title: "Ошибка aaaRequestDisallowedByPolicy с политикой ресурсов Azure | Документы Microsoft"
description: "Описывает причину ошибки RequestDisallowedByPolicy hello hello."
services: azure-resource-manager,azure-portal
documentationcenter: 
author: genlin
manager: cshepard
editor: 
ms.service: azure-resource-manager
ms.workload: multiple
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/12/2017
ms.author: genli
ms.openlocfilehash: 7870e40205cf433ccb4ba02376b5fe809f20d0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="c1cb8-103">Ошибка RequestDisallowedByPolicy с политикой ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="c1cb8-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="c1cb8-104">В этой статье описывается hello причиной ошибки RequestDisallowedByPolicy hello, он также предоставляет решение для этой ошибки.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-104">This article describes hello cause of hello RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="c1cb8-105">Симптом</span><span class="sxs-lookup"><span data-stu-id="c1cb8-105">Symptom</span></span>

<span data-ttu-id="c1cb8-106">При попытке toodo действия во время развертывания, может появиться **RequestDisallowedByPolicy** выполнить ошибка, не позволяющая действие hello.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-106">When you try toodo an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents hello action be performed.</span></span> <span data-ttu-id="c1cb8-107">Hello ниже приведен образец hello ошибки.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-107">hello following is a sample of hello error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="c1cb8-108">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="c1cb8-108">Troubleshooting</span></span>

<span data-ttu-id="c1cb8-109">tooretrieve подробные сведения о hello политики блокировки развертывания, используйте hello, выполнив один из методов hello.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-109">tooretrieve details about hello policy that blocked your deployment, use hello following one of hello methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="c1cb8-110">Метод 1</span><span class="sxs-lookup"><span data-stu-id="c1cb8-110">Method 1</span></span>

<span data-ttu-id="c1cb8-111">В PowerShell, предоставить идентификатор политики как hello **идентификатор** параметр tooretrieve подробные сведения о hello политики блокировки развертывания.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-111">In PowerShell, provide that policy identifier as hello **Id** parameter tooretrieve details about hello policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="c1cb8-112">Метод 2</span><span class="sxs-lookup"><span data-stu-id="c1cb8-112">Method 2</span></span> 

<span data-ttu-id="c1cb8-113">В Azure 2.0 CLI предоставить имя определения политики hello hello.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-113">In Azure CLI 2.0, provide hello name of hello policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="c1cb8-114">Решение</span><span class="sxs-lookup"><span data-stu-id="c1cb8-114">Solution</span></span>

<span data-ttu-id="c1cb8-115">Возможно, ваш ИТ-отдел для обеспечения безопасности или соответствия применяет некоторые политики ресурсов, например такие, которые запрещают создавать общедоступные IP-адреса, сетевые группы безопасности, определяемые пользователем маршруты или таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="c1cb8-116">В образце hello hello сообщения об ошибке, описанной в разделе «Проблема» hello, называется политики hello **regionPolicyDefinition**, но он может отличаться.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-116">In hello sample of hello error message that is described in hello "Symptoms" section, hello policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="c1cb8-117">tooresolve эту проблему, работы ИТ-политикам отдел tooreview hello ресурсов и определить, как tooperform hello запрошенное действие в соответствии с этими политиками.</span><span class="sxs-lookup"><span data-stu-id="c1cb8-117">tooresolve this problem, work with your IT department tooreview hello resource policies, and determine how tooperform hello requested action in compliance with those policies.</span></span>


<span data-ttu-id="c1cb8-118">Дополнительные сведения см. в разделе hello в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="c1cb8-118">For more information, see hello following articles:</span></span>

- [<span data-ttu-id="c1cb8-119">Общие сведения о политике ресурсов</span><span class="sxs-lookup"><span data-stu-id="c1cb8-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="c1cb8-120">Описание для RequestDisallowedByPolicy в статье о распространенных ошибках развертывания</span><span class="sxs-lookup"><span data-stu-id="c1cb8-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


