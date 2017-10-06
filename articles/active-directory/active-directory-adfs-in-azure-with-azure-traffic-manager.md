---
title: "aaaHigh доступности географической между AD FS развертывания в Azure с помощью диспетчера трафика Azure | Документы Microsoft"
description: "В этом документе вы узнаете, как toodeploy AD FS в Azure для непрерывной работы."
keywords: "Службы федерации Active Directory с Azure traffic manager, adfs с диспетчером трафика Azure, географические, multi центра обработки данных, географической центрах обработки данных, несколькими центрами обработки данных географической, развертывание AD FS в azure, развертывание служб федерации Active Directory azure, azure служб федерации Active Directory, azure ad fs, развертывание служб федерации Active Directory, развертывание служб федерации Active Directory adfs в azure, развертывание служб федерации Active Directory в azure, развертывание AD FS в azure, azure служб федерации Active Directory, введение tooAD федерации Active Directory, Azure, AD FS в Azure iaas, ADFS, переместите tooazure служб федерации Active Directory"
services: active-directory
documentationcenter: 
author: anandyadavmsft
manager: femila
editor: 
ms.assetid: a14bc870-9fad-45ed-acd5-a90ccd432e54
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 09/01/2016
ms.author: anandy;billmath
ms.openlocfilehash: c5838d749cdc5c8aabbe62b255d568525da747ab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-cross-geographic-ad-fs-deployment-in-azure-with-azure-traffic-manager"></a>Развертывание AD FS высокого уровня доступности в нескольких регионах Azure с помощью диспетчера трафика Azure
[Развертывание AD FS в Azure](active-directory-aadconnect-azure-adfs.md) предоставляет пошаговые инструкции как toohow развертыванием простой инфраструктуры AD FS для вашей организации в Azure. Эта статья содержит следующие шаги hello toocreate кросс географический развертывания AD FS в Azure с помощью [диспетчера трафика Azure](../traffic-manager/traffic-manager-overview.md). Диспетчер трафика Azure позволяет создать географически распределенный высокого уровня доступности и высокой производительности инфраструктуры AD FS для вашей организации, делая использование диапазона различных доступных toosuit требуется от инфраструктуры hello методов маршрутизации.

Инфраструктура AD FS высокого уровня доступности, развернутая в нескольких регионах, дает ряд преимуществ.

* **Устранение узких мест:** с отказоустойчивости диспетчера трафика Azure, даже в том случае, если один из центров данных hello в части земной шар hello выходит из строя можно добиться высокой доступности инфраструктуры AD FS
* **Улучшенная производительность:** можно использовать hello предложенные развертывания в этой статье tooprovide инфраструктуры AD FS высокой производительности, который поможет пользователям быстрее проверки подлинности. 

## <a name="design-principles"></a>Принципы проектирования
![Общая схема](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/blockdiagram.png)

Основные принципы Hello будет осуществлять такие же, как указано в принципы разработки в статье hello развертывания AD FS в Azure. Hello приведенной выше схеме показаны простого расширения hello базовое развертывание tooanother географического региона. Ниже приведены некоторые точки tooconsider при расширении географический регион toonew развертывания

* **Виртуальная сеть:** следует создать новую виртуальную сеть в географическом регионе hello требуется инфраструктура toodeploy дополнительных AD FS. В приведенной выше схеме hello появятся Geo1 виртуальной сети и виртуальной сети Geo2 как hello две виртуальные сети в каждом географическом регионе.
* **Контроллеры домена и серверы AD FS в новой виртуальной сети географических:** toodeploy контроллеры домена в новый географический регион hello рекомендуется, чтобы серверы hello AD FS в новой области hello не имеют toocontact контроллера домена в другой момент Размещение сети toocomplete проверку подлинности и тем самым улучшение производительности hello.
* **Учетные записи хранения:** учетные записи хранения строго привязаны к региону. Поскольку вы будете развертывать машин в новый географической области, будет иметь toocreate новых учетных записей хранения toobe, используемой в регионе hello.  
* **Группы безопасности сети:** как и учетные записи хранения, группы безопасности сети нельзя использовать в другом географическом регионе. Таким образом необходимо будет toocreate новый сетевой безопасности групп аналогичные toothose в hello первый географическом регионе для подсети INT и DMZ в hello новый географическом регионе.
* **Метки DNS для общедоступных IP-адресов:** диспетчера трафика Azure может ссылаться tooendpoints только через DNS метки. Таким образом вы, требуется toocreate метки DNS для общедоступных IP-адресов hello внешней подсистемы балансировки нагрузки.
* **Диспетчер трафика Azure:** диспетчера трафика Microsoft Azure позволяет распространения hello toocontrol пользователя трафика tooyour конечных точек службы, работающих в различных центрах обработки данных вокруг Здравствуй, мир. Диспетчер трафика Azure работает на уровне DNS hello. Он использует DNS ответов toodirect конечного пользователя трафика распределенных tooglobally конечные точки. Затем клиенты напрямую подключаться toothose конечных точек. С различными параметрами производительности, взвешенное и приоритет маршрутизации можно легко hello маршрутизации вариант лучше всего подходит для вашей организации. 
* **V-net tooV net подключение между двумя областями:** toohave подключения между виртуальными сетями hello не требуется сам. Поскольку каждая виртуальная сеть имеет доступ toodomain контроллеры и установлен сервер AD FS и WAP само по себе, их можно использовать без все подключения между виртуальными сетями hello в разных регионах. 

