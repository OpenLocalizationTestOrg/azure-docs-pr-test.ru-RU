---
title: "aaaUse toodo захват пакетов упреждающего мониторинга с оповещениями и функциями Azure сети | Документы Microsoft"
description: "В этой статье описывается, как toocreate оповещение запускается захват пакетов с Наблюдатель сети Azure"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: 75e6e7c4-b3ba-4173-8815-b00d7d824e11
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: 4722a831f3a9d5537c0e6f53daba4dfc35d0cf24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-packet-capture-for-proactive-network-monitoring-with-alerts-and-azure-functions"></a>Использование записи пакетов для упреждающего мониторинга сети с помощью оповещений и функций Azure

Захват пакетов Наблюдатель сети создает сеансы регистрации tootrack трафика и из него виртуальных машин. Hello файл записи может иметь фильтр, который определяется tootrack hello только трафик, что требуется toomonitor. Эти данные затем сохраняются в хранилище BLOB-объекта или локально на гостевой машине hello.

Эта возможность допускает удаленный запуск из других сценариев службы автоматизации, таких как функции Azure. Предоставляет захват пакетов hello упреждающего получает возможность toorun на основе определенных аномалий сети. Они также помогают выполнять сбор сетевой статистики, получать сведения о сетевых вторжениях, выполнять отладку передачи данных между клиентом и сервером и другие операции.

Развернутые в Azure ресурсы работают круглосуточно и без выходных. Вам и вашим сотрудникам не может отслеживать активно hello все ресурсы 24/7. К примеру, что вы будете делать, если сбой произойдет в два часа ночи?

С использованием Наблюдатель сети, предупреждения и функции из hello Azure экосистемы можно заранее ответить hello данными и средствами toosolve проблем в сети.

![Сценарий][scenario]

## <a name="prerequisites"></a>Предварительные требования

* Hello последнюю версию [Azure PowerShell](/powershell/azure/install-azurerm-ps).
* Существующий экземпляр службы "Наблюдатель за сетями". Если у вас нет экземпляра этой службы, [создайте его](network-watcher-create.md).
* Существующую виртуальную машину в hello одном регионе Наблюдатель сети с hello [расширение Windows](../virtual-machines/windows/extensions-nwa.md) или [расширение виртуальной машины Linux](../virtual-machines/linux/extensions-nwa.md).

## <a name="scenario"></a>Сценарий

В этом примере ВМ отправляет дополнительные TCP-сегментов, чем обычно, и требуется toobe оповещения. TCP-сегменты используются только в качестве примера. Вы можете использовать любое условие оповещения.

Оповещения отображаются, их нужно toounderstand tooreceive данных на уровне пакета, почему увеличилось связи. Затем можно предпринять шаги tooreturn hello виртуальной машины tooregular связи.

В этом сценарии предполагается, что у вас есть экземпляр службы "Наблюдатель за сетями", а также группа ресурсов с допустимой виртуальной машиной.

После списка Hello приведен обзор hello рабочего процесса, который имеет место.

1. На виртуальной машине активируется оповещение.
1. Предупреждение Hello вызывает функцию Azure через веб-перехватчик.
1. Функции Azure обрабатывает предупреждения hello и запускает сеанс отслеживания пакетов Наблюдатель сети.
1. Захват пакетов Hello выполняется на ВМ hello и собирает трафика.
1. Hello пакет отслеживания передачи файла tooa учетной записи хранилища для их просмотра и диагностики.

tooautomate этого процесса она создана и подключиться оповещение на наш tootrigger виртуальной Машины при возникновении hello инцидента. Также мы создадим toocall функции в Наблюдатель сети.

Этот сценарий hello следующие:

* создает функцию Azure, которая запускает запись пакетов;
* Создает правило генерации оповещений на виртуальной машине и настраивает hello правило оповещения toocall hello Azure функции.

## <a name="create-an-azure-function"></a>Создание функции Azure

Первым шагом Hello toocreate tooprocess hello Azure функции оповещения и создать захват пакетов.

