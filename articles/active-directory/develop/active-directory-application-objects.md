---
title: "aaaAzure приложение Active Directory и субъектов-служб | Документы Microsoft"
description: "Обсуждение hello отношение между приложением и основной объектов службы в Azure Active Directory"
documentationcenter: dev-center-name
author: dstrockis
manager: mbaldwin
services: active-directory
editor: 
ms.assetid: adfc0569-dc91-48fe-92c3-b5b4833703de
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 04/28/2016
ms.author: dastrock
ms.custom: aaddev
ms.openlocfilehash: ff7e308c0b326c3a32b101b7b323f2c0362763e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-principal-objects-in-azure-active-directory-azure-ad"></a>Объекты приложения и субъекта-службы в Azure Active Directory (Azure AD)
Иногда hello смысл hello термин «приложение» может быть не учитываются при использовании в контексте hello Azure AD. Hello цель этой статьи — toomake яснее, указывая, общие и конкретные аспекты интеграция приложения Azure AD, с иллюстрация регистрации и разрешения для его [многопользовательского приложения](active-directory-dev-glossary.md#multi-tenant-application).

## <a name="overview"></a>Обзор
Приложение, интегрированное с Azure AD имеет последствия, которые выходят за рамки аспект hello программного обеспечения. «Приложение» часто используется в качестве концептуальной термин, ссылающиеся toonot только hello hello прикладном программном обеспечении, но также регистрации Azure AD и роли в «диалогов» во время выполнения проверки подлинности и авторизации. По определению, приложение может работать в [клиента](active-directory-dev-glossary.md#client-application) роли (использование ресурса), [сервер ресурсов](active-directory-dev-glossary.md#resource-server) или даже обе эти роли (предоставление доступа к API-интерфейсы tooclients). Протокол диалога Hello определяется [поток предоставления авторизации OAuth 2.0](active-directory-dev-glossary.md#authorization-grant), позволяя tooaccess hello клиента или ресурса или защиты ресурсов данных соответственно. Теперь давайте рассмотрим более глубокого уровня и посмотрите, как модель приложения hello Azure AD представляет приложения во время разработки и во время выполнения. 

## <a name="application-registration"></a>Регистрация приложения
При регистрации приложения Azure AD в hello [портал Azure][AZURE-Portal], создаются два объекта в клиенте Azure AD: объект приложения и главного объекта службы.

#### <a name="application-object"></a>Объект приложения
Приложения Azure AD определяется его один и только объект приложения, который находится в клиенте hello Azure AD, где зарегистрирован приложения hello, известные как «home» клиента приложения hello. Hello Azure AD Graph [сущность приложения] [ AAD-Graph-App-Entity] определяет hello схему для свойства объект приложения. 

#### <a name="service-principal-object"></a>Объект субъекта-службы
Владелец учетной записи службы Hello определяет политику hello и разрешения для использования приложением в конкретных клиентов, предоставляя hello основу для приложения hello toorepresent участника безопасности во время выполнения. Hello Azure AD Graph [сущность ServicePrincipal] [ AAD-Graph-Sp-Entity] определяет hello схемы для свойств основного объекта службы. 

#### <a name="application-and-service-principal-relationship"></a>Отношение приложения и субъекта-службы
Рассмотрим объект приложения hello как hello *глобальной* представления приложения для использования во всех клиентов и hello участника-службы в качестве hello *локального* представление для использования в определенном клиент. Hello объекта приложения выступает в качестве hello шаблона от какие общих и свойства по умолчанию — *производный* для использования при создании соответствующих объектов участника службы. Объект приложения, поэтому имеет отношение 1:1 с программного приложения hello и 1 этапе: возможности связи с его соответствующие объекты участника службы.

Субъект-службы должны создаваться в каждый клиент там, где будут использоваться приложения hello, позволяя тем самым tooestablish удостоверения для входа в систему и/или защищаемой клиентом hello tooresources доступа. Приложение с одним клиентом будет иметь только один субъект-службу (в домашнем клиенте), который обычно создается (и на который дается согласие на использование) во время регистрации приложения. Мультитенантное веб-приложения и API также будет иметь участника-службы, созданные в каждый клиент согласился где пользователя из этого клиента используйте tooits.  

> [!NOTE]
> Любые внесенные tooyour объект приложения, также отражаются в его главного объекта службы приложения hello домашней клиента только (hello клиента, где она была зарегистрирована). Многопользовательских приложений объект приложения toohello изменения не отражаются в объекты principal любой потребитель клиентов службы, пока не будет удалена hello доступ через hello [панели доступа приложений](https://myapps.microsoft.com) и предоставить снова.
><br>  
> Обратите также внимание, что собственные приложения по умолчанию регистрируются как мультитенантные.
> 
> 

## <a name="example"></a>Пример
Hello следующей схеме показана связь hello объекта приложения и объекты principal в контексте hello образец многопользовательского приложения с именем соответствующей службы приложения **приложение по управлению Персоналом**. В этом сценарии используются три клиента Azure AD. 

* **Adatum** - hello клиента, используемые hello компании, разработанным hello **приложение по управлению Персоналом**
* **Contoso** - hello клиента, используемых в организации Contoso, который является потребителем hello hello **приложение по управлению Персоналом**
* **Fabrikam** - hello клиента, используемые hello организации Fabrikam, которая также использует hello **приложение по управлению Персоналом**

![Связь между объектом приложения и объектом субъекта-службы](./media/active-directory-application-objects/application-objects-relationship.png)

В предыдущей диаграмме hello шаг 1 — Создание приложения hello и объекты principal службы в клиенте домашней приложения hello процесс hello.

На шаге 2 завершении согласия, Contoso и Fabrikam Администраторы главного объекта службы создается в клиент Azure AD компании и разрешения, назначенные hello предоставлен администратором hello. Также Обратите внимание, что приложение hello HR может быть настроен разработан tooallow согласия пользователями для индивидуального использования.

На шаге 3 из hello HR приложения (Contoso и Fabrikam) каждого клиентов потребителя hello имеют свои собственные главного объекта службы. Каждое представляет их в использовании экземпляр приложения hello во время выполнения, регулируются согласие разрешения приветствия соответствующих администратором hello.

## <a name="next-steps"></a>Дальнейшие действия
Объект приложения приложения может запускаться через hello API Azure AD Graph hello [портал Azure] [ AZURE-Portal] редакторе манифеста приложения, или [командлеты Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), представленный его OData [сущность приложения][AAD-Graph-App-Entity].

Основной объект приложения службы может запускаться через API Azure AD Graph hello или [командлеты Azure AD PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azureadps-2.0), представленный его OData [сущность ServicePrincipal] [ AAD-Graph-Sp-Entity].

Hello [Azure AD Graph Explorer](https://graphexplorer.azurewebsites.net/) полезен для выполнения запросов приложения hello и объекты principal службы.

<!--Image references-->

<!--Reference style links -->
[AAD-Graph-App-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#application-entity
[AAD-Graph-Sp-Entity]: https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/entity-and-complex-type-reference#serviceprincipal-entity
[AZURE-Portal]: https://portal.azure.com
