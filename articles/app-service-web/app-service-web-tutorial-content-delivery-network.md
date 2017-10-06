---
title: "aaaAdd tooan CDN службе приложений Azure | Документы Microsoft"
description: "Добавьте toocache службе приложений Azure tooan сети доставки содержимого (CDN) и подготовить статические файлы с серверов закрыть tooyour клиентам по всему Здравствуй, мир."
services: app-service\web
author: syntaxc4
ms.author: cfowler
ms.date: 05/31/2017
ms.topic: tutorial
ms.service: app-service-web
manager: erikre
ms.workload: web
ms.custom: mvc
ms.openlocfilehash: 88b7fd884517279064472b804a6d1dc2921cbd24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-content-delivery-network-cdn-tooan-azure-app-service"></a>Добавление сети доставки содержимого (CDN) tooan службы приложений Azure

[Azure сеть доставки содержимого (CDN)](../cdn/cdn-overview.md) кэширует статического веб-содержимого в стратегически расположенных пунктах tooprovide максимальную пропускную способность для доставки содержимого toousers. Hello CDN также уменьшает нагрузку на сервер на веб-приложения. В этом учебнике показано как Azure CDN tooa tooadd [веб-приложения в службе приложений Azure](app-service-web-overview.md). 

Вот hello Домашняя страница hello образец статических HTML узла, который вы будете работать с:

![Домашняя страница примера приложения](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page.png)

Из этого руководства вы узнаете, как выполнять такие задачи:

> [!div class="checklist"]
> * создание конечной точки CDN;
> * обновление кэшированных ресурсов;
> * Использовать запрос строк в кэше toocontrol версии.
> * Используйте настраиваемый домен для конечной точки CDN hello.

## <a name="prerequisites"></a>Предварительные требования

toocomplete этого учебника:

