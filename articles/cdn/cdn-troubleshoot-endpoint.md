---
title: "конечные точки Azure CDN aaaTroubleshooting, возвращая состояния 404 | Документы Microsoft"
description: "Устранение неполадок с конечными точками Azure CDN, связанных с кодами ответа 404."
services: cdn
documentationcenter: 
author: zhangmanling
manager: erikre
editor: 
ms.assetid: b588a1eb-ab69-4fc7-ae4d-157c3e46f4a8
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 450bfbd641c869cfd88169a12c4b69819eaa7c26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-cdn-endpoints-returning-404-statuses"></a>Устранение неполадок конечных точек CDN, возвращающих состояние 404
Эта статья поможет вам устранить неполадки с [конечными точками CDN](cdn-create-new-endpoint.md) , возвращающими ошибки 404.

Если вам нужна дополнительная помощь в любой момент в этой статье, можно обратиться в hello экспертов Azure на [hello MSDN Azure и hello переполнения стека форумы](https://azure.microsoft.com/support/forums/). Кроме того, можно зарегистрировать обращение в службу поддержки Azure. Go toohello [сайте поддержки Azure](https://azure.microsoft.com/support/options/) и выберите команду **Get Support**.

## <a name="symptom"></a>Симптом
Вы создали CDN профиль и конечную точку, но очевидно toobe на hello CDN контента.  Пользователи, которые пытаются tooaccess контент через URL-адрес CDN hello получать коды состояния HTTP 404. 

## <a name="cause"></a>Причина:
Возможно несколько причин, включая указанные ниже.

* формат файла Hello не видны toohello CDN
* неправильно Hello конечной точки, причиной hello CDN toolook в неправильном месте hello
* заголовок узла hello из hello CDN отклоняет Hello узла
* Конечная точка Hello не было времени toopropagate на протяжении hello CDN

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок
> [!IMPORTANT]
> После создания конечной точки CDN, он будет недоступен немедленно для использования, сколько потребуется времени для hello toopropagate регистрации через hello CDN.  Для профилей <b>Azure CDN от Akamai</b> распространение обычно завершается в течение одной минуты.  Для профилей <b>Azure CDN от Verizon</b> распространение обычно завершается в течение 90 минут, но в некоторых случаях может занимать больше времени.  Если вы завершите шаги hello в этом документе и вы по-прежнему видите ответов 404, рассмотрите возможность ожидания несколько часов toocheck еще раз, прежде чем открыть запрос в службу поддержки.
> 
> 

### <a name="check-hello-origin-file"></a>Проверьте файл начального приветствия
Во-первых, следует проверить hello мы хотим кэшированного файла hello можно найти в нашем источника и является общедоступным.  Здравствуйте быстрым способом toodo, tooopen браузера в сеансе в закрытый или анонимный и перейдите непосредственно toohello файл.  Просто введите или вставьте hello URL-адрес в поле адреса hello и если, преобразуется в файл hello, ожидаемых в разделе.  В этом примере я toouse файла в учетную запись хранилища Azure, доступны в `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`.  Как видите, успешно проходит тест hello.

![Готово!](./media/cdn-troubleshoot-endpoint/cdn-origin-file.png)

> [!WARNING]
> Пока это hello быстрый и простой способ tooverify файл является общедоступным, некоторые конфигурации сети в вашей организации может предоставить вам hello впечатление, что этот файл является общедоступным, когда, на самом деле только видимым toousers вашей сети) даже если она размещается в Azure).  При наличии внешнем браузере, из которого можно проверить, например мобильного устройства, не подключенной сети организации tooyour или виртуальную машину в Azure, которая будет лучше.
> 
> 

