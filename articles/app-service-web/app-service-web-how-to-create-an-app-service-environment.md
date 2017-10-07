---
title: "aaaHow tooCreate v1 среды службы приложений"
description: "Описание процесса создания среды службы приложений версии 1."
services: app-service
documentationcenter: 
author: ccompy
manager: stefsch
editor: 
ms.assetid: 81bd32cf-7ae5-454b-a0d2-23b57b51af47
ms.service: app-service
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/11/2017
ms.author: ccompy
ms.openlocfilehash: 95feb33854eee5bac02fa68b066e2fc10eb3fede
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-an-app-service-environment-v1"></a>Как tooCreate v1 среды службы приложений 

> [!NOTE]
> Эта статья является о hello v1 среды службы приложений. Имеется более новая версия hello среды службы приложений, удобнее toouse и выполняется на более мощный инфраструктуры. Дополнительные сведения о новой версии hello начинаться с hello toolearn [toohello введение среды службы приложений](../app-service/app-service-environment/intro.md).
> 

### <a name="overview"></a>Обзор
Hello среды службы приложений (ASE) — это параметр службы Premium службы приложения Azure, которая обеспечивает возможность расширенной настройки, недоступные в hello отметки нескольких клиентов. функция ASE Hello фактически развертывает hello службе приложений Azure в виртуальной сети клиента. toogain предлагаемых лучшего понимания возможностей hello по среды службы приложения чтения hello [возможности среды службы приложений] [ WhatisASE] документации.

### <a name="before-you-create-your-ase"></a>Перед созданием среды службы приложений
Это важные toobe учитывать hello вещей, которые нельзя изменить. Ниже перечислены параметры среды ASE, которые нельзя изменить после ее создания.

* Расположение
* Подписка
* Группа ресурсов
* Используемая виртуальная сеть
* Используемая подсеть 
* Размер подсети

При выбора виртуальной сети и указании подсети, убедитесь, что он является достаточно большим tooaccomodate увеличение в будущем. 

### <a name="creating-an-app-service-environment-v1"></a>Создание среды службы приложений версии 1
toocreate v1 среды службы приложений, необходимо toosearch hello Azure Marketplace для ***v1 среды службы приложений***, или через Создать -> Web + Mobile -> среды службы приложений. toocreate ASEv1:

1. Укажите имя вашей ASE hello. Hello имя, указанное для hello ASE будет использоваться для приложения hello, созданные в hello ASE. Если имя hello ASE-appsvcenvdemo будет имя поддомена hello. *appsvcenvdemo.p.azurewebsites.net*. Если создать веб-приложение с именем *mytestapp*, то к нему можно будет обращаться по адресу *mytestapp.appsvcenvdemo.p.azurewebsites.net*. Нельзя использовать пустое пространство в имя вашей ASE hello. При использовании прописных букв в имени hello hello доменное имя будет hello версии общее нижнем регистре с тем же именем. Если используется внутренний балансировщик нагрузки, то имя среды ASE не используется в поддомене, а указывается явно во время создания среды ASE.
   
    ![][1]
2. Выберите свою подписку. Hello подписку для вашего ASE также является hello один, будет создана со всеми приложениями, ASE. Невозможно разместить среду ASE в виртуальной сети, которая находится в другой подписке.
3. Выберите или укажите новую группу ресурсов. группы ресурсов Hello, используемой для вашего ASE должен быть hello те же данные, используемые для виртуальной сети. Если выбрать существующую виртуальную сеть, а затем hello выбранную группу ресурсов для вашего ASE будет обновленные tooreflect, виртуальной сети.
   
    ![][2]
