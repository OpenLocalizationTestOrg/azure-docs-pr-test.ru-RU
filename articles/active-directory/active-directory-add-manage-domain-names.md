---
title: "aaaManaging пользовательские имена доменов в Azure Active Directory | Документы Microsoft"
description: "Основные принципы и указания по управлению личными доменами в Azure Active Directory"
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: cf3523bd-9ee0-439e-963d-ccea038867b9
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: curtand
ms.custom: oldportal;it-pro;
robots: NOINDEX
ms.openlocfilehash: 4b6d06fecf3be0621be51c38a1330eafdc1b4d35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Управление личными доменными именами в Azure Active Directory
Доменное имя может выступать важным идентификатором для многих ресурсов каталога как часть:

* имени или адреса электронной почты пользователя;
* адрес Hello для группы
* приложение Hello URI идентификатора приложения

Ресурс в Azure Active Directory (Azure AD) может включать имя домена, которое уже проверена, что владельцем toobe hello каталог, содержащий ресурс hello. Задачи управления доменами в Azure AD может выполнять только глобальный администратор.

> [!IMPORTANT]
> Корпорация Майкрософт рекомендует управлять Azure AD, используя hello [Центр администрирования Azure AD](https://aad.portal.azure.com) в hello портал Azure, вместо использования hello классический портал Azure, в этой статье. Как toomanage домена имена в центре администрирования hello Azure AD, в разделе [управление пользовательские имена доменов в Azure Active Directory](active-directory-domains-manage-azure-portal.md).

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Задайте имя основного домена hello для вашего каталога Azure AD
При создании каталога hello исходное имя домена, например «contoso.onmicrosoft.com», также является именем основного домена hello для вашего каталога. Основной домен Hello — hello по умолчанию доменное имя для нового пользователя, при создании нового пользователя в hello [классический портал Azure](https://manage.windowsazure.com/), или других порталов, такие как портал администрирования Office 365 hello. Это упрощает процесс hello для администратора toocreate новых пользователей на портале hello.

Имя основного домена hello toochange для каталога:

1. Войдите в toohello [классический портал Azure](https://manage.windowsazure.com/) с учетной записью пользователя, который является глобальным администратором каталога Azure AD.
2. Выберите **Active Directory** на левой навигационной панели hello.
3. Откройте свой каталог.
4. Выберите hello **домены** вкладки.
5. Выберите hello **изменение основной** кнопки на панели команд hello.
6. Выберите домен hello, что требуется toobe hello новый основной домен для вашего каталога.

Можно изменить hello основное имя домена для вашего каталога toobe проверенный пользовательский домен, который не является федеративным. Изменение основного домена hello для вашего каталога не изменит приветствия имен пользователей для всех существующих пользователей.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Добавить tooyour имена пользовательских доменов Azure AD
Можно добавить пользовательский домен имена too900 tooeach-каталог Azure AD. Здравствуйте процесса слишком[добавить дополнительные пользовательские доменные имена](active-directory-add-domain.md) hello одинаково для hello первое имя пользовательского домена.

## <a name="add-subdomains-of-a-custom-domain"></a>Добавление поддоменов для личного домена
Tooadd имя домена третьего уровня, например «europe.contoso.com» tooyour каталога следует сначала следует добавить и проверить hello домена второго уровня, например contoso.com. Hello поддомен проверяются автоматически с помощью Azure AD. проверил toosee, hello поддомен, который вы только что добавили hello страницу в браузере hello, список доменов hello в вашем каталоге.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Какие toodo при изменении hello регистратора DNS для пользовательского имени домена
Если изменить hello регистратора DNS для пользовательского имени домена, вы можете продолжить toouse пользовательское имя домена с Azure AD без прерывания работы и дополнительные задачи по настройке. При использовании настраиваемого имени домена с Office 365, Intune и других служб, использующих пользовательские имена доменов в Azure AD см. документацию toohello для этих служб.

## <a name="delete-a-custom-domain-name"></a>Удаление имени личного домена
Пользовательское доменное имя можно удалить из Azure AD, если ваша организация больше не использует это имя домена, или в том случае, если требуется toouse этого доменного имени в другой Azure AD.

toodelete пользовательского имени домена, сначала убедитесь, что нет ресурсов в вашем каталоге зависят от hello доменное имя. Доменное имя невозможно удалить из каталога в следующих случаях:

* Любой пользователь получает имя пользователя, адрес электронной почты или адрес прокси-сервера, включают hello доменное имя.
* Любая группа имеет адрес электронной почты или адрес прокси-сервера, который включает имя домена hello.
* Любое приложение в Azure AD имеет идентификатор URI, который включает hello имя домена приложения.

Необходимо изменить или удалить любой такой ресурс в каталоге Azure AD, перед удалением hello пользовательское имя домена.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Используйте PowerShell или Graph API toomanage доменных имен
Большинство задач по управлению доменными именами в Azure Active Directory также можно выполнить с помощью Microsoft PowerShell или программными средствами с помощью API Graph Azure AD.

* [С помощью PowerShell toomanage доменных имен в Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [С помощью Graph API toomanage доменных имен в Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Дальнейшие действия
* [Дополнительные сведения об именах доменов в Azure AD](active-directory-add-domain-concepts.md)
* [Управление именами пользовательских доменов](active-directory-add-manage-domain-names.md)

