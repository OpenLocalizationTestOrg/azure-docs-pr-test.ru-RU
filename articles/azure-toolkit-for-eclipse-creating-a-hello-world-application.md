---
title: "aaaCreate Hello World облачной службы для Azure в Eclipse"
description: "Узнайте, как простого приложения Hello World с использованием toocreate hello средств Azure для Eclipse."
services: 
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 7262e705-59d6-43ce-b888-29a21c8e0cb7
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: multiple
ms.devlang: Java
ms.topic: article
ms.date: 04/14/2017
ms.author: robmcm
ms.openlocfilehash: dfb81374aaf78e933c0bf83a1dbd98023801491a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-hello-world-cloud-service-for-azure-in-eclipse"></a>Создание облачной службы Hello World для Azure в Eclipse
Hello следующие шаги показывают, как toocreate и развертывание основных tooAzure приложения JSP, с помощью hello набора средств Azure для Eclipse. Пример с JSP приведен для простоты, но при развертывании в Azure можно применять практически идентичные шаги для сервлета Java.

приложение Hello будет выглядеть аналогично toohello следующее:

![][ic600360]

## <a name="prerequisites"></a>Предварительные требования
* Java Developer Kit (JDK), версия 1.7 или более поздняя.
* Интегрированная среда разработки Eclipse для разработчиков Java EE, версия Indigo или более поздняя. Скачать ее можно на веб-странице <http://www.eclipse.org/downloads/>.
* Дистрибутив веб-сервера или сервера приложений на основе Java, например Apache Tomcat, GlassFish, сервер приложений JBoss, Jetty или IBM® WebSphere® Application Server Liberty Core.
* Подписка на Azure, которую можно получить, перейдя по ссылке <http://azure.microsoft.com/pricing/purchase-options/>.
* Здравствуйте, средств Azure для Eclipse. Дополнительные сведения см. в разделе [hello Установка средств Azure для Eclipse][Installing hello Azure Toolkit for Eclipse].

## <a name="toocreate-a-hello-world-application"></a>toocreate приложения Hello World
Сначала необходимо создать проект Java.

1. Запустите Eclipse и hello меню пункт **файл**, нажмите кнопку **New**и нажмите кнопку **динамический веб-проект**. (Если вы не видите **динамический веб-проект** после нажатия кнопки в списке доступных проектов **файл**, **New**, затем hello следующие: щелкните **файл**, нажмите кнопку **New**, нажмите кнопку **проекта...** , разверните **Web**, нажмите кнопку **динамический веб-проект**и нажмите кнопку **Далее**.)

1. В целях этого учебника назовите проект hello **MyHelloWorld**. (Убедитесь, используйте это имя, последующие шаги в этом учебнике ожидается, что ваш файл toobe WAR, с именем MyHelloWorld). На экране появится примерно следующее toohello:

   ![][ic589576]

1. Нажмите кнопку **Готово**

1. В окне обозревателя проектов в Eclipse разверните узел **MyHelloWorld**. Щелкните правой кнопкой мыши **WebContent**, выберите **Создать**, затем щелкните **JSP File** (JSP-файл).

1. В hello **Создание JSP-файла** диалогового окна, имя файла hello **index.jsp**. Сохранить hello родительскую папку как **MyHelloWorld/WebContent**, как показано в следующих hello:

   ![][ic659262]

1. В hello **Выбор шаблона JSP** диалоговое окно, в целях этого учебника выберите **новый JSP-файл (html)** и нажмите кнопку **Готово**.

1. При открытии файла index.jsp hello в Eclipse добавьте в виде текста toodynamically **Здравствуй, мир!** в существующих hello `<body>` элемента. Обновленный `<body>` должно отобразиться содержимое hello следующим образом:
   ```
   <body>
   <b><% out.println("Hello World!"); %></b>
   </body>
   ```
1. Сохраните index.jsp.

## <a name="toodeploy-your-application-tooazure-hello-quick-and-simple-way"></a>toodeploy ваше приложение tooAzure, hello быстрый и простой способ
Как только Java tootest готовности веб приложения, можно использовать следующие сочетания tootry, он помещает непосредственно на hello Azure cloud hello.

