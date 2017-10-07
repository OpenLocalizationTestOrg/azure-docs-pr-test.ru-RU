---
title: "сжатие файлов aaaTroubleshooting в Azure CDN | Документы Microsoft"
description: "Узнайте, как устранить неполадки со сжатием файлов Azure CDN."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: a6624e65-1a77-4486-b473-8d720ce28f8b
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: f00b98beaf6b3b3cd30108ece65a8191edc06ff5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Устранение неполадок со сжатием файлов CDN
Эта статья поможет вам устранить неполадки со [сжатием файлов CDN](cdn-improve-performance.md).

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello MSDN Azure и hello переполнения стека форумы](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайте поддержки Azure](https://azure.microsoft.com/support/options/) и нажмите кнопку **Get Support**.

## <a name="symptom"></a>Симптом
Сжатие для конечной точки включено, но файлы возвращаются без сжатия.

> [!TIP]
> toocheck файлы возвращаются сжатые, необходимость toouse, такие как средство [Fiddler](http://www.telerik.com/fiddler) или обозревателя [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/).  Заголовки ответа hello HTTP проверки возвращаемые CDN кэшированного содержимого.  Если есть заголовок с именем `Content-Encoding` со значением **gzip**, **bzip2** или **deflate**, то содержимое сжато.
> 
> ![Заголовок Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Причина:
Возможно несколько причин, включая указанные ниже.

* Hello указанного содержимого не подходит для сжатия.
* Не включено сжатие для hello запрошенный тип файла.
* Hello HTTP-запроса не включать заголовок, запрашивает тип допустимым сжатия.

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок
> [!TIP]
> Наряду с развертыванием новых конечных точек, CDN изменений конфигурации вступают некоторые toopropagate времени через сеть hello.  Как правило, изменения применяются в течение 90 минут.  Если это hello при первом запуске настройки сжатия для конечной точки CDN, следует ожидания действительно распространения параметров сжатия hello извлекает toohello toobe 1 – 2 часов. 
> 
> 

### <a name="verify-hello-request"></a>Проверьте запрос hello
Во-первых мы должны сделать быстрого проверочной меры по запросу hello.  Можно использовать в браузере [средств разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) tooview hello запросов.

* Проверьте запрос hello отправляется URL-адрес конечной точки tooyour `<endpointname>.azureedge.net`, а не в источник.
* Проверьте запрос hello содержит **Accept-Encoding** содержит заголовок, значение заголовка и hello **gzip**, **deflate**, или **bzip2** .

> [!NOTE]
> Профили **Azure CDN от Akamai** поддерживают только кодирование **GZIP**.
> 
> 

![Заголовки запроса CDN](./media/cdn-troubleshoot-compression/cdn-request-headers.png)

### <a name="verify-compression-settings-standard-cdn-profile"></a>Проверка параметров сжатия (стандартный профиль CDN)
> [!NOTE]
> Это действие применимо только для профилей **Azure CDN уровня "Стандартный" от Verizon** или **Azure CDN уровня "Стандартный" от Akamai**. 
> 
> 

Перейдите tooyour конечной точки в hello [портал Azure](https://portal.azure.com) и нажмите кнопку hello **Настройка** кнопки.

* Проверьте, включено ли сжатие.
* Проверьте hello тип MIME для содержимого, сжатые toobe входит в список hello сжатых форматов hello.

![Параметры сжатия CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Проверка параметров сжатия (профиль CDN уровня "Премиум")
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN уровня "Премиум" от Verizon** .
> 
> 

Перейдите tooyour конечной точки в hello [портал Azure](https://portal.azure.com) и нажмите кнопку hello **управление** кнопки.  Hello дополнительный портал будет открыт.  Наведите указатель мыши hello **HTTP больших** , а затем наведите указатель мыши hello **параметры кэша** всплывающим меню.  Щелкните **Сжатие**. 

* Проверьте, включено ли сжатие.
* Проверьте hello **типы файлов** список содержит список разделенных запятыми (без пробелов) типов MIME.
* Проверьте hello тип MIME для содержимого, сжатые toobe входит в список hello сжатых форматов hello.

![Параметры сжатия CDN уровня "Премиум"](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-hello-content-is-cached"></a>Убедитесь, что кэш содержимого hello
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").
> 
> 

С помощью средств разработчика в браузере, убедитесь, что файл hello tooensure заголовки ответа hello кэшируются в области hello, где он был запрошен.

* Проверьте hello **сервера** заголовок ответа.  Hello заголовок должен иметь формат hello **платформы (POP-сервер ID)**, как показано в следующий пример hello.
* Проверьте hello **X кэша** заголовок ответа.  следует прочитать заголовок Hello **ПОПАДАНИЙ**.  

![Заголовки ответа CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-hello-file-meets-hello-size-requirements"></a>Убедитесь, что файл hello отвечает требованиям к размеру hello
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").
> 
> 

toobe отсрочить сжатие, файл должен соответствовать hello следующие требования к размеру:

* более 128 байт;
* менее 1 МБ.

### <a name="check-hello-request-at-hello-origin-server-for-a-via-header"></a>Проверка запроса hello на исходном сервере hello для **через** заголовок
Hello **через** заголовок HTTP указывает toohello веб-сервера, hello запрос передается через прокси-сервер.  Веб-серверов Microsoft IIS по умолчанию не сжатия ответов, когда запрос hello содержит **через** заголовок.  toooverride такое поведение следующих hello:

* **IIS 6**: [задать HcNoCompressionForProxies = «FALSE» в свойствах hello метабазы IIS](https://msdn.microsoft.com/library/ms525390.aspx)
* **Службы IIS 7 и выше**: [установите **noCompressionForHttp10** и **noCompressionForProxies** tooFalse в конфигурации сервера hello](http://www.iis.net/configreference/system.webserver/httpcompression)

