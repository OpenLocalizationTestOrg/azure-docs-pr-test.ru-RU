---
title: "кластер Service Fabric aaaCreate в hello портал Azure | Документы Microsoft"
description: "В этой статье описывается, как hello tooset безопасности кластера Service Fabric в Azure с помощью портала Azure и хранилищем ключей Azure."
services: service-fabric
documentationcenter: .net
author: chackdan
manager: timlt
editor: vturecek
ms.assetid: 426c3d13-127a-49eb-a54c-6bde7c87a83b
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/21/2017
ms.author: chackdan
ms.openlocfilehash: 045f71b491260e741ce7a54a75c440e1b33059a8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-hello-azure-portal"></a>Создание кластера Service Fabric в Azure с помощью портала Azure hello
> [!div class="op_single_selector"]
> * [Диспетчер ресурсов Azure](service-fabric-cluster-creation-via-arm.md)
> * [Портал Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Это пошаговое руководство, которое поможет выполнить действия hello настройки безопасности кластера Service Fabric в Azure с помощью портала Azure hello. Это руководство поможет выполнить следующие шаги hello:

* Настройка хранилища ключей toomanage ключей для обеспечения безопасности кластера.
* Создание защищенных кластеров в Azure через портал Azure hello.
* Аутентификация администраторов с помощью сертификатов.

> [!NOTE]
> Для обеспечения дополнительных параметров безопасности, таких как аутентификация пользователей с помощью Azure Active Directory и настройка сертификатов для безопасности приложений, [создайте кластер с помощью Azure Resource Manager][create-cluster-arm].
> 
> 

Безопасный кластер представляет кластер, запрещающую операции toomanagement несанкционированного доступа, включая развертывание, обновление и удаление приложений, служб и данных hello, которые они содержат. Небезопасные кластер — это кластер, что любой пользователь может подключиться tooat в любое время и выполнять операции управления. Хотя это возможно toocreate небезопасные кластера, это **безопасного кластера настоятельно рекомендуется toocreate**. Незащищенный кластер **невозможно будет защитить позднее** , для этого нужно будет создать новый кластер.

Основные понятия Hello hello же для создания защищенных кластеров hello кластеры, кластеры Linux или кластерах Windows. Дополнительные сведения о создании безопасных кластеров Linux, а также вспомогательные скрипты см. в статье [Создание безопасных кластеров в Linux](service-fabric-cluster-creation-via-arm.md#secure-linux-clusters). Hello параметры, получаемые с hello вспомогательный сценария, предоставленного могут быть введены непосредственно в портал hello как описано в разделе "hello" [создания кластера в hello портал Azure](#create-cluster-portal).

## <a name="log-in-tooazure"></a>Войдите в tooAzure
В этом руководстве используется [Azure PowerShell][azure-powershell]. При запуске нового сеанса PowerShell, войдите в tooyour учетная запись Azure и выберите подписку перед выполнением команды Azure.

Войдите в учетную запись tooyour azure:

```powershell
Login-AzureRmAccount
```

Выберите свою подписку.

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

## <a name="set-up-key-vault"></a>Настройка хранилища ключей
В этой части руководства hello описывается создание хранилища ключей для кластера Service Fabric в Azure и для приложения Service Fabric. Полное руководство по в хранилище ключей, в разделе hello [хранилище ключей Знакомство с][key-vault-get-started].

Service Fabric использует сертификаты X.509 toosecure кластера. Хранилище ключей Azure является toomanage используемые сертификаты для кластеров Service Fabric в Azure. При развертывании в Azure, ответственный за создание кластеров Service Fabric поставщика ресурсов Azure hello извлекает сертификаты из хранилища ключей и устанавливает их на hello кластера виртуальных машин.

Hello следующей схеме показана связь hello хранилище ключей, кластер Service Fabric и hello поставщика ресурсов Azure, которая использует сертификаты, хранящиеся в хранилище ключей при создании кластера.

![Установка сертификата][cluster-security-cert-installation]

### <a name="create-a-resource-group"></a>Создание группы ресурсов
Hello первым шагом является toocreate группы ресурсов, в частности для хранилища ключей. Размещение в собственной группе ресурсов хранилища ключей рекомендуется, чтобы можно было удалить вычислений и хранения групп ресурсов — например, группа ресурсов hello, имеющий кластера Service Fabric — без потери ключи и секретные коды. Группа ресурсов Hello с вашего хранилища ключей должен быть в hello же регионе, что кластер hello, он используется.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: hello output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

### <a name="create-key-vault"></a>Создание хранилища ключей
Создание хранилища ключей в новую группу ресурсов hello. Hello хранилище ключей **должна быть включена для развертывания** tooallow hello Service Fabric сертификаты tooget поставщика ресурсов из него и установить на узлах кластера:

```powershell

    PS C:\Users\vturecek> New-AzureRmKeyVault -VaultName 'myvault' -ResourceGroupName 'mycluster-keyvault' -Location 'West US' -EnabledForDeployment


    Vault Name                       : myvault
    Resource Group Name              : mycluster-keyvault
    Location                         : West US
    Resource ID                      : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault
    Vault URI                        : https://myvault.vault.azure.net
    Tenant ID                        : <guid>
    SKU                              : Standard
    Enabled For Deployment?          : False
    Enabled For Template Deployment? : False
    Enabled For Disk Encryption?     : False
    Access Policies                  :
                                       Tenant ID                :    <guid>
                                       Object ID                :    <guid>
                                       Application ID           :
                                       Display Name             :    
                                       Permissions tooKeys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions tooSecrets   :    all


    Tags                             :
```

При наличии существующего хранилища ключей можно сделать его доступным для развертывания с помощью командной строки Azure (Azure CLI).

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


## <a name="add-certificates-tookey-vault"></a>Добавьте сертификаты tooKey хранилища
Сертификаты используются в Service Fabric tooprovide проверки подлинности и шифрования toosecure различные аспекты кластера и его применения. Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].

### <a name="cluster-and-server-certificate-required"></a>Сертификат кластера и сервера (обязательно)
Этот сертификат является обязательным toosecure кластером и предотвратить несанкционированный доступ tooit. Он обеспечивает безопасность кластера несколькими способами.

* **Аутентификация в кластере** позволяет аутентифицировать обмен данными между узлами для федерации кластера. Только узлы, которые можно подтвердить свою личность с помощью этого сертификата можно соединить hello кластера.
* **Проверка подлинности сервера:** проверяет подлинность hello кластера управления конечными точками tooa клиента управления, чтобы hello управления клиент узнает, осуществляет обмен данными toohello реальные кластера. Этот сертификат также предоставляет SSL для hello API управления HTTPS и обозреватель Service Fabric по протоколу HTTPS.

tooserve этих целей, hello сертификат должен удовлетворять hello следующие требования:

* Hello сертификат должен содержать закрытый ключ.
* необходимо создать сертификат Hello для обмена ключами, tooa экспортируемый файл обмена личной информацией (PFX-файл).
* Hello имя субъекта сертификата должно соответствовать кластера Service Fabric hello tooaccess домен, используемый hello. Это обязательный tooprovide SSL для конечных точек управления HTTPS и обозреватель Service Fabric hello кластера. Не удается получить SSL-сертификат центра сертификации (ЦС), для hello `.cloudapp.azure.com` домена. Необходимо получить имя личного домена для кластера. При запросе сертификата из имени субъекта сертификата hello ЦС должно соответствовать имени пользовательского домена hello, используемые для кластера.

### <a name="client-authentication-certificates"></a>Сертификаты проверки подлинности клиента
Дополнительные сертификаты клиента используются для аутентификации администраторов при выполнении задач управления кластером. Service Fabric имеет два уровня доступа: **администратор** и **пользователь только для чтения**. Необходимо использовать хотя бы один сертификат для административного доступа. Для получения дополнительного доступа на уровне пользователя необходимо предоставить отдельный сертификат. Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric][service-fabric-cluster-security-roles].

