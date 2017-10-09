---
title: "Служба разделения слияния aaaDeploy | Документы Microsoft"
description: "Разбиение и объединение с помощью инструментов эластичной базы данных"
services: sql-database
documentationcenter: 
author: ddove
manager: jhubbard
editor: 
ms.assetid: 9a993c0f-7052-46cd-aa59-073bea8d535a
ms.service: sql-database
ms.custom: scale out apps
ms.workload: sql-database
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: ddove
ms.openlocfilehash: 6fef641cbc1e73ce34a851c53298a072dade8f9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-split-merge-service"></a>Развертывание службы разбиения и объединения
средство разделения слияния Hello позволяет перемещать данные между сегментированных баз данных. См. статью [Перемещение данных между масштабируемыми облачными базами данных](sql-database-elastic-scale-overview-split-and-merge.md).

## <a name="download-hello-split-merge-packages"></a>Загрузить пакеты разделения слияния hello
1. Загрузка последней версии NuGet hello из [NuGet](http://docs.nuget.org/docs/start-here/installing-nuget).
2. Откройте командную строку и перейдите в каталог toohello, который вы загрузили nuget.exe. Hello загружаемый файл содержит PowerShell commmands.
3. Загрузите последнюю версию пакета разделения слияния hello в текущий каталог hello с hello ниже команду:
   ```
   nuget install Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge
   ```  

Hello файлы помещаются в каталог с именем **Microsoft.Azure.SqlDatabase.ElasticScale.Service.SplitMerge.x.x.xxx.x** где *x.x.xxx.x* отражает hello номер версии. Поиск файлов служба разделения слияния hello в hello **content\splitmerge\service** вложенный каталог и hello сценариев PowerShell разделения слияния (и необходимые клиентских библиотек) в hello **content\splitmerge\powershell** вложенный каталог.

## <a name="prerequisites"></a>Предварительные требования
1. Создание базы данных база данных SQL Azure, будет использоваться в качестве базы данных состояние разделения слияния hello. Go toohello [портал Azure](https://portal.azure.com). Создайте новую **Базу данных SQL**. Имя базы данных hello и создания нового администратора и пароль. Быть убедиться, что toorecord hello имя и пароль для последующего использования.
2. Убедитесь, что сервер базы данных SQL Azure позволяет tooit tooconnect служб Azure. В hello hello портале **параметры брандмауэра**, убедитесь, что hello **разрешить доступ службы tooAzure** установлено слишком**на**. Щелкните hello значок «Сохранить».
   
   ![Допустимые службы][1]
3. Создайте учетную запись хранения Azure, которая будет использоваться для вывода диагностических данных. Go toohello портала Azure. Hello левой панели щелкните **New**, нажмите кнопку **данные + хранилище**, затем **хранения**.
4. Создайте облачную службу Azure для размещения службы разбиения и объединения.  Go toohello портала Azure. Hello левой панели щелкните **New**, затем **вычислений**, **облачной службы**, и **создать**. 

## <a name="configure-your-split-merge-service"></a>Настройка службы разбиения и объединения
### <a name="split-merge-service-configuration"></a>Настройка службы разбиения и объединения
1. В папке hello, куда вы загрузили сборки hello разделения слияния создайте копию hello **ServiceConfiguration.Template.cscfg** файл, который входит в состав **SplitMergeService.cspkg** и переименуйте его в **ServiceConfiguration.cscfg**.
2. Откройте **ServiceConfiguration.cscfg** в текстовом редакторе, например Visual Studio, которая проверяет входные данные, такие как формат hello отпечатки сертификата.
3. Создать новую базу данных или выберите существующий tooserve базы данных в качестве базы данных состояние hello операции разделения слияния и получения строки соединения hello этой базы данных. 
   
   > [!IMPORTANT]
   > В настоящее время базы данных состояние hello необходимо использовать параметры сортировки Latin hello (SQL\_Latin1\_Общие\_CP1\_CI\_AS). Дополнительные сведения см. в статье [Имя параметров сортировки Windows (Transact-SQL)](https://msdn.microsoft.com/library/ms188046.aspx).
   >

   С базу данных SQL Azure строка подключения hello обычно имеет форму hello:
      ```
      Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
      ```

4. Введите эту строку подключения в файле cscfg hello в обоих hello **SplitMergeWeb** и **SplitMergeWorker** роли подразделы ElasticScaleMetadata приветствия.
5. Для hello **SplitMergeWorker** роли, введите допустимое соединение хранилища tooAzure строку hello **WorkerRoleSynchronizationStorageAccountConnectionString** параметр.

### <a name="configure-security"></a>Настройка безопасности
Подробные инструкции tooconfigure hello безопасность службы hello, см. в разделе toohello [конфигурация безопасности разделения слияния](sql-database-elastic-scale-split-merge-security-configuration.md).

Hello целях простое тестовое развертывание для этого учебника минимальный набор конфигурации, шаги будут выполнены tooget hello служба создана и запущена. Следующие действия включить только hello одного компьютера или учетной записи выполнение их toocommunicate со службой hello.

### <a name="create-a-self-signed-certificate"></a>Создание самозаверяющего сертификата
Создать новый каталог и из следующие команды с помощью execute hello этот каталог система [Командная строка разработчика для Visual Studio](http://msdn.microsoft.com/library/ms229859.aspx) окна:

   ```
    makecert ^
    -n "CN=*.cloudapp.net" ^
    -r -cy end -sky exchange -eku "1.3.6.1.5.5.7.3.1,1.3.6.1.5.5.7.3.2" ^
    -a sha1 -len 2048 ^
    -sr currentuser -ss root ^
    -sv MyCert.pvk MyCert.cer
   ```

Предлагается ввести пароль tooprotect hello закрытый ключ. Введите надежный пароль и подтвердите его. Затем запрашивается hello toobe пароль, используемый еще раз после этого. Нажмите кнопку **Да** в конец tooimport hello его toohello хранилище доверенных корневых центров сертификации.

### <a name="create-a-pfx-file"></a>Создание PFX-файла
Выполните следующую команду из hello hello же окно, в котором был выполнен makecert; Используйте hello пароль можно использовать toocreate hello сертификата:

    pvk2pfx -pvk MyCert.pvk -spc MyCert.cer -pfx MyCert.pfx -pi <password>

### <a name="import-hello-client-certificate-into-hello-personal-store"></a>Импортируйте сертификат клиента hello в личном хранилище hello
1. В проводнике Windows дважды щелкните **MyCert.pfx**.
2. В hello **мастер импорта сертификатов** выберите **текущего пользователя** и нажмите кнопку **Далее**.
3. Проверьте путь к файлу hello и нажмите кнопку **Далее**.
4. Введите пароль hello, оставьте **включают все расширенные свойства** этот флажок установлен и нажмите кнопку **Далее**.
5. Оставьте **hello автоматически выбрать хранилище сертификатов [...]**  этот флажок установлен и нажмите кнопку **Далее**.
6. Нажмите кнопки **Готово** и **ОК**.

### <a name="upload-hello-pfx-file-toohello-cloud-service"></a>Отправка hello PFX файл toohello облачной службы
1. Go toohello [портала Azure](https://portal.azure.com).
2. Выберите **Облачные службы**.
3. Выберите облачную службу hello, созданной выше для hello служба разделения или слияния.
4. Нажмите кнопку **сертификаты** hello верхнем меню.
5. Нажмите кнопку **отправить** hello нижней панели.
6. Выберите файл PFX hello и введите hello того же пароля.
7. После завершения копирования hello отпечаток сертификата из hello новую запись в списке hello.

### <a name="update-hello-service-configuration-file"></a>Обновить файл конфигурации службы hello
Вставьте отпечаток сертификата hello выше копируется hello отпечаток значение атрибута из этих параметров.
Для hello рабочей роли:
   ```
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Для hello веб-роли:

   ```
    <Setting name="AdditionalTrustedRootCertificationAuthorities" value="" />
    <Setting name="AllowedClientCertificateThumbprints" value="" />
    <Setting name="DataEncryptionPrimaryCertificateThumbprint" value="" />
    <Certificate name="SSL" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="CA" thumbprint="" thumbprintAlgorithm="sha1" />
    <Certificate name="DataEncryptionPrimary" thumbprint="" thumbprintAlgorithm="sha1" />
   ```

Обратите внимание, в производственной среде следует использовать отдельные сертификаты для hello ЦС, для шифрования, hello сертификата сервера и клиентских сертификатов. Подробные указания см. в статье [Настройка параметров безопасности для службы разбиения и объединения](sql-database-elastic-scale-split-merge-security-configuration.md).

## <a name="deploy-your-service"></a>Развертывание службы
1. Go toohello [портал Azure](https://manage.windowsazure.com).
2. Нажмите кнопку hello **облачные службы** hello левой части экрана и выберите hello облачной службы, которое было создано ранее.
3. Нажмите на кнопку **Панель мониторинга**.
4. Выберите hello в промежуточной среде, а затем нажмите кнопку **отправить новое промежуточное развертывание**.
   
   ![Промежуточная][3]
5. В диалоговом окне приветствия введите метку развертывания. Для «Пакета» и «Конфигурация» щелкните «Из локальной» и выберите hello **SplitMergeService.cspkg** файла и cscfg-файле ранее.
6. Убедитесь, что флажок hello **развернуть, даже если одна или несколько ролей содержат отдельный экземпляр** проверяется.
7. Нажмите кнопку деления hello в hello нижней правой toobegin hello развертывания. Ожидает ее tootake toocomplete несколько минут.

   ![Отправить][4]

## <a name="troubleshoot-hello-deployment"></a>Устранение неполадок развертывания hello
Веб-роли в случае toocome сети, существует вероятность проблемы с конфигурацией безопасности hello. Убедитесь, что hello SSL настроен, как описано выше.

Рабочей роли toocome сети, но веб-роли завершается успешно, это скорее проблемы с подключением toohello состояние базы данных, созданный ранее.

* Убедитесь, что строка подключения hello в вашей .cscfg точности.
* Проверьте существование hello сервера и базы данных, и что hello идентификатор пользователя и пароль указаны правильно.
* Для баз данных SQL Azure строка hello подключения должен иметь вид hello:

   ```  
   Server=myservername.database.windows.net; Database=mydatabasename;User ID=myuserID; Password=mypassword; Encrypt=True; Connection Timeout=30
   ```

* Убедитесь, что имя сервера hello не начинается с **https://**.
* Убедитесь, что сервер базы данных SQL Azure позволяет tooit tooconnect служб Azure. toodo это, откройте https://manage.windowsazure.com, щелкните «Базы данных SQL» hello слева, нажмите кнопку «Серверы» в верхнем hello и выберите сервер. Нажмите кнопку **Настройка** в hello top и убедитесь, что hello **служб Azure** установлено слишком «Да». (См. предварительные требования hello раздел hello верхней части этой статьи).

## <a name="test-hello-service-deployment"></a>Тестирование развертывания службы hello
### <a name="connect-with-a-web-browser"></a>Подключение с помощью веб-браузера
Определите hello web конечной точки службы разделения слияния. Его можно найти в hello классический портал Azure с переходом toohello **мониторинга** облачной службы и в разделе **URL-адрес сайта** hello правой стороны. Замените **http://** с **https://** так, как параметры безопасности по умолчанию hello отключить конечную точку hello HTTP. Страница приветствия нагрузки этот URL-адрес в адресную строку браузера.

### <a name="test-with-powershell-scripts"></a>Тестирование с помощью скриптов PowerShell
развертывания Hello и среду можно проверить, запустив hello включены примеры скриптов PowerShell.

Включенные файлы скриптов Hello — это:

1. **SetupSampleSplitMergeEnvironment.ps1** — задает уровень данных тестирования для разбиения и объединения (подробное описание см. в таблице ниже).
2. **ExecuteSampleSplitMerge.ps1** -выполняет операций тестирования, тестовом hello уровня данных (см. таблицу ниже для подробного описания)
3. **GetMappings.ps1** — верхнего уровня образец скрипта, который выводит текущее состояние сопоставления сегментов hello hello.
4. **ShardManagement.psm1** -вспомогательный сценарий, который создает оболочку для hello ShardManagement API
5. **SqlDatabaseHelpers.psm1** — это вспомогательный сценарий для создания баз данных SQL и управления ими.
   
   <table style="width:100%">
     <tr>
       <th>Файл PowerShell</th>
       <th>Действия</th>
     </tr>
     <tr>
       <th rowspan="5">SetupSampleSplitMergeEnvironment.ps1</th>
       <td>1.    Создает базу данных диспетчера сопоставления сегментов.</td>
     </tr>
     <tr>
       <td>2.    Создает 2 сегментированные базы данных.
     </tr>
     <tr>
       <td>3.    Создает сопоставление сегментов для этих баз данных (удаляет любые существующие сопоставления сегментов в этих базах данных). </td>
     </tr>
     <tr>
       <td>4.    Создает небольшой образец таблицы в обоих сегментов hello и заполняет таблицу hello в одном из сегментов hello.</td>
     </tr>
     <tr>
       <td>5.    Объявляет hello SchemaInfo для сегментированной таблицы hello.</td>
     </tr>
   </table>
   <table style="width:100%">
     <tr>
       <th>Файл PowerShell</th>
       <th>Действия</th>
     </tr>
   <tr>
       <th rowspan="4">ExecuteSampleSplitMerge.ps1 </th>
       <td>1.    Отправляет разбиение запроса toohello разделения слияния службы веб-клиента, разбивающего половина данных hello из hello первого сегмента toohello второй сегментов.</td>
     </tr>
     <tr>
       <td>2.    Опрашивает hello веб-клиентом для разбиения состояние запроса и ожидает до завершения запроса hello hello.</td>
     </tr>
     <tr>
       <td>3.    Отправляет слияния запроса toohello разделения слияния службы веб-клиента, который перемещает данные hello из hello второй сегмент задней toohello первого сегмента.</td>
     </tr>
     <tr>
       <td>4.    Веб-клиентом hello опрашивает состояние запроса слияния hello и ожидание завершения запроса hello.</td>
     </tr>
   </table>
   
## <a name="use-powershell-tooverify-your-deployment"></a>Используйте PowerShell tooverify развертывания
1. Открытие нового окна PowerShell и перейдите в каталог toohello, который вы загрузили hello разделения слияния пакет и перейдите в каталог «powershell» hello.
2. Создать сервер базы данных Azure SQL (или выберите существующий сервер) где диспетчера карты сегментов hello и сегменты будут созданы.
   
   > [!NOTE]
   > Hello SetupSampleSplitMergeEnvironment.ps1 скрипт создает эти базы данных на hello того же сервера с простой сценарий hello tookeep по умолчанию. Это не является ограничением для hello служба разделения слияния сам.
   >
   
   Учетные данные проверки подлинности SQL с toohello доступа чтения и записи, баз данных SQL Server необходимо указать для hello данных toomove разделения слияния службы и сопоставление сегментов hello обновления. Поскольку hello разделения слияния служба работает в облаке hello, он не поддерживает встроенную проверку подлинности.
   
   Убедитесь, что сервер Azure SQL hello настроен доступ tooallow из hello IP-адрес компьютера hello, выполнять эти скрипты. Этот параметр в разделе hello Azure SQL server можно найти / configuration / разрешенные IP-адреса.
3. Выполнение образца hello SetupSampleSplitMergeEnvironment.ps1 сценария toocreate hello среды.
   
   Выполнение этого скрипта будет очищают все существующие данные управления карты сегментов структуры в базе данных диспетчера карты сегментов hello и hello сегментов. Полезные toorerun hello скрипт может при желании карта сегментов hello toore инициализации или сегментов.
   
   Пример командной строки:

   ```   
     .\SetupSampleSplitMergeEnvironment.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'
   ```      
4. Выполнение hello Getmappings.ps1 сценария tooview hello сопоставления, которые в настоящий момент находятся в среде образец hello.
   
   ```
     .\GetMappings.ps1 
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net'

   ```         
5. Выполните сценарий tooexecute hello ExecuteSampleSplitMerge.ps1 операции split (перенос hello первого сегмента toohello второй сегмент половины данных hello), а затем операции слияния (hello данных обратное перемещение на первый сегмент hello). Если вы настроили SSL и левой hello конечной точки http отключен, убедитесь, вместо этого используйте конечную точку https:// hello.
   
   Пример командной строки:

   ```   
     .\ExecuteSampleSplitMerge.ps1
   
         -UserName 'mysqluser' 
         -Password 'MySqlPassw0rd' 
         -ShardMapManagerServerName 'abcdefghij.database.windows.net' 
         -SplitMergeServiceEndpoint 'https://mysplitmergeservice.cloudapp.net' 
         -CertificateThumbprint '0123456789abcdef0123456789abcdef01234567'
   ```      
   
   Получив hello ниже ошибка, скорее всего это проблема с сертификатом конечной точки веб. Попробуйте подключиться toohello сетевую конечную точку с избранных веб-браузере и проверьте, существует ли сообщение об ошибке сертификата.
   
     ```
     Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLSsecure channel.
     ```
   
   Если выполнено успешно, hello вывод должен выглядеть как hello ниже:
   
   ```
   > .\ExecuteSampleSplitMerge.ps1 -UserName 'mysqluser' -Password 'MySqlPassw0rd' -ShardMapManagerServerName 'abcdefghij.database.windows.net' -SplitMergeServiceEndpoint 'http://mysplitmergeservice.cloudapp.net' -CertificateThumbprint 0123456789abcdef0123456789abcdef01234567
   > Sending split request
   > Began split operation with id dc68dfa0-e22b-4823-886a-9bdc903c80f3
   > Polling split-merge request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Waiting for reference tables copy     completion.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > Sending merge request
   > Began merge operation with id 6ffc308f-d006-466b-b24e-857242ec5f66
   > Polling request status. Press Ctrl-C tooend
   > Progress: 0% | Status: Queued | Details: [Informational] Queued request
   > Progress: 5% | Status: Starting | Details: [Informational] Starting split-merge state machine for request.
   > Progress: 5% | Status: Starting | Details: [Informational] Performing data consistency checks on target     shards.
   > Progress: 20% | Status: CopyingReferenceTables | Details: [Informational] Moving reference tables from     source tootarget shard.
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Moving key range [100:110) of     Sharded tables
   > Progress: 44% | Status: CopyingShardedTables | Details: [Informational] Successfully copied key range     [100:110) for table [dbo].[MyShardedTable]
   > ...
   > ...
   > Progress: 90% | Status: Completing | Details: [Informational] Successfully deleted shardlets in table     [dbo].[MyShardedTable].
   > Progress: 90% | Status: Completing | Details: [Informational] Deleting any temp tables that were created     while processing hello request.
   > Progress: 100% | Status: Succeeded | Details: [Informational] Successfully processed request.
   > 
   ```
6. Поэкспериментируйте с другими типами данных! Все эти сценарии принимают дополнительный параметр - ShardKeyType, который позволяет вам тип ключа toospecify hello. по умолчанию Hello Int32, но можно также указать Int64, Guid или двоичный.

## <a name="create-requests"></a>Создание запросов
Hello службы можно с помощью веб-hello пользовательского интерфейса или путем импорта и с помощью модуля SplitMerge.psm1 PowerShell hello, который будет отправлять запросы через hello веб-роли.

Hello службы можно переместить данные в таблицах сегментированных и ссылочных таблиц. Сегментированная таблица содержит ключевой столбец сегментирования и различные строчные данные в каждом сегменте. Ссылочная таблица не сегментированных, он содержит hello же строки данных на каждый сегмент. Ссылочные таблицы полезны для часто не изменяется и используется tooJOIN с сегментированными таблицами в запросах данных.

Tooperform порядок разбиения слияние необходимо объявить сегментированными таблицами hello и ссылочные таблицы, которые нужно переместить toohave. Это осуществляется с помощью hello **SchemaInfo** API. Этот API является в hello **Microsoft.Azure.SqlDatabase.ElasticScale.ShardManagement.Schema** пространства имен.

1. Создайте для каждой сегментированной таблицы **ShardedTableInfo** объект, описывающий имя схемы таблицы hello родительского (необязательно, по умолчанию слишком «dbo»), hello имя таблицы и имя столбца в таблицы, который содержит ключ сегментирования hello hello.
2. Создайте для каждой таблицы ссылок **ReferenceTableInfo** описывающие имя схемы таблицы hello родительского объекта (необязательно, по умолчанию слишком «dbo») и имя таблицы hello.
3. Добавить hello выше новый tooa объектов TableInfo **SchemaInfo** объекта.
4. Получить tooa ссылку **ShardMapManager** и вызовите **GetSchemaInfoCollection**.
5. Добавить hello **SchemaInfo** toohello **SchemaInfoCollection**, указав имя сопоставления сегментов hello.

Примером этого может отображаться в hello SetupSampleSplitMergeEnvironment.ps1 сценария.

Hello разделения слияния службы не создать целевую базу данных hello (или схемы для всех таблиц в базе данных hello). Они должны быть предварительно созданы перед отправкой запроса на обслуживание toohello.

## <a name="troubleshooting"></a>Устранение неполадок
Может появиться hello следующее сообщение при выполнении скриптов powershell образец hello:

   ```
   Invoke-WebRequest : hello underlying connection was closed: Could not establish trust relationship for hello SSL/TLS secure channel.
   ```

Эта ошибка означает, что SSL-сертификат настроен неправильно. Следуйте инструкциям раздела, hello «Соединения с использованием веб-браузер».

Если не удается отправить запросы, может появиться такое сообщения:

```
[Exception] System.Data.SqlClient.SqlException (0x80131904): Could not find stored procedure 'dbo.InsertRequest'. 
```

В этом случае проверьте файл конфигурации, в определенной приветствия для **WorkerRoleSynchronizationStorageAccountConnectionString**. Эта ошибка обычно означает, что рабочая роль, hello не удалось инициализировать успешно hello базы данных метаданных при первом использовании. 

[!INCLUDE [elastic-scale-include](../../includes/elastic-scale-include.md)]

<!--Image references-->
[1]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/allowed-services.png
[2]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/manage.png
[3]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/staging.png
[4]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/upload.png
[5]: ./media/sql-database-elastic-scale-configure-deploy-split-and-merge/storage.png

