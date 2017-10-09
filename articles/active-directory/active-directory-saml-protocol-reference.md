---
title: "Справочник по протоколу AD SAML aaaAzure | Документы Microsoft"
description: "Это статье представлен обзор hello профилей единого входа и единого выхода SAML в Azure Active Directory."
services: active-directory
documentationcenter: .net
author: priyamohanram
manager: mbaldwin
editor: 
ms.assetid: 88125cfc-45c1-448b-9903-a629d8f31b01
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: priyamo
ms.openlocfilehash: d540b8cd9352e3196a0f4a40f0070d0e61127bee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# Как Azure Active Directory использует протокол SAML hello
Azure Active Directory (Azure AD) использует hello взаимодействие с пользователями tootheir tooenable приложений SAML 2.0 протокола tooprovide единым входом. Hello [Single Sign-On](active-directory-single-sign-on-protocol-reference.md) и [единого выхода](active-directory-single-sign-out-protocol-reference.md) профилей Azure AD SAML объясняется использование утверждений SAML, протоколы и привязки в службе поставщика удостоверений hello.

Протоколу SAML требуется hello поставщика удостоверений (Azure AD) и hello службы поставщика (приложение hello) tooexchange сведения о себе.

При регистрации приложения в Azure AD, разработчик приложения hello регистрирует сведения, относящиеся к федерации с Azure AD. Сюда входят hello **URI перенаправления** приложения hello.

Azure Active Directory предоставляет клиентские и общие (единые для всех клиентов) конечные точки единого входа и единого выхода. Эти URL-адреса представляют доступные расположения — они не просто идентификаторами--, поэтому можно перейти tooread hello toohello конечной точки метаданных.

* Конечная точка Hello конкретного клиента находится в каталоге `https://login.microsoftonline.com/<TenantDomainName>/FederationMetadata/2007-06/FederationMetadata.xml`.  Hello <TenantDomainName> заполнитель представляет зарегистрированное доменное имя или GUID TenantID клиента Azure AD. Например, расположенный hello метаданные федерации клиента contoso.com hello: https://login.microsoftonline.com/contoso.com/FederationMetadata/2007-06/FederationMetadata.xml

* Hello независимой от клиента конечная точка находится в каталоге `https://login.microsoftonline.com/common/FederationMetadata/2007-06/FederationMetadata.xml`. В адресе конечной точки **Общие** отображается вместо доменное имя клиента и идентификатор.

Сведения о документах метаданных федерации hello, публикуемых Azure AD см. в разделе [метаданные федерации](active-directory-federation-metadata.md).
