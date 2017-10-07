---
title: "aaaSet копирование хранилища ключей Azure с начала до конца смены ключей и аудит | Документы Microsoft"
description: "Используйте это как tootoohelp, получить настраиваются с помощью мониторинга журналы хранилища ключей и смены ключей."
services: key-vault
documentationcenter: 
author: swgriffith
manager: mbaldwin
tags: 
ms.assetid: 9cd7e15e-23b8-41c0-a10a-06e6207ed157
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/07/2017
ms.author: jodehavi;stgriffi
ms.openlocfilehash: e0c393873077e3b91adc9fa7f39128bc1b6abe26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-key-vault-with-end-to-end-key-rotation-and-auditing"></a>Настройка полной смены ключей и аудита в хранилище ключей
## <a name="introduction"></a>Введение
После создания хранилища ключей, будет может toostart ключи и секретные коды, с помощью этого toostore хранилища. Приложения больше не нужна toopersist ключей или секретные данные, но вместо этого будет запрашивать их из хранилища ключей hello при необходимости. Это позволяет вам tooupdate ключи и секретные коды без влияния на поведение приложения, который открывает разнообразные возможности вокруг ключ и секретный управления hello.

В этой статье рассматриваются пример использования toostore хранилище ключей Azure секрета, в этом случае ключ учетной записи хранилища Azure, доступ к которому приложение. Здесь также описан процесс плановой смены этого ключа. Наконец он проходит через демонстрацию как toomonitor hello журналы аудита хранилища ключей и создавать оповещения при внесении непредвиденные запросы.

> [!NOTE]
> Этот учебник не предполагаемого tooexplain детализации hello начальной настройки хранилища ключей. Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md). Инструкции по кроссплатформенному интерфейсу командной строки см. в статье [Управление хранилищем ключей с помощью CLI](key-vault-manage-with-cli2.md).
>
>

## <a name="set-up-key-vault"></a>Настройка хранилища ключей
tooenable приложения tooretrieve секрета из хранилища ключей, необходимо сначала создать секрет hello и отправьте его tooyour хранилища. Это можно сделать, запустите сеанс Azure PowerShell и вход tooyour учетная запись Azure с hello следующую команду:

```powershell
Login-AzureRmAccount
```

В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль. PowerShell получит все подписки hello, связанные с этой учетной записи. Использует PowerShell hello первый из них по умолчанию.

Если у вас несколько подписок, может потребоваться toospecify hello, входящая в используемых toocreate хранилища ключей. Введите hello, следуя toosee hello подписки для учетной записи:

```powershell
Get-AzureRmSubscription
```

toospecify hello подписки, связанной с хранилищем ключей hello, которые можно выполнять вход, введите:

```powershell
Set-AzureRmContext -SubscriptionId <subscriptionID>
```

Так как в этой статье в качестве секрета используется ключ учетной записи хранения, вам необходимо получить его.

```powershell
Get-AzureRmStorageAccountKey -ResourceGroupName <resourceGroupName> -Name <storageAccountName>
```

После получения ваш секрет (в данном случае ключ учетной записи хранилища), необходимо преобразовать этой защищенной строки tooa и создайте секрета с соответствующими значениями в хранилище ключей.

```powershell
$secretvalue = ConvertTo-SecureString <storageAccountKey> -AsPlainText -Force

Set-AzureKeyVaultSecret -VaultName <vaultName> -Name <secretName> -SecretValue $secretvalue
```
Затем следует получите hello URI для hello секрета, который был создан. Используется в дальнейшем при вызове hello хранилища ключей tooretrieve ваш секрет. Выполните следующую команду PowerShell hello и запишите значение идентификатора hello, которое является hello секрет URI.

```powershell
Get-AzureKeyVaultSecret –VaultName <vaultName>
```

## <a name="set-up-hello-application"></a>Настройка приложения hello
Теперь, когда секретов, хранимых можно использовать tooretrieve код и использовать его. Существуют несколько шагов, необходимых tooachieve это. Hello первый и самый важный шаг является зарегистрировать приложение в Azure Active Directory и затем о том, хранилище ключей информации о приложениях, чтобы его можно разрешить запросы от приложения.

