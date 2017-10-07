---
title: "aaaDeploy SAP EHP7 интегрированными средами разработки с пакетом обновления 3 для 6.0 ERP SAP в Azure | Документы Microsoft"
description: "Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure"
services: virtual-machines-windows
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 626c1523-1026-478f-bd8a-22c83b869231
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 09/16/2016
ms.author: hermannd
ms.openlocfilehash: 26d88c7b48a91d35602464c4f89ca7a30502c4b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-sap-ides-ehp7-sp3-for-sap-erp-60-on-azure"></a>Развертывание SAP IDES EHP7 SP3 для SAP ERP 6.0 в Azure
В этой статье описывается как toodeploy SAP интегрированными средами разработки системы с SQL Server и операционной системы Windows hello на Azure через hello SAP облачной устройства библиотеки (SAP CAL) 3.0. снимки экрана приветствия Показать пошаговый процесс hello. Выполните toodeploy другого решения hello одну последовательность шагов.

toostart с hello CAL SAP, последовательно выберите toohello [устройство библиотеки SAP облака](https://cal.sap.com/) веб-сайта. SAP также есть блог о hello новый [устройство библиотеки SAP облака 3.0](http://scn.sap.com/community/cloud-appliance-library/blog/2016/05/27/sap-cloud-appliance-library-30-came-with-a-new-user-experience). 

> [!NOTE]
Кроме как 29 мая 2017 г., можно использовать модель развертывания диспетчера ресурсов Azure hello toohello менее предпочтительным классическое развертывание модели toodeploy hello SAP CAL. Мы рекомендуем использовать hello новая модель развертывания диспетчера ресурсов и не принимать во внимание hello классической модели развертывания.

Если вы создали учетную запись SAP CAL, использующий hello классической модели, *toocreate требуется другой учетной записи SAP CAL*. Эта учетная запись должна tooexclusively развертывания в Azure с помощью модели hello диспетчера ресурсов.

После входа в toohello SAP CAL, первая страница hello обычно содержится руководство toohello **решения** страницы. Hello решения, предлагаемые на hello SAP CAL неуклонно растет, поэтому может понадобиться tooscroll немного toofind hello решение, которое требуется. решение SAP интегрированными средами разработки на основе Windows Hello выделяются, доступен только в Azure показан процесс развертывания hello:

![Решения SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic1.jpg)

### <a name="create-an-account-in-hello-sap-cal"></a>Создать учетную запись в hello SAP CAL
1. toosign в toohello SAP CAL для hello первая команда пользователя S SAP или других пользователей, зарегистрированных в SAP. Затем укажите учетную запись SAP клиентских лицензий, используемых устройств toodeploy hello SAP CAL в Azure. В определении hello учетной записи необходимо:

    а. Выберите модель развертывания hello в Azure (диспетчера ресурсов или Классическая версия).

    b. Введите подписку Azure. Учетной записи SAP CAL могут назначаться только tooone подписок. Если вам требуется более чем одной подписке, toocreate требуется другой учетной записи SAP CAL.
    
    c. Предоставьте разрешение toodeploy hello SAP CAL в вашей подписке Azure.

    > [!NOTE]
    Hello следующие шаги показывают, как учетная запись toocreate CAL SAP для развертывания диспетчера ресурсов. Если уже имеется связанный toohello классической модели развертывания, с учетной записью SAP CAL вы *требуется* toofollow toocreate эти действия учетной записи SAP CAL. Hello новой учетной записи SAP CAL должен toodeploy в модели hello диспетчера ресурсов.

2. toocreate новой клиентской лицензии SAP учетной записи, hello **учетные записи** странице отображаются два варианта для Azure: 

    а. **Microsoft Azure (классические)** является hello классической модели развертывания и больше не является предпочтительным.

    b. **Microsoft Azure** — hello новая модель развертывания диспетчера ресурсов.

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic-2a.PNG)

    Выберите toodeploy в модели hello диспетчер ресурсов, **Microsoft Azure**.

    ![Учетные записи CAL SAP](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

3. Введите hello Azure **идентификатор подписки** , можно найти на hello портал Azure. 

    ![Идентификатор подписки SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic3c.PNG)

4. определенные tooauthorize toodeploy SAP CAL hello в hello подписки Azure, щелкните **авторизовать**. После страницы приветствия появляется hello вкладке браузера:

    ![Вход в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic4c.PNG)

5. Если в списке больше одного пользователя, выберите hello учетной записи Майкрософт, связанного toobe coadministrator hello объекта hello Azure подписку, которую вы выбрали. После страницы приветствия появляется hello вкладке браузера:

    ![Подтверждение входа в облачные службы в Internet Explorer](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic5a.PNG)

6. Нажмите кнопку **Принимаю**. При успешном выполнении авторизации hello hello определения учетной записи SAP CAL отображаются снова. Через некоторое время сообщение подтверждает, что процесс авторизации hello была успешной.

7. tooassign hello только что созданный пользователь tooyour учетной записи SAP CAL, введите ваш **идентификатор пользователя** в текстовое поле в правой hello hello и нажмите кнопку **добавить**. 

    ![Сопоставление toouser учетной записи](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic8a.PNG)

8. Щелкните свою учетную запись с hello пользователя использовать toosign в toohello SAP CAL tooassociate **проверки**. 

9. Щелкните toocreate hello связь между пользователем и учетной записи SAP CAL вновь созданные hello, **создать**.

    ![Ассоциация tooaccount пользователя](./media/cal-ides-erp6-ehp7-sp3-sql/s4h-pic9b.PNG)

Вы успешно создали учетную запись SAP CAL, позволяющую выполнять следующие задачи:

- Использование модели развертывания диспетчера ресурсов hello.
- развертывать системы SAP в подписке Azure.

> [!NOTE]
Перед развертыванием hello SAP интегрированными средами разработки решений на базе Windows и SQL Server, может потребоваться toosign для подписки на SAP CAL. В противном случае решение hello может отображаться как **заблокирована** на страницу обзора hello.

### <a name="deploy-a-solution"></a>Развертывание решения
1. После настройки учетной записи SAP CAL выберите **hello SAP интегрированными средами разработки решений на Windows и SQL Server** решения. Нажмите кнопку **создать экземпляр**и подтвердите hello условия использования и условия. 

2. На hello **основной режим: создать экземпляр** страницы, необходимо:

    а. Введите **имя** экземпляра.

    b. Выберите **регион** Azure. Может потребоваться tooget подписки SAP CAL, предлагаемые в нескольких регионах Azure.

    c.  Введите образец hello **пароль** hello решения, как показано:

    ![Базовый режим SAP CAL: создание экземпляра](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic10a.png)

3. Щелкните **Создать**. Через некоторое время в зависимости от размера hello и сложности решения hello (приветствия SAP CAL предоставляет оценку), hello состояние отображается как активные и готов к использованию: 

    ![Экземпляры SAP CAL](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic12a.png)

4. Группа ресурсов toofind hello и всех объектов, которые были созданы путем hello SAP CAL см. toohello портал Azure. начиная с hello же экземпляра имени, указанному в hello SAP CAL можно найти Hello виртуальную машину.

    ![Объекты группы ресурсов](./media/cal-ides-erp6-ehp7-sp3-sql/ides_resource_group.PNG)

5. На портале hello SAP CAL, перейдите toohello развернуты экземпляры и нажмите кнопку **Connect**. Появится следующая всплывающее окно приветствия: 

    ![Подключение toohello экземпляра](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic14a.PNG)

6. Прежде чем использовать tooconnect toohello развернут hello параметры системы, нажмите кнопку **руководство по началу работы**. имена документации Hello hello пользователей для каждого из методов связи hello. пароли Hello для тех пользователей, задаются toohello главный пароль, которые определены в начале процесса развертывания hello hello. В документации hello других более работы пользователей в списке свои пароли, которые можно использовать toosign в toohello развертывания системы.

    ![Вводная документации по SAP](./media/cal-ides-erp6-ehp7-sp3-sql/ides-pic15.jpg)

Работоспособная система SAP IDES развертывается в Azure в течение нескольких часов.

Если вы приобрели подписку на SAP CAL, SAP полностью поддерживает развертываниями с помощью hello SAP CAL в Azure. очередь поддержки Hello — BC VCM клиентских лицензий.

