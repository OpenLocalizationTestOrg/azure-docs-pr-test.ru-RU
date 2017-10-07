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
# <a name="requestdisallowedbypolicy-error-with-azure-resource-policy"></a>Ошибка RequestDisallowedByPolicy с политикой ресурсов Azure

В этой статье описывается hello причиной ошибки RequestDisallowedByPolicy hello, он также предоставляет решение для этой ошибки.

## <a name="symptom"></a>Симптом

При попытке toodo действия во время развертывания, может появиться **RequestDisallowedByPolicy** выполнить ошибка, не позволяющая действие hello. Hello ниже приведен образец hello ошибки.

```
{
  "statusCode": "Forbidden",
  "serviceRequestId": null,
  "statusMessage": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}",
  "responseBody": "{\"error\":{\"code\":\"RequestDisallowedByPolicy\",\"message\":\"hello resource action 'Microsoft.Network/publicIpAddresses/write' is disallowed by one or more policies. Policy identifier(s): '/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition'.\"}}"
}
```

## <a name="troubleshooting"></a>Устранение неполадок

tooretrieve подробные сведения о hello политики блокировки развертывания, используйте hello, выполнив один из методов hello.

### <a name="method-1"></a>Метод 1

В PowerShell, предоставить идентификатор политики как hello **идентификатор** параметр tooretrieve подробные сведения о hello политики блокировки развертывания.

```PowerShell
(Get-AzureRmPolicyDefinition -Id "/subscriptions/{guid}/providers/Microsoft.Authorization/policyDefinitions/regionPolicyDefinition").Properties.policyRule | ConvertTo-Json
```

### <a name="method-2"></a>Метод 2 

В Azure 2.0 CLI предоставить имя определения политики hello hello. 

```azurecli
az policy definition show --name regionPolicyAssignment
```

## <a name="solution"></a>Решение

Возможно, ваш ИТ-отдел для обеспечения безопасности или соответствия применяет некоторые политики ресурсов, например такие, которые запрещают создавать общедоступные IP-адреса, сетевые группы безопасности, определяемые пользователем маршруты или таблицы маршрутизации. В образце hello hello сообщения об ошибке, описанной в разделе «Проблема» hello, называется политики hello **regionPolicyDefinition**, но он может отличаться.
tooresolve эту проблему, работы ИТ-политикам отдел tooreview hello ресурсов и определить, как tooperform hello запрошенное действие в соответствии с этими политиками.


Дополнительные сведения см. в разделе hello в следующих статьях:

- [Общие сведения о политике ресурсов](resource-manager-policy.md)
- [Описание для RequestDisallowedByPolicy в статье о распространенных ошибках развертывания](resource-manager-common-deployment-errors.md#requestdisallowedbypolicy)

 