> [!NOTE]
> Приложения должны быть созданы на hello же клиент Azure Active Directory в качестве хранилища ключей.
>
>

Перейдите на вкладку приложения hello Azure Active Directory.

![Вкладка "Приложения" в Azure Active Directory](./media/keyvault-keyrotation/AzureAD_Header.png)

Выберите **добавить** tooadd tooyour приложения Azure Active Directory.

![Выбор пункта "Добавить"](./media/keyvault-keyrotation/Azure_AD_AddApp.png)

Оставьте тип приложения hello как **веб-приложение и/или WEB API** и присвойте имя приложения.

![Имя hello приложения](./media/keyvault-keyrotation/AzureAD_NewApp1.png)

Укажите нужные значения в полях **URL-адрес входа** и **URI идентификатора приложения**. Для этого примера можно указать любые значения. Позже их можно изменить.

![Предоставление необходимых URI](./media/keyvault-keyrotation/AzureAD_NewApp2.png)

После добавления приложения hello tooAzure Active Directory, то будут введены в страницы приложения hello. Нажмите кнопку hello **Настройка** вкладку и затем найдите и скопируйте hello **идентификатор клиента** значение. Запишите идентификатор hello клиента для выполнения следующих действий.

Далее создайте ключ для вашего приложения, чтобы оно могло взаимодействовать с Azure Active Directory. Это можно создать в группе hello **ключей** раздела hello **конфигурации** вкладки. Запишите hello вновь созданный ключ из приложения Azure Active Directory для использования в дальнейшем.

![Ключи приложения Azure Active Directory](./media/keyvault-keyrotation/Azure_AD_AppKeys.png)

Перед установкой каких-либо вызовов из приложения в хранилище ключей hello, hello хранилища ключей необходимо сообщить о приложении и его разрешения. Hello следующая команда получает имя хранилища hello и hello идентификатор клиента из приложения Azure Active Directory и предоставляет **получить** хранилища ключей tooyour доступа для приложения hello.

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <clientIDfromAzureAD> -PermissionsToSecrets Get
```

На этом этапе вы являются готов toostart построение приложение вызывает. В приложении необходимо установить toointeract необходимые пакеты NuGet hello с хранилищем ключей Azure и Azure Active Directory. Из консоли диспетчера пакетов Visual Studio hello введите следующие команды hello. Hello написания данной статьи, hello текущей версии пакета hello Azure Active Directory является 3.10.305231913, поэтому может требуется последняя версия tooconfirm hello и соответствующим образом обновить.

```powershell
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 3.10.305231913

Install-Package Microsoft.Azure.KeyVault
```

В коде приложения создайте метод hello toohold класс для проверки подлинности Azure Active Directory. В этом примере ему присвоено имя **Utils**. Добавьте следующее hello с помощью инструкции:

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
```

Добавьте следующую токен JWT hello tooretrieve метода из Azure Active Directory hello. Для удобства обслуживания можно жестко заданная строка значений toomove hello в конфигурацию сети или приложения.

```csharp
public async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);

    ClientCredential clientCred = new ClientCredential("<AzureADApplicationClientID>","<AzureADApplicationClientKey>");

    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)

    throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

Добавить необходимый код hello toocall хранилище ключей и получить ваш секретное значение. Сначала необходимо добавить следующие hello с помощью инструкции:

```csharp
using Microsoft.Azure.KeyVault;
```

Добавить tooinvoke вызовы метода hello хранилища ключей и получить ваш секрет. В этом методе предоставляют hello секрет URI, который был сохранен на предыдущем шаге. Обратите внимание на использование hello hello **GetToken** метод hello **Utils** ранее созданного класса.

```csharp
var kv = new KeyVaultClient(new KeyVaultClient.AuthenticationCallback(Utils.GetToken));

