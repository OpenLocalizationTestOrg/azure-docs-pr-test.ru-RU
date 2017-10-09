---
title: "AAA» узла переменные среды вычислений пакета Azure | Документы Microsoft»"
description: "Справочник по переменным среды вычислительного узла для пакетной аналитики Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 05/05/2017
ms.author: tamram
ms.openlocfilehash: 860f34b530579a81fbd5cf8ffa31df79d917c080
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-batch-compute-node-environment-variables"></a>Переменные среды вычислительного узла пакетной службы Azure
Hello [пакетной службы Azure](https://azure.microsoft.com/services/batch/) задает hello следующие переменные среды на вычислительных узлах. Можно ссылаться на эти переменные среды в задачи команд из командной строки и программах hello и сценариев обслуживаемая hello команд из командной строки.

Дополнительные сведения об использовании переменных среды в пакетной службе см. в статье [Параметры среды для задач](https://docs.microsoft.com/azure/batch/batch-api-basics#environment-settings-for-tasks).

## <a name="environment-variable-visibility"></a>Видимость переменных среды

Эти переменные среды видимы только в контексте hello hello **пользователь задач**, hello учетной записи пользователя на узле hello, в котором выполняется задача. Вы будете *не* они отображаются, если вы [удаленного подключения](https://azure.microsoft.com/documentation/articles/batch-api-basics/#connecting-to-compute-nodes) tooa вычислительный узел посредством протокола удаленного рабочего стола (RDP) или Secure Shell (SSH) и список переменных среды hello. Это вызвано hello учетной записи пользователя, который используется для подключения к удаленному не hello аналогично hello учетной записи, которая используется задачей «hello».

## <a name="command-line-expansion-of-environment-variables"></a>Расширение переменных среды в командной строке

Hello командные строки, выполняется с помощью задач на вычислительные узлы, не выполняются в оболочке. Таким образом, эти команды могут использовать изначально оболочки функций, таких как расширение переменных среды (сюда входят hello `PATH`). tootake преимущества этих функций необходимо **вызова неуправляемого кода hello оболочки** в командной строке hello. Например, запустите `cmd.exe` на вычислительных узлах Windows или `/bin/sh` на узлах Linux:

`cmd /c MyTaskApplication.exe %MY_ENV_VAR%`

`/bin/sh -c MyTaskApplication $MY_ENV_VAR`

## <a name="environment-variables"></a>Переменные среды

| Имя переменной                     | Описание                                                              | Доступность | Пример |
|-----------------------------------|--------------------------------------------------------------------------|--------------|---------|
| AZ_BATCH_ACCOUNT_NAME           | Имя учетной записи пакетной hello, hello задачи Hello принадлежит.                  | Все задачи.   | mybatchaccount |
| AZ_BATCH_CERTIFICATES_DIR       | Каталог, находящийся внутри hello [рабочий каталог задач] [ files_dirs] в какие сертификаты хранятся Linux вычислительных узлов. Обратите внимание, что эта переменная среды не применяется tooWindows вычислительных узлов.                                                  | Все задачи.   |  /mnt/batch/tasks/workitems/batchjob001/job-1/task001/certs |
| AZ_BATCH_JOB_ID                 | Идентификатор Hello hello задания, которое hello задач принадлежит. | Все задачи, кроме задачи запуска. | batchjob001 |
| AZ_BATCH_JOB_PREP_DIR           | Полный путь Hello подготовки задания hello [каталог задач] [ files_dirs] на узле hello. | Все задачи, кроме задачи запуска и задачи подготовки задания. Доступна, только если задание hello настраивается с помощью задачи подготовки задания. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation |
| AZ_BATCH_JOB_PREP_WORKING_DIR   | Полный путь Hello подготовки задания hello [рабочий каталог задач] [ files_dirs] на узле hello. | Все задачи, кроме задачи запуска и задачи подготовки задания. Доступна, только если задание hello настраивается с помощью задачи подготовки задания. | C:\user\tasks\workitems\jobprepreleasesamplejob\job-1\jobpreparation\wd |
| AZ_BATCH_NODE_ID                | назначается идентификатор Hello узла hello, hello задачи. | Все задачи. | tvm-1219235766_3-20160919t172711z |
| AZ_BATCH_NODE_ROOT_DIR          | Hello полный путь к корневому каталогу hello всех [пакета каталоги] [ files_dirs] на узле hello. | Все задачи. | C:\user\tasks |
| AZ_BATCH_NODE_SHARED_DIR        | Полный путь Hello hello [общий каталог] [ files_dirs] на узле hello. Все задачи, которые выполняются на узле иметь каталог toothis доступа чтения и записи. Задачи, которые выполняются на других узлах не определяют каталог toothis удаленного доступа (он не является «общий» сетевого каталога). | Все задачи. | C:\user\tasks\shared |
| AZ_BATCH_NODE_STARTUP_DIR       | Полный путь Hello hello [запустите задачу каталога] [ files_dirs] на узле hello. | Все задачи. | C:\user\tasks\startup |
| AZ_BATCH_POOL_ID                | Идентификатор Hello пула hello, hello задача выполняется на. | Все задачи. | batchpool001 |
| AZ_BATCH_TASK_DIR               | Полный путь Hello hello [каталог задач] [ files_dirs] на узле hello. В этом каталоге содержатся hello `stdout.txt` и `stderr.txt` задачу hello и hello AZ_BATCH_TASK_WORKING_DIR. | Все задачи. | C:\user\tasks\workitems\batchjob001\job-1\task001 |
| AZ_BATCH_TASK_ID                | Идентификатор Hello hello текущей задачи. | Все задачи, кроме задачи запуска. | task001 |
| AZ_BATCH_TASK_WORKING_DIR       | Полный путь Hello hello [рабочий каталог задач] [ files_dirs] на узле hello. Привет, запущенных задач имеет каталог toothis доступа чтения и записи. | Все задачи. | C:\user\tasks\workitems\batchjob001\job-1\task001\wd |
| CCP_NODES                       | Список Hello узлы и количество ядер на узел, выделенных tooa [задач многоэкземплярные][multi_instance]. Узлы и ядра указываются в формате hello`numNodes<space>node1IP<space>node1Cores<space>`<br/>`node2IP<space>node2Cores<space> ...`, где hello количество узлов следует один или несколько IP-адреса узла, а hello количество ядер для каждой. |  Основные задачи и подзадачи с несколькими экземплярами. |`2 10.0.0.4 1 10.0.0.5 1` |
| AZ_BATCH_NODE_LIST              | Hello список узлов, которые выдаются tooa [задач многоэкземплярные] [ multi_instance] в формате hello `nodeIP;nodeIP`. | Основные задачи и подзадачи с несколькими экземплярами. | `10.0.0.4;10.0.0.5` |
| AZ_BATCH_HOST_LIST              | Hello список узлов, которые выдаются tooa [задач многоэкземплярные] [ multi_instance] в формате hello `nodeIP,nodeIP`. | Основные задачи и подзадачи с несколькими экземплярами. | `10.0.0.4,10.0.0.5` |
| AZ_BATCH_MASTER_NODE            | Hello IP-адрес и порт hello вычислительного узла в какой hello основной задачей [задач многоэкземплярные] [ multi_instance] запускает. | Основные задачи и подзадачи с несколькими экземплярами. | `10.0.0.4:6000`|
| AZ_BATCH_TASK_SHARED_DIR | Путь к каталогу, идентичный основная задача hello и каждый подзадачей [задач многоэкземплярные][multi_instance]. Hello путь существует на каждом узле, на которой работает задача многоэкземплярные hello и является чтение и запись команды задач доступны toohello, выполняющиеся на этом узле (оба hello [координации командной] [ coord_cmd] и hello [команды приложения][app_cmd]). Подзадачи или основной задачей, выполните на другие узлы не имеют каталог toothis удаленного доступа (он не является «общий» сетевого каталога). | Основные задачи и подзадачи с несколькими экземплярами. | C:\user\tasks\workitems\multiinstancesamplejob\job-1\multiinstancesampletask |
| AZ_BATCH_IS_CURRENT_NODE_MASTER | Указывает, является ли текущий узел hello hello главного узла для [задач многоэкземплярные][multi_instance]. Возможные значения: `true` и `false`.| Основные задачи и подзадачи с несколькими экземплярами. | `true` |
| AZ_BATCH_NODE_IS_DEDICATED | Если `true`, hello текущий узел является узлом выделенный. Если имеет значение `false`, то это [низкоприоритетный узел](batch-low-pri-vms.md). | Все задачи. | `true` |

[files_dirs]: https://azure.microsoft.com/documentation/articles/batch-api-basics/#files-and-directories
[multi_instance]: https://azure.microsoft.com/documentation/articles/batch-mpi/
[coord_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#coordination-command
[app_cmd]: https://azure.microsoft.com/documentation/articles/batch-mpi/#application-command
