---
title: "Устранение неполадок фабрики данных Azure"
description: "Узнайте, как устранять неполадки при использовании фабрики данных Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 38fd14c1-5bb7-4eef-a9f5-b289ff9a6942
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2018
ms.author: spelluru
robots: noindex
ms.openlocfilehash: d65787c0db2b4e6c7c7d30d69dc77fe25b1ae8d9
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 01/23/2018
---
# <a name="troubleshoot-data-factory-issues"></a>Устранение неполадок фабрики данных
> [!NOTE]
> Статья относится к версии 1 фабрики данных Azure, которая является общедоступной версией. 

В этой статье приводятся советы по устранению неполадок, возникающих при использовании фабрики данных Azure. В этой статье перечислены не все возможные проблемы использования службы, однако рассматриваются некоторые вопросы и приводятся общие рекомендации по устранению неполадок.   

## <a name="troubleshooting-tips"></a>Советы по устранению неполадок
### <a name="error-the-subscription-is-not-registered-to-use-namespace-microsoftdatafactory"></a>Ошибка "Подписка не зарегистрирована для использования пространства имен Microsoft.DataFactory"
Если эта ошибка возникает, поставщик ресурсов фабрики данных Azure не был зарегистрирован на компьютере. Выполните следующее:

1. Запустите Azure PowerShell.
2. Войдите в свою учетную запись Azure с помощью следующей команды:

    ```powershell
    Login-AzureRmAccount
    ```
3. Выполните следующую команду, чтобы зарегистрировать поставщик фабрики данных Azure:

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Проблема: ошибка авторизации при выполнении командлета фабрики данных
Скорее всего, для Azure PowerShell используется неправильная учетная запись или подписка Azure. Чтобы выбрать правильную учетную запись и подписку Azure для Azure PowerShell, используйте такие командлеты:

1. Login-AzureRmAccount — ввод имени пользователя и пароля.
2. Get-AzureRmSubscription — просмотр всех подписок в учетной записи.
3. Select-AzureRmSubscription &lt;имя_подписки&gt; — выбор нужной подписки. Используйте подписку, которая использовалась для создания фабрики данных на портале Azure.

### <a name="problem-fail-to-launch-data-management-gateway-express-setup-from-azure-portal"></a>Проблема: не удается запустить экспресс-установку шлюза управления данными с портала Azure
Для экспресс-установки шлюза управления данными требуется Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce. Если не удается запустить экспресс-установку, выполните одно из следующих действий:

* Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.

    Если вы используете браузер Chrome, перейдите в [интернет-магазин Chrome](https://chrome.google.com/webstore/), введите ClickOnce в строке поиска, а затем выберите и установите одно из расширений ClickOnce.

    То же самое (установку надстройки) сделайте и в случае с браузером Firefox. Нажмите кнопку "Открыть меню" на панели инструментов (три горизонтальные линии в правом верхнем углу), нажмите кнопку "Надстройки", введите "ClickOnce" в строку поиска, выберите одно из расширений ClickOnce и установите его.
* Щелкните ссылку **Установка вручную** в той же колонке на портале. Этот подход используется для скачивания файла установки и его запуска вручную. После успешного завершения установки откроется диалоговое окно настройки шлюза управления данными. Скопируйте **ключ** на экране портала и используйте его в диспетчере конфигурации, чтобы вручную зарегистрировать шлюз в службе.  

### <a name="problem-fail-to-connect-to-on-premises-sql-server"></a>Проблема: не удается подключиться к локальному серверу SQL Server
Запустите **диспетчер конфигурации шлюза управления данными** на компьютере шлюза и используйте вкладку **Устранение неполадок**, чтобы проверить подключение к SQL Server с компьютера шлюза. Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Проблема: срезы входных данных постоянно находятся в состоянии "Waiting"
Срезы могут находиться в состоянии **ожидания** по разным причинам. Одна из распространенных причин — для свойства **external** не задано значение **true**. Все наборы данных, созданные вне фабрики данных Azure, должны быть помечены свойством **external** . Это свойство указывает на то, что данные являются внешними и не поддерживаются какими-либо конвейерами в фабрике данных. После того как данные станут доступны в соответствующем хранилище, срезы данных помечаются флагом **Ready** (готово).

Пример использования свойства **external** приведен ниже. При необходимости можно указать свойство **externalData***, если для свойства external задано значение true.

Дополнительные сведения об этом свойстве см. в статье [Наборы данных](data-factory-create-datasets.md).

```json
{
  "name": "CustomerTable",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "MyLinkedService",
    "typeProperties": {
      "folderPath": "MyContainer/MySubFolder/",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": ";"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      }
    }
  }
}
```

Чтобы устранить эту ошибку, добавьте свойство **external** и дополнительный раздел **externalData** в определение JSON входной таблицы и повторно создайте эту таблицу.

### <a name="problem-hybrid-copy-operation-fails"></a>Проблема: сбой гибридной операции копирования
Действия по устранению неполадок с копированием в локальное хранилище данных и из него с помощью шлюза управления данными см. в статье [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Проблема: сбой подготовки HDInsight по запросу
При использовании связанной службы типа HDInsightOnDemandLinkedService нужно задать имя linkedServiceName, указывающее на хранилище BLOB-объектов Azure. Фабрика данных использует это хранилище для хранения журналов и вспомогательных файлов для кластера HDInsight по запросу.  Иногда подготовка кластера HDInsight по запросу завершается следующей ошибкой:

```
Failed to create cluster. Exception: Unable to complete the cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Обычно эта ошибка указывает на то, что расположение учетной записи хранения, указанной в linkedServiceName, не совпадает с расположением центра обработки данных, в котором происходит подготовка HDInsight. Например, если ваша фабрика данных Azure находится на Западе США (West US), а хранилище Azure расположено на Востоке США (East US), то подготовка по запросу на Западе США выполнена не будет.

Есть еще одно свойство JSON, additionalLinkedServiceNames, где можно указать дополнительные учетные записи хранения в HDInsight по запросу. Эти дополнительные связанные учетные записи хранения должны находиться в том же расположении, что и кластер HDInsight, иначе происходит сбой с той же ошибкой.

### <a name="problem-custom-net-activity-fails"></a>Проблема: сбой настраиваемого действия .NET
Подробные действия см. в разделе [Отладка конвейера с помощью настраиваемого действия](data-factory-use-custom-activities.md#troubleshoot-failures).

## <a name="use-azure-portal-to-troubleshoot"></a>Устранение неполадок с помощью портала Azure
### <a name="using-portal-blades"></a>Использование колонок на портале
Действия см. в статье [Мониторинг конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-a-pipeline).

### <a name="using-monitor-and-manage-app"></a>Использование приложения по мониторингу и управлению
Сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

## <a name="use-azure-powershell-to-troubleshoot"></a>Использование Azure PowerShell для устранения неполадок
### <a name="use-azure-powershell-to-troubleshoot-an-error"></a>Использование Azure PowerShell для устранения ошибок
Сведения см. в разделе [Мониторинг конвейеров фабрики данных с помощью Azure PowerShell](data-factory-build-your-first-pipeline-using-powershell.md#monitor-pipeline).

[adfgetstarted]: data-factory-copy-data-from-azure-blob-storage-to-sql-database.md
[use-custom-activities]: data-factory-use-custom-activities.md
[troubleshoot]: data-factory-troubleshoot.md
[developer-reference]: http://go.microsoft.com/fwlink/?LinkId=516908
[cmdlet-reference]: http://go.microsoft.com/fwlink/?LinkId=517456
[json-scripting-reference]: http://go.microsoft.com/fwlink/?LinkId=516971

[azure-portal]: https://portal.azure.com/

[image-data-factory-troubleshoot-with-error-link]: ./media/data-factory-troubleshoot/DataFactoryWithErrorLink.png

[image-data-factory-troubleshoot-datasets-with-errors-blade]: ./media/data-factory-troubleshoot/DatasetsWithErrorsBlade.png

[image-data-factory-troubleshoot-table-blade-with-problem-slices]: ./media/data-factory-troubleshoot/TableBladeWithProblemSlices.png

[image-data-factory-troubleshoot-activity-run-with-error]: ./media/data-factory-troubleshoot/ActivityRunDetailsWithError.png

[image-data-factory-troubleshoot-dataslice-blade-with-active-runs]: ./media/data-factory-troubleshoot/DataSliceBladeWithActivityRuns.png

[image-data-factory-troubleshoot-walkthrough2-with-errors-link]: ./media/data-factory-troubleshoot/Walkthrough2WithErrorsLink.png

[image-data-factory-troubleshoot-walkthrough2-datasets-with-errors]: ./media/data-factory-troubleshoot/Walkthrough2DataSetsWithErrors.png

[image-data-factory-troubleshoot-walkthrough2-table-with-problem-slices]: ./media/data-factory-troubleshoot/Walkthrough2TableProblemSlices.png

[image-data-factory-troubleshoot-walkthrough2-slice-activity-runs]: ./media/data-factory-troubleshoot/Walkthrough2DataSliceActivityRuns.png

[image-data-factory-troubleshoot-activity-run-details]: ./media/data-factory-troubleshoot/Walkthrough2ActivityRunDetails.png
