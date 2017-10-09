---
title: "Ведение журнала хранилища ключей aaaAzure | Документы Microsoft"
description: "Использовать этот учебник toohelp приступить к работе с хранилищем ключей Azure ведения журнала."
services: key-vault
documentationcenter: 
author: cabailey
manager: mbaldwin
tags: azure-resource-manager
ms.assetid: 43f96a2b-3af8-4adc-9344-bc6041fface8
ms.service: key-vault
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 07/19/2017
ms.author: cabailey
ms.openlocfilehash: 38a173297948748bef45e3d857c06b50b3e21e74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-key-vault-logging"></a>Ведение журнала хранилища ключей Azure
Хранилище ключей Azure доступно в большинстве регионов. Дополнительные сведения см. в разделе hello [страница цен в хранилище ключей](https://azure.microsoft.com/pricing/details/key-vault/).

## <a name="introduction"></a>Введение
После создания одного или нескольких хранилищ ключей, вероятно, стоит toomonitor, как и когда хранилищ ключа доступа и кем. Это можно сделать с помощью функции ведения журнала хранилища ключей, которая сохраняет информацию в указанной учетной записи хранения Azure. Для указанной учетной записи автоматически создается новый контейнер с именем **insights-logs-auditevent**. Эту же учетную запись можно использовать для сбора журналов нескольких хранилищ ключей.

Данные ведения журнала доступны в журнал не чаще, 10 минут после hello ключ в хранилище операции. В большинстве случаев это будет еще быстрее.  Он работает tooyou toomanage журналы в учетную запись хранилища:

* Используйте журналы toosecure методы управления стандартного доступа Azure, ограничив доступ к ним.
* Удалите журналы, которые больше не требуется tookeep вашей учетной записи хранилища.

Использовать этот учебник toohelp приступить к работе с ведения журнала, хранилище ключей Azure toocreate учетной записи хранилища, включите ведение журнала и интерпретации собираемых hello ведения журнала.  

> [!NOTE]
> Этот учебник не содержит инструкций для как toocreate ключа хранилища, ключи и секретные данные. Соответствующие сведения см. в статье [Приступая к работе с хранилищем ключей Azure](key-vault-get-started.md). Инструкции по кроссплатформенному интерфейсу командной строки см. в [этом руководстве](key-vault-manage-with-cli2.md).
>
> В настоящее время вы не можете настроить хранилище ключей Azure hello портал Azure. Вместо этого используйте эти указания по работе с Azure PowerShell.
>
>

Общие сведения о хранилище ключей Azure см. в статье [Что такое хранилище ключей Azure?](key-vault-whatis.md)

## <a name="prerequisites"></a>Предварительные требования
toocomplete этого учебника необходимо иметь следующие hello:

* Существующее хранилище ключей, которое вы используете.  
* Azure PowerShell, **начиная с версии 1.0.1**. tooinstall Azure PowerShell и связать ее с подпиской Azure см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Если вы уже установили Azure PowerShell и вы не знаете версии hello из консоли Azure PowerShell hello, введите `(Get-Module azure -ListAvailable).Version`.  
* Достаточный объем хранилища в Azure для журналов хранилищ ключей.

## <a id="connect"></a>Подключение tooyour подписки
Запустите сеанс Azure PowerShell и войдите в tooyour учетная запись Azure с hello следующую команду:  

    Login-AzureRmAccount

В hello всплывающем окне браузера введите имя пользователя учетной записи Azure и пароль. Azure PowerShell получит все подписки hello, которые связаны с этой учетной записью, а также по умолчанию, использует hello первое.

Если у вас несколько подписок, могут появиться toospecify одну из них, используемые toocreate вашего хранилища ключей Azure. Введите hello, следуя toosee hello подписки для учетной записи:

    Get-AzureRmSubscription

Затем toospecify hello подписки, связанной с хранилищу ключей, будет работать, тип:

    Set-AzureRmContext -SubscriptionId <subscription ID>

> [!NOTE]
> Этот шаг очень важен и особенно полезен, если с учетной записью связано несколько подписок. Если этот шаг пропускается, может появиться ошибка tooregister помощью Microsoft.Insights.
>   
>

Дополнительные сведения о настройке Azure PowerShell см. в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview).