## <a name="steps-toointegrate-azure-traffic-manager"></a>Toointegrate действия диспетчера трафика Azure
### <a name="deploy-ad-fs-in-hello-new-geographical-region"></a>Развертывание AD FS в новой географический регион hello
Выполните шаги hello и правила в [развертывания AD FS в Azure](active-directory-aadconnect-azure-adfs.md) toodeploy hello же топологии в hello новый географическом регионе.

### <a name="dns-labels-for-public-ip-addresses-of-hello-internet-facing-public-load-balancers"></a>Метки DNS для общедоступных IP-адресов из hello с выходом в Интернет (public) подсистемы балансировки нагрузки
Как упоминалось выше, hello диспетчера трафика Azure может ссылаться только метки tooDNS как конечные точки, и поэтому важно toocreate метки DNS для общедоступных IP-адресов hello внешней подсистемы балансировки нагрузки. Ниже снимке экрана показано, как настроить метку для hello общедоступный IP-адрес DNS. 

![DNS-имя](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfabstsdnslabel.png)

### <a name="deploying-azure-traffic-manager"></a>Развертывание диспетчера трафика Azure
Выполните действия hello ниже toocreate профиль диспетчера трафика. Дополнительные сведения можно также ссылаться слишком[управления профилем диспетчера трафика Azure](../traffic-manager/traffic-manager-manage-profiles.md).

1. **Создайте профиль диспетчера трафика** и присвойте этому профилю уникальное имя. Это имя профиля hello является частью DNS-имя hello и выступает в качестве префикса для метку имени домена диспетчера трафика hello. Имя Hello / добавлен префикс too.trafficmanager.net toocreate метка DNS для диспетчера трафика. Hello снимке экрана показано диспетчера трафика hello устанавливается как mysts и полученный метка DNS будет mysts.trafficmanager.net префикс DNS. 
   
    ![Создание профиля диспетчера трафика](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/trafficmanager01.png)
2. **Метод маршрутизации трафика:** в диспетчере трафика доступны три метода маршрутизации трафика.
   
   * Приоритет 
   * Производительность
   * Взвешенный
     
     **Производительность** hello рекомендуется использовать параметр tooachieve быстродействующего AD FS инфраструктуры. Но вы можете выбрать любой метод маршрутизации, который соответствует целям вашего развертывания. функции Hello AD FS не подвержен влиянию hello маршрутизации флажок. Дополнительные сведения см. в статье [Методы маршрутизации трафика диспетчером трафика](../traffic-manager/traffic-manager-routing-methods.md). В hello пример снимка экрана выше вы увидите hello **производительности** выбранного метода.
3. **Настройка конечных точек:** странице диспетчера трафика hello, щелкните конечных точек и выберите пункт Добавить. После этого откроется добавить конечную точку страницы аналогичные toohello снимке
   
   ![Настройка конечных точек](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/eastfsendpoint.png)
   
   Для hello различных входных данных выполните рекомендации hello ниже.
   
   **Тип:** выберите Azure конечной точки, как мы указывает tooan Azure общедоступный IP-адрес.
   
   **Имя:** создать имя, что требуется tooassociate с конечной точкой hello. Это не hello DNS-имя и никак не влияет на DNS-записей.
   
   **Целевой тип ресурса:** выберите общедоступный IP-адрес как свойство toothis значение hello. 
   
   **Целевой ресурс:** это даст вам возможность toochoose с разным меткам DNS hello имеются доступные в вашей подписке. Выберите hello, соответствующая конечная точка toohello, которую вы настраиваете метка DNS.
   
   Добавьте конечную точку для каждого географического региона нужные tooroute трафик hello диспетчера трафика Azure.
   Дополнительные сведения и подробные инструкции о том, как tooadd / настройки конечных точек диспетчера трафика см. в слишком[Добавление, отключение, включение или удаление конечных точек](../traffic-manager/traffic-manager-endpoints.md)
