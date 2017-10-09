---
title: "Подключаемый модуль для Eclipse Service Fabric aaaAzure | Документы Microsoft"
description: "Начало работы с hello Service Fabric подключаемого модуля для Eclipse."
services: service-fabric
documentationcenter: java
author: sayantancs
manager: timlt
editor: 
ms.assetid: bf84458f-4b87-4de1-9844-19909e368deb
ms.service: service-fabric
ms.devlang: java
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/21/2016
ms.author: saysa
ms.openlocfilehash: 4ba5a28a6282387249a2bd4e62314e891ff04162
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="service-fabric-plug-in-for-eclipse-java-application-development"></a>Подключаемый модуль Service Fabric для разработки приложений Eclipse на Java
Eclipse является одним из наиболее широко используемых hello интегрированной среды разработки (IDE) для разработчиков Java. В этой статье описывается как tooset копирование вашей toowork среды Eclipse разработки с Azure Service Fabric. Узнайте, как создать приложение Service Fabric hello tooinstall Service Fabric подключаемого модуля, и развертывания вашего Service Fabric приложения tooa локальный или удаленный Service Fabric кластера в Eclipse Neon.

## <a name="install-or-update-hello-service-fabric-plug-in-in-eclipse-neon"></a>Установите или обновите hello подключаемый модуль в Eclipse Neon Service Fabric
Вы можете установить подключаемый модуль Service Fabric в Eclipse. Подключаемый модуль Hello позволяет упростить процесс hello Создание и развертывание служб Java.

1.  Убедитесь, что последняя версия Eclipse Neon hello и hello последнюю версию Buildship установлен (1.0.17 или более поздней версии):
    -   toocheck hello версии установленных компонентов в Eclipse Neon go слишком**справки** > **сведения об установке**.
    -   в разделе tooupdate Buildship, [Eclipse Buildship: подключаемые модули Eclipse для Gradle][buildship-update].
    -   toocheck для и установка обновлений для Eclipse Neon go слишком**справки** > **проверять наличие обновлений**.

2.  hello tooinstall Service Fabric подключаемый модуль в Eclipse Neon go слишком**справки** > **Установка нового программного обеспечения**.
  1.    В hello **работать с** введите **http://dl.microsoft.com/eclipse**.
  2.    Щелкните **Добавить**.

         ![Подключаемый модуль Service Fabric для Eclipse Neon][sf-eclipse-plugin-install]
  3.    Выберите hello Service Fabric подключаемого модуля и нажмите кнопку **Далее**.
  4.    Выполните шаги установки hello и примите условия лицензии программного обеспечения корпорации Майкрософт hello.

Если уже имеется hello Service Fabric подключаемый модуль установлен, убедитесь, что имеется hello последнюю версию. toocheck наличие доступных обновлений go слишком**справки** > **сведения об установке**. В списке установленных подключаемых модулей hello выберите Service Fabric и нажмите кнопку **обновление**. После этого будут установлены доступные обновления.