## <a id="storage"></a>Создание учетной записи хранения для журналов
Несмотря на то, что можно использовать существующую учетную запись хранения для журналов, мы создадим новую учетную запись хранилища, выделенного tooKey хранилища журналов. Для удобства работы, когда у нас есть toospecify это более поздней версии, мы будем хранить сведения hello в переменную с именем **sa**.

Для дополнительных легкость управления, мы также используем hello одну группу ресурсов, как hello, содержащий нашей хранилища ключей. Из hello [учебник по началу работы](key-vault-get-started.md), эта группа ресурсов с именем **ContosoResourceGroup** и мы продолжим toouse hello Восточная Азия расположение. Замените эти значения собственными.

    $sa = New-AzureRmStorageAccount -ResourceGroupName ContosoResourceGroup -Name contosokeyvaultlogs -Type Standard_LRS -Location 'East Asia'


> [!NOTE]
> Если вы решите toouse существующую учетную запись хранения, необходимо использовать hello той же подписке, как хранилище ключей и его необходимо использовать модель развертывания диспетчера ресурсов hello, а не hello классической модели развертывания.
>
>

## <a id="identify"></a>Определите hello хранилища ключей для журналов
В обучении началу работы был наш имя хранилища ключей **ContosoKeyVault**, поэтому мы продолжим, имени и сохранение сведений о hello в переменную с именем toouse **Кв**:

    $kv = Get-AzureRmKeyVault -VaultName 'ContosoKeyVault'


## <a id="enable"></a>Включение ведения журналов
tooenable ведения журнала для хранилища ключей, мы будем использовать hello AzureRmDiagnosticSetting набор командлетов, вместе с переменными hello мы создали для нашей новой учетной записи хранения и наши хранилища ключей. Мы также настроить установим hello **-включена** флаг слишком**$true** и tooAuditEvent категории hello (hello только категория для ведения журнала хранилища ключей), задайте:

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent

включает Hello выходные данные для этого:

    StorageAccountId   : /subscriptions/<subscription-GUID>/resourceGroups/ContosoResourceGroup/providers/Microsoft.Storage/storageAccounts/ContosoKeyVaultLogs
    ServiceBusRuleId   :
    StorageAccountName :
        Logs
        Enabled           : True
        Category          : AuditEvent
        RetentionPolicy
        Enabled : False
        Days    : 0


Это позволит убедиться, что для хранилища ключей, сохранение сведений учетной записи хранилища tooyour теперь включено ведение журнала.

При необходимости можно также задать политику хранения для журналов, например политику, в соответствии с которой старые журналы будут автоматически удаляться. Например, задать политику хранения с помощью **- RetentionEnabled** флаг слишком**$true** и задайте **- RetentionInDays** параметр слишком**90** , что старше 90 дней журналы будут автоматически удалены.

    Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $true -Categories AuditEvent -RetentionEnabled $true -RetentionInDays 90

Регистрируются следующие данные:

* все прошедшие проверку подлинности запросы REST API, включая запросы, ставшие неудачными из-за определенных разрешений на доступ, системных ошибок или неправильных запросов;
* Операции с ключом hello хранилище себя, включая создание, удаление, параметр политики доступа хранилища ключей, и теги, такие как обновление атрибутов хранилища ключей.
* Операции над ключи и секретные данные в хранилище ключей hello, включая создание, изменение или удаление эти ключи и секретные данные; операции, такие как знак, убедитесь, шифрования, расшифровки, перенос и распаковки ключей, секреты, список ключей и секреты и их версиями.
* непроверенные запросы, которые приводят к появлению ответа 401 (например, запросы без токена носителя, с недействительным токеном, а также запросы неправильного формата или просроченные запросы).  

## <a id="access"></a>Доступ к журналам
Хранилище ключей журналы хранятся в hello **аналитики журналов auditevent** контейнера в учетной записи хранения hello, вы указали. toolist все большие двоичные объекты hello в этом контейнере, введите следующую команду:

Во-первых создайте переменную для имени контейнера hello. Он будет использоваться на протяжении hello остальной части пошагового hello.

    $container = 'insights-logs-auditevent'

