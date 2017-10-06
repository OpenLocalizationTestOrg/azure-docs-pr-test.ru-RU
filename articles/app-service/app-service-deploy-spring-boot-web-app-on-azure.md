---
title: "aaaDeploy toohello Spring загрузки приложения службы приложений Azure | Документы Microsoft"
description: "Этот учебник поможет разработчиками с помощью hello действия toodeploy hello Spring начальной загрузки web app tooAzure службы приложений."
services: app-service\web
documentationcenter: java
author: rmcmurray
manager: cfowler
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 08/04/2017
ms.author: asirveda;robmcm
ms.openlocfilehash: 69f9c4903fd740125194402cdb4b4db46a1f2773
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-spring-boot-application-toohello-azure-app-service"></a>Развертывание приложения загрузки Spring toohello службе приложений Azure

Hello  **[Spring Framework]**  — это решение с открытым исходным кодом, которое Java разработчики могут создавать приложения корпоративного уровня, и один из проектов более популярных hello которых построено на основе этой платформы [Загрузки spring], который предоставляет упрощенный подход для создания изолированного приложения Java.

Этот учебник поможет вам хотя Создание hello образец Spring начальной загрузки веб-приложения и развертывание слишком[службе приложений Azure].

### <a name="prerequisites"></a>Предварительные требования

В порядке toocomplete hello шагов в этом учебнике требуется toohave hello следующее:

* Подписка Azure; если у вас еще нет подписки Azure, вы можете активировать [преимущества для подписчиков MSDN] или зарегистрироваться для получения [бесплатной учетной записи Azure].
* Актуальная версия [Java Developer Kit (JDK)].
* Средство сборки [Maven] (версия 3) от Apache.
* Клиент [Git].

## <a name="create-hello-spring-boot-getting-started-web-app"></a>Создать hello Spring начальной загрузки веб-приложение

Hello ниже поможет hello шаги, необходимые toocreate простого Spring загрузки веб-приложения и протестировать на локальном компьютере.

1. Откройте командную строку и создать toohold локальный каталог, приложение и перейдите в каталог toothat; Например:
   ```
   md C:\SpringBoot
   cd C:\SpringBoot
   ```
   -- или --
   ```
   md /users/robert/SpringBoot
   cd /users/robert/SpringBoot
   ```

1. Клон hello [Spring начальной загрузки] образец проекта в каталог hello, только что созданный; например:
   ```
   git clone https://github.com/spring-guides/gs-spring-boot.git
   ```

1. Изменение каталога toohello завершения проекта; Например:
   ```
   cd gs-spring-boot
   cd complete
   ```

1. Построение hello JAR-файл с помощью Maven; Например:
   ```
   mvn package
   ```

1. После создания веб-приложения hello изменить каталог toohello JAR-файл и запустить веб-приложение hello; Например:
   ```
   cd target
   java -jar gs-spring-boot-0.1.0.jar
   ```

1. Тестирование веб-приложения hello, перейдя в веб-браузере toohttp://localhost:8080, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:
   ```
   curl http://localhost:8080
   ```

1. Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**

   ![Обзор образца приложения][SB01]

## <a name="create-an-azure-web-app-for-use-with-java"></a>Создание веб-приложения Azure для использования с Java

Hello следующие шаги пошаговыми руководствами hello действия toocreate веб-приложение Azure, настройте hello необходимые параметры для Java и настроить учетные данные FTP.

1. Обзор toohello [портал Azure] и войдите в систему.

1. После входа в вашу учетную запись на hello портал Azure, щелкните значок меню hello **службы приложений**:
   
   ![Портал Azure][AZ01]

1. Здравствуйте, когда **службы приложений** страница отображается, щелкните **+ добавить** toocreate нового приложения службы.

   ![Создание службы приложений][AZ02]

1. При отображении hello список шаблонов веб-приложение, щелкните ссылку hello для hello основные веб-приложение Microsoft.

   ![Шаблоны веб-приложений][AZ03]

1. Когда откроется страница приветствия сведения для шаблона веб-приложения hello, нажмите кнопку **создать**.

   ![Создание веб-приложения][AZ04]

1. Укажите уникальное имя веб-приложения и задайте дополнительные параметры, после чего нажмите кнопку **Создать**.

   ![Параметры создания веб-приложения][AZ05]

1. После создания веб-приложения, щелкните значок меню hello **службы приложений**и выберите только что созданный веб-приложения:

   ![Список веб-приложений][AZ06]

1. При отображении веб-приложения, укажите hello версии Java с помощью hello следующие шаги:

   а. Нажмите кнопку hello **параметры приложения** элемента меню.

   b. Выберите **Java 8** hello версии Java.

   c. Выберите **Newest** для hello дополнительный номер версии Java.

   d. Выберите **новейшие 8.5 Tomcat** для hello web контейнера. (Этот контейнер не фактически будет использоваться; Azure будет использовать контейнер hello Spring загрузки приложения.)

   д. Щелкните **Сохранить**.

   ![Параметры приложения][AZ07]

1. Укажите учетные данные развертывания FTP, используя hello следующие шаги:

   а. Нажмите кнопку hello **учетные данные развертывания** элемента меню.

   b. Укажите имя пользователя и пароль.

   c. Щелкните **Сохранить**.

   ![Указание учетных данных развертывания][AZ08]

