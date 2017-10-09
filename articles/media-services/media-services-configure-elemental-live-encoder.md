---
title: "aaaConfigure hello toosend кодировщика Live элементарных односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello toosend кодировщика Live элементарных каналы tooAMS односкоростной поток, которые включены для динамического кодирования."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 9c6bf6a9-6273-4fdd-9477-f0e565280b5b
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: cenkd;anilmur;juliako
ms.openlocfilehash: 9a5de6189bfb123768a9da038b8c8db69cf85e91
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-elemental-live-encoder-toosend-a-single-bitrate-live-stream"></a>Использовать toosend кодировщика Live элементарных hello односкоростного динамического потока
> [!div class="op_single_selector"]
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

В этом разделе показано, как tooconfigure hello [элементарных Live](http://www.elementaltechnologies.com/products/elemental-live) toosend кодировщика односкоростной поток tooAMS каналы, которые включены для динамического кодирования.  Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).

В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE). Это средство запускается только на компьютерах с ОС Windows. Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).

## <a name="prerequisites"></a>Предварительные требования
* Необходимо иметь опыт работы с помощью элементарных Live веб-интерфейс toocreate динамической события.
* [Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).
* Убедитесь, что запущена конечная точка потоковой передачи. Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).
* Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.
* Запустите средство hello и tooyour AMS учетной записи для подключения.

## <a name="tips"></a>Советы
* По возможности используйте проводное подключение к Интернету.
* Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов. Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.
* При использовании программных кодировщиков закройте все ненужные программы.

## <a name="elemental-live-with-rtp-ingest"></a>Использование Elemental Live с протоколом RTP
В этом разделе показано, как tooconfigure hello элементарных Live кодировщик, который отправляет односкоростной динамический поток через RTP.  Дополнительные сведения см. в подразделе, посвященному [передаче потока MPEG-TS по протоколу RTP](media-services-manage-live-encoder-enabled-channels.md#channel).

### <a name="create-a-channel"></a>Создание канала

1. В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello. Выберите **Создать канал...** меню "hello".

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental1.png)

2. Укажите имя канала hello поле описания является необязательным. Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTP (MPEG-TS)**. Остальные параметры можно оставить без изменений.

    Убедитесь, что hello **начала hello новый канал теперь** выбран.

3. Щелкните **Создать канал**.

   ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental12.png)

> [!NOTE]
> Hello канала может занять до toostart 20 минут.
>
>

Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-elemental-live-encoder.md#configure_elemental_rtp).

> [!IMPORTANT]
> Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности. Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

### <a id=configure_elemental_rtp></a>Настройка hello элементарных динамического кодировщика
В этот учебник hello используются следующие параметры вывода. Hello оставшейся части этого раздела описываются шаги настройки более подробно.

**Видео:**

* Кодек: H.264
* Профиль: High (уровень 4.0)
* Скорость: 5000 Кбит/с
* Опорный кадр: 2 секунды (60 секунд)
* Частота кадров: 30

**Звук:**

* Кодек: AAC (LC)
* Скорость: 192 Кбит/с
* Частота выборки: 44,1 кГц

#### <a name="configuration-steps"></a>Этапы настройки
1. Перейдите toohello **элементарных Live** веб-интерфейса и настройка hello кодировщика для **UDP/служб Терминалов** потоковой передачи.
2. После создания нового события прокрутите toohello выходные группы и добавить hello **UDP/служб Терминалов** выходной группы.
3. Создайте выходные данные, щелкнув **New Stream** (Новый поток), а затем **Add Output** (Добавить выходные данные).  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental13.png)

   > [!NOTE]
   > Рекомендуется элементарных события hello имеет слишком задать код времени hello повторного подключения кодировщика hello toohelp «Системные часы» в случае сбоя потока hello.
   >
   >
4. Hello выходных данных будет создан, щелкните кнопку **добавить поток**. Теперь можно настроить параметры вывода Hello.
5. Прокрутите вниз toohello «Stream 1», созданную ранее, щелкните hello **видео** слева hello и разверните hello **Дополнительно** разделе "Параметры".

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental4.png)

    Хотя элементарных Live имеет широкий спектр доступных Настройка, hello рекомендуются следующие настройки для начала работы с потоковой передачи tooAMS.

   * Разрешение: 1280 x 720
   * Частота кадров: 30
   * Размер GOP: 60 кадров
   * Режим развертки: прогрессивная
   * Скорость: 5000000 бит/сек (это значение можно изменить в зависимости от ограничений сети)

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental5.png)

1. Получение входной URL-адрес канала hello.

    Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello. После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.

    При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental6.png)
2. Вставить данные в hello **основной целевой** поле hello кодировщики Elemental. Другие параметры могут оставаться по умолчанию hello.

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental14.png)

    Для дополнительных избыточности повторите эти действия в hello URL-адрес получателя входные данные путем создания отдельной вкладке «Выход» для потоковой передачи UDP/служб Терминалов.
3. Нажмите кнопку **создать** (если он был создан новое событие) или **обновление** (если изменяете существующие события) и затем продолжить toostart hello кодировщика.

> [!IMPORTANT]
> Прежде чем нажимать кнопку **запустить** на hello элементарных Live веб-интерфейса вы **должен** гарантировать готовность канала hello.
> Кроме того, убедитесь, что не tooleave hello канала в состоянии готовности без событие более > 15 минут.
>
>

После выполнения потока hello в течение 30 секунд, перейдите назад toohello AMSE средство и тестирования воспроизведения.  

### <a name="test-playback"></a>Проверка воспроизведения

Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы. Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental8.png)

Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.

При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены. См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.   

### <a name="create-a-program"></a>Создание программы
1. После проверки воспроизведения канала создайте программу. В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.  

    ![Elemental](./media/media-services-elemental-live-encoder/media-services-elemental9.png)
2. Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию). Также можно указать место хранения или оставьте значения по умолчанию hello.  
3. Проверьте hello **теперь hello запуска программы** поле.
4. Щелкните **Create Program**(Создать программу).  

    >[!NOTE]
    > Создание программы занимает меньше времени, чем создание канала.   
      
5. После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.  
6. После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").

поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.  

## <a name="troubleshooting"></a>Устранение неполадок
См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
