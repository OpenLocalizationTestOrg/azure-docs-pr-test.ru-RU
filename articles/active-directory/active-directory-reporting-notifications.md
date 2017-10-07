---
title: "aaaAzure уведомления Reporting Active Directory"
description: "Как toouse hello уведомления отчетов Azure Active Directory для подозрительных входа в систему."
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ae6d4b0e-5931-4cb3-98bf-9be91b381c92
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.custom: oldportal
ms.reviewer: dhanyahk
ms.openlocfilehash: 3843c45eaf9d68e671943bfdbc7ab68933f38fbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-notifications"></a>Уведомления отчетов Azure Active Directory
## <a name="what-reports-generate-email-notifications"></a>Какие отчеты создают уведомления по электронной почте
В настоящее время только hello нестандартные действия при входе в триггерах отчетов действия уведомления по электронной почте.

## <a name="what-is-an-irregular-sign-in"></a>Что такое «нестандартные попытки входа»?
Нестандартных попытках входа, которые идентифицируются нашей алгоритмов машинного обучения, на основе hello условие «невозможно переместиться», в сочетании с нестандартного расположения и устройства. Это может означать, что злоумышленник попытки toosign имени этой учетной записи.

## <a name="who-receives-hello-email-notifications"></a>Кто получает уведомления по электронной почте hello?
Hello электронное письмо отправляется tooall глобальных администраторов, которым была назначена лицензия Active Directory Premium. tooensure, оно будет доставлено, мы отправляем его также администраторы toohello запасной адрес электронной почты. Администраторы должны включить aad-alerts-noreply@mail.windowsazure.com в свой список надежных отправителей, чтобы не пропустить hello электронной почты.

## <a name="how-often-are-these-emails-sent"></a>Как часто отправляются эти сообщения?
Hello электронное письмо отправляется в том случае, если 10 новых нестандартных вход действия выполняются в hello последние 30 дней или с момента последнего hello сообщения электронной почты было отправлено, какое значение меньше.

## <a name="how-do-i-access-hello-report-mentioned-in-hello-email"></a>Как получить доступ к отчетов hello, упомянутые в hello электронной почты?
При нажатии на ссылку hello, будет перенаправленный toohello страницы отчета в пределах hello классический портал Azure. В порядке tooaccess Здравствуйте отчет, необходимо, чтобы оба toobe:

* администратором или соадминистратором подписки Azure;
* Глобальный администратор в каталоге hello и назначить лицензию Active Directory Premium. Дополнительные сведения см. в разделе [Выпуски Azure Active Directory](active-directory-editions.md).

## <a name="can-i-turn-off-these-emails"></a>Можно ли отключить эти сообщения?
Да, tooturn вывод всех уведомлений, связанных с tooanomalous входа в систему в течение hello классический портал Azure, нажмите кнопку **Настройка**, а затем выберите **отключено** под hello **уведомления**раздел.

## <a name="whats-next"></a>Что дальше?
* Интересуют доступные отчеты о безопасности, аудиту и действиях? См. раздел [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
* [Начало работы с Azure Active Directory Premium](active-directory-get-started-premium.md)
* [Добавить корпоративную фирменную символику tooyour страницы входа и панели доступа](active-directory-add-company-branding.md)

