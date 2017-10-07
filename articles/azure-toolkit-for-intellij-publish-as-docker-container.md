---
title: "контейнер Docker с помощью aaaPublish hello Azure Toolkit для IntelliJ | Документы Microsoft"
description: "Узнайте, как toopublish tooMicrosoft приложения web Azure в качестве контейнера Docker с помощью hello Azure Toolkit для IntelliJ."
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
ms.openlocfilehash: bee94cb269ea707ae7ad55232e23e915aec48c34
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="publish-a-web-app-as-a-docker-container-by-using-hello-azure-toolkit-for-intellij"></a>Публикация веб-приложения как контейнер Docker с помощью hello Azure Toolkit для IntelliJ

Контейнеры Docker широко используются при развертывании веб-приложений. При использовании контейнеров Docker разработчиков можно объединить все файлы проекта и зависимости в один пакет для развертывания сервера tooa. набор средств Azure для IntelliJ Hello упрощает этот процесс для разработчиков Java, добавив *опубликовать как контейнер Docker* компоненты для развертывания tooMicrosoft Azure. В этой статье описывается toopublish необходимые шаги hello tooAzure вашего приложения как контейнеры Docker.

> [!NOTE]
>
> Дополнительные сведения о Docker доступен на hello [веб-узел Docker].
>

[!INCLUDE [azure-toolkit-for-intellij-prerequisites](../includes/azure-toolkit-for-intellij-prerequisites.md)]

## <a name="publish-your-web-app-tooazure-by-using-a-docker-container"></a>Публикация вашего tooAzure web app с помощью контейнера Docker