var sec = kv.GetSecretAsync(<SecretID>).Result.Value;
```

При запуске приложения, вы должны теперь проходят проверку подлинности tooAzure Active Directory, а затем получение вашего секретное значение из хранилища ключей Azure.

## <a name="key-rotation-using-azure-automation"></a>Смена ключей с помощью службы автоматизации Azure
Реализовать смену значений секретов в хранилище ключей Azure можно разными способами. Их можно сменить вручную, программным методом с помощью вызовов API или с использованием скрипта службы автоматизации. В целях hello этой статьи можно с помощью Azure PowerShell в сочетании с toochange автоматизации Azure ключ доступа учетной записи хранилища Azure. Затем с помощью нового ключа вы обновите секрет хранилища ключей.

tooallow автоматизации Azure tooset значения секрета в хранилище ключей, необходимо получить идентификатор клиента hello hello подключения с именем AzureRunAsConnection, который был создан при установке экземпляра службы автоматизации Azure. Это значение можно получить в окне **Активы** в экземпляре службы автоматизации Azure. После этого выберите **подключений** , а затем выберите hello **AzureRunAsConnection** участника службы. Запишите hello **идентификатор приложения**.

![Идентификатор клиента службы автоматизации Azure](./media/keyvault-keyrotation/Azure_Automation_ClientID.png)

В окне **Активы** выберите пункт **Модули**. Из **модули**выберите **коллекции**и выполните поиск и **импорта** обновленные версии hello следующие модули:

    Azure
    Azure.Storage
    AzureRM.Profile
    AzureRM.KeyVault
    AzureRM.Automation
    AzureRM.Storage


> [!NOTE]
> В hello написания данной статьи, hello toobe было отмечено выше модули, необходимые обновляется только для hello, выполнив сценарий. Если задание по автоматизации завершится сбоем, убедитесь, что вы импортировали все необходимые модули и зависимости.
>
>

После получения идентификатора приложения hello для подключения к службе автоматизации Azure необходимо сообщить хранилища ключей, что это приложение имеет доступ tooupdate секреты в хранилище. Это можно сделать с помощью hello следующую команду PowerShell:

```powershell
Set-AzureRmKeyVaultAccessPolicy -VaultName <vaultName> -ServicePrincipalName <applicationIDfromAzureAutomation> -PermissionsToSecrets Set
```

В экземпляре службы автоматизации Azure выберите пункт **Модули Runbook**, а затем — **Добавить Runbook**. Выберите **Быстрое создание**. Имя модуля runbook и выберите **PowerShell** как тип runbook hello. У вас есть параметр tooadd hello описание. Наконец, нажмите кнопку **Создать**.

![Создание модуля Runbook](./media/keyvault-keyrotation/Create_Runbook.png)

Вставьте следующий сценарий PowerShell hello область редактора для новый модуль runbook hello:

```powershell
$connectionName = "AzureRunAsConnection"
try
{
    # Get hello connection "AzureRunAsConnection "
    $servicePrincipalConnection=Get-AutomationConnection -Name $connectionName         

    "Logging in tooAzure..."
    Add-AzureRmAccount `
        -ServicePrincipal `
        -TenantId $servicePrincipalConnection.TenantId `
        -ApplicationId $servicePrincipalConnection.ApplicationId `
        -CertificateThumbprint $servicePrincipalConnection.CertificateThumbprint
    "Login complete."
}
catch {
    if (!$servicePrincipalConnection)
    {
        $ErrorMessage = "Connection $connectionName not found."
        throw $ErrorMessage
    } else{
        Write-Error -Message $_.Exception
        throw $_.Exception
    }
}

#Optionally you may set hello following as parameters
$StorageAccountName = <storageAccountName>
$RGName = <storageAccountResourceGroupName>
$VaultName = <keyVaultName>
$SecretName = <keyVaultSecretName>

#Key name. For example key1 or key2 for hello storage account
New-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName -KeyName "key2" -Verbose
$SAKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $RGName -Name $StorageAccountName

$secretvalue = ConvertTo-SecureString $SAKeys[1].Value -AsPlainText -Force