Не обязательно tooupload клиента проверки подлинности сертификатов tooKey хранилище toowork в Service Fabric. Эти сертификаты должны только toobe предоставленный toousers, авторизованных для управления кластером. 

> [!NOTE]
> Azure Active Directory является hello рекомендуется клиентов tooauthenticate способом для кластера операций управления. toouse Azure Active Directory необходимо [создание кластера с помощью диспетчера ресурсов Azure][create-cluster-arm].
> 
> 

### <a name="application-certificates-optional"></a>Сертификаты приложения (необязательно)
В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений. Перед созданием кластера, рассмотрим hello безопасности приложений, требующих toobe сертификатов, установленных на узлах hello, такие как:

* шифрование и расшифровка значений конфигурации приложений;
* шифрование данных между узлами во время репликации. 

При создании кластера с помощью портала Azure hello сертификатов приложения нельзя настроить. сертификаты tooconfigure приложения во время установки кластера, необходимо [создание кластера с помощью диспетчера ресурсов Azure][create-cluster-arm]. Можно также добавить кластера toohello сертификаты приложения после его создания.

### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Форматирование сертификатов для использования поставщиком ресурсов Azure
Файлы закрытого ключа (PFX-файлы) можно добавить в хранилище ключей и использовать непосредственно из него. Однако hello поставщика ресурсов Azure требует toobe ключи, хранящиеся в специальном формате JSON, включающий hello PFX-файл в Base64-кодировке строки и hello пароль закрытого ключа. tooaccommodate эти требования ключей необходимо поместить в строку JSON и сохраняется как *секреты* в хранилище ключей.

