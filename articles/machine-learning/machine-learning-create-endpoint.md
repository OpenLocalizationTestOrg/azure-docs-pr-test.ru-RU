---
title: "конечные точки службы Web aaaCreating в машинном обучении | Документы Microsoft"
description: "Создание конечных точек веб-службы в машинном обучении Azure"
services: machine-learning
documentationcenter: 
author: hiteshmadan
manager: padou
editor: cgronlun
ms.assetid: 4657fc1b-5228-4950-a29e-bc709259f728
ms.service: machine-learning
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 10/04/2016
ms.author: himad
ms.openlocfilehash: 10a2bc586c6fe35e28d8bf0293854c578827c453
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-endpoints"></a>Создание конечных точек
> [!NOTE]
>  В этом разделе описывается tooa применимые методы **классический** веб-машины обучения службы.
> 
> 

При создании веб-служб, торгующих прямой tooyour клиентов необходимо tooprovide обученных моделей tooeach клиента, которые по-прежнему связанные toohello эксперимент, из которого hello Web служба была создана. Кроме того все обновления, должно быть toohello эксперимента применяемой выборочно tooan конечной точки без перезаписи hello настроек.

tooaccomplish, машинного обучения Azure позволяет toocreate несколько конечных точек для развернутого веб-службы. Каждая конечная точка веб-службы hello независимо обращаться, регулирование и управляемых. Каждая конечная точка является уникальным ключом URL-адрес и авторизации, можно распространять tooyour клиентов.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="adding-endpoints-tooa-web-service"></a>Добавление конечных точек tooa веб-служб
Существует три способа tooadd tooa конечной точки веб-службы.

* Программным образом
* Через портал веб-службы Azure Machine Learning hello
* Хотя hello классический портал Azure

После создания конечной точки hello, можно использовать его через синхронного API, пакетных API и листы excel. В дополнение к этому tooadding конечные точки через этот пользовательский Интерфейс, можно также использовать API-интерфейсы управления конечной точки tooprogrammatically hello добавить конечные точки.

> [!NOTE]
> Если вы добавили toohello дополнительные конечные точки веб-службы, нельзя удалить конечную точку по умолчанию hello.
> 
> 

## <a name="adding-an-endpoint-programmatically"></a>Добавление конечной точки программным путем
Можно добавить веб-служба конечной точки tooyour программно с помощью hello [AddEndpoint](https://github.com/raymondlaghaeian/AML_EndpointMgmt/blob/master/Program.cs) пример кода.

## <a name="adding-an-endpoint-using-hello-azure-machine-learning-web-services-portal"></a>Добавление конечной точки с помощью портала веб-службы Azure Machine Learning hello
1. В студии машинного обучения на столбце hello навигации слева, нажмите кнопку веб-служб.
2. Внизу hello hello мониторинга веб-службы, нажмите кнопку **Управление конечными точками**. портал веб-службы Azure Machine Learning Hello, откроется страница toohello конечных точек для hello веб-службы.
3. Нажмите кнопку **Создать**.
4. Введите имя и описание для новой конечной точки hello. Имена конечных точек должны и состоять из строчных букв или цифр и не могут содержать более 24 символов. Выберите уровень ведения журнала hello и включена ли образец данных. Дополнительные сведения о ведении журнала см. в статье [Включение функции ведения журналов для веб-служб машинного обучения](machine-learning-web-services-logging.md).

## <a name="adding-an-endpoint-using-hello-azure-classic-portal"></a>Добавление конечной точки с помощью hello классический портал Azure
1. Войдите в toohello [классический портал Azure](http://manage.windowsazure.com), нажмите кнопку **машинного обучения** в левом столбце hello. Щелкните рабочую область hello, который содержит hello веб-службы, в котором вы заинтересованы.
   
    ![Перейдите tooworkspace](./media/machine-learning-create-endpoint/figure-1.png)
2. Щелкните **Веб-службы**.
   
    ![Переход службы tooWeb](./media/machine-learning-create-endpoint/figure-2.png)
3. Выберите веб-служба hello, вас интересует toosee hello список доступных конечных точек.
   
    ![Перейдите tooendpoint](./media/machine-learning-create-endpoint/figure-3.png)
4. Внизу hello страницы приветствия щелкните **добавить конечную точку**. Введите имя и описание, убедитесь, что нет других конечных точек с hello точно такое же имя в веб-службу. Оставьте уровень регулировки hello со значением по умолчанию, если у вас нет особых требований. toolearn Дополнительные сведения о регулирования количества запросов, в разделе [масштабирование конечные точки API](machine-learning-scaling-webservice.md).
   
    ![Создать конечную точку](./media/machine-learning-create-endpoint/figure-4.png)

## <a name="next-steps"></a>Дальнейшие действия
[Как tooconsume в Azure Machine обучения, веб-службу](machine-learning-consume-web-services.md).

