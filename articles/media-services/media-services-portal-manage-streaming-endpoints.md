---
title: "конечные точки с портала Azure hello потоковой передачи aaaManage | Документы Microsoft"
description: "В этом разделе показано, как toomanage конечных точек потоковой передачи с hello портал Azure."
services: media-services
documentationcenter: 
author: Juliako
writer: juliako
manager: cfowler
editor: 
ms.assetid: bb1aca25-d23a-4520-8c45-44ef3ecd5371
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: dfa9352894d37edb317a6334d7f109419deb362b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-streaming-endpoints-with-hello-azure-portal"></a>Управление конечных точек потоковой передачи с hello портал Azure

В этом разделе показано, как toouse hello Azure портала toomanage конечных точек потоковой передачи. 

>[!NOTE]
>Убедитесь, что hello tooreview [Обзор](media-services-streaming-endpoints-overview.md) раздела. 

Сведения о том, как tooscale hello конечной точки потоковой передачи см. в разделе [это](media-services-portal-scale-streaming-endpoints.md) раздела.

## <a name="start-managing-streaming-endpoints"></a>Как приступить к управлению конечными точками потоковой передачи 

Управление конечных точек потоковой передачи для вашей учетной записи toostart hello следующие.

1. В hello [портал Azure](https://portal.azure.com/), выберите учетную запись служб мультимедиа Azure.
2. В hello **параметры** колонке выберите **конечные точки потоковой передачи**.
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints1.png)

> [!NOTE]
> Плата взимается, только когда конечная точка потоковой передачи используется.

## <a name="adddelete-a-streaming-endpoint"></a>Добавление или удаление конечной точки потоковой передачи

>[!NOTE]
>не удается удалить конечную точку потоковой передачи по умолчанию Hello.

Потоковая передача с помощью конечной точки tooadd или удаления Здравствуйте портал Azure, hello следующие:

1. tooadd конечную точку потоковой передачи, нажмите кнопку hello **+ конечной точки** вверху hello страницы приветствия. 

    Вы можете несколько конечных точек потоковой передачи, если планируется toohave различных CDN или CDN и прямой доступ.

2. Нажмите клавишу toodelete конечной точки потоковой передачи **удалить** кнопки.      
3. Нажмите кнопку hello **запустить** hello toostart кнопку конечной точки потоковой передачи.
   
    ![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints2.png)


## <a id="configure_streaming_endpoints"></a>Настройка конечной точки потоковой передачи hello
Конечная точка потоковой передачи обеспечивает hello tooconfigure следующие свойства:

* управление доступом;
* управление кэшем;
* межсайтовые политики доступа.

Дополнительные сведения об этих свойствах см. [здесь](https://docs.microsoft.com/rest/api/media/operations/streamingendpoint).

Можно настроить конечную точку потоковой передачи, выполнив hello ниже:

1. Выберите hello требуется tooconfigure конечной точки потоковой передачи.
2. Щелкните **Параметры**.

Краткое описание hello поля ниже.

![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints4.png)

1. Политика кэширования: используется tooconfigure время существования кэша для активов, обслуживаемых с помощью этой конечной точки потоковой передачи. Если значение не задано, используется по умолчанию hello. значения по умолчанию Hello также можно создавать непосредственно в хранилище Azure. Для hello конечной точки потоковой передачи включена Azure CDN, не устанавливайте сборки hello кэша политики значение более 600 секунд.  
2. Разрешенные IP-адреса: использовать toospecify IP-адресов, которые допустимы tooconnect toohello публикации конечной точки потоковой передачи. Если IP-адреса не указано, любой IP-адрес будет может tooconnect. Можно указать отдельный IP-адрес (например, 10.0.0.1) или диапазон IP-адресов, используя IP-адрес и маску подсети CIDR (например, 10.0.0.1/22) или IP-адрес и маску подсети с точками (например, 10.0.0.1(255.255.255.0)).
3. Конфигурация для проверки подлинности заголовка подписи Akamai: использовать toospecify, как настроен запрос проверки подлинности заголовка подписи от серверов Akamai. Срок действия указывается в формате UTC.

## <a name="scale-your-premium-streaming-endpoint"></a>Масштабирование конечной точки потоковой передачи уровня "Премиум"

Чтобы узнать больше, ознакомьтесь с [этим](media-services-portal-scale-streaming-endpoints.md) разделом.

## <a id="enable_cdn"></a>Включение интеграции Azure CDN

При создании учетной записи интеграция Azure CDN с конечной точкой потоковой передачи включена по умолчанию.

Если требуется более поздней версии hello toodisable Включение CDN, потоковой передачи конечной точки должны находиться в hello **остановлена** состояния. Через все hello извлекает CDN может занять несколько часов too2 для hello Azure CDN integration tooget включен и toobe изменения hello active. Тем не менее вы можете запустить ваш потоковой передачи конечной точки и потока без прерываний из hello конечной точки потоковой передачи и после завершения интеграции hello поток hello доставляется в от hello CDN. Во время подготовки период hello вашей конечной точки потоковой передачи будет находиться в **запуск** состояния и вы заметите degredad производительности.

Во всех execpt центрах обработки данных Azure hello Китае и областей федеральным Goverment включена интеграция CDN.

После включения hello **управления доступом**, **пользовательского имени узла** и **проверки подлинности подписи Akamai** конфигурация получает отключена.
 
> [!IMPORTANT]
> Для конечных точек потоковой передачи уровня "Стандартный" интеграция служб мультимедиа Azure с Azure CDN реализуется на базе **Azure CDN от Verizon**. Конечные точки потоковой передачи уровня "Премиум" можно настроить, используя все **ценовые категории и поставщики Azure CDN**. Дополнительные сведения о функциях Azure CDN см. в разделе hello [Обзор CDN](../cdn/cdn-overview.md).
 
### <a name="additional-considerations"></a>Дополнительные замечания

* При включении CDN для конечной точки потоковой передачи клиентам не удается запросить содержимое непосредственно из источника hello. Если требуется возможность tootest hello контент с или без CDN, можно создать другой конечной точки потоковой передачи, не включена CDN.
* Ваш потоковой передачи остается имя узла конечной точки hello же после включения CDN. Не нужно toomake любой рабочий процесс изменения tooyour media services после включения CDN. Например если ваш потоковой передачи узла конечной точки, strasbourg.streaming.mediaservices.windows.net, после включения CDN используется hello точно того же имени узла.
* Для новых конечных точек потоковой передачи можно включить CDN просто путем создания новой конечной точки; для существующих конечных точек потоковой передачи необходимо toofirst stop hello endpoint, а затем включить или отключить hello CDN.
* Конечную точку потоковой передачи уровня "Стандартный" можно настроить только с помощью **поставщика CDN уровня "Стандартный" от Verizon** на портале управления Azure. Тем не менее вы можете включить другие поставщики Azure CDN с помощью REST API.

## <a name="configure-cdn-profile"></a>Настройка профиля CDN

Можно настроить профиль CDN hello, выбрав hello **управление CDN** кнопку сверху hello.

![конечной точки потоковой передачи](./media/media-services-portal-manage-streaming-endpoints/media-services-manage-streaming-endpoints6.png)

## <a name="next-steps"></a>Дальнейшие действия
Просмотрите схемы обучения работе со службами мультимедиа.

[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Отзывы
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

