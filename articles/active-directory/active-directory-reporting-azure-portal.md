---
title: "aaaAzure Active Directory отчетов | Документы Microsoft"
description: "Общий обзор отчетов Azure Active Directory."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 6141a333-38db-478a-927e-526f1e7614f4
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/13/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c91813acbdc4b0bfcd164169b0b575accac227d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting"></a>Отчеты Azure Active Directory

С отчетами Azure Active Directory можно получить важные сведения о том, как работает ваша среда.  
Hello предоставленных данных позволяет делать следующее:

- определять, как приложения и службы используются пользователями;
- Определить потенциальные угрозы влияющих на работоспособность hello среды
- устранить неполадки, влияющие на работу пользователей.  

Архитектура подготовки отчетов Hello основывается на двух основных основы:

- Отчеты о безопасности
- Отчеты об активности

![Отчеты](./media/active-directory-reporting-azure-portal/01.png)



## <a name="security-reports"></a>Отчеты о безопасности

отчеты о безопасности Hello в Azure Active Directory помогают вам tooprotect удостоверения организации.  
В Azure Active Directory существует два типа отчетов безопасности:

- **Пользователи с отметкой риск** — hello [пользователей с отметкой риск безопасности отчета](active-directory-reporting-security-user-at-risk.md), получить обзор учетных записей пользователей, которые могут быть скомпрометированы.

- **Рискованные входы** — используя hello [рискованным безопасности отчетов](active-directory-reporting-security-risky-sign-ins.md), отображается индикатор попыток входа, которые может быть выполнено с тем, кто является не hello законный владелец учетной записи пользователя. 

**Какая лицензия Azure AD необходимо tooaccess безопасности отчета?**  
Все выпуски Azure Active Directory предоставляют оба типа отчетов безопасности.  
Однако hello уровень детализации отчета может различаться между выпусками hello: 

- В hello **выпуски Azure Active Directory Free и Basic**, вы уже получить список пользователей, помеченных для риска и рискованно входа в систему. 

- Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета. 

- Hello **Azure Active Directory Premium 2** edition предоставляет вам hello наиболее подробные сведения о hello базового события рисков и позволяет также tooconfigure политики безопасности, которые автоматически отвечать tooconfigured уровней риска.


## <a name="activity-reports"></a>Отчеты об активности

В Azure Active Directory существует два типа отчетов об активности:

- **Журналы аудита** - hello [журналы аудита, отчет о действиях](active-directory-reporting-activity-audit-logs.md) предоставляет доступ к истории toohello из каждой задачей, выполняемой в клиенте.

- **Входа в систему** — используя hello [входа в систему отчета об активности](active-directory-reporting-activity-sign-ins.md), можно определить, кто выполнил задачи hello, сообщаемые отчета журналов аудита hello.



Hello **отчет о журналах аудита** предоставляет записей действий системы для соответствия.
Помимо прочего hello при условии, что данных можно tooaddress распространенные сценарии такие как:

- Кто-то в клиент получил доступ tooan административной группы. Кто предоставил этот доступ? 

- Требуется список hello tooknow пользователи, входящие в определенное приложение с момента я недавно выставленных hello приложения и требуется tooknow, если он также выполняет

- Я хочу tooknow сколько пароль сбрасывает отключены в моей клиента


**Какая лицензия Azure AD необходимо отчета журналов аудита hello tooaccess?**  
отчет журналы аудита Hello доступен для компонентов, для которых имеются лицензии. При наличии лицензии для определенного компонента также имеется доступ toohello данные журнала для него аудита.

Дополнительные сведения см. в разделе **сравнение общедоступной возможности выпусков Free, Basic и Premium hello** в [средства Azure Active Directory и возможности](https://www.microsoft.com/cloud-platform/azure-active-directory-features).   



Hello **входа в систему отчета об активности** tootoofind включает отвечает tooquestions, такие как:

- Что такое hello вход шаблон пользователя?
- Сколько пользователей входили в течение недели?
- Что такое состояние hello эти входа в систему?


**Какая лицензия Azure AD вы должны tooaccess hello отчета об активности входа в систему?**  
tooaccess Здравствуйте отчета об активности входа в систему, клиент должен иметь лицензию Azure AD Premium, связанные с ним.


## <a name="programmatic-access"></a>Программный доступ

В пользовательском интерфейсе добавления toohello отчетов Azure Active Directory также предоставляет [программный доступ](active-directory-reporting-api-getting-started-azure-portal.md) toohello данных отчетов. Hello данные этих отчетов могут быть очень полезным tooyour приложения, такие как системы SIEM, аудита и средства бизнес-аналитики. Hello Azure AD сообщивший об API обеспечивают программный доступ к данным toohello через набор API на основе REST. Эти интерфейсы API можно вызвать, используя различные языки и инструменты программирования. 


## <a name="next-steps"></a>Дальнейшие действия

Если Дополнительные сведения о hello tooknow различных типов отчетов в Azure Active Directory, см.:

- [отчетом о пользователях, находящихся в группе риска](active-directory-reporting-security-user-at-risk.md);
- [отчетом о входах, представляющих риск](active-directory-reporting-security-risky-sign-ins.md);
- [отчетом о журналах аудита](active-directory-reporting-activity-audit-logs.md);
- [отчетом о журналах входа](active-directory-reporting-activity-sign-ins.md).

Если tooknow больше о доступе к hello hello hello reporting API с помощью данных отчетов, см.: 

- [Приступая к работе с API отчетов Azure Active Directory "hello"](active-directory-reporting-api-getting-started-azure-portal.md)


<!--Image references-->
[1]: ./media/active-directory-reporting-azure-portal/ic195031.png