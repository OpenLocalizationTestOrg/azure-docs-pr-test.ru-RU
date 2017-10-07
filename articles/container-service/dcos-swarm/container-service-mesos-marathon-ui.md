---
title: "aaaManage Azure DC/OS кластера с пользовательским Интерфейсом Marathon | Документы Microsoft"
description: "Развертывание службы кластеров контейнеры tooan контейнера службы Azure с помощью hello Marathon пользовательского веб-интерфейса."
services: container-service
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: acs, azure-container-service
keywords: "Docker, контейнеры, микрослужбы, Mesos, Azure"
ms.service: container-service
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/04/2017
ms.author: danlep
ms.custom: mvc
ms.openlocfilehash: a90180e1b4763e6d2ddfa699ed4b7269f209f728
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="manage-an-azure-container-service-dcos-cluster-through-hello-marathon-web-ui"></a>Управление контейнера службы Azure DC/OS кластера с помощью hello Marathon пользовательского веб-интерфейса
Контроллер домена/OS предоставляет среду для развертывания и масштабирования кластерных рабочих нагрузок сталкиваясь аппаратным обеспечением hello. На базе DC/OS работает платформа, которая управляет планированием и выполнением вычислительных рабочих нагрузок.

Хотя платформы доступны для многих распространенных рабочих нагрузок, в этом документе описывается, как tooget запущена развертывания контейнеров с Marathon. 


## <a name="prerequisites"></a>Предварительные требования
Для выполнения этих примеров вам потребуется кластер DC/OS, настроенный в службе контейнеров Azure. Необходимо также кластера toothis toohave возможности удаленного подключения. Дополнительные сведения об этих элементах см. следующие статьи hello:

* [Развертывание кластера службы контейнеров Azure](container-service-deployment.md)
* [Подключите кластер tooan контейнера службы Azure](../container-service-connect.md)

> [!NOTE]
> В этой статье предполагается, что toohello DC/OS кластера туннелирования через локальный порт 80.
>

## <a name="explore-hello-dcos-ui"></a>Просмотр hello DC/OS пользовательского интерфейса
Secure Shell (SSH) туннелю [установить](../container-service-connect.md), Обзор toohttp://localhost/. Это загружает hello DC/OS пользовательского веб-интерфейса и отображает сведения о кластере hello, например используемых ресурсов, агенты active и работу служб.

![Пользовательский интерфейс DC/OS](./media/container-service-mesos-marathon-ui/dcos2.png)

## <a name="explore-hello-marathon-ui"></a>Просмотр hello Marathon пользовательского интерфейса
Здравствуйте, toosee Marathon пользовательского интерфейса, toohttp://localhost/marathon обзора. На этом экране можно запустить новый контейнер или другое приложение hello контейнера службы Azure DC/OS кластера. Здесь вы также можете просмотреть информацию о работе контейнеров и приложений.  

![Пользовательский интерфейс Marathon](./media/container-service-mesos-marathon-ui/dcos3.png)

## <a name="deploy-a-docker-formatted-container"></a>Развертывание контейнера формата Docker
Щелкните новый контейнер с помощью Marathon, toodeploy **Создание приложения**и введите следующую информацию в вкладок формы hello hello:

| Поле | Значение |
| --- | --- |
| ИД |nginx |
| Память | 32 |
| Образ — |nginx |
| Сеть |Bridged (Мостовая) |
| Host Port (Порт узла) |80 |
| Протокол |TCP |

![Пользовательский интерфейс нового приложения: вкладка "Общие"](./media/container-service-mesos-marathon-ui/dcos4.png)

![Пользовательский интерфейс нового приложения: контейнер Docker](./media/container-service-mesos-marathon-ui/dcos5.png)

![Пользовательский интерфейс нового приложения: обнаружение служб и портов](./media/container-service-mesos-marathon-ui/dcos6.png)

Если требуется порт toostatically карты hello порт контейнера tooa hello агента необходимо toouse режим JSON. toodo таким образом, переключение мастер новое приложение hello слишком**JSON режим** с помощью переключателя hello. Затем введите следующий параметр в разделе hello hello `portMappings` раздел определения приложения hello. В этом примере привязывает портом 80 контейнера hello tooport 80 hello DC/OS агента. Когда изменение будет внесено, мастер можно перевести в другой режим.

```none
"hostPort": 80,
```

![Пользовательский интерфейс нового приложения: пример порта 80](./media/container-service-mesos-marathon-ui/dcos13.png)

Проверку работоспособности tooenable следует задать путь на hello **работоспособности проверяет** вкладки.

![Пользовательский интерфейс "Новое приложение", вкладка "Проверки работоспособности"](./media/container-service-mesos-marathon-ui/dcos_healthcheck.png)

с набором агентов частных и общедоступных развернут кластер DC/OS Hello. Для hello кластера toobe может tooaccess приложений из Интернета hello необходимо toodeploy приложения hello tooa открытый агента. toodo таким образом, выберите hello **необязательно** вкладке Мастер новое приложение hello и введите **slave_public** для hello **принят ролей ресурса**.

Затем щелкните **Create Application** (Создать приложение).

![Пользовательский интерфейс нового приложения: параметры общедоступного агента](./media/container-service-mesos-marathon-ui/dcos14.png)

На главной странице Marathon hello можно просмотреть состояние развертывания hello для контейнера hello. Сначала отобразится состояние **Deploying** (Развертывание). После успешного развертывания hello изменения состояния слишком**под управлением**.

![Пользовательский интерфейс главной страницы Marathon: состояние развертывания контейнера](./media/container-service-mesos-marathon-ui/dcos7.png)

При переходе назад toohello DC/OS пользовательского веб-интерфейса (http://localhost/), вы видите, что задачи (в данном случае контейнер Docker в формате) работает на кластере DC/OS hello.

![Контроллер домена/OS веб-Интерфейс — задачи, выполняемой в кластере hello](./media/container-service-mesos-marathon-ui/dcos8.png)

узел кластера hello toosee, hello задача выполняется на приветствия щелкните **узлы** вкладки.

![Пользовательский веб-интерфейс DC/OS: узел кластера, на котором выполняется задача](./media/container-service-mesos-marathon-ui/dcos9.png)

## <a name="reach-hello-container"></a>Достижения контейнера hello

В этом примере hello приложение выполняется на узле открытого агента. Достичь приложение hello из hello Интернет путем просмотра агента toohello полное доменное имя кластера hello: `http://[DNSPREFIX]agents.[REGION].cloudapp.azure.com`, где:

* **DNSPREFIX** — префикс DNS hello, указанный при развертывании кластера hello.
* **ОБЛАСТЬ** — hello область, в которой находится в группе ресурсов.

    ![Доступ к Nginx из Интернета](./media/container-service-mesos-marathon-ui/nginx.png)


## <a name="next-steps"></a>Дальнейшие действия
* [Работа с контроллера домена/OS и hello Marathon API](container-service-mesos-marathon-rest.md)

* Близкое знакомство с hello контейнера службы Azure с Mesos

    > [!VIDEO https://channel9.msdn.com/Events/Microsoft-Azure/AzureCon-2015/ACON203/player]
    > 