модуль PowerShell — toomake удобным это процесс, [на сайте GitHub][service-fabric-rp-helpers]. Выполните эти шаги toouse hello модуля.

1. Загрузите все содержимое репозитория hello hello в локальный каталог. 
2. Импорт модуля hello в окне PowerShell:

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Hello `Invoke-AddCertToKeyVault` команды в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строке JSON и отправляет его tooKey хранилища. Используйте сертификат кластера hello tooadd и любые дополнительные приложения сертификаты tooKey хранилища. Повторите это действие другие сертификаты, требуется tooinstall в кластере.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context tooSubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: hello output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret toomyvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Это все предварительные условия hello хранилища ключей для настройки шаблона диспетчера ресурсов кластера Service Fabric, устанавливает сертификаты для проверки подлинности узла, безопасность конечной точки управления и проверки подлинности и любые дополнительная безопасность приложений функции, которые используют сертификаты X.509. На этом этапе вы добавили hello, после завершения программы установки в Azure:

* группа ресурсов хранилища ключей;
  * хранилище ключей;
    * сертификат проверки подлинности сервера кластера;

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-hello-azure-portal"></a>Создание кластера в hello портал Azure
### <a name="search-for-hello-service-fabric-cluster-resource"></a>Поиск hello ресурса кластера Service Fabric
![Поиск шаблона кластера Service Fabric на hello портал Azure.][SearchforServiceFabricClusterTemplate]

1. Войдите в toohello [портал Azure][azure-portal].
2. Нажмите кнопку **New** tooadd новый шаблон ресурсов. Поиск шаблона кластера Service Fabric hello в hello **Marketplace** под **все**.
3. Выберите **кластера Service Fabric** из списка hello.
4. Перейдите toohello **кластера Service Fabric** колонка, щелкните **создать**,
5. Hello **кластера Service Fabric создать** колонке имеет hello следующие четыре шага.

#### <a name="1-basics"></a>1. Основы
![Снимок экрана: создание группы ресурсов.][CreateRG]

В колонке основы hello необходимо tooprovide hello основные сведения для кластера.

1. Введите имя кластера hello.
2. Введите **имя пользователя** и **пароль** для удаленного рабочего стола для hello виртуальных машин.
3. Убедитесь, что hello tooselect **подписки** требуется toobe вашего кластера, развертывания, особенно в том случае, если у вас несколько подписок.
4. Создайте **новую группу ресурсов**. Это наиболее toogive hello совпадает с именем кластера hello, так как он помогает в поиске их позднее, особенно в том случае, если выполняется развертывание tooyour toomake изменения или удаления кластера.
   
   > [!NOTE]
   > Несмотря на то, что toouse существующую группу ресурсов, можно определить, является хорошей практикой toocreate новую группу ресурсов. Это позволяет легко toodelete кластеры, которые не требуется.
   > 
   > 
5. Выберите hello **область** требуется toocreate hello кластера. Необходимо использовать hello не совпадают, ваш ключ в хранилище.

#### <a name="2-cluster-configuration"></a>2. Конфигурация кластера
![Создание типа узла][CreateNodeType]

