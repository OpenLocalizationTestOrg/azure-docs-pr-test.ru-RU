---
title: "сервер приложений Java aaaRun в классической виртуальной Машине Azure | Документы Microsoft"
description: "В этом учебнике используются ресурсы, созданные с помощью hello классической модели развертывания и показывает, как toocreate Windows виртуальной машины и настройте его toorun сервера приложений Apache Tomcat."
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: d627aa09-f7d6-4239-8110-f8fc5111b939
ms.service: virtual-machines-windows
ms.workload: web
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 03/16/2017
ms.author: robmcm
ms.openlocfilehash: 2d9f586c9f628d3738522b320996b95b078d7454
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-java-application-server-on-a-virtual-machine-created-with-hello-classic-deployment-model"></a>Как toorun сервера приложений Java на виртуальной машине, созданные с hello классической модели развертывания
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Toodeploy веб-приложение, с помощью Java 8 и Tomcat шаблона диспетчера ресурсов. в разделе [здесь](https://azure.microsoft.com/documentation/templates/201-web-app-java-tomcat/).

С помощью Azure можно использовать возможности сервера tooprovide виртуальной машины. Например виртуальная машина, работающая в Azure может быть toohost настроенный сервер приложений Java, такие как Apache Tomcat.

Изучив это руководство, будет иметь представление о том, как toocreate виртуальной машины в Azure и настройте его toorun сервера приложений Java. Будет Дополнительные сведения и выполните следующие задачи hello.

* Как toocreate виртуальной машины имеет Java Development Kit (JDK) уже установлена.
* Как tooremotely вход tooyour виртуальной машины.
* Как tooinstall сервера приложений Java — Apache Tomcat — на виртуальной машине.
* Как toocreate конечную точку для виртуальной машины.
* Как tooopen hello порт брандмауэра для сервера приложений.

Hello завершить результаты установки в Tomcat, работающий на виртуальной машине.

![Виртуальная машина с Apache Tomcat][virtual_machine_tomcat]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate виртуальной машины
1. Войдите в toohello [портал Azure](https://portal.azure.com).  
2. Нажмите кнопку **New**, нажмите кнопку **вычислений**, нажмите кнопку **все** в hello **рекомендуемыми приложениями**.
3. Нажмите кнопку **JDK**, нажмите кнопку **JDK 8** в hello **JDK** области.  
   Создание образа виртуальной машины, поддерживающие **JDK 6** и **JDK 7** доступны, если у вас есть устаревшие приложения, которые не готовы toorun JDK 8.
4. В области hello JDK 8 выберите **классический**, нажмите кнопку **создать**.
5. В hello **основы** колонки:
   1. Укажите имя для виртуальной машины hello.
   2. Введите имя администратора hello в hello **имя пользователя** поля. Запомнить это имя и соответствующий пароль в следующее поле hello hello. Они необходимы, при удаленном входе в toohello виртуальной машины.
   3. Введите пароль в hello **новый пароль** поле, а затем введите его в hello **подтверждение пароля** поля. Этот пароль — для hello учетной записи администратора.
   4. Выберите hello соответствующие **подписки**.
   5. Для hello **группы ресурсов**, нажмите кнопку **создать новый** и введите имя новой группы ресурсов hello. Или щелкните **использовать существующие** и выберите один из hello доступных групп ресурсов.
   6. Выберите расположение, где находится hello виртуальной машины, такие как **центральных штатах юга США**.
6. Щелкните **Далее**.
7. В hello **размер образа виртуальной машины** колонке выберите **A1 Standard** или другой соответствующий образ.
8. Нажмите кнопку **Выбрать**.

9. В hello **параметры** колонка, щелкните **ОК**. Можно использовать значения по умолчанию hello, предоставляемых Azure.  
10. В hello **Сводка** колонка, щелкните **ОК**.

## <a name="tooremotely-sign-in-tooyour-virtual-machine"></a>tooremotely входа tooyour виртуальной машины
1. Войдите на toohello [портал Azure](https://portal.azure.com).
2. Щелкните **Виртуальные машины (классические)**. При необходимости щелкните **больше услуг** на hello нижний левый угол в группе категорий услуг hello. Hello **виртуальные машины (классические)** запись указана в hello **вычислений** группы.
3. Щелкните имя hello виртуальную машину, которую требуется toosign в hello.
4. После запуска виртуальной машины hello меню вверху hello области hello разрешены подключения.
5. Щелкните **Подключить**.
6. Принятия приглашения toohello необходимые tooconnect toohello виртуальной машины. Как правило сохранении или открытии hello RDP-файл, содержащий сведения о соединении hello. Может иметь toocopy hello URL-адрес: порт hello последнюю часть первая строка hello hello RDP-файл и вставьте его в приложение удаленного входа.

## <a name="tooinstall-a-java-application-server-on-your-virtual-machine"></a>tooinstall сервера приложений Java на виртуальной машине
Можно скопировать виртуальной машины tooyour сервера приложений Java, или можно установить до установки сервера приложений Java.

В этом учебнике используется Tomcat как tooinstall сервера приложений Java hello.

1. Если вы вошли в tooyour виртуальной машины, откройте сеанс браузера слишком[Apache Tomcat](http://tomcat.apache.org/download-80.cgi).
2. Дважды щелкните ссылку hello **установщика службы Windows 32-разрядной или 64-разрядной**. При использовании этого метода сервер Tomcat устанавливается в качестве службы Windows.
3. При появлении запроса выберите установщик toorun hello.
4. В рамках hello **Apache Tomcat установки** tooinstall Tomcat по запросу мастера, выполните hello. Для целей этого учебника hello принять значения по умолчанию hello нормально. По достижении hello **hello завершение работы мастера установки Apache Tomcat** диалоговое окно, можно при необходимости проверить **запустить Apache Tomcat** toohave теперь начала Tomcat. Нажмите кнопку **Готово** toocomplete hello процесс установки Tomcat.

## <a name="toostart-tomcat"></a>toostart Tomcat

Tomcat можно запустить вручную, открыв командную строку на виртуальной машине и hello команды **net&nbsp;запустить&nbsp;Tomcat8**.

После запуска Tomcat можно получить доступ к Tomcat, введя URL-адрес hello <http://localhost: 8080> в браузере hello виртуальной машины.

toosee Tomcat при запуске с внешним компьютерам, нужно toocreate конечной точки и открыть порт.

## <a name="toocreate-an-endpoint-for-your-virtual-machine"></a>toocreate конечную точку для виртуальной машины
1. Войдите в toohello [портал Azure](https://portal.azure.com).
2. Щелкните **Виртуальные машины (классические)**.
3. Щелкните имя hello hello виртуальной машины, на котором выполняется сервер приложений Java.
4. Нажмите кнопку **Конечные точки**.
5. Щелкните **Добавить**.
6. В hello **добавить конечную точку** диалоговое окно:
   1. Укажите имя для конечной точки hello; например **HttpIn**.
   2. Выберите **TCP** для протокола hello.
   3. Укажите **80** hello открытого порта.
   4. Укажите **8080** для hello частный порт.
   5. Выберите **отключено** для hello плавающей IP-адрес.
   6. Оставьте hello список управления доступом как есть.
   7. Нажмите кнопку hello **ОК** кнопку hello tooclose-диалоговое окно и создать конечную точку hello.

## <a name="tooopen-a-port-in-hello-firewall-for-your-virtual-machine"></a>tooopen порта в брандмауэре hello для виртуальной машины
1. Войдите в tooyour виртуальной машины.
2. Нажмите **кнопку "Пуск" в Windows**.
3. Нажмите **Панель управления**.
4. Щелкните **Система и безопасность**, **Брандмауэр Windows**, а затем — **Расширенные настройки**.
5. Щелкните **Правила для входящих подключений**, а затем — **Создать правило**.  
   ![Новое правило для входящего подключения][NewIBRule]
6. Для hello **тип правила**выберите **порт**, а затем нажмите кнопку **Далее**.  
   ![Порт нового правила для входящего подключения][NewRulePort]
7. На hello **протокол и порты** выберите **TCP**, укажите **8080** как hello **определенный порт локального**и нажмите кнопку **Далее**.  
  ![Новое правило для входящего подключения][NewRuleProtocol]
8. На hello **действия** выберите **разрешить подключение hello**, а затем нажмите кнопку **Далее**.
   ![Действие нового правила для входящего подключения][NewRuleAction]
9. На hello **профиль** экране, убедитесь, что **домена**, **закрытый**, и **открытый** выбраны и нажмите кнопку **Далее** .
   ![Профиль нового правила для входящего подключения][NewRuleProfile]
10. На hello **имя** укажите имя для правила hello, таких как **HttpIn** (имя правила hello не имя конечной точки требуется toomatch hello, однако) и нажмите кнопку **Готово**.  
    ![Имя нового правила для входящего подключения][NewRuleName]

С этого момента ваш веб-сайт Tomcat должен быть доступен для просмотра во внешнем браузере. В окне браузера hello адреса введите URL-адрес формы hello  **http://*вашей\_DNS\_имя*. cloudapp.net**, где ***вашей\_DNS\_имя*** hello DNS-именем, указанным при создании hello виртуальной машины.

## <a name="application-lifecycle-considerations"></a>Вопросы, связанные с жизненным циклом приложения
* Можно создать собственные веб-архива приложения (WAR) и добавьте его toohello **веб-приложений** папки. Например, создайте динамический веб-проект базовой страницы службы Java (JSP) и экспортируйте его как WAR-файл. Затем скопируйте toohello WAR hello Apache Tomcat **веб-приложений** папки на виртуальной машине hello, запустите его в браузере.
* По умолчанию при установке службы Tomcat hello, он имеет значение toostart вручную. Можно переключить его toostart автоматически с помощью оснастки hello службы. Запустите оснастку hello службы, щелкнув **Пуск**, **Администрирование**, а затем **службы**. Дважды щелкните hello **Apache Tomcat** и задайте для **тип запуска** слишком**автоматического**.

    ![Параметр toostart службы автоматически][service_automatic_startup]

    Hello преимущество наличия Tomcat автоматический запуск — что он начинает работу во время перезагрузки hello виртуальной машины (например, после установки обновления программного обеспечения, которые требуют перезагрузки).

## <a name="next-steps"></a>Дальнейшие действия
Вы можете узнать о других служб (например, хранилище Azure, служебной шины и базы данных SQL), которые вы можете tooinclude с приложениями Java. Просмотреть hello сведений, доступных в hello [центра разработчиков Java](https://azure.microsoft.com/develop/java/).

[virtual_machine_tomcat]:media/java-run-tomcat-app-server/WA_VirtualMachineRunningApacheTomcat.png

[service_automatic_startup]:media/java-run-tomcat-app-server/WA_TomcatServiceAutomaticStart.png









[NewIBRule]:media/java-run-tomcat-app-server/NewInboundRule.png
[NewRulePort]:media/java-run-tomcat-app-server/NewRulePort.png
[NewRuleProtocol]:media/java-run-tomcat-app-server/NewRuleProtocol.png
[NewRuleAction]:media/java-run-tomcat-app-server/NewRuleAction.png
[NewRuleName]:media/java-run-tomcat-app-server/NewRuleName.png
[NewRuleProfile]:media/java-run-tomcat-app-server/NewRuleProfile.png


<!-- Deleted from hello "toocreate an ednpoint for your virtual mache" 3/17/2017,
     toouse hello new portal.
6. In hello **Add endpoint** dialog box, ensure **Add standalone endpoint** is selected, and then click **Next**.
7. In hello **New endpoint details** dialog box:
-->