1. В hello [портал Azure](https://portal.azure.com)выберите **New** > **вычислений** > **функции приложения**.

    ![Создание приложения-функции][1-1]

2. На hello **функции приложения** колонки, введите следующие значения hello, а затем выберите **ОК** приложение hello toocreate:

    |**Параметр** | **Значение** | **Дополнительные сведения** |
    |---|---|---|
    |**Имя приложения**|PacketCaptureExample|имя функции приложение hello Hello.|
    |**Подписка**|[Подписки] hello подписки, для которых приложение функции hello toocreate.||
    |**Группа ресурсов**|PacketCaptureRG|ресурс группы toocontain hello функция приложение Hello.|
    |**План размещения**|План потребления| Тип Hello плана ваша функция использует приложение. Можно выбрать план потребления или план службы приложений Azure. |
    |**Расположение**|Центральный регион США| область какое приложение toocreate hello функции Hello.|
    |**Учетная запись хранения**|{autogenerated}| Учетная запись хранения Hello, требуются функции Azure для хранения общего назначения.|

3. На hello **приложений-функций PacketCaptureExample** колонке выберите **функции** > **пользовательские функции**  >  **+**.

4. Выберите **HttpTrigger Powershell**, а затем введите hello оставшиеся сведения. Наконец, toocreate функции hello, выберите **создать**.

    |**Параметр** | **Значение** | **Дополнительные сведения** |
    |---|---|---|
    |**Сценарий**|Экспериментальная возможность|Тип сценария|
    |**Имя функции**|AlertPacketCapturePowerShell|Имя функции hello|
    |**Уровень авторизации**|Функция|Уровень авторизации для функции hello|

![Пример функций][functions1]

> [!NOTE]
> шаблон PowerShell Hello является экспериментальной и не имеет полную поддержку.

Настройки требуются для этого примера и описаны в hello следующие шаги.

### <a name="add-modules"></a>Добавление модулей

функция приложение hello последнюю PowerShell модуль toohello отправить toouse командлеты PowerShell Наблюдатель сети.

1. На локальном компьютере с hello установлены последние модули Azure PowerShell выполните следующую команду PowerShell hello.

    ```powershell
    (Get-Module AzureRM.Network).Path
    ```

    Это пример дает hello локальный путь к модули Azure PowerShell. Мы используем эти папки позже. Hello модули, используемые в этом сценарии являются:

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

    ![Папки PowerShell][functions5]

1. Выберите **функции параметров приложения** > **Go tooApp редактор службы**.

    ![Параметры приложения-функции][functions2]

1. Щелкните правой кнопкой мыши hello **AlertPacketCapturePowershell** папки и создайте папку с именем **azuremodules**. 

4. Создайте вложенную папку для каждого требуемого модуля.

    ![Папки и вложенные папки][functions3]

    * AzureRM.Network

    * AzureRM.Profile

    * AzureRM.Resources

1. Щелкните правой кнопкой мыши hello **AzureRM.Network** вложенную папку, а затем выберите **передача файлов**. 

6. Go tooyour Azure модули. В локальной hello **AzureRM.Network** папку, выберите все файлы hello в папке hello. Нажмите кнопку **ОК**. 

7. Повторите эти шаги для папок **AzureRM.Profile** и **AzureRM.Resources**.

    ![Отправка файлов][functions6]

1. После завершения, каждой папки должен быть hello файлы модуля PowerShell с локального компьютера.

    ![Файлы PowerShell][functions7]

### <a name="authentication"></a>Аутентификация

командлеты PowerShell toouse hello, вы должны пройти проверку подлинности. Настройте проверку подлинности в приложении функции hello. tooconfigure проверки подлинности, необходимо настроить переменные среды и передачи приложения функции toohello зашифрованный файл ключа.

> [!NOTE]
> Этот сценарий обеспечивает лишь один пример того, как tooimplement проверки подлинности с помощью функций Azure. Существуют другие способы toodo это.

#### <a name="encrypted-credentials"></a>Зашифрованные учетные данные

Следующий сценарий PowerShell Hello создает файл ключа с именем **PassEncryptKey.key**. Он также предоставляет зашифрованную версию пароля hello, входящую в. Этот пароль — hello пароль, который определен для приложения hello Azure Active Directory, который используется для проверки подлинности.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

В hello редактор службы приложения hello функции приложения, создайте папку с именем **ключей** под **AlertPacketCapturePowerShell**. Затем отправьте hello **PassEncryptKey.key** файл, созданный в предыдущем примере PowerShell hello.

![Ключ для функций][functions8]

### <a name="retrieve-values-for-environment-variables"></a>Извлечение значений переменных среды

Hello окончательного требованием является tooset копирование hello переменные среды, которые являются значениями hello tooaccess, необходимые для проверки подлинности. Hello ниже перечислены hello переменные среды, которые создаются.

* AzureClientID

* AzureTenant

* AzureCredPassword


#### <a name="azureclientid"></a>AzureClientID

Идентификатор клиента Hello — hello код приложения в Azure Active Directory.

1. Если у вас еще нет toouse приложения, запустите приложение после toocreate пример hello.

    ```powershell
    $app = New-AzureRmADApplication -DisplayName "ExampleAutomationAccount_MF" -HomePage "https://exampleapp.com" -IdentifierUris "https://exampleapp1.com/ExampleFunctionsAccount" -Password "<same password as defined earlier>"
    New-AzureRmADServicePrincipal -ApplicationId $app.ApplicationId
    Start-Sleep 15
    New-AzureRmRoleAssignment -RoleDefinitionName Contributor -ServicePrincipalName $app.ApplicationId
    ```

   > [!NOTE]
   > Hello пароль, используемый при создании приложения hello должно быть hello пароль, который был создан ранее, при сохранении файла ключа hello.

1. В hello портал Azure, выберите **подписки**. Выберите toouse hello подписки, а затем выберите **(IAM) управления доступом к**.

    ![Функции (IAM)][functions9]

1. Выберите учетную запись toouse hello, а затем выберите **свойства**. Скопируйте hello идентификатор приложения.

    ![Идентификатор приложений-функций][functions10]

#### <a name="azuretenant"></a>AzureTenant

Получите идентификатор клиента hello, выполнив следующий пример скрипта PowerShell hello:

```powershell
(Get-AzureRmSubscription -SubscriptionName "<subscriptionName>").TenantId
```

#### <a name="azurecredpassword"></a>AzureCredPassword

Hello значение переменной среды AzureCredPassword hello значение hello, получить запуск hello следующий пример скрипта PowerShell. В этом примере hello же, что показано в предыдущем hello **зашифровал учетные данные** раздела. Здравствуйте, значение, которое требуется представляет выходные данные hello hello `$Encryptedpassword` переменной.  Это основной пароль службы hello, который зашифрован с помощью сценария PowerShell hello.

```powershell
#Variables
$keypath = "C:\temp\PassEncryptKey.key"
$AESKey = New-Object Byte[] 32
$Password = "<insert a password here>"

#Keys
[Security.Cryptography.RNGCryptoServiceProvider]::Create().GetBytes($AESKey) 
Set-Content $keypath $AESKey

#Get encrypted password
$secPw = ConvertTo-SecureString -AsPlainText $Password -Force
$AESKey = Get-content $KeyPath
$Encryptedpassword = $secPw | ConvertFrom-SecureString -Key $AESKey
$Encryptedpassword
```

### <a name="store-hello-environment-variables"></a>Переменные среды hello хранилища

1. Go toohello функции приложения. Затем последовательно выберите **Параметры приложения-функции** > **Настроить параметры приложения**.

    ![Настройка параметров приложения][functions11]

1. Добавьте hello переменных среды и их значения toohello приложение параметров, а затем выберите **Сохранить**.

    ![Параметры приложения][functions12]

### <a name="add-powershell-toohello-function"></a>Добавление функции toohello PowerShell

Это теперь время toomake вызывает Наблюдатель сети из внутри hello Azure функции. Hello реализация этой функции могут различаться в зависимости от требований hello. Однако поток общие hello hello кода выглядит следующим образом:

1. Обработка входных параметров.
2. Существующий пакет записывает tooverify ограничения и разрешения конфликтов имен.
3. Создание записи пакетов с необходимыми параметрами.
4. Периодический опрос процесса записи пакетов вплоть до его завершения.
5. Уведомите пользователя hello, что сеанс захвата hello пакета завершена.

Hello ниже приведен код PowerShell, который может использоваться в функции hello. Нет значения, которые необходимо заменить для toobe **subscriptionId**, **resourceGroupName**, и **storageAccountName**.

```powershell
            #Import Azure PowerShell modules required toomake calls tooNetwork Watcher
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Profile\AzureRM.Profile.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Network\AzureRM.Network.psd1" -Global
            Import-Module "D:\home\site\wwwroot\AlertPacketCapturePowerShell\azuremodules\AzureRM.Resources\AzureRM.Resources.psd1" -Global

            #Process alert request body
            $requestBody = Get-Content $req -Raw | ConvertFrom-Json

            #Storage account ID toosave captures in
            $storageaccountid = "/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/{storageAccountName}"

            #Packet capture vars
            $packetcapturename = "PSAzureFunction"
            $packetCaptureLimit = 10
            $packetCaptureDuration = 10

            #Credentials
            $tenant = $env:AzureTenant
            $pw = $env:AzureCredPassword
            $clientid = $env:AzureClientId
            $keypath = "D:\home\site\wwwroot\AlertPacketCapturePowerShell\keys\PassEncryptKey.key"

            #Authentication
            $secpassword = $pw | ConvertTo-SecureString -Key (Get-Content $keypath)
            $credential = New-Object System.Management.Automation.PSCredential ($clientid, $secpassword)
            Add-AzureRMAccount -ServicePrincipal -Tenant $tenant -Credential $credential #-WarningAction SilentlyContinue | out-null


            #Get hello VM that fired hello alert
            if($requestBody.context.resourceType -eq "Microsoft.Compute/virtualMachines")
            {
                Write-Output ("Subscription ID: {0}" -f $requestBody.context.subscriptionId)
                Write-Output ("Resource Group:  {0}" -f $requestBody.context.resourceGroupName)
                Write-Output ("Resource Name:  {0}" -f $requestBody.context.resourceName)
                Write-Output ("Resource Type:  {0}" -f $requestBody.context.resourceType)

                #Get hello Network Watcher in hello VM's region
                $nw = Get-AzurermResource | Where {$_.ResourceType -eq "Microsoft.Network/networkWatchers" -and $_.Location -eq $requestBody.context.resourceRegion}
                $networkWatcher = Get-AzureRmNetworkWatcher -Name $nw.Name -ResourceGroupName $nw.ResourceGroupName

                #Get existing packetCaptures
                $packetCaptures = Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher

                #Remove existing packet capture created by hello function (if it exists)
                $packetCaptures | %{if($_.Name -eq $packetCaptureName)
                { 
                    Remove-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -PacketCaptureName $packetCaptureName
                }}

                #Initiate packet capture on hello VM that fired hello alert
                if ((Get-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher).Count -lt $packetCaptureLimit){
                    echo "Initiating Packet Capture"
                    New-AzureRmNetworkWatcherPacketCapture -NetworkWatcher $networkWatcher -TargetVirtualMachineId $requestBody.context.resourceId -PacketCaptureName $packetCaptureName -StorageAccountId $storageaccountid -TimeLimitInSeconds $packetCaptureDuration
                    Out-File -Encoding Ascii -FilePath $res -inputObject "Packet Capture created on ${requestBody.context.resourceID}"
                }
            } 
 ``` 
#### <a name="retrieve-hello-function-url"></a>Получить URL-адрес функции hello 
1. После создания функции, настройте URL-адрес hello предупреждения toocall, связанной с функции hello. tooget это значение URL-адрес функции hello копирование из приложения функция.

    ![Поиск URL-адрес функции hello][functions13]

2. Скопируйте URL-адрес функции hello функции приложения.

    ![Копирование URL-адрес функции hello][2]

Если требуется пользовательских свойств в полезных данных запроса POST веб-перехватчика hello hello ссылаться слишком[настроить веб-перехватчика на оповещение Azure метрики](../monitoring-and-diagnostics/insights-webhooks-alerts.md).

## <a name="configure-an-alert-on-a-vm"></a>Настройка оповещения на виртуальной машине

Предупреждения может быть настроенный toonotify отдельных пользователей, когда конкретную метрику пересекает пороговое значение, которое назначается tooit. В этом примере hello предупреждение включено hello TCP-сегментов, которые отправляются, но hello предупреждение можно запустить для многих других показателей. В этом примере предупреждение — настроенное toocall функции hello toocall веб-перехватчика.

### <a name="create-hello-alert-rule"></a>Создание правила оповещения hello

Go tooan существующей виртуальной машины, а затем добавьте правило оповещения. Дополнительные сведения о настройке оповещений см. в статье [Создание оповещений в Azure Monitor для служб Azure с помощью портала Azure](../monitoring-and-diagnostics/insights-alerts-portal.md). Введите следующие значения в hello hello **правило оповещения** колонки, а затем выберите **ОК**.

  |**Параметр** | **Значение** | **Дополнительные сведения** |
  |---|---|---|
  |**Имя**|TCP_Segments_Sent_Exceeded|Имя правила оповещения hello.|
  |**Описание**|Число отправленных TCP-сегментов превысило пороговое значение|Описание правила оповещений hello Hello.||
  |**Метрика**|Отправлено TCP-сегментов| Hello метрики toouse tootrigger hello предупреждений. |
  |**Condition**|Больше| Hello toouse условия, при вычислении показателя hello.|
  |**Пороговое значение**.|100| Hello значение для показателя hello hello предупреждение. Это должно быть значение tooa допустимое значение для вашей среды.|
  |**Период**|За последние пять минут hello| Определяет период hello в какие toolook для hello пороговое значение метрики hello.|
  |**webhook**|[URL-адрес веб-перехватчика из приложения-функции]| Hello веб-перехватчика URL-адрес из приложения функция hello, созданный на предыдущих этапах hello.|

> [!NOTE]
> Метрика сегментов Hello TCP не включен по умолчанию. Дополнительные сведения о tooenable дополнительные метрики, посетив [включить наблюдение и диагностику](../monitoring-and-diagnostics/insights-how-to-use-diagnostics.md).

## <a name="review-hello-results"></a>Просмотрите результаты hello

После критерии hello для оповещения триггеры hello создается захват пакетов. Перейти tooNetwork наблюдателя, а затем выберите **захват пакетов**. На этой странице можно выбрать hello записи файла ссылки toodownload hello пакетов захват пакетов.

![Просмотр записи пакетов][functions14]

Если файл записи hello хранится локально, его можно получить при входе в toohello виртуальной машины.

Инструкции по скачиванию файлов из учетных записей хранения Azure см. в статье [Приступая к работе с хранилищем BLOB-объектов Azure с помощью .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md). Кроме того, можно использовать такое средство, как [обозреватель хранилищ](http://storageexplorer.com/).

Когда вы скачаете нужную запись, ее можно просмотреть в любом средстве, поддерживающем формат **CAP**. Ниже приведены ссылки tootwo этих средств:

- [Анализатор сообщений (Майкрософт)](https://technet.microsoft.com/library/jj649776.aspx).
- [Wireshark](https://www.wireshark.org/).

## <a name="next-steps"></a>Дальнейшие действия

Узнайте, как tooview вашей снимки пакетов, посетив [анализ захват пакетов с помощью Wireshark](network-watcher-deep-packet-inspection.md).


[1]: ./media/network-watcher-alert-triggered-packet-capture/figure1.png
[1-1]: ./media/network-watcher-alert-triggered-packet-capture/figure1-1.png
[2]: ./media/network-watcher-alert-triggered-packet-capture/figure2.png
[3]: ./media/network-watcher-alert-triggered-packet-capture/figure3.png
[functions1]:./media/network-watcher-alert-triggered-packet-capture/functions1.png
[functions2]:./media/network-watcher-alert-triggered-packet-capture/functions2.png
[functions3]:./media/network-watcher-alert-triggered-packet-capture/functions3.png
[functions4]:./media/network-watcher-alert-triggered-packet-capture/functions4.png
[functions5]:./media/network-watcher-alert-triggered-packet-capture/functions5.png
[functions6]:./media/network-watcher-alert-triggered-packet-capture/functions6.png
[functions7]:./media/network-watcher-alert-triggered-packet-capture/functions7.png
[functions8]:./media/network-watcher-alert-triggered-packet-capture/functions8.png
[functions9]:./media/network-watcher-alert-triggered-packet-capture/functions9.png
[functions10]:./media/network-watcher-alert-triggered-packet-capture/functions10.png
[functions11]:./media/network-watcher-alert-triggered-packet-capture/functions11.png
[functions12]:./media/network-watcher-alert-triggered-packet-capture/functions12.png
[functions13]:./media/network-watcher-alert-triggered-packet-capture/functions13.png
[functions14]:./media/network-watcher-alert-triggered-packet-capture/functions14.png
[scenario]:./media/network-watcher-alert-triggered-packet-capture/scenario.png
