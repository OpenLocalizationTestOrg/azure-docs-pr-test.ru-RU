---
title: "aaaHow toouse пользовательского образа Docker для веб-приложения Azure для Linux | Документы Microsoft"
description: "Как пользовательские Docker toouse изображения для веб-приложения Azure в Linux."
keywords: "служба приложений azure, веб-приложение, docker, контейнер"
services: app-service
documentationcenter: 
author: naziml
manager: erikre
editor: 
ms.assetid: b97bd4e6-dff0-4976-ac20-d5c109a559a8
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/16/2017
ms.author: naziml;wesmc
ms.openlocfilehash: 8853095d0e1067cfea4297bbd23b622fe4a0d4db
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-a-custom-docker-image-for-azure-web-app-on-linux"></a>Применение пользовательского образа Docker для веб-приложения Azure на платформе Linux #

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]


Служба приложений включает предопределенные стеки приложений на платформе Linux с поддержкой определенных версий, включая PHP 7.0 и Node.js 4.5. Службы приложений на платформе Linux использует контейнеры Docker toohost эти готовые стеки приложений. Также можно использовать пользовательские toodeploy образа Docker вашего веб-приложения tooan приложения решения, еще не определен в Azure. Пользовательские образы Docker могут размещаться как в открытых, так и закрытых репозиториях Docker.