Настройте узлы кластера. Типы узлов определяют размеры виртуальных Машин hello, hello число виртуальных машин и их свойства. Кластер может иметь более одного типа узла, но тип основного узла hello (hello первое заданное вами на портале hello) должен иметь по крайней мере пять ВМ, так как этот тип узла hello там, где размещены службы структуры системных служб. Не настраивайте параметры **Свойства размещения** , так как стандартное свойство размещения NodeTypeName добавляется автоматически.

> [!NOTE]
> Распространенный сценарий для нескольких типов узлов — это приложение, содержащее интерфейсную и серверную службы. Вы tooput hello клиентской службы на более мелкие виртуальных машинах (размеры виртуальных Машин как D2) toohello открытых портов Интернета, но чтобы tooput hello внутренней службы на ВМ большего размера (с размеры виртуальных Машин как D4, D6, D15 и т. д) с нет открытых портов с выходом в Интернет.
> 
> 

1. Выберите имя для вашего типа узла (1 too12 знаков, содержащий только буквы и цифры).
2. Минимальная Hello **размер** виртуальных машин для hello основном узле типа определяется hello **устойчивость** уровня, выберите для hello кластера. по умолчанию Hello hello уровень устойчивости, бронза. Дополнительные сведения об устойчивости см. в разделе [как hello toochoose Service Fabric кластера, надежность и устойчивость][service-fabric-cluster-capacity].
3. Выберите размер виртуальной Машины hello и ценовой категории. Виртуальные машины серии D оснащены твердотельными накопителями (SSD) и настоятельно рекомендуются для приложений с отслеживанием состояния. Не используйте SKU виртуальной машины с частичными ядрами и менее чем 7 ГБ свободного места на диске. 
4. Минимальная Hello **номер** виртуальных машин для hello основном узле типа определяется hello **надежности** выборе уровня. по умолчанию Hello hello уровень надежности, серебряный. Дополнительные сведения о надежности см. в разделе [как hello toochoose Service Fabric кластера, надежность и устойчивость][service-fabric-cluster-capacity].
5. Выберите hello число виртуальных машин для типа узла hello. Можно масштабировать вверх или вниз hello число виртуальных машин в тип узла позднее, но на тип основного узла hello, минимальное hello определяется уровень надежности hello, которые были выбраны. Для других типов узлов можно задать минимум 1 виртуальную машину.
6. Настройте пользовательские конечные точки. Это поле позволяет tooenter запятыми список портов, которые должны tooexpose через toohello подсистемы балансировки нагрузки Azure hello общедоступный Интернет для ваших приложений. Например, если планируется toodeploy веб-приложения tooyour кластера, введите «80» здесь tooallow трафик через порт 80 в кластере. Дополнительные сведения о конечных точках см. в статье [Подключение к службам в Service Fabric и взаимодействие с ними][service-fabric-connect-and-communicate-with-services].
7. Настройте **систему диагностики** кластера. По умолчанию включены диагностические сообщения на ваш tooassist кластера при устранении неполадок. Чтобы изменить диагностику toodisable hello **состояние** переключения слишком**Off**. Отключать систему диагностики **не** рекомендуется.
8. Выберите hello структуры обновление в режиме, необходимо задать кластера. Выберите **автоматического**, если хотите hello системы tooautomatically отгрузки hello последнюю версию и повторите tooupgrade tooit вашего кластера. Установить режим hello слишком**вручную**, если вы хотите toochoose поддерживаемой версии.

> [!NOTE]
> Корпорация Майкрософт поддерживает только кластеры под управлением поддерживаемых версий Service Fabric. Выбрав hello **вручную** режиме делаются на tooupgrade ответственности hello поддерживается tooa версии кластера. См. Дополнительные сведения о режиме обновления Fabric hello hello [документа службы структуры-— обновления кластера.][service-fabric-cluster-upgrade]
> 
> 

#### <a name="3-security"></a>3. Безопасность
![Снимок экрана: настройка безопасности на портале Azure.][SecurityConfigs]

Последний шаг Hello — tooprovide сертификата сведения toosecure hello кластера с помощью hello хранилища ключей и сертификатов, сведения, созданного ранее.