> [!NOTE]
> * toopublish веб-приложения необходимо создать артефакт готовым к развертыванию. toolearn. более того, в разделе hello [Дополнительные сведения о создании артефактов](#artifacts) раздела.
>
> * Мастер развертывания hello выполнено хотя бы один раз, большая часть параметров, используемые по умолчанию, при запуске мастера hello.
>

1. Откройте проект веб-приложения в IntelliJ.

2. toostart hello **опубликовать как контейнер Docker** мастер, выполните одно из следующих hello:

   * В hello **проекта** окно инструментов, щелкните правой кнопкой мыши проект, нажмите кнопку **Azure**, а затем нажмите кнопку **опубликовать как контейнер Docker**:

      ![Hello опубликовать как команда контейнера Docker][PUB01]

   * На панели инструментов IntelliJ hello, нажмите кнопку hello **публикации группы** , а затем нажмите **опубликовать как контейнер Docker**:

      ![Hello опубликовать как команда контейнера Docker][PUB02]  
    Hello **развертывания контейнера Docker в Azure** откроется мастер.

   ![Развертывание контейнера Docker в Azure мастер Hello][PUB03]

3. В hello **введите имя образа, выберите путь артефакта hello и проверьте toobe узла Docker используется** окне hello следующие: 

   а. В hello **имя образа Docker** введите уникальное имя для узла Docker. (hello мастер автоматически создает имя, но ее можно изменить). 

   b. Hello **узлов** области отображаются узлы Docker, уже создан. Выполните одно из следующих hello. 
      * Если у вас есть существующий узел Docker, можно развернуть вашей tooit web app.
      * toocreate узел Docker, щелкните зеленый hello "плюс" (**+**).  
       Hello **создать узел Docker** откроется диалоговое окно. 

      ![Мастер развертывания контейнера Docker в Azure][PUB04a]

4. В hello **настроить новую виртуальную машину hello** окна, укажите следующую информацию о вашем узле Docker hello. (hello мастер автоматически создает большую часть информации hello для вас, но вы можете изменить любые из них). 

   а. В hello **имя** введите уникальное имя для узла Docker hello. (Это не так же, как имя образа Docker, указанный ранее hello hello.) 
    
   b. В hello **подписки** введите hello подписки Azure, которая используется для узла. 
      
   c. В hello **область** введите hello географический регион, где находится вашего узла.
      
   d. На hello **ОС и размер** вкладки, hello следующие:      
      * **Системы узла**: Введите hello операционной системы для виртуальной машины hello, содержащий вашего узла. 
      * **Размер**: Введите размер hello виртуальной машины для узла.   
       
   д. На hello **группы ресурсов** выберите одно из следующих hello:      
      * **Новая группа ресурсов.** Создайте группу ресурсов для узла.
      * **Существующая группа ресурсов.** Укажите имеющуюся группу ресурсов из учетной записи Azure. 
       
   f. На hello **сети** выберите одно из следующих hello:      
      * **New virtual network** (Новая виртуальная сеть). Создайте виртуальную сеть для узла.
      * **Existing virtual network** (Имеющаяся виртуальная сеть). Укажите имеющуюся виртуальную сеть из учетной записи Azure. 
       
   ж. На hello **хранения** выберите одно из следующих hello:      
      * **Создать учетную запись хранения.** Создайте учетную запись хранения для узла.
      * **Existing storage account** (Имеющаяся учетная запись хранения). Укажите имеющуюся учетную запись хранения из учетной записи Azure.
       
5. Щелкните **Далее**.  
     Hello **настроить журнал учетные данные и параметры порта** открывается окно.

      ![журнал настройки Hello в учетные данные и окно "Параметры" порт][PUB05]

6. Выберите один из следующих вариантов hello.

      * **Import credentials from Azure Key Vault** (Импортировать учетные данные из Azure Key Vault). Укажите сохраненный ранее набор учетных данных, хранящихся в подписке Azure.

          > [!NOTE]
          > Хранилище ключей Azure, созданная с определенной учетной записи или субъекта-службы автоматически недоступна по другой учетной записи или субъекта-службы, использующего hello подписки. в хранилище другой учетной записи или служба ключ субъекта toouse hello tooallow, необходимо использовать учетную запись Azure портала tooadd hello hello или участника-службы.

      * **New log in credentials** (Новые учетные данные для входа). Создайте набор учетных данных для входа в систему. Если этот флажок установлен, hello следующие:

        а. На hello **учетные данные для виртуальной Машины** укажите следующую информацию для hello виртуальной машины учетных данных для узла Docker hello: * **Username**: Введите hello пользователя для имени входа виртуальной машины учетные данные.
             * **Пароль** и **Подтверждение**: hello пароль для учетных данных входа в систему виртуальной машины.
             * **SSH**: Введите параметры hello Secure Shell (SSH) для узла Docker. Можно выбрать один из следующих вариантов hello: * **нет**: Указывает, что виртуальная машина не разрешают соединений по протоколу SSH.
                * **Автоматическое создание**: автоматически создает hello необходимые параметры для подключения по протоколу SSH.
                * **Импорт из каталога**: позволяет toospecify каталог, содержащий набор ранее сохраненные параметры SSH. Hello каталог должен содержать hello, следующие два файла:
                
                  * *id_rsa*: Contains hello RSA identification for a user.
                  * *id_rsa.pub*: Contains hello RSA public key that is used for authentication.
            
        b. На hello **доступа управляющей программы Docker** укажите hello следующую информацию:

          ![Окно Create Docker Host (Создание узла Docker)][PUB06]
    
             * **Docker Daemon port**: Enter hello unique TCP port for your Docker host.
             * **TLS Security**: Enter hello Transport Layer Security settings for your Docker host. You can choose from hello following options:
                * **None**: Specifies that your virtual machine does not allow TLS connections.
                * **Auto-generate**: Automatically creates hello requisite settings for connecting via TLS.
                * **Import from directory**: Specifies a directory that contains a set of previously saved TLS settings. hello directory must contain hello following six files: 
                   * *ca.pem* and *ca-key.pem*: Contain hello certificate and public key for hello TLS Certificate Authority.
                   * *cert.pem* and *key.pem*: Contain client certificate and public key which will be used for TLS authentication.
                   * *server.pem* and *server-key.pem*: Contain hello client certificate and public key that is used for TLS authentication.

7. После ввода hello необходимые сведения, нажмите кнопку **Готово**.  
    Hello **развертывания контейнера Docker в Azure** снова появится мастер.

   ![Мастер развертывания контейнера Docker в Azure][PUB07]

8. Щелкните **Далее**.  
    Hello **Настройка hello Docker контейнера toobe создан** открывается окно.

   ![Настройка Hello hello контейнера Docker toobe создания окна][PUB08]

9. В hello **Настройка hello Docker контейнера toobe создан** окна, предоставляют hello следующую информацию: 

   а. В hello **имя контейнера Docker** введите уникальное имя для контейнера Docker.

   b. Выберите один из следующих образов Docker hello. 

      * **Predefined Docker image** (Предопределенный образ Docker). Укажите имеющийся образ Docker из Azure. 

        > [!NOTE]
        > Hello список образов Docker в этом поле состоит из нескольких изображений, hello, набор средств Azure был настроен toopatch так, что автоматически развертывается на артефакт. 

      * **Custom Dockerfile** (Пользовательский Dockerfile). Укажите сохраненный ранее Dockerfile на локальном компьютере.

        > [!NOTE]
        > Это еще одна возможность разработчикам, создающим собственные Dockerfile toodeploy. Тем не менее он работает toodevelopers, использующих этот tooensure параметр, правильно ли построено их Dockerfile. Поскольку hello набора средств Azure не проверяет содержимое hello в пользовательских Dockerfile, hello может произойти сбой развертывания Если hello Dockerfile вызывает проблемы. Кроме того поскольку hello набора средств Azure ожидает hello пользовательских Dockerfile toocontain артефакт web app, он предпринимает tooopen HTTP-соединение. Если разработчики публикуют артефакт другого типа, то после развертывания могут возникнуть некритичные ошибки.

   c. В hello **параметры порта** введите уникальную привязку порта TCP hello для контейнера Docker. 

10. После завершения предыдущих шагах hello нажмите **Готово**. 

Hello набора средств Azure начинается развертывание вашей tooAzure приложения web в контейнер Docker. Если вы настроили toobe IntelliJ, развернутых в фоновом режиме hello, **развертывание tooAzure** отображается индикатор хода выполнения. 

![индикатор хода выполнения развертывания Hello][PUB09]

<a name="artifacts"></a>
## <a name="additional-information-about-creating-artifacts"></a>Дополнительные сведения о создании артефактов

toocreate артефакт готовым к развертыванию hello следующие:

1. Откройте проект веб-приложения в IntelliJ.

2. В меню **File** (Файл) выберите **Project Structure** (Структура проекта).

   ![Структура проекта команда Hello][ART01]

3. tooadd на артефакт, щелкните зеленый hello "плюс" (**+**), а затем нажмите кнопку **веб-приложения: архив**.

   ![Команда «Архива: веб-приложения» Hello][ART02]

4. В hello **имя** введите имя для вашей артефакта (не включайте hello *.war* расширения) и нажмите кнопку **ОК**.

   ![поле "имя" Hello артефакта][ART03]

Дополнительные сведения о создании артефактов в IntelliJ см. в разделе [Настройка артефакты] на веб-сайте JetBrains hello.

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

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure] и hello [Java средств для Visual Studio Team Services].

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

[центра разработчиков Java Azure]: https://azure.microsoft.com/develop/java/
[Java средств для Visual Studio Team Services]: https://java.visualstudio.com/ (Инструменты Java для Visual Studio Team Services)

[веб-узел Docker]: https://www.docker.com/
[Настройка артефакты]: https://www.jetbrains.com/help/idea/2016.1/configuring-artifacts.html (Настройка артефактов)

<!-- IMG List -->

[PUB01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB01.png
[PUB02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB02.png
[PUB03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB03.png
[PUB04a]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04a.png
[PUB04b]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04b.png
[PUB04c]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04c.png
[PUB04d]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB04d.png
[PUB05]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB05.png
[PUB06]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB06.png
[PUB07]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB07.png
[PUB08]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB08.png
[PUB09]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/PUB09.png

[ART01]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART01.png
[ART02]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART02.png
[ART03]: ./media/azure-toolkit-for-intellij-publish-as-docker-container/ART03.png
