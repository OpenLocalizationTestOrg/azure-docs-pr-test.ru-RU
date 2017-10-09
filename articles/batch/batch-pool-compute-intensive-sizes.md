---
title: "aaaUse вычислений виртуальные машины Azure с использованием пакета | Документы Microsoft"
description: "Как tootake преимуществами функцией RDMA или поддержкой графического Процессора виртуальной Машины размером в пулах пакетной службы Azure"
services: batch
documentationcenter: 
author: dlepow
manager: timlt
editor: 
ms.assetid: 
ms.service: batch
ms.workload: big-compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: danlep
ms.openlocfilehash: 6a462a5f2a44ddcec8bf4e5c200d444cac8fafe6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-rdma-capable-or-gpu-enabled-instances-in-batch-pools"></a>Использование экземпляров с поддержкой RDMA или графического процессора (GPU) в пулах пакетной службы

toorun определенных пакетных заданий может потребоваться tootake преимуществами предназначены для крупномасштабных вычисления размеров виртуальных Машин Azure. Например, несколькими экземплярами toorun [рабочих нагрузок MPI](batch-mpi.md), вы можете A8, A9, или H-series размеры, которые есть сеть интерфейс для удаленного прямого доступа к памяти (RDMA). Эти размеры подключиться к сети InfiniBand tooan для обмена данными между узлами, которая ускоряет приложений MPI. Для приложений CUDA можно выбрать размеры серии N, которые включают карты графического процессора (GPU) NVIDIA Tesla.

Эта статья содержит рекомендации и примеры toouse специализированные размер Azure в пулах пакета. Спецификации и общие сведения см. по следующим ссылкам:

* размеры виртуальных машин, оптимизированных для высокопроизводительных вычислений ([Linux](../virtual-machines/linux/sizes-hpc.md), [Windows](../virtual-machines/windows/sizes-hpc.md)); 

* размеры виртуальных машин с поддержкой графического процессора (GPU) ([Linux](../virtual-machines/linux/sizes-gpu.md), [Windows](../virtual-machines/windows/sizes-gpu.md)). 


## <a name="subscription-and-account-limits"></a>Ограничения подписки и учетной записи

