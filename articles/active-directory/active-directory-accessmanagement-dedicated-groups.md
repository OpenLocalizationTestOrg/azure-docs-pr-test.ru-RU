---
title: "aaaDedicated группы в Azure Active Directory | Документы Microsoft"
description: "Обзор работы выделенных групп в Azure Active Directory и способов их создания."
services: active-directory
documentationcenter: 
author: curtand
manager: femila
editor: 
ms.assetid: 86158909-083a-41fe-8090-955e96ad1865
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/08/2017
ms.author: curtand
ms.openlocfilehash: 8feec6e1a4e6b384470392d3043caeeec2b03dd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="dedicated-groups-in-azure-active-directory"></a>Выделенные группы в Azure Active Directory
В Azure Active Directory (Azure AD) функция выделенные группы hello автоматически создает и заполняет членство группы Azure AD предопределенные. Не удается добавить элементы выделенных групп или удален с помощью hello Azure классического портала, командлеты Windows PowerShell или программно.

> [!NOTE]
> Выделенные группы требуют назначения лицензии Azure AD Premium:
>
> * Здравствуйте, администратор, ответственный за управление hello правила в группе
> * все пользователи, которые выбираются hello правило toobe является членом группы hello
>
>

**tooenable выделенной группы**

1. В hello [классический портал Azure](https://manage.windowsazure.com)выберите **Active Directory**, а затем откройте каталог вашей организации.
2. Выберите hello **группы** вкладку и откройте hello группу tooedit.
3. Выберите hello **Настройка** и затем задайте **Включить выделенные группы** слишком**Да**.

После переключения включить целевые группы hello слишком**Да**, можно дополнительно включить hello directory tooautomatically создать hello всех пользователей, отдельная группа, задание hello **«Все пользователи» включить группы** Переключение слишком**Да**. Вы также можно отредактировать имя этой целевой группы hello, введя его в hello **отображаемое имя для «Все пользователи» группа** поля.

можно использовать группы все пользователи Hello tooassign hello и те же разрешения tooall hello пользователи в вашем каталоге. Например можно предоставить всем пользователям в ваш каталог доступа tooa приложения SaaS, назначив доступ для всех пользователей отдельная группа toothis приложения hello.

Hello выделенной группы все пользователи входят все пользователи в каталоге hello, включая гостей и внешних пользователей. Если требуется группа, исключает внешних пользователей, то это можно сделать, создав группу с основанное на атрибутах динамическое правило hello ниже:

                (user.userPrincipalName -notContains "#EXT#@")

Группы, который исключает всем гостевым системам используйте правило, например hello следующее:

                (user.userType -ne "Guest")

toolearn о том, как toocreate *Дополнительно* правил (правил, которые может содержать несколько сравнения) динамическое членство в группе, в разделе [с помощью атрибутов toocreate расширенные правила](active-directory-accessmanagement-groups-with-advanced-rules.md).

### <a name="next-steps"></a>Дальнейшие действия
В следующих статьях содержатся дополнительные сведения об Azure Active Directory.

* [Управление tooresources доступ с помощью групп Azure Active Directory](active-directory-manage-groups.md)
* [Указатель статьей по управлению приложениями в Azure Active Directory](active-directory-apps-index.md)
* [Что такое Microsoft Azure Active Directory](active-directory-whatis.md)
* [Интеграция локальных удостоверений с Azure Active Directory](active-directory-aadconnect.md)