1. В обозревателе проектов Eclipse щелкните правой кнопкой мыши **MyHelloWorld**.

2. Hello инструментов Eclipse нажмите hello **публикации** кнопка раскрытия списка и нажмите кнопку **опубликовать как облачные службы**

   ![][publishDropdownButton]

3. Если вы не создали проект развертывания Azure для этого приложения, прежде чем публикации этого приложения tooAzure для hello первый раз, проект развертывания Azure создаются автоматически. Должны появиться следующие hello приглашении перечнем hello JDK пакета и сервера приложений, будет автоматически toorun приложение развернуто.

   ![][ic789598]
   
   Этот подход позволяет tootest быстрый и простой способ вашего приложения в Azure без tooconfigure определенного сервера или JDK, который отличается от значения по умолчанию hello. Если вас устраивают значения по умолчанию hello, можно щелкнуть **ОК** toocontinue с hello следующие шаги.
   Тем не менее если требуется, чтобы toochange hello JDK или toouse сервера приложений для приложения, это можно сделать позже, изменив hello проект развертывания Azure, который был автоматически создан автоматически, или можно щелкнуть **отменить** сейчас» и «чтение Hello **проекты развертывания Azure о разделе** этого учебника.

4. В hello **публикации tooAzure** диалогового окна:

   1. Если нет подписок tooselect hello **подписки** список еще не, выполните эти шаги tooimport сведений о подписке:
      1. Щелкните **Импорт из PUBLISHSETTINGS-файла**.
      2. В hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку **загрузить файл параметров публикации**. Если вы еще не выполнили вход в учетную запись Azure, появится запрос toolog в. Затем вам будет предложено toosave Azure файл параметров публикации. Сохраните tooyour локального компьютера.
      3. По-прежнему в hello **Импорт сведений о подписке** диалоговое окно, нажмите кнопку hello **Обзор** кнопку, выберите hello опубликовать файл параметров, который был сохранен локально на предыдущем шаге hello и нажмите кнопку  **Откройте**. Экран должен выглядеть примерно toohello следующее:![][ic644267]
      4. Нажмите кнопку **ОК**.
   2. Для **подписки**, выберите hello подписку, которую нужно использовать для развертывания.
   3. Для **учетной записи хранилища**, выберите учетную запись хранения hello, должны быть toouse, или нажмите кнопку **New** toocreate новой учетной записи хранения.
   4. Для **имя службы**, выберите облачную службу hello, должны быть toouse, или нажмите кнопку **New** toocreate новой облачной службы.
   5. Для **целевая ОС**выберите версию hello hello операционной системы требуется toouse для развертывания.
   6. В поле **Целевая среда** для целей этого руководства выберите **Промежуточная среда**. (Когда вы будете готовы toodeploy tooyour рабочего сайта, мы изменим это слишком**рабочей**.)
   7. Необязательно: Убедитесь, что **перезапись предыдущего развертывания** проверяется, если требуется, чтобы ваш новый tooautomatically развертывания перезаписи hello предыдущего развертывания. При выборе этого варианта будет не проблемы качества «409 конфликт» при публикации toohello местоположения.
      Обратите внимание, что hello **публикации tooAzure** диалоговое окно содержит раздел для **удаленного доступа**. По умолчанию удаленный доступ выключен, и мы не будем включать его в этом примере. tooenable удаленного доступа, можно ввести toouse имя и пароль пользователя при входе удаленно. Дополнительные сведения об удаленном доступе см. в статье [Включение удаленного доступа для развертываний Azure в Eclipse][Enabling Remote Access for Azure Deployments in Eclipse].
      Ваш **публикации tooAzure** диалогового окна появится примерно следующее toohello:![][ic719488]