4. **Настройка проверки:** странице диспетчера трафика hello, щелкните в конфигурации. На странице конфигурации hello понадобится tooprobe параметры монитора toochange hello в HTTP-порт 80 и /adfs/probe относительный путь
   
    ![Настройка пробы](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/mystsconfig.png) 
   
   > [!NOTE]
   > **Убедитесь, что состояние hello hello конечных точек сети после завершения настройки hello**. Если все конечные точки находятся в состоянии «деградации», диспетчер трафика Azure будет выполнять наиболее попытки hello трафика tooroute при условии, что неверный диагностики hello и все конечные точки должны быть доступны.
   > 
   > 
5. **Изменения записей DNS для диспетчера трафика Azure:** вашей службы федерации должно представлять собой имя DNS диспетчера трафика Azure toohello CNAME. Создайте запись CNAME в hello общедоступные записи DNS, чтобы кто пытается службы федерации hello tooreach фактически достиг hello диспетчера трафика Azure.
   
    Например, toopoint hello федерации fs.fabidentity.com toohello диспетчера трафика, потребовалось бы tooupdate вашей hello toobe записей ресурсов DNS следующие:
   
    <code>fs.fabidentity.com IN CNAME mysts.trafficmanager.net</code>

## <a name="test-hello-routing-and-ad-fs-sign-in"></a>Тестирование маршрутизации hello и входа в AD FS
### <a name="routing-test"></a>Проверка маршрутизации
Очень базовое тестирование маршрутизации hello бы tootry ping hello федерации с компьютера в каждом географическом регионе DNS-имя. В зависимости от метода маршрутизации hello выбран будут отражены в отображения ping hello hello конечной точки, которую он фактически выполняет проверку связи. Например если вы выбрали hello производительности маршрутизации, затем конечная точка hello ближайшая toohello области клиента hello истекает. Ниже приведен снимок hello два запросы проверки связи от двух разных регионах клиентских компьютеров: EastAsia области и на Западе США. 

![Проверка маршрутизации](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/pingtest.png)

### <a name="ad-fs-sign-in-test"></a>Проверка входа в AD FS
tootest простым способом Hello AD FS можно с помощью страницы IdpInitiatedSignon.aspx hello. В порядке toobe может toodo, что это требуется tooenable hello IdpInitiatedSignOn свойств hello AD FS. Выполните действия hello ниже tooverify вашей установки AD FS

1. Запуск hello ниже на сервере hello AD FS с помощью PowerShell, tooset его tooenabled. 
   Set-AdfsProperties -EnableIdPInitiatedSignonPage $true.
2. С любого внешнего компьютера перейдите по адресу https://<yourfederationservicedns>/adfs/ls/IdpInitiatedSignon.aspx
3. Должна отобразиться страница приветствия AD FS, аналогичные показанным ниже:
   
    ![Тестирование ADFS — запрос проверки подлинности](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest1.png)
   
    Если вход будет выполнен успешно, отобразится сообщение об успешном выполнении, как показано ниже.
   
    ![Тестирование ADFS — успешная проверка подлинности](./media/active-directory-adfs-in-azure-with-azure-traffic-manager/adfstest2.png)

## <a name="related-links"></a>Связанные ссылки
* [Развертывание AD FS в Azure](active-directory-aadconnect-azure-adfs.md)
* [Microsoft Azure Traffic Manager](../traffic-manager/traffic-manager-overview.md)
* [Методы маршрутизации трафика средствами диспетчера трафика](../traffic-manager/traffic-manager-routing-methods.md)

## <a name="next-steps"></a>Дальнейшие действия
* [Управление профилем диспетчера трафика Azure](../traffic-manager/traffic-manager-manage-profiles.md)
* [Добавление, отключение, включение и удаление конечных точек](../traffic-manager/traffic-manager-endpoints.md) 

