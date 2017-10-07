---
title: "aaaDeploy SAP S/4HANA или BW/4HANA на Виртуальной машине Azure | Документы Microsoft"
description: "Развертывание SAP S/4HANA или BW/4HANA на виртуальной машине Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 44bbd2b6-a376-4b5c-b824-e76917117fa9
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 7e57f7daa7667b7c7dbcb86f6892a54e4295b74c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-s4hana-or-bw4hana-on-azure"></a>Развертывание SAP S/4HANA или BW/4HANA в Azure
В этой статье описывается, как toodeploy S/4HANA в Azure с помощью hello SAP облачной устройства библиотеки (SAP CAL) 3.0. toodeploy других решений на основе SAP HANA, например BW/4HANA выполните hello одну последовательность шагов.

> [!NOTE]
Дополнительные сведения о hello SAP CAL go toohello [SAP облачной устройства библиотеки](https://cal.sap.com/) веб-сайта. SAP также есть блог о hello [устройство библиотеки SAP облака 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience).

> [!NOTE]
Кроме как 29 мая 2017 г., можно использовать модель развертывания диспетчера ресурсов Azure hello toohello менее предпочтительным классическое развертывание модели toodeploy hello SAP CAL. Мы рекомендуем использовать hello новая модель развертывания диспетчера ресурсов и не принимать во внимание hello классической модели развертывания.

## <a name="step-by-step-process-toodeploy-hello-solution"></a>Пошаговый процесс toodeploy hello решения

Следующая последовательность снимков экрана приветствия показано, как toodeploy S/4HANA в Azure с помощью hello клиентская лицензия SAP. Hello процесс работает hello одинаково для других решений, таких как BW/4HANA.

Hello **решения** странице отображаются некоторые hello доступных решений на основе SAP HANA клиентскую Лицензию в Azure. **SAP S/4HANA 1610 FPS01, устройство Fully-Activated** в среднем ряду hello:

![Решения SAP CAL](./media/cal-s4h/s4h-pic-1c.png)

### <a name="create-an-account-in-hello-sap-cal"></a>Создать учетную запись в hello SAP CAL
1. toosign в toohello SAP CAL для hello первая команда пользователя S SAP или других пользователей, зарегистрированных в SAP. Затем укажите учетную запись SAP клиентских лицензий, используемых устройств toodeploy hello SAP CAL в Azure. В определении hello учетной записи необходимо:

    а. Выберите модель развертывания hello в Azure (диспетчера ресурсов или Классическая версия).

    b. Введите подписку Azure. Учетной записи SAP CAL могут назначаться только tooone подписок. Если вам требуется более чем одной подписке, toocreate требуется другой учетной записи SAP CAL.

    c. Предоставьте разрешение toodeploy hello SAP CAL в вашей подписке Azure.

    > [!NOTE]
    Hello следующие шаги показывают, как учетная запись toocreate CAL SAP для развертывания диспетчера ресурсов. Если уже имеется связанный toohello классической модели развертывания, с учетной записью SAP CAL вы *требуется* toofollow toocreate эти действия учетной записи SAP CAL. Hello новой учетной записи SAP CAL должен toodeploy в модели hello диспетчера ресурсов.

2. Создайте учетную запись SAP CAL. Hello **учетные записи** странице отображаются три варианта для Azure: 

    а. **Microsoft Azure (классические)** является hello классической модели развертывания и больше не является предпочтительным.

    b. **Microsoft Azure** — hello новая модель развертывания диспетчера ресурсов.

    c. **Эксплуатироваться Windows Azure, обслуживаемой 21Vianet** является параметром в Китае, использующий hello классической модели развертывания.

    Выберите toodeploy в модели hello диспетчер ресурсов, **Microsoft Azure**.

    ![Сведения об учетной записи SAP CAL](./media/cal-s4h/s4h-pic-2a.png)

3. Введите hello Azure **идентификатор подписки** , можно найти на hello портал Azure.

   ![Учетные записи CAL SAP](./media/cal-s4h/s4h-pic3c.png)

4. определенные tooauthorize toodeploy SAP CAL hello в hello подписки Azure, щелкните **авторизовать**. После страницы приветствия появляется hello вкладке браузера:

   ![Вход в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic4c.png)

5. Если в списке больше одного пользователя, выберите hello учетной записи Майкрософт, связанного toobe coadministrator hello объекта hello Azure подписку, которую вы выбрали. После страницы приветствия появляется hello вкладке браузера:

   ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-s4h/s4h-pic5a.png)

6. Нажмите кнопку **Принимаю**. При успешном выполнении авторизации hello hello определения учетной записи SAP CAL отображаются снова. Через некоторое время сообщение подтверждает, что процесс авторизации hello была успешной.

7. tooassign hello только что созданный пользователь tooyour учетной записи SAP CAL, введите ваш **идентификатор пользователя** в текстовое поле в правой hello hello и нажмите кнопку **добавить**.

   ![Сопоставление toouser учетной записи](./media/cal-s4h/s4h-pic8a.png)

8. Щелкните свою учетную запись с hello пользователя использовать toosign в toohello SAP CAL tooassociate **проверки**. 
 
