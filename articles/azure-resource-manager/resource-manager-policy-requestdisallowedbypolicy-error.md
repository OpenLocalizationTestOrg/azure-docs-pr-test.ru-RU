---
title: "Ошибка RequestDisallowedByPolicy с политикой ресурсов Azure | Документация Майкрософт"
description: "Описывает причину ошибки RequestDisallowedByPolicy."
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
ms.openlocfilehash: 182a27e444c2f5db66d518a1a0c608d3e319d553
ms.sourcegitcommit: 422efcbac5b6b68295064bd545132fcc98349d01
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/29/2017
---
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a><span data-ttu-id="886ef-103">Ошибка RequestDisallowedByPolicy с политикой ресурсов Azure</span><span class="sxs-lookup"><span data-stu-id="886ef-103">RequestDisallowedByPolicy error with Azure resource policy</span></span>

<span data-ttu-id="886ef-104">В этой статье описывается причина ошибки RequestDisallowedByPolicy, а также предлагается решение для ее устранения.</span><span class="sxs-lookup"><span data-stu-id="886ef-104">This article describes the cause of the RequestDisallowedByPolicy error, it also provides solution for this error.</span></span>

## <a name="symptom"></a><span data-ttu-id="886ef-105">Симптом</span><span class="sxs-lookup"><span data-stu-id="886ef-105">Symptom</span></span>

<span data-ttu-id="886ef-106">Когда вы пытаетесь выполнить действие во время развертывания, может появиться ошибка **RequestDisallowedByPolicy**, которая блокирует выполнение этого действия.</span><span class="sxs-lookup"><span data-stu-id="886ef-106">When you try to do an action during deployment, you might receive a **RequestDisallowedByPolicy** error that prevents the action be performed.</span></span> <span data-ttu-id="886ef-107">Вот пример такой ошибки:</span><span class="sxs-lookup"><span data-stu-id="886ef-107">The following is a sample of the error:</span></span>

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"The resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a><span data-ttu-id="886ef-108">Устранение неполадок</span><span class="sxs-lookup"><span data-stu-id="886ef-108">Troubleshooting</span></span>

<span data-ttu-id="886ef-109">Чтобы получить информацию о том, какая политика блокирует развертывание, используйте один из следующих методов.</span><span class="sxs-lookup"><span data-stu-id="886ef-109">To retrieve details about the policy that blocked your deployment, use the following one of the methods:</span></span>

### <a name="method-1"></a><span data-ttu-id="886ef-110">Метод 1</span><span class="sxs-lookup"><span data-stu-id="886ef-110">Method 1</span></span>

<span data-ttu-id="886ef-111">В PowerShell укажите идентификатор политики в качестве значения для параметра **Id**, чтобы получить сведения о политике, заблокировавшей развертывание.</span><span class="sxs-lookup"><span data-stu-id="886ef-111">In PowerShell, provide that policy identifier as the **Id** parameter to retrieve details about the policy that blocked your deployment.</span></span>

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a><span data-ttu-id="886ef-112">Метод 2</span><span class="sxs-lookup"><span data-stu-id="886ef-112">Method 2</span></span> 

<span data-ttu-id="886ef-113">В Azure CLI 2.0 укажите имя определения политики.</span><span class="sxs-lookup"><span data-stu-id="886ef-113">In Azure CLI 2.0, provide the name of the policy definition:</span></span> 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a><span data-ttu-id="886ef-114">Решение</span><span class="sxs-lookup"><span data-stu-id="886ef-114">Solution</span></span>

<span data-ttu-id="886ef-115">Возможно, ваш ИТ-отдел для обеспечения безопасности или соответствия применяет некоторые политики ресурсов, например такие, которые запрещают создавать общедоступные IP-адреса, сетевые группы безопасности, определяемые пользователем маршруты или таблицы маршрутизации.</span><span class="sxs-lookup"><span data-stu-id="886ef-115">For security or compliance, your IT department might enforce a resource policy that prohibits creating Public IP addresses, Network Security Groups, User-Defined Routes, or route tables.</span></span> <span data-ttu-id="886ef-116">В нашем примере ошибки, представленном в разделе "Проблема", проблемная политика имеет имя **regionPolicyDefinition**. Это имя может быть любым.</span><span class="sxs-lookup"><span data-stu-id="886ef-116">In the sample of the error message that is described in the "Symptoms" section, the policy is named **regionPolicyDefinition**, but it could be different.</span></span>
<span data-ttu-id="886ef-117">Чтобы устранить такую проблему, свяжитесь с ИТ-отделом, совместно оцените политики ресурсов и определите приемлемый метод выполнить нужное действие, не нарушая политики организации.</span><span class="sxs-lookup"><span data-stu-id="886ef-117">To resolve this problem, work with your IT department to review the resource policies, and determine how to perform the requested action in compliance with those policies.</span></span>


<span data-ttu-id="886ef-118">Дополнительные сведения см. в следующих статьях:</span><span class="sxs-lookup"><span data-stu-id="886ef-118">For more information, see the following articles:</span></span>

- [<span data-ttu-id="886ef-119">Общие сведения о политике ресурсов</span><span class="sxs-lookup"><span data-stu-id="886ef-119">Resource policy overview</span></span>](resource-manager-policy.md)
- [<span data-ttu-id="886ef-120">Описание для RequestDisallowedByPolicy в статье о распространенных ошибках развертывания</span><span class="sxs-lookup"><span data-stu-id="886ef-120">Common deployment errors-RequestDisallowedByPolicy</span></span>](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