> [!NOTE]
> При установке или обновлении hello Service Fabric подключаемый модуль выполняется медленно, возможно из-за параметра tooan Eclipse. Eclipse собирает метаданных на все сайты tooupdate изменения, зарегистрированные в вашем экземпляре Eclipse. toospeed hello процесс проверки и установки обновления Service Fabric подключаемого модуля, go слишком**доступных сайтов программного обеспечения**. Снимите флажки hello для всех сайтов, за исключением hello тот, который указывает расположение подключаемого модуля Service Fabric toohello (http://dl.microsoft.com/eclipse/azure/servicefabric).

## <a name="create-a-service-fabric-application-in-eclipse"></a>Создание приложения Service Fabric в Eclipse

1.  В Eclipse Neon перейдите слишком**файл** > **New** > **других**. Выберите **Service Fabric Project** (Проект Service Fabric) и нажмите кнопку **Next** (Далее).

    ![Создание проекта Service Fabric, страница 1][create-application/p1]

2.  Введите имя проекта и нажмите кнопку **Next** (Далее).

    ![Создание проекта Service Fabric, страница 2][create-application/p2]

3.  В списке шаблонов hello выберите **шаблона службы**. Выберите тип шаблона службы (субъект, без отслеживания состояния, контейнер или гостевой двоичный файл) и нажмите кнопку **Next** (Далее).

    ![Создание проекта Service Fabric, страница 3][create-application/p3]

4.  Введите имя службы hello и службы сведения и нажмите кнопку **Готово**.

    ![Создание проекта Service Fabric, страница 4][create-application/p4]

5. При создании первого проекта Service Fabric в hello **открыть связанный перспективу** диалоговое окно, нажмите кнопку **Да**.

    ![Создание проекта Service Fabric, страница 5][create-application/p5]

6.  Новый проект выглядит следующим образом:

    ![Создание проекта Service Fabric, страница 6][create-application/p6]

## <a name="build-and-deploy-a-service-fabric-application-in-eclipse"></a>Создание и развертывание приложения Service Fabric в Eclipse

1.  Щелкните правой кнопкой мыши новое приложение Service Fabric, а затем выберите **Service Fabric**.

    ![Контекстное меню Service Fabric][publish/RightClick]

2. В подменю «hello» выберите нужный параметр hello:
    -   Щелкните приложение hello toobuild без очистки, **сборки приложения**.
    -   Нажмите кнопку toodo чистую сборку приложения hello **перестроить приложения**.
    -   приложение hello tooclean артефактов сборки, откройте **чистой приложения**.

3.  В этом меню также есть параметры, позволяющие развернуть, отменить развертывание и опубликовать приложение.
    -   toodeploy tooyour локального кластера, нажмите кнопку **развертывание приложения**.
    -   В hello **публикация приложения** диалогового окна выберите профиль публикации:
        -  **Local.json**;
        -  **Cloud.json**.

     Эти файлы JavaScript Object Notation (JSON) хранения сведений (например, конечные точки подключения и сведения о безопасности), которые требуется tooconnect tooyour локальной или кластера с облаком (Azure).

  ![Меню публикации Service Fabric][publish/Publish]

Альтернативный способ toodeploy приложения Service Fabric с помощью Eclipse выполняется конфигураций.

  1.    Go слишком**запуска** > **конфигурации запусков**.
  2.    В разделе **проекта Gradle**выберите hello **ServiceFabricDeployer** конфигурации запуска.
  3.    В правой панели hello в hello **аргументы** вкладке для **publishProfile**выберите **локального** или **облака**.  по умолчанию Hello — **локальной**. toodeploy tooa удаленного или облака кластера, выберите **облака**.
  4.    tooensure, что соответствующие сведения hello заполняется hello профилей публикации, изменить **Local.json** или **Cloud.json** при необходимости. Вы можете добавить или обновить сведения о конечной точке и учетные данные безопасности.
  5.    Убедитесь, что **рабочий каталог** указывает toohello приложение, toodeploy. toochange Здравствуйте, приложения, нажмите кнопку hello **рабочей** кнопку, а затем выберите приложение hello.
  6.    Щелкните **Apply** (Применить), а затем — **Run** (Запуск).

Приложение будет собрано и развернуто через несколько секунд. Можно отслеживать состояние развертывания hello в обозреватель Service Fabric.  

## <a name="add-a-service-fabric-service-tooyour-service-fabric-application"></a>Добавить tooyour служба Service Fabric приложения Service Fabric

tooadd Service Fabric service tooan существующие приложения Service Fabric, hello следующие действия:

1.  Щелкните правой кнопкой мыши проект hello вы tooadd службе и нажмите кнопку **Service Fabric**.

    ![Добавление службы Service Fabric, страница 1][add-service/p1]

2.  Нажмите кнопку **добавьте служба Service Fabric**, а hello полный набор tooadd действия проект toohello службы.
3.  Шаблон службы выберите hello tooadd tooyour проекта и нажмите кнопку **Далее**.

    ![Добавление службы Service Fabric, страница 2][add-service/p2]

4.  Введите имя службы hello (и другие сведения, при необходимости) и нажмите кнопку hello **добавить службу** кнопки.  

    ![Добавление службы Service Fabric, страница 3][add-service/p3]

5.  После добавления службы hello общей структуры проекта выглядит примерно toohello следующих проектов:

    ![Добавление службы Service Fabric, страница 4][add-service/p4]

## <a name="edit-manifest-versions-of-your-service-fabric-java-application"></a>Изменение версий манифеста приложения Service Fabric на Java

tooedit версии манифеста, щелкните правой кнопкой мыши проект hello, go слишком**Service Fabric** и выберите **изменение версии манифеста...**  из раскрывающегося меню hello. В мастере приветствия, можно обновить hello манифеста для манифеста, манифест службы приложения и hello версии для **кода**, **Config** и **данные** пакетов.

Если выбран параметр hello **автоматическое обновление версий приложения и службы** и затем обновить версию, затем hello манифеста версии будут обновляться автоматически. toogive пример сначала выбрать флажок hello, а затем обновленную версию hello **кода** версии из 0.0.0 too0.0.1 и нажмите кнопку **Готово**, затем службы версии манифеста и манифест приложения версия будет автоматически обновляются too0.0.1.

## <a name="upgrade-your-service-fabric-java-application"></a>Обновление приложения Service Fabric на Java

Для сценария обновления, предположим, вы создали hello **App1** проекта с помощью подключаемого модуля в Eclipse Service Fabric hello. Он был развернут с помощью подключаемого модуля toocreate hello приложения с именем **fabric: / App1Application**. Тип приложения Hello **App1AppicationType**, и версия приложения hello-1.0. Теперь требуется tooupgrade приложения без прерывания доступа.

Во-первых, внесите изменения tooyour приложения, а затем перестроить hello изменения службы. Обновление hello изменить файл манифеста службы (ServiceManifest.xml) с версиями hello обновления для службы hello (и кода, конфигурации и данных, таких как соответствующие). Кроме того изменить манифест приложения hello (ApplicationManifest.xml) с hello обновить номер версии для приложения hello и hello измененные службы.  

tooupgrade приложения с помощью Eclipse Neon, можно создать профиль повторяющиеся конфигурации запуска. Затем используйте tooupgrade приложения при необходимости.

1.  Go слишком**запуска** > **конфигурации запусков**. Hello левой панели щелкните hello маленькую стрелку toohello слева от **Gradle проекта**.
2.  Щелкните правой кнопкой мыши **ServiceFabricDeployer** и выберите **Duplicate** (Дублировать). Введите новое имя для этой конфигурации, например **ServiceFabricUpgrader**.
3.  На правой панели hello и на hello **аргументы** измените **- Pconfig = «развертывание»** слишком**- Pconfig = «обновить»**и нажмите кнопку **применить**.

Этот процесс создает и сохраняет профиль конфигурации запуска можно использовать в любое время tooupgrade приложения. Он также возвращает hello последнюю версию типа обновленное приложение из файла манифеста приложения hello.

обновление приложения Hello занимает несколько минут. Вы можете отслеживать обновления приложения hello в обозреватель Service Fabric.

## <a name="migrating-old-service-fabric-java-applications-toobe-used-with-maven"></a>Миграция старый toobe приложений Java структуры службы, используемые с Maven
Служба Fabric Java библиотеки недавно были удалены из репозитория tooMaven Service Fabric Java SDK. Хотя hello новые приложения, созданные с помощью Eclipse, создаст последних измененных проектов (которые будут может toowork с Maven), необходимо обновить существующие структуры службы без сохранения состояния и приложения Java субъектов, которые использовали hello Service Fabric Java SDK более ранние версии, toouse hello Java структуры службы зависимостей из Maven. Выполните шаги hello упомянутые [здесь](service-fabric-migrate-old-javaapp-to-use-maven.md) tooensure старые приложения работает с Maven.

<!-- Images -->

[sf-eclipse-plugin-install]: ./media/service-fabric-get-started-eclipse/service-fabric-eclipse-plugin.png

[create-application/p1]:./media/service-fabric-get-started-eclipse/create-application/p1.png
[create-application/p2]:./media/service-fabric-get-started-eclipse/create-application/p2.png
[create-application/p3]:./media/service-fabric-get-started-eclipse/create-application/p3.png
[create-application/p4]:./media/service-fabric-get-started-eclipse/create-application/p4.png
[create-application/p5]:./media/service-fabric-get-started-eclipse/create-application/p5.png
[create-application/p6]:./media/service-fabric-get-started-eclipse/create-application/p6.png

[publish/Publish]: ./media/service-fabric-get-started-eclipse/publish/Publish.png
[publish/RightClick]: ./media/service-fabric-get-started-eclipse/publish/RightClick.png

[add-service/p1]: ./media/service-fabric-get-started-eclipse/add-service/p1.png
[add-service/p2]: ./media/service-fabric-get-started-eclipse/add-service/p2.png
[add-service/p3]: ./media/service-fabric-get-started-eclipse/add-service/p3.png
[add-service/p4]: ./media/service-fabric-get-started-eclipse/add-service/p4.png

<!-- Links -->
[buildship-update]: https://projects.eclipse.org/projects/tools.buildship
