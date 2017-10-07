---
title: "aaaUpload файлы в учетную запись служб мультимедиа Azure с помощью Aspera | Документы Microsoft"
description: "Этот учебник поможет вам выполнить этапы hello передачи файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа, используя hello ** Aspera Server по запросу ** службы в Azure."
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
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>Отправка файлов в учетную запись служб мультимедиа с использованием hello службы Aspera Server по запросу в Azure

## <a name="overview"></a>Обзор

**Aspera** — это программное обеспечение для высокоскоростной передачи файлов. **Aspera Server On Demand** для Azure позволяет быстро отправлять большие файлы непосредственно в хранилище BLOB-объектов Azure и скачивать их из него. Сведения о **Aspera On Demand**, в разделе hello [Aspera облака](http://cloud.asperasoft.com/) сайта. 
  
**Aspera Server по запросу** для Azure можно приобрести из hello [Azure marketplace](https://azure.microsoft.com/en-us/marketplace/). Чтобы toocomplete покупке **Aspera Server по запросу** Azure, войдите в Azure Marketplace со своего Windows Live ID.

Этот учебник поможет вам выполнить этапы hello передачи файлов в учетную запись хранилища, связанный с учетной записью служб мультимедиа, используя hello **Aspera Server по запросу** службы в Azure. 

Можно найти пример, в котором показано, как функционирует toouse Azure со службами мультимедиа и Aspera [здесь](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest).

>[!NOTE]
>Имеется ограничение toohello максимальный размер файла поддерживается для обработки с помощью служб мультимедиа Azure media процессоров (MP). См. в разделе [это](media-services-quotas-and-limitations.md) сведения о hello ограничения размера файла.
>

## <a name="prerequisites"></a>Предварительные требования 

toocomplete этого учебника, необходимо:

* Учетная запись Windows Live ID.
* [Учетная запись Azure](https://azure.microsoft.com). Дополнительные сведения см. в разделе [Бесплатная пробная версия Azure](https://azure.microsoft.com/pricing/free-trial/). 
* [Учетная запись служб мультимедиа Azure](media-services-portal-create-account.md).

## <a name="purchase-aspera-on-demand-for-azure"></a>Покупка службы Aspera On Demand для Azure

После входа в Azure Marketplace, выполните эти шаги toocomplete приобретение Aspera On Demand for Azure.

1. Выполните поисковый запрос Aspera и выберите Server On Demand.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. Просмотрите планы hello подписки и нажмите кнопку «Зарегистрироваться»

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. Заполните hello особенностей сервера для подписки по запросу.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. Щелкните hello **ценовую категорию** и выделите нужный месяц тома панели sub hello. В hello **вопросам планирования** панель, выберите **ОК**. Затем в hello **выберите ценовую категорию** нажмите кнопку **выберите**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. Щелкните **условия** tooview и примите условия hello панели sub hello. Изучив hello условиями, нажмите кнопку **покупки**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. Завершить покупку hello, щелкнув **создать**.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. Hello панель мониторинга Azure будут сообщать, что Подготовка службы hello.  После завершения при подготовке hello новую подписку можно найти путем поиска в ресурсы для hello имя службы hello. Найденной службы hello, дважды щелкните его портала управления службами toolaunch hello.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. Запустите портал управления Aspera hello. После обнаружения новой службой Aspera портал управления access toohello, можно получить, щелкнув службу hello.  Откроется новая панель. Из этой новой панели необходимо tooclick на hello **имя ресурса** новой службы.  В следующий снимок экрана приветствия hello ресурс называется «AsperaTransferDemo». После нажатия кнопки на имя ресурса hello, другой панели, будет запущен. На ней вы увидите кнопку "Управление". Щелкните «Управление» связь toolaunch hello Aspera портала управления hello.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Щелкнув hello управлять ссылку, отобразится страница регистрации toohello, который требуется tooaccess hello службы.

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. На этом этапе должен иметь доступ toohello Aspera портала управления службами, где можно создать ключи доступа, загрузите Aspera клиентов и лицензий, сведения об использовании и Дополнительные сведения о hello API-интерфейсы.

    Hello следующем снимке экрана показано создание доступа hello. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    Hello следующем снимке экрана показано использование hello reporting интерфейсы hello портала. 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>Отправка файлов с помощью Aspera

1. Загрузите и установите программное обеспечение клиента Aspera hello.
    
    * [подключаемый модуль браузера](http://downloads.asperasoft.com/connect2/);
    * [полнофункциональный клиент](http://downloads.asperasoft.com/en/downloads/2).

2. Выполните первую передачу. В порядке toouse hello Aspera клиента tootransfer с hello Aspera служба передачи необходимо toocomplete hello следующее: 

    1. Создайте ключ доступа, с помощью портала Aspera hello.  
    2. Загрузку, установку и Aspera клиентских лицензий hello (программного обеспечения можно найти на портале Aspera hello).  

    >[!NOTE]
    >Прочитайте руководство для клиента Aspera hello сведения о конфигурации.
    
    3. Получить некоторые сведения о вашей учетной записи хранилища, связанный с учетной записью мультимедиа Azure с помощью hello [портал Azure](https://portal.azure.com/). В частности, имя и ключ и имя контейнера больших двоичных объектов хранилища hello toowhich требуется tooplace контента. 

        * сведения о хранилище hello tooget из портала hello: найти вашу учетную запись хранения, щелкайте клавиши доступа hello и копирования hello имя и hello ключ учетной записи.
        * Имя контейнера hello tooget: найти вашей учетной записи хранилища, выберите **большие двоичные объекты**выберите hello имя контейнера hello, tooupload содержимое hello в. 

    Ниже приведен снимок экрана приветствия клиента Aspera hello **диспетчера соединений** где необходимо указать тип хранения «Azure» hello и учетные данные, а также контейнер больших двоичных объектов hello.

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>Ресурсы

следующие ресурсы Hello, упомянутых в этой статье. 

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

