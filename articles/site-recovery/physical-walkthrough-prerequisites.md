---
title: "aaaPrerequisites для физического сервера tooAzure репликации с помощью Azure Site Recovery | Документы Microsoft"
description: "Hello приводятся сводные сведения об репликации рабочих нагрузок на физических серверах tooAzure Windows и Linux, с помощью службы Azure Site Recovery hello."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 318156ba-793b-48d0-98d4-cc5436bf28a3
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: b0ed53a143079877a2ad21ee17aae5510e0dc058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-physical-server-tooazure-replication"></a>Шаг 2: Проверьте hello компоненты на физическом сервере tooAzure репликации

Ознакомьтесь с необходимыми условиями hello, представленные в таблице hello.


**Предварительные требования** | **Дополнительные сведения**
--- | ---
**Таблицы Azure** | Ознакомьтесь с [требованиями Azure](site-recovery-prereq.md#azure-requirements).
**Локальный сервер конфигурации** | Вам потребуется физический сервер или виртуальная машина VMware под управлением Windows Server 2012 R2 или более поздней версии. Настройте этот сервер при развертывании Site Recovery.<br/><br/> По умолчанию hello процессом и главного целевого сервера также будут установлены на этом компьютере. При увеличении масштаба может понадобиться отдельный сервер обработки. В противном случае он имеет hello же требованиям, что сервер конфигурации hello.<br/><br/> [Подробнее](site-recovery-set-up-vmware-to-azure.md#configuration-server-minimum-requirements).
**Локальные виртуальные машины** | Машины, нужно tooreplicate должна быть запущена [поддерживаемой операционной системы](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions) и соответствовать [Azure необходимые условия](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL-адреса** | Сервер конфигурации Hello должен иметь доступ к toothese URL-адреса:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Если правила брандмауэра на основе адресов IP, убедитесь, что они позволяют tooAzure связи.<br/></br> Разрешить hello [диапазоны IP-адресов центра обработки данных Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)и hello порта HTTPS (443).<br/></br> Разрешить диапазоны IP-адресов для hello регион Azure, подписки и Запад США (используется для контроля доступа и удостоверений).<br/><br/> Разрешить этот URL-адрес для загрузки MySQL hello: http://cdn.mysql.com/archives/mysql-5.5/mysql-5.5.37-win32.msi.
**Служба Mobility Service** | Должна быть установлена на каждом реплицированном сервере.




## <a name="limitations"></a>Ограничения

Обратите внимание на ограничения hello, приведены в таблице hello перед развертыванием.

**Ограничения** | **Дополнительные сведения**
--- | ---
**Таблицы Azure** | Учетные записи хранилища и сети должны быть в hello же регионе, что хранилище hello<br/><br/> Если вы используете учетную запись хранения premium, необходимо также стандарт хранения журналов репликации toostore учетной записи<br/><br/> Не удается выполнить репликацию учетных записей toopremium в центральной и Южной Индии.
**Локальный сервер конфигурации** | При использовании виртуальной Машины VMware в качестве машины сервера конфигурации hello hello тип адаптера виртуальной Машины VMware должно быть VMXNET3. В обратном случае [установите это обновление](https://kb.vmware.com/selfservice/microsites/search.do?cmd=displayKC&docType=kc&externalId=2110245&sliceId=1&docTypeID=DT_KB_1_1&dialogID=26228401&stateId=1).<br/><br/> При использовании виртуальной машины VMware на ней нужно установить vSphere PowerCLI 6.0.<br/><br> Hello машины не должен быть контроллером домена.<br/><br/> Hello компьютер должен иметь статический IP-адрес.<br/><br/> Hello имя узла должно быть 15 символов или меньше, и операционная система должна быть на английском языке.
**Репликация компьютеров** | Проверьте [ограничения виртуальной машины Azure](site-recovery-prereq.md#azure-requirements).<br/><br/> Нельзя реплицировать виртуальные машины с зашифрованными дисками или дисками с типом загрузки UEFI или EFI.<br/><br> Кластеры общих дисков не поддерживаются. Если объединение Сетевых карт hello исходной виртуальной Машины, он преобразуется tooa один сетевой Адаптер после отработки отказа.<br/><br/> Если виртуальные машины iSCSI-диск, его преобразует Site Recovery tooa VHD-файл после отработки отказа. При достижении цели iSCSI hello, hello виртуальной Машины Azure подключается tooit и видит и hello виртуального жесткого диска. В этом случае отключите hello цели iSCSI.<br/><br/> Если непротиворечивости tooenable нескольких виртуальных Машин, что позволяет восстановить же рабочая нагрузка toobe hello работающих виртуальных машин вместе tooa согласованные данные точек, откройте порт 20004 hello виртуальной Машины.<br/><br/> Необходимо установить Windows на диск hello C. диск ОС Hello должен быть базовый, а не динамические. диск данных Hello могут быть динамическими.<br/><br/> Файл/etc/hosts Linux на виртуальных машинах, должен содержать записи, которые сопоставляют hello имя локального узла tooIP адреса, связанные со всеми сетевыми адаптерами. Здравствуйте, имя узла, точек подключения, имя устройства, пути к системным папкам и имена файлов (/ etc; / usr) должно быть только на английском языке.<br/><br/> Поддерживаются определенные типы [хранилищ Linux](site-recovery-support-matrix-to-azure.md#support-for-storage).<br/><br/>Создать или установить **disk.enableUUID=true** в параметрах виртуальной Машины hello. Это обеспечивает согласованного toohello UUID VMDK-ФАЙЛ, который подключает правильно и обеспечивает только незначительные изменения передаются назад tooon организациями во время восстановления размещения без полной репликации.


## <a name="next-steps"></a>Дальнейшие действия

- При выполнении полного развертывания, перейдите в слишком[Step 3: Планирование емкости](physical-walkthrough-capacity.md)
- Если вы выполняете развертывание простых тестов, слишком перейдите[шаг 4: Планирование сети](physical-walkthrough-network.md).