9. Щелкните toocreate hello связь между пользователем и учетной записи SAP CAL вновь созданные hello, **создать**.

   ![Сопоставление учетной записи пользователя tooSAP клиентской лицензии](./media/cal-s4h/s4h-pic9b.png)

Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:

- Использование модели развертывания диспетчера ресурсов hello.
- развертывать системы SAP в подписке Azure.

Теперь вы можете запустить toodeploy S/4HANA в подписки пользователя в Azure.

> [!NOTE]
Прежде чем продолжить, проверьте, есть ли у вас квоты ядер Azure для виртуальных машин Azure серии H. В момент hello hello SAP CAL использует toodeploy H серии виртуальных машин Azure некоторые решения на основе SAP HANA hello. Ваша подписка может не иметь квот ядер для серии Н. В этом случае может потребоваться tooget поддержки Azure toocontact Квота ядер менее 16 H-Series.

> [!NOTE]
При развертывании решения на платформе Azure в hello SAP CAL, возможно, которые можно выбрать только один регион Azure. toodeploy в Azure регионах, отличных от hello один предложенными hello SAP CAL, необходимо toopurchase CAL подписки из SAP. Также может потребоваться tooopen сообщение с SAP toohave вашей toodeliver CAL учетная запись включена в Azure регионах, отличных от тех, которые изначально предлагаются hello.

### <a name="deploy-a-solution"></a>Развертывание решения

Давайте развертывание решения из hello **решения** страница hello клиентская лицензия SAP. Hello SAP CAL состоит из двух toodeploy последовательности.

- Базовой последовательности, использующий развернут toobe hello системы одной страницы toodefine
- Расширенная последовательность, которая позволяет выбрать определенные размеры виртуальных машин. 

Показывается здесь toodeployment базовый путь hello.

1. На hello **сведения об учетной записи** страницы, необходимо:

    а. Выберите учетную запись SAP CAL. (Использовать учетную запись, которая является toodeploy, связанные с моделью развертывания диспетчера ресурсов hello).

    b. Введите **имя** экземпляра.

    c. Выберите **регион** Azure. Hello SAP CAL предлагает область. Если требуется другой регион Azure, и у вас нет подписки SAP CAL, вам потребуется подписка tooorder клиентская лицензия с SAP.

    d. Введите главного **пароль** для решения hello 8 или 9 символов. Hello пароль используется для администраторов hello hello различных компонентов.

   ![Базовый режим SAP CAL: создание экземпляра](./media/cal-s4h/s4h-pic10a.png)

2. Нажмите кнопку **создать**, а в окне сообщения hello, которое отображается, нажмите кнопку **ОК**.

   ![Поддерживаемые SAP CAL размеры виртуальных машин](./media/cal-s4h/s4h-pic10b.png)

3. В hello **закрытый ключ** диалоговое окно, нажмите кнопку **хранилища** toostore hello закрытый ключ в hello клиентская лицензия SAP. Защита паролем toouse для hello закрытый ключ, нажмите кнопку **загрузить**. 

   ![Закрытый ключ SAP CAL](./media/cal-s4h/s4h-pic10c.png)

4. Чтение hello SAP CAL **предупреждение** сообщение и нажмите кнопку **ОК**.

   ![Предупреждения SAP CAL](./media/cal-s4h/s4h-pic10d.png)

    Теперь развертывание hello вступает в силу. Через некоторое время в зависимости от размера hello и сложности решения hello (приветствия SAP CAL предоставляет оценку), hello состояние отображается как активные и готов к использованию.

5. виртуальные машины toofind hello, собранные с помощью hello других связанных ресурсов в одной группе ресурсов, перейдите toohello портала Azure: 

   ![Клиентская лицензия SAP объекты, развертываемые в новый портал hello](./media/cal-s4h/sapcaldeplyment_portalview.png)

6. На портале hello SAP CAL, hello состояние отображается как **Active**. tooconnect toohello решение, нажмите кнопку **Connect**. Различные варианты tooconnect toohello различные компоненты развертываются в рамках этого решения.

   ![Экземпляры SAP CAL](./media/cal-s4h/active_solution.png)

7. Прежде чем использовать tooconnect toohello развернут hello параметры системы, нажмите кнопку **руководство по началу работы**. 

   ![Подключение toohello экземпляра](./media/cal-s4h/connect_to_solution.png)

    имена документации Hello hello пользователей для каждого из методов связи hello. пароли Hello для тех пользователей, задаются toohello главный пароль, которые определены в начале процесса развертывания hello hello. В документации hello других более работы пользователей в списке свои пароли, которые можно использовать toosign в toohello развертывания системы. 

    Например если вы используете hello GUI SAP, предварительно установленное на компьютере удаленного рабочего стола Windows hello, hello S/4 системы может выглядеть следующим образом:

   ![SM50 в hello предустановлен SAP GUI](./media/cal-s4h/gui_sm50.png)

    Или, при использовании hello DBACockpit hello экземпляр может выглядеть следующим образом:

   ![SM50 в hello DBACockpit SAP GUI](./media/cal-s4h/dbacockpit.png)

В течение нескольких часов в Azure будет развернуто работоспособное устройство S/4SAP.

Если вы приобрели подписку на SAP CAL, SAP полностью поддерживает развертываниями с помощью hello SAP CAL в Azure. очередь поддержки Hello — BC VCM клиентских лицензий.