5. Нажмите кнопку **публикации** toopublish toohello промежуточной среде.

   Если запрос tooperform полное построение, нажмите кнопку **Да**. Это может занять несколько минут для первого построения hello.
   В разделе представлений с вкладками Eclipse откроется **журнал действий Azure** .
   ![][ic719489]Вы можете использовать этот журнал, а также hello **консоли** просмотра toosee hello хода выполнения развертывания. Альтернативным вариантом является toolog в toohello [портала управления Azure][Azure Management Portal]и использовать hello **облачные службы** toomonitor hello состояние статьи.

6. После успешного развертывания развертывания hello **журнал действий Azure** будет отображаться статус **опубликовано**. Нажмите кнопку **опубликовано**, как показано в следующих hello изображения и браузере откроется экземпляр развертывания.

   ![][ic719490]

Так как это было tooa развертывания, в промежуточной среде, hello DNS-имя будет иметь вид http:// hello&lt;*guid*&gt;. cloudapp.net и hello URL-адрес будет содержать hello DNS-имя и суффикс для приложения. Например, http://447564652c20426f6220526f636b7321.cloudapp.net/MyHelloWorld. (hello **MyHelloWorld** часть чувствителен к регистру.) Можно также просмотреть hello DNS имя, если щелкнуть имя развертывания hello в hello портала управления платформой Azure (в части облачных служб hello для портала управления hello).

Несмотря на то, что это пошаговое руководство предназначено для toohello развертывания, в промежуточной среде, следует tooproduction развертывания hello же шаги, за исключением внутри hello **публикации tooAzure** диалогового окна выберите **рабочей** вместо **промежуточной** для hello **целевой среды**. Приводит URL-адрес, на основе имени DNS hello по своему усмотрению, вместо GUID, используемого для промежуточной tooproduction развертывания.

> [!WARNING]
> На этом этапе вы развернули свое облако toohello приложения Azure. Тем не менее прежде чем продолжить, понимать, что развертываемое приложение, даже если она не запущена, будут продолжать tooaccrue Оплачиваемое время для вашей подписки. Поэтому крайне важно удалять ненужные развертывания из подписки Azure.
> 
> 

## <a name="about-azure-deployment-projects"></a>О проектах развертывания Azure
Чтобы toodeploy один или несколько tooAzure приложений Java, требуется проект развертывания Azure. Он выступает hello hello «пакет», которые приложения должны toobe в оболочку в порядке toobe публикации в Azure.

Помимо hello сведения о приложениях проект развертывания Azure также содержит сведения о других ключевых компонентах развертывания, самое главное: hello toorun контейнер сервера приложений в веб-приложения и hello toorun среды выполнения Java его в. В Azure доступно большое количество сред выполнения Java и серверов приложений Java.

Несмотря на то, что здесь используется пример hello существенно упрощен в образовательных целях, проект развертывания Azure также может содержать другие важные сведения о конфигурации, позволяющая toocreate произвольные и довольно сложные, масштабируемые и высокой доступности многоуровневые облачные службы с приложениями. Вы можете включить **сходство сеансов** ("прикрепленные сеансы"), **быстрое кэширование**, **разгрузку SSL**, **маршрутизацию брандмауэра и порта**, **удаленный доступ** и ряд других эффективных возможностей.

Если после завершения предыдущего раздела этого учебника hello («toodeploy ваше приложение tooAzure, hello быстрый и простой способ»), будет отображен новый проект развертывания Azure в hello обозревателя проектов создается автоматически и с именем « **MyHelloWorld_onAzure**».

Можно также начать этого учебника путем создания пустого проекта развертывания Azure самостоятельно и затем добавив tooit вашего приложения. Она больше процесс, но что дает больший контроль над hello начальной конфигурации с начала hello.

toocreate нового проекта развертывания Azure с нуля, нажмите кнопку hello **новый проект развертывания Azure** кнопку ![][ic710876].

Независимо от того, работа с уже существующим проектом развертывания Azure, или создать его с нуля, вы могли toochange его параметры конфигурации и компоненты, такие как hello JDK или сравнительно просто hello сервера приложений в любое время.

hello toochange JDK, или сервер приложений hello или hello список приложений в существующем проекте развертывания Azure:

1. Разверните узел проекта hello (например **MyHelloWorld_onAzure**) в обозревателе проектов hello

2. Щелкните правой кнопкой мыши **WorkerRole1**

3. Разверните hello **Azure** подменю в контекстном меню hello

4. Нажмите кнопку **Конфигурация сервера**

Вне зависимости от вас запущен ли эти шаги по настройке сервера путем изменения существующего проекта развертывания Azure, как показано выше, или создать новую с нуля, вы увидите hello того же типа, диалоговых окон, позволяя tooconfigure пакет JDK, сервера и приложения компоненты. toolearn более как параметры toochange hello в этих диалоговых окнах, например toochange hello JDK, hello сервера приложений и добавления или удаления приложения при развертывании в разделе hello [свойства конфигурации сервера] [ Server configuration properties] статьи.

## <a name="windows-only-toodeploy-your-application-toohello-compute-emulator"></a>Только для Windows: toodeploy эмулятор вычислений toohello вашего приложения

> [!NOTE]
> Hello эмулятор Azure доступен только в Windows. Этот раздел можно пропустить, если вы используете другую операционную систему.
> 
> 

При создании нового проекта развертывания Azure hello действий, описанных ранее, т. е. неявным образом, путем публикации вашей tooAzure приложения hello JDK и серверы приложений были настроены для облака hello, но не для локальной эмуляции. tooprepare проекта для тестирования в локальном эмуляторе hello, выполните следующие действия:

1. В обозревателе проектов Eclipse щелкните **MyHelloWorld_onAzure**.

2. Щелкните правой кнопкой мыши **WorkerRole1**.

3. Разверните hello **Azure** подменю в контекстном меню hello.

4. Щелкните **Конфигурация сервера**.

5. На hello **JDK** проверьте, если hello toolkit предварительную настройку локального JDK. Если не или если требуется toochange hello, предполагается, что значения по умолчанию, убедитесь, что hello **hello использовать JDK по этому пути к файлу для локального тестирования** установлен флажок, и указано расположение установки JDK, что требуется toouse hello. Если требуется, чтобы toochange его, щелкните hello **Обзор** и с помощью элемента управления обзора hello, выберите расположение каталога hello JDK toouse hello.

6. Нажмите кнопку hello **сервера** вкладки.

7. В hello **путь к локальному серверу** текстовое поле внизу hello диалогового окна "hello", введите путь hello локально установленному серверу, который соответствует типу hello и основной номер версии сервера hello, выбранного в верхней hello диалогового окна "hello", в разделе Hello **развернуть сервер этого типа** флажок. Если требуется toouse другой тип или основной номер версии сервера приложения hello, сначала измените hello выбора в списке, соответствующий флажок.

8. Нажмите кнопку **ОК**.

9. Hello инструментов Eclipse нажмите hello **запуск в эмуляторе Azure** кнопки ![][ic710879]. Если hello **запуск в эмуляторе Azure** кнопка недоступна, убедитесь, что **MyHelloWorld_onAzure** выбран в обозревателе проектов Eclipse и убедитесь, что в обозревателе проектов Eclipse имеет фокус, как hello текущее окно. Это будет сначала запущено полное построение проекта, а затем запустить веб-приложение Java в эмуляторе вычислений hello. (Обратите внимание, что в зависимости от характеристик производительности компьютера, hello первого построения может занять от нескольких секунд tooa несколько минут, но последующие построения будут запускаться быстрее). После завершения первого шага построения hello, вам нужно будет с помощью Windows (Учетных записей) tooallow toomake этой команды изменяется tooyour компьютера. Щелкните **Да**.

> [!IMPORTANT]
> Если вы не видите hello UAC приглашения, проверка hello задач Windows для значка UAC hello и щелкните его. Иногда hello Контроля учетных записей не отображается поверх всех окон, однако является видимым только как значок на панели задач.
> 
> 

1. Изучите выходные данные hello toodetermine пользовательского интерфейса эмулятора вычислений hello, если возникли проблемы с проектом. В зависимости от содержимого hello развертывания может потребоваться несколько минут для вашего приложения toobe, полностью запустится в эмуляторе вычислений hello.