### <a name="check-hello-origin-settings"></a>Проверьте параметры источника hello
Теперь, когда мы проверили hello файлов, доступных в Здравствуйте Интернета, нам необходимо проверить параметры источника.  В hello [портала Azure](https://portal.azure.com)профиля CDN tooyour найдите и щелкните конечную точку hello при устранении неполадок.  В возникающие hello **конечной точки** колонка, щелкните источник hello.  

![Колонка "Конечная точка" с выделенным источником](./media/cdn-troubleshoot-endpoint/cdn-endpoint.png)

Hello **источника** колонке отображается. 

![Колонка "Источник"](./media/cdn-troubleshoot-endpoint/cdn-origin-settings.png)

#### <a name="origin-type-and-hostname"></a>Тип и имя узла источника
Проверьте hello **тип источника** правильно, проверьте hello, и **имя узла источника**.  В нашем примере `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, часть hostname hello hello URL-адрес — `cdndocdemo.blob.core.windows.net`.  Как видно на снимке экрана приветствия, это верно.  Для хранилища Azure, веб-приложения и облачная служба источников hello **имя узла источника** поля является раскрывающийся список, поэтому нам не нужен tooworry о правильность написания.  Однако если вы используете настраиваемый источник, *очень важно* правильно указать имя вашего узла.

#### <a name="http-and-https-ports"></a>Порты HTTP и HTTPS
Hello других toocheck вещь здесь является вашей **HTTP** и **порты HTTPS**.  В большинстве случаев значения 80 и 443 правильны и изменять их не требуется.  Тем не менее если hello исходного сервера прослушивает другой порт, который потребуется toobe, представленный здесь.  Если вы не уверены, взгляните на hello URL-адрес для файла источника.  Hello HTTP и HTTPS спецификации указать в качестве значения по умолчанию hello порты 80 и 443. В моей URL-адрес `https://cdndocdemo.blob.core.windows.net/publicblob/lorem.txt`, порт не указан, поэтому по умолчанию hello 443 принимается и параметры заданы правильно.  

Тем не менее, скажем hello URL-адрес для вашего исходного файла, ранее тестируемую `http://www.contoso.com:8080/file.txt`.  Примечание hello `:8080` конце hello hello hostname сегмента.  Сообщающее hello браузера toouse порт `8080` tooconnect toohello веб-сервером по `www.contoso.com`, поэтому вам понадобится tooenter 8080 в hello **HTTP-порт** поля.  Это важные toonote, что эти параметры портов влияют только на какие hello порта конечной точки использует tooretrieve информацию из источника hello.

> [!NOTE]
> **Azure CDN с Akamai** конечные точки не допускают hello полного диапазона TCP-портов для источников.  Список запрещенных портов источников см. в статье о [разрешенных портах источников Azure CDN от Akamai](https://msdn.microsoft.com/library/mt757337.aspx).  
> 
> 

### <a name="check-hello-endpoint-settings"></a>Проверьте параметры конечной точки hello
Включите hello **конечной точки** колонке щелкните hello **Настройка** кнопки.

![Колонка "Конечная точка" с выделенной кнопкой "Настройка"](./media/cdn-troubleshoot-endpoint/cdn-endpoint-configure-button.png)

Здравствуйте, конечной точки **Настройка** колонке отображается.

![Колонка «Настройка»](./media/cdn-troubleshoot-endpoint/cdn-configure.png)

#### <a name="protocols"></a>Протоколы
Для **протоколы**, убедитесь, что протокол hello, используемые клиентами hello.  Hello же протокол, используемый клиентом hello будет использован один источник tooaccess hello, поэтому очень важно toohave hello источника порты неправильно настроена в предыдущем разделе hello hello.  Hello конечная точка прослушивает только hello по умолчанию порты HTTP и HTTPS (80 и 443), независимо от источника портов hello.

Давайте вернемся tooour гипотетический пример с `http://www.contoso.com:8080/file.txt`.  Как вы помните, компания Contoso указала `8080` как HTTP-порт, однако также предположим, что она указала `44300` как HTTPS-порт.  Если сотрудники компании создали конечную точку с именем `contoso`, то именем узла их конечной точки CDN будет `contoso.azureedge.net`.  Запрос `http://contoso.azureedge.net/file.txt` является HTTP-запроса, чтобы использовать hello конечной точки HTTP на порт 8080 tooretrieve его от начала координат hello.  Безопасный запрос по протоколу HTTPS, `https://contoso.azureedge.net/file.txt`, используется для перевода toouse hello конечной точки HTTPS через порт 44300 при при получении hello файл из исходной hello.

#### <a name="origin-host-header"></a>Заголовок узла источника
Hello **заголовок исходного узла** значение заголовка узла hello отправляется источника toohello с каждым запросом.  В большинстве случаев это должен быть hello же, как hello **имя узла источника** мы проверили ранее.  Неверное значение в этом поле не будут вызывать обычно состояния 404, но является toocause, скорее всего, другие состояния 4xx, в зависимости от того, какой источник hello ожидает.

#### <a name="origin-path"></a>Путь к источнику
Наконец, следует проверить **путь к источнику**.  По умолчанию это пустое поле.  В этом поле следует использовать только в случае, если требуется область hello toonarrow hello размещенных источника ресурсов требуется на hello CDN toomake.  

Например, в конечная точка, мне все ресурсы на мой toobe учетной записи хранения доступно, так что я **исходный путь** пустым.  Это означает, что запрос слишком`https://cdndocdemo.azureedge.net/publicblob/lorem.txt` результатов в соединении из конечная точка слишком`cdndocdemo.core.windows.net` , запрашивает `/publicblob/lorem.txt`.  Аналогичным образом, запрос `https://cdndocdemo.azureedge.net/donotcache/status.png` результатов в запросе конечной точки hello `/donotcache/status.png` от начала координат hello.

Но что делать, если не нужны toouse hello CDN для каждого пути моей исходной конфигурации?  Произнесите I вместо tooexpose hello `publicblob` пути.  Если ввести */publicblob* в моей **исходный путь** поля, что вызовет tooinsert hello конечной точки */publicblob* перед каждым запросом, выполненный toohello источника.  Это означает этот запрос hello для `https://cdndocdemo.azureedge.net/publicblob/lorem.txt` фактически теперь займет часть запроса hello hello URL-адрес, `/publicblob/lorem.txt`и добавления `/publicblob` toohello начало. Это приводит к запросу `/publicblob/publicblob/lorem.txt` от начала координат hello.  Если этот путь не разрешается tooan сам файл, источник hello вернет 404 состояния.  Hello правильный URL-адрес tooretrieve lorem.txt в этом примере будет фактически `https://cdndocdemo.azureedge.net/lorem.txt`.  Обратите внимание, что мы не включать hello */publicblob* , так как часть запроса hello hello URL-адрес указан `/lorem.txt` и добавляет конечную точку hello `/publicblob`, в результате `/publicblob/lorem.txt` передаваемого запроса hello toohello источника .

