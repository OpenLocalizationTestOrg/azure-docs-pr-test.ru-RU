---
title: "руководство по aaaTroubleshooting для динамической потоковой передачи | Документы Microsoft"
description: "В этом разделе приводятся рекомендации, в том, как tootroubleshoot live проблемы потоковой передачи."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: 3a7f6c1d-ce57-4fa4-a7a6-edb526b3ffbf
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: juliako
ms.openlocfilehash: 8549bae947ff3b225ce624220d1e48b63f90208c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-for-live-streaming"></a>Руководство по устранению неполадок потоковой передачи в реальном времени
В этом разделе приводятся рекомендации о том, как tootroubleshoot некоторые динамической потоковой передачи проблем.

## <a name="issues-related-tooon-premises-encoders"></a>Проблемы, связанные с локальной tooon кодировщики
В этом разделе рассматриваются рекомендации по настройке toosend tootroubleshoot проблем связанных tooon локальных кодировщиков, которые являются каналы tooAMS односкоростной поток, которые включены для динамического кодирования.

### <a name="problem-would-like-toosee-logs"></a>Проблема: Хотел toosee журналы
* **Потенциальная проблема**. Не удается найти журналы кодировщика, которые могут помочь в отладке.
  
  * **Telestream Wirecast**. Обычно журналы можно найти в папке C:\Users\{имя_пользователя}\AppData\Roaming\Wirecast\. 
  * **Элементарных Live**: можно найти, содержит toologs ссылки на портал управления hello. Щелкните **Статистика**, а затем **Журналы**. На hello **файлы журналов** страницы, вы увидите список журналов для всех hello LiveEvent элементы, выбрать hello подходящих текущего сеанса. 
  * **Flash Media Live Encoder**: можно найти hello **каталог журналов...**  , перейдя по toohello **кодирование журнала** вкладки.

### <a name="problem-there-is-no-option-for-outputting-a-progressive-stream"></a>Проблема. Невозможно вывести поток с прогрессивной разверткой
* **Потенциальная проблема**: используется кодировщик hello не объединения полей автоматически. 
  
    **Действия по устранению неполадок**: поиск чередование параметра в интерфейсе кодировщика hello. После включения устранения чересстрочной развертки еще раз проверьте настройки вывода потока с прогрессивной разверткой. 

### <a name="problem-tried-several-encoder-output-settings-and-still-unable-tooconnect"></a>Проблема: Попытка несколько выходные параметры кодировщика и по-прежнему не удается tooconnect.
* **Потенциальная причина**. Канал службы кодирования Azure не был сброшен должным образом. 
  
    **Действия по устранению неполадок**: Убедитесь, что кодировщик hello больше не внедряет tooAMS, остановите и сброс hello канала. После повторного запуска попытайтесь подключиться к нему кодировщик hello новыми параметрами. Если это по-прежнему не устраняет проблему hello, попробуйте создать полностью новый канал, иногда каналов может быть поврежден, после нескольких неудачных попыток.  
* **Потенциальная проблема**: hello GOP размер или параметры кадра не являются оптимальными. 
  
    **Шаги по устранению неполадок**. Рекомендуемое значение размера GOP или интервала опорного кадра — 2 секунды. В некоторых кодировщиках этот параметр задается в количестве кадров, в других — в количестве секунд. Например: при выводе 30 кадров/с, hello размер GOP бы 60 кадров это эквивалент too2 секунд.  
* **Потенциальная проблема**: закрытый порты блокируют поток hello. 
  
    **Действия по устранению неполадок**: во время потоковой передачи через RTMP, проверьте брандмауэр и/или tooconfirm параметры прокси-сервера, что 1935 и 1936 исходящие порты открыты. При потоковой передаче через RTP убедитесь, что открыт исходящий порт 2010. 

### <a name="problem-when-configuring-hello-encoder-toostream-with-hello-rtp-protocol-there-is-no-place-tooenter-a-host-name"></a>Проблема: При настройке toostream кодировщика hello с hello протокола RTP, нет места нет tooenter имя узла.
* **Потенциальная проблема**: многие RTP кодировщиков не допускают имена узлов и IP-адрес, потребуется получить toobe.  
  
    **Действия по устранению неполадок**: toofind Здравствуйте IP-адрес, откройте командную строку на любом компьютере. toodo это в Windows, откройте hello запуска выполнения (WIN + R) и введите «cmd» tooopen.  
  
    После открытия hello командной строке введите «Ping [имя ведущего AMS]». 
  
    Имя узла Hello могут быть производными, не указывайте номер порта hello hello Azure URL-адрес приема, как видно из hello в следующем примере: 
  
    rtp://test2-amstest009.rtp.channel.mediaservices.windows.net:2010/ 
  
    ![fmle](./media/media-services-fmle-live-encoder/media-services-fmle10.png)

> [!NOTE]
> Если после выполнения действия по устранению неполадок hello, вы по-прежнему не удается направить поток успешно, отправьте запрос на поддержку с помощью портала Azure hello.
> 
> 

## <a name="media-services-learning-paths"></a>Схемы обучения работе со службами мультимедиа
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

