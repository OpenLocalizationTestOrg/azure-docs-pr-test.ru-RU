---
title: "Создание кластера Service Fabric на портале Azure | Документация Майкрософт"
description: "В этой статье описывается настройка защищенного кластера Service Fabric в Azure с помощью портала Azure и хранилища ключей Azure."
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
ms.openlocfilehash: be880efdcf1276252c76f27c2f2fd99edd606caa
ms.sourcegitcommit: 821b6306aab244d2feacbd722f60d99881e9d2a4
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 12/18/2017
---
# <a name="create-a-service-fabric-cluster-in-azure-using-the-azure-portal"></a>Создание кластера Service Fabric в Azure с помощью портала Azure
> [!div class="op_single_selector"]
> * [Azure Resource Manager](service-fabric-cluster-creation-via-arm.md)
> * [Портал Azure](service-fabric-cluster-creation-via-portal.md)
> 
> 

Это пошаговое руководство поможет выполнить настройку защищенного кластера Service Fabric в Azure с помощью портала Azure. Данное руководство описывает следующие действия:

* Настройка хранилища ключей для управления ключами для обеспечения безопасности кластера.
* Создание защищенного кластера в Azure с помощью портала Azure.
* Аутентификация администраторов с помощью сертификатов.

> [!NOTE]
> Для обеспечения дополнительных параметров безопасности, таких как аутентификация пользователей с помощью Azure Active Directory и настройка сертификатов для безопасности приложений, [создайте кластер с помощью Azure Resource Manager][create-cluster-arm].
> 
> 

Защищенный кластер — это кластер, который предотвращает несанкционированный доступ к операциям управления, включая развертывание, обновление и удаление приложений, служб и данных, которые они содержат. Незащищенный кластер — это кластер, к которому в любое время может подключиться любой пользователь и выполнять операции управления. Хотя можно создать незащищенный кластер, **настоятельно рекомендуется создать защищенный кластер**. Незащищенный кластер **невозможно будет защитить позднее** , для этого нужно будет создать новый кластер.

