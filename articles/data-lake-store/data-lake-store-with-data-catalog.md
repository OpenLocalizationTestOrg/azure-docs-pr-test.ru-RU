---
title: "aaaRegister данные из хранилища Озера данных в каталоге данных Azure | Документы Microsoft"
description: "Регистрация данных из хранилища озера данных в каталоге данных Azure"
services: data-lake-store,data-catalog
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3294d91e-a723-41b5-9eca-ace0ee408a4b
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 3e895b42cab4ba39d288950763312a243883cbdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="register-data-from-data-lake-store-in-azure-data-catalog"></a>Регистрация данных из хранилища озера данных в каталоге данных Azure
В этой статье вы узнаете, как toointegrate Azure Озера данных хранения с toomake каталога данных Azure данных обнаружения в пределах организации интегрируя с помощью каталога данных. Дополнительные сведения о каталогизации данных см. в статье [Каталог данных Azure](../data-catalog/data-catalog-what-is-data-catalog.md). toounderstand сценарии, в которых можно использовать каталог данных. в разделе [каталога данных Azure распространенные сценарии](../data-catalog/data-catalog-common-scenarios.md).

## <a name="prerequisites"></a>Предварительные требования
Прежде чем начать работу с учебником, необходимо иметь следующие hello.

* **Подписка Azure**. Ознакомьтесь с [бесплатной пробной версией Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Настройте свою подписку Azure** для использования общедоступной предварительной версии Data Lake Store. Ознакомьтесь с [инструкциями](data-lake-store-get-started-portal.md).
* **Учетная запись хранилища озера данных Azure**. Следуйте инструкциям hello в [Приступая к работе с хранилища Озера данных Azure, с помощью портала Azure hello](data-lake-store-get-started-portal.md). Давайте в целях этого учебника создадим учетную запись хранилища данных озера и назовем ее **datacatalogstore**.

    После создания учетной записи hello, отправьте tooit образец набора данных. В этом учебнике, сообщите нам отправить все файлы CSV-файл hello в hello **AmbulanceData** папки в hello [репозитории Озера данных Azure](https://github.com/Azure/usql/tree/master/Examples/Samples/Data/AmbulanceData/). Можно использовать различные клиенты, такие как [обозреватель хранилищ Azure](http://storageexplorer.com/), контейнер больших двоичных объектов tooa tooupload данных.
* **Каталог данных Azure**. В организации уже должен быть создан каталог данных Azure. Для каждой организации допускается только один каталог.

## <a name="register-data-lake-store-as-a-source-for-data-catalog"></a>Регистрация хранилища озера данных в качестве источника для каталога данных

> [!VIDEO https://channel9.msdn.com/Series/AzureDataLake/ADCwithADL/player]

1. Go слишком`https://azure.microsoft.com/services/data-catalog`и нажмите кнопку **начать**.
2. Войдите на портал каталога данных Azure hello и щелкните **публикации данных**.

    ![Регистрация источника данных](./media/data-lake-store-with-data-catalog/register-data-source.png "Регистрация источника данных")
3. На следующей странице приветствия нажмите кнопку **запустить приложение**. Будет загружен файл манифеста приложения hello на вашем компьютере. Дважды щелкните toostart hello hello файл манифеста приложения.
4. На начальной странице приветствия нажмите кнопку **входа**и введите свои учетные данные.

    ![Экран приветствия](./media/data-lake-store-with-data-catalog/welcome.screen.png "Экран приветствия")
5. На hello выбора источника данных страницы, выберите **Озера данных Azure**, а затем нажмите кнопку **Далее**.

    ![Выбор источника данных](./media/data-lake-store-with-data-catalog/select-source.png "Выбор источника данных")
6. На следующей странице приветствия обеспечивают hello имя учетной записи хранилища Озера данных, которые должны tooregister в каталог данных. Оставьте hello другие параметры по умолчанию и нажмите кнопку **Connect**.

    ![Подключить источник toodata](./media/data-lake-store-with-data-catalog/connect-to-source.png "источника toodata Connect")
7. Следующая страница приветствия можно разделить на следующие сегменты hello.

    а. Hello **иерархии сервера** прямоугольник представляет структуру папок для учетной записи хранилища Озера данных hello. **$Root** представляет hello корневой учетной записи хранилища Озера данных, и **AmbulanceData** представляет hello папку, созданную на корень hello hello хранилища Озера данных.

    b. Hello **доступные объекты** содержит список hello файлы и папки внутри hello **AmbulanceData** папки.

    c. **Поле зарегистрированные объекты toobe** hello списки файлов и папок, которые должны tooregister в каталоге данных Azure.

    ![Просмотр структуры данных](./media/data-lake-store-with-data-catalog/view-data-structure.png "Просмотр структуры данных")
8. В этом учебнике необходимо зарегистрировать все файлы hello в каталоге hello. Для этого щелкните hello (![перемещение объектов](./media/data-lake-store-with-data-catalog/move-objects.png "перемещение объектов")) toomove кнопку Здравствуйте, все файлы слишком**toobe объектов зарегистрирован** поле.

    Поскольку hello данных будет зарегистрирован в каталог данных организации, это рекомендуемых подходов tooadd некоторые метаданные, который можно использовать позже tooquickly нахождения данных hello. Например можно добавить адрес электронной почты владельца данных hello (например, по одному, передача данных hello) или добавить тег tooidentify hello данным. Снимок экрана приветствия ниже показано тег, достаточно добавить toohello данных.

    ![Просмотр структуры данных](./media/data-lake-store-with-data-catalog/view-selected-data-structure.png "Просмотр структуры данных")

    Щелкните **Зарегистрировать**.
9. Hello следующий снимок экрана означает, что данные hello успешно зарегистрирован в hello каталога данных.

    ![Регистрация завершена](./media/data-lake-store-with-data-catalog/registration-complete.png "Просмотр структуры данных")
10. Нажмите кнопку **портала представление** toogo резервное toohello портала каталога данных и убедитесь, что теперь можно hello доступа зарегистрированных данных через портал hello. toosearch hello данных, можно использовать hello тег, который вы использовали при регистрации данных hello.

     ![Поиск данных в каталоге](./media/data-lake-store-with-data-catalog/search-data-in-catalog.png "Поиск данных в каталоге")
11. Теперь можно выполнять такие операции, как добавление заметок и документации toohello данных. Дополнительные сведения см. в разделе hello ссылкам.

    * [Создание заметок к источникам данных](../data-catalog/data-catalog-how-to-annotate.md)
    * [Создание документации по источникам данных](../data-catalog/data-catalog-how-to-documentation.md)

## <a name="see-also"></a>Дополнительные материалы
* [Создание заметок к источникам данных](../data-catalog/data-catalog-how-to-annotate.md)
* [Создание документации по источникам данных](../data-catalog/data-catalog-how-to-documentation.md)
* [Интеграция хранилища озера данных с другими службами Azure](data-lake-store-integrate-with-other-services.md)
