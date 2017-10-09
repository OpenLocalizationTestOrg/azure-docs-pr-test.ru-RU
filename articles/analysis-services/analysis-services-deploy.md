---
title: "tooAzure aaaDeploy служб Analysis Services с помощью SSDT | Документы Microsoft"
description: "Узнайте, как toodeploy tooan табличной модели Azure служб Analysis Services с помощью SSDT."
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 5f1f0ae7-11de-4923-a3da-888b13a3638c
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/01/2017
ms.author: owend
ms.openlocfilehash: e3f3771fe32a37b9e0173c274080c647152edd4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-a-model-from-ssdt"></a>Развертывание модели из SSDT
После создания сервера в вашей подписке Azure, вы готовы toodeploy tooit базы данных табличной модели. Можно использовать SQL Server Data Tools (SSDT) toobuild и развертывание проекта табличной модели, над которым вы работаете. 

## <a name="prerequisites"></a>Предварительные требования
tooget работы, необходимо:

* **Сервер Analysis Services** в Azure. toolearn более, в разделе [создать сервер служб Azure Analysis Services](analysis-services-create-server.md).
* **Проект табличной модели** в SSDT или существующей табличной модели hello 1200 или высоким уровнем совместимости. Не создавали такую модель ранее? Повторите hello [учебник по Adventure Works Интернет продаж табличного моделирования](https://msdn.microsoft.com/library/hh231691.aspx).
* **Локальный шлюз** -Если один или несколько источников данных в локальной сети вашей организации, необходимо tooinstall [локального шлюза данных](analysis-services-gateway.md). Hello шлюз необходим для tooyour локальной данных источников tooprocess и обновления данных в модели hello подключиться к серверу в облаке hello.

> [!TIP]
> Перед развертыванием, убедитесь, что может обрабатывать данные hello в таблицах. В средстве SSDT последовательно выберите элементы **Модель** > **Обработать** > **Обработать все**. Если обработка завершается сбоем, вы не сможете выполнить развертывание.
> 
> 

## <a name="toodeploy-a-tabular-model-from-ssdt"></a>toodeploy табличной модели из SSDT

1. Перед развертыванием, нужно имя сервера tooget hello. В **портал Azure** > сервера > **Обзор** > **имя сервера**, имя сервера hello копирования.
   
    ![Получение имени сервера в Azure](./media/analysis-services-deploy/aas-deploy-get-server-name.png)
2. В SSDT > **обозревателе решений**, щелкните правой кнопкой мыши проект hello > **свойства**. Затем в **развертывания** > **сервера** вставьте имя сервера hello.   
   
    ![Вставьте имя сервера в свойства сервера развертывания](./media/analysis-services-deploy/aas-deploy-deployment-server-property.png)
3. В окне **Обозреватель решений** щелкните правой кнопкой мыши элемент **Свойства** и выберите команду **Развернуть**. Возможно, запрошенные toosign в tooAzure.
   
    ![Развертывание tooserver](./media/analysis-services-deploy/aas-deploy-deploy.png)
   
    Состояние развертывания отображается в окне вывода обоих hello и в развертывание.
   
    ![Состояния развертывания](./media/analysis-services-deploy/aas-deploy-status.png)

Это все, имеется tooit!


## <a name="troubleshooting"></a>Устранение неполадок
Если происходит сбой развертывания при развертывании метаданных, вполне вероятно, так как SSDT не удалось подключиться к серверу tooyour. Убедитесь, что можно подключить сервер tooyour, с помощью среды SSMS. Убедитесь в правильности hello свойства сервера развертывания для проекта hello.

Если развертывание завершается ошибкой на таблице, вполне вероятно, так как серверу не удалось подключиться к tooa источника данных. Если источником данных является локальной в сети вашей организации, быть убедиться, что tooinstall [локального шлюза данных](analysis-services-gateway.md).

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда сервер tooyour развернутой табличной модели, вы готовы tooconnect tooit. Вы можете [подключитесь к SSMS tooit](analysis-services-manage.md) toomanage его. И вы можете [подключиться с помощью клиентского средства tooit](analysis-services-connect.md) , такие как Power BI, Power BI Desktop или Excel и начала создания отчетов.

