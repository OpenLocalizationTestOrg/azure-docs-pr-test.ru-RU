---
title: "Доменные службы Azure Active Directory: включение ограниченного делегирования Kerberos | Документация Майкрософт"
description: "Включение ограниченного делегирования Kerberos в управляемых доменах доменных служб Azure Active Directory"
services: active-directory-ds
documentationcenter: 
author: mahesh-unnikrishnan
manager: stevenpo
editor: curtand
ms.assetid: 938a5fbc-2dd1-4759-bcce-628a6e19ab9d
ms.service: active-directory-ds
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: maheshu
ms.openlocfilehash: d32547c8018dd1f99c992e95a01d2711d460a261
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-kerberos-constrained-delegation-kcd-on-a-managed-domain"></a>Настройка ограниченного делегирования Kerberos в управляемом домене
Во многих приложениях нужно tooaccess ресурсов в контексте hello hello пользователя. Active Directory поддерживает делегирование Kerberos — механизм, который позволяет использовать эту возможность. Кроме того вы можете ограничить делегирование, чтобы только определенных ресурсов может осуществляться в контексте hello hello пользователя. Управляемые домены доменных служб Azure AD отличаются от традиционных доменов Active Directory, поскольку они безопаснее заблокированы.

В этой статье показано, как tooconfigure kerberos ограниченного делегирования в Azure AD управляемого домена доменных служб.

## <a name="kerberos-constrained-delegation-kcd"></a>Ограниченное делегирование Kerberos
Делегирование Kerberos позволяет учетной записи tooimpersonate другой ресурсам участника (например, пользователь) tooaccess безопасности. Рассмотрим веб-приложение, которое обращается к серверной части веб-API в контексте пользователя hello. В этом примере hello веб-приложения (выполняется в контексте учетной записи службы или учетной записи компьютера/machine hello) олицетворяют hello пользователя при доступе к ресурсу hello (фоновая веб-API). Делегирование Kerberos не защищен, поскольку не ограничивает hello hello ресурсы олицетворения учетной записи может получить доступ в контексте hello hello пользователя.

Ограниченное делегирование Kerberos (KCD) ограничивает hello, службы и ресурсы toowhich hello указанного сервера может действовать от имени hello пользователя. Традиционные проверки подлинности Kerberos требуется tooconfigure привилегии администратора домена учетной записи домена для службы и он ограничивает hello учетной записи tooa один домен.

Традиционное ограниченное делегирование Kerberos связано с несколькими трудностями. В предыдущих версиях операционных систем, где hello администратор домена настроил службы hello администратор служб hello имел нет удобного способа tooknow, какие службы интерфейса делегированы toohello ресурсов службы осуществлялись. И все службы интерфейса, которые могли делегировать службы ресурсов tooa под угрозой атаки. Если было настроенных toodelegate tooresource службы сервера, на котором размещалась служба интерфейса был скомпрометирован, службы hello ресурсов также могли быть скомпрометированы.

> [!NOTE]
> В управляемом домене доменных служб Azure AD у вас нет привилегий администратора домена. Таким образом **традиционное ограниченное делегирование Kerberos нельзя настроить в управляемом домене**. Используйте основанное на ресурсах ограниченное делегирование Kerberos, как описано в этой статье. Этот механизм также более безопасен.
>
>

## <a name="resource-based-kerberos-constrained-delegation"></a>Ограниченное делегирование Kerberos на основе ресурсов
В Windows Server 2012 R2 и Windows Server 2012 hello возможность tooconfigure ограниченное делегирование для службы hello была передана от администратора службы toohello администратора домена hello. Таким образом Здравствуйте, администратор служб может разрешить или запретить службы интерфейса. Эта модель называется **ограниченное делегирование Kerberos на основе ресурсов**.

Ограниченное делегирование Kerberos на основе ресурсов настраивается с помощью PowerShell. Используйте hello Set-ADComputer или командлета Set-ADUser, в зависимости от того, является ли hello олицетворения учетной записи учетную запись или учетную запись службы или учетной записи пользователя.

### <a name="configure-resource-based-kcd-for-a-computer-account-on-a-managed-domain"></a>Настройка ограниченного делегирования Kerberos на основе ресурсов для учетной записи компьютера в управляемом домене
Предположим, что веб-приложения, запущенного на компьютере hello "contoso100-webapp.contoso100.com". Он должен tooaccess hello ресурсов (на веб-API "contoso100-api.contoso100.com") в контексте hello пользователей домена. Вот как можно настроить ограниченное делегирование Kerberos на основе ресурсов для этого сценария.

```
$ImpersonatingAccount = Get-ADComputer -Identity contoso100-webapp.contoso100.com
Set-ADComputer contoso100-api.contoso100.com -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

### <a name="configure-resource-based-kcd-for-a-user-account-on-a-managed-domain"></a>Настройка ограниченного делегирования Kerberos на основе ресурсов для учетной записи пользователя в управляемом домене
Предположим, у вас есть веб-приложения, выполняющиеся как учетная запись службы «appsvc» и он должен tooaccess hello ресурсов (веб-API работает под учетной записью службы - «backendsvc») в контексте hello пользователей домена. Вот как можно настроить ограниченное делегирование Kerberos на основе ресурсов для этого сценария.

```
$ImpersonatingAccount = Get-ADUser -Identity appsvc
Set-ADUser backendsvc -PrincipalsAllowedToDelegateToAccount $ImpersonatingAccount
```

## <a name="related-content"></a>Похожий контент
* [Приступая к работе с доменными службами Azure AD](active-directory-ds-getting-started.md)
* [(Обзор ограниченного делегирования Kerberos)](https://technet.microsoft.com/library/jj553400.aspx)