toolist все большие двоичные объекты hello в этом контейнере, введите следующую команду:

    Get-AzureStorageBlob -Container $container -Context $sa.Context
Hello результат будет выглядеть toothis что-нибудь подобное:

**Универсальный код ресурса (URI) контейнера: https://contosokeyvaultlogs.blob.core.windows.net/insights-logs-auditevent**

**Имя**

- - -
**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=05/h=01/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=02/m=00/PT1H.json**

**resourceId=/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSORESOURCEGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT/y=2016/m=01/d=04/h=18/m=00/PT1H.json****

Как видно из этих выходных данных, hello больших двоичных объектов Следуйте соглашению об именах: **resourceId =<ARM resource ID>/y =<year>/m =<month>/d =<day of month>/h =<hour>/m =<minute>/filename.json**

Hello значений даты и времени используйте время UTC.

Так как hello учетную запись хранения может быть журналы toocollect используется для нескольких ресурсов, hello полный идентификатор ресурса в имени большого двоичного объекта hello является полезным tooaccess или загрузки только hello большие двоичные объекты, необходимые. Но перед этим мы рассмотрим сначала как toodownload все hello больших двоичных объектов.

Создайте папку toodownload hello больших двоичных объектов. Например:

    New-Item -Path 'C:\Users\username\ContosoKeyVaultLogs' -ItemType Directory -Force

Затем выведите список всех BLOB-объектов.  

    $blobs = Get-AzureStorageBlob -Container $container -Context $sa.Context

Передайте этот список при помощи «Get-AzureStorageBlobContent» toodownload hello BLOB-объектов в нашем папку назначения:

    $blobs | Get-AzureStorageBlobContent -Destination 'C:\Users\username\ContosoKeyVaultLogs'