$secret = Set-AzureKeyVaultSecret -VaultName $VaultName -Name $SecretName -SecretValue $secretvalue
```

Панели редактора hello выберите **области тестов** tootest сценария. После hello сценарий выполняется без ошибок, можно выбрать **публикации**, и примените расписание для runbook hello обратно в область конфигурации hello runbook.

## <a name="key-vault-auditing-pipeline"></a>Конвейер аудита для хранилища ключей
При настройке хранилища ключей можно включить аудит toocollect журналы на запросы доступа toohello хранилища ключей. Эти журналы хранятся в назначенной учетной записи службы хранилища Azure. Их можно извлекать, отслеживать и анализировать. Hello следующий сценарий использует функций Azure, Azure логику приложения и toocreate журналы аудита хранилища ключей toosend конвейера сообщение электронной почты при приложения, которое соответствует идентификатор приложения hello веб-приложения hello извлекает секретные данные из хранилища hello.

Сначала нужно включить ведение журнала в хранилище ключей. Это можно сделать с помощью следующих команд PowerShell hello (полные сведения отображаются на [ключ хранилища ведения журнала](key-vault-logging.md)):

```powershell
$sa = New-AzureRmStorageAccount -ResourceGroupName <resourceGroupName> -Name <storageAccountName> -Type Standard\_LRS -Location 'East US'
$kv = Get-AzureRmKeyVault -VaultName '<vaultName>'
Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent
```

После включения это журналы аудита начала сбор в hello, назначенные учетной записи хранилища. В этих журналах содержатся сведения о том, кто, как и когда осуществлял доступ к хранилищам ключей.

> [!NOTE]
> Данные ведения журнала можно открыть 10 минут после операции hello хранилища ключей. Обычно они доступны даже раньше.
>
>

Hello следующим шагом является слишком[Создание очереди служебной шины Azure](../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md). Туда будут помещаться журналы аудита хранилища ключей. Если hello очереди сообщений в журнале аудита hello, приложение hello логику их собирают и работает с ними. Создание служебной шины с hello следующие шаги:

1. Создание пространства имен Service Bus (если это уже сделано, который будет toouse для этого пропустите tooStep 2).
2. Обзор toohello служебной шины в hello портал Azure и выберите приветствия имен toocreate hello очереди в требуемый.
3. Выберите **New** и выберите **Service Bus > очереди** и введите сведения о необходимых hello.
4. Выберите сведения о соединении Service Bus hello путем выбора имен hello и щелкнув **сведения о соединении**. Эти сведения понадобятся для следующего раздела hello.

Далее, [создать Azure функцию](../azure-functions/functions-create-first-azure-function.md) toopoll хранилища ключей в hello учетной записи хранилища и журналы получают новые события. Эта функция будет запускаться по расписанию.

Выберите toocreate функцию Azure **Создать > функции приложения** в hello портал Azure. Можно использовать для этого действующий план размещения или создать новый. Кроме того, можно использовать динамическое размещение. Дополнительные сведения о функции вариантов размещения можно найти в [как tooscale функции Azure](../azure-functions/functions-scale.md).

При создании hello Azure функция tooit перейдите и выберите таймер, функции и C\#. Затем щелкните **Создать эту функцию**.

![Начальная колонка функций Azure](./media/keyvault-keyrotation/Azure_Functions_Start.png)

На hello **разработка** вкладки, замените код run.csx hello hello следующее:

```csharp
#r "Newtonsoft.Json"

using System;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.ServiceBus.Messaging;
using System.Text;

