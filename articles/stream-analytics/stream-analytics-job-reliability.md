---
title: "Устранение прерывания работы служб с помощью заданий Azure Stream Analytics | Документация Майкрософт"
description: "Руководство по обеспечению надежности заданий Stream Analytics при установке новых версий служб."
services: stream-analytics
documentationCenter: 
authors: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 3ac65c93ecb47e93e963dd9869a7af70f73b19c7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="guarantee-stream-analytics-job-reliability-during-service-updates"></a>Обеспечение надежности заданий Stream Analytics во время обновления служб

Выполняется полностью управляемую службу входит hello возможность toointroduce новые функции, службы и улучшения в быструю темпе. Это позволяет Stream Analytics осуществлять обновление служб еженедельно (или даже чаще). Независимо от того, какую часть тестирования выполняется по-прежнему есть риск, что существующий, выполнение задания может быть поврежден из-за появлением toohello ошибки. Для пользователей, выполняющих важные потоковых заданий обработки этих рисков должны избегать toobe. Механизм клиенты могут использовать tooreduce этот риск будет Azure  **[парном регионе](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  модели. 

## <a name="how-do-azure-paired-regions-address-this-concern"></a>Как сопряженные регионы Azure помогают устранить эту проблему?

Stream Analytics гарантирует, что задания в сопряженных регионах обновляются в разных пакетах. В результате имеется достаточно временной промежуток между обновлениями hello tooidentify потенциальных критические ошибки и исправлять их.

_За исключением hello из центральной Индии_ (которого парном регионе, Южной Индии и не имеет присутствия Stream Analytics), hello развертывания обновления tooStream Analytics не будет находиться во hello одновременную в набор парных регионов. Развертывание в нескольких регионах **в hello одной группе** может возникнуть **в hello одновременно**.

Hello статьи на  **[доступности и парных регионов](https://docs.microsoft.com/azure/best-practices-availability-paired-regions)**  имеет hello наиболее актуальные сведения, в которой сопоставляются области.

Клиенты, желательно toodeploy идентичные задания tooboth пару областей. В дополнение к этому tooStream Analytics внутренней мониторингу, клиентов, также рекомендуется toomonitor hello задания как если бы **оба** рабочих заданий. Если разрыв идентифицированных toobe результат обновления службы Stream Analytics hello, повышать уровень соответствующим образом и перенести никаких выходных данных задания работоспособное toohello потребителей потока данных. Укрупнение toosupport предотвращения влияния, новое развертывание hello парном регионе hello и сохраняет целостность hello hello пару заданий.