- [установите Git](https://git-scm.com/);
- [Установите Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli).

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-hello-web-app"></a>Создать веб-приложение hello

toocreate hello веб-приложение, вы будете работать с hello выполните [статических HTML краткое руководство](app-service-web-get-started-html.md) через hello **toohello приложения обзора** шаг.

### <a name="have-a-custom-domain-ready"></a>Подготовка личного домена

шаг настраиваемого домена hello toocomplete этого учебника требуется tooown пользовательского домена и иметь доступ tooyour DNS реестра для поставщика домена (например, GoDaddy). Например, tooadd DNS-записей для `contoso.com` и `www.contoso.com`, должен иметь параметры доступа tooconfigure hello DNS для hello `contoso.com` корневого домена.

Если у вас еще нет имени домена, попробуйте выполнить hello [учебника домена службы приложений](custom-dns-web-site-buydomains-web-app.md) toopurchase домена с помощью hello портал Azure. 

## <a name="log-in-toohello-azure-portal"></a>Войдите в toohello портал Azure

Откройте браузер и перейдите toohello [портал Azure](https://portal.azure.com).

## <a name="create-a-cdn-profile-and-endpoint"></a>Создание профиля CDN и конечной точки

В hello навигации слева, выберите **службы приложений**и выберите приложение hello, созданную в hello [статических HTML краткое руководство](app-service-web-get-started-html.md).

![Выберите приложение служб приложений портала hello](media/app-service-web-tutorial-content-delivery-network/portal-select-app-services.png)

В hello **службы приложений** страницы в hello **параметры** выберите **сетевые подключения > Настройка Azure CDN для вашего приложения**.

![Выберите CDN hello портала](media/app-service-web-tutorial-content-delivery-network/portal-select-cdn.png)

В hello **сети доставки содержимого Azure** укажите hello **новую конечную точку** параметры, как указано в таблице hello.

![Создание профиля и конечной точки на портале hello](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint.png)

| Настройка | Рекомендуемое значение | Описание |
| ------- | --------------- | ----------- |
| **Профиль CDN** | myCDNProfile | Выберите **создать новый** toocreate профиля CDN. Профиль CDN-это набор конечных точек CDN с hello же ценовой категории. |
| **Ценовая категория** | Akamai уровня "Стандартный" | Hello [ценовой категории](../cdn/cdn-overview.md#azure-cdn-features) указывает hello поставщика и новых возможностей. В этом руководстве используется ценовая категория Akamai уровня "Стандартный". |
| **Имя конечной точки CDN** | Любое имя, которое является уникальным в домене azureedge.net hello | Доступ кэшированные ресурсы в домене hello  *\<endpointname >. azureedge.net*.

Нажмите кнопку **Создать**.

Azure создает профиль hello и конечной точки. появляется новая конечная точка Hello в hello **конечные точки** списке hello одной странице, и при его подготовке hello состояние **под управлением**.

![Новая конечная точка в списке](media/app-service-web-tutorial-content-delivery-network/portal-new-endpoint-in-list.png)

### <a name="test-hello-cdn-endpoint"></a>Тест hello конечной точки CDN

Если выбрать ценовую категорию Verizon, распространение конечной точки может занять около 90 минут. В ценовой категории Akamai распространение длится несколько минут.

содержит пример приложения Hello `index.html` файла и *css*, *img*, и *js* папки, содержащие другие статические активы. Hello содержимого, что пути для всех этих файлов являются одинаковыми hello в конечной точке CDN hello. Например, обе следующие URL-адреса hello доступ hello *bootstrap.css* файла в hello *css* папки:

```
http://<appname>.azurewebsites.net/css/bootstrap.css
```

```
http://<endpointname>.azureedge.net/css/bootstrap.css
```

Найдите toohello браузера, URL-адреса:

```
http://<endpointname>.azureedge.net/index.html
```

![Домашняя страница примера приложения, которая передается из CDN](media/app-service-web-tutorial-content-delivery-network/sample-app-home-page-cdn.png)

 Вы увидите hello же страницу, что вы выполняли ранее в Azure веб-приложение. Azure CDN извлеченные активы hello источника веб-приложения и обслуживает их из конечной точки CDN hello

tooensure, что эта страница кэшируется в hello CDN, обновите страницу приветствия. Два запросах hello одного средства необходимы иногда для hello CDN toocache hello запрошенного содержимого.

Дополнительные сведения о создании профилей и конечных точек Azure CDN см. в статье [Начало работы с Azure CDN](../cdn/cdn-create-new-endpoint.md).

## <a name="purge-hello-cdn"></a>Очистка hello CDN

Hello CDN периодически обновляет его ресурсы из hello источника веб-приложения на основе hello срока жизни (TTL) конфигурации. TTL по умолчанию Hello составляет семь дней.

В некоторых случаях может потребоваться toorefresh hello CDN перед hello TTL истечение срока действия — например, при развертывании обновленного toohello содержимого веб-приложения. tootrigger обновления можно вручную очистить ресурсы CDN hello. 

В этом разделе учебника hello развертывание веб-приложения toohello изменений и очистка hello CDN tootrigger hello CDN toorefresh свой кэш.

### <a name="deploy-a-change-toohello-web-app"></a>Развертывание изменений toohello веб-приложения

Откройте hello `index.html` и добавьте «-V2 «заголовок toohello H1, как показано в следующий пример hello: 

```
<h1>Azure App Service - Sample Static HTML Site - V2</h1>
```

Зафиксировать внесенные изменения и развернуть ее toohello веб-приложения.

```bash
git commit -am "version 2"
git push azure master
```

После завершения развертывания обзора toohello URL-адрес приложения отобразится изменить hello.

```
http://<appname>.azurewebsites.net/index.html
```

![Элемент "V2" в заголовке веб-приложения](media/app-service-web-tutorial-content-delivery-network/v2-in-web-app-title.png)

Обзор toohello конечной точки CDN URL-адрес для домашней страницы приветствия и вы не видите hello изменить, так как кэшированная версия hello в hello CDN еще не истек. 

```
http://<endpointname>.azureedge.net/index.html
```

![В заголовке в CDN нет элемента "V2"](media/app-service-web-tutorial-content-delivery-network/no-v2-in-cdn-title.png)

### <a name="purge-hello-cdn-in-hello-portal"></a>Очистка hello CDN hello портала

tootrigger hello его кэшированная версия CDN tooupdate, удалите hello CDN.

Hello портала левой навигационной панели, выберите **групп ресурсов**, а затем выберите группу ресурсов hello, созданный для веб-приложения (myResourceGroup).

![Выбор группы ресурсов](media/app-service-web-tutorial-content-delivery-network/portal-select-group.png)

Выберите конечную точку CDN hello списка ресурсов.

![Выбор конечной точки](media/app-service-web-tutorial-content-delivery-network/portal-select-endpoint.png)

Вверху hello hello **конечной точки** щелкните **очистки**.

![Нажатие кнопки "Очистить"](media/app-service-web-tutorial-content-delivery-network/portal-select-purge.png)

Ввод пути к содержимому hello, нужно toopurge. Можно передать toopurge полный путь файла по отдельности или toopurge сегмента пути и обновить все содержимое в папке. Поскольку вы изменили `index.html`, убедитесь, что это один из путей hello.

Hello нижней части страницы приветствия, выберите **очистки**.

![Страница очистки](media/app-service-web-tutorial-content-delivery-network/app-service-web-purge-cdn.png)

### <a name="verify-that-hello-cdn-is-updated"></a>Убедитесь, что hello обновления CDN

Подождите, пока запрос очистку hello завершает обработку, обычно за несколько минут. toosee hello текущее состояние, выберите hello значок колокольчика вверху hello страницы приветствия. 

![Уведомление об очистке](media/app-service-web-tutorial-content-delivery-network/portal-purge-notification.png)

Обзор URL-адрес конечной точки CDN toohello для `index.html`, и вы увидите hello V2, что добавлен заголовок toohello на домашней странице приветствия. Это значит, что обновления кэша CDN hello.

```
http://<endpointname>.azureedge.net/index.html
```

!["V2" в заголовке в CDN](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title.png)

Дополнительные сведения см. в статье [Очистка конечной точки сети CDN Azure](../cdn/cdn-purge-endpoint.md). 

## <a name="use-query-strings-tooversion-content"></a>Использование содержимого tooversion строки запроса

Hello Azure CDN предлагает следующие варианты кэширования поведение hello.

* игнорировать строки запросов;
* обходить кэширование для строк запросов;
* кэшировать все уникальные URL-адреса. 

Здравствуйте, сначала из них — по умолчанию hello, то есть только один кэшированная версия актива независимо от hello строки запроса в URL-адрес hello. 

В этом разделе учебника hello изменить hello кэширование toocache поведение каждый уникальный URL-адрес.

### <a name="change-hello-cache-behavior"></a>Изменить поведение кэширования hello

В hello портал Azure **конечной точки CDN** выберите **кэша**.

Выберите **кэшировать каждый уникальный URL-адрес** из hello **режим кэширования строк запросов** раскрывающегося списка.

Щелкните **Сохранить**.

![Выбор режима кэширования строки запроса](media/app-service-web-tutorial-content-delivery-network/portal-select-caching-behavior.png)

### <a name="verify-that-unique-urls-are-cached-separately"></a>Проверка кэширования уникальных URL-адресов по отдельности

В браузере перейдите на домашнюю страницу toohello в конечной точке CDN hello, но включать строки запроса: 

```
http://<endpointname>.azureedge.net/index.html?q=1
```

Hello CDN возвращает hello текущего веб-приложения содержимого, включая «Версии 2» в заголовке hello. 

tooensure, что эта страница кэшируется в hello CDN, обновите страницу приветствия. 

Откройте `index.html` и измените «Версии 2», слишком «V3» и развернуть изменение hello. 

```bash
git commit -am "version 3"
git push azure master
```

В браузере перейдите URL-адрес конечной точки CDN toohello с новой строки запроса, такие как `q=2`. Hello CDN возвращает текущий hello `index.html` и отображает «V3».  Однако после перехода конечной точки CDN toohello с hello `q=1` строка запроса отображается «V2».

```
http://<endpointname>.azureedge.net/index.html?q=2
```

!["V3" в заголовке CDN, строка запроса 2](media/app-service-web-tutorial-content-delivery-network/v3-in-cdn-title-qs2.png)

```
http://<endpointname>.azureedge.net/index.html?q=1
```

!["V2" в заголовке CDN, строка запроса 1](media/app-service-web-tutorial-content-delivery-network/v2-in-cdn-title-qs1.png)

Этот результат показывает, что каждая строка запроса обрабатывается по-разному:

* строка "q=1" использовалась ранее, поэтому возвращается кэшированное содержимое (V2);
* q = 2 является новым, поэтому содержимое приложения web последнюю hello, извлекаются и возвращается (V3).

Дополнительные сведения см. в статье [Управление режимом кэширования Azure CDN с помощью строк запросов](../cdn/cdn-query-string.md).

## <a name="map-a-custom-domain-tooa-cdn-endpoint"></a>Сопоставить конечную точку CDN tooa пользовательского домена

Необходимо сопоставить ваш пользовательский домен tooyour конечной точки CDN, создав запись CNAME. Запись CNAME является функцией DNS, которая сопоставляет исходный домен tooa целевой домен. Например, можно сопоставить `cdn.contoso.com` или `static.contoso.com` слишком`contoso.azureedge.net`.

Если настраиваемый домен отсутствует, попробуйте выполнить hello [учебника домена службы приложений](custom-dns-web-site-buydomains-web-app.md) toopurchase домена с помощью hello портал Azure. 

### <a name="find-hello-hostname-toouse-with-hello-cname"></a>Найти hello toouse имя узла с hello CNAME

В hello портал Azure **конечной точки** убедитесь, что **Обзор** выбран hello оставить навигации и выберите hello **+ пользовательский домен** кнопку вверху hello страницы приветствия.

![Нажатие кнопки добавления личного домена](media/app-service-web-tutorial-content-delivery-network/portal-select-add-domain.png)

В hello **добавить пользовательский домен** страницы, вы видите toouse имя узла hello конечной точки при создании записи CNAME. Имя узла Hello является производным от URL-адрес конечной точки CDN:  **&lt;EndpointName >. azureedge.net**. 

![Страница добавления домена](media/app-service-web-tutorial-content-delivery-network/portal-add-domain.png)

### <a name="configure-hello-cname-with-your-domain-registrar"></a>Настройка hello CNAME с помощью регистратора доменных имен

Перейдите на веб-сайте регистратора домена tooyour и найдите раздел hello создания записей DNS. Это может быть такой раздел, как **Доменное имя**, **DNS** или **Управление сервером доменных имен**.

Найдите раздел hello управления записями CNAME. Могут содержать дополнительные параметры страницы toogo tooan и искать слова hello CNAME, псевдонима или поддомены.

Создайте запись CNAME, которая сопоставляет выбранный вами поддомен (например, **статических** или **cdn**) toohello **имя узла конечной точки** показанный выше в портал hello. 

### <a name="enter-hello-custom-domain-in-azure"></a>Введите пользовательский домен hello в Azure

Вернуть toohello **добавить пользовательский домен** страницы и введите свой домен, включая поддомен hello в диалоговое окно «hello». Например, введите `cdn.contoso.com`.   
   
Azure проверяет наличие записи CNAME hello для hello доменное имя, которое вы ввели. Если правильно hello CNAME, проверяется вашего домена.

Для серверов tooname toopropagate записей CNAME hello на hello Интернет занимает время. Если домен не проверяется сразу, подождите несколько минут и повторите попытку.

### <a name="test-hello-custom-domain"></a>Пользовательский домен hello теста

В браузере перейдите toohello `index.html` текстовый файл с помощью личного домена (например, `cdn.contoso.com/index.html`) tooverify, результат hello Здравствуйте таким же, как при переходе непосредственно слишком`<endpointname>azureedge.net/index.html`.

![Домашняя страница примера приложения по URL-адресу с личным доменом](media/app-service-web-tutorial-content-delivery-network/home-page-custom-domain.png)

Дополнительные сведения см. в разделе [личный домен CDN Azure карты содержимого tooa](../cdn/cdn-map-content-to-custom-domain.md).

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

## <a name="next-steps"></a>Дальнейшие действия

Вы научились выполнять следующие задачи:

> [!div class="checklist"]
> * создание конечной точки CDN;
> * обновление кэшированных ресурсов;
> * Использовать запрос строк в кэше toocontrol версии.
> * Используйте настраиваемый домен для конечной точки CDN hello.

Узнайте, как производительность CDN toooptimize hello следующие статьи:

> [!div class="nextstepaction"]
> [Повышение производительности за счет сжатия файлов в Azure CDN](../cdn/cdn-improve-performance.md)

> [!div class="nextstepaction"]
> [Предварительная загрузка ресурсов на конечной точке CDN Azure](../cdn/cdn-preload-endpoint.md)