public static void Run(TimerInfo myTimer, TextReader inputBlob, TextWriter outputBlob, TraceWriter log)
{
    log.Info("Starting");

    CloudStorageAccount sourceStorageAccount = new CloudStorageAccount(new StorageCredentials("<STORAGE_ACCOUNT_NAME>", "<STORAGE_ACCOUNT_KEY>"), true);

    CloudBlobClient sourceCloudBlobClient = sourceStorageAccount.CreateCloudBlobClient();

    var connectionString = "<SERVICE_BUS_CONNECTION_STRING>";
    var queueName = "<SERVICE_BUS_QUEUE_NAME>";

    var sbClient = QueueClient.CreateFromConnectionString(connectionString, queueName);

    DateTime dtPrev = DateTime.UtcNow;
    if(inputBlob != null)
    {
        var txt = inputBlob.ReadToEnd();

        if(!string.IsNullOrEmpty(txt))
        {
            dtPrev = DateTime.Parse(txt);
            log.Verbose($"SyncPoint: {dtPrev.ToString("O")}");
        }
        else
        {
            dtPrev = DateTime.UtcNow;
            log.Verbose($"Sync point file didnt have a date. Setting toonow.");
        }
    }

    var now = DateTime.UtcNow;

    string blobPrefix = "insights-logs-auditevent/resourceId=/SUBSCRIPTIONS/<SUBSCRIPTION_ID>/RESOURCEGROUPS/<RESOURCE_GROUP_NAME>/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/<KEY_VAULT_NAME>/y=" + now.Year +"/m="+now.Month.ToString("D2")+"/d="+ (now.Day).ToString("D2")+"/h="+(now.Hour).ToString("D2")+"/m=00/";

    log.Info($"Scanning:  {blobPrefix}");

    IEnumerable<IListBlobItem> blobs = sourceCloudBlobClient.ListBlobs(blobPrefix, true);

    log.Info($"found {blobs.Count()} blobs");

    foreach(var item in blobs)
    {
        if (item is CloudBlockBlob)
        {
            CloudBlockBlob blockBlob = (CloudBlockBlob)item;

            log.Info($"Syncing: {item.Uri}");

            string sharedAccessUri = GetContainerSasUri(blockBlob);

            CloudBlockBlob sourceBlob = new CloudBlockBlob(new Uri(sharedAccessUri));

            string text;
            using (var memoryStream = new MemoryStream())
            {
                sourceBlob.DownloadToStream(memoryStream);
                text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
            }

            dynamic dynJson = JsonConvert.DeserializeObject(text);

            //required tooorder by time as they may not be in hello file
            var results = ((IEnumerable<dynamic>) dynJson.records).OrderBy(p => p.time);

            foreach (var jsonItem in results)
            {
                DateTime dt = Convert.ToDateTime(jsonItem.time);

                if(dt>dtPrev){
                    log.Info($"{jsonItem.ToString()}");

                    var payloadStream = new MemoryStream(Encoding.UTF8.GetBytes(jsonItem.ToString()));
                    //When sending tooServiceBus, use hello payloadStream and set keeporiginal tootrue
                    var message = new BrokeredMessage(payloadStream, true);
                    sbClient.Send(message);
                    dtPrev = dt;
                }
            }
        }
    }
    outputBlob.Write(dtPrev.ToString("o"));
}

