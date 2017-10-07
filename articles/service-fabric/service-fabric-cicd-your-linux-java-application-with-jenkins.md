---
title: "aaaContinuous сборки и интеграции для Azure Service Fabric Linux приложение Java с помощью Jenkins | Документы Microsoft"
description: "Непрерывное создание и интеграция приложения Linux на Java с помощью Jenkins"
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: 02b51f11-5d78-4c54-bb68-8e128677783e
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/23/2017
ms.author: saysa
ms.openlocfilehash: 15da2cb8c759233219369ea889550da93748129f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-jenkins-toobuild-and-deploy-your-linux-java-application"></a>Использовать Jenkins toobuild и развертывать приложения Linux Java
Jenkins — это популярное средство для непрерывной интеграции и развертывания приложений. Вот как toobuild и развертывания приложения Azure Service Fabric с помощью Jenkins.

## <a name="general-prerequisites"></a>Общие предварительные требования
- Необходимо иметь локальный репозиторий Git. Можно установить соответствующую версию Git hello из [hello Git загружает страницу](https://git-scm.com/downloads)в зависимости от операционной системы. Если новый tooGit, Дополнительные сведения о нем hello [Git документации](https://git-scm.com/docs).
- Hello Jenkins структуры службы подключаемый модуль иметь под рукой. Его можно скачать [здесь](https://servicefabricdownloads.blob.core.windows.net/jenkins/serviceFabric.hpi).

## <a name="set-up-jenkins-inside-a-service-fabric-cluster"></a>Настройка Jenkins в кластере Service Fabric

Jenkins можно настроить внутри или за пределами кластера Service Fabric. Hello следующие разделы Показать tooset его в кластере при использовании хранилища Azure учетной записи toosave hello состояние экземпляра контейнера hello.

### <a name="prerequisites"></a>Предварительные требования
1. Подготовьте кластер Service Fabric под управлением Linux. Кластер Service Fabric, создаваемых hello портал Azure уже имеет установленным Docker. Если кластер hello выполняются локально, проверьте, установлены ли Docker с помощью команды hello ``docker info``. Если он не установлен, установите его соответствующим образом с помощью hello следующих команд:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```
2. Есть hello Service Fabric контейнера приложение развернуто в кластере hello, с помощью hello следующие шаги:

  ```sh
git clone https://github.com/Azure-Samples/service-fabric-java-getting-started.git
cd service-fabric-java-getting-started/Services/JenkinsDocker/
```

3. Требуется hello подключитесь параметр подробные сведения о hello общей папки хранилища Azure, которой будет toopersist hello состояние экземпляра контейнера Jenkins hello. При использовании hello портал Microsoft Azure для hello одинаковые, пожалуйста выполните действия hello, — создавать учетную запись хранилища Azure, например ``sfjenkinsstorage1``. Затем создайте **общую папку** для этой учетной записи хранения, например ``sfjenkins``. Щелкните **Connect** для общей папки и Примечание hello hello значения отображаются в разделе **подключение из Linux**, скажем должен выглядеть следующим образом —
```sh
sudo mount -t cifs //sfjenkinsstorage1.file.core.windows.net/sfjenkins [mount point] -o vers=3.0,username=sfjenkinsstorage1,password=<storage_key>,dir_mode=0777,file_mode=0777
```

4. Обновить значения заполнителя hello hello ```setupentrypoint.sh``` скрипт с соответствующие сведения о хранилище azure.
```sh
vi JenkinsSF/JenkinsOnSF/Code/setupentrypoint.sh
```
Замените ``[REMOTE_FILE_SHARE_LOCATION]`` со значением hello ``//sfjenkinsstorage1.file.core.windows.net/sfjenkins`` из вывода hello hello соединения в точке 3 выше.
Замените ``[FILE_SHARE_CONNECT_OPTIONS_STRING]`` со значением hello ``vers=3.0,username=sfjenkinsstorage1,password=GB2NPUCQY9LDGeG9Bci5dJV91T6SrA7OxrYBUsFHyueR62viMrC6NIzyQLCKNz0o7pepGfGY+vTa9gxzEtfZHw==,dir_mode=0777,file_mode=0777`` из точки 3 выше.

5. Подключите кластер toohello и установить приложение hello контейнера.
```azurecli
sfctl cluster select --endpoint http://PublicIPorFQDN:19080   # cluster connect command
bash Scripts/install.sh
```
Устанавливает контейнер Jenkins в кластере hello и может отслеживаться с помощью Service Fabric Explorer hello.

### <a name="steps"></a>Действия
1. В браузере перейдите слишком``http://PublicIPorFQDN:8081``. Он предоставляет hello toosign требуется пароль администратора начальной hello в путь. Вы можете продолжить toouse Jenkins как администратор. Или можно создать и изменить пользователя hello после входа с учетной записью администратора начальной hello.

   > [!NOTE]
   > Убедитесь, что порт 8081 hello как порт конечной точки приложения hello при создании кластера hello.
   >

2. Получить идентификатор экземпляра hello контейнера с помощью ``docker ps -a``.
3. Secure Shell (SSH) входа в контейнере toohello и вставьте путь hello, которые были выявлены на портале Jenkins hello. Например, если в портал hello отображает hello путь `PATH_TO_INITIAL_ADMIN_PASSWORD`, hello следующей:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash   # This takes you inside Docker shell
  cat PATH_TO_INITIAL_ADMIN_PASSWORD
  ```

4. Установка toowork GitHub с Jenkins, с помощью действия hello, упомянутые в [Создание нового ключа SSH и его добавления агента SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
    * Используйте инструкции hello, предоставляемых SSH-ключ hello toogenerate GitHub и tooadd hello SSH ключа toohello учетной записи GitHub, на котором размещается репозиторий.
    * Выполните команды hello, упомянутые в hello предшествующий ссылку в hello оболочки Jenkins Docker (и не на узле).
    * toosign в toohello Jenkins оболочки с вашего узла hello используйте следующую команду:

  ```sh
  docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
  ```

## <a name="set-up-jenkins-outside-a-service-fabric-cluster"></a>Настройка Jenkins за пределами кластера Service Fabric

Jenkins можно настроить внутри или за пределами кластера Service Fabric. Здравствуйте, следующие разделы Показать как tooset его вне кластера.

### <a name="prerequisites"></a>Предварительные требования
Необходимо toohave установленным Docker. Привет, следующие команды можно используется tooinstall Docker из hello терминалов:

  ```sh
  sudo apt-get install wget
  wget -qO- https://get.docker.io/ | sh
  ```

Теперь при выполнении ``docker info`` в hello терминалов должны отображаться в выходных данных hello, hello службой Docker.

### <a name="steps"></a>Действия
  1. Образ контейнера hello Jenkins структуры службы по запросу:``docker pull raunakpandya/jenkins:v1``
  2. Выполните hello образ контейнера.``docker run -itd -p 8080:8080 raunakpandya/jenkins:v1``
  3. Получите идентификатор hello hello контейнера изображения экземпляра. Можно перечислить все контейнеры Docker hello командой hello``docker ps –a``
  4. Войти в toohello Jenkins портал, используя hello следующие шаги:

    * ```sh
    docker exec [first-four-digits-of-container-ID] cat /var/jenkins_home/secrets/initialAdminPassword
    ```
    Если идентификатор контейнера имеет значение 2d24a73b5964, используйте 2d24.
    * Этот пароль необходим для входа в панель мониторинга Jenkins toohello из портала, который является``http://<HOST-IP>:8080``
    * После регистрации для hello первый раз, можно создать собственную учетную запись пользователя и использовать его для будущих целей или продолжить учетной записи администратора toouse hello. После создания пользователя необходимо toocontinue со спецификацией.
  5. Установка toowork GitHub с Jenkins, с помощью действия hello, упомянутые в [Создание нового ключа SSH и его добавления агента SSH toohello](https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/).
        * Используйте инструкции hello, предоставляемых SSH-ключ hello toogenerate GitHub и tooadd hello SSH ключа toohello учетной записи GitHub, на котором размещается hello репозитория.
        * Выполните команды hello, упомянутые в hello предшествующий ссылку в hello оболочки Jenkins Docker (и не на узле).
      * toosign в toohello Jenkins оболочки с вашего узла hello используйте следующие команды:

      ```sh
      docker exec -t -i [first-four-digits-of-container-ID] /bin/bash
      ```

Убедитесь, что hello кластера или компьютера, где hello образ контейнера Jenkins размещается имеет общедоступный IP-адрес. Это позволяет hello Jenkins экземпляр tooreceive уведомления с сайта GitHub.

## <a name="install-hello-service-fabric-jenkins-plug-in-from-hello-portal"></a>Установка hello Jenkins структуры службы подключаемого модуля из портала hello

1. Go слишком``http://PublicIPorFQDN:8081``
2. Панель мониторинга Jenkins hello, выберите **управления Jenkins** > **управление подключаемыми модулями** > **Дополнительно**.
Здесь можно загрузить подключаемый модуль. Выберите **выбрать файл**, а затем выберите hello **serviceFabric.hpi** файл, который был загружен в списке необходимых компонентов. При выборе **отправить**, Jenkins автоматически устанавливает hello подключаемого модуля. При необходимости выполните перезагрузку.

## <a name="create-and-configure-a-jenkins-job"></a>Создание и настройка задания Jenkins

1. Создайте **новый элемент** из панели мониторинга.
2. Введите имя элемента, например **MyJob**. Выберите **проект в свободной форме** и нажмите кнопку **ОК**.
3. Переход на страницу приветствия задания и нажмите кнопку **Настройка**.

   а. В разделе Основные hello в разделе **GitHub проекта**, укажите URL-адрес проекта GitHub. Этот URL-адреса узлов hello службы структуры приложения Java, которые должны toointegrate с hello непрерывной интеграции Jenkins, непрерывного развертывания (CI/CD) потока (например, ``https://github.com/sayantancs/SFJenkins``).

   b. В разделе hello **управление исходным кодом** выберите **Git**. Укажите URL-адрес hello репозитория, где размещается приложение Java структуры службы hello, что требуется toointegrate с hello потока Jenkins CI или компакт-диска (например, ``https://github.com/sayantancs/SFJenkins.git``). Кроме того, здесь можно указать, какие ветви toobuild (например, **/образце**).
4. Настройка вашего *GitHub* (который размещение hello репозитория) так, чтобы его могли tootalk tooJenkins. Используйте следующие шаги hello.

   а. Переход на страницу репозитория GitHub tooyour. Go слишком**параметры** > **интеграции и службы**.

   b. Выберите **добавить службу**, тип **Jenkins**и выберите hello **Jenkins GitHub подключаемого модуля**.

   c. Введите URL-адрес webhook для Jenkins (по умолчанию это должен быть ``http://<PublicIPorFQDN>:8081/github-webhook/``). **Добавьте или обновите службу**.

   d. Событие проверки отправляется tooyour Jenkins экземпляра. Вы увидите зеленый флажок с веб-перехватчика hello в GitHub и проект будет построен.

   д. В разделе hello **сборки триггеров** выберите нужный вариант построения. Для этого примера требуется tootrigger сборки каждый раз, когда некоторые принудительной toohello репозитория. поэтому выберите параметр **GitHub hook trigger for GITScm polling** (Обработчик триггера Github для опроса GITScm). (Ранее, этот параметр был вызван **сборки при изменении помещается tooGitHub**.)

   f. Под hello **построения раздел**, из раскрывающегося списка hello **добавить шаг сборки**, выберите параметр hello **вызова скрипта Gradle**. В hello мини-приложении, входящий в путь hello слишком**корневой создания скрипта** для вашего приложения. Он принимает build.gradle из указанного пути hello и соответствующим образом работает. Если вы создаете проект с именем ``MyActor`` (с помощью подключаемого модуля или Yeoman генератора hello Eclipse), скрипт построения корневой hello должен содержать ``${WORKSPACE}/MyActor``. В разделе hello следующий снимок экрана в качестве примера того, как это выглядит:

    ![Действие при сборке Jenkins для Service Fabric][build-step]

   ж. Из hello **действия после построения** раскрывающийся список, выберите **развернуть проект службы структуры**. Здесь требуется tooprovide кластер, который будет разворачиваться сведений, где hello Jenkins скомпилированные приложения Service Fabric. Вы можете также указать сведения о дополнительных приложения использует приложение hello toodeploy. В разделе hello следующий снимок экрана в качестве примера того, как это выглядит:

    ![Действие при сборке Jenkins для Service Fabric][post-build-step]

   > [!NOTE]
   > Hello кластера здесь может быть то же, что один размещения hello hello Jenkins приложения-контейнера, в случае, если вы используете образ контейнера Jenkins hello toodeploy Service Fabric.
   >

## <a name="next-steps"></a>Дальнейшие действия
Теперь GitHub и Jenkins настроены, Попробуйте сделать изменения в образцов вашей ``MyActor`` проекта в примере hello репозитория https://github.com/sayantancs/SFJenkins. Push вашей tooa изменения удаленного ``master`` ветвь (или любой из ветвей, которое вы настроили toowork с). При этом запускается задание hello Jenkins, ``MyJob``, который вы настроили. Выбирает hello изменения из GitHub, их строит и развертывает конечной кластера toohello приложения hello, указанной в действия после построения.  

  <!-- Images -->
  [build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/build-step.png
  [post-build-step]: ./media/service-fabric-cicd-your-linux-java-application-with-jenkins/post-build-step.png
