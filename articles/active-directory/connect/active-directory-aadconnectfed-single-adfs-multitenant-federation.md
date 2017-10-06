---
title: "aaaFederating несколько Azure AD с помощью одной службы федерации Active Directory | Документы Microsoft"
description: "В этом документе вы узнаете, как toofederate несколько Azure AD с одной AD FS."
keywords: "федерация, ADFS, AD FS, несколько клиентов, один клиент AD FS, один экземпляр ADFS, федерация нескольких клиентов, федерация ADFS с несколькими лесами, AAD Сonnect, федерация, федерация между клиентами"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: anandy; billmath
ms.openlocfilehash: 442192896b3b13f7bf9388396cd3769e194329d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
#<a name="federate-multiple-instances-of-azure-ad-with-single-instance-of-ad-fs"></a>Федерация нескольких экземпляров Azure AD с одним экземпляром AD FS

Одна высокодоступная ферма AD FS может объединять несколько лесов при наличии взаимного доверия между ними. Эти несколько лесов может или не может соответствовать toohello же Azure Active Directory. В этой статье описано, как tooconfigure федерацию между одно развертывание AD FS и несколько лесов, toodifferent синхронизации Azure AD.

![Федерация нескольких клиентов с одним экземпляром AD FS](media/active-directory-aadconnectfed-single-adfs-multitenant-federation/concept.png)
 
> [!NOTE]
> В этом сценарии не поддерживаются обратная запись устройств и автоматическое присоединение устройств.

> [!NOTE]
> Azure AD Connect не может быть федерации tooconfigure используется в этом случае Azure AD Connect можно настроить федерации для доменов в одном Azure AD.

##<a name="steps-for-federating-ad-fs-with-multiple-azure-ad"></a>Шаги для федерации AD FS и нескольких экземпляров Azure AD

Рассмотрите возможность уже включена в федерацию с hello AD FS локально установленный в среде Active Directory contoso.com локального домена contoso.com в Azure Active Directory contoso.onmicrosoft.com. Fabrikam.com является доменом в fabrikam.onmicrosoft.com Azure Active Directory.

##<a name="step-1-establish-a-two-way-trust"></a>Шаг 1. Установка взаимного доверия
 
Для AD FS в contoso.com пользователи могут tooauthenticate toobe в fabrikam.com требуется двустороннее отношение доверия между contoso.com и fabrikam.com. Выполните рекомендации hello в этом [статьи](https://technet.microsoft.com/library/cc816590.aspx) toocreate hello двустороннее отношение доверия.
 
##<a name="step-2-modify-contosocom-federation-settings"></a>Шаг 2. Изменение параметров федерации contoso.com 
 
Издатель по умолчанию Hello, заданное для одного домена федеративной tooAD FS является «http://ADFSServiceFQDN/adfs/services/trust», например, «http://fs.contoso.com/adfs/services/trust». Служба Azure Active Directory требует отдельного издателя для каждого федеративного домена. Поскольку hello же AD FS будут toofederate два домена, значение издателя hello должен toobe изменены таким образом, чтобы он уникален для каждого домена AD FS создает федерацию с Azure Active Directory. 
 
На сервере AD FS hello откройте Azure AD PowerShell и выполните следующие шаги hello.
 
Подключение Azure Active Directory, содержащий hello домена contoso.com Connect-MsolService обновления hello параметры федерации для contoso.com Update-MsolFederatedDomain - DomainName contoso.com toohello – SupportMultipleDomain
 
Будет изменено издателя в параметра федерации доменов hello слишком «http://contoso.com/adfs/services/trust» и выдачи утверждений, правило будет добавлено для hello Azure AD доверия с проверяющей стороной tooissue hello правильное значение issuerId на основании hello суффикс UPN.
 
##<a name="step-3-federate-fabrikamcom-with-ad-fs"></a>Шаг 3. Федерация fabrikam.com с AD FS
 
В Azure AD powershell сеанс выполнять следующие шаги hello: подключение tooAzure Active Directory, содержащую hello домена fabrikam.com

    Connect-MsolService
Преобразуйте toofederated домена fabrikam.com управляемых hello:

    Convert-MsolDomainToFederated -DomainName anandmsft.com -Verbose -SupportMultipleDomain
 
Hello выше операции будет федерацию hello домена fabrikam.com с hello же AD FS. Параметры домена hello можно проверить с помощью Get-MsolDomainFederationSettings для обоих доменов.

## <a name="next-steps"></a>Дальнейшие действия
[Подключение Active Directory к Azure Active Directory](active-directory-aadconnect.md)