1. Получить сведения о подключении к FTP, с помощью hello следующие шаги:

   а. Нажмите кнопку hello **учетные данные развертывания** элемента меню.

   b. Скопируйте полное имя пользователя FTP и URL-адрес и сохранить их для hello следующей части этого учебника.

   ![URL-адрес и учетные данные FTP][AZ09]

## <a name="deploy-your-spring-boot-web-app-tooazure"></a>Развертывание вашей tooAzure приложения web Spring загрузки

Hello, выполнив действия поможет toodeploy действия hello вашей tooAzure приложения web Spring загрузки.

1. Откройте текстовый редактор, например Блокнот и вставьте следующий текст в новый документ hello, а затем сохраните файл как файл hello *web.config*:
   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <configuration>
     <system.webServer>
       <handlers>
         <add name="httpPlatformHandler" path="*" verb="*" modules="httpPlatformHandler" resourceType="Unspecified" />
       </handlers>
       <httpPlatform processPath="%JAVA_HOME%\bin\java.exe"
           arguments="-Djava.net.preferIPv4Stack=true -Dserver.port=%HTTP_PLATFORM_PORT% -jar &quot;%HOME%\site\wwwroot\gs-spring-boot-0.1.0.jar&quot;">
       </httpPlatform>
     </system.webServer>
   </configuration>
   ```

1. После сохранения hello *web.config* файловая система tooyour, подключите tooyour веб-приложения по протоколу FTP, с помощью hello URL-адрес, имя пользователя и пароль из hello предшествующий разделе этого учебника. Например:
   ```
   ftp
   open waws-prod-sn0-000.ftp.azurewebsites.windows.net
   user wingtiptoys-springboot\wingtiptoysuser
   pass ********
   ```

1. Изменение hello удаленный каталог toohello корневую папку веб-приложения (который находится на */сайт/wwwroot*), затем скопируйте Spring загрузки приложения hello JAR-файл и hello *web.config* из более ранних версий. Например:
   ```
   cd site/wwwroot
   put gs-spring-boot-0.1.0.jar
   put web.config
   ```

1. После развертывания вашего JAR и *web.config* файлы tooyour веб-приложения, необходимо toorestart веб-приложения с помощью портала Azure hello:

   ![][AZ10]

1. Тестирование веб-приложения hello путем просмотра URL-адрес tooyour веб-приложения в веб-браузере, или с помощью синтаксиса hello как следующий пример, при наличии доступных перелистывание hello:
   ```
   curl http://wingtiptoys-springboot.azurewebsites.net/
   ```

1. Должно появиться сообщение, отображаемое после hello: **Greetings с Spring загрузки!**

   ![Обзор образца приложения][SB02]

## <a name="next-steps"></a>Дальнейшие действия

Дополнительные сведения об использовании приложений Spring загрузки в Azure см. следующие статьи hello:

* [Развертывание приложения загрузки Spring в Linux в hello контейнера службы Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-linux.md)

* [Развертывание приложения загрузки Spring в кластере Kubernetes в hello контейнера службы Azure](../container-service/kubernetes/container-service-deploy-spring-boot-app-on-kubernetes.md)

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

Дополнительные сведения о tooAzure приложения web depoying, с помощью протокола FTP см. в разделе [развертывание вашего приложения tooAzure службы приложений с помощью FTP/S].

Дополнительные сведения о проекте образец hello Spring загрузки см. [Spring начальной загрузки].

Справку по Приступая к работе с приложениями Spring загрузки см. в разделе hello **Spring Initializr** на https://start.spring.io/.

Дополнительные сведения о настройке дополнительных параметров для веб-приложения см. в статье [Настройка веб-приложений в службе приложений Azure].

<!-- URL List -->

[службе приложений Azure]: https://azure.microsoft.com/services/app-service/
[Azure Container Service]: https://azure.microsoft.com/services/container-service/
[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[портал Azure]: https://portal.azure.com/
[Настройка веб-приложений в службе приложений Azure]: /azure/app-service-web/web-sites-configure
[развертывание вашего приложения tooAzure службы приложений с помощью FTP/S]: https://docs.microsoft.com/azure/app-service-web/app-service-deploy-ftp
[бесплатной учетной записи Azure]: https://azure.microsoft.com/pricing/free-trial/
[Git]: https://github.com/
[Java Developer Kit (JDK)]: http://www.oracle.com/technetwork/java/javase/downloads/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)
[Maven]: http://maven.apache.org/
[преимущества для подписчиков MSDN]: https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/
[Загрузки spring]: http://projects.spring.io/spring-boot/
[Spring начальной загрузки]: https://github.com/spring-guides/gs-spring-boot
[Spring Framework]: https://spring.io/

<!-- IMG List -->

[SB01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB01.png
[SB02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/SB02.png

[AZ01]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ01.png
[AZ02]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ02.png
[AZ03]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ03.png
[AZ04]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ04.png
[AZ05]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ05.png
[AZ06]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ06.png
[AZ07]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ07.png
[AZ08]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ08.png
[AZ09]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ09.png
[AZ10]: ./media/app-service-deploy-spring-boot-web-app-on-azure/AZ10.png
