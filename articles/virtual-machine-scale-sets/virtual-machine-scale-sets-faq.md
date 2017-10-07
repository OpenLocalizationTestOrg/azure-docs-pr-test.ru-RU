---
title: "часто задаваемые вопросы о задает aaaAzure масштабирования виртуальных машин | Документы Microsoft"
description: "Получите ответы toofrequently вопросы и ответы о наборы масштабирования виртуальных машин."
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 76ac7fd7-2e05-4762-88ca-3b499e87906e
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/20/2017
ms.author: negat
ms.custom: na
ms.openlocfilehash: 0deb9e2bb79f87f17bbf748397b94dc53070cfbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machine-scale-sets-faqs"></a>Часто задаваемые вопросы о масштабируемых наборах виртуальных машин Azure

Ответы задает toofrequently вопросы и ответы о масштабирования виртуальных машин в Azure.

## <a name="autoscale"></a>Autoscale

### <a name="what-are-best-practices-for-azure-autoscale"></a>Существуют ли рекомендации по автомасштабированию Azure?

Рекомендации по автомасштабированию виртуальных компонентов см. в [этой статье](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-best-practices).

### <a name="where-do-i-find-metric-names-for-autoscaling-that-uses-host-based-metrics"></a>Где можно найти имена метрик на основе узла, используемые в процессе автомасштабирования?

