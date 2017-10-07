---
title: "aaaHow toouse hello Azure Active Directory пакет содержимого Power BI | Документы Microsoft"
description: "Узнайте, как toouse hello Azure Active Directory пакет содержимого Power BI"
services: active-directory
author: MarkusVi
manager: femila
ms.assetid: addd60fe-d5ac-4b8b-983c-0736c80ace02
ms.service: active-directory
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d07d678aedbe3089c4ea5f981f72311bdb389a17
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-azure-active-directory-power-bi-content-pack"></a>Как toouse hello Azure Active Directory пакет содержимого Power BI

Вам, как ИТ-администратору, важно знать, как ваши пользователи внедряют и используют возможности Azure Active Directory. Она позволяет tooplan tooincrease использования ИТ инфраструктуры и обмен данными и tooget hello наиболее эффективно использовать возможности AAD. Содержимое Power BI пакет для Azure Active Directory предоставляет hello toofurther возможность анализировать вашей toounderstand данные об использовании этого данных toogather всестороннее анализировать происходящем с их Azure Active Directory для hello различные функциональные возможности вы активно используют.  С hello интеграции Azure Active Directory, интерфейсы API в Power BI можно легко загрузить hello готовые пакеты содержимого и анализировать действия tooall hello в Azure Active Directory с помощью Power BI предлагает широкие возможности визуализации опытом. Вы можете создавать собственные панели мониторинга и легко предоставлять к ним доступ любому пользователю в организации. 

Этот раздел содержит пошаговые инструкции по hello как tooinstall и использования содержимого пакета в вашей среде.

## <a name="installation"></a>Установка  

**hello tooinstall пакет содержимого Power BI:**

1. Войдите на [Power BI](https://app.powerbi.com/groups/me/getdata/services) с вашей учетной записью Power BI (это hello учетной записью вашей учетной записи Azure AD или Office 365).

2. Hello нижней части панели навигации слева hello, выберите **получение данных**.

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/01.png)
 
3. В hello **службы** щелкните **получить**.
   
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/02.png)

4.  Выполните поиск по запросу **Azure Active Directory**.

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/03.png)
 
5.  При появлении запроса введите свой идентификатор клиента Azure AD и нажмите кнопку **Далее**.

    > [!TIP] 
    > Hello tooget быстро ИД клиента для вашего клиента Office 365 или Azure AD — toologin toohello портала Azure AD, детализация углублением toohello каталог и скопируйте идентификатор hello из hello URL-адреса: https://manage.windowsazure.com/woodgroveonline.com#Workspaces/ ActiveDirectoryExtension иликаталога/<tenantid>/directoryQuickStart

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/04.png) 

6.  Нажмите кнопку **Войти**. 
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/05.png) 



7.  Введите имя пользователя и пароль, а затем нажмите кнопку **Войти**.
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/06.png) 

8.  В диалоговом окне согласия приложения hello, нажмите кнопку **Accept**.
 
9.  Когда панель мониторинга журналов действий Active Directory Azure будет создана, щелкните ее.
 
    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/08.png) 

## <a name="what-can-i-do-with-this-content-pack"></a>Что можно сделать с помощью этого пакета содержимого?

Прежде чем мы зайдем в возможностях этого пакета содержимого, Вот краткий обзор hello различных отчетов hello содержимого пакета. Отчет данных возвращается toohello **последние 30 дней**.

### <a name="reports-included-in-this-version-of-azure-active-directory-logs-content-pack"></a>Отчеты, включенные в эту версию пакета содержимого журналов Azure Active Directory

**Отчет об использовании приложения и тенденции**: анализ приложения hello, используемых в вашей организации и какие из них используются наиболее hello и когда. Можно использовать этот отчет toogather ценную информацию об использовании приложения, которые вы недавно распространен в вашей организации или узнать, какие приложения часто используются. Таким образом, можно улучшить использование, если вы видите, если приложение hello не используется.

**Войти в систему пользователями и расположение**: понять все hello входов выполняется с использованием удостоверения Azure и позволяет анализировать hello удостоверения пользователей hello. Из этого отчета вы можете получить более подробную информацию об отдельных входах и ответить на следующие вопросы.

