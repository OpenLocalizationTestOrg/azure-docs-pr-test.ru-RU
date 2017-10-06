---
title: "aaaConfigure hello toosend кодировщик Telestream Wirecast односкоростного динамического потока | Документы Microsoft"
description: "В этом разделе показано, как tooconfigure hello Wirecast live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования. "
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 0d2f1e81-51a6-4ca9-894a-6dfa51ce4c70
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: ne
ms.topic: article
ms.date: 01/05/2017
ms.author: juliako;cenkdin;anilmur
ms.openlocfilehash: e373f6c08232c652e65db584ded409c405d8cffe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-wirecast-encoder-toosend-a-single-bitrate-live-stream"></a>Используйте hello Wirecast encoder toosend односкоростного динамического потока
> [!div class="op_single_selector"]
> * [Wirecast](media-services-configure-wirecast-live-encoder.md)
> * [Elemental Live](media-services-configure-elemental-live-encoder.md)
> * [Tricaster](media-services-configure-tricaster-live-encoder.md)
> * [FMLE](media-services-configure-fmle-live-encoder.md)
>
>

В этом разделе показано, как tooconfigure hello [Telestream Wirecast](http://www.telestream.net/wirecast/overview.htm) live toosend кодировщика каналы tooAMS односкоростной поток, которые включены для динамического кодирования.  Дополнительные сведения см. в разделе [работа с каналами, что включено tooPerform Live кодирование выполняется с помощью служб мультимедиа Azure](media-services-manage-live-encoder-enabled-channels.md).

В этом учебнике показано, как toomanage служб мультимедиа Azure (AMS) с помощью средства обозревателя служб мультимедиа Azure (AMSE). Это средство запускается только на компьютерах с ОС Windows. Если вы находитесь на Mac или Linux, используйте hello Azure портала toocreate [каналы](media-services-portal-creating-live-encoder-enabled-channel.md#create-a-channel) и [программы](media-services-portal-creating-live-encoder-enabled-channel.md).

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

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast1.png)

2. Укажите имя канала hello поле описания является необязательным. Установите параметры канала **Стандартная** для hello параметр динамического кодирования с hello ввода протокола значение слишком**RTMP**. Остальные параметры можно оставить без изменений.

    Убедитесь, что hello **начала hello новый канал теперь** выбран.

3. Щелкните **Создать канал**.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast2.png)

> [!NOTE]
> Hello канала может занять до toostart 20 минут.
>
>

Во время запуска hello канала можно [Настройка кодировщика hello](media-services-configure-wirecast-live-encoder.md#configure_wirecast_rtmp).

> [!IMPORTANT]
> Обратите внимание, что тарификация начинается сразу же после перехода канала в состояние готовности. Дополнительные сведения см. в разделе о [состояниях каналов](media-services-manage-live-encoder-enabled-channels.md#states).
>
>

## <a id=configure_wirecast_rtmp></a>Настройка hello кодировщик Telestream Wirecast
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
1. Откройте приложение hello Telestream Wirecast на компьютер hello не используется и для потоковой передачи RTMP.
2. Настройка вывода hello, перейдя по toohello **вывода** и выбрать **параметры вывода...** .

    Убедитесь, что hello **места назначения вывода** задано слишком**RTMP-сервер**.
3. Нажмите кнопку **ОК**.
4. На странице "Параметры" hello задайте hello **назначения** toobe поле **служб мультимедиа Azure**.

    Hello кодировка профиль автоматически выбирается слишком**Azure H.264 720 p 16:9 (1280 x 720)**. toocustomize эти параметры, выберите hello toohello значок шестеренки справа от приветствия раскрывающийся список, а затем выберите **новый набор параметров**.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast3.png)
5. Настройка предустановок кодировщика.

    Hello имя конфигурации и для проверки наличия hello следующие рекомендуемые параметры:

    **Видео**

   * Кодировщик: MainConcept H.264
   * Кадров в секунду: 30
   * Средняя скорость: 5000 кбит/сек (это значение можно изменить в зависимости от ограничений сети)
   * Профиль: основной
   * Ключевой кадр: каждые 60 кадров

    **Звук:**

   * Конечная скорость: 192 Кбит/сек
   * Частота выборки: 44,100 кГц

     ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast4.png)
6. Нажмите кнопку **Save**(Сохранить).

    поле Encoding Hello теперь имеет hello только что созданный профиль, доступные для выбора.

    Убедитесь, что выбран новый профиль hello.
7. Получение входной URL-адрес канала hello в порядке tooassign его toohello Wirecast **конечной точки RTMP**.

    Перейдите назад toohello AMSE средство и проверить состояние завершения канала hello. После hello состояние изменилось с **запуск** слишком**под управлением**, вы можете получить hello входной URL-адрес.

    При выполнении hello канала, щелкните правой кнопкой мыши имя канала hello, перемещаться вниз toohover **tooclipboard скопировать URL-адрес входа** , а затем выберите **основной URL-адрес входа**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast6.png)
8. В hello Wirecast **параметры вывода** окна, вставьте эти сведения в hello **адрес** поле из раздела вывода hello и назначьте имя потока.

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast5.png)

1. Нажмите кнопку **ОК**.
2. На главном hello **Wirecast** Подтвердите источников входных данных для видео и аудио готовы и нажмите клавишу **поток** в верхний левый угол hello.

   ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast7.png)

> [!IMPORTANT]
> Прежде чем нажимать кнопку **поток**, вы **должен** гарантировать готовность канала hello.
> Кроме того, убедитесь, что веб-канала не tooleave hello канала в состоянии готовности без ввода вклад более > 15 минут.
>
>

## <a name="test-playback"></a>Проверка воспроизведения

Перейдите toohello AMSE средство, и щелкните правой кнопкой мыши toobe канала hello протестированы. Меню "hello", наведите указатель мыши на **воспроизведения hello предварительного просмотра** и выберите **с помощью Azure Media Player**.  

    ![wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast8.png)

Если поток hello отображается в проигрывателе hello, кодировщик hello был правильно настроен tooconnect tooAMS.

При получении ошибки канала hello потребуется toobe сброса и кодировщик параметры изменены. См. в разделе hello [Устранение неполадок](media-services-troubleshooting-live-streaming.md) разделе рекомендации.  

## <a name="create-a-program"></a>Создание программы
1. После проверки воспроизведения канала создайте программу. В разделе hello **Live** в средство AMSE hello, щелкните правой кнопкой мыши в пределах области программы hello и выберите **создать новую программу**.  

    ![Wirecast](./media/media-services-wirecast-live-encoder/media-services-wirecast9.png)
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

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]