* Заполнить поля основной сертификат hello hello выходные данные, полученные от передачи hello **кластера сертификат** tooKey хранилище, используя hello `Invoke-AddCertToKeyVault` команды PowerShell.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Проверьте hello **Настройка дополнительных параметров** поле tooenter клиентских сертификатов для **администрирования клиента** и **клиента только для чтения**. В этих полях введите отпечаток вашего сертификата клиента администратора hello и hello отпечаток сертификата клиента пользователя только для чтения, если это применимо. Когда администраторы устанавливают tooconnect toohello кластера, предоставляются доступ только в том случае, если они имеют сертификат с отпечатком, соответствующий значениям hello отпечаток введенное здесь.  

#### <a name="4-summary"></a>4. Сводка
![Снимок экрана доски начала hello отображение «Развертывание кластера Service Fabric». ][Notifications]

Создание кластера toocomplete hello, нажмите кнопку **Сводка** toosee hello конфигураций, которые вы указали, или загрузите hello шаблона Azure Resource Manager, который используется toodeploy кластера. После ввода обязательные параметры hello hello **ОК** кнопка становится зеленой, и процесс создания кластера hello можно запустить, щелкнув его.

Вы увидите ход создания hello в уведомлениях hello. (Щелкните значок колокольчика «hello» рядом с hello строку состояния в hello верхнем правом углу экрана.) После щелчка **tooStartboard ПИН-код** при создании кластера hello, вы увидите **развертывание кластера Service Fabric** закрепленные toohello **запустить** платы.

### <a name="view-your-cluster-status"></a>Просмотр состояния кластера
![Снимок экрана: сведения о кластере в панели мониторинга hello.][ClusterDashboard]

После создания кластера можно проверить кластер на портале hello:

1. Go слишком**Обзор** и нажмите кнопку **кластерами структуры службы**.
2. Найдите нужный кластер и щелкните его.
3. Теперь можно просмотреть сведения hello кластера на панели мониторинга hello, включая общедоступную конечную точку кластера hello и ссылка tooService Fabric Explorer.

Hello **монитора узла** раздел на панели мониторинга кластера hello указывает hello число виртуальных машин, которые работоспособны и неработоспособны. Можно найти дополнительные сведения о работоспособности кластера hello в [введение модель работоспособности Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Кластеров Service Fabric требуется определенное количество узлов toobe всегда toomaintain доступности и сохранить состояние - ссылка tooas «поддержания кворума». Поэтому, это обычно не безопасном tooshut работу всех машин в кластере hello Если сначала была выполнена [полного резервного копирования состояния][service-fabric-reliable-services-backup-restore].
> 
> 

## <a name="remote-connect-tooa-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Удаленное подключение tooa набора масштабирования виртуальных машин экземпляра или узла кластера
Каждый из hello NodeTypes задается в результатов в наборе масштабирования виртуальных машин Приступая к настройке кластера. В разделе [удаленного подключения экземпляра набора масштабирования виртуальных машин tooa] [ remote-connect-to-a-vm-scale-set] подробные сведения.

## <a name="next-steps"></a>Дальнейшие действия
На этом этапе у вас имеется защищенный кластер, использующий сертификаты для аутентификации управления. Далее, [подключения кластера tooyour](service-fabric-connect-to-secure-cluster.md) и узнайте, каким образом слишком[управление секретами приложения](service-fabric-application-secret-management.md).  Кроме того, узнайте [о вариантах поддержки Service Fabric](service-fabric-support.md).

<!-- Links -->
[azure-powershell]: https://azure.microsoft.com/documentation/articles/powershell-install-configure/
[service-fabric-rp-helpers]: https://github.com/ChackDan/Service-Fabric/tree/master/Scripts/ServiceFabricRPHelpers
[azure-portal]: https://portal.azure.com/
[key-vault-get-started]: ../key-vault/key-vault-get-started.md
[create-cluster-arm]: service-fabric-cluster-creation-via-arm.md
[service-fabric-cluster-security]: service-fabric-cluster-security.md
[service-fabric-cluster-security-roles]: service-fabric-cluster-security-roles.md
[service-fabric-cluster-capacity]: service-fabric-cluster-capacity.md
[service-fabric-connect-and-communicate-with-services]: service-fabric-connect-and-communicate-with-services.md
[service-fabric-health-introduction]: service-fabric-health-introduction.md
[service-fabric-reliable-services-backup-restore]: service-fabric-reliable-services-backup-restore.md
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-vm-scale-set-instance-or-a-cluster-node
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
