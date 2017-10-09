---
title: "aaaAssign пользователи tooa пользовательского домена в Azure Active Directory | Документы Microsoft"
description: "Как toopopulate пользовательского домена в Azure Active Directory с учетными записями пользователей."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 717b5a7c-7bc3-4ab1-98b5-4740b53338fe
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 23c338a361a90fddf42d4df90db94c9774305886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="assign-users-tooa-custom-domain"></a>Назначить пользователей tooa пользовательского домена
После добавления tooAzure ваш пользовательский домен Active Directory, необходимо добавить hello учетные записи пользователей для этого домена, чтобы можно было начать они проходят проверку подлинности.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Как toomanage домена имена в центре администрирования hello Azure AD, в разделе [управление пользовательские имена доменов в Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="users-synced-from-a-on-premises-directory"></a>Пользователи, синхронизированные из локального каталога
Если вы уже настроили подключение между вашей локальной Active Directory и Azure Active Directory, синхронизации можно заполнить hello учетных записей. Дополнительные сведения о том, как toosynchronize Azure Active Directory с локальными службами Active Directory, см. [интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md).

## <a name="users-added-and-managed-in-hello-cloud"></a>Пользователи добавляются и управляются в облаке hello
домен hello toochange для существующей учетной записи пользователя:

1. Откройте hello классический портал Azure, используя учетную запись глобального администратора или администратора пользователей.
2. Откройте свой каталог.
3. Выберите hello **пользователей** вкладки.
4. Выберите hello пользователя из списка hello.
5. Изменить домен hello hello пользователя, а затем выберите **Сохранить**.

Это также может быть сделано с помощью [Microsoft PowerShell](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains) или hello [Graph API](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations).

## <a name="select-a-custom-domain-when-creating-a-new-user"></a>Выбор пользовательского домена при создании пользователя
1. Откройте hello классический портал Azure, используя учетную запись глобального администратора или администратора пользователей.
2. Откройте свой каталог.
3. Выберите hello **пользователей** вкладки.
4. В панели команд hello, выберите **добавить**.
5. При добавлении имени пользователя hello выберите hello пользовательского домена из списка доменов hello.
6. Щелкните **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
* [С помощью пользовательских доменных имен toosimplify hello входа в систему для пользователей](active-directory-add-domain.md)
* [Управление именами пользовательских доменов](active-directory-add-manage-domain-names.md)
* [Общие сведения об управлении доменами в Azure AD](active-directory-add-domain-concepts.md)

