---
title: "журналы aaaIntegrate из хранилища ключей Azure с помощью концентраторов событий | Документы Microsoft"
description: "Учебник, в котором предоставляет необходимые шаги hello toomake хранилище ключей журналы доступны tooa SIEM с помощью интеграции журналов Azure"
services: security
author: barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.topic: article
ms.date: 08/07/2017
ms.author: Barclayn
ms.custom: AzLog
ms.openlocfilehash: ada2fc846cc6bf09e12cc2c016815b27afef0d50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-log-integration-tutorial-process-azure-key-vault-events-by-using-event-hubs"></a>Руководство по интеграции журналов Azure. Обработка событий Azure Key Vault с помощью концентраторов событий

Можно использовать tooretrieve в журнал события журнала интеграции Azure и сделать их tooyour доступные сведения и событий системы управления безопасностью (SIEM). Этот учебник является примером как интеграции журналов Azure можно использовать tooprocess журналы, полученные через концентраторов событий Azure.
 
С помощью этого учебника tooget изучать как рабочих журналов интеграции Azure и концентраторов событий друг с другом, выполнив hello примеры действий и основные сведения о поддержке решений hello каждого шага. Затем вы сможете, что вы узнали здесь toocreate toosupport свои собственные шаги уникальные требования вашей компании.

>[!WARNING]
шаги Hello и команды в этом учебнике не предполагаемого toobe операций копирования и вставки. Они предоставляются только в качестве примеров. Не используйте команды PowerShell hello «как есть» в динамической среде. Их необходимо настраивать с учетом уникальной среды.


Этот учебник поможет выполнить процесс hello получения концентратора событий регистрируется tooan действие хранилища ключей Azure и делая ее доступной в качестве системы SIEM tooyour файлы JSON. Затем можно настроить SIEM системы tooprocess hello JSON-файлов.

>[!NOTE]
>Большая часть hello шагах данного учебника включают Настройка хранилищ ключей, учетные записи хранения и концентраторов событий. конкретные шаги интеграции Azure журнала Hello, hello конце этого учебника. Не выполняйте следующие действия в рабочей среде. Они предназначены для работы в лабораторной среде. Перед использованием их в рабочей среде необходимо настроить действия hello.

Сведения предоставлены вдоль hello способ помогает понять hello лежит в основе каждого шага. Статьи tooother ссылки предоставляют подробные сведения на определенных разделов.

Дополнительные сведения о службах hello, которые упоминаются в этом учебнике см. в разделе: 

- [Хранилище ключей Azure](../key-vault/key-vault-whatis.md)
- [Концентраторы событий Azure](../event-hubs/event-hubs-what-is-event-hubs.md)
- [Интеграция журналов Azure](security-azure-log-integration-overview.md)


## <a name="initial-setup"></a>Начальная настройка

Перед выполнением действия hello в этой статье, необходимо hello следующее:

1. Подписка Azure и учетная запись для этой подписки с правами администратора. Если у вас нет подписки, вы можете [создать бесплатную учетную запись](https://azure.microsoft.com/free/).
 
2. В системе с toohello доступа Интернета, отвечающий требованиям hello для интеграции Azure журнала установки. Hello системы может размещаться в облачной службе или в локальной среде.

3. Установленная служба [интеграции журналов Azure](https://www.microsoft.com/download/details.aspx?id=53324). tooinstall его:

   а. Использование удаленного рабочего стола tooconnect toohello системы, упомянутых в шаге 2.   
   b. Скопируйте hello Azure журнала установщика toohello системы интеграции. Вы можете [загружать файлы установки hello](https://www.microsoft.com/download/details.aspx?id=53324).   
   c. Запустите установщик hello и примите условия лицензии программного обеспечения Microsoft hello.   
   d. При указании данные телеметрии, оставьте hello флажок установлен. Если вы предпочитаете не отправлять tooMicrosoft сведения об использовании, снимите флажок "hello".
   
   Дополнительные сведения об интеграции журналов Azure и как tooinstall, в разделе [интеграции Azure журнала с помощью ведения журнала диагностики Azure и пересылки событий Windows](security-azure-log-integration-get-started.md).

4. Последняя версия PowerShell Hello.
 
   Если у вас установлен Windows Server 2016, по меньшей мере у вас есть PowerShell 5.0. Если вы используете другие версии Windows Server, может потребоваться установить более раннюю версию PowerShell. Можно проверить версии hello, введя ```get-host``` в окне PowerShell. Если версия PowerShell 5.0 не установлена, ее можно [скачать](https://www.microsoft.com/download/details.aspx?id=50395).

   После того как вы по крайней мере PowerShell 5.0, можно продолжить tooinstall hello последней версии:
   
   а. В окне PowerShell, введите hello ```Install-Module Azure``` команды. Выполните действия по установке hello.    
   b. Введите hello ```Install-Module AzureRM``` команды. Выполните действия по установке hello.

   Дополнительные сведения см. в статье [Установка Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-4.0.0).


## <a name="create-supporting-infrastructure-elements"></a>Создание вспомогательных элементов инфраструктуры

1. Откройте окно PowerShell с повышенными привилегиями и перейдите слишком**интеграции журнала C:\Program Files\Microsoft Azure**.
2. Импортируйте командлеты AzLog hello, выполнив сценарий hello LoadAzLogModule.ps1. Введите hello `.\LoadAzLogModule.ps1` команды. (Обратите внимание hello «. \» в этой команде.) Вы увидите нечто вроде этого:</br>

   ![Список загруженных модулей](./media/security-azure-log-integration-keyvault-eventhub/loaded-modules.png)

3. Введите hello `Login-AzureRmAccount` команды. В окне приветствия входа введите hello учетные данные для подписки hello, который будет использоваться для этого учебника.

   >[!NOTE]
   >Если это впервые hello, заносимых в журнал в tooAzure на данном компьютере, появится сообщение о разрешении данные об использовании PowerShell toocollect Microsoft. Рекомендуется включить эту коллекцию, так как они будут использоваться tooimprove Azure PowerShell.

4. После успешной проверки подлинности выполнен вход, и вы увидите сведения hello в следующий снимок экрана приветствия. Запишите имя идентификатора и подписки подписка hello, так как они потребуются позднее шаги toocomplete.

   ![Окно PowerShell](./media/security-azure-log-integration-keyvault-eventhub/login-azurermaccount.png)
5. Создайте переменные toostore значения, которые будут использоваться позже. Введите каждый из следующих строк PowerShell hello. Может потребоваться tooadjust hello значения toomatch вашей среде.
    - ```$subscriptionName = ‘Visual Studio Ultimate with MSDN’``` (У вашей подписки может быть другое имя. Вы увидите его как часть hello выходные данные предыдущей команды hello.)
    - ```$location = 'West US'```(Эта переменная будет расположение используемых toopass hello, которой должен быть создан ресурсы. Можно изменить этот переменной toobe любой папку по своему усмотрению.)
    - ```$random = Get-Random```
    - ``` $name = 'azlogtest' + $random```(имя hello может быть любым, но оно должно включать только строчные буквы и цифры).
    - ``` $storageName = $name```(Эта переменная будет использоваться hello имени учетной записи хранения.)
    - ```$rgname = $name ```(Эта переменная будет использоваться для имени группы ресурсов hello.)
    - ``` $eventHubNameSpaceName = $name```(Это имя hello hello пространство имен концентратора событий).
6. Укажите hello подписку, которая будет использоваться с:
    
    ```Select-AzureRmSubscription -SubscriptionName $subscriptionName```
7. Создайте группу ресурсов:
    
    ```$rg = New-AzureRmResourceGroup -Name $rgname -Location $location```
    
   Если ввести `$rg` на этом этапе вы увидите примерно toothis экрана выходные данные:

   ![Выходные данные после создания группы ресурсов](./media/security-azure-log-integration-keyvault-eventhub/create-rg.png)
8. Создайте учетную запись хранилища, который будет использоваться tookeep отслеживания сведений о состоянии:
    
    ```$storage = New-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename -Location $location -SkuName Standard_LRS```
9. Создайте пространство имен концентратора событий hello. Это обязательный toocreate концентратора событий.
    
    ```$eventHubNameSpace = New-AzureRmEventHubNamespace -ResourceGroupName $rgname -NamespaceName $eventHubnamespaceName -Location $location```
10. Получите идентификатор правила hello, который будет использоваться с поставщиком аналитики hello:
    
    ```$sbruleid = $eventHubNameSpace.Id +'/authorizationrules/RootManageSharedAccessKey' ```
11. Получить все возможные местоположения Azure и добавьте hello имена tooa переменную, которая может использоваться в дальнейшем.
    
    а. ```$locationObjects = Get-AzureRMLocation```    
    b. ```$locations = @('global') + $locationobjects.location```
    
    Если ввести `$locations` на этом этапе имена можно увидеть hello расположение без hello дополнительные данные, возвращаемые командлетом Get-AzureRmLocation.
12. Создайте профиль журнала Azure Resource Manager: 
    
    ```Add-AzureRmLogProfile -Name $name -ServiceBusRuleId $sbruleid -Locations $locations```
    
    Дополнительные сведения о hello Azure log профиль в разделе [Обзор hello журнал действий Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md).

> [!NOTE]
> Может появиться сообщение об ошибке при попытке toocreate профиля журнала. Затем можно просматривать документацию hello для Get-AzureRmLogProfile и Remove AzureRmLogProfile. При выполнении Get-AzureRmLogProfile появиться сведения о профиле журнала hello. Можно удалить существующий профиль журнала hello, введя hello ```Remove-AzureRmLogProfile -name 'Log Profile Name' ``` команды.
>
>![Ошибка профиля Resource Manager](./media/security-azure-log-integration-keyvault-eventhub/rm-profile-error.png)

## <a name="create-a-key-vault"></a>Создайте хранилище ключей.

1. Создание хранилища ключей hello:

   ```$kv = New-AzureRmKeyVault -VaultName $name -ResourceGroupName $rgname -Location $location ```

2. Настройка ведения журнала для хранилища ключей hello:

   ```Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -ServiceBusRuleId $sbruleid -Enabled $true ```

## <a name="generate-log-activity"></a>Создание действия журнала

Запросы должны toobe отправлено tooKey хранилище toogenerate журнала действий. Действия, например создание ключей, хранение секретов или чтение секретов из Key Vault, будут создавать записи в журнале.

1. Для отображения текущего хранилища ключей hello:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
2. Создайте ключ **key2**:
    
   ```New-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname -KeyName key2```
3. Показывать ключи hello и видеть, что **key2** содержит другое значение:
    
   ```Get-AzureRmStorageAccountKey -Name $storagename -ResourceGroupName $rgname  | ft -a```
4. Установка и считывание секретный toogenerate дополнительные записи журнала:
    
   а. ```Set-AzureKeyVaultSecret -VaultName $name -Name TestSecret -SecretValue (ConvertTo-SecureString -String 'Hi There!' -AsPlainText -Force)``` Б. ```(Get-AzureKeyVaultSecret -VaultName $name -Name TestSecret).SecretValueText```

   ![Возвращенный секрет](./media/security-azure-log-integration-keyvault-eventhub/keyvaultsecret.png)


## <a name="configure-azure-log-integration"></a>Настройка интеграции журналов Azure

Настройки всех концентратора событий tooan ведения журнала хранилища ключей hello обязательные элементы toohave требуется tooconfigure интеграции журнала Azure:

1. ```$storage = Get-AzureRmStorageAccount -ResourceGroupName $rgname -Name $storagename```
2. ```$eventHubKey = Get-AzureRmEventHubNamespaceKey -ResourceGroupName $rgname -NamespaceName $eventHubNamespace.name -AuthorizationRuleName RootManageSharedAccessKey```
3. ```$storagekeys = Get-AzureRmStorageAccountKey -ResourceGroupName $rgname -Name $storagename```
4. ``` $storagekey = $storagekeys[0].Value```

Выполните команду AzLog hello для каждого концентратора событий:

1. ```$eventhubs = Get-AzureRmEventHub -ResourceGroupName $rgname -NamespaceName $eventHubNamespaceName```
2. ```$eventhubs.Name | %{Add-AzLogEventSource -Name $sub' - '$_ -StorageAccount $storage.StorageAccountName -StorageKey $storageKey -EventHubConnectionString $eventHubKey.PrimaryConnectionString -EventHubName $_}```

После минуты или это выполнения hello последние две команды вы должны увидеть создаваемых файлов JSON. Подтвердите отслеживания каталога hello **C:\users\AzLog\EventHubJson**.

## <a name="next-steps"></a>Дальнейшие действия

- [Интеграция журналов Azure: часто задаваемые вопросы](security-azure-log-integration-faq.md)
- [Приступая к работе со службой интеграции журналов Azure](security-azure-log-integration-get-started.md)
- [Интеграция журналов из ресурсов Azure в системы SIEM](security-azure-log-integration-overview.md)
