---
title: "риск безопасности отчетов на портале Azure Active Directory hello с отметкой aaaUsers | Документы Microsoft"
description: "Дополнительные сведения о пользователях hello, помеченных для риск безопасности отчетов на портале Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 5077cd61d6119745a85ed712623904633a151331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="users-flagged-for-risk-security-report-in-hello-azure-active-directory-portal"></a>Пользователи с отметкой риск безопасности отчетов на портале Azure Active Directory hello

Hello безопасности отчетов в hello Azure Active Directory (Azure AD) позволяет получить подробные сведения о вероятности hello скомпрометированных учетных записей пользователей в вашей среде. 

Azure Active Directory обнаруживает подозрительные действия, которые являются связанные tooyour учетных записей пользователей. Для каждого обнаруженного действия создается запись, которая называется *событием риска*. Дополнительные сведения см. в статье [События риска Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hello обнаружил, что риск события, используемые toocalculate:

- **Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя. Дополнительные сведения см. в разделе [Вход, представляющий риск](active-directory-identityprotection.md#risky-sign-ins). 

- **Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена. Дополнительные сведения см. в разделе [Пользователи, помеченные для события риска](active-directory-identityprotection.md#users-flagged-for-risk).  

В hello портал Azure, можно найти hello безопасности сообщает о hello **Azure Active Directory** колонки в hello **безопасности** раздела.  

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/10.png)



## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Какая лицензия Azure AD необходимо tooaccess безопасности отчета?  

Все выпуски Azure Active Directory предоставляют отчеты о пользователях, находящихся в группе риска.  
Однако hello уровень детализации отчета может различаться между выпусками hello: 

- В hello **выпуски Azure Active Directory Free и Basic**, вы уже получить список пользователей, помеченных для риска. 

- Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета. 

- Hello **Azure Active Directory Premium 2** выпуск предлагает вам hello наиболее подробные сведения обо всех событиях риска, базовый и позволяет tooconfigure политик безопасности, которые автоматически реагировать tooconfigured риска уровни.



## <a name="azure-active-directory-free-and-basic-edition"></a>Выпуски "Бесплатный" и "Базовый" Azure Active Directory

Hello пользователей, помеченных для риска отчета в свободной и основные выпуски hello Azure Active Directory предоставляет список учетных записей пользователей, которые могли быть скомпрометированы. 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/03.png)

При выборе пользователя открывает колонку данные соответствующих пользователей hello.
Для пользователей, которые находятся под угрозой можно просмотреть журнал вход пользователя hello и сбросить пароль hello, при необходимости.

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/46.png)


Это диалоговое окно предоставляет следующие возможности:

- Загрузить отчет hello

- Поиск пользователей

![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/16.png)


## <a name="azure-active-directory-premium-editions"></a>Выпуски Azure Active Directory Premium

Hello пользователей, помеченных для отчета риска в выпуски premium hello Azure Active Directory обеспечивает:

- [Список учетных записей пользователей](active-directory-identityprotection.md#users-flagged-for-risk), которые, возможно, были скомпрометированы. 

- Статистической информации о hello [типы событий риска](active-directory-identity-protection-risk-events.md) , обнаружены

- Параметр toodownload hello отчета

- Параметр tooconfigure [политика исправления риск пользователя](active-directory-identityprotection.md#user-risk-security-policy)  


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/71.png)

При выборе пользователя отображается подробное представление отчета об этом пользователе, предоставляющее перечисленные ниже возможности.

- Просмотреть все входы откройте hello

- Сброс пароля пользователя hello

- Отклонение всех событий.

- Проанализируйте обнаруженную риск события для пользователя hello. 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/324.png)


tooinvestigate события риска, выберите один из hello tooopen список hello **сведения** колонку для этого события риска. На hello **сведения** колонки, у вас есть параметр tooeither hello [вручную закрыть события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторно активировать событие вручную закрытого риска. 


![События входа, представляющие риск](./media/active-directory-reporting-security-user-at-risk/325.png)



## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о защите идентификации Azure см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).

