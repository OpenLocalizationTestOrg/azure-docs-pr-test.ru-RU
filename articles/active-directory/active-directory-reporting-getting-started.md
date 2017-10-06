---
title: "Отчетность Azure Active Directory: начало работы | Документация Майкрософт"
description: "Здравствуйте, списки различных доступных отчетов reporting Azure Active Directory"
services: active-directory
documentationcenter: 
author: dhanyahk
manager: femila
editor: 
ms.assetid: 7ac99919-8df5-4424-9298-fc7c025ba949
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/16/2017
ms.author: dhanyahk;markvi
ms.openlocfilehash: f47875708398391dd7f3efdc56a741fdba273b76
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-active-directory-reporting"></a>Приступая к работе со средством создания отчетов Azure Active Directory
## <a name="what-it-is"></a>Что это
Azure Active Directory (Azure AD) формирует отчеты о безопасности, активности и аудите каталога. Ниже приведен список включенных отчетов hello:

### <a name="security-reports"></a>Отчеты о безопасности
* Попытки входа из неизвестных источников
* "Операции входа после нескольких неудачных попыток";
* "Операции входа из нескольких географических регионов".
* Попытки входа с IP-адресов с подозрительными действиями
* Нестандартные действия при входе
* Попытки входа с возможно инфицированных устройств
* Пользователи с аномальными событиями при входе

### <a name="activity-reports"></a>Отчеты об активности
* Использование приложения: сводка
* Использование приложения: подробности
* Панель мониторинга приложений
* Ошибки подготовки учетной записи
* Устройства отдельного пользователя
* Активность отдельного пользователя
* Отчет о действиях групп
* Отчет о событиях регистрации для сброса пароля
* Действие сброса пароля

### <a name="audit-reports"></a>Отчеты об аудите
* Отчет об аудите каталога

> [!TIP]
> Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="how-it-works"></a>Принцип работы
### <a name="reporting-pipeline"></a>Конвейер отчетов
Hello отчетов конвейер состоит из трех основных этапов. Каждый раз при входе или проверка подлинности, происходит hello следующее:

* Во-первых проверки подлинности пользователя hello (успешно или неуспешно) и hello результат сохраняется в базах данных службы Azure Active Directory hello.
* Все недавние попытки пользователей войти в систему регулярно обрабатываются с определенными интервалами. На этом этапе наши алгоритмы безопасности и поиска аномальных событий проверяют все недавние входы в систему на предмет подозрительных действий.
* После обработки hello отчеты записываются, кэшируются и обработаны в hello классический портал Azure.

### <a name="report-generation-times"></a>Время создания отчета
Из-за toohello большой объем проверки подлинности и входа, что модули обрабатываемых hello платформы Azure AD hello последнего входа в систему обработки, в среднем старого один час. В редких случаях может потребоваться копирование too8 часы tooprocess hello последнего входа в систему.

Изучив текст справки hello hello верхней части каждого отчета, можно найти вход hello последней обработки.

![Текст справки hello верхней части каждого отчета](./media/active-directory-reporting-getting-started/reportingWatermark.PNG)

> [!TIP]
> Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="getting-started"></a>Приступая к работе
### <a name="sign-into-hello-azure-classic-portal"></a>Вход в hello классический портал Azure
Во-первых, необходимо toosign в hello [классический портал Azure](https://manage.windowsazure.com) администратор глобальной или соответствия. Также должен быть администратором службы подписки Azure или соадминистратора, или использовать hello» доступа tooAzure AD» подписки Azure.

### <a name="navigate-tooreports"></a>Перейдите tooReports
Отчеты tooview Перейдите вкладку отчеты toohello вверху hello вашего каталога.

Если вы впервые, просмотр отчетов hello, вам потребуется tooa tooagree-диалоговое окно перед просмотром отчетов hello. Это tooensure, что он допустим для администраторов в вашей организации tooview эти данные, которые может рассматриваться как конфиденциальные сведения, в некоторых странах.

![Диалоговое окно](./media/active-directory-reporting-getting-started/dialogBox.png)

### <a name="explore-each-report"></a>Изучение каждого отчета
Перейдите в каждой toosee hello отчета во время сбора и обработки входа в систему hello. Можно найти [списка всех отчетов hello здесь](active-directory-reporting-guide.md).

![Все отчеты](./media/active-directory-reporting-getting-started/reportsMain.png)

### <a name="download-hello-reports-as-csv"></a>Загрузить hello отчеты в формате CSV
Каждый отчет можно загрузить как CSV-файл (с разделителями-запятыми). Можно использовать эти файлы в Excel, PowerBI или анализа сторонних программ toofurther анализа данных.

любой отчет в виде CSV-ФАЙЛ, toodownload перейдите toohello отчета и нажмите кнопку «Загрузить» внизу hello.

![Кнопка загрузки](./media/active-directory-reporting-getting-started/downloadButton.png)

> [!TIP]
> Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="next-steps"></a>Дальнейшие действия
### <a name="customize-alerts-for-anomalous-sign-in-activity"></a>Настройка оповещений в случае аномальных действий при входе в систему
Перейдите toohello вкладку «Настройка» каталога.

Прокрутите toohello раздел «Уведомления».

Включить или отключить раздел «Уведомления по электронной почте об аномальных попытках входа» hello.

![Hello раздел уведомлений](./media/active-directory-reporting-getting-started/notificationsSection.png)

### <a name="integrate-with-hello-azure-ad-reporting-api"></a>Интеграция с hello API отчетов Azure AD
В разделе [Приступая к работе с hello Reporting API](active-directory-reporting-api-getting-started.md).

### <a name="engage-multi-factor-authentication-on-users"></a>Включение службы Multi-Factor Authentication для пользователей
Выберите пользователя в отчете.

Нажмите кнопку «Включить многофакторную проверку Подлинности» hello hello нижней части экрана приветствия.

![Кнопка многофакторной проверки подлинности Hello hello нижней части экрана приветствия](./media/active-directory-reporting-getting-started/mfaButton.png)

> [!TIP]
> Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
> 
> 

## <a name="learn-more"></a>Подробнее
### <a name="audit-events"></a>Аудит событий
Дополнительные сведения о какие события подлежат аудиту в каталоге hello в [Azure Active Directory Reporting событий аудита](active-directory-reporting-audit-events.md).

### <a name="api-integration"></a>Интеграция API
В разделе [Приступая к работе с hello Reporting API](active-directory-reporting-api-getting-started.md) и hello [справочная документация по API](https://msdn.microsoft.com/library/azure/mt126081.aspx).

### <a name="get-in-touch"></a>Будьте на связи
Чтобы отправить отзыв, получить справку или задать вопросы, напишите электронное письмо по адресу [aadreportinghelp@microsoft.com](mailto:aadreportinghelp@microsoft.com) .

> [!TIP]
> Дополнительную документацию по Azure AD Reporting см. в статье [Просмотр отчетов о доступе и использовании](active-directory-view-access-usage-reports.md).
> 
> 

