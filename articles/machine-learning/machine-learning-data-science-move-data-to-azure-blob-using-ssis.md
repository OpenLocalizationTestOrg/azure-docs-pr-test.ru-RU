---
title: "aaaMove tooor данных из хранилища больших двоичных объектов с помощью соединителей служб SSIS | Документы Microsoft"
description: "Переместите tooor данных из хранилища больших двоичных объектов с помощью соединителей служб SSIS."
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 96a1b5fb-34d1-4b9b-8d99-2bb8289e0398
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 15068af1c69f11e74e109ee5ae2b9f1a674ea388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooor-from-azure-blob-storage-using-ssis-connectors"></a>Tooor перемещения данных из хранилища больших двоичных объектов с помощью соединителей служб SSIS
Hello [SQL Server Integration Services Feature Pack для Azure](https://msdn.microsoft.com/library/mt146770.aspx) предоставляет компоненты tooconnect tooAzure, передачи данных между Azure и локальными источниками данных и обработки данных, хранящихся в Azure.

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

После клиентов перешло локальных данных в облаке hello, их можно открыть из любой службы Azure tooleverage hello всю мощь hello набор технологий Azure. К примеру, их можно использовать в машинном обучении Azure или в кластере HDInsight.

Как правило, это будет первым шагом hello для hello [SQL](machine-learning-data-science-process-sql-walkthrough.md) и [HDInsight](machine-learning-data-science-process-hive-walkthrough.md) пошаговые руководства.

Обсуждение канонические сценарии, использующие tooaccomplish деловых служб SSIS должен Общие в гибридных сценариях интеграции данных, см. в разделе [делать больше с SQL Server Integration Services Feature Pack для Azure](http://blogs.msdn.com/b/ssis/archive/2015/06/25/doing-more-with-sql-server-integration-services-feature-pack-for-azure.aspx) блога.

> [!NOTE]
> Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и слишком[больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).
> 
> 

## <a name="prerequisites"></a>Предварительные требования
tooperform hello задачи, описанные в этой статье, необходимо иметь подписку на Azure и учетную запись хранилища Azure. Необходимо знать вашего хранилища Azure учетная запись имени и учетной записи ключа tooupload или загрузки данных.

* tooset копирование **подписки Azure**, в разделе [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).
* Инструкции по созданию **учетной записи хранения** и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md).

toouse hello **соединители служб SSIS**, необходимо загрузить:

* **SQL Server 2014 или 2016 Standard (или более поздняя версия)**: установка включает в себя SQL Server Integration Services.
* **Microsoft SQL Server 2014 и 2016 пакет дополнительных компонентов интеграции служб для Azure**: они могут быть загружены, соответственно, с hello [SQL Server 2014 Integration Services](http://www.microsoft.com/download/details.aspx?id=47366) и [интеграции SQL Server 2016 Службы](https://www.microsoft.com/download/details.aspx?id=49492) страниц.

> [!NOTE]
> Службы SSIS устанавливается вместе с SQL Server, но не включена в версию Express hello. Сведения о приложениях, которые включены в различные выпуски SQL Server, см. в статье [SQL Server 2016 SP1 editions](http://www.microsoft.com/en-us/server-cloud/products/sql-server-editions/) (Выпуски SQL Server 2016 с пакетом обновления 1 (SP1)).
> 
> 

Обучающие материалы о службах SSIS см. в [этой статье](http://www.microsoft.com/download/details.aspx?id=20766).

Сведения о том, как tooget вверх и запуска с помощью SISS toobuild простого извлечения, преобразования и загрузки (ETL) пакетов, в разделе [учебник по службам SSIS: создание простого ETL-пакета](https://msdn.microsoft.com/library/ms169917.aspx).

## <a name="download-nyc-taxi-dataset"></a>Загрузка набора данных для такси Нью-Йорка
Hello описанном примере здесь использовать публично доступные наборы данных — hello [NYC такси приема-передачи](http://www.andresmh.com/nyctaxitrips/) набора данных. Hello набор данных состоит из такси и около 173 миллионов в NYC года hello 2013. В нем используется два типа данных: сведения о поездках и тарифах. Так как для каждого месяца заведен отдельный файл, всего у нас есть 24 файла, каждый из которых занимает объем примерно 2 ГБ (в несжатом виде).

## <a name="upload-data-tooazure-blob-storage"></a>Отправка больших двоичных объектов хранилища данных tooAzure
данные toomove hello служб SSIS с помощью пакета дополнительных компонентов из локального хранилища больших двоичных объектов tooAzure, мы используем экземпляр hello [ **задача передачи BLOB-объектов Azure**](https://msdn.microsoft.com/library/mt146776.aspx), показано ниже:

![configure-data-science-vm](./media/machine-learning-data-science-move-data-to-azure-blob-using-ssis/ssis-azure-blob-upload-task.png)

Здесь описаны параметры Hello, Здравствуйте, задача использует:

| Поле | Описание |
| --- | --- |
| **AzureStorageConnection** |Указывает существующий диспетчер подключений хранилища Azure или создает новый, ссылается tooan учетной записи хранилища Azure, указывающий файлы больших двоичных объектов hello toowhere размещаются. |
| **BlobContainer** |Указывает имя hello hello контейнер больших двоичных объектов, для хранения файлов hello загружен как большие двоичные объекты. |
| **BlobDirectory** |Указывает каталог больших двоичных объектов hello, где hello отправленный файл хранится как большой двоичный объект блока. каталог больших двоичных объектов Hello — это виртуальная иерархическая структура. Если hello BLOB-объект уже существует, заменить ia ИТ. |
| **LocalDirectory** |Указывает hello локальный каталог, содержащий toobe файлы hello отправлен. |
| **FileName** |Определяет имя фильтра tooselect файлы hello указанным шаблоном имен. Например, MySheet\*.xls\* включает в себя файлы MySheet001.xls и MySheetABC.xlsx. |
| **TimeRangeFrom/TimeRangeTo** |Задает фильтр диапазона времени. Сюда включаются файлы, входящие в диапазон, крайними значениями которого являются *TimeRangeFrom* и *TimeRangeTo*. |

> [!NOTE]
> Hello **AzureStorageConnection** учетные данные нужны toobe правильный и hello **BlobContainer** должна существовать до попытки передачи hello.
> 
> 

## <a name="download-data-from-azure-blob-storage"></a>Загрузка данных из хранилища BLOB-объектов Azure
toodownload данные из локальной tooon хранилища BLOB-объектов Azure с помощью служб SSIS, используйте экземпляр hello [задача передачи BLOB-объектов Azure](https://msdn.microsoft.com/library/mt146779.aspx).

## <a name="more-advanced-ssis-azure-scenarios"></a>Более сложные сценарии SSIS-Azure
пакет дополнительных компонентов служб SSIS Hello допускает более сложные toobe потоков, одновременно обрабатываемых задач упаковки. Например hello больших двоичных объектов может веб-канала данных непосредственно в кластере HDInsight, выходные данные которого может быть загружен задней tooa больших двоичных объектов, а затем tooon локальное хранилище. Службы SSIS могут запускать задания Hive и Pig в кластере HDInsight с помощью дополнительных соединительных служб SSIS.

* скрипт Hive в HDInsight Azure кластера с помощью служб SSIS, используйте toorun [задача Hive для Azure HDInsight](https://msdn.microsoft.com/library/mt146771.aspx).
* сценарий Pig в Azure HDInsight кластера с помощью служб SSIS, используйте toorun [задачу Pig для Azure HDInsight](https://msdn.microsoft.com/library/mt146781.aspx).