Принципы создания безопасных кластеров в Linux или Windows аналогичны. Дополнительные сведения и вспомогательных сценариев для создания защищенных кластеров Linux, см. в статье [создания защищенных кластеров](service-fabric-cluster-creation-via-arm.md). Параметры, полученные с помощью вспомогательного скрипта, можно указать непосредственно на портале, как описано в разделе [Создание кластера на портале Azure](#create-cluster-portal).

## <a name="configure-key-vault"></a>Настройка Key Vault 
### <a name="log-in-to-azure"></a>Вход в Azure
В этом руководстве используется [Azure PowerShell][azure-powershell]. При запуске нового сеанса PowerShell войдите в свою учетную запись Azure и выберите подписку перед выполнением команд Azure.

Войдите в свою учетную запись Azure.

```powershell
Login-AzureRmAccount
```

Выберите свою подписку.

```powershell
Get-AzureRmSubscription
Set-AzureRmContext -SubscriptionId <guid>
```

### <a name="set-up-key-vault"></a>Настройка хранилища ключей
В этой части руководства описывается создание хранилища ключей для кластера Service Fabric в Azure и для приложений Service Fabric. Полное описание Key Vault см. в [руководстве по началу работы с Key Vault][key-vault-get-started].

Для защиты кластера Service Fabric использует сертификаты X.509. Хранилище ключей Azure используется для управления сертификатами кластеров Service Fabric в Azure. При развертывании кластера в Azure поставщик ресурсов Azure, ответственный за создание кластеров Service Fabric, извлекает сертификаты из хранилища ключей и устанавливает их на виртуальные машины кластера.

На приведенной ниже схеме показана связь между хранилищем ключей, кластером Service Fabric и поставщиком ресурсов Azure, который использует сертификаты из хранилища ключей при создании кластера.

![Установка сертификата][cluster-security-cert-installation]

#### <a name="create-a-resource-group"></a>Создание группы ресурсов
Первым шагом является создание новой группы ресурсов специально для хранилища ключей. Рекомендуется поместить хранилище ключей в собственную группу ресурсов. Это позволит удалять группы вычислительных ресурсов и ресурсов хранилища (например, группу ресурсов с кластером Service Fabric) без потери ключей и секретов. Группа ресурсов с хранилищем ключей должна находиться в том же регионе, что и кластер, который ее использует.

```powershell

    PS C:\Users\vturecek> New-AzureRmResourceGroup -Name mycluster-keyvault -Location 'West US'
    WARNING: The output object type of this cmdlet will be modified in a future release.

    ResourceGroupName : mycluster-keyvault
    Location          : westus
    ProvisioningState : Succeeded
    Tags              :
    ResourceId        : /subscriptions/<guid>/resourceGroups/mycluster-keyvault

```

#### <a name="create-key-vault"></a>Создание хранилища ключей
Создайте хранилище ключей в новой группе ресурсов. Хранилище ключей **должно быть доступно для развертывания**. Это позволит поставщику ресурсов Service Fabric получить из него сертификаты и установить их на узлах кластера.

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
                                       Permissions to Keys      :    get, create, delete, list, update, import, backup, restore
                                       Permissions to Secrets   :    all


    Tags                             :
```

Если у вас есть существующие хранилища ключей, его можно включить для развертывания с использованием одного из следующих способов:

##### <a name="azure-powershell"></a>Azure PowerShell

```powershell
PS C:\Users\vturecek> Set-AzureRmKeyVaultAccessPolicy -VaultName 'myvault' -EnabledForDeployment
```

##### <a name="azure-cli"></a>Azure CLI:

```cli
> azure login
> azure account set "your account"
> azure config mode arm 
> azure keyvault list
> azure keyvault set-policy --vault-name "your vault name" --enabled-for-deployment true
```


### <a name="add-certificates-to-key-vault"></a>Добавление сертификатов в хранилище ключей
Сертификаты используются в Service Fabric, чтобы обеспечить функции аутентификации и шифрования для защиты различных аспектов кластера и его приложений. Дополнительные сведения о том, как сертификаты используются в Service Fabric, см. в статье [Сценарии защиты кластера Service Fabric][service-fabric-cluster-security].

#### <a name="cluster-and-server-certificate-required"></a>Сертификат кластера и сервера (обязательно)
Этот сертификат требуется для защиты кластера и предотвращения несанкционированного доступа к нему. Он обеспечивает безопасность кластера несколькими способами.

* **Аутентификация в кластере** позволяет аутентифицировать обмен данными между узлами для федерации кластера. Только узлы, которые могут подтвердить свою подлинность с помощью этого сертификата, могут присоединиться к кластеру.
* **Аутентификация сервера** позволяет аутентифицировать конечные точки управления кластера в клиенте управления, чтобы он "знал", что обращается к настоящему кластеру. Этот сертификат также предоставляет SSL для API управления HTTPS и Service Fabric Explorer по протоколу HTTPS.

Для этого сертификат должен отвечать следующим требованиям:

* Сертификат должен содержать закрытый ключ.
* Сертификат должен быть создан для обмена ключами, которые можно экспортировать в файл обмена личной информацией (PFX-файл).
* Имя субъекта сертификата должно совпадать с доменным именем, которое используется для обращения к кластеру Service Fabric. Это необходимо, чтобы предоставить протокол SSL для конечных точек управления HTTPS в кластере и Service Fabric Explorer. Невозможно получить SSL-сертификат от центра сертификации (ЦС) для домена `.cloudapp.azure.com` . Необходимо получить имя личного домена для кластера. При запросе сертификата из ЦС имя субъекта сертификата должно совпадать с именем личного домена, используемого для кластера.

#### <a name="client-authentication-certificates"></a>Сертификаты проверки подлинности клиента
Дополнительные сертификаты клиента используются для аутентификации администраторов при выполнении задач управления кластером. Service Fabric имеет два уровня доступа: **администратор** и **пользователь только для чтения**. Необходимо использовать хотя бы один сертификат для административного доступа. Для получения дополнительного доступа на уровне пользователя необходимо предоставить отдельный сертификат. Дополнительные сведения о ролях доступа см. в статье [Контроль доступа на основе ролей для клиентов Service Fabric][service-fabric-cluster-security-roles].

Для работы с Service Fabric не нужно передавать сертификаты проверки подлинности клиента в хранилище ключей. Эти сертификаты должны предоставляться только пользователям, уполномоченным осуществлять управление кластером. 

> [!NOTE]
> Azure Active Directory является рекомендуемым способом аутентификации клиентов при допуске к операциям управления кластером. Для использования Azure Active Directory необходимо [создать кластер с помощью Azure Resource Manager][create-cluster-arm].
> 
> 

#### <a name="application-certificates-optional"></a>Сертификаты приложения (необязательно)
В кластере можно установить любое количество дополнительных сертификатов для обеспечения безопасности приложений. Перед созданием кластера рассмотрите сценарии безопасности приложений, которые требуют установки сертификатов на узлах, в том числе:

* шифрование и расшифровка значений конфигурации приложений;
* шифрование данных между узлами во время репликации. 

При создании кластера с помощью портала Azure настройка сертификатов приложения недоступна. Чтобы настроить сертификаты приложения в процессе настройки кластера, необходимо [создать кластер с помощью Azure Resource Manager][create-cluster-arm]. Также можно добавить сертификаты приложения в кластер после его создания.

#### <a name="formatting-certificates-for-azure-resource-provider-use"></a>Форматирование сертификатов для использования поставщиком ресурсов Azure
Файлы закрытого ключа (PFX-файлы) можно добавить в хранилище ключей и использовать непосредственно из него. Тем не менее поставщику ресурсов Azure необходимо, чтобы ключи хранились в специальном формате JSON, включающем в себя PFX-файл в виде строки в кодировке Base64 и пароль закрытого ключа. Чтобы соблюсти эти требования, ключи должны быть помещены в строку JSON и сохранены как *секреты* в хранилище ключей.

Для упрощения этого процесса [на сайте GitHub][service-fabric-rp-helpers] доступен соответствующий модуль PowerShell. Ниже приведены указания по использованию этого модуля.

1. Скачайте все содержимое репозитория в локальный каталог. 
2. Импортируйте модуль в окне PowerShell.

```powershell
  PS C:\Users\vturecek> Import-Module "C:\users\vturecek\Documents\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"
```

Команда `Invoke-AddCertToKeyVault` в этом модуле PowerShell автоматически форматирует закрытый ключ сертификата в строку JSON и передает ее в хранилище ключей. Используйте его для добавления сертификата кластера и всех дополнительных сертификатов приложения в хранилище ключей. Повторите этот шаг для всех дополнительных сертификатов, которые нужно установить в кластере.

```powershell
PS C:\Users\vturecek> Invoke-AddCertToKeyVault -SubscriptionId <guid> -ResourceGroupName mycluster-keyvault -Location "West US" -VaultName myvault -CertificateName mycert -Password "<password>" -UseExistingCertificate -ExistingPfxFilePath "C:\path\to\mycertkey.pfx"

    Switching context to SubscriptionId <guid>
    Ensuring ResourceGroup mycluster-keyvault in West US
    WARNING: The output object type of this cmdlet will be modified in a future release.
    Using existing valut myvault in West US
    Reading pfx file from C:\path\to\key.pfx
    Writing secret to myvault in vault myvault


Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47

```

Это все обязательные компоненты хранилища ключей, необходимые для настройки шаблона Resource Manager кластера Service Fabric, который устанавливает сертификаты для аутентификации на узлах, защиты конечных точек управления и аутентификации на них, а также для каких-либо дополнительных функций безопасности приложений, которые используют сертификаты X.509. На этом этапе в Azure должна быть представлена следующая конфигурация:

* группа ресурсов хранилища ключей;
  * хранилище ключей;
    * сертификат проверки подлинности сервера кластера;

</a "create-cluster-portal" ></a>

## <a name="create-cluster-in-the-azure-portal"></a>Создание кластера на портале Azure
### <a name="search-for-the-service-fabric-cluster-resource"></a>Поиск кластерных ресурсов Service Fabric
![поиск шаблона кластера Service Fabric на портале Azure.][SearchforServiceFabricClusterTemplate]

1. Войдите на [портал Azure][azure-portal].
2. Щелкните **Создать** , чтобы добавить новый шаблон ресурсов. Найдите шаблон "Кластер Service Fabric" в **Marketplace** в разделе **Все**.
3. Выберите в списке **Кластер Service Fabric** .
4. Перейдите к колонке **Кластер Service Fabric** и выберите **Создать**.
5. В колонке **Создание кластера Service Fabric** необходимо выполнить четыре шага.

#### <a name="1-basics"></a>1. Основы
![Снимок экрана: создание группы ресурсов.][CreateRG]

В колонке "Основные сведения" требуется указать основные сведения для кластера.

1. Введите имя кластера.
2. Введите **имя пользователя** и **пароль** для удаленного рабочего стола виртуальных машин.
3. Выберите **подписку** , в которой вы хотите развернуть кластер, особенно при наличии нескольких подписок.
4. Создайте **новую группу ресурсов**. Рекомендуется присвоить ей имя, совпадающее с именем кластера. Это облегчит дальнейший поиск, особенно при внесении изменений в развертывание или удалении кластера.
   
   > [!NOTE]
   > Хотя вы можете использовать существующую группу ресурсов, рекомендуется создать новую. Это позволит легко удалить ненужные кластеры.
   > 
   > 
5. Выберите **регион** , в котором требуется создать кластер. Необходимо использовать тот же регион, в котором расположено ваше хранилище ключей.

#### <a name="2-cluster-configuration"></a>2. Конфигурация кластера
![Создание типа узла][CreateNodeType]

Настройте узлы кластера. Он определяет размер виртуальных машин, их количество и свойства. Кластер может содержать узлы нескольких типов, однако первичный узел (тот, который вы задали на портале) должен включать не менее пяти виртуальных машин, так как на узлах такого типа расположены системные службы Service Fabric. Не настраивайте параметры **Свойства размещения** , так как стандартное свойство размещения NodeTypeName добавляется автоматически.

> [!NOTE]
> Распространенный сценарий для нескольких типов узлов — это приложение, содержащее интерфейсную и серверную службы. Интерфейсную службу нужно разместить на виртуальных машинах меньшего размера (например, D2) с портами, открытыми для доступа через Интернет, а серверную службу — на более крупных виртуальных машинах (D4, D6, D15 и т. д.) без портов, имеющих выход в Интернет.
> 
> 

1. Выберите имя для типа узла (от 1 до 12 буквенно-цифровых символов).
2. Минимальный **размер** виртуальных машин для первичного узла зависит от выбранного для кластера уровня **устойчивости**. Значение по умолчанию для уровня устойчивости — bronze (бронзовый). Дополнительные сведения об уровнях устойчивости см. в статье [Рекомендации по планированию загрузки кластера Service Fabric][service-fabric-cluster-capacity].
3. Выберите ценовую категорию и размер виртуальной машины. Виртуальные машины серии D оснащены твердотельными накопителями (SSD) и настоятельно рекомендуются для приложений с отслеживанием состояния. Не используйте SKU виртуальной машины с частичными ядрами и менее чем 7 ГБ свободного места на диске. 
4. Минимальное **количество** виртуальных машин для первичного узла зависит от выбранного для кластера уровня **надежности**. Значение по умолчанию для уровня надежности — Silver. Дополнительные сведения о надежности см. в статье [Рекомендации по планированию загрузки кластера Service Fabric][service-fabric-cluster-capacity].
5. Выберите количество виртуальных машин для типа узла. Количество виртуальных машин для типа узла можно увеличить или уменьшить позже, но минимальное количество виртуальных машин на первичном узле зависит от выбранного уровня надежности. Для других типов узлов можно задать минимум 1 виртуальную машину.
6. Настройте пользовательские конечные точки. Это поле позволяет ввести список портов с разделителями-запятыми. С помощью Azure Load Balancer для приложений будет открыт общий доступ через Интернет к указанным здесь портам. Например, если вы планируете развернуть в своем кластере веб-приложение, то введите здесь "80", чтобы разрешить в этом кластере трафик через порт 80. Дополнительные сведения о конечных точках см. в статье [Подключение к службам в Service Fabric и взаимодействие с ними][service-fabric-connect-and-communicate-with-services].
7. Настройте **систему диагностики** кластера. Диагностика в кластере включена по умолчанию. Это упрощает устранение неполадок. Если вы хотите отключить систему диагностики, установите переключатель **Состояние** в положение **Выкл**. Отключать систему диагностики **не** рекомендуется.
8. Выберите режим обновления Service Fabric, который необходимо задать для кластера. Если требуется, чтобы система автоматически получала последнюю версию и выполняла попытку обновить до нее кластер, выберите пункт **Автоматически**. Если вы хотите выбирать поддерживаемую версию, задайте режим **Вручную**.

> [!NOTE]
> Корпорация Майкрософт поддерживает только кластеры под управлением поддерживаемых версий Service Fabric. Выбрав режим **Вручную**, вы принимаете на себя ответственность за обновление кластера до поддерживаемой версии. Дополнительные сведения о режиме обновления Service Fabric см. в статье [Обновление кластера Service Fabric][service-fabric-cluster-upgrade].
> 
> 

#### <a name="3-security"></a>3. Безопасность
![Снимок экрана: настройка безопасности на портале Azure.][SecurityConfigs]

Последним шагом является предоставление сведений о сертификате для защиты кластера с помощью хранилища ключей, а также ранее созданных сведений о сертификате.

* Заполните поля основного сертификата, используя выходные данные, полученные при передаче **сертификата кластера** в хранилище ключей с помощью команды PowerShell `Invoke-AddCertToKeyVault`.

```powershell
Name  : CertificateThumbprint
Value : <value>

Name  : SourceVault
Value : /subscriptions/<guid>/resourceGroups/mycluster-keyvault/providers/Microsoft.KeyVault/vaults/myvault

Name  : CertificateURL
Value : https://myvault.vault.azure.net:443/secrets/mycert/4d087088df974e869f1c0978cb100e47
```

* Установите флажок **Настройка дополнительных параметров**, чтобы ввести сертификаты клиента в поля **Клиент администратора** и **Клиент только для чтения**. В эти поля введите отпечаток сертификата клиента администратора и отпечаток сертификата клиента только для чтения (при наличии). Когда администраторы пытаются подключиться к кластеру, им предоставляется доступ только в том случае, если у них есть сертификат с отпечатком, соответствующим указанным здесь значениям.  

#### <a name="4-summary"></a>4. Сводка

Чтобы завершить создание кластера, выберите **Сводка** и проверьте указанные параметры или скачайте шаблон Azure Resource Manager, который используется для развертывания кластера. После указания обязательных параметров активируется кнопка **ОК**. Нажав ее, вы сможете начать процесс создания кластера.

Ход создания кластера будет отображаться в области уведомлений. (Щелкните значок колокольчика рядом со строкой состояния в правом верхнем углу экрана). Если при создании кластера вы установили флажок **Закрепить на начальной панели**, то на **начальной доске** вы увидите закрепленный элемент **Развертывание кластера Service Fabric**.

### <a name="view-your-cluster-status"></a>Просмотр состояния кластера
![Снимок экрана: сведения о кластере на панели мониторинга.][ClusterDashboard]

После создания кластера его можно просмотреть на портале.

1. Щелкните **Обзор** и выберите **Кластеры Service Fabric**.
2. Найдите нужный кластер и щелкните его.
3. На панели мониторинга отобразятся подробные сведения о кластере, включая общедоступную конечную точку кластера и ссылку на Service Fabric Explorer.

В разделе **Монитор узла** колонки панели мониторинга кластера отображается количество работоспособных и неработоспособных виртуальных машин. Дополнительные сведения о состоянии работоспособности кластеров см. в статье [Общие сведения о наблюдении за работоспособностью системы в Service Fabric][service-fabric-health-introduction].

> [!NOTE]
> Для постоянной работы кластеров Service Fabric требуется определенное количество узлов, чтобы все время поддерживать доступность и сохранять состояние, которое называется "поддержание кворума". Поэтому обычно не рекомендуется завершать работу всех виртуальных машин в кластере, пока не будет выполнена [полная архивация состояния][service-fabric-reliable-services-backup-restore], так как это может быть небезопасно.
> 
> 

## <a name="remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node"></a>Удаленное подключение к экземпляру из набора масштабирования виртуальных машин или узлу кластера
Каждый из типов узлов, задаваемый в кластере, отражается на конфигурации масштабируемого набора виртуальных машин. <!--See [Remote connect to a Virtual Machine Scale Set instance][remote-connect-to-a-vm-scale-set] for details. -->

## <a name="next-steps"></a>Дальнейшие действия
На этом этапе у вас имеется защищенный кластер, использующий сертификаты для аутентификации управления. Далее [подключитесь к этому кластеру](service-fabric-connect-to-secure-cluster.md) и узнайте, как [управлять секретами приложений](service-fabric-application-secret-management.md).  Кроме того, узнайте [о вариантах поддержки Service Fabric](service-fabric-support.md).

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
<!--[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md#remote-connect-to-a-virtual-machine-scale-set-instance-or-a-cluster-node -->
[remote-connect-to-a-vm-scale-set]: service-fabric-cluster-nodetypes.md
[service-fabric-cluster-upgrade]: service-fabric-cluster-upgrade.md

<!--Image references-->
[SearchforServiceFabricClusterTemplate]: ./media/service-fabric-cluster-creation-via-portal/SearchforServiceFabricClusterTemplate.png
[CreateRG]: ./media/service-fabric-cluster-creation-via-portal/CreateRG.png
[CreateNodeType]: ./media/service-fabric-cluster-creation-via-portal/NodeType.png
[SecurityConfigs]: ./media/service-fabric-cluster-creation-via-portal/SecurityConfigs.png
[Notifications]: ./media/service-fabric-cluster-creation-via-portal/notifications.png
[ClusterDashboard]: ./media/service-fabric-cluster-creation-via-portal/ClusterDashboard.png
[cluster-security-cert-installation]: ./media/service-fabric-cluster-creation-via-arm/cluster-security-cert-installation.png
