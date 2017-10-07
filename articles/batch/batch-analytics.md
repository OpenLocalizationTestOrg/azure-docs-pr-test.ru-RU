---
title: "aaaAzure пакета аналитики | Документы Microsoft"
description: "Справочник по пакетной аналитике Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>Пакетная аналитика
разделы Hello в пакете аналитики содержатся справочные сведения по hello событий и предупреждений, доступных для ресурсов службы пакета.

Статья [Ведение журналов диагностики пакетной службы Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) содержит дополнительные сведения о включении и использовании журналов диагностики пакетной службы.

## <a name="diagnostic-logs"></a>Журналы диагностики

Hello пакетной службы Azure создает следующие события журнала диагностики во время существования hello определенных ресурсов пакета hello.

**События журнала службы**
* [Создание пула](batch-pool-create-event.md)
* [Начало удаления пула](batch-pool-delete-start-event.md)
* [Завершение удаления пула](batch-pool-delete-complete-event.md)
* [Начало изменения размера пула](batch-pool-resize-start-event.md)
* [Завершение изменения размера пула](batch-pool-resize-complete-event.md)
* [Начало выполнения задачи](batch-task-start-event.md)
* [Завершение выполнения задачи](batch-task-complete-event.md)
* [Сбой выполнения задачи](batch-task-fail-event.md)