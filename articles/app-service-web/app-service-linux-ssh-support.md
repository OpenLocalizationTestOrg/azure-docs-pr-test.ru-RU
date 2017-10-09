---
title: "Поддержка aaaSSH Azure приложение службы веб-приложения на платформе Linux | Документы Microsoft"
description: "Сведения об использовании SSH для веб-приложения Azure на платформе Linux."
keywords: "служба приложений azure, веб-приложение, linux, oss"
services: app-service
documentationcenter: 
author: wesmc7777
manager: erikre
editor: 
ms.assetid: 66f9988f-8ffa-414a-9137-3a9b15a5573c
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/25/2017
ms.author: wesmc
ms.openlocfilehash: e00be6d4631e8936a2a8bc106da1fc06237a4b39
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="ssh-support-for-azure-web-app-on-linux"></a>Поддержка SSH для веб-приложения Azure на платформе Linux

[!INCLUDE [app-service-linux-preview](../../includes/app-service-linux-preview.md)]

## <a name="overview"></a>Обзор

[Secure Shell (SSH)](https://en.wikipedia.org/wiki/Secure_Shell) —это сетевой протокол шифрования, предназначенный для безопасного использования сетевых служб. Это наиболее часто используемые toolog в систему удаленно безопасно из командной строки и выполнение административных команд удаленно.

Веб-приложения на платформе Linux обеспечивает поддержку SSH в контейнер приложения hello с каждым hello встроенных Docker изображения для hello стека выполнения новых веб-приложений. 

![Стеки времени выполнения](./media/app-service-linux-ssh-support/app-service-linux-runtime-stack.png)

Можно также использовать SSH с пользовательских образов Docker, включая сервера SSH hello как часть изображения hello и его настройки, как описано в этом разделе.



## <a name="making-a-client-connection"></a>Создание подключения клиента

toomake подключение клиента SSH hello основного сайта должна быть запущена. 

Конечная точка управления элемента управления источника (SCM) hello веб-приложения, вставьте в адресную строку браузера, используя hello следующие формы:

        https://<your sitename>.scm.azurewebsites.net/webssh/host

Если вы не прошли проверку подлинности, не требуется tooauthenticate с tooconnect вашей подписки Azure.

![SSL-подключение](./media/app-service-linux-ssh-support/app-service-linux-ssh-connection.png)


## <a name="ssh-support-with-custom-docker-images"></a>Поддержка SSH в пользовательских образах Docker

Чтобы сообщение SSH toosupport изображения пользовательских Docker между контейнера hello и клиента hello в hello портал Azure выполните следующие шаги для образа Docker hello. 

Эти действия не отображаются в hello репозитория службы приложений Azure в качестве примера [здесь](https://github.com/Azure-App-Service/node/blob/master/6.9.3/).

1. Включить hello `openssh-server` установки в [ `RUN` инструкция](https://docs.docker.com/engine/reference/builder/#run) в hello Dockerfile для изображения и hello пароля для учетной записи root hello слишком`"Docker!"`. 

    > [!NOTE] 
    > Эта конфигурация не позволяет контейнера toohello внешних подключений. SSH может осуществляться только через hello Kudu / SCM сайта, который проходит проверку подлинности с помощью hello учетные данные для публикации.

    ```docker
    # ------------------------
    # SSH Server support
    # ------------------------
    RUN apt-get update \ 
      && apt-get install -y --no-install-recommends openssh-server \
      && echo "root:Docker!" | chpasswd
    ``` 

2. Добавить [ `COPY` инструкция](https://docs.docker.com/engine/reference/builder/#copy) toohello Dockerfile toocopy [sshd_config](http://man.openbsd.org/sshd_config) файл toohello */д/ssh/* каталога. Файл конфигурации должны быть основаны на наш файл sshd_config в репозитории GitHub службе приложений Azure hello [здесь](https://github.com/Azure-App-Service/node/blob/master/6.11/sshd_config).

    > [!NOTE] 
    > Hello *sshd_config* файл должен включать следующие hello или сбой подключения hello: 
    > * `Ciphers`должно содержать по крайней мере одно из следующих hello: `aes128-cbc,3des-cbc,aes256-cbc`.
    > * `MACs`должно содержать по крайней мере одно из следующих hello: `hmac-sha1,hmac-sha1-96`.

    ```docker
    COPY sshd_config /etc/ssh/
    ```


3. Включить порт 2222 в hello [ `EXPOSE` инструкции](https://docs.docker.com/engine/reference/builder/#expose) для hello Dockerfile. Несмотря на то, что известен пароль учетной записи root hello, порт 2222 нельзя получить доступ из hello Интернета. Это внутренняя только порт доступен только по контейнерам внутри сетевого bridge hello частной виртуальной сети.

    ```docker
    EXPOSE 2222 80
    ```

4. Убедитесь, что toostart hello ssh службы. пример Hello [здесь](https://github.com/Azure-App-Service/node/blob/master/6.9.3/startup/init_container.sh) использует сценарий оболочки в */bin* каталога.

    ```bash
    #!/bin/bash
    service ssh start
    ```

    Hello Dockerfile использует hello [ `CMD` инструкция](https://docs.docker.com/engine/reference/builder/#cmd) toorun hello скрипта.

    ```docker
    COPY init_container.sh /bin/
      ...
    RUN chmod 755 /bin/init_container.sh 
      ...       
    CMD ["/bin/init_container.sh"]
    ```



## <a name="next-steps"></a>Дальнейшие действия
См. следующие ссылки для получения дополнительных сведений о веб-приложения на платформе Linux hello. Если у вас возникли вопросы, опубликуйте их на [нашем форуме](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazurewebsitespreview).

* [Как toouse пользовательские Docker изображения для веб-приложения Azure в Linux](app-service-linux-using-custom-docker-image.md)
* [Использование конфигурации PM2 для Node.js в веб-приложении Azure на платформе Linux](app-service-linux-using-nodejs-pm2.md)
* [Использование .NET Core в веб-приложении Azure на платформе Linux](app-service-linux-using-dotnetcore.md)
* [Использование Ruby в веб-приложении Azure на платформе Linux](app-service-linux-ruby-get-started.md)
* [Вопросы и ответы о веб-приложении службы приложений Azure на платформе Linux](app-service-linux-faq.md)

