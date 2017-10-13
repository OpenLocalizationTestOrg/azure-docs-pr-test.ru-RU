---
title: "Устранение неполадок со сжатием файлов в Azure CDN | Документация Майкрософт"
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
ms.openlocfilehash: 5ef8a8262eb40aa827161764f03a63d031e43273
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-cdn-file-compression"></a>Устранение неполадок со сжатием файлов CDN
Эта статья поможет вам устранить неполадки со [сжатием файлов CDN](cdn-improve-performance.md).

Если вам потребуется дополнительная помощь по любому из вопросов, рассматриваемых в статье, вы можете обратиться к экспертам по Azure на [форумах MSDN Azure и Stack Overflow](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Перейдите на [веб-сайт поддержки Azure](https://azure.microsoft.com/support/options/) и щелкните **Получить поддержку**.

## <a name="symptom"></a>Симптом
Сжатие для конечной точки включено, но файлы возвращаются без сжатия.

> [!TIP]
> Чтобы проверить, сжаты ли возвращаемые файлы, используйте такой инструмент, как [Fiddler](http://www.telerik.com/fiddler), или [инструменты разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) в браузере.  Проверьте заголовки HTTP-ответа, возвращаемые с кэшированным содержимым CDN.  Если есть заголовок с именем `Content-Encoding` со значением **gzip**, **bzip2** или **deflate**, то содержимое сжато.
> 
> ![Заголовок Content-Encoding](./media/cdn-troubleshoot-compression/cdn-content-header.png)
> 
> 

## <a name="cause"></a>Причина:
Возможно несколько причин, включая указанные ниже.

* Запрошенное содержимое не подходит для сжатия.
* Сжатие не включено для запрошенного типа файла.
* В запросе HTTP не было заголовка, запрашивающего допустимый тип сжатия.

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок
> [!TIP]
> Как и при развертывании новых конечных точек, требуется некоторое время для распространения изменений конфигурации CDN по сети.  Как правило, изменения применяются в течение 90 минут.  Если сжатие для конечной точки CDN задается впервые, следует подождать один-два часа, чтобы настройки сжатия гарантированно распространились на серверы POP. 
> 
> 

### <a name="verify-the-request"></a>Проверка запроса
Сначала следует быстро проверить запрос.  Чтобы просмотреть поступивший запрос, можно использовать [средства разработчика](https://developer.microsoft.com/microsoft-edge/platform/documentation/f12-devtools-guide/) в браузере.

* Запрос должен отправляться по URL-адресу конечной точки ( `<endpointname>.azureedge.net`), а не в источник.
* Запрос должен содержать заголовок **Accept-Encoding** со значением **gzip**, **deflate** или **bzip2**.

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

Перейдите к конечной точке на [портале Azure](https://portal.azure.com) и нажмите кнопку **Настроить** .

* Проверьте, включено ли сжатие.
* Убедитесь в том, что тип MIME для сжимаемого содержимого включен в список сжимаемых форматов.

![Параметры сжатия CDN](./media/cdn-troubleshoot-compression/cdn-compression-settings.png)

### <a name="verify-compression-settings-premium-cdn-profile"></a>Проверка параметров сжатия (профиль CDN уровня "Премиум")
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN уровня "Премиум" от Verizon** .
> 
> 

Перейдите к конечной точке на [портале Azure](https://portal.azure.com) и нажмите кнопку **Управление** .  Откроется дополнительный портал.  Наведите указатель мыши на вкладку **HTTP Large** (Большая платформа HTTP), а затем наведите указатель мыши на всплывающий элемент **Параметры кэша**.  Щелкните **Сжатие**. 

* Проверьте, включено ли сжатие.
* Список **Типы файлов** должен включать разделенный запятыми список типов MIME (без пробелов).
* Убедитесь в том, что тип MIME для сжимаемого содержимого включен в список сжимаемых форматов.

![Параметры сжатия CDN уровня "Премиум"](./media/cdn-troubleshoot-compression/cdn-compression-settings-premium.png)

### <a name="verify-the-content-is-cached"></a>Проверка кэширования содержимого
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").
> 
> 

С помощью средств разработчика в браузере проверьте заголовки ответов, чтобы убедиться в том, что файл кэширован в регионе, где он запрашивается.

* Проверьте заголовок ответа **Server** в формате  **платформа (POP/идентификатор сервера)**, как показано в примере ниже.
* Проверьте заголовок ответа **X-Cache** .  Он должен иметь значение **HIT**.  

![Заголовки ответа CDN](./media/cdn-troubleshoot-compression/cdn-response-headers.png)

### <a name="verify-the-file-meets-the-size-requirements"></a>Проверка соответствия файла требованиям к размеру
> [!NOTE]
> Это действие применимо только для профиля **Azure CDN от Verizon** (уровня "Премиум" или "Стандартный").
> 
> 

Чтобы сжатие файла было возможным, его размер должен удовлетворять таким требованиям:

* более 128 байт;
* менее 1 МБ.

### <a name="check-the-request-at-the-origin-server-for-a-via-header"></a>Проверьте, есть ли в запросе на сервере-источнике заголовок **Via** .
HTTP-заголовок **Via** указывает веб-серверу, что запрос передается через прокси-сервер.  Если запрос содержит заголовок **Via** , веб-серверы Microsoft IIS по умолчанию не сжимают ответы.  Чтобы изменить это поведение, сделайте следующее.

* **IIS 6**: [задайте HcNoCompressionForProxies="FALSE" в свойствах метабазы IIS](https://msdn.microsoft.com/library/ms525390.aspx)
* **IIS 7 и выше**: [присвойте параметрам **noCompressionForHttp10** и **noCompressionForProxies** значение False в конфигурации сервера](http://www.iis.net/configreference/system.webserver/httpcompression).

