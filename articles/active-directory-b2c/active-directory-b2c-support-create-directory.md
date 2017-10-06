---
title: "Устранение неполадок при создании клиентов Azure Active Directory B2C | Документация Майкрософт"
description: "В этой статье описаны проблемы и их решения при создании клиента Azure Active Directory или клиента Azure Active Directory B2C."
services: active-directory-b2c
documentationcenter: 
author: swkrish
manager: mbaldwin
editor: bryanla
ms.assetid: 7ba4c6b2-161b-45b5-b3bd-ccb662f5d7a0
ms.service: active-directory-b2c
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/06/2016
ms.author: swkrish
ms.openlocfilehash: 4bb7ec6ec67d3368a0e36c098f290f582510714a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-creating-an-azure-active-directory-or-azure-active-directory-b2c-tenant"></a>Устранение неполадок при создании клиентов Azure Active Directory или Azure Active Directory B2C 

## <a name="create-an-azure-ad-tenant"></a>Создание клиента Azure AD
Если при первой попытке hello не удается создать клиент Azure Active Directory (Azure AD), повторите попытку. Если hello проблема будет повторяться, обратитесь в службу поддержки Azure.

## <a name="create-an-azure-ad-b2c-tenant"></a>Создание клиента Azure AD B2C
При возникновении проблем при вы [Создание Azure Active Directory B2C клиента (Azure AD B2C)](active-directory-b2c-get-started.md), попробуйте hello следующие параметры:

* Если клиент Azure AD B2C hello не отображается в списке клиентов, повторите попытку toocreate hello клиента.
* Если вы видите сообщение об ошибке после hello hello Azure AD B2C клиента отображаются в списке клиентов, удалите hello клиента и создайте его заново:

    «Не удалось завершить создание клиента B2C hello «contosob2c» hello. Please visit this [link](http://go.microsoft.com/fwlink/?LinkID=624192&clcid=0x409) for more guidance." (Не удалось завершить создание клиента B2C contosob2c. Щелкните ссылку, чтобы получить дополнительные рекомендации).
* Существуют известные проблемы при удалении существующей Azure AD B2C клиента и создать его повторно с помощью hello таким же именем домена. При создании клиента Azure AD B2C необходимо использовать другое доменное имя.
* Если ни одно из приведенных решений не помогло, обратитесь в службу поддержки Azure. Дополнительные сведения см. в статье [Azure Active Directory B2C: регистрация запросов в службу поддержки](active-directory-b2c-support.md).

