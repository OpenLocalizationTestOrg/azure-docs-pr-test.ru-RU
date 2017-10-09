---
title: "проблемы aaaTroubleshoot фабрики данных Azure"
description: "Узнайте, как tootroubleshoot проблемы с помощью фабрики данных Azure."
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
ms.date: 08/14/2017
ms.author: spelluru
ms.openlocfilehash: cf65bcf3e1c3f061d3ac1dbf32e99cc7b014f9dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-data-factory-issues"></a>Устранение неполадок фабрики данных
В этой статье приводятся советы по устранению неполадок, возникающих при использовании фабрики данных Azure. В этой статье не включает все возможные причины неполадок hello, при использовании службы hello, однако он охватывает некоторые проблемы и Общие советы по устранению неполадок.   

## <a name="troubleshooting-tips"></a>Советы по устранению неполадок
### <a name="error-hello-subscription-is-not-registered-toouse-namespace-microsoftdatafactory"></a>Ошибка: hello подписки не зарегистрированного toouse пространством имен «Microsoft.DataFactory»
Если эта ошибка поставщика ресурсов hello фабрики данных Azure не был зарегистрирован на компьютере. Здравствуйте, следующие:

1. Запустите Azure PowerShell.
2. Войдите в систему tooyour учетная запись Azure с помощью hello следующую команду.

    ```powershell
    Login-AzureRmAccount
    ```
3. Выполните следующие команды tooregister hello фабрики данных Azure поставщика hello.

    ```powershell        
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```

### <a name="problem-unauthorized-error-when-running-a-data-factory-cmdlet"></a>Проблема: ошибка авторизации при выполнении командлета фабрики данных
Возможно, не используются hello справа учетной записи Azure или подписок с hello Azure PowerShell. Используйте следующие командлеты tooselect hello справа Azure toouse учетной записи и подписки с hello Azure PowerShell hello.

1. AzureRmAccount входа - используйте hello правой пользователя и пароль
2. Get-AzureRmSubscription - представление всех hello подписки для учетной записи hello.
3. Выберите AzureRmSubscription &lt;имя подписки&gt; -выберите подходящую подписку hello. Используйте hello один на портал Azure hello используется toocreate фабрики данных.

### <a name="problem-fail-toolaunch-data-management-gateway-express-setup-from-azure-portal"></a>Проблема: Не toolaunch экспресс-установки данных управления шлюза с портала Azure
Установка экспресс-выпуск Hello для hello шлюз управления данными требуется Internet Explorer или браузер, совместимый Microsoft ClickOnce. При сбое установки Express hello toostart выполните одно из следующих hello.

