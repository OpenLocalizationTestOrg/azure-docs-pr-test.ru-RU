---
title: "aaaConfigure hello кодировщика toosend NewTek TriCaster односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello Tricaster live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования."
services: media-services
documentationcenter: 
author: cenkdin
manager: cfowler
editor: 
ms.assetid: 8973181a-3059-471a-a6bb-ccda7d3ff297
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkd;anilmur
ms.openlocfilehash: 57dcf62a6a76b04e69f147a738be78ccb3c3ecdc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-newtek-tricaster-encoder-toosend-a-single-bitrate-live-stream"></a>Использовать hello кодировщика NewTek TriCaster toosend односкоростного динамического потока
> [!div class="op_single_selector"]
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

В этом разделе показано, как tooconfigure hello [NewTek TriCaster](http://newtek.com/products/tricaster-40.html) live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования. Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).

В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE). Это средство запускается только на компьютерах с ОС Windows. Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).

> [!NOTE]
> При использовании Tricaster для отправки в публикацию веб-канала tooAMS каналы, которые включены для динамического кодирования, может существовать сбоев аудио/видео в передачи интерактивного события при использовании некоторых возможностей Tricaster, такие как быстрая вырезания между потоками или переключения от портативные ПК . работа команды Hello AMS о решении этих проблем, до тех пор, рекомендуется не toouse эти функции.
>
>

## <a name="prerequisites"></a>Предварительные требования
* [Создайте учетную запись служб мультимедиа Azure](media-services-portal-create-account.md).
* Убедитесь, что запущена конечная точка потоковой передачи. Дополнительные сведения см. в статье об [управлении конечными точками потоковой передачи с помощью учетной записи служб мультимедиа](media-services-portal-manage-streaming-endpoints.md).
* Установите последнюю версию hello hello [AMSE](https://github.com/Azure/Azure-Media-Services-Explorer) средства.
* Запустите средство hello и tooyour AMS учетной записи для подключения.

## <a name="tips"></a>Советы
* По возможности используйте проводное подключение к Интернету.
* Хорошее проверенное правило при определении требований к пропускной способности — toodouble hello, потоковая передача битрейтов. Хотя это не является обязательным, он будет позволяет снизить влияние hello перегрузки сети.
* При использовании программных кодировщиков закройте все ненужные программы.

## <a name="create-a-channel"></a>Создание канала
1. В средстве AMSE hello, перейдите toohello **Live** вкладку и щелкните правой кнопкой мыши в пределах области канала hello. Выберите **Создать канал...** меню "hello".

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster1.png)

2. Укажите имя канала hello поле описания является необязательным. Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTMP**. Остальные параметры можно оставить без изменений.

    Убедитесь, что hello **начала hello новый канал теперь** выбран.

3. Щелкните **Создать канал**.

   ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster2.png)

> [!NOTE]
> Hello канала может занять до toostart 20 минут.
>
>

Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-tricaster-live-encoder.md#configure_tricaster_rtmp).

> [!IMPORTANT]
> Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности. Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_tricaster_rtmp></a>Настройка hello NewTek TriCaster кодировщика
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

### <a name="configuration-steps"></a>Этапы настройки
1. Создайте новый проект **NewTek TriCaster** в зависимости от того, какой входной источник видео используется.
2. Один раз в рамках проекта, найти hello **поток** кнопки и меню hello шестеренки значок Далее tooit tooaccess hello потока конфигурации.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster3.png)
3. Когда открытых hello меню, щелкните **New** под заголовком hello соединения. При появлении запроса для типа соединения hello выберите **Adobe Flash**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster4.png)
4. Нажмите кнопку **ОК**.
5. Профиль FMLE теперь может быть импортирован, щелкнув hello стрелку раскрывающегося списка под **профиль Streaming** и переход слишком**Обзор**.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster5.png)
6. Перейдите toowhere hello настроен FMLE профиль был сохранен.
7. Выберите его и нажмите кнопку **ОК**.

    После загрузки профиля hello продолжить toohello следующий шаг.
8. Получение входной URL-адрес канала hello в порядке tooassign его toohello Tricaster **конечной точки RTMP**.

    Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello. После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.

    При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster6.png)
9. Вставить данные в hello **расположение** под **Flash Server** в рамках проекта Tricaster hello. Также назначить имя потока в hello **идентификатор потока** поля.

    Если профиль FMLE toohello был добавлен поток информации, его можно также импортировать toothis статьи, щелкнув **Импорт параметров**, навигация по toohello сохранить FMLE профиль и щелкнув **ОК**. Hello соответствующие поля Flash Server необходимо заполнить данными hello из FMLE.

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster7.png)
10. По завершении нажмите кнопку **ОК** hello нижней части экрана приветствия. По мере готовности видео- и аудиопотоки входными данными для hello Tricaster начать потоковую передачу tooAMS, щелкнув hello **поток** кнопки.

     ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster11.png)

> [!IMPORTANT]
> Прежде чем нажимать кнопку **поток**, вы **должен** гарантировать готовность канала hello.
> Кроме того, убедитесь, что веб-канала не tooleave hello канала в состоянии готовности без ввода вклад более > 15 минут.
>
>

## <a name="test-playback"></a>Проверка воспроизведения
Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы. Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.  

    ![tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster8.png)

Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.

При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены. См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.  

## <a name="create-a-program"></a>Создание программы
1. После проверки воспроизведения канала создайте программу. В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.  

    ![Tricaster](./media/media-services-tricaster-live-encoder/media-services-tricaster9.png)
2. Имя программы hello и, при необходимости, исправьте hello **размер окна архива** (часы too4 какие значения по умолчанию). Также можно указать место хранения или оставьте значения по умолчанию hello.  
3. Проверьте hello **теперь hello запуска программы** поле.
4. Щелкните **Create Program**(Создать программу).  

    >[!NOTE]
    >Создание программы занимает меньше времени, чем создание канала.
        
5. После запуска программы hello, подтвердите воспроизведения, щелкнув правой кнопкой мыши hello программы, а затем перейдя слишком**программах hello воспроизведения** и выбрав **с помощью Azure Media Player**.  
6. После подтверждения, щелкните правой кнопкой мыши hello программы снова и выберите **скопируйте hello выходной URL-адрес tooClipboard** (или извлечь эту информацию из hello **программы сведения и параметры** параметр меню "hello").

поток Hello теперь является готов toobe, внедренных в проигрывателе или распределенных tooan аудитория live Просмотр.  

## <a name="troubleshooting"></a>Устранение неполадок
См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.

## <a name="next-step"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
