---
title: "aaaGetting к работе с Azure CDN | Документы Microsoft"
description: "В этом разделе показано, как tooenable hello Azure доставки содержимого сети (CDN). Hello учебника вы научитесь hello Создание нового профиля CDN и конечной точки."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: 4ca51224-5423-419b-98cf-89860ef516d2
ms.service: cdn
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 0ce9802bfd7b60e70a9a62330f5593fc17ea07d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-azure-cdn"></a>Начало работы с Azure CDN
В этой статье объясняется, как включить Azure CDN, создав новый профиль и конечную точку CDN.

> [!IMPORTANT]
> Введение toohow CDN работает, а также список функций, в разделе hello [Обзор CDN](cdn-overview.md).
> 
> 

## <a name="create-a-new-cdn-profile"></a>Создание нового профиля сети CDN
Профиль сети CDN представляет собой коллекцию конечных точек сети CDN.  Каждый профиль содержит одну или несколько конечных точек сети CDN.  Вы можете toouse несколько профилей tooorganize конечными точками CDN с Интернет-домен, веб-приложения или некоторых других критериев.

> [!NOTE]
> По умолчанию одной подписки Azure является ограниченной tooeight CDN профилей. Каждый профиль CDN является ограниченной tooten конечных точек CDN.
> 
> Цены CDN применяется на уровне профиля CDN hello. Если вы хотите toouse сочетание Azure CDN ценовым категориям, потребуется несколько профилей CDN.
> 
> 

[!INCLUDE [cdn-create-profile](../../includes/cdn-create-profile.md)]

## <a name="create-a-new-cdn-endpoint"></a>Создание новой конечной точки сети CDN
**toocreate новой конечной точки CDN**

1. В hello [портала Azure](https://portal.azure.com), перейдите tooyour профиля CDN.  Может закрепленной его toohello панели мониторинга в предыдущем шаге hello.  Если вы не, можно найти его, нажав кнопку **Обзор**, затем **CDN профилей**, и щелкнув профиля hello планируется tooadd для конечной точки.
   
    Откроется колонка профиля CDN Hello.
   
    ![Профиль сети CDN][cdn-profile-settings]
2. Нажмите кнопку hello **добавить конечную точку** кнопки.
   
    ![Кнопка "Добавить конечную точку"][cdn-new-endpoint-button]
   
    Hello **добавить конечную точку** колонке отображается.
   
    ![Колонка "Добавление конечной точки"][cdn-add-endpoint]
3. Введите **имя** конечной точки сети CDN.  Это имя будет использоваться tooaccess кэшированные ресурсы в домене hello `<endpointname>.azureedge.net`.
4. В hello **тип источника** раскрывающийся список, выберите тип источника.  Выберите **Служба хранилища** для учетной записи хранения Azure, **Облачная служба** для облачной службы Azure, **Веб-приложение** для веб-приложения Azure или **Настраиваемый источник** для любого другого общедоступного источника на веб-сервере (размещенного в Azure или в другом месте).
   
    ![Тип источника CDN](./media/cdn-create-new-endpoint/cdn-origin-type.png)
5. В hello **имя узла источника** раскрывающийся список, выберите или введите ваш исходный домен.  Hello раскрывающемся списке будут перечислены все доступные источники hello типа, указанного на шаге 4.  Если вы выбрали *пользовательский источник* как ваш **тип источника**, вводе hello домен вашей настраиваемого источника.
6. В hello **исходный путь** текста введите hello путь toohello ресурсов, toocache или оставьте пустым tooallow кэша любые ресурсы на hello домена, указанный на шаге 5.
7. В hello **заголовок исходного узла**введите заголовок узла hello требуется hello toosend CDN с каждым запросом, или оставьте по умолчанию hello.
   
   > [!WARNING]
   > Некоторые типы источников, таких как хранилище Azure и веб-приложениям, потребует домена hello узла заголовок toomatch hello происхождения hello. При отсутствии источника, требующий заголовок узла, отличается от домена, следует оставить значение по умолчанию hello.
   > 
   > 
8. Для **протокола** и **порта источника**укажите hello протоколы и порты tooaccess используемые ресурсы в hello начала координат.  Необходимо указать хотя бы один протокол (HTTP или HTTPS).
   
   > [!NOTE]
   > Hello **порта источника** влияет только на какие hello порта конечной точки использует tooretrieve информацию из источника hello.  Hello конечной точки, сам только будет доступен tooend клиентов на hello по умолчанию порты HTTP и HTTPS (80 и 443), независимо от того, hello **порта источника**.  
   > 
   > **Azure CDN с Akamai** конечные точки не допускают hello полного диапазона TCP-портов для источников.  Список запрещенных портов источников см. в статье о [разрешенных портах источников Azure CDN от Akamai](https://msdn.microsoft.com/library/mt757337.aspx).  
   > 
   > Доступ к CDN содержимое с использованием HTTPS имеет hello следующие ограничения:
   > 
   > * Необходимо использовать SSL-сертификат hello, предоставляемые hello CDN. Сертификаты третьих сторон не поддерживаются.
   > * Необходимо использовать домен CDN техники hello (`<endpointname>.azureedge.net`) содержимое tooaccess HTTPS. Поддержка HTTPS недоступна для пользовательских имен домена (CNAME), поскольку hello CDN не поддерживает пользовательские сертификаты в данный момент.
   > 
   > 
9. Нажмите кнопку hello **добавить** toocreate кнопку hello новой конечной точки.
10. После создания конечной точки hello, он отображается в списке конечных точек для профиля hello. представления списка Hello показывает, что tooaccess toouse hello URL-адрес в кэше содержимого, а также hello исходный домен.
    
    ![Конечная точка сети CDN][cdn-endpoint-success]
    
    > [!IMPORTANT]
    > Конечная точка Hello будет недоступен немедленно для использования, сколько потребуется времени для hello toopropagate регистрации через hello CDN.  Для профилей <b>Azure CDN от Akamai</b> распространение обычно занимает не более минуты.  Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.
    > 
    > Пользователям, пытающимся имени домена CDN hello toouse перед hello конфигурацию конечной точки распространения toohello извлекает получит коды ответа HTTP 404.  Если прошло несколько часов с момента создания конечной точки и вы по-прежнему получаете ответы 404, см. статью [Устранение неполадок конечных точек CDN, возвращающих состояние 404](cdn-troubleshoot-endpoint.md).
    > 
    > 

## <a name="see-also"></a>См. также
* [Управление режимом кэширования запросов CDN с использованием строк запроса](cdn-query-string.md)
* [Как tooMap содержимого CDN tooa пользовательского домена](cdn-map-content-to-custom-domain.md)
* [Предварительная загрузка ресурсов на конечной точке CDN Azure](cdn-preload-endpoint.md)
* [Очистка конечной точки сети CDN Azure](cdn-purge-endpoint.md)
* [Troubleshooting CDN endpoints returning 404 statuses (Устранение неполадок конечных точек CDN, возвращающих состояние 404)](cdn-troubleshoot-endpoint.md)

[cdn-profile-settings]: ./media/cdn-create-new-endpoint/cdn-profile-settings.png
[cdn-new-endpoint-button]: ./media/cdn-create-new-endpoint/cdn-new-endpoint-button.png
[cdn-add-endpoint]: ./media/cdn-create-new-endpoint/cdn-add-endpoint.png
[cdn-endpoint-success]: ./media/cdn-create-new-endpoint/cdn-endpoint-success.png
