---
title: "Средство оценки решения аналитики aaaCortana | Документы Microsoft"
description: "Партнеры Майкрософт вот все hello шаги, которые toofollow toopublish tooAppSource решение вашей Cortana аналитики."
services: machine-learning
documentationcenter: 
author: AnupamMicrosoft
manager: jhubbard
editor: cgronlun
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: anupams;v-bruham;garye
ms.openlocfilehash: 76cde4e2090c121683b7026f3d80f90f64566607
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="cortana-intelligence-solution-evaluation-tool"></a>Средство оценки решений Cortana Intelligence
## <a name="overview"></a>Обзор
Можно использовать hello tooassess средство оценки решения аналитики Cortana решениях расширенной аналитики на соответствие рекомендациям Майкрософт. Корпорация Майкрософт считает сообщаем toowork со своими партнерами (независимые поставщики программного обеспечения и SIs) tooprovide высококачественных решений для заказчиков, торговых посредников и реализации. В этом руководстве будет Пройдите hello процесс использования средства оценки решения hello вместе с вашим решением и описывают hello конкретные рекомендации в проверки.

## <a name="getting-started"></a>Приступая к работе
Проверьте [загрузки](https://aka.ms/aa-evaluation-tool-download) и установить средства оценки решения аналитики Cortana hello.

Предварительные требования:
- Windows 10: [официальный сайт Windows 10](https://www.microsoft.com/en-us/windows);
- Azure Powershell: [Install and configure Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0) (Установка и настройка Azure PowerShell).

## <a name="identifying-your-app"></a>Определение приложения
После завершения установки откройте средство hello и перед началом первого знакомства с.

![Открытие средства оценки](./media/cortana-intelligence-appsource-evaluation-tool/1-open-evaluation-tool.png)

Укажите идентификационные сведения о решении.

![Подключение к подписке Azure](./media/cortana-intelligence-appsource-evaluation-tool/2-connect-azure-subscription.png)

Подключите tooyour подписки Azure и укажите группу ресурсов, содержащую приложение hello.

![Выбор ресурсов](./media/cortana-intelligence-appsource-evaluation-tool/3-select-resources.png)

После загрузки группы ресурсов hello выберите hello ресурсы, которые включены в решение и определить доступность hello все ресурсы данных, либо как:
- Прием
- Потребление
- Внутренний

Мы используем эти сведения toobetter понимать, как решение использует различные компоненты и компоненты пользовательского интерфейса tooensure согласованы с рекомендациями.

### <a name="ingestion"></a>Прием
В этом случае приема означает источников данных, используемых toopull в данных из внешних hello решения или что все службы вне решения hello использовать toopush данные в него.

### <a name="consumption"></a>Потребление
В этом случае потребление означает все наборы данных, которые пользователи tooend данных используется toopush, прямо или косвенно. Например:
- Наборы данных, используемые в прямых запросах из Power BI.
- Наборы данных, запрашиваемые в веб-приложениях.

>[!NOTE]
Если для приема и потребления используется конкретный ресурс, выберите **Потребление**.

### <a name="internal"></a>Внутренний
Укажите все внутренние ресурсы данных, которые используются только при обработке внутри приложения.

Далее будет запрашиваемые tooprovide действительные учетные данные для всех баз данных, указанное в предыдущем шаге hello:

![Настройка необходимых условий для теста](./media/cortana-intelligence-appsource-evaluation-tool/4-set-test-prerequisites.png)

## <a name="solution-test-cases"></a>Тестовые случаи приложений
Hello решения средство выполнит набор автоматических тестов в решении.

![Выполнение набора тестов](./media/cortana-intelligence-appsource-evaluation-tool/5-set-test-execution.png)

После завершения тестов hello, будет задаваемые tooprovide объяснение или обоснование почему решения отвечает требованию hello.

![Предоставление коммерческого обоснования](./media/cortana-intelligence-appsource-evaluation-tool/6-provide-business-justification.png)

Например если решение публикует tooAzure хранилища данных SQL, вычисления hello тестов требуется tooalso вы опубликовать tooAzure Analysis Services. 

Решение может использовать виртуальные машины IaaS под управлением SQL Server Analysis Services вместо Azure Analysis Services. Это может быть приемлемым причину сбоя теста hello.
## <a name="packaging-your-evaluation-results"></a>Упаковка результатов оценки
После завершения hello тестовые случаи, оценки пакета будет tooa экспортируемый ZIP-файл и будет выведено tooprovide отзывы на средства оценки hello. 

Требуется этот тест приводит к ZIP-файл с корпорацией Майкрософт для вашего решения toobe, вычисляется перед получением toobe утверждения добавлены tooshare tooAppSource

![Градация средства оценки](./media/cortana-intelligence-appsource-evaluation-tool/7-grade-evaluation-tool.png)

Над разделом это статье рассматриваются различные возможности средства hello, теперь давайте рассмотрим типы рекомендаций, это средство оценивает.

## <a name="security-evaluation-considerations"></a>Рекомендации по оценке безопасности
### <a name="databases-should-use-azure-active-directory-authentication"></a>Базы данных должны использовать проверку подлинности Azure Active Directory
Все ресурсы Azure SQL или хранилища данных SQL Azure в hello sloution должна быть включена с помощью проверки подлинности Azure Active Directory (AAD). AAD предоставляет toomanage единое место, все удостоверения и ролей.

| Дополнительные сведения | Статья |
| --- | --- |
| AAD с базой данных SQL Azure и хранилищем данных SQL | [Использование аутентификации Azure Active Directory для аутентификации с помощью базы данных SQL или хранилища данных SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication) |
| Настройка и управление AAD | [Настройка аутентификации Azure Active Directory и управление ею с использованием базы данных SQL или хранилища данных SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication-configure) |
| Проверки подлинности веб-приложений Azure | [Проверка подлинности и авторизация в службе приложений Azure](https://docs.microsoft.com/en-us/azure/app-service/app-service-authentication-overview) |
| Настройка веб-приложений с помощью AAD | [Как tooconfigure вход Azure Active Directory toouse приложения служб приложений](https://docs.microsoft.com/en-us/azure/app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication)|

### <a name="datasets-accessible-tooend-users-should-support-role-based-access-control"></a>Наборы данных доступны tooend — пользователи должны поддерживать управление доступом на основе ролей
Во время выполнения средства оценки hello, появится запрос toospecify отчеты или публикации ресурсов. Предполагается, что эти ресурсы предназначены для использования пользователями, а не разработчиками. Эти ресурсы должны быть обеспечивают управление доступом на основе ролей (RBAC) в порядке tooensure, конечные пользователи являются только может tooaccess полномочным данных.

В частности любой из hello следующие ресурсы Azure можно настроить с помощью RBAC и считаются приемлемыми:
- Защита HDInsight см. в разделе [безопасности tooHadoop Знакомство с кластерами HDInsight на присоединенных к домену](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-domain-joined-introduction)
- Общие сведения об Azure SQL см. в статье [Использование аутентификации Azure Active Directory для аутентификации с помощью базы данных SQL или хранилища данных SQL]( https://docs.microsoft.com/en-us/azure/sql-database/sql-database-aad-authentication).
- Общие сведения о службах Azure Analysis Services см. в статье [Manage database roles and users](https://docs.microsoft.com/azure/analysis-services/analysis-services-database-users) (Управление ролями баз данных и пользователями).
- Хранилище данных SQL Azure (так как хранилище данных SQL поддерживает RBAC, мы не рекомендуем предоставлять к нему доступ пользователям).

Если вы используете другой тип ресурса, поддерживающий RBAC, укажите, в тестовый случай обоснование hello.

### <a name="azure-data-lake-store-should-use-at-rest-encryption"></a>Для Azure Data Lake Store следует использовать шифрование неактивных данных
Azure Data Lake Store (ADLS) по умолчанию поддерживает шифрование неактивных данных с помощью ключей шифрования, под управлением ADLS. Шифрование также можно настроить с использованием Azure Key Vault.

Дополнительные сведения об указании параметров шифрования ADLS см. в разделе [Создание учетной записи хранения озера данных Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-get-started-portal#create-an-azure-data-lake-store-account).

### <a name="azure-sql-and-azure-sql-data-warehouse-should-use-encryption"></a>В Azure SQL и в хранилище данных SQL Azure следует использовать шифрование
Azure SQL и хранилище данных SQL Azure поддерживают прозрачное шифрование данных (TDE), обеспечивающее шифрование и расшифровку данных и файлов журналов в реальном времени.

| Дополнительные сведения | Статья |
| --- | --- |
| Прозрачное шифрование данных (TDE) | [Transparent Data Encryption (Прозрачное шифрование данных)](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-tde) |
| Хранилище данных Azure SQL с прозрачным шифрованием данных | [Начало работы с прозрачным шифрованием данных (TDE)](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-encryption-tde-tsql) |
| Настройка Azure SQL с прозрачным шифрованием данных | [Прозрачное шифрование данных в Базе данных SQL Azure](https://docs.microsoft.com/en-us/sql/relational-databases/security/encryption/transparent-data-encryption-with-azure-sql-database) |
| Настройка SQL Azure с шифрованием Always Encrypted | [Always Encrypted: защита конфиденциальных данных в Базе данных SQL и хранение ключей шифрования в хранилище ключей Azure](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-always-encrypted-azure-key-vault)|

Кроме tooTDE Azure SQL также поддерживает постоянное шифрование, новая технология шифрования данных, что гарантирует, что данные шифруются не только на rest и во время перемещения между клиентом и сервером, но при данных используется при выполнении команды на сервере hello.

### <a name="any-virtual-machines-must-be-deployed-from-hello-azure-marketplace"></a>Все виртуальные машины должны быть развернуты из hello Azure Marketplace
В порядке tooprovide приемлемый уровень безопасности по AppSource требует, что все виртуальные машины, развернутые как часть решения аналитики Cortana быть Сертифицировано и опубликована на hello Azure Marketplace.

toosearch hello текущий список образов Azure Marketplace в разделе [Microsoft Azure Marketplace](https://azuremarketplace.microsoft.com/en-us/marketplace/apps/category/compute).

Сведения о том, как toopublish образ виртуальной машины для Azure Marketplace см. в разделе [toocreate руководство образ виртуальной машины для hello Azure Marketplace](https://docs.microsoft.com/en-us/azure/marketplace-publishing/marketplace-publishing-vm-image-creation).

## <a name="scalability-evaluation-considerations"></a>Рекомендации по оценке масштабируемости
### <a name="cortana-intelligence-solutions-should-include-a-scalable-big-data-platform"></a>Решения Cortana Intelligence должны содержать масштабируемую платформу для больших данных
Решения аналитики Cortana следует использовать масштабирование toovery данные большого размера. В Azure это означает, что они должны включать одну из двух петабайт масштаб данных для hello платформ:
- Хранилище озера данных Azure
- Хранилище данных SQL Azure

Если решение не требуется поддержка этих размеров данных или при использовании платформу альтернативных данных опишите это в обоснование hello тестового случая.
### <a name="cortana-intelligence-solutions-should-include-dedicated-ingestion-data-environments"></a>Решения Cortana Intelligence должны содержать выделенные среды приема данных
Решения Cortana Intelligence не должны непосредственно вставлять данные в реляционные источники данных. Вместо этого необработанные данные должны храниться в неструктурированной среде с идемпотентными вставками или обновлениями в любом реляционном хранилище с помощью фабрики данных Azure.

Дополнительные сведения о копировании данных с помощью фабрики данных Azure см. в статье [Руководство. Создание конвейера с действием копирования с помощью Visual Studio](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-copy-activity-tutorial-using-visual-studio).

### <a name="azure-sql-data-warehouse-should-use-polybase-for-data-ingestion"></a>В хранилище данных SQL Azure для приема данных следует использовать PolyBase
Хранилище данных SQL поддерживает PolyBase для параллельного приема данных с высоким уровнем масштабируемости. PolyBase позволяет toouse хранилища данных SQL Azure tooissue запросы внешних наборов данных, хранящихся в хранилище больших двоичных объектов Azure или хранилища Озера данных Azure. Это обеспечивает высокую производительность tooalternative методов массового обновления.

Инструкции по началу работы с PolyBase и хранилищем данных SQL Azure см. в статье [Загрузка данных в хранилище данных SQL с помощью PolyBase](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-get-started-load-with-polybase).

Рекомендации по работе с PolyBase и хранилищем данных SQL Azure см. в статье [Руководство по использованию PolyBase в хранилище данных SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-load-polybase-guide).

## <a name="availability-evaluation-considerations"></a>Рекомендации по оценке доступности

### <a name="datasets-accessible-tooend-users-should-support-a-large-volume-of-concurrent-users"></a>Пользователям доступны tooend наборы данных должны поддерживать большое количество одновременных пользователей
Во время выполнения средства оценки hello, появится запрос toospecify отчеты или публикации ресурсов. Предполагается, что эти ресурсы предназначены для использования пользователями, а не разработчиками. Эти ресурсы должны поддерживать от среднего до большого количества одновременных пользователей.

В частности хранилище данных SQL Azure не должно быть hello единственным данных источника tooend доступных пользователей. Если хранилища данных SQL Azure предоставляется в качестве ресурса для опытных пользователей, Azure Analysis Services должны быть сделаны доступными tootypical пользователей.

Дополнительные сведения об ограничениях параллелизма хранилища данных SQL Azure см. в статье [Управление параллелизмом и рабочей нагрузкой в хранилище данных SQL](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-develop-concurrency).

Дополнительные сведения о службах Analysis Services Azure см. в статье [Службы Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-overview).

### <a name="azure-sql-resources-should-have-a-read-only-replica-for-failover"></a>Для отработки отказа ресурсы SQL Azure должны иметь реплику только для чтения
Базы данных SQL Azure поддерживают георепликацию tooa второй экземпляр. Этот экземпляр можно как отработки отказа экземпляр tooprovide высокий уровень доступности приложения.

Дополнительные сведения о георепликации в базе данных SQL Azure см. в статье [Обзор. Группы отработки отказа и активная георепликация](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-overview).

Дополнительные сведения о tooconfigure географическую репликацию данных Azure SQL в разделе [Настройка активной георепликации для базы данных SQL Azure с помощью Transact-SQL](https://docs.microsoft.com/en-us/azure/sql-database/sql-database-geo-replication-transact-sql).

### <a name="azure-sql-data-warehouse-should-have-geo-redundant-backups-enabled"></a>В хранилище данных SQL Azure необходимо включить геоизбыточное резервное копирование
Хранилища данных SQL поддерживает toogeo избыточного хранилища ежедневных резервных копий. Географическая репликация гарантирует, что вы можете восстановить hello хранилище данных даже в ситуациях, где не может получить доступ к моментальных снимков, хранящихся в основном регионе. Эта функция включена по умолчанию и не должна отключаться в решениях Cortana Intelligence.

Дополнительные сведения о резервных копиях и восстановлении хранилища данных SQL Azure см. в [этой статье ](https://docs.microsoft.com/en-us/azure/sql-data-warehouse/sql-data-warehouse-backups).

### <a name="virtual-machines-should-be-configured-with-availability-sets"></a>Виртуальные машины необходимо настроить с помощью групп доступности
Виртуальные машины Azure должны быть настроены в группах доступности в порядке toominimize hello воздействие обслуживания запланированных и незапланированных событий.

Дополнительные сведения о доступности виртуальной машины Azure см. в разделе [управлять доступностью hello виртуальных машинах в Azure](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/manage-availability).

## <a name="other-evaluation-considerations"></a>Рекомендации по другим оценкам
### <a name="cortana-intelligence-apps-should-use-a-centralized-tool-for-data-orchestration"></a>Приложения Cortana Intelligence должны использовать централизованное средство для оркестрации данных
Использование одного средства для планирования перемещения и преобразования данных, а также для управления этими процессами обеспечивает согласованность критически важных данных. Это обеспечивает четкую логику при управлении зависимостями, логику повторных попыток, предупреждения и ведения журнала и т. д. Рекомендуется использовать hello [фабрики данных Azure](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-introduction) для данных orchestration в Azure.

Если для оркестрации данных используется средство, отличное от фабрики данных Azure, опишите, какие именно средства вы используете.
### <a name="azure-machine-learning-models-should-be-retrained-using-azure-data-factory"></a>Переобучение моделей машинного обучения Azure следует выполнять с помощью фабрики данных Azure
Azure машинного обучения (AzureML) предоставляет средства easy toouse для hello Создание и развертывание прогнозирующее моделирование и машинное обучение конвейеров. Тем не менее важно рабочих развертываний этих моделей AzureML не зависит от одного основного набора данных, что вместо адаптирует toohello сдвиг dynamics реальных явлений.

Дополнительные сведения о создании переобучаемых веб-служб в AzureML см. в статье [Программное переобучение моделей машинного обучения](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-retrain-models-programmatically).

Дополнительные сведения об автоматизации процесса обучения модели hello, с помощью фабрики данных Azure см. в разделе [моделей обновления машинного обучения Azure, с помощью действия ресурса обновления](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-azure-ml-update-resource-activity).

## <a name="existing-documentation"></a>Имеющаяся документация
[Microsoft Azure Certified toogrow бизнеса облака](https://azure.microsoft.com/en-us/marketplace/programs/certified/)

[Сертификация Microsoft Azure: Cortana Intelligence](https://azure.microsoft.com/en-us/marketplace/programs/certified/cortana/)

