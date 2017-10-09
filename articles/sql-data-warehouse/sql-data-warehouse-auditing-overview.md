---
title: "aaaAuditing в хранилище данных SQL Azure | Документы Microsoft"
description: "Приступая к работе с аудитом в хранилище данных SQL Azure"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a>Аудит в хранилище данных SQL Azure
> [!div class="op_single_selector"]
> * [Аудит](sql-data-warehouse-auditing-overview.md)
> * [Обнаружение угроз](sql-data-warehouse-security-threat-detection.md)
> 
> 

Аудит хранилища данных SQL позволяет toorecord события в журнал аудита tooan базы данных в вашей учетной записи хранилища Azure. Аудит может помочь вам соблюсти стандарты, проанализировать работу с базой данных и получить представление о расхождениях и аномалиях, которые могут указывать на бизнес-проблемы или предполагаемые нарушения безопасности. Аудит хранилища данных SQL объединен с Microsoft Power BI для создания подробных отчетов и детального анализа.

Средства аудита включить и упростить соблюдение стандартов toocompliance, но не гарантируют соответствия. Дополнительные сведения о Azure программы, соответствие стандартам поддержки, см. в разделе hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Центр управления безопасностью Azure</a>.

* [Основы аудита баз данных]
* [Настройка аудита базы данных]
* [Анализ журналов и отчетов аудита]

## <a id="subheading-1"></a>Основы аудита баз данных хранилища данных SQL Azure
Аудит базы данных хранилища данных SQL позволяет:

* **Сохранить** журнал аудита выбранных событий. Можно определить категории аудита toobe действия базы данных.
* **Создавать отчеты** по действиям, производимым с базой данных. Можно использовать готовые отчеты и панели мониторинга tooget, быстро начать работу с действия и уведомления о событиях.
* **Анализировать** отчеты. Вы можете искать подозрительные события, необычную деятельность и тенденции.

Вы можете настроить аудит для hello, следующие категории событий:

**Обычный SQL** и **параметризованные SQL** для какой hello журналы аудита, собранные классифицируются как  

* **Toodata доступа**
* **Изменения в схеме данных (DDL)**
* **Изменения данных (DML)**
* **Учетные записи, роли и разрешения (DCL)**
* **Хранимая процедура**, **Вход в систему** и **Управления транзакциями**.

Для каждой категории событий **успешные** и **неуспешные** операции аудита настраиваются отдельно.

Дополнительные сведения о мероприятиях hello и аудит событий см. в разделе hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">ссылка на формат журнала аудита (Загрузка файла doc)</a>.

Журналы аудита хранятся в учетной записи хранения Azure. Срок хранения журнала аудита можно установить.

Политику аудита можно определить для конкретной базы данных или как политику сервера по умолчанию. Политика аудита сервера по умолчанию применяется tooall баз данных на сервере, не имеющих переопределение базы данных аудита определена конкретная политика.

Прежде чем настраивать проверку аудита, убедитесь, что вы используете [клиент прежних версий](sql-data-warehouse-auditing-downlevel-clients.md).

## <a id="subheading-2"></a>Настройка аудита базы данных
1. Запустите hello <a href="https://portal.azure.com" target="_blank">портал Azure</a>.
2. Go toohello **параметры** колонке hello требуется tooaudit хранилище данных SQL. В hello **параметры** колонке выберите **обнаружения аудита и угрозы**.
   
    ![][1]
3. Затем включите аудит, щелкнув hello **ON** кнопки.
   
    ![][3]
4. В hello аудит колонке конфигурации, выберите **сведения о ХРАНИЛИЩЕ** tooopen hello хранения журналов аудита колонку. Выберите учетную запись хранилища Azure, где будут сохраняться журналы hello и hello срока хранения. 
>[!TIP]
>Hello используйте учетную запись хранения для всех hello tooget аудита баз данных, наиболее эффективно использовать hello готовые отчеты шаблонов.
   
    ![][4]
5. Нажмите кнопку hello **ОК** кнопку toosave hello хранения сведений конфигурации.
6. В разделе **Ведение ЖУРНАЛА СОБЫТИЙ,**, нажмите кнопку **успех** и **СБОЯ** toolog все события или выберите отдельных категорий событий.
7. При настройке аудита для базы данных может потребоваться строка подключения hello tooalter вашей tooensure клиента, которые правильно захвачены данные аудита. Проверьте hello [изменить FDQN сервера в строке подключения hello](sql-data-warehouse-auditing-downlevel-clients.md) разделе для подключения клиентов нижнего уровня.
8. Нажмите кнопку **ОК**.

## <a id="subheading-3"></a>Анализ журналов и отчетов аудита
Журналы аудита объединяются в коллекции таблиц хранилища с **SQLDBAuditLogs** префикс в hello учетной записи хранилища Azure, которые были выбраны во время установки. Просматривать файлы журнала можно с помощью таких инструментов, как <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">обозреватель хранилищ Azure</a>.

Шаблон отчета предварительно настроенных панель мониторинга доступна как <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">электронная таблица Excel</a> toohelp быстрого анализа данных журнала. шаблон hello toouse на журналов аудита, требуются Excel 2013 или более поздней версии и Power Query, который можно загрузить <a href="http://www.microsoft.com/download/details.aspx?id=39379">здесь</a>.

шаблон Hello имеет вымышленной образец данных в нем, и можно настроить tooimport Power Query журнал аудита непосредственно из вашей учетной записи хранилища Azure.

## <a id="subheading-4"></a>Повторное создание ключа к хранилищу данных
В рабочей среде, скорее всего, toorefresh хранилища ключей периодически. При обновлении ключей, вы должны toosave hello политики. Hello процесс выглядит следующим образом:

1. В hello аудит колонке конфигурации (описано выше в программе установки hello аудита раздела) переключение hello **ключ доступа к хранилищу** из *основной* слишком*получателя* и  **Сохранить**.

   ![][4]
2. Колонку настройки хранилища перейдите toohello и **повторно создать** hello *первичный ключ доступа*.
3. Вернитесь к предыдущему окну toohello аудит колонке конфигурации коммутатора hello **ключ доступа к хранилищу** из *получателя* слишком*основной* и нажмите клавишу **Сохранить**.
4. Вернитесь к предыдущему окну хранилища toohello пользовательского интерфейса и **повторно создать** hello *вторичный ключ доступа* (при подготовке к hello Далее ключи цикл обновления.

## <a id="subheading-5"></a>Автоматизация (PowerShell или REST API)
Также можно настроить аудит в хранилище данных SQL Azure с помощью следующих средств автоматизации hello.

* **Командлеты PowerShell**

   * [Get-AzureRMSqlDatabaseAuditingPolicy][101]
   * [Get-AzureRMSqlServerAuditingPolicy][102]
   * [Remove-AzureRMSqlDatabaseAuditing][103]
   * [Remove-AzureRMSqlServerAuditing][104]
   * [Set-AzureRMSqlDatabaseAuditingPolicy][105]
   * [Set-AzureRMSqlServerAuditingPolicy][106]
   * [Use-AzureRMSqlServerAuditingPolicy][107]

<!--Anchors-->
[Основы аудита баз данных]: #subheading-1
[Настройка аудита базы данных]: #subheading-2
[Анализ журналов и отчетов аудита]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy