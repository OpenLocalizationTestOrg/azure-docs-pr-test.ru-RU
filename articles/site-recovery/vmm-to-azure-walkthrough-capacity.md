---
title: "aaaPlan емкости и масштабирования для tooAzure репликации (с помощью VMM) виртуальных Машин Hyper-V с помощью Azure Site Recovery | Документы Microsoft"
description: "Использовать статьи tooplan емкости и масштабирования при репликации виртуальных машин Hyper-V в VMM облаков tooAzure с Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 41c3c83e-6b1a-496a-8179-498c552ef0c7
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 9818ada9bb21f60ac00b3894696201b06630cb2b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-3-plan-capacity-and-scaling-for-hyper-v-with-vmm-tooazure-replication"></a>Шаг 3: Планирование емкости и масштабирования для tooAzure репликации Hyper-V (с помощью VMM)

После знакомства hello [необходимые условия для развертывания](vmm-to-azure-walkthrough-prerequisites.md), использовать этот toofigure статьи о планировании емкости и масштабирования, при репликации локальных виртуальных машин Hyper-V в tooAzure облаках диспетчера виртуальных машин System Center (VMM), с [Azure Site Recovery](site-recovery-overview.md).

После считывания в этой статье, отправлять любые комментарии внизу hello или задавайте технические вопросы на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="how-do-i-start-capacity-planning"></a>С чего начать планирование загрузки?


Можно собирать сведения о вашей среды репликации, а затем емкость плана с использованием данных hello, а также вопросы hello выделено в этой статье.


## <a name="gather-information"></a>Сбор сведений

1. Соберите сведения о среде репликации, включая информацию о виртуальных машинах, количестве дисков на виртуальную машину и объеме хранилища на диск.
2. Определите частоту ежедневных изменений (обновлений) реплицированных данных. Загрузите hello [средства планирования емкости Hyper-V](https://www.microsoft.com/download/details.aspx?id=39057) скорость изменения tooget hello. Мы рекомендуем установить это средство по toocapture недели средние значения.
 

## <a name="figure-out-capacity"></a>Планирование ресурсов

На основании hello информации после сбора сведений запустите hello [планировщика емкости восстановления сайта](http://aka.ms/asr-capacity-planner-excel) tooanalyze исходной среде и рабочих нагрузок, Оценка требований к пропускной способности и ресурсов сервера для расположения источника hello и hello ресурсы (виртуальные машины и хранилища и т. д), необходимые в целевом расположении hello. Можно запустить средство hello в нескольких режимах.

- Быстрый планирования: запустите средство hello в этом режиме tooget сети и серверов проекции, основанные на среднее количество виртуальных машин, диски, хранилища и скорость изменения.
- Подробные планирования: запустите средство hello в этом режиме и укажите сведения о каждой рабочей нагрузки на уровне виртуальной Машины. Проанализируйте совместимость виртуальной машины и получите проекции сети и сервера.

Теперь запустите средство hello.

1. Загрузите hello [средства](http://aka.ms/asr-capacity-planner-excel)
2. Быстрый планировщик toorun hello, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-quick-planner)и выберите hello сценарий **tooAzure Hyper-V**.
3. toorun Здравствуйте подробные планировщик, выполните [эти инструкции](site-recovery-capacity-planner.md#run-the-detailed-planner)и выберите hello сценарий **tooAzure Hyper-V**.

## <a name="control-network-bandwidth"></a>Управление пропускной способностью сети

После вычисляемых hello пропускной способности, необходимые, у вас есть два способа управления hello объем пропускной способности, используемой для репликации:

* **Регулирование полосы пропускания**: Hyper-V реплицирует tooAzure трафик проходит через конкретного узла Hyper-V. Можно отрегулировать пропускной способности на сервере узла hello.
* **Повлиять на пропускную способность**: вы можете влиять hello пропускной способности, используемой для репликации несколько разделов реестра.

### <a name="throttle-bandwidth"></a>Регулирование пропускной способности
1. Откройте hello Microsoft Azure Backup MMC оснастку на сервере узла Hyper-V hello. По умолчанию для быстрого архивации Microsoft Azure доступна на рабочем столе hello, или в C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. В оснастке hello щелкните **изменить свойства**.
3. На hello **регулирование** выберите **включить регулирования для операций резервного копирования использование пропускной способности Интернета**и ограничить hello для рабочих и нерабочих часов. Допустимые диапазоны: от 512 Кбит/с too102 Мбит/с в секунду.

    ![Регулирование пропускной способности](./media/vmm-to-azure-walkthrough-capacity/throttle2.png)

Можно также использовать hello [Set-OBMachineSetting](https://technet.microsoft.com/library/hh770409.aspx) регулирования tooset командлета. Рассмотрим пример:

    $mon = [System.DayOfWeek]::Monday
    $tue = [System.DayOfWeek]::Tuesday
    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth  (512*1024) -NonWorkHourBandwidth (2048*1024)

**Set-OBMachineSetting -NoThrottle** указывает, что регулирование не требуется.

### <a name="influence-network-bandwidth"></a>Изменение пропускной способности сети
1. В реестре hello перейдите слишком**Backup\Replication Azure параметру**.
   * tooinfluence hello пропускную способность трафика репликации диска изменить значение hello hello **UploadThreadsPerVM**, или создать ключ hello в том случае, если он не существует.
   * пропускная способность hello tooinfluence для восстановления размещения трафик из Azure, измените значение hello **DownloadThreadsPerVM**.
2. значение по умолчанию Hello — 4. В сети «избыточная Подготовка» следует изменить эти разделы реестра из значения по умолчанию hello. Hello максимальное — 32. Мониторинг трафика toooptimize hello значение.

## <a name="next-steps"></a>Дальнейшие действия

Go слишком[шаг 4: Планирование сети](vmm-to-azure-walkthrough-network.md).