Имена метрик на основе узла, используемые в процессе автомасштабирования, перечислены в статье [Метрики, поддерживаемые Azure Monitor](https://azure.microsoft.com/documentation/articles/monitoring-supported-metrics/).

### <a name="are-there-any-examples-of-autoscaling-based-on-an-azure-service-bus-topic-and-queue-length"></a>Существуют ли какие-либо образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure?

Да. Образцы автомасштабирования на основе раздела или длины очереди служебной шины Azure см. в статье [Общие метрики автомасштабирования Azure Monitor](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/).

Для очереди Service Bus используйте следующий JSON hello:

```json
"metricName": "MessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ServiceBus/namespaces/mySB/queues/myqueue"
```

Для очереди службы хранилища используйте следующий JSON hello:

```json
"metricName": "ApproximateMessageCount",
"metricNamespace": "",
"metricResourceUri": "/subscriptions/s1/resourceGroups/rg1/providers/Microsoft.ClassicStorage/storageAccounts/mystorage/services/queue/queues/mystoragequeue"
```

Замените примеры значений соответствующими универсальными кодами ресурсов (URI).


### <a name="should-i-autoscale-by-using-host-based-metrics-or-a-diagnostics-extension"></a>Следует ли выполнять автомасштабирование с использованием метрик на основе узла или с применением расширения диагностики?

Можно создать параметров автоматического масштабирования для метрик уровня узла виртуальных Машин toouse или гостевой ОС на базе метрики.

Список поддерживаемых метрик см. в статье [Общие метрики автомасштабирования Azure Monitor](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-autoscale-common-metrics). 

Полное определение конфигурации масштабируемых наборов см. в статье [Расширенная настройка автомасштабирования с помощью шаблонов Resource Manager для масштабируемых наборов виртуальных машин](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-advanced-autoscale-virtual-machine-scale-sets). 

Образец Hello использует метрики ЦП на уровне узла hello и метрики число сообщений.



### <a name="how-do-i-set-alert-rules-on-a-virtual-machine-scale-set"></a>Как можно задать правила оповещений в масштабируемом наборе виртуальных машин?

Оповещения на основе метрик в масштабируемых наборах виртуальных машин можно создать с помощью PowerShell или Azure CLI. Дополнительные сведения см. в разделе [Создание правил генерации оповещений](https://azure.microsoft.com/documentation/articles/insights-powershell-samples/#create-alert-rules) и [Работа с оповещениями](https://azure.microsoft.com/documentation/articles/insights-cli-samples/#work-with-alerts).

Hello идентификатором TargetResourceId набора масштабирования виртуальной машины hello выглядит следующим образом: 

/subscriptions/идентификатор_подписки/resourceGroups/группа_ресурсов/providers/Microsoft.Compute/virtualMachineScaleSets/имя_набора.

Можно выбрать любого счетчика производительности виртуальной Машины как метрики tooset hello оповещение для. Дополнительные сведения см. в разделе [показатели гостевой ОС для виртуальных машин на основе диспетчера ресурсов Windows](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-resource-manager-based-windows-vms) и [показатели гостевой ОС для ВМ Linux](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/#guest-os-metrics-linux-vms) в hello [общих метрик автоматическое масштабирование Azure монитор](https://azure.microsoft.com/documentation/articles/insights-autoscale-common-metrics/)статьи.

### <a name="how-do-i-set-up-autoscale-on-a-virtual-machine-scale-set-by-using-powershell"></a>Как можно задать параметры автомасштабирования в масштабируемом наборе виртуальных машин с помощью PowerShell?

tooset копирование автомасштабирования на значение с помощью PowerShell, масштабирования виртуальных машин см. hello блога [как задать tooan автомасштабирования tooadd масштабирования виртуальной машины Azure](https://msftstack.wordpress.com/2017/03/05/how-to-add-autoscale-to-an-azure-vm-scale-set/).




## <a name="certificates"></a>Сертификаты

### <a name="how-do-i-securely-ship-a-certificate-toohello-vm-how-do-i-provision-a-virtual-machine-scale-set-toorun-a-website-where-hello-ssl-for-hello-website-is-shipped-securely-from-a-certificate-configuration-hello-common-certificate-rotation-operation-would-be-almost-hello-same-as-a-configuration-update-operation-do-you-have-an-example-of-how-toodo-this"></a>Как безопасно выдать сертификат toohello виртуальной Машины? Как подготовить toorun набор масштабирования виртуальной машины веб-сайт, где hello SSL для веб-сайта hello поставляется безопасно из конфигурации сертификата? (hello распространенная операция смены сертификата может быть практически hello такой же, как операция обновления настройки.) У вас есть пример toodo это? 

toosecurely отправить сертификат toohello виртуальной Машины, можно установить сертификат клиента непосредственно в хранилище сертификатов Windows из хранилища ключей hello клиента.

Используйте следующие JSON hello.

```json
"secrets": [
    {
        "sourceVault": {
            "id": "/subscriptions/{subscriptionid}/resourceGroups/myrg1/providers/Microsoft.KeyVault/vaults/mykeyvault1"
        },
        "vaultCertificates": [
            {
                "certificateUrl": "https://mykeyvault1.vault.azure.net/secrets/{secretname}/{secret-version}",
                "certificateStore": "certificateStoreName"
            }
        ]
    }
]
```

Код Hello поддерживает Windows и Linux.

Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/mt589035.aspx).


### <a name="example-of-self-signed-certificate"></a>Пример самозаверяющего сертификата

1.  Создайте самозаверяющий сертификат в хранилище ключей.

    Используйте следующие команды PowerShell hello.

    ```powershell
    Import-Module "C:\Users\mikhegn\Downloads\Service-Fabric-master\Scripts\ServiceFabricRPHelpers\ServiceFabricRPHelpers.psm1"

    Login-AzureRmAccount

    Invoke-AddCertToKeyVault -SubscriptionId <Your SubID> -ResourceGroupName KeyVault -Location westus -VaultName MikhegnVault -CertificateName VMSSCert -Password VmssCert -CreateSelfSignedCertificate -DnsName vmss.mikhegn.azure.com -OutputPath c:\users\mikhegn\desktop\
    ```

    Это команда дает hello входных данных для шаблона Azure Resource Manager hello.

    Пример toocreate самозаверяющий сертификат в хранилище ключей, в статье [сценарии безопасности кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/).

2.  Изменение шаблона диспетчера ресурсов hello.

    Это свойство добавлено слишком**virtualMachineProfile**, как часть hello ресурса набора масштабирования виртуальных машин:

    ```json 
    "osProfile": {
        "computerNamePrefix": "[variables('namingInfix')]",
        "adminUsername": "[parameters('adminUsername')]",
        "adminPassword": "[parameters('adminPassword')]",
        "secrets": [
            {
                "sourceVault": {
                    "id": "[resourceId('KeyVault', 'Microsoft.KeyVault/vaults', 'MikhegnVault')]"
                },
                "vaultCertificates": [
                    {
                        "certificateUrl": "https://mikhegnvault.vault.azure.net:443/secrets/VMSSCert/20709ca8faee4abb84bc6f4611b088a4",
                        "certificateStore": "My"
                    }
                ]
            }
        ]
    }
    ```
  

### <a name="can-i-specify-an-ssh-key-pair-toouse-for-ssh-authentication-with-a-linux-virtual-machine-scale-set-from-a-resource-manager-template"></a>Можно указать toouse пару ключей SSH для проверки подлинности SSH с набор из шаблона диспетчера ресурсов масштабирования виртуальных машин Linux?  

Да. Hello API-интерфейса REST для **osProfile** — примерно toohello Стандартная виртуальная машина API-интерфейса REST. 

Включите раздел **osProfile** в свой шаблон:

```json 
"osProfile": {
    "computerName": "[variables('vmName')]",
    "adminUsername": "[parameters('adminUserName')]",
    "linuxConfiguration": {
        "disablePasswordAuthentication": "true",
        "ssh": {
            "publicKeys": [
                {
                    "path": "[variables('sshKeyPath')]",
                    "keyData": "[parameters('sshKeyData')]"
                }
            ]
        }
    }
}
```
 
Этот блок JSON используется в [GitHub краткого hello 101 ВМ ключа SSH шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).
 
Hello профиль ОС также используется в [grelayhost.json hello GitHub быстрого запуска шаблона](https://github.com/ExchMaster/gadgetron/blob/master/Gadgetron/Templates/grelayhost.json).

Дополнительные сведения см. в разделе о [создании и обновлении масштабируемого набора виртуальных машин](https://msdn.microsoft.com/library/azure/mt589035.aspx#linuxconfiguration).
  

### <a name="how-do-i-remove-deprecated-certificates"></a>Как удалить устаревшие сертификаты? 

tooremove рекомендуется использовать сертификаты, hello удалить старый сертификат из списка сертификатов hello хранилища. Оставьте все сертификаты hello требуется tooremain на компьютере, в списке hello. Этот сертификат не будет удален hello из всех виртуальных машин. Он также добавляет сертификат hello toonew виртуальных машин, которые создаются в наборе масштабирования виртуальных машин hello. 

tooremove hello сертификат из существующих виртуальных машин, написать сценарий пользовательские расширения toomanually remove hello сертификаты из хранилища сертификатов.
 
### <a name="how-do-i-inject-an-existing-ssh-public-key-into-hello-virtual-machine-scale-set-ssh-layer-during-provisioning-i-want-toostore-hello-ssh-public-key-values-in-azure-key-vault-and-then-use-them-in-my-resource-manager-template"></a>Как вставить существующий открытый ключ SSH в hello виртуальной машины шкалы набор SSH слоя во время инициализации? Я toostore hello SSH открытого ключа значений в хранилище ключей Azure и затем использовать их в шаблон диспетчера ресурсов.

Если вы указываете hello виртуальные машины только с помощью открытого ключа SSH, нет необходимости tooput hello открытых ключей в хранилище ключей. Открытые ключи не являются секретом.
 
При создании виртуальной машины Linux открытые ключи SSH можно указать в обычном текстовом формате.

```json
"linuxConfiguration": {
    "ssh": {
        "publicKeys": [
            {
                "path": "path",
                "keyData": "publickey"
            }
        ]
    }
```
 
Имя элемента конфигурации Linux | Обязательно | Тип | Описание
--- | --- | --- | --- |  ---
ssh | Нет | Коллекция | Указывает hello конфигурации ключа SSH для ОС Linux.
path | Да | Строка | Указывает путь к файлу Linux hello где hello ключи SSH или сертификат должен быть расположен
keyData | Да | Строка | Указывает открытый ключ SSH в кодировке Base64.

Пример см. в разделе [GitHub краткого hello 101 ВМ ключа SSH шаблона](https://github.com/Azure/azure-quickstart-templates/blob/master/101-vm-sshkey/azuredeploy.json).

 
### <a name="when-i-run-update-azurermvmss-after-adding-more-than-one-certificate-from-hello-same-key-vault-i-see-hello-following-message"></a>При запуске `Update-AzureRmVmss` после добавления более одного сертификата из hello ключ хранилища, я вижу hello следующего сообщения:
 
>Update-AzureRmVmss: список секретов содержит повторяющиеся экземпляры /subscriptions/<идентификатор_моей_подписки>/resourceGroups/internal-rg-dev/providers/Microsoft.KeyVault/vaults/internal-keyvault-dev, которые запрещены.
 
Это может произойти при попытке toore-добавить hello же хранилища вместо использования нового сертификата хранилища для существующей исходное хранилище hello. Hello `Add-AzureRmVmssSecret` команда не работает правильно при добавлении дополнительных секретные данные.
 
tooadd дополнительные секретные данные из hello же хранилище ключей, список $vmss.properties.osProfile.secrets[0].vaultCertificates hello обновления.
 
Hello ожидалось входной структуре, см. в разделе [создания или обновления виртуальной машины установите](https://msdn.microsoft.com/library/azure/mt589035.aspx).
 
Найти секрет hello в объект набора масштабирования виртуальной машины hello в хранилище ключей hello. Затем можно добавить список toohello Справочник (hello URL-адрес и имя секрета хранилища hello) сертификат, связанный с хранилищем hello.

> [!NOTE] 
> В настоящее время невозможно удалить сертификаты из виртуальных машин с помощью API набор масштабирования виртуальной машины hello.
>

Новые виртуальные машины не будет иметь Здравствуй, старый сертификат. Однако виртуальные машины, имеют сертификат hello и который уже развернут будет Здравствуй, старый сертификат.
 
### <a name="can-i-push-certificates-toohello-virtual-machine-scale-set-without-providing-hello-password-when-hello-certificate-is-in-hello-secret-store"></a>Можно передать набор без указания пароля hello, в том случае, когда сертификат hello в секретное хранилище hello масштабирования виртуальных машин toohello сертификаты?

Код toohard пароли в сценариях не обязательно. Можно динамически получить пароли с разрешениями hello с помощью сценария развертывания toorun hello. Если у вас есть скрипт, который перемещает сертификат из хранилища ключей секретное хранилище hello, hello секретное хранилище `get certificate` команда также выводит пароль hello hello PFX-файла.
 
### <a name="how-does-hello-secrets-property-of-virtualmachineprofileosprofile-for-a-virtual-machine-scale-set-work-why-do-i-need-hello-sourcevault-value-when-i-have-toospecify-hello-absolute-uri-for-a-certificate-by-using-hello-certificateurl-property"></a>Как hello секреты свойство virtualMachineProfile.osProfile для масштабирования виртуальных машин задать работы? Почему при работе с toospecify hello абсолютный URI на сертификат с помощью свойства certificateUrl hello должны hello sourceVault значение? 

Ссылку на сертификат удаленного управления Windows (WinRM) должен присутствовать в hello секреты свойство hello профиль ОС. 

Hello, указывающее, hello исходное хранилище предназначено политики управления доступом управления доступом tooenforce, имеющихся в модели пользователя облачной службы Azure. Если не указана hello исходное хранилище, пользователей, которые не имеют разрешения доступа или toodeploy секреты tooa хранилище ключей будет может toothrough вычислений ресурсов поставщика (CRP). Политики ACL применяются даже к еще не созданным ресурсам.

Если указан неверный исходный идентификатор хранилища, но URL-адрес допустимого ключа хранилища, сообщение об ошибке при опросе hello операции.
 
### <a name="if-i-add-secrets-tooan-existing-virtual-machine-scale-set-are-hello-secrets-injected-into-existing-vms-or-only-into-new-ones"></a>Если добавить tooan секреты существующего набора масштабирования виртуальных машин, секреты hello вводится в существующих виртуальных машин или только на новые? 

Сертификаты добавляются tooall виртуальные машины, даже те существующая. Если ваш масштабирования виртуальной машины задано свойство upgradePolicy задано слишком**вручную**, hello добавления сертификата toohello виртуальной Машины при выполнении обновления вручную для hello виртуальной Машины.
 
### <a name="where-do-i-put-certificates-for-linux-vms"></a>Куда следует поместить сертификаты виртуальных машин Linux?

как toodeploy для виртуальных машин Linux, см. toolearn [развертывание tooVMs сертификаты из хранилища ключей с управлением клиентом](https://blogs.technet.microsoft.com/kv/2015/07/14/deploy-certificates-to-vms-from-customer-managed-key-vault/).
  
### <a name="how-do-i-add-a-new-vault-certificate-tooa-new-certificate-object"></a>Как добавить новые хранилища сертификатов tooa сертификат объекта?

tooadd хранилище секрета существующих сертификатов tooan, см. следующий пример PowerShell hello. Используйте только один объект секрета.
 
```powershell
$newVaultCertificate = New-AzureRmVmssVaultCertificateConfig -CertificateStore MY -CertificateUrl https://sansunallapps1.vault.azure.net:443/secrets/dg-private-enc/55fa0332edc44a84ad655298905f1809
 
$vmss.VirtualMachineProfile.OsProfile.Secrets[0].VaultCertificates.Add($newVaultCertificate)
 
Update-AzureRmVmss -VirtualMachineScaleSet $vmss -ResourceGroup $rg -Name $vmssName
```
 
### <a name="what-happens-toocertificates-if-you-reimage-a-vm"></a>Что если toocertificates пересоздать виртуальной Машины?

После пересоздания образа виртуальной машины сертификаты удаляются. Преобразует весь диск ОС удалений hello. 
 
### <a name="what-happens-if-you-delete-a-certificate-from-hello-key-vault"></a>Что произойдет, если удалить сертификат из хранилища ключей hello?

Если секрет hello удаляется из хранилища ключей hello и затем запустить `stop deallocate` для всех виртуальных машин и затем запустите их снова, возникнет ошибка. Hello произошел сбой, так как hello CRP необходим tooretrieve hello секретов из хранилища ключей hello, но он не может. В этом случае можно удалить из модели набора масштабирования виртуальной машины hello hello сертификаты. 

компонент CRP Hello не сохраняет секреты клиента. При запуске `stop deallocate` для всех виртуальных машин в наборе масштабирования виртуальных машин hello hello кэш удаляется. В этом сценарии секретные данные извлекаются из хранилища ключей hello.

Эта проблема не встречаются при горизонтальное масштабирование, так как отсутствует кэшированная копия секрета hello в Azure Service Fabric (в модели структуры одного клиента hello).
 
### <a name="why-do-i-have-toospecify-hello-exact-location-for-hello-certificate-url-httpsname-of-hello-vaultvaultazurenet443secretsexact-location-as-indicated-in-service-fabric-cluster-security-scenarioshttpsazuremicrosoftcomdocumentationarticlesservice-fabric-cluster-security"></a>Почему у toospecify hello точное расположение URL-адрес сертификата hello (https://<name of hello vault>.vault.azure.net:443/secrets/<exact location>), как указано в [сценарии безопасности кластера Service Fabric](https://azure.microsoft.com/documentation/articles/service-fabric-cluster-security/)?
 
Документация по хранилищу ключей Azure Hello состояний, получить секрет API-интерфейса REST должен возвращать hello последнюю версию секрета hello, если не указана версия hello приветствия.
 
Метод | URL-адрес
--- | ---
ПОЛУЧЕНИЕ | https://mykeyvault.vault.azure.net/secrets/{имя_секрета}/{версия_секрета}?api-version={версия_API}

Замените {*имя секрета*} с именем hello и замените {*версии секрета*} с версией hello секрет hello требуется tooretrieve. может быть исключено Hello версию секрета. В этом случае будет получена текущая версия hello.
  
### <a name="why-do-i-have-toospecify-hello-certificate-version-when-i-use-key-vault"></a>Почему у toospecify hello сертификата версии при использовании хранилища ключей?

Hello hello версии хранилища ключей требование toospecify hello сертификат предназначен toomake снимите toohello пользователя какие сертификат развертывается на их виртуальные машины.

При создании виртуальной Машины и обновите ваш секрет в хранилище ключей hello, новый сертификат hello не загруженные tooyour виртуальных машин. Но tooreference и новые виртуальные машины могут получать новый секрет hello отображаются виртуальные машины. tooavoid, являются обязательным tooreference версию секрета.

### <a name="my-team-works-with-several-certificates-that-are-distributed-toous-as-cer-public-keys-what-is-hello-recommended-approach-for-deploying-these-certificates-tooa-virtual-machine-scale-set"></a>Моя группа работает с несколькими сертификаты, распространяемые toous как открытые ключи CER-файл. Что такое рекомендованный подход для развертывания этих сертификатов набора масштабирования виртуальных машин tooa hello

toodeploy .cer открытые ключи tooa масштабный набор виртуальных машин, можно создать в PFX-файл, который содержит только файлы CER-файл. toodo это, используйте `X509ContentType = Pfx`. Например загрузить hello CER-файл как объект x509Certificate2 в C# или PowerShell, а затем вызывайте метод hello. 

Дополнительные сведения о методе X509Certificate.Export см. в [этой статье](https://msdn.microsoft.com/library/24ww6yzk(v=vs.110.aspx)).

### <a name="i-do-not-see-an-option-for-users-toopass-in-certificates-as-base64-strings-most-other-resource-providers-have-this-option"></a>Отсутствует параметр для toopass пользователей в сертификатах как строки в кодировке base64. Большинство других поставщиков ресурсов предоставляют этот параметр.

tooemulate, передавая сертификата в виде строки base64, можно извлечь hello последние версии URL-адрес в шаблона диспетчера ресурсов. Следующие hello следующие свойства JSON в шаблон диспетчера ресурсов.

```json 
"certificateUrl": "[reference(resourceId(parameters('vaultResourceGroup'), 'Microsoft.KeyVault/vaults/secrets', parameters('vaultName'), parameters('secretName')), '2015-06-01').secretUriWithVersion]"
```
 
### <a name="do-i-have-toowrap-certificates-in-json-objects-in-key-vaults"></a>Имеются ли в объектах JSON в хранилищах ключей toowrap сертификаты?

В масштабируемых наборах и на виртуальных машинах сертификаты нужно помещать в объекты JSON. 

Кроме того, поддерживается тип содержимого hello приложения/x-pkcs12. Инструкции по использованию application/x-pkcs12 см. в записи блога об [использовании PFX-сертификатов в Azure Key Vault](http://www.rahulpnath.com/blog/pfx-certificate-in-azure-key-vault/).
 
Сейчас мы не поддерживаем CER-файлы. toouse CER-файлами, экспортировать их в контейнеры PFX-файл.



## <a name="compliance"></a>Соответствие нормативным требованиям

### <a name="are-virtual-machine-scale-sets-pci-compliant"></a>Соответствуют ли масштабируемые наборы виртуальных машин требованиям стандарта PCI?

Наборы масштабирования виртуальной машины — это тонкий слой API на основе hello CRP. Оба компонента являются частью платформы вычислений hello в hello Azure дерева служб.

С точки зрения соответствия наборы масштабирования виртуальных машин являются основной частью платформы hello вычислений Azure. Они совместно используют команды, средства, процессы, методологии развертывания, управления безопасностью, just-in-time (JIT) компиляции, мониторинга, предупреждений и т. д с CRP hello сам. Наборы масштабирования виртуальных машин, индустрии платежных карт (PCI)-совместимые, так как hello CRP является частью текущего PCI данных безопасности стандартной (DSS) аттестации hello.

Дополнительные сведения см. в разделе [hello Центр управления безопасностью Microsoft](https://www.microsoft.com/TrustCenter/Compliance/PCI).






## <a name="extensions"></a>расширения.

### <a name="how-do-i-delete-a-virtual-machine-scale-set-extension"></a>Как удалить расширение масштабируемого набора виртуальных машин?

toodelete масштабирования виртуальных машин установите расширение hello используйте следующий пример PowerShell:

```powershell
$vmss = Get-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" 

$vmss=Remove-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name "extensionName"

Update-AzureRmVmss -ResourceGroupName "resource_group_name" -VMScaleSetName "vmssName" -VirtualMacineScaleSet $vmss
```
 
Можно найти значение extensionName hello в `$vmss`.
   
### <a name="is-there-a-virtual-machine-scale-set-template-example-that-integrates-with-operations-management-suite"></a>Существует ли пример шаблона масштабируемого набора виртуальных машин, который интегрируется с Operations Management Suite?

Для примера шаблона, которое интегрируется с Operations Management Suite набора масштабирования виртуальных машин, см. во втором примере hello в [развертывание кластера Azure Service Fabric и включите наблюдение с помощью аналитики журналов](https://github.com/krnese/AzureDeploy/tree/master/OMS/MSOMS/ServiceFabric).
   
### <a name="extensions-seem-toorun-in-parallel-on-virtual-machine-scale-sets-this-causes-my-custom-script-extension-toofail-what-can-i-do-toofix-this"></a>Расширения кажутся toorun параллельно на наборы масштабирования виртуальных машин. В этом случае Мой toofail расширение пользовательского скрипта. Что можно делать toofix это?

toolearn о виртуализации расширения в наборы масштабирования виртуальных машин, в разделе [расширения виртуализации в наборы масштабирования виртуальной машины Azure](https://msftstack.wordpress.com/2016/05/12/extension-sequencing-in-azure-vm-scale-sets/).
 
 
### <a name="how-do-i-reset-hello-password-for-vms-in-my-virtual-machine-scale-set"></a>Как сбросить пароль hello для виртуальных машин в моей масштабный набор виртуальных машин?

пароль hello tooreset для виртуальных машин в вашей масштабирования виртуальных машин необходимо задать, использовать расширения access ВМ. 

Используйте следующий пример PowerShell hello.

```powershell
$vmssName = "myvmss"
$vmssResourceGroup = "myvmssrg"
$publicConfig = @{"UserName" = "newuser"}
$privateConfig = @{"Password" = "********"}
 
$extName = "VMAccessAgent"
$publisher = "Microsoft.Compute"
$vmss = Get-AzureRmVmss -ResourceGroupName $vmssResourceGroup -VMScaleSetName $vmssName
$vmss = Add-AzureRmVmssExtension -VirtualMachineScaleSet $vmss -Name $extName -Publisher $publisher -Setting $publicConfig -ProtectedSetting $privateConfig -Type $extName -TypeHandlerVersion "2.0" -AutoUpgradeMinorVersion $true
Update-AzureRmVmss -ResourceGroupName $vmssResourceGroup -Name $vmssName -VirtualMachineScaleSet $vmss
```
 
 
### <a name="how-do-i-add-an-extension-tooall-vms-in-my-virtual-machine-scale-set"></a>Как добавить расширение tooall виртуальных машин в моей масштабный набор виртуальных машин?

Если политика обновления задано слишком**автоматического**, повторного развертывания шаблона hello с новыми свойствами расширения hello обновляет все виртуальные машины.

Если политика обновления задано слишком**вручную**, сначала обновить расширение hello и вручную обновить все экземпляры в виртуальные машины.

  
### <a name="if-hello-extensions-associated-with-an-existing-virtual-machine-scale-set-are-updated-are-existing-vms-affected-that-is-will-hello-vms-not-match-hello-virtual-machine-scale-set-model-or-are-they-ignored-when-an-existing-machine-is-service-healed-or-reimaged-are-hello-scripts-that-are-currently-configured-on-hello-virtual-machine-scale-set-executed-or-are-hello-scripts-that-were-configured-when-hello-vm-was-first-created-used"></a>Если обновляются hello расширения, связанные с существующего набора масштабирования виртуальной машины, существующие виртуальные машины в затронутых? (То есть виртуальные машины будут hello *не* модели набора масштабирования виртуальной машины hello соответствия?) Или они игнорируются? Когда существующей машины восстанавливаются службы, или повторного создания образа, hello скрипты, которые в настоящий момент на выполнении набора масштабирования виртуальных машин hello или являются hello скрипты, которые были настроены при использовании hello создания виртуальной Машины?

Если определение расширения hello в масштабирования виртуальных машин hello обновить модель и hello upgradePolicy задано слишком**автоматического**, он обновляет виртуальные машины hello. Если свойство upgradePolicy hello задано слишком**вручную**, расширения, помечаются как не соответствует модели hello. 

Если существующей виртуальной Машины восстанавливаются службы, он отображается как перезагрузка и расширения hello не выполняют повторный запуск. При его повторном создании это как замены диска ОС hello hello исходного образа. Все специализации из последней модели hello, такие как расширения, выполняются.
 
### <a name="how-do-i-join-a-virtual-machine-scale-set-tooan-azure-ad-domain"></a>Как присоединить к домену tooan Azure AD набор масштабирования виртуальной машины?

toojoin домена Azure Active Directory (Azure AD) tooan набор масштабирования виртуальной машины, можно определить расширение. 

toodefine расширения, используйте свойство JsonADDomainExtension hello:

```json
"extensionProfile": {
    "extensions": [
        {
            "name": "joindomain",
            "properties": {
                "publisher": "Microsoft.Compute",
                "type": "JsonADDomainExtension",
                "typeHandlerVersion": "1.3",
                "settings": {
                    "Name": "[parameters('domainName')]",
                    "OUPath": "[variables('ouPath')]",
                    "User": "[variables('domainAndUsername')]",
                    "Restart": "true",
                    "Options": "[variables('domainJoinOptions')]"
                },
                "protectedsettings": {
                    "Password": "[parameters('domainJoinPassword')]"
                }
            }
        }
    ]
}
```
 
### <a name="my-virtual-machine-scale-set-extension-is-trying-tooinstall-something-that-requires-a-reboot-for-example-commandtoexecute-powershellexe--executionpolicy-unrestricted-install-windowsfeature-name-fs-resource-manager-includemanagementtools"></a>Расширения набора масштабирования виртуальной машины пытается tooinstall то, что требуется перезагрузка. Например, "commandToExecute": "powershell.exe -ExecutionPolicy Unrestricted Install-WindowsFeature –Name FS-Resource-Manager –IncludeManagementTools".

Если расширения набора масштабирования виртуальной машины пытается tooinstall то, что требует перезагрузки, можно использовать расширение hello Azure автоматизации настройки требуемого состояния (DSC службы автоматизации). Если hello операционная система Windows Server 2012 R2, Azure запрашивает в программе установки Windows Management Framework (WMF) 5.0 hello, перезагрузки, а затем продолжает hello конфигурации. 
 
### <a name="how-do-i-turn-on-antimalware-in-my-virtual-machine-scale-set"></a>Как включить антивредоносную программу в масштабируемом наборе виртуальных машин?

tooturn для защиты от вредоносных программ на шкале виртуальной машине установлена, следует использовать hello следующий пример PowerShell:

```powershell
$rgname = 'autolap'
$vmssname = 'autolapbr'
$location = 'eastus'
 
# Retrieve hello most recent version number of hello extension.
$allVersions= (Get-AzureRmVMExtensionImage -Location $location -PublisherName "Microsoft.Azure.Security" -Type "IaaSAntimalware").Version
$versionString = $allVersions[($allVersions.count)-1].Split(".")[0] + "." + $allVersions[($allVersions.count)-1].Split(".")[1]
 
$VMSS = Get-AzureRmVmss -ResourceGroupName $rgname -VMScaleSetName $vmssname
echo $VMSS
Add-AzureRmVmssExtension -VirtualMachineScaleSet $VMSS -Name "IaaSAntimalware" -Publisher "Microsoft.Azure.Security" -Type "IaaSAntimalware" -TypeHandlerVersion $versionString
Update-AzureRmVmss -ResourceGroupName $rgname -Name $vmssname -VirtualMachineScaleSet $VMSS 
```

### <a name="i-need-tooexecute-a-custom-script-thats-hosted-in-a-private-storage-account-hello-script-runs-successfully-when-hello-storage-is-public-but-when-i-try-toouse-a-shared-access-signature-sas-it-fails-this-message-is-displayed-missing-mandatory-parameters-for-valid-shared-access-signature-linksas-works-fine-from-my-local-browser"></a>Мне нужна tooexecute пользовательского скрипта, который размещен в личной учетной записи хранения. Hello скрипт успешно запускается, если открытый hello хранилища, но при попытке toouse подпись общего доступа (SAS), происходит сбой. и отображается следующее сообщение об ошибке: "Отсутствуют обязательные параметры для допустимой подписи коллективного доступа". В локальном браузере проблемы с подписанным URL-адресом и ссылкой не возникали.

tooexecute пользовательского скрипта, который размещен в личной учетной записи хранения, задать параметры защищенного hello ключ учетной записи хранилища и имя. Дополнительные сведения см. в статье [Расширение Custom Script в ОС Windows](https://azure.microsoft.com/documentation/articles/virtual-machines-windows-extensions-customscript/#template-example-for-a-windows-vm-with-protected-settings).







## <a name="networking"></a>Сеть
 
### <a name="is-it-possible-tooassign-a-network-security-group-nsg-tooa-scale-set-so-that-it-will-apply-tooall-hello-vm-nics-in-hello-set"></a>Это возможно tooassign задать шкалу tooa группы безопасности сети (NSG), таким образом, он будет применить hello tooall сетевых адаптеров виртуальной Машины в наборе hello?

Да. Группы безопасности сети можно применять непосредственно задать масштаб tooa обратившись в разделе интерфейса hello hello сетевых профилей. Пример:

```json
"networkProfile": {
    "networkInterfaceConfigurations": [
        {
            "name": "nic1",
            "properties": {
                "primary": "true",
                "ipConfigurations": [
                    {
                        "name": "ip1",
                        "properties": {
                            "subnet": {
                                "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/virtualNetworks/', variables('vnetName'), '/subnets/subnet1')]"
                            }
                "loadBalancerInboundNatPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/inboundNatPools/natPool1')]"
                                }
                            ],
                            "loadBalancerBackendAddressPools": [
                                {
                                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/loadBalancers/', variables('lbName'), '/backendAddressPools/addressPool1')]"
                                 }
                            ]
                        }
                    }
                ],
                "networkSecurityGroup": {
                    "id": "[concat('/subscriptions/', subscription().subscriptionId,'/resourceGroups/', resourceGroup().name, '/providers/Microsoft.Network/networkSecurityGroups/', variables('nsgName'))]"
                }
            }
        }
    ]
}
```

### <a name="how-do-i-do-a-vip-swap-for-virtual-machine-scale-sets-in-hello-same-subscription-and-same-region"></a>Как это сделать Операцию переключения наборы масштабирования виртуальных машин в hello же подписке и одном регионе?

При наличии двух виртуальных масштабирования машины задает с интерфейсных подсистемы балансировки нагрузки Azure, и они находятся в hello ту же подписку и регион, можно освободить hello общих IP-адресов из каждого из них и назначить toohello других. Пример приведен в статье [VIP Swap: Blue-green deployment in Azure Resource Manager](https://msftstack.wordpress.com/2017/02/24/vip-swap-blue-green-deployment-in-azure-resource-manager/) (Переключение виртуальных IP-адресов: развертывание по схеме "blue-green" в Azure Resource Manager). Это подразумевает задержку на то, что как hello ресурсы освобождены выделенной на уровне сети hello. Более быстрый параметр — toouse шлюза приложения Azure с двумя внутренние пулы и правила маршрутизации. Также можно разместить приложение в [службе приложений Azure](https://azure.microsoft.com/en-us/services/app-service/), которая обеспечивает быстрое переключение между промежуточными и рабочими слотами.
 
### <a name="how-do-i-specify-a-range-of-private-ip-addresses-toouse-for-static-private-ip-address-allocation"></a>Как указать диапазон частных toouse IP адресов для статического выделения частных IP-адресов?

IP-адреса выбираются из указанной подсети. 

метод распределения Hello IP-адресов, набор масштабирования виртуальной машины всегда «динамических», но это не значит, что можно изменить эти IP-адреса. В этом случае «динамических» означает только что hello IP-адрес не указан в запросе PUT. Укажите статический hello устанавливается с помощью подсети hello. 
    
### <a name="how-do-i-deploy-a-virtual-machine-scale-set-tooan-existing-azure-virtual-network"></a>Развертывание виртуальной машины шкалы набор tooan существующей виртуальной сети Azure 

toodeploy масштабирования виртуальных машин задайте tooan существующей виртуальной сети Azure см. в разделе [развертывание виртуальной машины шкалы набор tooan существующей виртуальной сети](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-existing-vnet). 

### <a name="how-do-i-add-hello-ip-address-of-hello-first-vm-in-a-virtual-machine-scale-set-toohello-output-of-a-template"></a>Как добавить IP-адрес hello hello первая виртуальная машина в масштабирования виртуальных машин установите toohello выходные данные шаблона?

первая виртуальная машина в виртуальной машине шкалы набор toohello выходных данных шаблона, в разделе tooadd hello IP-адрес hello [ARM: получение VMSS частных IP-адресов](http://stackoverflow.com/questions/42790392/arm-get-vmsss-private-ips).

### <a name="can-i-use-scale-sets-with-accelerated-networking"></a>Можно ли использовать масштабируемые наборы с ускоренной сетью?

Да. toouse accelerated сети, задать enableAcceleratedNetworking tootrue в шкалу набора конфигураций сетевого интерфейса. Например: 
```json
"networkProfile": {
    "networkInterfaceConfigurations": [
    {
        "name": "niconfig1",
        "properties": {
        "primary": true,
        "enableAcceleratedNetworking" : true,
        "ipConfigurations": [
                ]
            }
            }
        ]
        }
    }
    ]
}
```

### <a name="how-can-i-configure-hello-dns-servers-used-by-a-scale-set"></a>Как настроить hello DNS-серверы, используемые набором масштабирования

toocreate набора масштабирования виртуальных Машин с пользовательской конфигурацией DNS, добавить шкалу dnsSettings пакета JSON toohello задать раздел конфигураций сетевого интерфейса. Пример:
```json
    "dnsSettings":{
        "dnsServers":["10.0.0.6", "10.0.0.5"]
    }
```

### <a name="how-can-i-configure-a-scale-set-tooassign-a-public-ip-address-tooeach-vm"></a>Как настроить tooassign набор масштабирования открытый IP адрес tooeach виртуальной Машины

toocreate набор масштабирования виртуальных Машин, назначается открытый IP адрес tooeach виртуальной Машины, убедитесь, что версия hello API hello Microsoft.Compute/virtualMAchineScaleSets ресурсов 2017 г., 03, 30 и добавить _publicipaddressconfiguration_ пакетов JSON задать масштаб toohello раздел IP-конфигурации. Пример:

```json
    "publicipaddressconfiguration": {
        "name": "pub1",
        "properties": {
        "idleTimeoutInMinutes": 15
        }
    }
```

### <a name="can-i-configure-a-scale-set-toowork-with-multiple-application-gateways"></a>Можно настроить набор масштабирования toowork с несколькими шлюзы приложений

Да. Можно добавить hello ресурсов идентификаторы для нескольких пулов toohello адрес шлюза приложений серверной _applicationGatewayBackendAddressPools_ списка в hello _IP-конфигураций_ раздел набора масштабирования сетевой профиль.

## <a name="scale"></a>Масштаб

### <a name="in-what-case-would-i-create-a-virtual-machine-scale-set-with-fewer-than-two-vms"></a>В каких случаях следует создавать масштабируемый набор с одной виртуальной машиной или без них?

Одна из причин toocreate набора масштабирования виртуальных машин с менее двух виртуальных машин будет иметь значение toouse hello эластичной параметров масштабирования виртуальных машин. Например можно развернуть набор масштабирования виртуальной машины с нуля toodefine виртуальных машин инфраструктуры без оплаты виртуальной Машине под управлением затрат. Затем когда вы будете готовы toodeploy виртуальных машин, увеличьте hello «емкость» hello набор масштабирования виртуальной машины toohello число экземпляров рабочей.

Вторая причина заключается в том, что в масштабируемом наборе выполняются операции, не учитывающие доступность в таком же смысле, что и группы доступности с отдельными виртуальными машинами. Наборы масштабирования виртуальной машины предоставляют способ toowork с форматными вычислительных единиц, которые взаимозаменяемые. Это единообразие является ключевым преимуществом при выборе между масштабируемыми наборами виртуальных машин и группами доступности. Многие рабочие нагрузки без отслеживания состояния не учитывают отдельные единицы. Удаляет hello рабочей нагрузки, можно масштабировать tooone единица измерения вычислений и затем масштабировать toomany при увеличении рабочей нагрузки hello.

### <a name="how-do-i-change-hello-number-of-vms-in-a-virtual-machine-scale-set"></a>Как изменить hello число виртуальных машин в наборе масштабирования виртуальных машин?

toochange hello число виртуальных машин в наборе масштабирования виртуальных машин в разделе [изменить количество экземпляров hello набора масштабирования виртуальных машин](https://msftstack.wordpress.com/2016/05/13/change-the-instance-count-of-an-azure-vm-scale-set/).

### <a name="how-do-i-define-custom-alerts-for-when-certain-thresholds-are-reached"></a>Как настроить пользовательские оповещения, отображающиеся при достижении определенных пороговых значений?

Обработкой оповещений при достижении определенных пороговых значений можно управлять несколькими способами. Например, вы можете определить настраиваемые объекты webhook. Следующий пример веб-перехватчика Hello взят из шаблона диспетчера ресурсов.

```json
{
    "type": "Microsoft.Insights/autoscaleSettings",
    "apiVersion": "[variables('insightsApi')]",
    "name": "autoscale",
    "location": "[parameters('resourceLocation')]",
    "dependsOn": [
        "[concat('Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]"
    ],
    "properties": {
        "name": "autoscale",
        "targetResourceUri": "[concat('/subscriptions/',subscription().subscriptionId, '/resourceGroups/',  resourceGroup().name, '/providers/Microsoft.Compute/virtualMachineScaleSets/', parameters('vmSSName'))]",
        "enabled": true,
        "notifications": [
            {
                "operation": "Scale",
                "email": {
                    "sendToSubscriptionAdministrator": true,
                    "sendToSubscriptionCoAdministrators": true,
                    "customEmails": [
                        "youremail@address.com"
                    ]
                },
                "webhooks": [
                    {
                        "serviceUri": "https://events.pagerduty.com/integration/0b75b57246814149b4d87fa6e1273687/enqueue",
                        "properties": {
                            "key1": "custommetric",
                            "key2": "scalevmss"
                        }
                    }
                ]
            }
        ],
```

В этом примере оповещение становится tooPagerduty.com при достижении порогового значения.



## <a name="patching-and-operations"></a>Установка исправлений и эксплуатация

### <a name="how-do-i-create-a-scale-set-in-an-existing-resource-group"></a>Как создать масштабируемый набор в существующей группе ресурсов?

Создание набора масштабирования в существующий ресурс группы еще невозможно из hello портал Azure, но при развертывании шкалу на основе шаблона диспетчера ресурсов Azure можно указать существующую группу ресурсов. Можно также указать существующую группу ресурсов при создании масштабируемого набора с помощью Azure PowerShell или интерфейса командной строки.

### <a name="can-we-move-a-scale-set-tooanother-resource-group"></a>Мы можно переместить группы ресурсов tooanother набора масштабирования?

Да, можно переместить шкалы набор ресурсов tooa новую подписку или группу ресурсов.

### <a name="how-tooi-update-my-virtual-machine-scale-set-tooa-new-image-how-do-i-manage-patching"></a>Обновления tooI Мой масштабирования виртуальных машин установлены tooa новый образ? и как управлять установкой исправлений?

tooupdate вашей виртуальной машины в наборе tooa нового образа и toomanage исправлений, в разделе [обновление набора масштабирования виртуальных машин](https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-upgrade-scale-set).

### <a name="can-i-use-hello-reimage-operation-tooreset-a-vm-without-changing-hello-image-that-is-i-want-reset-a-vm-toofactory-settings-rather-than-tooa-new-image"></a>Можно использовать tooreset операции hello повторное создание образа виртуальной Машины без изменения образа hello (То есть, требуется сбросить параметры виртуальной Машины toofactory вместо tooa нового изображения.)

Да, можно использовать tooreset операции hello повторное создание образа виртуальной Машины без изменения образа hello. Тем не менее, если задать масштаб вашей виртуальной машины ссылается на образ платформы с `version = latest`, ВМ можно обновить tooa образа ОС более поздней версии при вызове `reimage`.

Дополнительные сведения см. в статье об [управлении всеми виртуальными машинами в масштабируемом наборе](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-all-vms-in-a-set).



## <a name="troubleshooting"></a>Устранение неполадок

### <a name="how-do-i-turn-on-boot-diagnostics"></a>Как включить диагностику загрузки?

tooturn на Диагностика загрузки, во-первых, создайте учетную запись хранилища. Затем поместите этот блок JSON в наборе масштабирования виртуальных машин **virtualMachineProfile**и обновить набор масштабирования виртуальной машины hello:

```json
"diagnosticsProfile": {
    "bootDiagnostics": {
        "enabled": true,
        "storageUri": "http://yourstorageaccount.blob.core.windows.net"
    }
}
```

При создании новой виртуальной Машины hello свойство InstanceView hello виртуальных Машин показывает данные hello для экрана приветствия и т. д. Ниже приведен пример:
 
```json
"bootDiagnostics": {
    "consoleScreenshotBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.screenshot.bmp",
    "serialConsoleLogBlobUri": "https://o0sz3nhtbmkg6geswarm5.blob.core.windows.net/bootdiagnostics-swarmagen-4157d838-8335-4f78-bf0e-b616a99bc8bd/swarm-agent-9574AE92vmss-0_2.4157d838-8335-4f78-bf0e-b616a99bc8bd.serialconsole.log"
  }
```


## <a name="virtual-machine-properties"></a>Свойства виртуальной машины

### <a name="how-do-i-get-property-information-for-each-vm-without-making-multiple-calls-for-example-how-would-i-get-hello-fault-domain-for-each-of-hello-100-vms-in-my-virtual-machine-scale-set"></a>Как получить сведения о свойствах каждой виртуальной машины, не выполняя несколько вызовов? Например как бы заставить домен сбоя hello для каждого hello 100 виртуальных машин в моей масштабный набор виртуальных машин?

сведения о свойстве tooget для каждой виртуальной Машины без несколько вызовов, можно вызвать `ListVMInstanceViews` , выполнив REST API `GET` на hello, следуя ресурса (URI):

/subscriptions/<идентификатор_подписки>/resourceGroups/<имя_группы_ресурсов>/providers/Microsoft.Compute/virtualMachineScaleSets/<имя_масштабируемого_набора>/virtualMachines?$expand=instanceView&$select=instanceView.

### <a name="can-i-pass-different-extension-arguments-toodifferent-vms-in-a-virtual-machine-scale-set"></a>Можно передавать аргументы другое расширение toodifferent виртуальные машины в наборе масштабирования виртуальных машин?

Нет, нельзя передавать аргументы другое расширение toodifferent виртуальные машины набора масштабирования виртуальных машин. Тем не менее расширения может действовать на основе уникальных свойств hello hello ВМ работают для, такого как имя машины hello. Расширения также можно запрашивать метаданные экземпляра на http://169.254.169.254 tooget Дополнительные сведения о hello виртуальной Машины.

### <a name="why-are-there-gaps-between-my-virtual-machine-scale-set-vm-machine-names-and-vm-ids-for-example-0-1-3"></a>Почему между именами виртуальных машин в масштабируемом наборе и их идентификаторами существуют пропуски? Например, 0, 1, 3...

Существуют пропуски между ВМ идентификаторы и имена компьютеров виртуальной Машины набора масштабирования виртуальной машины, поскольку вашей виртуальной машины в наборе **избыточной подготовки** задано значение по умолчанию toohello **true**. Если избыток задано слишком**true**, больше виртуальных машин, чем запрошено создаются. Лишние виртуальные машины удаляются. В этом случае получить развертывания повысить надежность, но за счет hello смежных именования и смежных сетевых адресов (NAT) правила. 

Это свойство можно задать слишком**false**. На надежность развертывания небольших масштабируемых наборов это не окажет значительного влияния.

### <a name="what-is-hello-difference-between-deleting-a-vm-in-a-virtual-machine-scale-set-and-deallocating-hello-vm-when-should-i-choose-one-over-hello-other"></a>Что такое hello различие между удалением виртуальной Машины в наборе масштабирования виртуальных машин и освобождение hello виртуальной Машины Когда один над другим hello выбрать?

Hello основное различие между удалением виртуальной Машины в наборе масштабирования виртуальных машин и освобождение hello виртуальной Машины, звучит `deallocate` не приводит к удалению hello виртуальные жесткие диски (VHD). При выполнении команды `stop deallocate` взимается плата за хранение. Может использовать один или другой — для одного из следующих причин hello hello:

- Требуется toostop дополнительные затраты на вычислений, но желательно состояние диска hello tookeep hello виртуальных машин.
- Вы хотите toostart набор виртуальных машин гораздо быстрее, чем можно развернуть масштаб набора масштабирования виртуальных машин.
  - Связанные toothis сценарий, вы могли создать собственный механизм автоматического масштабирования и хотите быстрее шкалы начала до конца.
- У вас есть масштабируемый набор, неравномерно распределенный между доменами сбоя и обновления. Причиной этого может быть выборочное удаление или удаление после избыточной подготовки виртуальных машин. Под управлением `stop deallocate` следуют `start` на виртуальной машине hello равномерно наборе масштабирования распределяет виртуальные машины hello домены сбоя и доменах обновления.