При выполнении этой команды второй hello  **/**  разделитель в именах blob hello создайте полный папки в папке назначения hello, и эта структура будет используется toodownload и хранилище hello большие двоичные объекты как файлы.

tooselectively загрузка больших двоичных объектов, использовать подстановочные знаки. Например:

* Если имеется несколько хранилищ ключей и должны toodownload журналы для одной хранилища ключей, с именем CONTOSOKEYVAULT3:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/VAULTS/CONTOSOKEYVAULT3
* Если существует несколько групп ресурсов и будут toodownload журналы только одной группы ресурсов, используйте `-Blob '*/RESOURCEGROUPS/<resource group name>/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/RESOURCEGROUPS/CONTOSORESOURCEGROUP3/*'
* Toodownload все журналы hello месяц hello: Январь 2016 г., используйте `-Blob '*/year=2016/m=01/*'`:

        Get-AzureStorageBlob -Container $container -Context $sa.Context -Blob '*/year=2016/m=01/*'

Вы теперь готовы toostart, просмотрев возможности hello заносит в журнал. Но до перехода, две дополнительные параметры для Get-AzureRmDiagnosticSetting, которые могут потребоваться tooknow:

* состояние hello tooquery параметров диагностики для ресурса хранилища ключей:`Get-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId`
* Ведение журнала toodisable для ресурса хранилища ключей:`Set-AzureRmDiagnosticSetting -ResourceId $kv.ResourceId -StorageAccountId $sa.Id -Enabled $false -Categories AuditEvent`

## <a id="interpret"></a>Интерпретация журналов хранилища ключей
Отдельные BLOB-объекты хранятся как текст в формате JSON. Вот пример записи журнала после выполнения команды `Get-AzureRmKeyVault -VaultName 'contosokeyvault'`:

    {
        "records":
        [
            {
                "time": "2016-01-05T01:32:01.2691226Z",
                "resourceId": "/SUBSCRIPTIONS/361DA5D4-A47A-4C79-AFDD-XXXXXXXXXXXX/RESOURCEGROUPS/CONTOSOGROUP/PROVIDERS/MICROSOFT.KEYVAULT/VAULTS/CONTOSOKEYVAULT",
                "operationName": "VaultGet",
                "operationVersion": "2015-06-01",
                "category": "AuditEvent",
                "resultType": "Success",
                "resultSignature": "OK",
                "resultDescription": "",
                "durationMs": "78",
                "callerIpAddress": "104.40.82.76",
                "correlationId": "",
                "identity": {"claim":{"http://schemas.microsoft.com/identity/claims/objectidentifier":"d9da5048-2737-4770-bd64-XXXXXXXXXXXX","http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn":"live.com#username@outlook.com","appid":"1950a258-227b-4e31-a9cf-XXXXXXXXXXXX"}},
                "properties": {"clientInfo":"azure-resource-manager/2.0","requestUri":"https://control-prod-wus.vaultcore.azure.net/subscriptions/361da5d4-a47a-4c79-afdd-XXXXXXXXXXXX/resourcegroups/contosoresourcegroup/providers/Microsoft.KeyVault/vaults/contosokeyvault?api-version=2015-06-01","id":"https://contosokeyvault.vault.azure.net/","httpStatusCode":200}
            }
        ]
    }


Hello следующей таблице перечислены имена полей hello и описания.

| Имя поля | Описание |
| --- | --- |
| Twitter в режиме реального |Дата и время (в формате UTC). |
| resourceId |Идентификатор ресурса диспетчера ресурсов Azure. Для журналов хранилища ключей это значение всегда равно hello хранилище ключей, идентификатор ресурса. |
| operationName |Имя операции hello, как описано в следующей таблице hello. |
| operationVersion |Это версия интерфейса API REST hello, необходимая для клиента hello. |
| category |Для журналов хранилища ключей AuditEvent значение hello единый, доступны. |
| resultType |Результат запроса REST API. |
| resultSignature |Состояние HTTP. |
| resultDescription |Дополнительное описание о результате hello, если оно доступно. |
| durationMs |Время, затраченное запроса REST API tooservice hello, в миллисекундах. Это не включает hello задержки в сети, поэтому время hello мер на стороне клиента hello может не совпадать с этого времени. |
| callerIpAddress |IP-адрес клиента hello, сделавшего запрос hello. |
| correlationId |Необязательный идентификатор GUID, который hello клиента можно передать toocorrelate клиентские журналы с журналами (хранилище ключей) на стороне службы. |
| identity |Удостоверение из hello токена, который был предоставлен при выполнении запроса API-интерфейса REST hello. Обычно это «пользователь», «субъект-служба» или комбинация «пользователь + идентификатор приложения» при запросе с помощью командлета Azure PowerShell. |
| properties |Это поле будет содержать различные данные на основании hello операцию (Имя_операции). В большинстве случаев содержит сведения о клиенте (hello useragent строка передается по hello клиента), hello точное URI запроса API-Интерфейс REST и код состояния HTTP. Кроме того объект, возвращаемый в результате запроса (например, KeyCreate или VaultGet) он также содержит hello URI ключа (в виде «id»), хранилище URI или URI секрета. |

Hello **Имя_операции** значения полей находятся в формате ObjectVerb. Например:

* Все операции хранилища ключей имеют hello "хранилище`<action>`" форматирования, такие как `VaultGet` и `VaultCreate`.
* Все операции с ключами имеют hello ' ключ`<action>`"форматирования, такие как `KeySign` и `KeyList`.
* Все операции с секретом имеют hello "секрет`<action>`" форматирования, такие как `SecretGet` и `SecretListVersions`.

Hello в следующей таблице перечислены Имя_операции hello и соответствующей команды REST API.

| operationName | Команда API REST |
| --- | --- |
| Authentication |Через конечную точку Azure Active Directory |
| VaultGet |[Получение сведений о хранилище ключей](https://msdn.microsoft.com/en-us/library/azure/mt620026.aspx) |
| VaultPut |[Создание или обновление хранилища ключей](https://msdn.microsoft.com/en-us/library/azure/mt620025.aspx) |
| VaultDelete |[Удаление хранилища ключей](https://msdn.microsoft.com/en-us/library/azure/mt620022.aspx) |
| VaultPatch |[Update a key vault (Создание или обновление хранилища ключей)](https://msdn.microsoft.com/library/azure/mt620025.aspx) |
| VaultList |[Список всех хранилищ ключей в группе ресурсов](https://msdn.microsoft.com/en-us/library/azure/mt620027.aspx) |
| KeyCreate |[Создание ключа](https://msdn.microsoft.com/en-us/library/azure/dn903634.aspx) |
| KeyGet |[Получение сведений о ключе](https://msdn.microsoft.com/en-us/library/azure/dn878080.aspx) |
| KeyImport |[Импорт ключа в хранилище](https://msdn.microsoft.com/en-us/library/azure/dn903626.aspx) |
| KeyBackup |[Создание резервной копии ключа](https://msdn.microsoft.com/en-us/library/azure/dn878058.aspx) |
| KeyDelete |[Удаление ключа](https://msdn.microsoft.com/en-us/library/azure/dn903611.aspx) |
| KeyRestore |[Восстановление ключа](https://msdn.microsoft.com/en-us/library/azure/dn878106.aspx) |
| KeySign |[Вход с помощью ключа](https://msdn.microsoft.com/en-us/library/azure/dn878096.aspx) |
| KeyVerify |[Проверка с помощью ключа](https://msdn.microsoft.com/en-us/library/azure/dn878082.aspx) |
| KeyWrap |[Перенос ключа](https://msdn.microsoft.com/en-us/library/azure/dn878066.aspx) |
| KeyUnwrap |[Развертывание ключа](https://msdn.microsoft.com/en-us/library/azure/dn878079.aspx) |
| KeyEncrypt |[Шифрование с помощью ключа](https://msdn.microsoft.com/en-us/library/azure/dn878060.aspx) |
| KeyDecrypt |[Расшифровка с помощью ключа](https://msdn.microsoft.com/en-us/library/azure/dn878097.aspx) |
| KeyUpdate |[Обновление ключа](https://msdn.microsoft.com/en-us/library/azure/dn903616.aspx) |
| KeyList |[Список ключей hello в хранилище](https://msdn.microsoft.com/en-us/library/azure/dn903629.aspx) |
| KeyListVersions |[Список версий hello ключа](https://msdn.microsoft.com/en-us/library/azure/dn986822.aspx) |
| SecretSet |[Создание секрета](https://msdn.microsoft.com/en-us/library/azure/dn903618.aspx) |
| SecretGet |[Получение сведений о секрете](https://msdn.microsoft.com/en-us/library/azure/dn903633.aspx) |
| SecretUpdate |[Обновление секрета](https://msdn.microsoft.com/en-us/library/azure/dn986818.aspx) |
| SecretDelete |[Удаление секрета](https://msdn.microsoft.com/en-us/library/azure/dn903613.aspx) |
| SecretList |[Список секретов в хранилище](https://msdn.microsoft.com/en-us/library/azure/dn903614.aspx) |
| SecretListVersions |[Список версий секрета](https://msdn.microsoft.com/en-us/library/azure/dn986824.aspx) |

## <a id="loganalytics"></a>Использование Log Analytics

Можно использовать решение хранилища ключей Azure hello в tooreview аналитики журналов, журналов AuditEvent хранилище ключей Azure. Дополнительные сведения, включая tooset это, см. в [решения хранилища ключей Azure в службе анализа журналов](../log-analytics/log-analytics-azure-key-vault.md). В этой статье также содержит инструкции, если вам требуется toomigrate из hello старое хранилище ключей решение, предложенное во время предварительного просмотра анализа журналов hello, где сначала направляться к tooan журналы учетной записи хранилища Azure и настроены службы анализа журналов tooread оттуда.

## <a id="next"></a>Дальнейшие действия
Руководство по использованию хранилища ключей Azure в веб-приложении см. в статье [Использование хранилища ключей Azure из веб-приложения](key-vault-use-from-web-application.md).

Программирование ссылки, в разделе [hello хранилище ключей Azure в руководстве разработчика](key-vault-developers-guide.md).

Полный список командлетов Azure PowerShell 1.0 для хранилища ключей Azure см. в статье [Azure Key Vault Cmdlets](/powershell/module/azurerm.keyvault/#key_vault) (Командлеты хранилища ключей Azure).

Учебник по смены ключей и журнала аудита с хранилищем ключей Azure см. в разделе [как toosetup хранилище ключей с конечным tooend ключа аудит и поворота](key-vault-key-rotation-log-monitoring.md).
