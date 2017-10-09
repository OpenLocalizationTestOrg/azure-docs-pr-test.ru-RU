---
title: "Always Encrypted: База данных SQL и Azure Key Vault | Документация Майкрософт"
description: "В этой статье показано, как toosecure конфиденциальных данных в базе данных SQL с использованием шифрования данных hello мастер постоянного шифрования в SQL Server Management Studio. Оно также содержит инструкции, которые будет показано, как toostore каждый ключ шифрования в хранилище ключей Azure."
keywords: "шифрование данных, ключ шифрования, шифрование в облаке"
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: cgronlun
ms.assetid: 6ca16644-5969-497b-a413-d28c3b835c9b
ms.service: sql-database
ms.custom: security
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/06/2017
ms.author: sstein
ms.openlocfilehash: 8226bfef584e979643f5bb0747d4df16569f8204
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="always-encrypted-protect-sensitive-data-in-sql-database-and-store-your-encryption-keys-in-azure-key-vault"></a>Always Encrypted: защита конфиденциальных данных в Базе данных SQL и хранение ключей шифрования в хранилище ключей Azure

В этой статье показано, как базы данных с помощью шифрования данных с помощью hello toosecure конфиденциальных данных в SQL [мастер постоянного шифрования](https://msdn.microsoft.com/library/mt459280.aspx) в [SQL Server Management Studio (SSMS)](https://msdn.microsoft.com/library/hh213248.aspx). Оно также содержит инструкции, которые будет показано, как toostore каждый ключ шифрования в хранилище ключей Azure.

Всегда шифрование — это новая технология шифрования данных в базе данных SQL Azure и SQL Server, который помогает защитить конфиденциальные данные хранятся на сервере hello во время перемещения между клиентом и сервером, а также hello данных во время использования. Всегда шифрование гарантирует, конфиденциальные данные никогда не отображается как обычный текст внутри hello системы базы данных. После настройки шифрования данных только для клиентских приложений или серверов приложений, которые имеют toohello клавиши доступа можно доступ к данным открытым текстом. Дополнительные сведения см. в статье [Always Encrypted (ядро СУБД)](https://msdn.microsoft.com/library/mt163865.aspx).

После настройки базы данных toouse hello, постоянное шифрование, вы создадите клиентское приложение на C# с toowork Visual Studio с hello зашифрованные данные.

Выполните действия hello в этой статье и узнайте, как tooset копирование постоянного шифрования для базы данных Azure SQL. В этой статье вы узнаете, как hello tooperform следующие задачи:

* Мастер постоянного шифрования используйте hello в SSMS toocreate [ключей постоянного шифрования](https://msdn.microsoft.com/library/mt163865.aspx#Anchor_3).
  * Создавать [главный ключ столбца (CMK)](https://msdn.microsoft.com/library/mt146393.aspx).
  * Создавать [ключ шифрования столбца (CEK)](https://msdn.microsoft.com/library/mt146372.aspx).
* Создавать таблицу базы данных и шифровать столбцы.
* Создание приложения, которое вставляет, выбирает и отображает данные из столбцов шифрования hello.

## <a name="prerequisites"></a>Предварительные требования
Для работы с этим руководством вам потребуется:

* Учетная запись и подписка Azure. Если у вас ее нет, зарегистрируйтесь, чтобы [воспользоваться бесплатной пробной версией](https://azure.microsoft.com/pricing/free-trial/).
* [SQL Server Management Studio](https://msdn.microsoft.com/library/mt238290.aspx) версии 13.0.700.242 или более поздней версии.
* [.NET framework 4.6](https://msdn.microsoft.com/library/w0x726c2.aspx) или более поздней версии (на компьютере клиента hello).
* [Visual Studio](https://www.visualstudio.com/downloads/download-visual-studio-vs.aspx)
* [Azure PowerShell](/powershell/azure/overview) 1.0.0 или более поздней версии. Тип **(Get-Module azure - ListAvailable). Версия** toosee управлением какой версии PowerShell.

## <a name="enable-your-client-application-tooaccess-hello-sql-database-service"></a>Включить службы клиентского приложения tooaccess hello базы данных SQL
Необходимо включить службы клиентского приложения tooaccess hello базы данных SQL, настроив hello обязательную проверку подлинности и получении hello *ClientId* и *секрет* потребуется tooauthenticate приложение hello, следующий код.

1. Откройте hello [классический портал Azure](http://manage.windowsazure.com).
2. Выберите **Active Directory** и щелкните экземпляр Active Directory hello, приложение будет использовать.
3. Щелкните **Приложения**, а затем — **Добавить**.
4. Введите имя для вашего приложения (например: *myClientApp*), выберите **веб-приложение**и щелкните стрелку toocontinue hello.
5. Для hello **URL-адрес входа** и **URI идентификатора приложения** можно ввести допустимый URL-адрес (например, *http://myClientApp*) и продолжить.
6. Нажмите **НАСТРОИТЬ**.
7. Скопируйте значение **ИДЕНТИФИКАТОР КЛИЕНТА**. (Оно потребуется в коде позже.)
8. В hello **ключей** выберите **1 год** из hello **выберите длительность** раскрывающегося списка. (Необходимо будет скопировать ключ hello после сохранения на шаге 13.)
9. Прокрутите вниз и щелкните **Добавить приложение**.
10. Оставить **Показать** значение слишком**приложения Майкрософт** и выберите **API управления службами Microsoft Azure**. Щелкните флажок toocontinue hello.
11. Выберите **Azure службы управления доступом...**  из hello **делегированные разрешения** раскрывающегося списка.
12. Щелкните **СОХРАНИТЬ**.
13. После hello сохранить завершения, скопируйте значение ключа hello в hello **ключей** раздела. (Оно потребуется в коде позже.)

## <a name="create-a-key-vault-toostore-your-keys"></a>Создание ключей toostore хранилища ключей
Теперь, клиентское приложение настроено, и у вас есть свой идентификатор клиента, он время toocreate хранилища ключей и настроить ее политику доступа, вы и приложения могут получить доступ hello хранилище секретов (ключи постоянного шифрования hello). Hello *создания*, *получить*, *списка*, *входа*, *проверить*, *wrapKey*, и *unwrapKey* требуются разрешения для создания нового главного ключа столбца и настройке шифрования с SQL Server Management Studio.

Можно быстро создать хранилище ключей, выполнив следующий скрипт hello. Подробное описание этих командлетов и дополнительные сведения о создании и настройке хранилища ключей см. в статье [Приступая к работе с хранилищем ключей Azure](../key-vault/key-vault-get-started.md).

    $subscriptionName = '<your Azure subscription name>'
    $userPrincipalName = '<username@domain.com>'
    $clientId = '<client ID that you copied in step 7 above>'
    $resourceGroupName = '<resource group name>'
    $location = '<datacenter location>'
    $vaultName = 'AeKeyVault'


    Login-AzureRmAccount
    $subscriptionId = (Get-AzureRmSubscription -SubscriptionName $subscriptionName).Id
    Set-AzureRmContext -SubscriptionId $subscriptionId

    New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    New-AzureRmKeyVault -VaultName $vaultName -ResourceGroupName $resourceGroupName -Location $location

    Set-AzureRmKeyVaultAccessPolicy -VaultName $vaultName -ResourceGroupName $resourceGroupName -PermissionsToKeys create,get,wrapKey,unwrapKey,sign,verify,list -UserPrincipalName $userPrincipalName
    Set-AzureRmKeyVaultAccessPolicy  -VaultName $vaultName  -ResourceGroupName $resourceGroupName -ServicePrincipalName $clientId -PermissionsToKeys get,wrapKey,unwrapKey,sign,verify,list




## <a name="create-a-blank-sql-database"></a>Создание пустой базы данных SQL
1. Войдите в toohello [портал Azure](https://portal.azure.com/).
2. Go слишком**New** > **данные + хранилище** > **базы данных SQL**.
3. Создайте **пустую** базу данных **Clinic** на новом или имеющемся сервере. Подробные инструкции о том, как toocreate базы данных в hello портал Azure отображается [первой базы данных Azure SQL](sql-database-get-started-portal.md).
   
    ![Создание пустой базы данных](./media/sql-database-always-encrypted-azure-key-vault/create-database.png)

Будет необходимо hello строка подключения далее в учебнике hello, поэтому после создания базы данных hello перейдите toohello новую Clinic базы данных и скопируйте hello строку подключения. Строка подключения hello можно получить в любое время, но это просто toocopy его в hello портал Azure.

1. Go слишком**баз данных SQL** > **Clinic** > **Показать строки подключения базы данных**.
2. Скопируйте строку подключения hello для **ADO.NET**.
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted-azure-key-vault/connection-strings.png)

## <a name="connect-toohello-database-with-ssms"></a>Подключитесь к SSMS toohello базы данных
Откройте SSMS и подключите сервер toohello с базой данных Clinic hello.

1. Откройте среду SSMS. (Перейдите слишком**Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** окно, если он еще не открыт.)
2. Введите имя сервера и учетные данные. Имя сервера Hello можно найти в колонке базы данных SQL hello и в строке подключения hello скопированное ранее. Имя полного сервера hello типа, включая *database.windows.net*.
   
    ![Скопируйте строку подключения hello](./media/sql-database-always-encrypted-azure-key-vault/ssms-connect.png)

Если hello **новое правило брандмауэра** откроется окно входа в tooAzure и SSMS позволяют создать новое правило брандмауэра для вас.

## <a name="create-a-table"></a>Создание таблицы
В этом разделе вы создадите таблицу данных пациента toohold. Это не первоначально зашифрованы--вы настроите шифрования в следующем разделе hello.

1. Разверните узел **Базы данных**.
2. Щелкните правой кнопкой мыши hello **Clinic** базы данных и нажмите кнопку **новый запрос**.
3. Вставить hello, следуя Transact-SQL (T-SQL) в новое окно запроса hello и **Execute** его.

        CREATE TABLE [dbo].[Patients](
         [PatientId] [int] IDENTITY(1,1),
         [SSN] [char](11) NOT NULL,
         [FirstName] [nvarchar](50) NULL,
         [LastName] [nvarchar](50) NULL,
         [MiddleName] [nvarchar](50) NULL,
         [StreetAddress] [nvarchar](50) NULL,
         [City] [nvarchar](50) NULL,
         [ZipCode] [char](5) NULL,
         [State] [char](2) NULL,
         [BirthDate] [date] NOT NULL
         PRIMARY KEY CLUSTERED ([PatientId] ASC) ON [PRIMARY] );
         GO


## <a name="encrypt-columns-configure-always-encrypted"></a>Шифрование столбцов (настройка Always Encrypted)
Среда SSMS предоставляет мастер, который помогает легко настроить постоянного шифрования с помощью настройки главного ключа столбца hello, ключ шифрования столбца и зашифрованных столбцов для вас.

1. Разверните узел **Базы данных** > **Clinic** > **Таблицы**.
2. Щелкните правой кнопкой мыши hello **пациентов** таблицы и выберите **зашифровать столбцы** мастер постоянного шифрования tooopen hello:
   
    ![Шифрование столбцов…](./media/sql-database-always-encrypted-azure-key-vault/encrypt-columns.png)

Hello мастер постоянного шифрования включает в себя hello в следующих разделах: **выделенный фрагмент столбца**, **Конфигурация главного ключа**, **проверки**, и **Сводка** .

### <a name="column-selection"></a>Выполните действия на странице Выбор столбцов.
Нажмите кнопку **Далее** на hello **Введение** страницы приветствия tooopen **выделенный фрагмент столбца** страницы. На этой странице будет выбрать столбцы, которые вы хотите tooencrypt, [hello тип шифрования и определите, какой ключ шифрования столбца (CEK)](https://msdn.microsoft.com/library/mt459280.aspx#Anchor_2) toouse.

Для каждого пациента необходимо зашифровать данные в столбцах **SSN** и **BirthDate**. столбец SSN Hello будет использовать детерминированного шифрования, поддерживающую равенство, соединения и группировать. столбец BirthDate Hello будет использовать при выполнении случайного шифрования не поддерживает операции.

Набор hello **тип шифрования** для столбца hello SSN слишком**Deterministic** и hello столбца BirthDate слишком**случайное**. Щелкните **Далее**.

![Шифрование столбцов…](./media/sql-database-always-encrypted-azure-key-vault/column-selection.png)

### <a name="master-key-configuration"></a>Настройка главного ключа
Hello **Конфигурация главного ключа** страница является задаются копии базы данных и выберите hello поставщика хранилища ключей CMK hello CMK хранения. В настоящее время Главным можно хранить в хранилище сертификатов Windows hello, хранилище ключей или аппаратный модуль безопасности (HSM).

В этом учебнике показано как toostore ключей в хранилище ключей Azure.

1. Выберите **Хранилище ключей Azure**.
2. Выберите нужное хранилище ключей hello hello раскрывающегося списка.
3. Щелкните **Далее**.

![Настройка главного ключа](./media/sql-database-always-encrypted-azure-key-vault/master-key-configuration.png)

### <a name="validation"></a>Проверка
Могут быть зашифрованы hello столбцы сейчас или сохранить сценарий PowerShell toorun позже. В этом учебнике выберите **теперь продолжить toofinish** и нажмите кнопку **Далее**.

### <a name="summary"></a>Сводка
Убедитесь, что hello параметры заданы правильно и нажмите кнопку **Готово** toocomplete hello установки для постоянного шифрования.

![Сводка](./media/sql-database-always-encrypted-azure-key-vault/summary.png)

### <a name="verify-hello-wizards-actions"></a>Проверка действий мастера hello
После завершения работы мастера hello базы данных настроена для постоянного шифрования. выполнить мастер hello Hello, следующие действия:

* Создал главный ключ столбца и сохранил его в хранилище ключей Azure.
* Создал ключ шифрования столбца и сохранил его в хранилище ключей Azure.
* Настроенный hello выбранные столбцы для шифрования. Таблица сведений о пациентах Hello в настоящее время не содержит данных, но все существующие данные в столбцах выбран hello теперь зашифрованы.

Можно проверить hello Создание ключей hello в SSMS, развернув **Clinic** > **безопасности** > **ключей постоянного шифрования**.

## <a name="create-a-client-application-that-works-with-hello-encrypted-data"></a>Создание клиентского приложения, которое работает с данными зашифрован hello
Теперь, когда Настройка постоянного шифрования можно построить приложение, выполняющее *вставляет* и *выбирает* на hello зашифрованные столбцы.  

> [!IMPORTANT]
> Приложение должно использовать [SqlParameter](https://msdn.microsoft.com/library/system.data.sqlclient.sqlparameter.aspx) объектов при передаче сервер toohello данных открытого текста с всегда зашифрованным столбцам. Передача значений литералов без использования объектов SqlParameter приведет к возникновению исключения.
> 
> 

1. Откройте Visual Studio и создайте **консольное приложение** C# (Visual Studio 2015 и более ранней версии) или **консольное приложение (.NET Framework)** (Visual Studio 2017 и более поздней версии). Убедитесь, что проект настроен слишком**.NET Framework 4.6** или более поздней версии.
2. Имя проекта hello **AlwaysEncryptedConsoleAKVApp** и нажмите кнопку **ОК**.
3. Установить следующие пакеты NuGet, перейдя слишком hello**средства** > **диспетчера пакетов NuGet** > **консоль диспетчера пакетов**.

Запустите эти две строки кода в hello консоль диспетчера пакетов.

    Install-Package Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider
    Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory



## <a name="modify-your-connection-string-tooenable-always-encrypted"></a>Изменение вашей tooenable строку соединения, постоянное шифрование
В этом разделе объясняется, как tooenable всегда зашифрованы в строке подключения базы данных.

tooenable постоянного шифрования, необходимо tooadd hello **параметр шифрования столбца** tooyour соединения ключевое слово строки и задать для него слишком**включено**.

Это можно задать непосредственно в строке подключения hello или его можно задать с помощью [SqlConnectionStringBuilder](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.aspx). Пример приложения Hello в hello следующем разделе показано как toouse **SqlConnectionStringBuilder**.

### <a name="enable-always-encrypted-in-hello-connection-string"></a>Включить постоянное шифрование в строке подключения hello
Добавьте следующие строки подключения tooyour ключевое слово hello.

    Column Encryption Setting=Enabled


### <a name="enable-always-encrypted-with-sqlconnectionstringbuilder"></a>Включение функции Always Encrypted с помощью SqlConnectionStringBuilder
Здравствуйте, как следующий код показывает tooenable постоянное шифрование, задав [SqlConnectionStringBuilder.ColumnEncryptionSetting](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectionstringbuilder.columnencryptionsetting.aspx) слишком[включено](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnectioncolumnencryptionsetting.aspx).

    // Instantiate a SqlConnectionStringBuilder.
    SqlConnectionStringBuilder connStringBuilder =
       new SqlConnectionStringBuilder("replace with your connection string");

    // Enable Always Encrypted.
    connStringBuilder.ColumnEncryptionSetting =
       SqlConnectionColumnEncryptionSetting.Enabled;

## <a name="register-hello-azure-key-vault-provider"></a>Регистрация поставщика хранилища ключей Azure hello
Hello следующий код показывает, как tooregister hello поставщика хранилища ключей Azure с драйвером ADO.NET hello.

    private static ClientCredential _clientCredential;

    static void InitializeAzureKeyVaultProvider()
    {
       _clientCredential = new ClientCredential(clientId, clientSecret);

       SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
          new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

       Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
          new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

       providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
       SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
    }



## <a name="always-encrypted-sample-console-application"></a>Пример консольного приложения с функцией постоянного шифрования
В этом примере показано, как:

* Измените ваш tooenable строку соединения, постоянное шифрование.
* Зарегистрируйте хранилище ключей Azure, так как поставщик хранилища ключей приложения hello.  
* Вставка данных в hello зашифрованные столбцы.
* Выбрать запись, выполнив фильтрацию по конкретному значению в зашифрованном столбце.

Замените содержимое hello **Program.cs** с hello, следующий код. Замените hello строка подключения для hello connectionString глобальной переменной в строку hello, непосредственно предшествующий hello метод Main с вашей допустимую строку соединения из hello портал Azure. Это единственное изменение hello требуется toomake toothis код.

Запустите toosee приложения hello постоянного шифрования в действии.

    using System;
    using System.Collections.Generic;
    using System.Linq;
    using System.Text;
    using System.Threading.Tasks;
    using System.Data;
    using System.Data.SqlClient;
    using Microsoft.IdentityModel.Clients.ActiveDirectory;
    using Microsoft.SqlServer.Management.AlwaysEncrypted.AzureKeyVaultProvider;

    namespace AlwaysEncryptedConsoleAKVApp
    {
    class Program
    {
        // Update this line with your Clinic database connection string from hello Azure portal.
        static string connectionString = @"<connection string from hello portal>";
        static string clientId = @"<client id from step 7 above>";
        static string clientSecret = "<key from step 13 above>";


        static void Main(string[] args)
        {
            InitializeAzureKeyVaultProvider();

            Console.WriteLine("Signed in as: " + _clientCredential.ClientId);

            Console.WriteLine("Original connection string copied from hello Azure portal:");
            Console.WriteLine(connectionString);

            // Create a SqlConnectionStringBuilder.
            SqlConnectionStringBuilder connStringBuilder =
                new SqlConnectionStringBuilder(connectionString);

            // Enable Always Encrypted for hello connection.
            // This is hello only change specific tooAlways Encrypted
            connStringBuilder.ColumnEncryptionSetting =
                SqlConnectionColumnEncryptionSetting.Enabled;

            Console.WriteLine(Environment.NewLine + "Updated connection string with Always Encrypted enabled:");
            Console.WriteLine(connStringBuilder.ConnectionString);

            // Update hello connection string with a password supplied at runtime.
            Console.WriteLine(Environment.NewLine + "Enter server password:");
            connStringBuilder.Password = Console.ReadLine();


            // Assign hello updated connection string tooour global variable.
            connectionString = connStringBuilder.ConnectionString;


            // Delete all records toorestart this demo app.
            ResetPatientsTable();

            // Add sample data toohello Patients table.
            Console.Write(Environment.NewLine + "Adding sample patient data toohello database...");

            InsertPatient(new Patient()
            {
                SSN = "999-99-0001",
                FirstName = "Orlando",
                LastName = "Gee",
                BirthDate = DateTime.Parse("01/04/1964")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0002",
                FirstName = "Keith",
                LastName = "Harris",
                BirthDate = DateTime.Parse("06/20/1977")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0003",
                FirstName = "Donna",
                LastName = "Carreras",
                BirthDate = DateTime.Parse("02/09/1973")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0004",
                FirstName = "Janet",
                LastName = "Gates",
                BirthDate = DateTime.Parse("08/31/1985")
            });
            InsertPatient(new Patient()
            {
                SSN = "999-99-0005",
                FirstName = "Lucy",
                LastName = "Harrington",
                BirthDate = DateTime.Parse("05/06/1993")
            });


            // Fetch and display all patients.
            Console.WriteLine(Environment.NewLine + "All hello records currently in hello Patients table:");

            foreach (Patient patient in SelectAllPatients())
            {
                Console.WriteLine(patient.FirstName + " " + patient.LastName + "\tSSN: " + patient.SSN + "\tBirthdate: " + patient.BirthDate);
            }

            // Get patients by SSN.
            Console.WriteLine(Environment.NewLine + "Now lets locate records by searching hello encrypted SSN column.");

            string ssn;

            // This very simple validation only checks that hello user entered 11 characters.
            // In production be sure toocheck all user input and use hello best validation for your specific application.
            do
            {
                Console.WriteLine("Please enter a valid SSN (ex. 999-99-0003):");
                ssn = Console.ReadLine();
            } while (ssn.Length != 11);

            // hello example allows duplicate SSN entries so we will return all records
            // that match hello provided value and store hello results in selectedPatients.
            Patient selectedPatient = SelectPatientBySSN(ssn);

            // Check if any records were returned and display our query results.
            if (selectedPatient != null)
            {
                Console.WriteLine("Patient found with SSN = " + ssn);
                Console.WriteLine(selectedPatient.FirstName + " " + selectedPatient.LastName + "\tSSN: "
                    + selectedPatient.SSN + "\tBirthdate: " + selectedPatient.BirthDate);
            }
            else
            {
                Console.WriteLine("No patients found with SSN = " + ssn);
            }

            Console.WriteLine("Press Enter tooexit...");
            Console.ReadLine();
        }


        private static ClientCredential _clientCredential;

        static void InitializeAzureKeyVaultProvider()
        {

            _clientCredential = new ClientCredential(clientId, clientSecret);

            SqlColumnEncryptionAzureKeyVaultProvider azureKeyVaultProvider =
              new SqlColumnEncryptionAzureKeyVaultProvider(GetToken);

            Dictionary<string, SqlColumnEncryptionKeyStoreProvider> providers =
              new Dictionary<string, SqlColumnEncryptionKeyStoreProvider>();

            providers.Add(SqlColumnEncryptionAzureKeyVaultProvider.ProviderName, azureKeyVaultProvider);
            SqlConnection.RegisterColumnEncryptionKeyStoreProviders(providers);
        }

        public async static Task<string> GetToken(string authority, string resource, string scope)
        {
            var authContext = new AuthenticationContext(authority);
            AuthenticationResult result = await authContext.AcquireTokenAsync(resource, _clientCredential);

            if (result == null)
                throw new InvalidOperationException("Failed tooobtain hello access token");
            return result.AccessToken;
        }

        static int InsertPatient(Patient newPatient)
        {
            int returnValue = 0;

            string sqlCmdText = @"INSERT INTO [dbo].[Patients] ([SSN], [FirstName], [LastName], [BirthDate])
     VALUES (@SSN, @FirstName, @LastName, @BirthDate);";

            SqlCommand sqlCmd = new SqlCommand(sqlCmdText);


            SqlParameter paramSSN = new SqlParameter(@"@SSN", newPatient.SSN);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            SqlParameter paramFirstName = new SqlParameter(@"@FirstName", newPatient.FirstName);
            paramFirstName.DbType = DbType.String;
            paramFirstName.Direction = ParameterDirection.Input;

            SqlParameter paramLastName = new SqlParameter(@"@LastName", newPatient.LastName);
            paramLastName.DbType = DbType.String;
            paramLastName.Direction = ParameterDirection.Input;

            SqlParameter paramBirthDate = new SqlParameter(@"@BirthDate", newPatient.BirthDate);
            paramBirthDate.SqlDbType = SqlDbType.Date;
            paramBirthDate.Direction = ParameterDirection.Input;

            sqlCmd.Parameters.Add(paramSSN);
            sqlCmd.Parameters.Add(paramFirstName);
            sqlCmd.Parameters.Add(paramLastName);
            sqlCmd.Parameters.Add(paramBirthDate);

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();
                }
                catch (Exception ex)
                {
                    returnValue = 1;
                    Console.WriteLine("hello following error was encountered: ");
                    Console.WriteLine(ex.Message);
                    Console.WriteLine(Environment.NewLine + "Press Enter key tooexit");
                    Console.ReadLine();
                    Environment.Exit(0);
                }
            }
            return returnValue;
        }


        static List<Patient> SelectAllPatients()
        {
            List<Patient> patients = new List<Patient>();


            SqlCommand sqlCmd = new SqlCommand(
              "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients]",
                new SqlConnection(connectionString));


            using (sqlCmd.Connection = new SqlConnection(connectionString))

            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patients.Add(new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            });
                        }
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }

            return patients;
        }


        static Patient SelectPatientBySSN(string ssn)
        {
            Patient patient = new Patient();

            SqlCommand sqlCmd = new SqlCommand(
                "SELECT [SSN], [FirstName], [LastName], [BirthDate] FROM [dbo].[Patients] WHERE [SSN]=@SSN",
                new SqlConnection(connectionString));

            SqlParameter paramSSN = new SqlParameter(@"@SSN", ssn);
            paramSSN.DbType = DbType.AnsiStringFixedLength;
            paramSSN.Direction = ParameterDirection.Input;
            paramSSN.Size = 11;

            sqlCmd.Parameters.Add(paramSSN);


            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    SqlDataReader reader = sqlCmd.ExecuteReader();

                    if (reader.HasRows)
                    {
                        while (reader.Read())
                        {
                            patient = new Patient()
                            {
                                SSN = reader[0].ToString(),
                                FirstName = reader[1].ToString(),
                                LastName = reader["LastName"].ToString(),
                                BirthDate = (DateTime)reader["BirthDate"]
                            };
                        }
                    }
                    else
                    {
                        patient = null;
                    }
                }
                catch (Exception ex)
                {
                    throw;
                }
            }
            return patient;
        }


        // This method simply deletes all records in hello Patients table tooreset our demo.
        static int ResetPatientsTable()
        {
            int returnValue = 0;

            SqlCommand sqlCmd = new SqlCommand("DELETE FROM Patients");
            using (sqlCmd.Connection = new SqlConnection(connectionString))
            {
                try
                {
                    sqlCmd.Connection.Open();
                    sqlCmd.ExecuteNonQuery();

                }
                catch (Exception ex)
                {
                    returnValue = 1;
                }
            }
            return returnValue;
        }
    }

    class Patient
    {
        public string SSN { get; set; }
        public string FirstName { get; set; }
        public string LastName { get; set; }
        public DateTime BirthDate { get; set; }
    }
    }



## <a name="verify-that-hello-data-is-encrypted"></a>Убедитесь, что hello шифрование
Вы можете быстро проверить hello фактические данные на сервере hello зашифрован запрос hello пациентов данных с помощью среды SSMS (с использованием текущего подключения где **параметр шифрования столбца** еще не включен).

Запустите приветствия при следующем запросе в базе данных Clinic hello.

    SELECT FirstName, LastName, SSN, BirthDate FROM Patients;

Вы увидите, что hello зашифрованные столбцы не содержат все зашифрованные данные.

   ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-encrypted.png)

toouse SSMS tooaccess Здравствуйте зашифрованные данные, можно добавить hello *параметр шифрования столбца = включен* параметр toohello соединения.

1. В **обозревателе объектов** SSMS щелкните сервер правой кнопкой мыши и выберите пункт **Отключить**.
2. Нажмите кнопку **Connect** > **компонент Database Engine** tooopen hello **подключения tooServer** и щелкните **параметры**.
3. Щелкните **Дополнительные параметры соединения** и введите **Column Encryption Setting=enabled**.
   
    ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-connection-parameter.png)
4. Запустите приветствия при следующем запросе в базе данных Clinic hello.
   
        SELECT FirstName, LastName, SSN, BirthDate FROM Patients;
   
     Теперь можно увидеть hello зашифрованные данные в столбцах hello зашифрованы.

    ![Новое консольное приложение](./media/sql-database-always-encrypted-azure-key-vault/ssms-plaintext.png)


## <a name="next-steps"></a>Дальнейшие действия
После создания базы данных, которая использует постоянное шифрование, вы можете toodo hello следующее:

* [Сменить и очистить ключи](https://msdn.microsoft.com/library/mt607048.aspx).
* [Перенести данные, которые уже зашифрованы с использованием функции Always Encrypted.](https://msdn.microsoft.com/library/mt621539.aspx)

## <a name="related-information"></a>Связанные сведения
* [Always Encrypted (разработка клиентских приложений)](https://msdn.microsoft.com/library/mt147923.aspx)
* [Прозрачное шифрование данных](https://msdn.microsoft.com/library/bb934049.aspx)
* [Шифрование SQL Server](https://msdn.microsoft.com/library/bb510663.aspx)
* [Мастер настройки Always Encrypted](https://msdn.microsoft.com/library/mt459280.aspx)
* [Блог о функции Always Encrypted](http://blogs.msdn.com/b/sqlsecurity/archive/tags/always-encrypted/)

