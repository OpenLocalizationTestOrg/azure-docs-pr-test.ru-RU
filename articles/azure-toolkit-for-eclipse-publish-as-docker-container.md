---
title: "Здравствуйте, aaaPublish контейнер Docker с помощью средств Azure для Eclipse | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: 53ec3a7f7a171691024e03622fd48d6f1e257b50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-eclipse"></a>Публикация веб-приложения как контейнер Docker с помощью hello набора средств Azure для Eclipse

Контейнеры Docker широко используются при развертывании веб-приложений. При использовании контейнеров Docker разработчиков можно объединить все файлы проекта и зависимости в один пакет для развертывания сервера tooa. Hello средств Azure для Eclipse, добавив упрощает этот процесс для разработчиков Java *опубликовать как контейнер Docker* компоненты для развертывания tooMicrosoft Azure. В этой статье описывается toopublish необходимые шаги hello tooAzure вашего приложения как контейнеры Docker.

> [!NOTE]
> Дополнительные сведения о Docker доступен на hello [веб-узел Docker].
>

[!INCLUDE [azure-toolkit-for-eclipse-prerequisites](../includes/azure-toolkit-for-eclipse-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Публикация вашего tooAzure web app с помощью контейнера Docker

1. Откройте проект веб-приложения в Eclipse.

2. toostart hello **опубликовать как контейнер Docker** мастер, выполните одно из следующих hello:

   * В hello **Навигатор** , щелкните правой кнопкой мыши проект, щелкните **Azure**, а затем нажмите кнопку **опубликовать как контейнер Docker**.

      ![Представление навигатора, команда публикации в виде контейнера Docker][PUB01]

   * На панели инструментов Eclipse hello, нажмите кнопку hello **публикации** , а затем нажмите **опубликовать как контейнер Docker**.

      ![Панель инструментов Eclipse, команда публикации в виде контейнера Docker][PUB02]
      
    Hello **развертывания контейнера Docker в Azure** откроется мастер.

    ![Развертывание контейнера Docker в Azure мастер Hello][PUB03]

3. В hello **введите имя образа, выберите путь артефакта hello и проверьте toobe узла Docker используется** окне hello следующие:

    а. В hello **имя образа Docker** введите уникальное имя для узла Docker. (hello мастер автоматически создает имя, но ее можно изменить).

    b. Hello **узлов** области отображаются узлы Docker, уже создан. Выполните одно из следующих hello.

    * Если у вас есть существующий узел Docker, можно развернуть вашей tooit web app.
    * Щелкните новый узел Docker, toocreate **добавить**.  
      
    Hello **создать узел Docker** откроется диалоговое окно.

    ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. В hello **настроить новую виртуальную машину hello** окне укажите следующие параметры для узла Docker hello. (hello мастер автоматически создает большую часть параметров hello, но вы можете изменить любые из них).

   а. **Имя**: Введите уникальное имя для узла Docker hello. (Это не так же, как имя образа Docker, указанный ранее hello hello.)

   b. **Подписки**: Введите hello подписки Azure, которая используется для узла.

   c. **Область**: hello географический регион, где находится на узле, введите.

   d. На hello **узла и размер** вкладки:
     * **Системы узла**: Введите hello операционной системы для виртуальной машины hello, содержащий вашего узла.
     * **Размер**: Введите размер hello виртуальной машины для узла.

   д. На hello **группы ресурсов** вкладки:
     * **Новая группа ресурсов**. Создайте группу ресурсов для узла.
     * **Существующая группа ресурсов**. Укажите имеющуюся группу ресурсов из учетной записи Azure.

   f. На hello **сети** вкладки:
     * **New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.
     * **Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure.

   ж. На hello **хранения** вкладки:
     * **Создать учетную запись хранения**. Создайте учетную запись хранения для узла.
     * **Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.

5. Щелкните **Далее**.

6. В hello **настроить журнал учетные данные и параметры порта** окно, выберите один из следующих вариантов hello:

    * **Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.

      >[!NOTE]
      >Хранилище ключей Azure, созданная с определенной учетной записи или субъекта-службы автоматически недоступна по другой учетной записи или субъекта-службы, использующего hello подписки. tooallow другой учетной записи или служба основной toouse Здравствуйте хранилище ключей, необходимо использовать учетную запись Azure портала tooadd hello hello или участника-службы.

    * **New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему. Если этот флажок установлен, hello следующие:
    
      * На hello **учетные данные для виртуальной Машины** выберите один из следующих hello параметров для учетных данных входа в систему виртуальной машины hello узла Docker:

          * **Имя пользователя**: Введите hello пользователя для учетных данных входа в систему виртуальной машины.
          * **Пароль** и **Подтверждение**: hello пароль для учетных данных входа в систему виртуальной машины.
          * **SSH**: Введите параметры hello Secure Shell (SSH) для узла Docker. Можно выбрать один из следующих вариантов hello:
            * **None** (Нет): указывает, что виртуальная машина не разрешает SSH-подключения.
            * **Автоматическое создание**: автоматически создает hello необходимые параметры для подключения по протоколу SSH.
            * **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров SSH. Hello каталог должен содержать hello, следующие два файла:
                * *id_rsa*: содержит hello идентификации RSA для пользователя.
                * *id_rsa.pub*: содержит открытый ключ RSA hello, который используется для проверки подлинности.
        
        ![Окно Create Docker Host (Создание узла Docker)][PUB05]

      * На hello **учетные данные управляющей программы Docker** укажите hello следующие параметры:

          * **Порт управляющей программы docker**: Введите уникальный порт TCP hello для узла Docker.
          * **Безопасность TLS**: Введите hello параметры безопасности транспортного уровня для узла Docker. Можно выбрать один из следующих вариантов hello:
            * **None** (Нет): указывает, что виртуальная машина не разрешает TLS-подключения.
            * **Автоматическое создание**: автоматически создает hello необходимые параметры для подключения через TLS.
            * **Import from directory** (Импорт из каталога). Позволяет указать каталог, содержащий набор ранее сохраненных параметров TLS. В частности hello каталог должен содержать следующие шесть файлы hello:
                * *CA.pem* и *key.pem ЦС*: содержат hello сертификат и открытый ключ для hello TLS центром сертификации.
                * *CERT.pem* и *key.pem*: содержать hello клиентский сертификат и открытый ключ, используемый для проверки подлинности TLS.
                * *Server.pem* и *key.pem сервера*: содержать hello сертификат и открытый ключ для узла hello.

        ![Окно Create Docker Host (Создание узла Docker)][PUB06]

7. После того как введены все предшествующие сведения hello, нажмите кнопку **Готово**.

8. В hello **развертывания контейнера Docker в Azure** мастера, нажмите кнопку **Далее**.

   ![Развертывание контейнера Docker в Azure мастер Hello][PUB07]

9. В hello **Настройка hello Docker контейнера toobe создан** окне hello следующие:

   а. В hello **имя контейнера Docker** введите уникальное имя для контейнера Docker.

   b. Выберите один из следующих образов Docker hello.
     * **Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure.

       >[!NOTE]
       >Hello список образов Docker в этом поле состоит из нескольких изображений, hello, набор средств Azure был настроен toopatch так, что автоматически развертывается на артефакт.

     * **Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.

       >[!NOTE]
       >Это еще одна возможность разработчикам, создающим собственные Dockerfile toodeploy. Тем не менее он работает toodevelopers, использующих этот tooensure параметр, правильно ли построено их Dockerfile. Hello набора средств Azure не проверяет содержимое hello в пользовательский файл Dockerfile, поэтому hello развертывание может завершиться ошибкой, если hello Dockerfile вызывает проблемы. Кроме того hello набора средств Azure ожидает hello пользовательских Dockerfile toocontain артефакт web app и он попытается tooopen HTTP-соединение. Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.

   c. **Параметры порта**: Введите уникальную привязку порта TCP hello для контейнера Docker.

     ![Настройка Hello hello контейнера Docker toobe создания окна][PUB08]

10. После завершения предыдущих шагах hello щелкните **Готово**.

Hello набора средств Azure начинается развертывание вашей tooAzure приложения web в контейнер Docker. 

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения о hello наборы инструментов Azure для Java интегрированные среды разработки см. следующие ресурсы hello:

* [Набор средств Azure для Eclipse]
  * [Новые возможности средств Azure для Eclipse hello]
  * [Установка средств Azure для Eclipse hello]
  * [Инструкции вход для hello средств Azure для Eclipse]
  * [Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]
* [Набор средств Azure для IntelliJ]
  * [Новые возможности средств Azure для IntelliJ hello]
  * [Установка hello Azure Toolkit для IntelliJ]
  * [Вход инструкции для hello Azure Toolkit для IntelliJ]
  * [Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]

Дополнительные сведения об использовании Azure см. в [центре разработчиков Java для Azure] и на странице [средств Java для Visual Studio Team Services].

Дополнительные ресурсы для Docker см. в разделе официальные hello [веб-узел Docker].

<!-- URL List -->

[Набор средств Azure для Eclipse]: ./azure-toolkit-for-eclipse.md
[Набор средств Azure для IntelliJ]: ./azure-toolkit-for-intellij.md
[Создание веб-приложения Azure (цен. категория "Базовый") с помощью Eclipse]: ./app-service-web/app-service-web-eclipse-create-hello-world-web-app.md
[Создание веб-приложения Azure (цен. категория "Базовый") в IntelliJ]: ./app-service-web/app-service-web-intellij-create-hello-world-web-app.md
[Установка средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-installation.md
[Установка hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-installation.md
[Инструкции вход для hello средств Azure для Eclipse]: ./azure-toolkit-for-eclipse-sign-in-instructions.md
[Вход инструкции для hello Azure Toolkit для IntelliJ]: ./azure-toolkit-for-intellij-sign-in-instructions.md
[Новые возможности средств Azure для Eclipse hello]: ./azure-toolkit-for-eclipse-whats-new.md
[Новые возможности средств Azure для IntelliJ hello]: ./azure-toolkit-for-intellij-whats-new.md

[центре разработчиков Java для Azure]: https://azure.microsoft.com/develop/java/
[средств Java для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[веб-узел Docker]: https://www.docker.com/

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-eclipse-publish-as-docker-container/PUB08.png