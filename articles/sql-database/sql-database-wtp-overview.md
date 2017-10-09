---
title: "aaaIntro Wingtip SaaS - мультитенантное приложение базы данных SQL Azure | Документы Microsoft"
description: "Дополнительные сведения с помощью нескольких клиентов пример приложения, использующего базу данных SQL Azure, приложение hello Wingtip SaaS"
keywords: "руководство по базе данных sql"
services: sql-database
author: stevestein
manager: jhubbard
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: sstein
ms.openlocfilehash: daeed293116fca22718831b780533be6ef2ad178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toohello-wingtip-saas-application"></a>Введение toohello приложения Wingtip SaaS

Hello *Wingtip SaaS* приложения представляет собой образец мультитенантное приложение, демонстрирует преимущества уникальный hello базы данных SQL. приложение Hello использует базы данных отдельных клиентов, модель приложения SaaS, tooservice нескольких клиентов. Это приложение Hello спроектированный tooshowcase функции базы данных SQL Azure, позволяющие SaaS сценариев, включая несколько шаблонов проектирования и управления SaaS. tooquickly запуск и работает, менее чем за пять минут развертывает приложение Wingtip SaaS hello!

Приложение исходного кода и сценариев управления доступны в hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) в репозитории github. сценарии toorun hello, [hello модулей обучения папка загрузки](#download-and-unblock-the-wingtip-saas-scripts) tooyour локального компьютера.

## <a name="sql-database-wingtip-saas-tutorials"></a>Руководства по SaaS Wingtip базы данных SQL

После развертывания приложения hello, изучите следующие учебники, которые созданы на основе первоначального развертывания hello hello. В этих руководствах рассматриваются распространенные шаблоны SaaS, использующие преимущества встроенных функций базы данных SQL, хранилища данных SQL и других служб Azure. Учебники содержат сценариев PowerShell, с помощью подробные пояснения, которые существенно упрощают анализ, и реализация hello SaaS управления шаблоны в приложениях.


| Учебник | Описание |
|:--|:--|
|[Развертывание и просмотр приложения Wingtip SaaS hello](sql-database-saas-tutorial.md)| **НАЧНИТЕ ЗДЕСЬ!** Развертывание и просмотр tooyour приложения Wingtip SaaS hello подписки Azure. |
|[Подготовка новых клиентов и их регистрация в каталоге](sql-database-saas-tutorial-provision-and-catalog.md)| Узнайте, как приложение hello подключается tootenants, используя базу данных каталога и сопоставление каталога hello клиенты tootheir данных. |
|[Мониторинг производительности примера приложения SaaS Wingtip](sql-database-saas-tutorial-performance-monitoring.md)| Узнайте, как мониторинг toouse функции базы данных SQL и как tooset оповещения при превышении пороговых значений производительности. |
|[Настройка и использование Log Analytics (OMS) с примером приложения SaaS WTP](sql-database-saas-tutorial-log-analytics.md) | Дополнительные сведения об использовании [анализа журналов](../log-analytics/log-analytics-overview.md) toomonitor большое количество ресурсов для нескольких пулов. |
|[Восстановление базы данных отдельного клиента](sql-database-saas-tutorial-restore-single-tenant.md)| Узнайте, как toorestore предыдущего клиента tooa базы данных на определенный момент времени. Действия toorestore tooa параллельных базы данных, создание hello существующего клиента через Интернет, также будут включены. |
|[Управление схемой для нескольких клиентов в приложении SaaS Wingtip](sql-database-saas-tutorial-schema-management.md)| Узнайте, как tooupdate схемы и обновление ссылки на данные, распределяются по всем клиентам Wingtip SaaS. |
|[Выполнение запросов ad-hoc-аналитики по всем клиентам SaaS Wingtip](sql-database-saas-tutorial-adhoc-analytics.md) | Создание базы данных аналитики ad-hoc и выполнение распределенных запросов в реальном времени по всем клиентам.  |
|[Выполнение распределенных запросов в нескольких базах данных SQL Azure](sql-database-saas-tutorial-tenant-analytics.md) | Извлечение данных клиента в базу данных аналитики или хранилище данных для выполнения автономных аналитических запросов. |



## <a name="application-architecture"></a>Архитектура приложения

приложение Wingtip SaaS Hello использует hello модели базы данных каждого клиента и эффективность toomaximize пулах эластичных БД SQL. Для подготовки и сопоставление данных tootheir клиентов, используется база данных каталога. приложение Wingtip SaaS core Hello, использует пул с тремя образец клиентов, а также hello каталога базы данных. Завершение работы многие hello учебники Wingtip SaaS привести начальное развертывание toohello надстройки, путем введения аналитических баз данных, межбазовые схем управления и т. д.


![Архитектура SaaS Wingtip](media/sql-database-wtp-overview/app-architecture.png)


Во время прохождения по учебники hello и работа с приложение hello, это важно toofocus SaaS с комбинациями hello относятся toohello уровня данных. Другими словами сосредоточиться на уровень данных hello, а не более чем анализировать само приложение hello. Основные сведения о реализации hello эти шаблоны SaaS является ключа tooimplementing этих шаблонов в приложениях, принимая во внимание необходимые изменения для конкретных бизнес-требований.

## <a name="download-and-unblock-hello-wingtip-saas-scripts"></a>Загрузите и разблокировать сценарии Wingtip SaaS hello

Исполняемое содержимое (скрипты, библиотеки DLL) может быть заблокировано Windows, в то время как ZIP-файлы можно загрузить с внешнего источника, а затем извлечь их содержимое. При извлечении hello скрипты из ZIP-файл, ***выполните действия hello ниже toounblock hello ZIP-файл перед извлечением***. Это гарантирует, что hello сценарии могут toorun.

1. Обзор слишком[Wingtip SaaS hello в репозитории github](https://github.com/Microsoft/WingtipSaaS).
1. Выберите **Clone or download** (Клонировать или скачать).
1. Нажмите кнопку **загрузить ZIP** и сохраните файл hello.
1. Щелкните правой кнопкой мыши hello **WingtipSaaS master.zip** правой кнопкой мыши и выберите **свойства**.
1. На hello **Общие** выберите **Unblock**.
1. Нажмите кнопку **ОК**.
1. Извлеките файлы hello.

Скрипты, расположенные в hello *... \\WingtipSaaS master\\модулей обучения* папки.


## <a name="working-with-hello-wingtip-saas-powershell-scripts"></a>Работа с hello сценариев PowerShell Wingtip SaaS

tooget hello наиболее из образца hello необходимо toodive в предоставленный hello скрипты. Использование точек останова и прохождение по скриптам hello, проверив hello подробные сведения о реализации различных шаблонов SaaS hello. пошагово tooeasily hello предоставленные сценарии и модули для hello, лучше всего понимание того, мы рекомендуем использовать hello [интегрированной среды Сценариев PowerShell](https://msdn.microsoft.com/powershell/scripting/core-powershell/ise/introducing-the-windows-powershell-ise).

### <a name="update-hello-configuration-file-for-your-deployment"></a>Обновить файл конфигурации hello для развертывания

Изменить hello **UserConfig.psm1** файл с hello ресурсов пользователей и групп значение, заданное во время развертывания:

1. Откройте hello *интегрированной среды Сценариев PowerShell* и загрузки... \\Модулях обучения\\*UserConfig.psm1* 
1. Обновление *ResourceGroupName* и *имя* с определенными значениями hello для развертывания (в строках, 10 и 11 только).
1. Сохраните изменения hello!

Установка этих значений ниже просто позволяет избежать tooupdate эти значения относящиеся к развертыванию в каждом сценарии.

### <a name="execute-scripts-by-pressing-f5"></a>Выполнение скрипта нажатием клавиши F5

Используйте несколько скриптов *$PSScriptRoot* папки toonavigate и *$PSScriptRoot* вычисляются только при выполнении скриптов, нажав клавишу **F5**.  Если выделить несколько скриптов и запустить их (**F8**), может произойти ошибка, поэтому нажмите клавишу **F5** при выполнении скриптов.

### <a name="step-through-hello-scripts-tooexamine-hello-implementation"></a>Пошаговое выполнение реализации hello tooexamine сценарии hello

— Hello лучшим способом toounderstand hello скрипты, настроив их toosee их возможности. Извлечение hello включены **Демонстрация -** сценарии, представляющие легко toofollow высокоуровневый рабочий процесс. Hello **Демонстрация -** сценарий, демонстрирующий tooaccomplish необходимые шаги hello каждой задачи таким образом задать точки останова и детализации глубже в отдельные hello вызывает toosee сведения о реализации для hello различных шаблонов SaaS.

Советы для просмотра и пошагового выполнения скриптов PowerShell:

* Откройте **Демонстрация -** сценариев в интегрированной среде Сценариев PowerShell hello.
* Выполните скрипт или продолжайте работу, нажав клавишу **F5** (использование клавиши **F8** не рекомендуется, так как при этом переменная *$PSScriptRoot* не обрабатывается во время выполнения нескольких скриптов).
* Поместите точки останова, щелкнув или выбрав линию и нажав клавишу **F9**.
* Чтобы обойти функцию или вызов скрипта, нажмите клавишу **F10**.
* Чтобы перейти к функции или вызову скрипта, нажмите клавишу **F11**.
* Шаг с выходом из текущей функции hello, или с помощью вызова **Shift + F11**.


## <a name="explore-database-schema-and-execute-sql-queries-using-ssms"></a>Просмотр схемы базы данных и выполнение SQL-запросов с помощью SSMS

Используйте [SQL Server Management Studio (SSMS)](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms) tooconnect и обзор hello серверы приложений и баз данных.

Развертывание Hello изначально имеет две базы данных SQL серверы tooconnect слишком hello *tenants1 -&lt;пользователя&gt;*  сервера и hello *каталога -&lt;пользователя&gt;* сервера. оба сервера имеют tooensure соединение успешно Демонстрация [правило брандмауэра](sql-database-firewall-configure.md) разрешение всех IP-адресов через.


1. Откройте *SSMS* и подключите toohello *tenants1 -&lt;пользователя&gt;. database.windows.net* сервера.
1. Щелкните **Подключить** > **Компонент ядра СУБД…**:

   ![сервер каталога](media/sql-database-wtp-overview/connect.png)

1. Используйте такие демонстрационные учетные данные: имя пользователя — *developer*, пароль — *P@ssword1*.

   ![connection;](media\sql-database-wtp-overview\tenants1-connect.png)

1. Повторите шаги 2-3 и подключите toohello *каталога -&lt;пользователя&gt;. database.windows.net* сервера.

После успешного подключения вы увидите оба сервера. Список баз данных может отличаться в зависимости от hello клиентов, которые подготовлены:

![обозреватель объектов](media/sql-database-wtp-overview/object-explorer.png)



## <a name="next-steps"></a>Дальнейшие действия

[Развертывание приложения Wingtip SaaS hello](sql-database-saas-tutorial.md)
