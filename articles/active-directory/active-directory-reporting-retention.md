---
title: "политики хранения отчетов aaaAzure Active Directory | Документы Microsoft"
description: "Политики хранения данных отчета в Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 183e53b0-0647-42e7-8abe-3e9ff424de12
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: c46a68198cb34e9c92662b2f8461010745392c04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-report-retention-policies"></a>Политики хранения отчетов Azure Active Directory


Этот раздел содержит ответы toohello самые распространенные вопросы в сочетании с hello хранение данных для отчетов hello другого действия в Azure Active Directory. 

**Вопрос. как получить коллекцию hello данных действий запуска?**

**Ответ.**

| Выпуск Azure AD | Начало сбора |
| :--              | :--   |
| Azure AD Premium P1 <br /> Azure AD Premium P2 | При регистрации для подписки |
| Azure AD уровня "Бесплатный" | Здравствуйте, первый раз при открытии hello [колонке Azure Active Directory](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/Overview) или использовать hello [reporting API-интерфейсы](https://aka.ms/aadreports)  |

---
**В. когда данные о действиях доступен в hello портал Azure?**

**Ответ.**

- **Немедленно** — Если вы уже работали с отчетами в hello классический портал Azure
- **В течение 2 часов** — Если вы не включили reporting в hello классический портал Azure

---
**Вопрос. как получить коллекцию hello сигналы безопасности работы?**  

**Ответ** сигналов безопасности hello коллекции процесс начинается при вы явно согласиться на центр защиты toouse hello удостоверения. 


---
**Вопрос для продолжительность hello собранные данные хранятся?**

**Ответ.**

**Отчеты о действиях**    

| Отчет                 | Azure AD уровня "Бесплатный" | Azure AD Premium P1 | Azure AD Premium P2 |
| :--                    | :--           | :--                 | :--                 |
| Аудит каталога        | 7 дней        | 30 дней             | 30 дней             |
| Действия при входе       | 7 дней        | 30 дней             | 30 дней             |

**Сигналы системы безопасности**

| Отчет         | Azure AD уровня "Бесплатный" | Azure AD Premium P1 | Azure AD Premium P2 |
| :--            | :--           | :--                 | :--                 |
| пользователи под угрозой;  | 7 дней        | 30 дней             | 90 дней             |
| Вход, представляющий риск | 7 дней        | 30 дней             | 90 дней             |

---