* **Квоты** -одну или несколько квот Azure может ограничить число hello или тип узлов можно добавить tooa пула. Вы являетесь, скорее всего, toobe ограниченный при выборе функцией RDMA, GPU включен, или другие многоядерными размеры виртуальных Машин. В зависимости от типа hello созданную учетную запись пакета квоты hello применить toohello с учетной записью или tooyour подписки.

    * При создании учетной записи пакета в hello **пакетной службы** конфигурации, ограничиваются hello [Квота выделенных ядер на учетную запись пакетной](batch-quota-limit.md#resource-quotas). По умолчанию задана квота в 20 ядер. Отдельные Квота также применяется[виртуальные машины с низким приоритетом](batch-low-pri-vms.md), если они используются. 

    * Если вы создали учетную запись hello в hello **подписки пользователя** конфигурации подписки ограничивает число hello Виртуальных машинах в одном регионе. Ознакомьтесь со статьей [Подписка Azure, границы, квоты и ограничения службы](../azure-subscription-service-limits.md). Подписки также применяется региональные квоты размера виртуальной Машины toocertain, включая экземпляры HPC и GPU. В конфигурации подписки пользователя hello без дополнительных квот применяются toohello пакетной учетной записи. 

  Может потребоваться tooincrease одну или несколько квот при использовании специализированных размер виртуальной Машины в пакете. Увеличение квоты, откройте toorequest [запрос на получение поддержки сети клиента](../azure-supportability/how-to-create-azure-support-request.md) бесплатно.

* **Область доступности** - вычислений виртуальные машины могут быть недоступны в регионах hello создаются учетные записи пакета. toocheck, что размер доступен в разделе [продукты, доступные по регионам](https://azure.microsoft.com/regions/services/).


## <a name="dependencies"></a>Зависимости

Hello RDMA и возможности GPU размеров большим объемом вычислений, поддерживаются только в определенных операционных системах. В зависимости от операционной системы может потребоваться tooinstall или Настройка дополнительных драйверов или другого программного обеспечения. Привет, в следующей таблице приведены эти зависимости. Перейдите по ссылке, чтобы просмотреть дополнительные сведения. Параметры tooconfigure пакета пулы см. Далее в этой статье.


### <a name="linux-pools---virtual-machine-configuration"></a>Пулы Linux — конфигурация виртуальной машины

| Размер | Функция | Операционные системы | Необходимое программное обеспечение | Параметры пула |
| -------- | -------- | ----- |  -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/linux/sizes-hpc.md#rdma-capable-instances) | RDMA | SUSE Linux Enterprise Server 12 HPC или<br/>Экземпляр HPC на платформе CentOS<br/>(Microsoft Azure Marketplace) | Intel MPI 5 | Включение связи между узлами, отключение параллельного выполнения задач |
| [Серия NC*](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms) | Графический процессор NVIDIA Tesla K80 | Ubuntu 16.04 LTS.<br/>Red Hat Enterprise Linux 7.3 или<br/>Версия 7.3 на основе CentOS<br/>(Microsoft Azure Marketplace) | Драйверы для набора средств NVIDIA CUDA Toolkit 8.0 | Недоступно | 
| [Серия NV](../virtual-machines/linux/n-series-driver-setup.md#install-grid-drivers-for-nv-vms) | Графический процессор NVIDIA Tesla M60 | Ubuntu 16.04 LTS<br/>Red Hat Enterprise Linux 7.3<br/>Версия 7.3 на основе CentOS<br/>(Microsoft Azure Marketplace) | Драйверы для NVIDIA GRID 4.3 | Недоступно |

* Подключение RDMA на виртуальных машинах NC24r поддерживается в экземпляре HPC на платформе CentOS 7.3 с Intel MPI.



### <a name="windows-pools---virtual-machine-configuration"></a>Пулы Windows — конфигурация виртуальной машины

| Размер | Функция | Операционные системы | Необходимое программное обеспечение | Параметры пула |
| -------- | ------ | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2 или<br/>Windows Server 2012 (Microsoft Azure Marketplace) | Microsoft MPI 2012 R2 или более поздней версии либо<br/> Intel MPI 5<br/><br/>Расширение виртуальных машин Azure HpcVMDrivers | Включение связи между узлами, отключение параллельного выполнения задач |
| [Серия NC*](../virtual-machines/windows/n-series-driver-setup.md) | Графический процессор NVIDIA Tesla K80 | Windows Server 2016 или <br/>Windows Server 2012 R2 (Microsoft Azure Marketplace) | Драйверы NVIDIA Tesla или драйверы набора средств CUDA Toolkit 8.0| Недоступно | 
| [Серия NV](../virtual-machines/windows/n-series-driver-setup.md) | Графический процессор NVIDIA Tesla M60 | Windows Server 2016 или<br/>Windows Server 2012 R2 (Microsoft Azure Marketplace) | Драйверы для NVIDIA GRID 4.3 | Недоступно |

* Подключение RDMA на виртуальных машинах NC24r поддерживается на Windows Server 2012 R2 с расширением HpcVMDrivers и Microsoft MPI или Intel MPI.

### <a name="windows-pools---cloud-services-configuration"></a>Пулы Windows — конфигурация облачных служб

> [!NOTE]
> N-й серии размеры не поддерживаются в пулах пакета с hello конфигурация облачных служб.
>

| Размер | Функция | Операционные системы | Необходимое программное обеспечение | Параметры пула |
| -------- | ------- | -------- | -------- | ----- |
| [H16r, H16mr, A8, A9](../virtual-machines/windows/sizes-hpc.md#rdma-capable-instances) | RDMA | Windows Server 2012 R2,<br/>Windows Server 2012 или<br/>Windows Server 2008 R2 (семейство версий гостевой ОС) | Microsoft MPI 2012 R2 или более поздней версии либо<br/>Intel MPI 5<br/><br/>Расширение виртуальных машин Azure HpcVMDrivers | Включение связи между узлами,<br/> отключение параллельного выполнения задач |





## <a name="pool-configuration-options"></a>Варианты настройки пула

tooconfigure специализированные размер виртуальной Машины для пула, API-интерфейсы пакета hello и средства пакета предоставляют несколько программного обеспечения tooinstall необходимые параметры или драйверов, включая:

* [Запустить задачу](batch-api-basics.md#start-task) -Загрузите пакет установки как tooan файл ресурсов учетной записи хранилища Azure в hello же регионе, что hello пакетной учетной записи. Создания файла ресурсов hello tooinstall начала задачи командной строки без вмешательства пользователя, при запуске пула hello. Дополнительные сведения см. в разделе hello [документация по REST API](/rest/api/batchservice/add-a-pool-to-an-account#bk_starttask).

  > [!NOTE] 
  > Задача запуска Hello необходимо запустить с повышенными привилегиями (администратор) разрешениями и дождитесь успешного завершения.
  >

* [Пакет приложения](batch-application-packages.md) — Добавление ZIP-папки установки пакета tooyour пакетной учетной записи и настройка пакета справочника в пуле hello. Этот параметр передает и распаковывает hello пакета на всех узлах в кластере hello. Если hello пакет установщика, создайте приложение hello установки начала задачи командной строки toosilently на всех узлах пула. Дополнительно можно установите hello пакета, если задача становится запланированных toorun на узле.

* [Пул настраиваемых изображений](batch-api-basics.md#pool) — создать пользовательские Windows или образ ВМ Linux, содержащий драйверы, программного обеспечения и другие параметры требуется для hello размер виртуальной Машины. При создании учетной записи пакета в конфигурации подписки пользователя hello укажите hello пользовательского образа для пула пакета. (Пользовательские образы, не поддерживаются в учетных записях в конфигурации службы пакета hello.) Пользовательские изображения может использоваться только с пулами в конфигурации виртуальной машины hello.

  > [!IMPORTANT]
  > В пулах пакетной службы сейчас нельзя использовать пользовательские образы, созданные с помощью управляемых дисков или хранилища класса Premium.
  >



* [Пакетное Shipyard](https://github.com/Azure/batch-shipyard) автоматически настраивает hello GPU и RDMA toowork прозрачно контейнерного рабочих нагрузок на пакетной службы Azure. Для выполнения действий Batch Shipyard полностью полагается на файлы конфигурации. Существует много образец рецепт доступны конфигурации, позволяющие GPU и RDMA рабочих нагрузок, например hello [CNTK GPU рецепт](https://github.com/Azure/batch-shipyard/tree/master/recipes/CNTK-GPU-OpenMPI) которого выполняет предварительную настройку GPU драйверы на виртуальные машины серии N и загружает программного обеспечения Microsoft Когнитивных Toolkit как образ Docker.


## <a name="example-microsoft-mpi-on-an-a8-vm-pool"></a>Пример: Microsoft MPI в пуле виртуальной машины A8

toorun приложений Windows MPI в пуле узлов Azure A8, необходимо tooinstall поддерживаемой реализации MPI. Вот пример действия tooinstall [Microsoft MPI](https://msdn.microsoft.com/library/bb524831(v=vs.85).aspx) Windows и пула, с помощью пакета приложения пакета.

1. Загрузите hello [пакет установки](http://go.microsoft.com/FWLink/p/?LinkID=389556) (MSMpiSetup.exe) для hello последнюю версию Microsoft MPI.
2. Создайте ZIP-файл пакета hello.
3. Отправьте hello пакета tooyour пакетной учетной записи. Пошаговые инструкции см. в разделе hello [пакетов приложений](batch-application-packages.md) рекомендации. Укажите идентификатор приложения, например *MSMPI*, и его версию, например *8.1*. 
4. С помощью API-интерфейсы пакета hello или портал Azure, создание пула в конфигурации службы hello облака с hello требуемого числа узлов и масштаб. Hello Следующая таблица показывает пример tooset параметры копирования MPI в автоматическом режиме с помощью задачи запуска:

| Настройка | Значение |
| ---- | ----- | 
| **Тип образа** | Облачные службы |
| **Семейство ОС** | Windows Server 2012 R2 (семейство ОС 4) |
| **Размер узла** | A8 уровня "Стандартный" |
| **Включена связь между узлами** | Да |
| **Максимальное число заданий на узел** | 1 |
| **Ссылки на пакет приложения** | MSMPI |
| **Start task enabled** (Включена задача запуска) | Да<br>**Командная строка** - `"cmd /c %AZ_BATCH_APP_PACKAGE_MSMPI#8.1%\\MSMpiSetup.exe -unattend -force"`<br/>**Удостоверение пользователя.** Автоматический пользователь пула, администратор<br/>**Ожидать успешное выполнение.** True

## <a name="example-nvidia-tesla-drivers-on-nc-vm-pool"></a>Пример: драйверы NVIDIA Tesla в пуле виртуальных машин NC

toorun CUDA приложений в пуле узлов Linux NC, необходимо tooinstall CUDA Toolkit 8.0 на узлах hello. Hello Toolkit устанавливает необходимые драйверы NVIDIA Tesla GPU hello. Вот образец действия toodeploy пользовательского образа Ubuntu 16.04 LTS драйверов GPU hello.

1. Разверните виртуальную машину Azure NC6 под управлением Ubuntu 16.04 LTS. Например создайте hello виртуальной Машины в hello нам Южная центральном регионе. Убедитесь, что создание hello виртуальной Машины, с помощью стандартного хранилища и *без* управляемых дисках.
2. Выполните toohello tooconnect hello действия виртуальной Машины и [установки драйверов CUDA](../virtual-machines/linux/n-series-driver-setup.md#install-cuda-drivers-for-nc-vms).
3. Отзыв агент Linux hello и затем записать образ виртуальной Машины с Linux с помощью команд hello Azure CLI 1.0. Пошаговые инструкции см. в статье [Запись виртуальной машины Linux, работающей в Azure](../virtual-machines/linux/capture-image-nodejs.md). Запишите образ hello URI.
  > [!IMPORTANT]
  > Не использовать Azure CLI 2.0 команды toocapture hello изображение для пакета Azure. В настоящее время команды hello CLI 2.0 записывать только виртуальные машины, созданные с помощью управляемых дисков.
  >
4. Создайте учетную запись пакета, в конфигурации подписки пользователя hello в регионе, который поддерживает виртуальные машины NC.
5. С помощью API-интерфейсы пакета hello или портал Azure, создание пула с помощью пользовательского образа hello и с hello требуемого числа узлов и масштаб. Hello следующей таблице показаны параметры пула образец hello образа.

| Настройка | Значение |
| ---- | ---- |
| **Тип образа** | Пользовательский образ |
| **Пользовательский образ** | URI формы hello изображения`https://yourstorageaccountdisks.blob.core.windows.net/system/Microsoft.Compute/Images/vhds/MyVHDNamePrefix-osDisk.xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx.vhd` |
| **Номер SKU агента узла** | batch.node.ubuntu 16.04 |
| **Размер узла** | NC6 уровня "Стандартный" |



## <a name="next-steps"></a>Дальнейшие действия

* задания MPI toorun в пуле пакетной службы Azure см. hello [Windows](batch-mpi.md) или [Linux](https://blogs.technet.microsoft.com/windowshpc/2016/07/20/introducing-mpi-support-for-linux-on-azure-batch/) примеры.

* Примеры рабочих нагрузок GPU в пакете см. в разделе hello [Shipyard пакета](https://github.com/Azure/batch-shipyard/) рецептами.
