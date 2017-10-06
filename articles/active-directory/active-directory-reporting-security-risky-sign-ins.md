---
title: "отчет aaaRisky входа в систему на портале Azure Active Directory hello | Документы Microsoft"
description: "Дополнительные сведения об отчете hello рискованным входа в систему на портале Azure Active Directory hello"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: 7728fcd7-3dd5-4b99-a0e4-949c69788c0f
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/24/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d8df5cafea6b38f3e364c24a6aff599abe088e88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="risky-sign-ins-report-in-hello-azure-active-directory-portal"></a>Рискованные входы отчетов на портале Azure Active Directory hello

Hello безопасности отчетов в Azure Active Directory (Azure AD) позволяет получить представление о вероятности hello скомпрометированных учетных записей в вашей среде. 

Azure AD обнаруживает подозрительные действия, которые являются связанные tooyour учетных записей пользователей. Для каждого обнаруженного действия создается запись, которая называется *событием риска*. Дополнительные сведения см. в статье о [событиях риска в Azure Active Directory](active-directory-identity-protection-risk-events.md). 

Hello обнаружил, что риск события, используемые toocalculate:

- **Рискованные входы** -рискованным вход является показателем для попытки входа, возможно, выполнены с тем, кто не hello законный владельцем учетной записи пользователя. Дополнительные сведения см. в [этом разделе](active-directory-identityprotection.md#risky-sign-ins). 

- **Пользователи, находящиеся в группе риска**. Такая пометка означает, что конфиденциальность учетной записи пользователя, возможно, нарушена. Дополнительные сведения см. в разделе о [пользователях, находящихся в группе риска](active-directory-identityprotection.md#users-flagged-for-risk).  

В [hello портал Azure](https://portal.azure.com), можно найти hello безопасности сообщает о hello **Azure Active Directory** колонки в hello **безопасности** раздела. 

![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/10.png)


## <a name="what-azure-ad-license-do-you-need-tooaccess-a-security-report"></a>Какая лицензия Azure AD необходимо tooaccess безопасности отчета?  

Все выпуски Azure Active Directory предоставляют отчеты о событиях входа, представляющих риск.  
Однако hello уровень детализации отчета может различаться между выпусками hello: 

- В hello **выпуски Azure Active Directory Free и Basic**, появляется список рискованным входа в систему. 

- Hello **Azure Active Directory Premium 1** edition расширяет возможности этой модели, также позволяя tooexamine некоторых hello базового события рисков, которые были обнаружены для каждого отчета. 

- Hello **Azure Active Directory Premium 2** обеспечивает с hello наиболее подробные сведения обо всех событиях риска, базовый и позволяет также tooconfigure политики безопасности, которые автоматически отвечать tooconfigured уровней риска.



## <a name="azure-active-directory-free-and-basic-edition"></a>Выпуски "Бесплатный" и "Базовый" Azure Active Directory

Hello Azure Active Directory free и basic Edition позволяют список рискованным входа в систему, обнаруженных для пользователей. В этом отчете указаны:

- **Пользователь** - hello имя пользователя hello, который использовался во время операции входа hello
- **IP** -hello IP-адрес устройства hello, используемые tooconnect tooAzure Active Directory
- **Расположение** -использовать расположение hello tooconnect tooAzure Active Directory
- **Время входа сохраняются** -hello время вход hello копии
- **Состояние** -hello состояние hello входа в систему


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/01.png)

На основании изучение hello рискованным вход, можно предоставить отзыв tooAzure Active Directory в форме hello, следующие действия:

- Разрешить
- Пометить как ложное срабатывание
- Игнорировать
- Повторно активировать

![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/21.png)

Дополнительные сведения см. в разделе [Закрытие событий риска вручную](active-directory-identityprotection.md#closing-risk-events-manually).

Этот отчет предоставляет следующие возможности:

- поиск ресурсов;
- Загрузить данные отчета hello


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/93.png)


## <a name="azure-active-directory-premium-editions"></a>Выпуски Azure Active Directory Premium

отчет рискованным входы Hello в выпуски premium hello Azure Active Directory обеспечивает:

- Статистической информации о hello [типы событий риска](active-directory-identity-protection-risk-events.md) , обнаружены

- Параметр toodownload hello отчета


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/456.png)


При выборе события риска отображается подробное представление отчета об этом событии, предоставляющее перечисленные ниже возможности.

- Параметр tooconfigure [политика исправления риск пользователя](active-directory-identityprotection.md#user-risk-security-policy)  

- Просмотрите hello обнаружения временная шкала событий риска hello  

- Просмотр списка пользователей, для которых было обнаружено это событие риска.

- [Ручное закрытие события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторная активация события риска, закрытого вручную. 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/457.png)

При выборе пользователя отображается подробное представление отчета об этом пользователе, предоставляющее перечисленные ниже возможности.

- Просмотреть все входы откройте hello

- Сброс пароля пользователя hello

- Отклонение всех событий.

- Проанализируйте обнаруженную риск события для пользователя hello. 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/324.png)


tooinvestigate события риска, выберите его из списка hello.  
При этом откроется hello **сведения** колонку для этого события риска. На hello **сведения** колонки, у вас есть параметр tooeither hello [вручную закрыть события риска](active-directory-identityprotection.md#closing-risk-events-manually) или повторно активировать событие вручную закрытого риска. 


![События входа, представляющие риск](./media/active-directory-reporting-security-risky-sign-ins/325.png)





## <a name="next-steps"></a>Дальнейшие действия

- Дополнительные сведения о защите идентификации Azure см. в статье [Защита идентификации Azure Active Directory](active-directory-identityprotection.md).