## <a name="how-to-set-a-custom-docker-image-for-a-web-app"></a>Практическое руководство. Определение пользовательского образа Docker для веб-приложения
Можно задать hello пользовательского образа Docker для обоих новых и существующих приложений веб-узлов. При создании веб-приложения на платформе Linux в hello [портал Azure](https://portal.azure.com/#create/Microsoft.AppSvcLinux), нажмите кнопку **Настройка контейнера** tooset пользовательского образа Docker:

![Определение пользовательского образа Docker для нового веб-приложения на платформе Linux][1]


## <a name="how-to-use-a-custom-docker-image-from-docker-hub"></a>Практическое руководство. Применение пользовательского образа Docker из Docker Hub ##
toouse пользовательского образа Docker из Docker Hub:

1. В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **контейнера Docker**.

2.  Выберите **Docker Hub** как hello **источник изображения**, либо нажмите кнопку **открытый** или **закрытый** и типа hello **изображения и Имя тега необязательно**, такие как `node:4.5`. Hello **команду запуска** задан автоматически на основе сеть, определенная в файле образа Docker hello, но можно задать собственные команды.  

    ![Настройка образа из открытого репозитория Docker Hub][2]

    Если образ доступен из частного хранилища, необходимо также tooenter hello Docker Hub учетные данные (**пользователя для входа** и **пароль**) для hello частном репозитории Docker Hub.

    ![Настройка образа из закрытого репозитория Docker Hub][3]

3. После настройки контейнера hello установите **Сохранить**.

## <a name="how-toouse-a-docker-image-from-a-private-image-registry"></a>Как toouse Docker изображение из реестра частный образ ##
toouse пользовательского образа Docker из реестра частных образов:

1. В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **контейнера Docker**.

2.  Нажмите кнопку **частного реестра** как hello **источник изображения**. Введите hello **изображения, а имя дополнительного тега**, **URL-адрес сервера** для частного реестра hello, вместе с учетными данными hello (**пользователя для входа** и **пароль** ). Щелкните **Сохранить**.

    ![Настройка образа Docker из закрытого реестра][4]


## <a name="how-to-set-hello-port-used-by-your-docker-image"></a>Как: задать hello порт, используемый образ Docker ##

При использовании настраиваемого образа Docker для веб-приложения можно использовать hello `WEBSITES_PORT` переменной среды в Dockerfile, который добавляется созданный toohello контейнера. Рассмотрим следующий пример файла docker для Ruby приложения hello.

    FROM ruby:2.2.0
    RUN mkdir /app
    WORKDIR /app
    ADD . /app
    RUN bundle install
    CMD bundle exec puma config.ru -p WEBSITES_PORT -e production

В последней строке команды hello можно видно, что переменная WEBSITES_PORT hello передается во время выполнения. Помните, что в командах учитывается регистр.

Ранее с помощью платформы hello `PORT` приложение, мы планирования toodeprecate hello использования этого параметра приложения и перемещение toousing `WEBSITES_PORT` исключительно.

При использовании существующий образ Docker, построенный другим пользователем, может возникнуть необходимость toospecify порт, отличный от порта 80 для приложения hello. tooconfigure Здравствуйте, порт, добавьте параметр `WEBSITES_PORT` со значением hello, как показано ниже:

![Настройка параметра приложения PORT для пользовательского образа Docker][6]

## <a name="how-to-set-hello-startup-time-for-your-docker-image"></a>Как: задать время запуска hello образа Docker ##

По умолчанию если контейнер не запускается до 230 секунд платформы hello перезапуск контейнера. Если в более 230 секунд начинается настраиваемого образа Docker, можно использовать hello `WEBSITES_CONTAINER_START_TIME_LIMIT` параметр приложения hello значение для этого параметра задается в секундах, это позволит сохранить платформы hello запущены, прежде чем его контейнера. значение по умолчанию Hello 230 секунд, и hello максимальное допустимое значение составляет 600 секунд.

## <a name="how-to-unmount-hello-platform-provided-storage"></a>Как: отключить hello, предоставленного платформой хранилища ##

По умолчанию hello платформы, будет подключать постоянное хранилище общей папки toohello `\home\` каталога. Если образ контейнера не требуется постоянное папки, можно отключить подключение, хранилища, установка hello `WEBSITES_ENABLE_APP_SERVICE_STORAGE` приложения задание слишком`false`. По-прежнему будет иметь toothat доступ к хранилищу с сайта scm hello и toohello файлы журнала, созданные платформой hello будут записаны все журналы Docker (если он включен).

## <a name="how-to-switch-back-toousing-a-built-in-image"></a>Как: коммутатора резервное toousing встроенного изображения ##

tooswitch из toousing настраиваемого образа встроенного изображения с помощью:

1. В hello [портал Azure](https://portal.azure.com), найдите веб-приложения в Linux, затем в **параметры** щелкните **службы приложений**.

2. Выберите ваш **стек времени выполнения** toouse для hello встроенного изображения, нажмите кнопку **Сохранить**. 

![Настройка встроенного образа Docker][5]


## <a name="troubleshooting"></a>Устранение неполадок ##

Toostart с настраиваемого образа Docker в случае сбоя приложения, проверьте журналы Docker в каталог LogFiles hello hello. Доступ к этому каталогу можно получить либо на сайте SCM, либо через FTP.
toolog hello `stdout` и `stderr` из контейнера, необходимо tooenable **ведения журнала контейнера Docker** под **журналы диагностики**.

![Включение ведения журнала][8]

![С помощью журналов Docker tooview Kudu][7]

Получить доступ к сайту SCM hello **дополнительные средства** в hello **средства разработки** меню.

## <a name="next-steps"></a>Дальнейшие действия ##

Выполните следующие ссылки tooget работы с веб-приложения на платформе Linux hello.   

* [Введение tooAzure веб-приложения в Linux](./app-service-linux-intro.md)
* [Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux](./app-service-linux-using-nodejs-pm2.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)

Если у вас возникли вопросы или проблемы, вы можете опубликовать их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).


<!--Image references-->
[1]: ./media/app-service-linux-using-custom-docker-image/new-configure-container.png
[2]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-public.png
[3]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-dockerhub-private.png
[4]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-privateregistry.png
[5]: ./media/app-service-linux-using-custom-docker-image/existingapp-configure-builtin.png
[6]: ./media/app-service-linux-using-custom-docker-image/setting-port.png
[7]: ./media/app-service-linux-using-custom-docker-image/kudu-docker-logs.png
[8]: ./media/app-service-linux-using-custom-docker-image/logging.png
