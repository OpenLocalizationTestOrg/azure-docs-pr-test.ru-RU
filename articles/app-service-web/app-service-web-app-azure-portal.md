---
title: "aaaReference для перемещения по hello портал Azure"
description: "Дополнительные сведения для веб-службы приложения hello разных пользовательских интерфейсов между hello Azure портал и портал управления hello"
services: app-service
documentationcenter: 
author: jaime-espinosa
manager: erikre
editor: jimbe
ms.assetid: 0cc6a3cc-bd89-4a96-9177-d25f6fb737bb
ms.service: app-service
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/26/2016
ms.author: jaime-espinosa
ms.openlocfilehash: dcf7c1fc17f9a0c31005ad0f2fd53723d2966058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reference-for-navigating-hello-azure-portal"></a>Ссылки для навигации по hello портал Azure
Веб-сайты Azure теперь называются [Веб-приложения службы приложений](http://go.microsoft.com/fwlink/?LinkId=529714). Идет обновление всех нашей документации tooreflect это имя изменений и tooprovide инструкции для hello портала Azure. До завершения этого процесса можно использовать в этом документе как руководство по работе с веб-приложений в hello портал Azure.

[!INCLUDE [app-service-web-to-api-and-mobile](../../includes/app-service-web-to-api-and-mobile.md)]

## <a name="hello-future-of-hello-azure-classic-portal"></a>будущее Hello hello классический портал Azure
Хотя можно заметить изменения на hello классический портал Azure для поставщиков hello, этот портал находится в процесс hello, заменяемое hello портала Azure. Как hello классического портала постепенно вытесняется, фокус hello для разработки новых приложений сдвиг toohello портала Azure. Всех будущих новых функций для веб-приложений будет иметь hello портала Azure. Начните использовать преимущества tootake портала Azure hello hello новейшим и лучшим у toooffer веб-приложений.

## <a name="layout-differences-between-hello-azure-classic-portal-and-azure-portal"></a>Макет различия между hello классический портал Azure и портала Azure
В классическом портале hello, все hello Azure hello левой стороны здесь перечислены услуги. Навигация в классическом портале hello следует элемент древовидной структуры, где запущен из службы hello, перейдите в каждый элемент. Эту структуру удобно использовать при управлении независимыми компонентами. Однако приложения, построенные на платформе Azure, представляют собой коллекцию взаимосвязанных служб, а древовидная структура не слишком хорошо подходит для работы с коллекциями служб. 

Hello портал Azure позволяет легко toobuild приложений-законченный с компонентами из нескольких служб. портал Hello организованы в виде *поездок*. Объект *пути* представляет собой ряд *колонок*, которые являются контейнерами для hello различных компонентов. Например, настройке автоматического масштабирования для веб-приложения является *пути* которой осуществляется переход несколько колонок как показано в следующий пример hello: hello **веб сайт** (что заголовок колонки еще не обновленные toouse колонку Hello новых терминов), hello **параметры** и, при необходимости hello **горизонтальное масштабирование** колонку. В примере hello автоматического масштабирования, задаваемое toodepend по загрузке ЦП, поэтому имеется также **процент использования ЦП** колонку. Hello компонентов в пределах hello *колонок* называются *частей*, который выглядеть плитки. 

![](./media/app-service-web-app-azure-portal/AutoScaling.png)

## <a name="navigation-example-create-a-web-app"></a>Пример навигации: создание веб-приложения
Создание нового веб-приложения осуществляется просто, как 1 — 2 — 3. Привет, следуя изображение показывает hello классический портал и hello портала side-by-side toodemonstrate измененного не слишком большой hello число шагов требуется tooget веб-приложения, копирование и работает. 

![](./media/app-service-web-app-azure-portal/CreateWebApp.png)

Hello портала можно из наиболее распространенных типов веб-приложений, включая галереи популярных приложений, таких как WordPress hello. Полный список доступных приложений, посетите hello [Azure Marketplace].

При создании веб-приложения, необходимо указать URL-адрес, план служб приложений и точно так же, как в классическом портале hello портала hello. 

![](./media/app-service-web-app-azure-portal/CreateWebAppSettings.png)

Кроме того портал hello позволяет определять другие общие параметры. Например [групп ресурсов](../azure-resource-manager/resource-group-overview.md) сделать ее простой toosee и управлять связанных ресурсов Azure. 

## <a name="navigation-example-settings-and-features"></a>Пример навигации: параметры и возможности
Здравствуйте, все параметры и функции теперь логически сгруппированы в один колонки, из которой можно перейти.

![](./media/app-service-web-app-azure-portal/WebAppSettings.png)

Например, можно создать пользовательские домены, нажав кнопку **пользовательские домены и SSL** в hello **параметры** колонку.

![](./media/app-service-web-app-azure-portal/ConfigureWebApp.png)

tooset копирование мониторинга оповещения, щелкните **запросов и ошибок** и затем **добавить предупреждение**.

![](./media/app-service-web-app-azure-portal/Monitoring.png)

Щелкните диагностики tooenable **журналы диагностики** в hello **параметры** колонку.

![](./media/app-service-web-app-azure-portal/Diagnostics.png)

Нажмите кнопку "Параметры приложения" tooconfigure **параметры приложения** в hello **параметры** колонку. 

![](./media/app-service-web-app-azure-portal/AppSettingsPreview.png)

Кроме hello собственное имя, несколько моментов, на портале hello был переименован или сгруппированы по-разному toomake его проще toofind их. Например, ниже приведен снимок экрана hello соответствующей страницы параметров приложения (**Настройка**) hello классического портала.

![](./media/app-service-web-app-azure-portal/AppSettings.png)

## <a name="more-resources"></a>Дополнительные ресурсы
[Azure Portal]: https://portal.azure.com
[Azure Marketplace]: /marketplace/

> [!NOTE]
> Tooget работы в службе приложений Azure перед регистрацией учетную запись Azure, перейдите слишком[повторите служб приложений](https://azure.microsoft.com/try/app-service/), в котором можно немедленно создать кратковременных начальный веб-приложения в службе приложений. Никаких кредитных карт и обязательств.
> 
> 

## <a name="whats-changed"></a>Изменения
* Toohello руководство изменений из tooApp веб-сайтов службы. в разделе: [службе приложений Azure и ее влияние на существующие службы Azure](http://go.microsoft.com/fwlink/?LinkId=529714)

