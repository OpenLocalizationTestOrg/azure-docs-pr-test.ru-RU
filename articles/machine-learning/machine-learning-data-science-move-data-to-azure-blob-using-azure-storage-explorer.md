---
title: "aaaMove tooand данных из хранилища больших двоичных объектов с помощью обозревателя хранилищ Azure | Документы Microsoft"
description: "Tooand перемещения данных из хранилища больших двоичных объектов с помощью обозревателя хранилищ Azure"
services: machine-learning,storage
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 10bd283f-0875-4c67-af63-6492270b7656
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 38d3bc009950c97d8474b0acceaf74814638dac0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-blob-storage-using-azure-storage-explorer"></a>Tooand перемещения данных из хранилища больших двоичных объектов с помощью обозревателя хранилищ Azure
Azure Storage Explorer является бесплатное средство корпорации Майкрософт, который позволяет вам toowork с данными хранилища Azure для Windows, macOS и Linux. В этом разделе описывается способ toouse его tooupload и загрузки данных из Azure хранилище больших двоичных объектов. Hello средство можно загрузить из [Microsoft Azure Storage Explorer](http://storageexplorer.com/).

[!INCLUDE [blob-storage-tool-selector](../../includes/machine-learning-blob-storage-tool-selector.md)]

> [!NOTE]
> При использовании виртуальной Машины, которая была настроена с помощью сценариев hello, предоставляемые [обработки и анализа данных в виртуальных машинах в Azure](machine-learning-data-science-virtual-machines.md), то обозреватель хранилища Azure уже установлены на hello виртуальной Машины.
> 
> [!NOTE]
> Хранилище больших двоичных объектов tooAzure подробное введение, см. в разделе слишком[основы больших двоичных объектов Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) и [больших двоичных объектов Azure](https://msdn.microsoft.com/library/azure/dd179376.aspx).   
> 
> 

## <a name="prerequisites"></a>Предварительные требования
В этом документе предполагается, что подписка Azure, учетная запись хранения и hello соответствующий ключ хранилища для этой учетной записи. Чтобы отправлять и скачивать данные, необходимо знать имя учетной записи хранения Azure и ее ключ. 

* tooset копирование подписку Azure, см. [бесплатной пробной версии один месяц](https://azure.microsoft.com/pricing/free-trial/).
* Инструкции по созданию учетной записи хранения и получению сведений об учетной записи и ключах см. в статье [Об учетных записях хранения Azure](../storage/common/storage-create-storage-account.md). Сделать Примечание hello ключ доступа для вашей учетной записи, необходимо, чтобы эта учетная запись toohello tooconnect ключа с помощью средства обозревателя хранилищ Azure hello.
* Средство обозревателя хранилищ Azure Hello можно загрузить из [Microsoft Azure Storage Explorer](http://storageexplorer.com/). Примите значения по умолчанию hello во время установки.

<a id="explorer"></a>

## <a name="use-azure-storage-explorer"></a>Использование обозревателя хранилищ Azure
Здравствуйте, следующие шаги документа как tooupload загрузку данных с помощью обозревателя хранилищ Azure. 

1. Запустите Microsoft Azure Storage Explorer.
2. toobring копирование hello **tooyour учетная запись для входа...**  мастера выберите **параметры учетной записи Azure** значок, затем **добавить учетную запись** и введите учетные данные. ![Добавление учетной записи хранения Azure](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/add-an-azure-store-account.png)
3. toobring копирование hello **подключения tooAzure хранения** приветствия мастера, выберите **подключения хранилища tooAzure** значок. ![Подключения tooAzure хранилища](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-1.png)
4. Введите ключ доступа hello из вашей учетной записи хранилища Azure на hello **подключения tooAzure хранения** мастера и затем **Далее**. ![Подключения tooAzure хранилища](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/connect-to-azure-storage-2.png)
5. Введите имя учетной записи хранения в hello **имя учетной записи** и затем выберите **Далее**. ![Подключение внешнего хранилища](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/attach-external-storage.png)
6. добавить учетную запись хранения Hello теперь должна быть указана. toocreate контейнер больших двоичных объектов в учетной записи хранилища, щелкните правой кнопкой мыши hello **контейнеров больших двоичных объектов** узла в этой учетной записи, выберите **создать контейнер больших двоичных объектов**и введите имя.
7. контейнер tooa tooupload данных, выберите hello целевой контейнер и нажмите кнопку hello **отправить** кнопки.![ Учетные записи хранения](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/storage-accounts.png)
8. Щелкните hello **...**  toohello справа от приветствия **файлы** , выберите один или несколько файлов tooupload hello файловой системе и нажмите кнопку **отправить** toobegin, передача файлов hello.![ Отправка файлов](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/upload-files-to-blob.png)
9. toodownload данных, выбрав hello большого двоичного объекта в соответствующий контейнер toodownload hello и нажмите кнопку **загрузить**. ![Скачивание файлов](./media/machine-learning-data-science-move-data-to-azure-blob-using-azure-storage-explorer/download-files-from-blob.png)

