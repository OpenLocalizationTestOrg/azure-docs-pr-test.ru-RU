---
title: "Отправка файлов в учетную запись служб мультимедиа Azure с помощью Aspera | Документация Майкрософт"
description: "Этот учебник поможет выполнить необходимые действия по передаче файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа с помощью ** Aspera Server по запросу ** службы в Azure."
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: e3090da9b2c5b8f99545a1f7f9601bfd8d5221f1
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="upload-files-into-a-media-services-account-using-the-aspera-server-on-demand-service-on-azure"></a>Отправка файлов в учетную запись служб мультимедиа с помощью службы Aspera Server On Demand в Azure

## <a name="overview"></a>Обзор

**Aspera** — это программное обеспечение для высокоскоростной передачи файлов. **Aspera Server On Demand** для Azure позволяет быстро отправлять большие файлы непосредственно в хранилище BLOB-объектов Azure и скачивать их из него. Дополнительные сведения о службе **Aspera On Demand** см. на сайте [Aspera Cloud](http://cloud.asperasoft.com/). 
  
**Aspera Server On Demand** для Azure можно приобрести в [Azure Marketplace](https://azure.microsoft.com/en-us/marketplace/). Чтобы купить **Aspera Server On Demand**, войдите в Azure Marketplace с помощью учетной записи Windows Live ID.

Из этого руководства вы узнаете, как отправлять файлы в учетную запись хранилища, связанную с учетной записью служб мультимедиа, с помощью службы **Aspera Server On Demand** в Azure. 

Пример, в котором показано, как пользоваться функциями Azure со службами мультимедиа и Aspera, вы можете найти [здесь](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Существует ограничение на максимальный размер файла, который могут обработать службы мультимедиа Azure. Подробные сведения об этом см. [здесь](media-services-quotas-and-limitations.md).
>

## <a name="prerequisites"></a>Предварительные требования 

Для работы с этим руководством необходимы указанные ниже компоненты.

* Учетная запись Windows Live ID.
* [Учетная запись Azure](https://azure.microsoft.com). Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
* [Учетная запись служб мультимедиа Azure](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Покупка службы Aspera On Demand для Azure

Войдя в Azure Marketplace, выполните следующие действия, чтобы приобрести службу Aspera On Demand для Azure.

1. Выполните поисковый запрос Aspera и выберите Server On Demand.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Просмотрите планы подписки и нажмите кнопку регистрации.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Укажите необходимые сведения для оформления подписки на службу Server on Demand.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Щелкните **Ценовая категория** и в открывшейся колонке выберите требуемый месячный объем. В колонке **Сведения о плане** нажмите кнопку **ОК**. Затем в колонке **Выбор ценовой категории** нажмите кнопку **Выбрать**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Щелкните **Условия**, а затем в открывшейся колонке просмотрите и примите условия использования. После этого нажмите кнопку **Приобрести**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Завершите покупку, нажав кнопку **Создать**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. На панели мониторинга Azure отобразится уведомление о том, что выполняется подготовка службы.  Когда она завершиться, новую подписку можно будет найти среди ресурсов путем поиска по имени службы. Найдя службу, дважды щелкните ее, чтобы открыть портал управления службами.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Откройте портал управления Aspera. Обнаружив свою новую службу Aspera, щелкните ее, чтобы получить доступ к порталу управления.  Откроется новая панель. На ней необходимо щелкнуть **имя ресурса** новой службы.  На следующем снимке экрана имя ресурса — это AsperaTransferDemo. Когда вы щелкните имя ресурса, откроется еще одна панель. На ней вы увидите кнопку "Управление". Нажмите эту кнопку, чтобы открыть портал управления Aspera.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Нажав кнопку "Управление", вы перейдете на страницу регистрации, которая необходима для доступа к службе.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. На этом этапе у вас должен быть доступ к порталу управления службами Aspera, на котором можно создавать ключи доступа, скачивать клиенты и лицензии Aspera, просматривать данные об использовании и получать сведения об интерфейсах API.

    На снимке экрана ниже показан процесс получения доступа. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    На следующем снимке экрана показаны интерфейсы отчетов об использовании на портале. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Отправка файлов с помощью Aspera

1. Скачайте и установите клиентское программное обеспечение Aspera:
    
    * [подключаемый модуль браузера](http://downloads.asperasoft.com/connect2/);
    * [полнофункциональный клиент](http://downloads.asperasoft.com/en/downloads/2).

2. Выполните первую передачу. Чтобы использовать клиент Aspera для передачи с помощью службы передачи Aspera, необходимо сделать следующее: 

    1. Создайте на портале Aspera ключ доступа.  
    2. Скачайте и установите клиент Aspera, а также активируйте лицензию (программное обеспечение можно найти на портале Aspera).  

    >[!NOTE]
    >Сведения о конфигурации содержатся в руководстве по клиенту Aspera, с которым рекомендуется ознакомиться.
    
    3. С помощью [портала Azure](https://portal.azure.com/) получите некоторые данные вашей учетной записи хранения, связанной с учетной записью служб мультимедиа Azure. В частности, имя, ключ и имя контейнера хранилища BLOB-объектов, в котором необходимо разместить содержимое. 

        * Для получения сведений о хранилище на портале сделайте следующее: найдите учетную запись хранения, щелкните ключи доступа и скопируйте имя и ключ своей учетной записи.
        * Чтобы получить имя контейнера, сделайте вот что: найдите учетную запись хранения, щелкните **BLOB-объекты** и выберите имя контейнера, в который необходимо отправить содержимое. 

    Ниже приведен снимок экрана **диспетчера подключений** в клиенте Aspera, в окне которого необходимо указать тип и учетные данные хранилища Azure, а также контейнер BLOB-объектов.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Ресурсы

В данной статье упоминались следующие ресурсы: 

* [подключаемый модуль Aspera Connect](http://downloads.asperasoft.com/connect2/);
* [справочная документация по Aspera Connect](http://downloads.asperasoft.com/en/documentation/8);
* [клиент Aspera](http://downloads.asperasoft.com/en/downloads/2);
* [справочная документация по клиенту Aspera](http://downloads.asperasoft.com/en/documentation/2).

## <a name="next-steps"></a>Дальнейшие действия

Теперь вы можете [копировать большие двоичные объекты из учетной записи хранения в учетную запись AMS](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account).

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

