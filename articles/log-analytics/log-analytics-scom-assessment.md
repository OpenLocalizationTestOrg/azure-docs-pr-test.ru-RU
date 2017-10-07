---
title: "aaaOptimize среды System Center Operations Manager с помощью анализа журналов Azure | Документы Microsoft"
description: "Можно использовать hello tooassess решения hello риска и работоспособности серверной среды с регулярным интервалом Manager оценка системных Center операций."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: tysonn
ms.assetid: 49aad8b1-3e05-4588-956c-6fdd7715cda1
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: c024e53826e91524c120bdb98ae7d96d6dc37d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-environment-with-hello-system-center-operations-manager-assessment-preview-solution"></a>Оптимизация среды с hello решения System Center Operations Manager оценки (Предварительная версия)

![Символ System Center Operations Manager Assessment](./media/log-analytics-scom-assessment/scom-assessment-symbol.png)

Можно использовать hello tooassess решения hello риска и работоспособности серверной среды System Center Operations Manager с регулярным интервалом Manager оценка системных Center операций. Эта статья поможет вам установить, настроить и использовать решение для hello, позволяют предпринимать корректирующие действия для потенциальных проблем.

Это решение предоставляет упорядоченный список рекомендаций конкретных tooyour развернутой серверной инфраструктуре. Hello рекомендации разделены на четыре фокуса, областей, которые помогают быстро понять hello риска и примите необходимые меры.

Hello рекомендации основаны на hello знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов. Каждая рекомендация содержит обоснования, почему проблема может играть важную роль tooyou и как tooimplement hello предложенные изменения.

Можно выбрать приоритетные области, наиболее важные tooyour организации и отслеживать выполнение задач по рисков формированию работоспособной и свободной среды.

После добавления решения hello и оценка завершенной, сводные данные по приоритетным областям отображается на hello **системы Center Operations Manager оценки** панель мониторинга для инфраструктуры. Hello ниже описано, как toouse hello сведения о hello **системы Center Operations Manager оценки** панели мониторинга, где можно просматривать и предпринимать рекомендуемые действия для инфраструктуры SCOM.

![Заголовок решения System Center Operations Manager](./media/log-analytics-scom-assessment/scom-tile.png)

![Панель мониторинга "Оценка System Center Operations Manager"](./media/log-analytics-scom-assessment/scom-dashboard01.png)

## <a name="installing-and-configuring-hello-solution"></a>Установка и настройка решения hello

Hello решение работает с Microsoft System Operations Manager 2012 R2 и 2012 с пакетом обновления 1.

Используйте следующие сведения tooinstall hello и настроить решение hello.

 - Перед использованием решения оценки в OMS, необходимо установить решение hello. Установка решения hello из [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.SCOMAssessmentOMS?tab=Overview) или в соответствии с инструкциями hello в [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md).

 - После добавления рабочей области toohello решения hello, hello системы Center Operations Manager плитки оценки на панели мониторинга hello отображает сообщения требуется дополнительная настройка hello. Щелкните плитку hello и выполните действия по настройке hello упомянутые на странице приветствия

 ![Элемент "Оценка System Center Operations Manager" на панели мониторинга](./media/log-analytics-scom-assessment/scom-configrequired-tile.png)

 Конфигурация hello System Center Operations Manager можно сделать с помощью сценария hello, следуя hello шаги, описанные на странице конфигурации hello hello решения в OMS.

 Вместо этого tooconfigure оценки hello через консоль SCOM, ниже hello выполните шаги в hello же заказа
