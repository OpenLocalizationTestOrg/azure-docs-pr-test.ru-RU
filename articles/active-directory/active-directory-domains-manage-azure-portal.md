---
title: "aaaManaging пользовательские имена доменов в Azure Active Directory | Документы Microsoft"
description: "Основные принципы и указания по управлению доменным именем в Azure Active Directory."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 5063cd0a-dba2-4ba9-aa65-b8117490d73a
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: curtand;jeffsta
ms.openlocfilehash: 4719524c4e972f6c981db39f016729da13b37670
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="managing-custom-domain-names-in-your-azure-active-directory"></a>Управление личными доменными именами в Azure Active Directory
Имя домена является важной частью идентификатора hello много ресурсов directory: он является частью адреса электронной почты пользователя для пользователя, часть адреса hello для группы и может быть частью hello URI идентификатора приложения для приложения. Ресурс в Azure Active Directory (Azure AD) может включать имя домена, которое уже проверена, как принадлежащие hello каталог, содержащий ресурс hello. Задачи управления доменами в Azure AD может выполнять только глобальный администратор.

## <a name="set-hello-primary-domain-name-for-your-azure-ad-directory"></a>Задайте имя основного домена hello для вашего каталога Azure AD
При создании каталога hello исходное имя домена, например «contoso.onmicrosoft.com», также является именем основного домена hello. Основной домен Hello — hello по умолчанию доменное имя для нового пользователя, при создании нового пользователя. Задание имени основного домена упрощает процесс hello для администратора toocreate новых пользователей на портале hello. Имя основного домена hello toochange:

1. Войдите в toohello [портал Azure](https://portal.azure.com) с помощью учетной записи глобального администратора каталога hello.
2. Выберите **дополнительные службы**, введите **Azure Active Directory** в hello текстовое поле, а затем выберите **ввод**.
   
   ![Открытие страницы "Управление пользователями"](./media/active-directory-domains-add-azure-portal/user-management.png)
3. На hello ***имя каталога*** колонке выберите **доменных имен**.
4. На hello  ***имя каталога* -имена домена** колонки, выберите hello доменное имя, хотелось бы toomake hello основное имя домена.
5. На hello ***доменное имя*** колонке (то есть hello стоечный модуль, открывается, имеющий имя нового домена в заголовок hello), выберите hello **сделать основным** команды. При появлении запроса подтвердите свой выбор.
   
   ![Назначение доменного имени основным](./media/active-directory-domains-manage-azure-portal/make-primary.png)

Можно изменить hello основное имя домена для вашего каталога toobe проверенный пользовательский домен, который не является федеративным. Изменение основного домена hello для вашего каталога не изменит приветствия имен пользователей для всех существующих пользователей.

## <a name="add-custom-domain-names-tooyour-azure-ad"></a>Добавить tooyour имена пользовательских доменов Azure AD
Можно добавить пользовательский домен имена too900 tooeach-каталог Azure AD. Здравствуйте процесса слишком[добавить дополнительные пользовательские доменные имена](add-custom-domain.md) hello одинаково для hello первое имя пользовательского домена.

## <a name="add-subdomains-of-a-custom-domain"></a>Добавление поддоменов для личного домена
Tooadd имя домена третьего уровня, например «europe.contoso.com» tooyour каталога следует сначала следует добавить и проверить hello домена второго уровня, например contoso.com. Hello поддомен проверяются автоматически с помощью Azure AD. проверил toosee, hello поддомен, который вы только что добавили hello страницу в браузере hello, список доменов hello.

## <a name="what-toodo-if-you-change-hello-dns-registrar-for-your-custom-domain-name"></a>Какие toodo при изменении hello регистратора DNS для пользовательского имени домена
Если изменить hello регистратора DNS для пользовательского имени домена, вы можете продолжить toouse пользовательское имя домена с Azure AD без прерывания работы и дополнительные задачи по настройке. При использовании настраиваемого имени домена с Office 365, Intune и других служб, использующих пользовательские имена доменов в Azure AD см. документацию toohello для этих служб.

## <a name="delete-a-custom-domain-name"></a>Удаление имени личного домена
Пользовательское доменное имя можно удалить из Azure AD, если ваша организация больше не использует это имя домена, или в том случае, если требуется toouse этого доменного имени в другой Azure AD.

toodelete пользовательского имени домена, сначала убедитесь, что нет ресурсов в вашем каталоге зависят от hello доменное имя. Доменное имя невозможно удалить из каталога в следующих случаях:

* Любой пользователь получает имя пользователя, адрес электронной почты или адрес прокси-сервера, который включает имя домена hello.
* Любая группа имеет адрес электронной почты или адрес прокси-сервера, который включает имя домена hello.
* Любое приложение в Azure AD имеет идентификатор URI, который включает hello имя домена приложения.

Необходимо изменить или удалить любой такой ресурс в каталоге Azure AD, перед удалением hello пользовательское имя домена.

## <a name="use-powershell-or-graph-api-toomanage-domain-names"></a>Используйте PowerShell или Graph API toomanage доменных имен
Большинство задач по управлению доменными именами в Azure Active Directory также можно выполнить с помощью Microsoft PowerShell или программными средствами с помощью API Graph Azure AD.

* [С помощью PowerShell toomanage доменных имен в Azure AD](https://msdn.microsoft.com/library/azure/e1ef403f-3347-4409-8f46-d72dafa116e0#BKMK_ManageDomains)
* [С помощью Graph API toomanage доменных имен в Azure AD](https://msdn.microsoft.com/Library/Azure/Ad/Graph/api/domains-operations)

## <a name="next-steps"></a>Дальнейшие действия
* [Добавление имен личных доменов](add-custom-domain.md)

