---
title: "aaaWhat — Azure Analysis Services | Документы Microsoft"
description: "Получите общую картину hello служб Analysis Services в Azure."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 83d7a29c-57ae-4aa0-8327-72dd8f00247d
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: 48830a86f47a8ddc7770e6c44dd56c29927fe582
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-azure-analysis-services"></a>Службы Azure Analysis Services
![Службы Azure Analysis Services](./media/analysis-services-overview/aas-overview-aas-icon.png)

Azure службы Analysis Services предоставляют моделирования в облаке hello данных уровня предприятия. Это полностью управляемая платформа как услуга (PaaS), интегрированная со службами платформ данных Azure. 

Службы Analysis Services позволяют комбинировать и объединять данные из нескольких источников, определять метрики и защищать данные в одной доверенной семантической модели данных. Hello модель данных предоставляет способ проще и быстрее вашей toobrowse пользователей значительные объемы данных с клиентскими приложениями, например Power BI, Excel, службы Reporting Services, сторонних и пользовательских приложений.

![Источники данных](./media/analysis-services-overview/aas-overview-data-sources.png)

Извлечение [в этом видеоролике](https://sec.ch9.ms/ch9/d6dd/a1cda46b-ef03-4cea-8f11-68da23c5d6dd/AzureASoverview_high.mp4) toolearn как Azure Analysis Services сочетается с Microsoft общую возможности бизнес-Аналитики и как можно обеспечить получение моделей данных в облаке hello.

## <a name="built-on-sql-server-analysis-services"></a>На основе SQL Server Analysis Services
Службы Azure Analysis Services совместимы с множеством полезных функций служб SQL Server Analysis Services выпуска Enterprise Edition. Azure службы Analysis Services поддерживают табличные модели на hello 1200 и 1400 [уровни совместимости](analysis-services-compat-level.md). Кроме того, поддерживаются секции, безопасность на уровне строк, двунаправленные связи и переводы. Режимы выполнения в памяти и DirectQuery обеспечивают высокую скорость обработки запросов в больших и сложных наборах данных.

Табличные модели помогают выполнять быструю разработку и использовать широкие возможности настройки. Для разработчиков табличные модели включают объекты модели toodescribe hello табличной модели объектов (TOM). TOM предоставляется в формате JSON с помощью hello [табличных языка скриптов модели (TMSL)](https://docs.microsoft.com/sql/analysis-services/tabular-model-scripting-language-tmsl-reference) и hello языка определения данных объектов AMO через hello [Microsoft.AnalysisServices.Tabular](https://msdn.microsoft.com/library/microsoft.analysisservices.tabular.aspx) пространства имен.

## <a name="better-with-azure"></a>Оптимизация с помощью Azure
Службы анализа Azure интегрируется с множество служб Azure, позволяя toobuild сложные аналитические решения. Интеграция с [Azure Active Directory](../active-directory/active-directory-whatis.md) обеспечивает защищенный доступ на основе ролей tooyour критически важных данных. Интеграция с [фабрики данных Azure](../data-factory/data-factory-introduction.md) конвейеры, включая действие, которое загружает данные в модели hello. Для упрощенной оркестрации моделей с применением пользовательского кода можно использовать [службу автоматизации Azure](../automation/automation-intro.md) и [Функции Azure](../azure-functions/functions-overview.md).

## <a name="get-up-and-running-quickly"></a>Быстрая настройка и подготовка к работе
На портале Azure вы можете [создать сервер](analysis-services-create-server.md) за считанные минуты. А с помощью PowerShell и [шаблонов](../azure-resource-manager/resource-manager-create-first-template.md) Azure Resource Manager можно подготовить серверы, используя декларативный шаблон. Используя один шаблон, можно развернуть несколько служб, включая такие компоненты Azure, как учетные записи хранения и Функции Azure. 

Создав сервер, приступайте к созданию табличной модели непосредственно на портале Azure. С помощью нового hello (Предварительная версия) [веб-компонентов конструктора](analysis-services-create-model-portal.md), можно подключиться tooan базы данных SQL Azure, источник данных в хранилище данных SQL Azure, или импортировать pbix-файла Power BI Desktop. Связи между таблицами создаются автоматически, и можно создавать меры или изменить файл model.bim hello в формате json вправо в браузере.

## <a name="scale-tooyour-needs"></a>Потребности tooyour шкалы
Службы Azure Analysis Services предоставляются на уровнях Developer, Basic и Standard. В рамках каждого уровня плана затраты на размер в зависимости от соответствующим tooprocessing питания, QPUs и памяти. Создавая сервер, выбирайте план в пределах одного уровня. Вы можете изменить планы или вниз в пределах hello же уровня или обновления tooa высокого уровня, но невозможно понизить из более высокого уровня tooa нижнего уровня.

Вы можете увеличить или уменьшить масштаб сервера, а также приостановить сервер. Используется hello портал Azure и полный контроль над на лету с помощью PowerShell. Вы платите только за то, что используете. в разделе toolearn Дополнительные сведения о различных планах hello и уровни и используйте hello ценовой калькулятор toodetermine hello продуманный план, [цены на Azure Analysis Services](https://azure.microsoft.com/pricing/details/analysis-services/).

## <a name="keep-your-data-close"></a>Централизованное хранение данных
Azure серверов служб Analysis Services можно создавать в следующих hello [регионах Azure](https://azure.microsoft.com/regions/):

| Северная и Южная Америка | Европа | Азиатско-Тихоокеанский регион |
|----------|--------|--------------|
|  Южная часть Бразилии<br> Центральная Канада<br> Восток США 2<br> Северо-центральный регион США<br> Южно-центральный регион США<br> Западно-центральная часть США<br> Запад США | Северная Европа<br> Южная часть Великобритании<br> Западная Европа |   Юго-Восточная часть Австралии<br> Восточная часть Японии<br> Юго-Восточная Азия<br> Западная Индия  |

Новые области добавляются все время hello, поэтому этот список может быть неполным. Выбрать расположение можно во время создания сервера на портале Azure или с помощью шаблонов Azure Resource Manager. tooget hello Наилучшая производительность, выберите расположение ближайшего наибольшее базы пользователей. А чтобы обеспечить [высокий уровень доступности](analysis-services-bcdr.md), развертывайте модели на избыточных серверах в нескольких регионах.

## <a name="migrate-your-existing-tabular-models"></a>Перенос существующих табличных моделей
Если уже существующих локальных решений модели SQL Server Analysis Services, можно перенести tooAzure Analysis Services без значительных изменений. toomigrate, можно использовать SSDT toodeploy сервера tooyour модели. Кроме того, в среде SSMS можно использовать резервное копирование и восстановление или скрипт TMSL.

Если у вас есть локальные источники данных, требуется tooinstall и настройте [локального шлюза данных](analysis-services-gateway.md). Если роли и члены ролей, которые уже настроены, перенести свои роли, но у вас есть члены роли tooreadd с помощью SSMS или PowerShell.

## <a name="connect-toopopular-data-sources"></a>Подключение источников данных toopopular
Azure службы Analysis Services поддерживают [подключение источников toodata](analysis-services-datasource.md) локально в вашей организации и в облаке hello. Вы также можете получить гибридное решение, объединив данные из локальных и облачных источников. 

Новых табличных моделей 1400 функция hello современных получение данных в SSDT на основе языка формул запроса hello M. Получить данные для toocreate возможности hello и дополнительные преобразования данных и другие возможности гибридного веб-приложения и изменить свои собственные сложные запросы языка формул M. Например, с помощью табличных моделей 1400 можно выполнять моделирование на основе файлов данных в хранилище BLOB-объектов Azure.

## <a name="use-hello-tools-you-already-know"></a>Используйте средства hello, вы уже знаете

![Средства разработчика бизнес-аналитики](./media/analysis-services-overview/aas-overview-dev-tools.png)

#### <a name="sql-server-data-tools-ssdt-for-visual-studio"></a>SQL Server Data Tools (SSDT) для Visual Studio
Разработка и развертывание моделей с произвольным hello [SQL Server Data Tools (SSDT) для Visual Studio](https://msdn.microsoft.com/library/mt204009.aspx). SSDT предоставляет шаблоны проектов Analysis Services для быстрой настройки и подготовки к работе. SSDT включает hello современных получить данные источника данных запроса и объединять функции для табличных моделей 1400. Если вы знакомы с получения данных в Power BI Desktop и Excel 2016, вы уже знаете, как легко toocreate высокой настраивать запросы к источнику данных.

#### <a name="sql-server-management-studio"></a>SQL Server Management Studio
Управляйте серверами и базами данных модели с помощью [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/mt238290.aspx). Подключите серверы tooyour в облаке hello. Выполните скрипты TMSL прямо из окна запросов XMLA hello и автоматизации задач с помощью скриптов TMSL. Новые возможности и функции SSMS появляются часто, так как обновления выходят каждый месяц.

#### <a name="powershell"></a>PowerShell
Задачи управления ресурсов сервера, такие как создание серверов, приостановка или возобновление работы сервера или изменение уровня службы hello (уровня) использовать командлеты диспетчера ресурсов Azure (AzureRM). Другие задачи для управления базами данных, такие как добавление или удаление членов роли обработки, или выполнение скриптов TMSL использовать командлеты в модуле SqlServer hello. Модули AzureRM и SQLServer доступны в hello [коллекции PowerShell](https://www.powershellgallery.com/).


## <a name="your-data-is-secure"></a>Надежное хранение данных
![Визуализации данных](./media/analysis-services-overview/aas-overview-secure.png)

#### <a name="authentication"></a>Аутентификация
Проверка подлинности пользователей в Azure Analysis Services осуществляется через [Azure Active Directory (AD)](../active-directory/active-directory-whatis.md). При попытке toolog в базе данных служб Analysis Services Azure tooan, пользователи используют удостоверение учетной записи организации с базой данных access toohello они пытаются tooaccess. Эти удостоверения пользователей должны быть членами по умолчанию hello Azure Active Directory для hello подписки, где находится сервер служб Analysis Services Azure hello. toolearn более, в разделе [проверки подлинности и пользовательские разрешения](analysis-services-manage-users.md).

#### <a name="data-security"></a>Защита данных
Azure Analysis Services использует toopersist хранилища больших двоичных объектов Azure, а также метаданные для баз данных служб Analysis Services. Файлы данных в большом двоичном объекте шифруются с использованием шифрования на стороне сервера. При использовании режима прямого запроса сохраняются только метаданные. Hello фактические данные можно получить из источника данных hello во время выполнения запроса.

#### <a name="on-premises-data-sources"></a>Локальные источники данных
Безопасный доступ toodata хранящихся локально в вашей организации достигается путем установки и настройки [локального шлюза данных](analysis-services-gateway.md). Шлюзы предоставляют доступ toodata для прямых запросов и режимами в памяти. При подключении источника данных tooan локальной модели служб Azure Analysis Services вместе с hello зашифрованные учетные данные для источника данных в локальной среде hello создания запроса. облачной службе шлюза Hello анализирует запрос hello и помещает tooan запрос hello Azure Service Bus. локальный шлюз Hello опрашивает hello Azure Service Bus для ожидающих запросов. затем Hello шлюза получает hello запрос, расшифровывает учетные данные hello и подключается toohello источника данных для выполнения. результаты Hello, затем отправлены из источника данных hello резервного шлюза toohello и на toohello Azure Analysis Services база данных.

Azure Analysis Services регулируется hello [Microsoft Online Services условия](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31) и hello [заявления о конфиденциальности Microsoft Online Services](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).
toolearn Дополнительные сведения о безопасности в Azure, в разделе hello [Центр управления безопасностью Microsoft](https://www.microsoft.com/trustcenter/Security/AzureSecurity).

## <a name="supports-hello-latest-client-tools"></a>Поддерживает новейшие средства клиента hello
![Визуализации данных](./media/analysis-services-overview/aas-overview-clients.png)

Современные средства просмотра и визуализации данных, в том числе Power BI, Excel и сторонние инструменты, предоставляют пользователям интерактивные визуальные представления моделей данных для анализа.

Клиенты используют MSOLAP, AMO или ADOMD [клиентские библиотеки](analysis-services-data-providers.md) tooconnect tooAnalysis служб серверов. Клиентские приложения Майкрософт, в частности Power BI Desktop и Excel, устанавливают все три клиентские библиотеки. Но помните, в зависимости от версии hello или частота обновления, клиентские библиотеки не может быть hello последние версии необходимых служб Azure Analysis Services. Hello применимо и к toocustom приложений или другие интерфейсы, такие как AsCmd TOM, ADOMD.NET. Эти приложения обычно требуется установка вручную hello библиотеки как часть пакета.


## <a name="get-help"></a>Получение справки

#### <a name="documentation"></a>Документация
Azure Analysis Services — простое tooset вверх и toomanage. Вы можете найти все сведения hello, нужно toocreate и управления службами сервера здесь. При создании сервера tooyour toodeploy модели данных, она имеет намного hello таким же как и для создания модели данных развертывается на локальном сервере tooan. В разделе [Analysis Services](https://docs.microsoft.com/sql/analysis-services/analysis-services) доступна обширная библиотека статей с общими и справочными сведениями, инструкциями и руководствами.

#### <a name="videos"></a>Видеоролики
[На сайте Channel 9](https://channel9.msdn.com/series/Azure-Analysis-Services) доступны полезные видео об Azure Analysis Services.

#### <a name="blogs"></a>Блоги
Обновления вносятся очень часто. Всегда можно получить hello последнюю информацию относительно hello [блоге группы разработчиков служб Analysis Services](https://blogs.msdn.microsoft.com/analysisservices/) и [блог Azure](https://azure.microsoft.com/blog/).

#### <a name="community"></a>Сообщество
Уже есть активное сообщество пользователей служб Analysis Services. Беседу hello [форум Azure Analysis Services](https://aka.ms/azureanalysisservicesforum).

## <a name="feedback"></a>Отзыв
У вас есть предложения или идеи касательно функций? Быть tooleave убедиться, что комментарии на [Azure Analysis Services отзыв](https://aka.ms/azureanalysisservicesfeedback).

Есть предложения по документации hello? Можно добавить комментарии, с помощью Livefyre hello нижней части каждой статьи.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда вы знаете, Дополнительные сведения о Azure Analysis Services, пришло время tooget работы. Узнайте, каким образом слишком[создать сервер](analysis-services-create-server.md) в Azure. Когда сервер готов, пошаговое выполнение hello [учебник по Adventure Works](tutorials/aas-adventure-works-tutorial.md) toolearn как toocreate полнофункциональные табличной модели и развернуть ее tooyour сервера.
