---
title: "aaaUse Azure портала tooget к выполнению хранилища Озера данных | Документы Microsoft"
description: "Использовать hello Azure toocreate портала учетной записи хранилища Озера данных и выполнения основных операций в hello хранилища Озера данных"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: fea324d0-ad1a-4150-81f0-8682ddb4591c
ms.service: data-lake-store
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/06/2017
ms.author: nitinme
ms.openlocfilehash: 6bb3413f00bfa4393f08aed18bc1d5f8a2f28fc5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-hello-azure-portal"></a>Приступая к работе с hello портал Azure с помощью хранилища Озера данных Azure
> [!div class="op_single_selector"]
> * [Портал](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [Пакет SDK для .NET](data-lake-store-get-started-net-sdk.md)
> * [Пакет SDK для Java](data-lake-store-get-started-java-sdk.md)
> * [REST API](data-lake-store-get-started-rest-api.md)
> * [Azure CLI 2.0](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
> 

Узнайте, как toouse hello Azure toocreate портала учетной записи хранилища Озера данных Azure и выполнения основных операций, таких как создание папками, отправка и загрузка файлов данных, удалите учетную запись, и т. д. Дополнительные сведения см. в [обзоре Azure Data Lake Store](data-lake-store-overview.md).

содержит следующие два видео Hello hello же сведения, как описано в этой статье:

* [Создание учетной записи хранения озера данных](https://mix.office.com/watch/1k1cycy4l4gen)
* [Управление данными в хранилище Озера данных с помощью hello обозреватель данных](https://mix.office.com/watch/icletrxrh6pc)

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь hello следующих элементов:

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).

## <a name="create-an-azure-data-lake-store-account"></a>Создание учетной записи хранения озера данных Azure

1. Войдите на новый toohello [портал Azure](https://portal.azure.com).
2. Щелкните **СОЗДАТЬ**, щелкните **Данные + хранилище**, а затем — **Azure Data Lake Store**. Прочитать данные hello в hello **хранилища Озера данных Azure** и, при необходимости нажмите кнопку **создать** в hello нижний левый угол колонка hello.
3. В hello **хранилища Озера данных New** колонке предоставления hello значения, как показано в следующий снимок экрана приветствия:
   
    ![Создание учетной записи Azure Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.New.Account.png "Создание учетной записи Azure Data Lake")
   
   * **Имя**. Введите уникальное имя для hello хранилища Озера данных.
   * **Подписка**. Выберите подписку hello, из которой требуется toocreate новую учетную запись хранилища Озера данных.
   * **Группа ресурсов**: выберите существующую группу ресурсов Azure или создайте новую группу. Выберите существующую группу ресурсов или hello **создать новый** toocreate параметр один. Группа ресурсов представляет собой контейнер, содержащий связанные ресурсы для приложения. Дополнительные сведения см. в разделе [Группы ресурсов](../azure-resource-manager/resource-group-overview.md#resource-groups).
   * **Расположение**: выберите расположение, где требуется учетная запись хранилища Озера данных hello toocreate.
   * **Параметры шифрования**. Доступны три параметра:
     
     * **Не включать шифрование**.
     * **Использовать ключи, управляемые Azure Data Lake**  Если вы хотите toomanage хранилища Озера данных Azure, ключей шифрования.
     * **Выбрать ключи из Azure Key Vault**. Вы можете выбрать существующее хранилище Azure Key Vault или создать новое. toouse hello ключи из хранилища ключей, необходимо назначить разрешения для учетной записи хранилища Озера данных Azure, что tooaccess hello хранилище ключей Azure hello. Hello инструкции см. в разделе [назначить разрешения tooAzure хранилище ключей](#assign-permissions-to-azure-key-vault).
       
        ![Шифрование Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-2.png "Шифрование Data Lake Store")
       
        Нажмите кнопку **ОК** в hello **параметры шифрования** колонку.

        Дополнительные сведения см. в статье [Шифрование данных в Azure Data Lake Store](./data-lake-store-encryption.md).

4. Щелкните **Создать**. Если выбрана панель мониторинга toohello toopin hello учетной записи, вы вернетесь toohello панели мониторинга, и вы можете следить за ходом hello подготовку учетных записей хранилища Озера данных. Один раз подготавливается hello хранилища Озера данных, отображается колонке hello учетной записи.

Вы можете также создать учетную запись Data Lake Store, используя шаблоны Azure Resource Manager. Эти шаблоны доступны на сайте [шаблонов быстрого запуска Azure](https://azure.microsoft.com/resources/templates/?term=data+lake+store).

- Шаблон без шифрования: [Deploy Azure Data Lake Store account with no data encryption](https://azure.microsoft.com/en-us/resources/templates/101-data-lake-store-no-encryption/) (Развертывание учетной записи Azure Data Lake Store без шифрования данных).
- С шифрованием данных с помощью Data Lake Store: [Deploy Data Lake Store account with encryption (Data Lake)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-adls/) (Развертывание учетной записи Data Lake Store с шифрованием данных (Data Lake)).
- С шифрованием данных с помощью Azure Key Vault: [Deploy Data Lake Store account with encryption (Key Vault)](https://azure.microsoft.com/resources/templates/101-data-lake-store-encryption-key-vault/) (Развертывание учетной записи Data Lake Store с шифрованием данных (Key Vault)).

### <a name="assign-permissions-to-azure-key-vault"></a>Назначьте разрешения tooAzure хранилища ключей
Если ключи из хранилища ключей Azure для шифрования tooconfigure используется на hello хранилища Озера данных, необходимо настроить доступ между учетной записи хранилища Озера данных hello и hello хранилище ключей Azure. Выполните hello, поэтому следующие шаги toodo.

1. При использовании ключей из хранилища ключей Azure hello hello колонке hello хранилища Озера данных отображает предупреждение, верхней hello. Нажмите кнопку hello предупреждение tooopen hello **настроить разрешения хранилища ключей** колонку.
   
    ![Шифрование Data Lake Store](./media/data-lake-store-get-started-portal/adls-encryption-3.png "Шифрование Data Lake Store")
2. Hello колонке показано два параметры tooconfigure подключение.
   
   * В hello первый вариант, нажмите кнопку **предоставить разрешение** tooconfigure доступа. Первый параметр Hello становится доступен только в том случае, если пользователь hello, который создал учетную запись хранилища Озера данных hello также имеет права администратора для hello хранилище ключей Azure.
   * Hello другой вариант — командлет PowerShell hello toorun, отображаются в колонке hello. Требуется владелец hello toobe hello хранилище ключей Azure или hello возможность toogrant на разрешение hello хранилище ключей Azure. После выполнения командлета hello вернитесь toohello колонки и нажмите кнопку **включить** tooconfigure доступа.

## <a name="createfolder"></a>Создание папок в учетной записи хранения озера данных Azure
Можно создать папки под вашей toomanage учетной записи хранилища Озера данных и хранения данных.

1. Открыть учетную запись хранилища Озера данных hello, созданный вами. Hello левой панели щелкните **Обзор**, нажмите кнопку **хранилища Озера данных**и щелкните hello имя учетной записи, под которой вы хотите toocreate папки из хранилища Озера данных колонке hello. Если закрепить начальной hello учетной записи toohello панели щелкните плитку этой учетной записи.
2. В колонке учетной записи «Хранилище озера данных» щелкните **Обозреватель данных**.
   
    ![Создание папок в учетной записи Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Create.Folder.png "Создание папок в учетной записи Data Lake Store")
3. В колонке учетной записи в хранилище Озера данных, нажмите кнопку **новую папку**, введите имя новой папки hello и нажмите кнопку **ОК**.
   
    ![Создание папок в учетной записи Data Lake Store](./media/data-lake-store-get-started-portal/ADL.Folder.Name.png "Создание папок в учетной записи Data Lake Store")
   
    вновь созданные Hello папки, перечисленные в hello **обозреватель данных** колонку. Вы можете создавать вложенные папки любого уровня.
   
    ![Создание папок в учетной записи Data Lake](./media/data-lake-store-get-started-portal/ADL.New.Directory.png "Создание папок в учетной записи Data Lake")

## <a name="uploaddata"></a>Отправка учетной записи хранилища Озера данных tooAzure данных
Можно передать вашей tooan данные учетной записи хранилища Озера данных Azure непосредственно в hello корневого уровня или tooa папку, созданную в пределах учетной записи hello. Hello следующий снимок экрана, следуйте tooupload действия hello вложенную папку файл tooa из hello **обозреватель данных** колонку. В этом снимке экрана hello файл является вложенной отправленного tooa показано адресная строка hello (помеченные в красный прямоугольник).

Если вы ищете некоторые tooupload образец данных, вы можете получить hello **скорая помощь данных** папку из hello [репозитории Озера данных Azure](https://github.com/MicrosoftBigData/usql/tree/master/Examples/Samples/Data/AmbulanceData).

![Отправка данных](./media/data-lake-store-get-started-portal/ADL.New.Upload.File.png "Отправка данных")

## <a name="properties"></a>Свойства и действия, доступные на hello хранимые данные
Нажмите кнопку hello добавленный файл tooopen hello **свойства** колонку. Hello свойства, связанные с файлом hello и hello действия, которые можно выполнить для файла hello доступны в этой колонке. Можно также скопировать toofile hello полный путь в вашей учетной записи хранилища Озера данных Azure, выделяются в поле hello красный hello следующий снимок экрана:

![Свойства данных hello](./media/data-lake-store-get-started-portal/ADL.File.Properties.png "свойства данных hello")

* Нажмите кнопку **предварительного просмотра** toosee возможность предварительного просмотра файла hello, непосредственно из браузера hello. Можно указать формат hello также предварительного просмотра hello. Нажмите кнопку **предварительного просмотра**, нажмите кнопку **формат** в hello **Просмотр файлов** колонке и в hello **Предварительная версия формата файла** колонке указания таких параметров hello как число строк toodisplay кодировка toouse, toouse разделитель, и т. д.
  
  ![Формат просмотра файла](./media/data-lake-store-get-started-portal/ADL.File.Preview.png "Формат просмотра файла")
* Нажмите кнопку **загрузки** toodownload hello файл tooyour компьютера.
* Нажмите кнопку **переименования файла** toorename hello файла.
* Нажмите кнопку **удалите файл** toodelete файл hello.

## <a name="secure-your-data"></a>Защита данных
Можно защитить hello данные, хранящиеся в вашей учетной записи хранилища Озера данных Azure с помощью Azure Active Directory и управления доступом (ACL). Дополнительные сведения о toodo, в разделе [защиты данных в хранилище Озера данных Azure](data-lake-store-secure-data.md).

## <a name="delete-azure-data-lake-store-account"></a>Удаление учетной записи хранения озера данных Azure
Выберите учетную запись хранилища Озера данных Azure, в колонке хранилища Озера данных toodelete **удалить**. Действие hello tooconfirm, вы будете имя hello запрашиваемые tooenter hello учетной записи, которые вы будете toodelete. Введите имя учетной записи hello hello и нажмите кнопку **удалить**.

![Удаление учетной записи Data Lake](./media/data-lake-store-get-started-portal/ADL.Delete.Account.png "Удаление учетной записи Data Lake")

## <a name="next-steps"></a>Дальнейшие действия
* [Защита данных в хранилище озера данных](data-lake-store-secure-data.md)
* [Использование аналитики озера данных Azure с хранилищем озера данных](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [Использование Azure HDInsight с хранилищем озера данных](data-lake-store-hdinsight-hadoop-use-portal.md)
* [Доступ к журналам диагностики Azure Data Lake Store](data-lake-store-diagnostic-logs.md)