4. Выберите виртуальную сеть и расположение. Можно выбрать toocreate новую виртуальную сеть или выбрать существующую виртуальную сеть. В случае выбора создания виртуальной сети можно указать ее имя и расположение. Hello новой виртуальной сети будут иметь 192.168.250.0/23 диапазона адресов hello и подсеть с именем **по умолчанию** , определенный как 192.168.250.0/24. Можно также просто выбрать уже существующую классическую виртуальную сеть или виртуальную сеть Resource Manager. Hello Выбор типа виртуальных IP-адресов определяет, если ваш ASE напрямую доступны из hello Интернета (внешний) или если он использует внутренние подсистемы балансировки нагрузки (ILB). Дополнительные сведения об их прочитать toolearn [использование внутренней подсистемы балансировки нагрузки с среды службы приложений][ILBASE]. Если выбран тип виртуального IP-адреса внешних объектов можно выбрать, сколько внешней системы hello адресов IP для целей IPSSL создается с. Если выбрать для внутреннего использования должны toospecify hello поддомен, который будет использовать ваш ASE. Среды ASE можно развертывать в виртуальных сетях, использующих *либо* диапазоны общедоступных адресов, *либо* адресные пространства RFC1918 (т. е. частные адреса). В порядке toouse с диапазоном общедоступный адрес виртуальной сети нужно будет toocreate hello виртуальной сети заранее. При выборе существующей виртуальной сети во время создания ASE потребуется toocreate новую подсеть. **Нельзя использовать предварительно созданной подсети hello портала. Создать среду ASE с уже существующей подсетью можно с помощью шаблона Resource Manager.** здесь сведения hello использовать toocreate ASE из шаблона [создание среды службы приложений на основе шаблона] [ ILBAseTemplate] и здесь [создание среды службы приложений ILB из шаблона] [ASEfromTemplate].

### <a name="details"></a>Сведения
Среда ASE создается с двумя внешними интерфейсами и двумя рабочими ролями. Hello внешних интерфейсов выступать в качестве конечных точек HTTP/HTTPS hello и отправлять трафик toohello работников, которые являются hello ролями, в которых размещены приложения. Можно настроить количество hello после создания ASE и даже устанавливать правила автоматического масштабирования для этих пулов ресурсов. Подробнее вокруг ручное масштабирование, управление и наблюдение за среды службы приложений здесь: [как tooconfigure среды службы приложений][ASEConfig] 

В подсети hello, используемые hello ASE может существовать ASE hello один. Hello подсети не может использоваться для любых данных, кроме hello ASE

### <a name="after-app-service-environment-v1-creation"></a>После создания среды службы приложений версии 1
После создания ASE можно настроить такие параметры:

* Количество внешних интерфейсов (минимальное: 2)
* Количество исполнителей (минимальное: 2)
* Количество IP-адресов, доступных для SSL на основе IP 
* Вычисления размера ресурсов, используемых hello внешних интерфейсов или рабочих процессов (минимальный размер внешнего интерфейса — P2)

Существуют дополнительные сведения о ручной масштабирования, управления и наблюдения за среды службы приложения здесь: [как tooconfigure среды службы приложений][ASEConfig] 

Сведения об автоматическом масштабировании имеется руководство по здесь: [как tooconfigure автоматического масштабирования для среды службы приложений][ASEAutoscale]

Существуют дополнительные зависимости, которые не доступны для настройки, такие как hello базы данных и хранилища. Это может быть обработано Azure и входящие в состав системы hello. Hello системы хранения поддерживает копирование too500 ГБ для hello всей среды службы приложений и при необходимости по масштабу hello hello системы базы данных hello регулируется Azure.

## <a name="getting-started"></a>Приступая к работе
Все статьи и как-для пользователя для среды службы приложений теперь доступны в hello [файл README для среды службы приложения](../app-service/app-service-app-service-environments-readme.md).

tooget к работе с v1 среды службы приложений. в разделе [toohello введение v1 среды службы приложений][WhatisASE]

Дополнительные сведения о платформе hello службе приложений Azure см. в разделе [службе приложений Azure][AzureAppService].

[!INCLUDE [app-service-web-whats-changed](../../includes/app-service-web-whats-changed.md)]

[!INCLUDE [app-service-web-try-app-service](../../includes/app-service-web-try-app-service.md)]

<!--Image references-->
[1]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-basecreateblade.png
[2]: ./media/app-service-web-how-to-create-an-app-service-environment/asecreate-vnetcreation.png

<!--Links-->
[WhatisASE]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-intro/
[ASEConfig]: http://azure.microsoft.com/documentation/articles/app-service-web-configure-an-app-service-environment/
[AppServicePricing]: http://azure.microsoft.com/pricing/details/app-service/ 
[AzureAppService]: http://azure.microsoft.com/documentation/articles/app-service-value-prop-what-is/ 
[ASEAutoscale]: http://azure.microsoft.com/documentation/articles/app-service-environment-auto-scale/
[ILBASE]: http://azure.microsoft.com/documentation/articles/app-service-environment-with-internal-load-balancer/
[ILBAseTemplate]: http://azure.microsoft.com/documentation/templates/201-web-app-ase-create/
[ASEfromTemplate]: http://azure.microsoft.com/documentation/articles/app-service-app-service-environment-create-ilb-ase-resourcemanager/