- Откуда этот пользователь входит в систему?
- Какие пользователя hello большинство входа в систему и где они вход из? 
- Успешно войти hello?  
 
Чтобы просмотреть подробные сведения, щелкните определенную дату или расположение.

**Число уникальных пользователей на каждое приложение.** Узнайте обо всех уникальных пользователях, использующих определенное приложение. Этот отчет включает только пользователей, которые *успешно* вошли в приложение.

**Войти в систему устройства**: получить представление о hello тип операционной системы и браузеры используются пользователями в организации с подробными сведениями с пользователями hello, включая:

- Имя пользователя
- IP-адрес
- Расположение 
- состояние входа. 

В этом отчете вы понимаете hello различные профили устройство используется в вашей организации и определить политики устройств, в зависимости от используемой

**Воронка SSPR.** Узнайте, как в вашей организации используется функция сброса пароля. Взгляните на сколько пароль сбрасывает была предпринята попытка через средство SSPR hello и сколько из них выполнены успешно. Глубже изучить сбоя сбрасывает пароль hello, с помощью SSPR воронкообразной hello и понять, почему произошел определенных ошибок. Этот отчет содержит более глубокого понимания hello SSPR средство использования вашей организации, можно принять правильные решения hello.

## <a name="customizing-azure-ad-activity-content-pack"></a>Настройка пакета содержимого действий Azure AD

**Измените визуализацию**: визуализации отчетов можно изменить, щелкнув **редактировать отчет** и выберите визуализацию hello требуется.
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/09.png) 
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/10.png) 

**Включить дополнительные поля**: можно добавить отчет toohello поля или удалите его, выбрав hello visual toowhich tooadd или удалить поле hello. В следующем примере hello я добавляю представление таблицы toohello поле «состояние». 
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/11.png) 

**Панель мониторинга tooyour визуализации ПИН-код**: можно настроить информационную панель и включить отчету toohello визуализации и закрепите его toohello панели мониторинга. В следующем примере hello добавлен новый фильтр, который называется «состояние» и его включения в отчет hello. Также заменяли линейчатой диаграммы tooa график визуализации hello и можно закрепить этой панели мониторинга visual toohello.

![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/12.png) 

![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/13.png) 
 

 


**Общий доступ к панели мониторинга**: после создания hello содержимого можно предоставить мониторинга hello hello пользователи в вашей организации. Обратите внимание, что после отправки отчета hello, они могут просматривать hello полей, выбранных в отчете hello.
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/14.png) 



## <a name="scheduling-a-daily-refresh-of-your-power-bi-report"></a>Планирование ежедневного обновления отчета Power BI

tooschedule ежедневного обновления отчета Power BI, перейдите в слишком**наборы данных > Параметры > расписание обновлений** и задайте его, как показано ниже.
 
![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/15.png) 

## <a name="updating-toonewer-version-of-content-pack"></a>Обновление версии toonewer содержимого пакета

Если требуется, чтобы tooupdate содержимое пакета tooget более новой версии:

- Загрузите новый пакет содержимого hello и настройте его согласно инструкциям, приведенным в статье.

- После настройки его, перейдите в слишком**источник данных > Параметры > учетные данные источника данных** и повторно введите учетные данные, как показано ниже

    ![Пакет содержимого Azure Active Directory Power BI](./media/active-directory-reporting-power-bi-content-pack-how-to/16.png) 

Как только новая версия пакета содержимого hello hello работает, при необходимости, удалив hello Базовые отчеты и наборы данных, связанные с этим пакетом содержимого можно удалить старую версию hello.

## <a name="still-having-issues"></a>Возникли проблемы? 

См. [руководство по устранению неполадок](active-directory-reporting-troubleshoot-content-pack.md). Общие сведения о Power BI см. в [справочных статьях](https://powerbi.microsoft.com/en-us/documentation/powerbi-service-get-started/).
 

## <a name="next-steps"></a>Дальнейшие действия

Обзор отчетов см. в разделе hello [отчетов Azure Active Directory](active-directory-reporting-azure-portal.md).