static string GetContainerSasUri(CloudBlockBlob blob)
{
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();

    sasConstraints.SharedAccessStartTime = DateTime.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```


> [!NOTE]
> Создайте переменные hello tooreplace убедиться, что предшествующий учетной записи хранилища tooyour toopoint код которой записи журналов хранилища ключей hello, hello hello служебной шины, который был создан ранее, и hello журналы хранения определенный путь toohello хранилища ключей.
>
>

функции Hello собирают hello последний файл журнала из учетной записи хранения hello где hello хранилища ключей журналы записываются, грабс hello последние события из этого файла и помещает в очередь Service Bus tooa. Так как один файл может иметь несколько событий, необходимо создать файл sync.txt, который также отслеживает функции hello toodetermine hello отметку времени последнего события hello, который был выбран. Это гарантирует, что не push hello того же события несколько раз. Этот файл sync.txt содержит отметку времени для последнего события обнаружен hello. Hello журналов, при загрузке имеют toobe сортируются на основе в неправильном порядке tooensure timestamp hello.

Для этой функции мы ссылаться на несколько дополнительных библиотек, которые недоступны в соответствующем hello в функциях Azure. tooinclude, нам нужно функции Azure toopull их с помощью NuGet. Выберите hello **Просмотр файлов** параметр.

![Элемент "Просмотреть файлы"](./media/keyvault-keyrotation/Azure_Functions_ViewFiles.png)

Затем добавьте новый файл project.json со следующим содержимым:

```json
    {
      "frameworks": {
        "net46":{
          "dependencies": {
                "WindowsAzure.Storage": "7.0.0",
                "WindowsAzure.ServiceBus":"3.2.2"
          }
        }
       }
    }
```
После **Сохранить**, функции Azure будут загружать необходимые hello двоичных файлов.

Переключение toohello **Интеграция** вкладку и предоставьте параметр таймера hello toouse понятное имя в пределах функции hello. В hello предшествующий код, ожидается, что называется toobe таймера hello *myTimer*. Укажите [выражение CRON](../app-service-web/web-sites-create-web-jobs.md#CreateScheduledCRON) следующим образом: 0 \* \* \* \* \* для hello таймер, который вызовет toorun функции hello раз в минуту.

На hello же **Интеграция** добавьте входные данные типа hello **хранилища больших двоичных объектов**. Это будет указывать toohello sync.txt файл, который содержит hello отметка времени последнего события hello рассказывали функцией hello. Он будет доступен в рамках функции hello по имени параметра hello. В предыдущих кода hello, входные данные для хранилища больших двоичных объектов hello ожидает toobe имя параметра hello *inputBlob*. Выберите учетную запись хранения hello, где будет находиться файл sync.txt hello (это может быть hello же или другую учетную запись хранения). В поля "путь" hello укажите путь hello, где находятся файл hello в формате hello {container-name}/path/to/sync.txt.

Добавление выходных данных типа hello *хранилища больших двоичных объектов* выходных данных. Указывает файл sync.txt toohello, заданных в hello входных данных. Это значение используется hello функция toowrite hello отметка времени последнего события hello рассмотрены. Hello предыдущий код ожидает, что этот параметр, toobe вызывается *outputBlob*.

На этом этапе функция hello готов. Сделать задней toohello убедиться, что tooswitch **разработка** вкладку и сохранение кода hello. Проверьте hello в окне вывода ошибок компиляции и исправьте их соответствующим образом. При компиляции кода hello, кода hello должны теперь проверять хранилище ключей журналы hello каждую минуту, и помещает новые события на hello определенные очереди Service Bus. Должны появиться сведения о ведении журнала, которые записывают окно журнала toohello каждый раз при запуске функции hello.

### <a name="azure-logic-app"></a>Приложение логики Azure
Далее необходимо создать приложение Azure логику, забирает hello событий, что функции hello внедряет toohello очереди Service Bus, выполняет синтаксический анализ содержимого hello и отправляет сообщение электронной почты, на основе условия сравниваемыми.

[Создание приложения логики](../logic-apps/logic-apps-create-a-logic-app.md) перейдя слишком**Создать > приложения логики**.

После создания приложения hello логики tooit перейдите и выберите **изменить**. Выбрать в редакторе логику приложения hello **очередь Service Bus** и введите ваш tooconnect учетные данные шины обслуживания его toohello очереди.

![Служебная шина приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_ServiceBus.png)

Затем выберите команду **Добавить условие**. В условии hello переключения toohello расширенный редактор и введите hello после кода, заменив APP_ID hello фактическое APP_ID веб-приложения:

```
@equals('<APP_ID>', json(decodeBase64(triggerBody()['ContentData']))['identity']['claim']['appid'])
```

По сути, это выражение возвращает **false** Если hello *appid* из hello не hello входящего события (который является текст hello сообщения hello Service Bus) *appid* из hello приложение.

Теперь создайте действие в разделе **If no, do nothing…** (Если нет, ничего не предпринимать).

![Выбор действия приложения логики Azure](./media/keyvault-keyrotation/Azure_LogicApp_Condition.png)

Действие hello выберите **Office 365 — отправлять по электронной почте**. Заполните поля toocreate hello toosend электронной почты при hello определено условие возвращает **false**. Если у вас Office 365, вам увидеть альтернативы tooachieve hello одинаковые результаты.

В этот момент у вас есть окончания tooend конвейера, который ищет новые журналы аудита хранилища ключей, раз в минуту. Он помещает новые журналы, он находит tooa очередь service bus. приложения логики Hello срабатывает, когда новое сообщение попадает в очередь hello. Если hello *appid* внутри hello событий не соответствует идентификатор приложения hello вызов приложения hello, он отправляет сообщение электронной почты.