* Используйте Internet Explorer или другой веб-браузер, совместимый с Microsoft ClickOnce.

    При использовании Chrome go toohello [Chrome веб-хранилище](https://chrome.google.com/webstore/)поиска с ключевым словом «ClickOnce», выбрав один из модулей ClickOnce hello и установить его.

    Здравствуйте же для Firefox (установка надстройки). Нажмите кнопку Открыть меню на панели инструментов hello (три горизонтальные линии в правом верхнем углу hello), выберите дополнительные компоненты, поиска с ключевым словом «ClickOnce», выбрать один из модулей ClickOnce hello и установить его.
* Используйте hello **ручной установки** ссылки, представленной на hello же колонке hello портала. Используйте этот подход toodownload установочный файл и запустить его вручную. После успешного завершения установки hello, появится диалоговое окно настройки шлюза управления данными hello. Копировать hello **ключ** из портала экран приветствия и используйте его в hello configuration manager toomanually зарегистрируйте шлюз hello службе hello.  

### <a name="problem-fail-tooconnect-tooon-premises-sql-server"></a>Проблема: Не tooconnect tooon локальный SQL Server
Запустите **диспетчера конфигурации шлюза управления данными** на компьютере шлюза hello и использовать hello **Устранение неполадок** вкладке tooSQL подключения tootest hello Server с компьютера шлюза hello. Советы по устранению неполадок, связанных со шлюзом или подключением, см. в разделе [Устранение неполадок в работе шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues).   

### <a name="problem-input-slices-are-in-waiting-state-for-ever"></a>Проблема: срезы входных данных постоянно находятся в состоянии "Waiting"
Hello срезы могут находиться в **ожидания** состояния из-за причин toovarious. Одной из распространенных причин hello является, hello **внешних** свойство не задано слишком**true**. Любой набор данных, производимых hello вне области фабрики данных Azure должны быть отмечены **внешних** свойство. Это свойство указывает, что данные hello внешний и не резервная копия по любой конвейера в фабрике данных hello. срезы данных Hello, помечаются как **готовности** после hello данные недоступны в хранилище соответствующие hello.

См. следующий пример использования hello hello hello **внешних** свойство. Дополнительно можно указать **externalData*** при задании внешнего tootrue.

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

tooresolve Здравствуйте ошибки, добавьте hello **внешних** свойство и необязательный hello **externalData** статьи toohello JSON определение входной таблицы hello и заново создайте таблицу hello.

### <a name="problem-hybrid-copy-operation-fails"></a>Проблема: сбой гибридной операции копирования
В разделе [Устранение неполадок шлюза](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) для хранения tootroubleshoot проблемы с копированием из локальных данных с помощью действия hello шлюз управления данными.

### <a name="problem-on-demand-hdinsight-provisioning-fails"></a>Проблема: сбой подготовки HDInsight по запросу
При использовании связанной службы типа HDInsightOnDemand, необходимо toospecify linkedServiceName, который указывает tooan хранилища больших двоичных объектов. Служба фабрики данных использует это хранилище toostore журналы и вспомогательные файлы для кластера HDInsight по требованию.  Иногда подготовки кластера HDInsight по требованию завершается hello следующая ошибка:

```
Failed toocreate cluster. Exception: Unable toocomplete hello cluster create operation. Operation failed with code '400'. Cluster left behind state: 'Error'. Message: 'StorageAccountNotColocated'.
```

Эта ошибка обычно указывает, что расположение hello hello учетной записи хранения указан в hello linkedServiceName не hello местоположении, где происходит Подготовка HDInsight hello центра обработки данных и те же данные. Пример: Если фабрики данных является на Западе США и hello хранилища Azure находится в США, Восток, hello подготовки завершается с ошибкой по запросу на Западе США.

Есть еще одно свойство JSON, additionalLinkedServiceNames, где можно указать дополнительные учетные записи хранения в HDInsight по запросу. Эти дополнительные связанные учетные записи хранения должно быть в hello местоположения кластера HDInsight hello, или она завершается ошибкой с hello же ошибка.

### <a name="problem-custom-net-activity-fails"></a>Проблема: сбой настраиваемого действия .NET
Подробные действия см. в разделе [Отладка конвейера с помощью настраиваемого действия](data-factory-use-custom-activities.md#troubleshoot-failures).

## <a name="use-azure-portal-tootroubleshoot"></a>Использование Azure tootroubleshoot портала
### <a name="using-portal-blades"></a>Использование колонок на портале
Действия см. в статье [Мониторинг конвейера](data-factory-build-your-first-pipeline-using-editor.md#monitor-pipeline).

### <a name="using-monitor-and-manage-app"></a>Использование приложения по мониторингу и управлению
Сведения см. в статье [Мониторинг конвейеров фабрики данных Azure и управление ими с помощью приложения по мониторингу и управлению](data-factory-monitor-manage-app.md).

## <a name="use-azure-powershell-tootroubleshoot"></a>Использовать tootroubleshoot Azure PowerShell
### <a name="use-azure-powershell-tootroubleshoot-an-error"></a>Использование Azure PowerShell tootroubleshoot ошибку
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
