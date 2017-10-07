---
title: "aaaHow tooScale приложения в среде службы приложений"
description: "Масштабирование приложения в среде службы приложений"
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: jimbe
ms.assetid: 78eb1e49-4fcd-49e7-b3c7-f1906f0f22e3
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/17/2016
ms.author: ccompy
ms.openlocfilehash: 08916eac056c46bf8cb6edffbf96285317b32062
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="scaling-apps-in-an-app-service-environment"></a>Масштабирование приложений в среде службы приложений
В службе приложений Azure hello существует обычно три вещи, которые можно масштабировать.

* план ценообразования;
* размер рабочей роли; 
* количество экземпляров.

В ASE нет нет необходимости tooselect или измените hello ценовой план.  С точки зрения возможностей среда уже находится на максимальном ценовом уровне.  

Размеры tooworker уважением ASE Здравствуйте, администратор можно назначить размер hello hello вычислительных ресурсов toobe для каждого рабочего пула.  Это значит, что при необходимости вы можете иметь пул исполнителей 1 с вычислительными ресурсами P4 и пул исполнителей 2 с вычислительными ресурсами P1.  У пользователя нет toobe в порядке размер.  Сведения о размерах hello и их ценовую см. в документе hello [цены на службу приложений Azure][AppServicePricing].  Это оставляет hello масштабирования для веб-приложений и планы службы приложений в toobe среды службы приложений:

* выбор пула исполнителей;
* количество экземпляров.

Изменение одного из осуществляется посредством hello соответствующие показано планы службы приложений, размещенных на ASE пользовательского интерфейса.  

![][1]

Не удается провести вертикальное масштабирование вашей ASP за пределами hello количество доступных вычислительных ресурсов в пуле рабочих процессов hello, ваши страницы ASP.  Если требуются вычислительные ресурсы, в этом пуле рабочего процесса необходимо tooget tooadd администратор вашей ASE их.  Для сведения вокруг повторной настройки вашей ASE прочитать здесь сведения hello: [как tooConfigure среду службы приложений][HowtoConfigureASE].  Вы также можете tootake преимуществами hello ASE функции автомасштабирования tooadd емкости на основе расписания или метрик.  см. Дополнительные сведения о настройке автоматического масштабирования для самой среде hello ASE tooget [как tooconfigure автоматического масштабирования для среды службы приложений][ASEAutoscale].

Можно создать несколько приложение с помощью вычислительных ресурсов из разных рабочих пулов планов обслуживания, или можно использовать hello же пуле рабочего процесса.  Для примера, при наличии (10) доступных вычислительных ресурсов в рабочей группы 1, можно выбрать toocreate одно приложение службы плана, с помощью (6) вычислительные ресурсы и второе приложение службы плана, использует вычислительные ресурсы, (4).

### <a name="scaling-hello-number-of-instances"></a>Масштабирование hello число экземпляров
При первом создании веб-приложения в среде службы приложений запускается один его экземпляр.  После этого можно масштабирования tooprovide экземпляров tooadditional дополнительные вычислительные ресурсы для приложения.   

Если среда ASE располагает достаточными ресурсами, сделать это будет очень просто.  Переходе tooyour план служб приложений, содержащий узлы hello tooscale вверх и выберите шкалы.  Откроется пользовательский Интерфейс, в котором можно вручную задать hello шкалы для вашего ASP или Настройка правил автоматического масштабирования для вашего ASP hello.  приложение просто набор масштабирования toomanually ***масштабирования по*** слишком***число экземпляров, вводимое вручную***.  Здесь перетащите hello ползунок toohello требуемого количества или введите его в hello поле Далее toohello ползунок.  

![][2] 

правила автомасштабирования Hello ASP в работе ASE hello таким же, как обычно.  Можно выбрать ***Процент использования ЦП*** для параметра ***Масштабировать по*** и создать правила автоматического масштабирования для ASP с учетом процента использования ЦП. Кроме того, можно создать более сложные правила, воспользовавшись ***правилами расписания и производительности***.  toosee более полных сведений о настройке автомасштабирования hello подачи здесь [масштабирование приложения в службе приложений Azure][AppScale]. 

### <a name="worker-pool-selection"></a>выбор пула исполнителей;
Как отмечалось ранее, Выбор пула рабочих hello осуществляется из hello ASP пользовательского интерфейса.  Откройте колонку hello для hello ASP tooscale и выберите рабочего пула.  Вы увидите все hello рабочих пулов, настроенных в среде службы приложений.  Если у вас есть только один рабочий процесс пула затем вы увидите только один пул hello в списке.  toochange какой рабочий пул вашей ASP, нужно просто выбрать, требуется, чтобы ваш план службы приложений toomove в пуле рабочих процессов hello.  

![][3]

Перед переходом к ASP из пула tooanother один рабочий процесс очень важных toomake в том, что имеется достаточно мощности для вашего ASP.  В списке hello рабочих пулов не только указывается имя пула рабочих hello, но можно также просмотреть, сколько рабочих процессов доступны в этом пуле рабочего процесса.  Убедитесь, что отсутствуют доступные toocontain достаточное количество экземпляров плана службы приложений.  Если требуется больше вычислительных ресурсов hello рабочего пула нужно toomove извлекаемого, затем администратор вашей ASE tooadd их.  

> [!NOTE]
> При перемещении ASP из пула один рабочий процесс вызовет холодного запускает приложения hello в ASP.  Это может привести к toorun запросы медленно как приложение холодного, начатый hello новые вычислительные ресурсы.  Hello холодный запуск можно избежать с помощью hello [прогрев возможностей приложения] [ AppWarmup] в службе приложений Azure.  модуль инициализации приложения Hello, описанное в статье hello также работает для холодного запуска, так как процесс инициализации hello также вызывается, когда приложения — холодного запуска на новые вычислительные ресурсы. 
> 
> 

## <a name="getting-started"></a>Приступая к работе
tooget к работе с среды службы приложения, в разделе [как tooCreate среды службы приложений][HowtoCreateASE]

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

<!--Image references-->
[1]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-aspblade.png
[2]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-manualscale.png
[3]: ./media/app-service-web-scale-a-web-app-in-an-app-service-environment/aseappscale-sizescale.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ScaleWebapp]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[HowtoCreateASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-an-app-service-environment/
[HowtoConfigureASE]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[CreateWebappinASE]: http://azure.microsoft.com/documentation/articles/app-service-web-how-to-create-a-web-app-in-an-ase/
[Appserviceplans]: http://azure.microsoft.com/documentation/articles/azure-web-sites-web-hosting-plans-in-depth-overview/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[AppScale]: http://azure.microsoft.com/documentation/articles/web-sites-scale/
[AppWarmup]: http://ruslany.net/2015/09/how-to-warm-up-azure-web-app-during-deployment-slots-swap/