2. Запустите браузер и используйте URL-адрес hello `http://localhost:8080/MyHelloWorld` как адрес hello (hello `MyHelloWorld` hello URL-адресе с учетом регистра). Вы увидите ваше приложение MyHelloWorld (результат index.jsp hello), аналогично toohello после изображения:

   ![][ic589579]

Все готово toostop выполнение приложения в эмуляторе вычислений hello, в панели инструментов Eclipse hello, нажмите кнопку hello **сбросить эмулятор Azure** кнопки ![][ic710880].

## <a name="toodelete-your-deployment"></a>toodelete развертывания
toodelete развертывание в hello средств Azure для Eclipse, убедитесь, что **MyHelloWorld_onAzure** будет выбран в обозревателе проектов Eclipse, убедитесь, hello обозревателя проектов Eclipse hello текущее окно сосредоточиться, а затем нажмите кнопку Hello **отменить публикацию** кнопки ![][ic710883], в панели инструментов Eclipse hello. (Это можно сделать Здравствуйте одной операции, щелкнув правой кнопкой мыши **MyHelloWorld_onAzure** в обозревателе проектов Eclipse, щелкнув **Azure** и выбрав **отменить развертывание в облаке Azure**.) При этом отобразится hello **Отмена публикации проекта Azure** диалогового окна.

![][ic719491]

Выберите подписку и облачную службу hello, содержащий развертывания, выберите hello развертывания требуется toodelete и нажмите кнопку **отменить публикацию**.

(Альтернативный toousing hello toolkit toodelete hello развертывания — toouse hello **облачные службы** раздел hello портала управления Azure: найдите tooyour развертывания, выберите его и нажмите кнопку hello **удаление** кнопки. Это остановите и удалите hello развертывания. Если нужен только toostop hello развертывания и удаляет его, нажмите кнопку hello **остановить** кнопки вместо hello **удалить** кнопку, но, как упоминалось выше, если не удалить развертывание hello, будет Оплачиваемое по-прежнему tooaccrue для развертывания даже если она была выключена).

## <a name="see-also"></a>См. также
[Набор средств Azure для Eclipse][Azure Toolkit for Eclipse]

[Установка средств Azure для Eclipse hello][Installing hello Azure Toolkit for Eclipse] 

[Новые возможности средств Azure для Eclipse hello][What's New in hello Azure Toolkit for Eclipse]

Дополнительные сведения об использовании Azure с Java см. в разделе hello [центра разработчиков Java Azure][Azure Java Developer Center].

<!-- URL List -->

[Azure Java Developer Center]: http://go.microsoft.com/fwlink/?LinkID=699547
[Azure Management Portal]: http://go.microsoft.com/fwlink/?LinkID=512959
[Azure Role Properties]: http://go.microsoft.com/fwlink/?LinkID=699525
[Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699529
[Enabling Remote Access for Azure Deployments in Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699538
[Installing hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkId=699546
[Server configuration properties]: http://go.microsoft.com/fwlink/?LinkID=699525#server_configuration_properties
[What's New in hello Azure Toolkit for Eclipse]: http://go.microsoft.com/fwlink/?LinkID=699552

<!-- IMG List -->

[ic589576]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589576.png
[ic589579]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic589579.png
[ic600360]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic600360.png
[ic644267]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic644267.png
[ic659262]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic659262.png
[ic710876]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710876.png
[ic710879]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710879.png
[ic710880]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710880.png
[ic710882]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710882.png
[ic710883]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic710883.png
[ic719488]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719488.png
[ic719489]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719489.png
[ic719490]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719490.png
[ic719491]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic719491.png
[ic789598]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/ic789598.png
[publishDropdownButton]: ./media/azure-toolkit-for-eclipse-creating-a-hello-world-application/publishDropdownButton.png

<!-- Legacy MSDN URL = https://msdn.microsoft.com/library/azure/hh690944.aspx -->
