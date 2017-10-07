---
title: "AAA» события начала задачи пакета Azure | Документы Microsoft»"
description: "Справочник по событию начала выполнения задачи пакетной службы."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Событие начала выполнения задачи

 Это событие создается после запланированного toostart на вычислительном узле задачи планировщиком hello. Обратите внимание, что если задачу hello повторно или повторно поставлен в очередь это событие будет создаваться повторно hello же задачу, но hello число повторных попыток и версию задачи системы будет обновлен соответствующим образом.


 Hello следующем примере показан текст hello события начала задачи.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|jobId|Строка|Идентификатор Hello hello задания, содержащий задачу hello.|
|id|Строка|Идентификатор Hello задачу hello.|
|taskType|Строка|Тип Hello задачу hello. Может быть установлено значение "JobManager", указывающее, что это задача диспетчера заданий, или значение "User", указывающее, что задача не относится к диспетчеру заданий.|
|systemTaskVersion|Int32|Это счетчик hello внутренних повторов задачи. Внутренне hello пакетной службы можно повторить попытку tooaccount задачи для временных проблем. Эти проблемы могут включать внутреннего планирования toorecover ошибок или попыток из вычислительных узлов в неверном состоянии.|
|[nodeInfo](#nodeInfo)|Сложный тип|Содержит сведения о hello вычислительных узлов, на какие hello запущена задача.|
|[multiInstanceSettings](#multiInstanceSettings)|Сложный тип|Указывает, что эта задача hello осуществляется несколькими экземплярами требуется несколько вычислительных узлов.  Дополнительные сведения см. в статье [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task).|
|[constraints](#constraints)|Сложный тип|ограничения выполнения Hello применимые toothis задачи.|
|[executionInfo](#executionInfo)|Сложный тип|Содержит сведения о выполнении hello задачи «hello».|

###  <a name="nodeInfo"></a> nodeInfo

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|poolId|Строка|Идентификатор Hello пула hello, на какие hello запущена задача.|
|nodeId|Строка|Идентификатор Hello hello узла, на какие hello запущена задача.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|numberOfInstances|int|количество вычислительных узлов, предусмотренного задачу hello Hello.|

###  <a name="constraints"></a> constraints

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Максимальное число повторных попыток задачу hello может быть Hello. Hello пакетная служба повторяет задачу, если ее код выхода имеет ненулевое значение.<br /><br /> Обратите внимание, что это значение определяет специально hello число повторных попыток. Пакетная служба Hello попытаться задачу hello один раз и повторите копирование toothis ограничение. Например если hello максимальное число повторных попыток равно 3, пакет пытается задачи вверх too4 времени (один начальной попытки и 3 попытки).<br /><br /> Если hello максимальное число повторных попыток равно 0, hello пакетная служба не выполняет повторную попытку запуска задачи.<br /><br /> Если hello максимальное число повторных попыток равно -1, hello пакетная служба повторяет задачи без ограничения.<br /><br /> значение по умолчанию Hello равно 0 (повторы отсутствуют).|

###  <a name="executionInfo"></a> executionInfo

|Имя элемента|Тип|Примечания|
|------------------|----------|-----------|
|retryCount|Int32|Здравствуйте, число повторных попыток задачу hello пакетной службой hello. Задача Hello перезапускается, если он выходит с ненулевой код выхода, копирование toohello указан MaxTaskRetryCount|
