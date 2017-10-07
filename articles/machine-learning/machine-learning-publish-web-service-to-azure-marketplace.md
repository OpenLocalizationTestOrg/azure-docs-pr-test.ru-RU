---
title: "AAA(deprecated) публикации машинного самообучения, web service tooAzure Marketplace | Документы Microsoft"
description: "(устарело) Как toopublish toohello вашего веб-служба Azure Machine Learning Azure Marketplace"
services: machine-learning
documentationcenter: 
author: BharathS
manager: jhubbard
editor: cgronlun
ms.assetid: 68e908be-3a99-4cd7-9517-e2b5f2f341b8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/02/2017
ms.author: bharaths
ROBOTS: NOINDEX
redirect_url: machine-learning-gallery-experiments
redirect_document_id: True
ms.openlocfilehash: 149abc3df9b79c1b37d233d5e85e803592ff1020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deprecated-publish-azure-machine-learning-web-service-toohello-azure-marketplace"></a>(устарело) Публикация веб-служба Azure Machine Learning toohello Azure Marketplace

> [!NOTE]
> Работа DataMarket и служб данных прекращается. Начиная с 31 марта 2017 г. имеющиеся подписки выводятся из эксплуатации и будут отменены. Поэтому мы не рекомендуем использовать эту статью. 
> 
> В качестве альтернативы можно опубликовать эксперименты в машинное обучение toohello [коллекции аналитики Cortana](https://gallery.cortanaintelligence.com/) преимущество hello сообщества обработки и анализа данных hello. Дополнительные сведения см. в разделе [общего ресурса и поиска ресурсов в коллекции Cortana аналитики hello](https://docs.microsoft.com/en-us/azure/machine-learning/machine-learning-gallery-how-to-use-contribute-publish).

Hello Azure Marketplace позволяет hello веб-службы машинного обучения Azure toopublish как платная или освобождения службы для потребления внешними клиентами. В этой статье Общие сведения об этом процессе с tooget tooguidelines ссылки, который был запущен. Используя этот процесс, можно сделать доступными для других tooconsume разработчики веб-служб в своих приложениях.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="overview-of-hello-publishing-process"></a>Обзор процесса публикации hello
Hello ниже приведены шаги hello для публикации tooAzure службы web машинного обучения Azure Marketplace.

1. Создайте и опубликуйте службу машинного обучения типа «запрос-ответ» (RRS).
2. Развертывание службы tooproduction hello и получите hello ключ API и OData сведения о конечной точке.
3. URL-адрес hello для hello используйте опубликованных web service toopublish слишком[Azure Marketplace (Data Market)](https://publish.windowsazure.com/workspace/) 
4. После отправки, анализируется ваше предложение и должен toobe утверждения перед клиентов можно запустить его приобретения. Hello публикации может занять несколько рабочих дней. 

## <a name="walk-through"></a>Пошаговое руководство
### <a name="step-1-create-and-publish-a-machine-learning-request-response-service-rrs"></a>Шаг 1. Создание и публикация службы машинного обучения типа «запрос-ответ» (RRS)
 Если вы еще не создали такую службу, ознакомьтесь с этим [пошаговым руководством](machine-learning-walkthrough-5-publish-web-service.md).

### <a name="step-2-deploy-hello-service-tooproduction-and-obtain-hello-api-key-and-odata-endpoint-information"></a>Шаг 2: Развертывание службы tooproduction hello и получить hello сведения о конечной точке OData и ключ API
1. Из hello [классический портал Azure](http://manage.windowsazure.com)выберите hello **МАШИННОГО ОБУЧЕНИЯ** hello левой навигационной панели и выберите рабочую область. 
2. Щелкните hello **веб-службы** вкладку и выберите hello веб-службы требуется toopublish toohello marketplace.
   
    ![Azure Marketplace][workspace]
3. Выберите конечную точку hello бы как toohave hello marketplace использовать. Если вы не создали все дополнительные конечные точки, можно выбрать hello **по умолчанию** конечной точки.
4. При щелчке на конечной точке hello будет hello может toosee **ключ API**. Скопируйте его. Эта информация потребуется далее на шаге 3.
   
    ![Azure Marketplace][apikey]
5. Щелкните hello **запрос-ОТВЕТ** метод на этом этапе мы не поддерживаем Публикация выполнения пакета служб toohello marketplace. Будет выполнен toohello API страницы справки для hello метода запроса и ответа.
6. Копировать hello **адрес конечной точки OData**, вам потребуется эта информация позже на шаге 3.
   
    ![Azure Marketplace][odata]

развертывание службы hello в рабочей среде.

### <a name="step-3-use-hello-url-of-hello-published-web-service-toopublish-tooazure-marketplace-datamarket"></a>Шаг 3: Используйте URL hello hello опубликованных tooAzure toopublish web service Marketplace (DataMarket)
1. Перейдите в слишком[Azure Marketplace (Data Market)](http://datamarket.azure.com/home) 
2. Щелкните hello **публикации** ссылку вверху hello страницы приветствия. Это может занять toohello [портал публикации Microsoft Azure](https://publish.windowsazure.com)
3. Щелкните hello **издателей** tooregister раздел как издатель.
4. При создании предложения выберите пункт **Службы данных**, а затем выберите команду **Create a New Data Service** (Создать службу данных). 
   
   ![Azure Marketplace][image1]
   
   <br />
5. На вкладке **Планы** укажите информацию о предложении, включая тарифный план. Определите, будет ли предложение платной или бесплатной службой. tooget оплачен, предоставляют сведения о платеже, такие как данные налогов и банка.
6. В разделе **маркетинга** предоставляют сведения о вашем предложении, например hello заголовок и описание для вашего предложения.
7. В разделе **цены** задать hello цены для планов для определенных стран или позволить системе hello «autoprice» ваше предложение.
8. На hello **службы данных** щелкните **веб-службы** как hello **источника данных**.
   
    ![Azure Marketplace][image2]
9. Получите hello web service URL-адрес и ключ API из hello классический портал Azure, как описано в шаге 2 выше.
10. В hello службы данных Marketplace диалогового окна настройки вставьте адрес конечной точки OData hello в hello **URL-адрес службы** текстовое поле.
11. Для **проверки подлинности**, выберите **заголовок** как hello **схему проверки подлинности**.
    
    * Введите «Авторизации» hello **имя заголовка**.
    * Для hello **значение заголовка**введите «Bearer» (без кавычек hello), щелкните hello **пространства** панели, а затем вставьте ключ hello API.
    * Выберите hello **данная служба является OData** флажок.
    * Нажмите кнопку **проверить подключение** tootest hello соединения.
12. На вкладке **Категории** выберите **Машинное обучение**.
13. По завершении ввода всех hello метаданные о вашем предложении, нажмите кнопку **публикации**, а затем **Push tooStaging**. На этом этапе вы получите уведомление о неполадках остальные необходимые toofix.
14. Убедившись завершения всех проблем hello щелкните **запросить утверждение toopush tooProduction**. Hello публикации может занять несколько рабочих дней. 

[image1]:./media/machine-learning-publish-web-service-to-azure-marketplace/image1.png
[image2]:./media/machine-learning-publish-web-service-to-azure-marketplace/image2.png
[workspace]:./media/machine-learning-publish-web-service-to-azure-marketplace/selectworkspace.png
[apikey]:./media/machine-learning-publish-web-service-to-azure-marketplace/apikey.png
[odata]:./media/machine-learning-publish-web-service-to-azure-marketplace/odata.png