1. [Установить для системы Center Operations Manager оценки hello запуска от имени учетной записи](#operations-manager-run-as-accounts-for-oms)  
2. [Настройка системы Center Operations Manager оценки правила hello](#configure-the-assessment-rule)

## <a name="system-center-operations-manager-assessment-data-collection-details"></a>Сведения о сборе данных оценки System Center Operations Manager

Hello оценки System Center Operations Manager собирает данные WMI, данные реестра, данные журнала событий, данных Operations Manager с помощью Windows PowerShell, SQL-запросов, с помощью сервера hello, включен сборщик данных файла.

Hello следующей таблице приведены методы сбора данных для оценки диспетчера Operations Center системы и как часто данные собираются агентом.

| платформа | Direct Agent | Агент SCOM | Хранилище Azure | Нужен ли SCOM? | Отправка данных агента SCOM через группу управления | частота сбора |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | | | | &#8226; | | 7 дней |

## <a name="operations-manager-run-as-accounts-for-oms"></a>Учетные записи запуска от имени в Operations Manager для службы OMS

OMS строится на пакетах управления для рабочих нагрузок tooprovide ценных служб. Каждая рабочая нагрузка требует наличия пакетов управления toorun привилегии, относящиеся в другом контексте безопасности, например учетной записи домена. Настройка Operations Manager запуска от имени учетной записи tooprovide учетные данные.

Используйте следующую информацию, tooset hello Operations Manager запуска от имени учетной записи для системы Center Operations Manager оценки hello.

### <a name="set-hello-run-as-account"></a>Набор hello учетная запись запуска от имени

1. В hello консоль Operations Manager перейдите toohello **администрирования** вкладки.
2. В разделе hello **Настройка запуска от имени**, нажмите кнопку **учетные записи**.
3. Создайте запись запуска от имени, выполнив через приветствия мастера создания учетной записи Windows hello. Hello toouse учетной записи имеет один определенный hello и наличие всех hello ниже предварительные условия:

    >[!NOTE]
    Hello учетная запись запуска от имени должен соответствовать следующим требованиям:
    - Учетная запись домена, членом hello локальной группы администраторов на всех серверах в среде hello (все Operations Manager роли - сервера управления, базы данных Operations Manager, хранилище данных, отчетов, веб-консоль, шлюз)
    - Роль администратора диспетчера операции для группы управления hello проверяемый
    - Выполнение hello [сценарий](#sql-script-to-grant-granular-permissions-to-the-run-as-account) toogrant учетной записи toohello Гранулярные разрешения на экземпляре SQL Server, используемой Operations Manager.
      Примечание: Если эта учетная запись уже имеет права системного администратора, пропустите hello выполнения скрипта.

4. В разделе **Безопасность распространения** выберите **Более безопасно**.
5. Укажите сервер управления hello расположений для распространения hello учетной записи.
3. Вернитесь toohello Настройка запуска от имени и нажмите кнопку **профилей**.
4. Поиск hello *профиль оценки SCOM*.
5. должно быть имя профиля Hello: *Microsoft System Center помощник по настройке ядра SCOM оценки запуска как профиль*.
6. Щелкните правой кнопкой мыши и обновите его свойства и добавить hello недавно создана учетная запись запуска от имени созданный на шаге 3.

### <a name="sql-script-toogrant-granular-permissions-toohello-run-as-account"></a>Гранулярные разрешения toogrant toohello учетная запись запуска от имени для SQL сценария

Выполните следующие SQL сценария toogrant необходимые разрешения toohello запуска от имени учетной записи на hello экземпляра SQL Server, используемой Operations Manager hello.

```
-- Replace <UserName> with hello actual user name being used as Run As Account.
USE master

-- Create login for hello user, comment this line if login is already created.
CREATE LOGIN [UserName] FROM WINDOWS


--GRANT permissions toouser.
GRANT VIEW SERVER STATE too[UserName]
GRANT VIEW ANY DEFINITION too[UserName]
GRANT VIEW ANY DATABASE too[UserName]

-- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
-- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
EXEC sp_msforeachdb N'USE [?]; CREATE USER [UserName] FOR LOGIN [UserName];'

Use msdb
GRANT SELECT too[UserName]
Go

--Give SELECT permission on all Operations Manager related Databases

--Replace hello Operations Manager database name with hello one in your environment
Use [OperationsManager];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager DatawareHouse database name with hello one in your environment
Use [OperationsManagerDW];
GRANT SELECT too[UserName]
GO

--Replace hello Operations Manager Audit Collection database name with hello one in your environment
Use [OperationsManagerAC];
GRANT SELECT too[UserName]
GO

--Give db_owner on [OperationsManager] DB
--Replace hello Operations Manager database name with hello one in your environment
USE [OperationsManager]
GO
ALTER ROLE [db_owner] ADD MEMBER [UserName]

```


### <a name="configure-hello-assessment-rule"></a>Настройка правила оценки hello

Hello Center операций Manager оценки решения пакет управления содержит правила с именем *Microsoft System Center помощник по настройке ядра SCOM оценки выполнения оценки правила*. Это правило отвечает за выполнение оценки hello. tooenable hello правила и настройки частоты повторения hello, используйте hello процедуры, описанные ниже.

По умолчанию hello Microsoft System Center помощник по настройке ядра SCOM оценки выполнения оценки правило отключено. Оценка toorun hello, необходимо включить правило hello на сервере управления. Используйте следующие шаги hello.

#### <a name="enable-hello-rule-for-a-specific-management-server"></a>Включить правило hello для конкретного сервера управления

1. В hello **Authoring** рабочей области консоли Operations Manager hello, найдите правило hello *Microsoft System Center помощник по настройке ядра SCOM оценки выполнения оценки правила* в hello **правила** области.
2. В результатах поиска hello hello выберите ту, которая включает текст hello *тип: сервер управления*.
3. Щелкните правой кнопкой мыши правило hello и нажмите кнопку **переопределяет** > **для конкретного объекта данного класса: сервер управления**.
4.  В списке серверов управления, доступных для hello выберите сервер управления hello, где следует запускать правило hello.
5.  Убедитесь, что значение переопределения слишком**True** для hello **включено** значение параметра.  
    ![Параметр переопределения](./media/log-analytics-scom-assessment/rule.png)

Хотя по-прежнему в этом окне настройте частоту hello hello, выполняются с использованием следующей процедуры hello.

#### <a name="configure-hello-run-frequency"></a>Настройка частоты выполнения hello

Hello оценки — интервал по умолчанию hello настроенных toorun каждые 10 080 минут (или семь дней). Можно переопределить hello значение tooa минимальное значение 1440 минут (или один день). значение Hello представляет hello минимальный интервал между последовательными оценки выполняется. Интервал приветствия toooverride, используйте следующие действия hello.

1. В hello **Authoring** рабочей области консоли Operations Manager hello, найдите правило hello *Microsoft System Center помощник по настройке ядра SCOM оценки выполнения оценки правила* в hello **правила** области.
2. В результатах поиска hello hello выберите ту, которая включает текст hello *тип: сервер управления*.
3. Щелкните правой кнопкой мыши правило hello и нажмите кнопку **hello переопределения правила** > **для всех объектов класса: сервер управления**.
4. Изменение hello **интервал** tooyour значение параметра требуемое значение интервала. В следующем примере hello hello значение too1440 минут (один день).  
    ![Параметр интервала](./media/log-analytics-scom-assessment/interval.png)  
    Если hello значение сборки более 1440 минут, hello правило выполняется с интервалом в один день. В этом примере hello правило не учитывает значение интервала hello и работает с частотой один день.


## <a name="understanding-how-recommendations-are-prioritized"></a>Основные сведения о приоритизации рекомендаций

Каждая рекомендация получает взвешенное значение, определяющее относительную важность рекомендаций hello hello. Отображаются только наиболее важных рекомендаций hello 10.

### <a name="how-weights-are-calculated"></a>Процесс вычисления взвешенного значения

Взвешенные значения являются статистическими значениями, основанными на трех ключевых факторах.

- Hello *вероятность* вызовет что проблемы, обнаруженной проблемы. Более высокие значения вероятности приравниваются tooa высокой общей оценке для рекомендации hello.
- Hello *влияние* проблемы hello в вашей организации, если она является причиной проблемы. Более высокая степень влияния приравнивается tooa высокой общей оценке для рекомендации hello.
- Hello *усилия* необходимые рекомендации tooimplement hello. Более высокое значение усилий приравнивается tooa меньшей общей оценке для рекомендации hello.

Hello весовой коэффициент для каждой рекомендации выражается в процентах от hello общей оценки, доступной для каждой приоритетной области. Например если рекомендация в hello доступность и непрерывность бизнес-процессов приоритетной области имеет показатель 5%, реализация этой рекомендации повышает на общую доступность и непрерывность бизнес-процессов показатель на 5%.

### <a name="focus-areas"></a>Приоритетные области

**Доступность и непрерывность бизнес-процессов**. Эта область содержит рекомендации в отношении доступности служб, устойчивости инфраструктуры и защиты бизнеса.

**Производительность и масштабируемость** -фокус в этой области отображается toohelp рекомендации вашей организации ИТ-инфраструктуры увеличиваться, убедитесь, что ИТ-среды требованиям текущей производительности и возможности toorespond toochanging требуется инфраструктура.

**Обновление, миграция и развертывание** — в этой области фокуса отображается toohelp рекомендации при обновлении, перенос и развертывание SQL Server tooyour существующей инфраструктуры.

**Операции и мониторинг** : фокус в этой области отображается оптимизировать toohelp рекомендации ИТ-операций, реализовать профилактического обслуживания и повышения производительности.

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a>Следует ли стремиться tooscore 100% в каждой приоритетной области?

Не обязательно. Hello рекомендации основываются на hello знания и опыт, приобретенные специалистами Майкрософт в результате многочисленных посещений клиентов. Однако не двух серверных инфраструктур, же hello и конкретные рекомендации могут быть более или менее соответствующие tooyou. Например некоторые рекомендации по безопасности может быть менее значимыми, если виртуальные машины не предоставляется toohello Интернета. Некоторые рекомендации о доступности могут иметь менее важное значение для служб, которые обеспечивают сбор низкоприоритетных данных. Проблемы, которые являются важной tooa зрелой организации может быть менее важные tooa при запуске. Можно tooidentify, какие области фокуса и затем отследить изменение оценок с течением времени.

В каждой рекомендации указано, почему она важна. Используйте это руководство tooevaluate целесообразность реализации рекомендации hello, условии hello характера ИТ служб и hello потребностям вашей организации.

## <a name="use-assessment-focus-area-recommendations"></a>Использование рекомендаций по оцениваемой приоритетной области

Перед использованием решения оценки в OMS, необходимо установить решение hello. tooread Дополнительные сведения об установке решений, в разделе [решений добавьте анализа журналов из коллекции решений hello](log-analytics-add-solutions.md). После установки, можно просмотреть сводку hello рекомендаций с помощью hello System Center Operations Manager плитки оценки на странице обзора hello в OMS.

Представление hello суммирование оценок соответствия для инфраструктуры, а затем глубже изучить рекомендации.

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a>рекомендации tooview фокус области и предпринять корректирующее действие

1. На hello **Обзор** щелкните hello **системы Center Operations Manager оценки** плитки.
2. На hello **системы Center Operations Manager оценки** , просмотрите сводные сведения о hello в одной из колонок приоритетной области hello и выберите один tooview рекомендации для этой приоритетной области.
3. На всех страницах интересующей области hello можно просмотреть hello приоритеты рекомендации для вашей среды. Щелкните рекомендацию, в разделе **затронутые объекты** tooview сведений о причинах hello рекомендации.  
    ![Приоритетная область](./media/log-analytics-scom-assessment/focus-area.png)
4. В разделе **Предложенные действия**представлены действия по исправлению, которые вы можете предпринять. Когда hello элементом будет устранена, последующие оценки будут указывать, что рекомендованные действия были выполнены, и тогда оценка соответствия возрастет. Исправленные элементы отображаются как **Прошедшие проверку объекты**.

## <a name="ignore-recommendations"></a>Игнорирование рекомендаций

Если у вас есть рекомендации, что требуется tooignore, можно создать текстовый файл, который OMS использует tooprevent отображения рекомендаций в результатах оценки.

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-want-tooignore"></a>tooidentify рекомендации, которые должны tooignore

1. Войдите в рабочую область tooyour и откройте раздел поиска журналов. Используйте hello рекомендации запроса toolist сбоев для компьютеров в вашей среде.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

    Вот запрос поиска журнала hello снимке экрана показан.  
    ![Поиск в журналах](./media/log-analytics-scom-assessment/scom-log-search.png)

2. Выберите рекомендации, которые должны tooignore. В следующей процедуре hello будут использоваться hello значения для recommendationid будут.

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a>toocreate и использование текстового файла IgnoreRecommendations.txt

1. Создайте файл с именем IgnoreRecommendations.txt.
2. Вставьте или введите каждое значение RecommendationId для каждой рекомендации требуется tooignore OMS в отдельной строке, а затем сохраните и закройте файл hello.
3. Поместите файл hello в следующие папки на каждом компьютере место рекомендации tooignore OMS hello.
4. На сервере управления Operations Manager hello - *SystemDrive*: \Program Files\Microsoft System Center 2012 R2\Operations Manager\Server.

### <a name="tooverify-that-recommendations-are-ignored"></a>tooverify игнорирования рекомендаций

1. После запуска hello следующего запланированного оценки по умолчанию каждые семь дней hello указан рекомендации помечаются как игнорируемые и не отображаются на панели мониторинга оценки hello.
2. Можно использовать hello следующих toolist запросы поиска журналов всех рекомендаций hello игнорируются.

    ```
    Type=SCOMAssessmentRecommendationRecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
    ```

3. Если вы решите позже, toosee учитываются рекомендации, удалите все файлы IgnoreRecommendations.txt или удалите из них Recommendationid.

## <a name="system-center-operations-manager-assessment-solution-faq"></a>Часто задаваемые вопросы по решению для оценки System Center Operations Manager

*Рабочая область OMS toomy решения оценки hello добавлены. Но я не вижу hello рекомендации. Почему так происходит?* После добавления решения hello, используйте hello следующих рекомендаций hello шагов представления на панели мониторинга OMS hello.  

- [Установить для системы Center Operations Manager оценки hello запуска от имени учетной записи](#operations-manager-run-as-accounts-for-oms)  
- [Настройка системы Center Operations Manager оценки правила hello](#configure-the-assessment-rule)


*Есть ли способ tooconfigure как часто выполняется оценка hello?* Да. В разделе [Настройка hello частота запуска](#configure-the-run-frequency).

*Если после добавления hello System Center Operations Manager решения по оценке обнаружен другой сервер, будет оценивается ли он?* Да, после обнаружения он будет оцениваться в дальнейшем. По умолчанию это будет происходить каждые семь дней.

*Что такое имя hello hello процесса, который hello сбора данных?* AdvisorAssessment.exe

*Где выполняется процесс AdvisorAssessment.exe hello?* AdvisorAssessment.exe выполняется hello службы работоспособности сервера управления hello включено правило оценки hello. С помощью этого процесса осуществляется обнаружение всей среды посредством удаленного сбора данных.

*Сколько времени требуется для сбора данных?* Время сбора данных на сервере hello занимает около одного часа. В средах, содержащих много экземпляров или баз данных Operations Manager, это может занять больше времени.

*Что делать, если задать интервал hello hello оценки сборки до 1440 мин?*  hello оценки — предварительно настроенных toorun на более чем один раз в день. Если значение tooa значение интервала hello меньше 1440 минут, оценки hello использует 1440 минут как значение интервала hello.

*Как tooknow в случае сбоев необходимых?* Если вы не видите результаты оценки hello выполнялся, будет скорее всего, что сбой некоторых hello предварительных требований для оценки hello. Можно выполнять запросы: `Type=Operation Solution=SCOMAssessment` и `Type=SCOMAssessmentRecommendation FocusArea=Prerequisites` в hello toosee поиска журналов сбой предварительных требований.

*Среди невыполненных предварительных требований отображается сообщение `Failed tooconnect toohello SQL Instance (….).`. Что такое hello проблему?* AdvisorAssessment.exe hello процесс, который собирает данные, выполняется hello службы работоспособности сервера управления hello. В ходе оценки hello hello процесс пытается tooconnect toohello SQL Server, где находится база данных Operations Manager hello. Эта ошибка может возникать, когда экземпляр SQL Server toohello подключения hello блокируют правила брандмауэра.

*Какие типы данных собираются?*  hello следующие типы данных собираются: - WMI - данные - EventLog - Operations Manager данных реестра через Windows PowerShell, SQL-запросы и файл сборщик данных.

*Почему у tooconfigure учетная запись запуска от имени* Для сервера Operations Manager выполняются различные SQL-запросы. Для них toorun, необходимо использовать учетная запись запуска от имени с необходимыми разрешениями. Кроме того учетные данные локального администратора, необходимые tooquery WMI.

*Почему отображаются только первые 10 рекомендаций hello?* Вместо исчерпывающим, полного списка задач, мы рекомендуем сконцентрироваться на рекомендациях hello приоритеты. После этого станут доступны дополнительные рекомендации. При желании toosee hello подробный список всех рекомендаций, с помощью поиска журналов можно просмотреть.

*Есть ли способ tooignore рекомендации?* Да, просмотреть hello [игнорировать рекомендации](#Ignore-recommendations).


## <a name="next-steps"></a>Дальнейшие действия

- [Выполнять поиск в журналах](log-analytics-log-searches.md) tooview подробных данных System Center Operations Manager оценки и рекомендации.
