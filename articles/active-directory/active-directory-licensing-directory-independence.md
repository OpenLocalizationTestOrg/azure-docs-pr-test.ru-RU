---
title: "aaaCharacteristics из Azure Active Directory клиента intercaction | Документы Microsoft"
description: "Управление клиентами Azure Active Directory как полностью независимыми ресурсами."
services: active-tenant
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 2b862b75-14df-45f2-a8ab-2a3ff1e2eb08
ms.service: active-tenant
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/27/2017
ms.author: curtand
ms.custom: H1Hack27Feb2017;it-pro
ms.reviewer: piotrci
ms.openlocfilehash: 57b677665c7cb4aee63f518c39d26754fe71a999
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-how-multiple-azure-active-directory-tenants-interact"></a>Сведения о взаимодействии нескольких клиентов Azure Active Directory

В Azure Active Directory (Azure AD), для каждого клиента является полностью независимым ресурсом: Здравствуйте, однорангового узла, которая логически независима от других клиентов, которыми вы управляете. Между клиентами нет связи типа "родительский объект — дочерний объект". Такая независимость клиентов подразумевает и независимость ресурсов, административную независимость и независимость синхронизации.

## <a name="resource-independence"></a>Независимость ресурсов
* Если создание или удаление ресурса в один клиент, он не оказывает влияния на любой ресурс другим клиентом, с единственным исключением hello внешних пользователей. 
* Если какое-либо из доменных имен используется для одного клиента, то оно не может использоваться для любого другого клиента.

## <a name="administrative-independence"></a>Административная независимость
Если пользователь без прав администратора клиента Contoso создает тестовый клиент Test, то:

* По умолчанию hello пользователь, создающий клиента добавляется как внешний пользователь в этот новый клиент и назначенный hello роли глобального администратора в этом клиенте.
* Администраторы клиента «Contoso» Hello иметь нет прямых административных полномочий tootenant 'Test', если администратор 'Test' предоставит им явным образом эти права. Тем не менее 'Contoso'-администраторы могут управлять доступом tootenant 'Test', если они управляют hello учетная запись пользователя, создавшего 'Test'.
* Если добавить или удалить роль администратора для пользователя в один клиент, не hello изменения не влияют на роли администратора hello, hello пользователем другим клиентом.

## <a name="synchronization-independence"></a>Независимость синхронизации
Можно настроить каждый Azure AD независимо друг от друга клиента tooget синхронизации данных от одного экземпляра либо:

* средства Hello Azure AD Connect toosynchronize данных с одним лесом AD.
* Здравствуйте клиента Azure Active соединитель для Forefront Identity Manager, toosynchronize данных одного или нескольких локальных лесов и/или источников данных без использования Azure AD.

## <a name="add-an-azure-ad-tenant"></a>Добавление клиента Azure AD
tooadd клиент Azure AD в hello портал Azure вход слишком[hello портал Azure](https://portal.azure.com) с учетной записью глобального администратора Azure AD, а hello слева, выберите **New**.

> [!NOTE]
> В отличие от других ресурсов Azure, клиенты не являются дочерними ресурсами подписки Azure. Если отмены или истек срок действия подписки Azure, можно получить доступ с помощью Azure PowerShell, hello Azure Graph API или Центр администрирования Office 365 hello данных клиента. Можно также связать другую подписку с клиентом hello.
>

## <a name="next-steps"></a>Дальнейшие действия
Общие сведения о лицензировании Azure AD и рекомендации по работе с этой службой см. в статье [Основы группового лицензирования в Azure Active Directory](active-directory-licensing-whatis-azure-portal.md).
