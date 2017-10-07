---
title: "Azure Site Recovery: вопросы и ответы | Документация Майкрософт"
description: "В этой статье приводятся ответы на распространенные вопросы об использовании Azure Site Recovery."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: вопросы и ответы
Данная статья содержит часто задаваемые вопросы об Azure Site Recovery. Если у вас есть вопросы этой статьи, задайте их на hello [форум по службам восстановления Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Общие сведения
### <a name="what-does-site-recovery-do"></a>Какие функции выполняет служба Site Recovery?
Site Recovery поддерживает, оркестрации и автоматизации репликации виртуальных машин Azure между регионами, локальных виртуальных машин и физических серверов tooAzure tooyour бесперебойной работе и стратегии аварийного восстановления (BCDR) и локальной машины tooa дополнительный центр обработки данных. [Подробнее](site-recovery-overview.md).

### <a name="what-can-site-recovery-protect"></a>Что можно защитить с помощью службы Site Recovery?
* **Виртуальные машины Azure**. Служба Site Recovery может реплицировать любую нагрузку, выполняющуюся на поддерживаемой виртуальной машине Azure.
* **Виртуальные машины Hyper-V**. Служба Site Recovery позволяет защитить любую рабочую нагрузку, запущенную на виртуальной машине Hyper-V.
* **Физические серверы**. Служба Site Recovery позволяет защитить физические серверы под управлением Windows или Linux.
* **Виртуальные машины VMware**. Служба Site Recovery позволяет защитить любую рабочую нагрузку, запущенную на виртуальной машине VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Site Recovery поддерживает модель hello диспетчера ресурсов Azure?
Site Recovery доступен в hello портал Azure с поддержкой для диспетчера ресурсов. Site Recovery поддерживает устаревший развертываний в hello классический портал Azure. Не удается создать новые хранилища классическом портале hello и новые функции не поддерживаются.

### <a name="can-i-replicate-azure-vms"></a>Можно ли выполнить репликацию виртуальных машин Azure?
Да, поддерживаемые виртуальные машины Azure можно реплицировать между регионами Azure. [Подробнее](site-recovery-azure-to-azure.md).

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>Каковы потребности в tooorchestrate репликации Hyper-V с Site Recovery?
Для сервера узла Hyper-V hello необходимые зависит от сценария развертывания hello. Проверьте hello требования Hyper-V в:

* [Репликация виртуальных машин Hyper-V (без VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [Репликация виртуальных машин Hyper-V (с помощью VMM) tooAzure](site-recovery-vmm-to-azure.md)
* [Дополнительный ЦОД tooa репликацию виртуальных машин Hyper-V](site-recovery-vmm-to-vmm.md)
* При реплицировании tooa вторичного центра обработки данных сведения о [поддерживаемых операционных системах для виртуальных машин Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Если выполняется репликация tooAzure, восстановление узла поддерживает все hello гостевых операционных систем, [поддерживается Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>Можно ли защитить виртуальные машины при запуске Hyper-V на клиентской операционной системе?
Нет, виртуальные машины должны быть расположены на сервере узла Hyper-V, который работает на компьютере под управлением поддерживаемой версии Windows Server. Если вам требуется tooprotect на клиентском компьютере можно выполнить репликацию ее как физический компьютер слишком[Azure](site-recovery-vmware-to-azure.md) или [дополнительный ЦОД](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Какие рабочие нагрузки можно защитить с помощью службы Site Recovery?
Tooprotect Site Recovery можно использовать большинство рабочих нагрузок на поддерживаемых виртуальная машина или физический сервер. Site Recovery обеспечивает поддержку поддержкой приложения репликации, чтобы приложения могут быть восстановлены tooan интеллектуальной состояния. Она интегрируется с приложениями Майкрософт, включая SharePoint, Exchange, Dynamics, SQL Server и Active Directory, а также тесно взаимодействует с решениями ведущих производителей, в том числе Oracle, SAP, IBM и Red Hat. [Подробнее](site-recovery-workload.md) о защите рабочей нагрузки.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Нужен ли узлы Hyper-V toobe в облаках VMM?
Если требуется tooreplicate tooa вторичный центр обработки данных, то виртуальные машины Hyper-V должны находиться в Hyper-V размещаются серверы, расположенные в облаке VMM. Следует tooreplicate tooAzure можно реплицировать виртуальные машины на несущих серверах Hyper-V с или без облака VMM. [Подробная информация](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>Можно ли развернуть службу Site Recovery с помощью VMM при наличии только одного сервера VMM?

Да. Можно выполнять репликацию виртуальных машин на серверах Hyper-V в tooAzure облака VMM hello, или можно выполнять репликацию между облаками VMM на hello же сервера. Для репликации tooon организациями в локальной среде рекомендуется иметь сервер VMM в hello первичных и вторичных сайтах.  

### <a name="what-physical-servers-can-i-protect"></a>Какие физические серверы можно защитить?
Можно реплицировать физические серверы под управлением Windows и Linux tooAzure или tooa вторичного сайта. [Узнайте](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) о требованиях к операционной системе.  Здравствуйте, применяются такие же требования к ли выполняется репликация физических серверов tooAzure или tooa вторичного сайта.


Обратите внимание, что если локальный сервер выйдет из строя, физические серверы запустятся в качестве виртуальных машин в Azure. Восстановление после сбоя tooan из локального физического сервера в настоящее время не поддерживается. Для компьютера, как физические вы можете только восстановление после сбоя tooa виртуальной машины VMware.

### <a name="what-vmware-vms-can-i-protect"></a>Какие виртуальные машины VMware можно защитить?

tooprotect виртуальных машин VMware необходимо vSphere низкоуровневой оболочки и виртуальных машин, работающих средства VMware. Также рекомендуется наличие гипервизорами VMware vCenter server toomanage hello. [Дополнительные сведения](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) о точные требования к репликации серверов VMware и tooAzure виртуальных машин или tooa вторичного сайта.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>Можно ли управлять аварийным восстановлением в офисах филиалов с помощью службы Site Recovery?
Да. При использовании Site Recovery tooorchestrate репликации и отработки отказа в филиалах, вы сможете получить единое orchestration и представление всех рабочих нагрузок office ветвь в центральном расположении. Можно легко выполнить переход на другой ресурс и администрировать аварийного восстановления все ветви из головного офиса, не заходя hello ветвей.

## <a name="pricing"></a>Цены

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Какие расходы я понесу при использовании Azure Site Recovery?
При использовании Site Recovery, с вас взимается плата за лицензии hello Site Recovery, хранилища Azure, транзакции с хранилищем и передачи исходящих данных. [Подробнее](https://azure.microsoft.com/pricing/details/site-recovery).

Лицензия Hello Site Recovery выполняется на уровне защищенных экземпляров, где экземпляр виртуальной Машины или физическом сервере.

- Если диска ВМ реплицирует tooa Стандартная учетная запись хранения, hello платы хранилища Azure — для использования хранилища hello. Например если размер диска hello источника используется 1 ТБ и 400 ГБ Site Recovery создает 1 ТБ VHD в Azure, но hello хранилища плата составляет 400 ГБ (плюс hello объем дискового пространства, используемый для журналов репликации).
- Если диск виртуальной Машины реплицирует tooa учетной записи хранения premium, hello платы хранилища Azure — для hello подготовить размер хранилища, округленное для hello ближайшего параметр диска для хранения premium. Например если размер диска источника hello составляет 50 ГБ, Site Recovery создает 50 ГБ дискового в Azure и Azure сопоставляет этот toohello ближайшего диска хранилища premium (P10).  Затраты рассчитываются на P10, а не на hello 50 ГБ места на диске.  [Подробнее](https://aka.ms/premium-storage-pricing).  При использовании хранилища premium также необходима учетная запись стандартного хранилища для ведения журнала репликации и также оплачивается hello объем стандартное пространство, используемое для этих журналов.
- Диски не создаются до тестовой отработки отказа или отработки отказа. В состоянии репликации hello, хранения расходов hello категории «страничный большой двоичный объект и диск» согласно hello [калькулятор хранения](https://azure.microsoft.com/en-in/pricing/calculator/) зависят от числа. Эти расходы основаны на тип хранения hello premium и standard и hello избыточности данных введите - LRS, GRS, RA-GRS и т. д.
- Если параметр toouse hello управляемых дисках на отработки отказа выбран, [расходов для управляемых дисков](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) применить после отработки отказа или тестовая отработка отказа. Тарифы для управляемых дисков не применяются во время репликации.
- Если диски toouse управляемый параметр hello в отказоустойчивом не выбран, хранения расходов hello категории «страничный большой двоичный объект и диск» согласно hello [калькулятор хранения](https://azure.microsoft.com/en-in/pricing/calculator/) нагрузки после отработки отказа. Эти расходы основаны на тип хранения hello premium и standard и hello избыточности данных введите - LRS, GRS, RA-GRS и т. д.
- Плата за транзакции с хранилищем начисляется во время репликации устойчивого состояния и за обычную работу виртуальной машины после отработки отказа или тестовой отработки отказа. Но эти издержки незначительны.

Во время тестовой отработки отказа, где будут применены стоимость операций hello ВМ, хранилища, хранилища и исходящего трафика также накопления затрат.



## <a name="security"></a>Безопасность
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Отправляются ли данные репликации службы Site Recovery toohello?
Нет, служба Site Recovery не перехватывает реплицируемые данные и не получает сведения о компонентах, запущенных на ваших виртуальных машинах или физических серверах.
Обмен данными репликации осуществляется между локальными узлами Hyper-V, низкоуровневыми оболочками VMware или физическими серверами и хранилищем Azure или дополнительным сайтом. Site Recovery имеет toointercept нет возможности этих данных. Только метаданные hello нужны tooorchestrate репликации и отработки отказа отправляются toohello службы Site Recovery.  

Site Recovery является ISO 27001: 2013, 27018, HIPAA, DPA сертификацию и в процессе hello SOC2 и FedRAMP JAB оценку.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Для обеспечения соответствия должен оставаться даже наши метаданные в локальной среде, в пределах hello одной географической области. Может ли служба Site Recovery помочь нам?
Да. При создании хранилище Site Recovery в регионе, мы убедитесь, что все метаданные, которые нам нужна tooenable и координировать репликации и отработки отказа в этом регионе географической границы.

### <a name="does-site-recovery-encrypt-replication"></a>Выполняет ли служба Site Recovery шифрование репликации?
При репликации виртуальных машин и физических серверов между локальными сайтами поддерживается шифрование в процессе передачи. Для виртуальных машин и физических серверов, репликация tooAzure оба шифрования передачи и [шифрования статических (в Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) поддерживаются.

## <a name="replication"></a>Репликация

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>Можно ли реплицировать через tooAzure сеть сеть VPN
Azure Site Recovery реплицирует учетной записи хранилища Azure tooan данных через общедоступную конечную точку. Репликация не выполняется через VPN-подключение типа "сеть — сеть". Вы можете создать такое подключение с помощью виртуальной сети Azure. Это никак не повлияет на репликацию Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>Можно использовать tooAzure виртуальные машины tooreplicate ExpressRoute?
Да, ExpressRoute может быть tooAzure tooreplicate используемых виртуальных машин. Azure Site Recovery реплицирует tooan данных учетной записи хранилища Azure через общедоступную конечную точку. Требуется tooset копирование [открытый пиринг](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute для восстановления сайта репликации. После hello виртуальных машин был перемещен tooan виртуальной сети Azure можно использовать их с помощью hello [частного пиринга](../expressroute/expressroute-circuit-peerings.md#private-peering) программу установки с hello виртуальной сети Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Существуют ли все необходимые компоненты для репликации виртуальных машин tooAzure?
Требуется tooreplicate tooAzure виртуальные машины должны соответствовать [требования Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

Учетная запись пользователя Azure должен toohave определенных [разрешений](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable репликацию новых tooAzure виртуальной машины.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>Как реплицировать tooAzure виртуальных машин второго поколения Hyper-V?
Да. Site Recovery преобразует из поколения 2 toogeneration 1 во время отработки отказа. Восстановление после сбоя hello машины является преобразованный задней toogeneration 2. [Подробная информация](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Если реплицировать tooAzure способ оплаты для виртуальных машин Azure?
Во время обычной репликации данные реплицируемой toogeo избыточности хранилища Azure и не требуется toopay любой виртуальной машине Azure IaaS накладные расходы, предоставляя значительное преимущество. При запуске tooAzure перехода на другой ресурс, Site Recovery автоматически создает виртуальные машины Azure IaaS, и после этого вам будет выставлен счет для hello вычислительных ресурсов, которые используют в Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>Можно ли автоматизировать сценарии Site Recovery с помощью пакета SDK?
Да. Можно автоматизировать с помощью API-интерфейса Rest hello, PowerShell или hello Azure SDK рабочие процессы аварийного восстановления сайта. Ниже перечислены сценарии развертывания Site Recovery с помощью PowerShell, которые поддерживаются в настоящее время.

* [Репликация виртуальных машин Hyper-V в облаках VMM tooAzure PowerShell диспетчера ресурсов](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Репликация виртуальных машин Hyper-V без VMM tooAzure PowerShell диспетчера ресурсов](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>Если реплицировать tooAzure тип учетной записи хранилища требуется?
* **Классический портал Azure**: Если вы развертываете Site Recovery в hello классический портал Azure, вам потребуется [географически избыточную учетную запись хранения standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Хранилище класса Premium в настоящее время не поддерживается. Учетная запись Hello должна быть в hello же регионе, что хранилище Site Recovery hello.
* **Портал Azure**: Если вы развертываете Site Recovery в hello портал Azure, вам потребуется учетной записи хранения LRS и GRS. Рекомендуется GRS данные устойчива региональном сбое происходит ли основной регион hello не может быть восстановлена. Учетная запись Hello должна быть в hello же регионе, что hello в хранилище служб восстановления. Хранилище Premium теперь поддерживается для виртуальной Машины VMware, виртуальных Машин Hyper-V и репликации физического сервера при развертывании в hello портала Azure Site Recovery.

### <a name="how-often-can-i-replicate-data"></a>Как часто можно реплицировать данные?
* **Hyper-V.** Виртуальные машины Hyper-V можно реплицировать каждые 30 секунд (но не для хранилища класса Premium), 5 или 15 минут. При настройке репликации сети SAN репликация является синхронной.
* **VMware и физические серверы.** Здесь частота репликации не имеет значения. Репликация является непрерывной.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>Можно расширить репликации из существующего сайта tooanother третичные сайт восстановления?
Расширенная репликация и цепочка репликации не поддерживаются. Запросите эту функцию на [форуме отзывов и предложений](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>Возможности репликации в автономном режиме hello реплицировать tooAzure первый раз?
Эта возможность не поддерживается. Запросить эту функцию в hello [форуме обратной связи](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>Можно ли исключить из репликации отдельные диски?
Эта возможность поддерживается, когда вы будете [репликация виртуальных машин VMware и виртуальных машин Hyper-V](site-recovery-exclude-disk.md) tooAzure, с помощью портала Azure hello.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>Можно ли реплицировать виртуальные машины с динамическими дисками?
Динамические диски поддерживаются при репликации виртуальных машин Hyper-V. Они также поддерживаются, если репликация виртуальных машин VMware и физических машин tooAzure. диск операционной системы Hello должен представлять собой базовый диск.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>Можно добавить новый tooan машины существующие группы репликации
Добавление новых групп репликации tooexisting машин поддерживается. toodo таким образом, выберите группы репликации hello (из колонки «Реплицированные элементы») и щелкните правой кнопкой мыши и выберите пункт контекстного меню для группы репликации hello и выберите соответствующий параметр hello.

![Добавить группу tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>Можно ли регулировать пропускную способность, выделенную для трафика репликации Hyper-V?
Да. Вы можете прочитать больше о регулирование полосы пропускания в статьях hello развертывания:

* [Планирование ресурсов для репликации виртуальных машин VMware и физических серверов](site-recovery-plan-capacity-vmware.md)
* [Планирование ресурсов для репликации виртуальных машин Hyper-V в облаках VMM](site-recovery-vmm-to-azure.md#capacity-planning)
* [Планирование ресурсов для репликации виртуальных машин Hyper-V без VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Отработка отказа
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Если я отработка отказа tooAzure, как открывать hello Azure виртуальные машины после отработки отказа?
Можно получить доступ к hello виртуальных машинах Azure через безопасное подключение к Интернету через VPN сайтами и через Azure ExpressRoute. Вам потребуется tooprepare количество действий в tooconnect порядке. [Дополнительные сведения](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Если я при сбое как Azure убедитесь, что tooAzure устойчива Мои данные?
Среда Azure разработана для обеспечения отказоустойчивости. Site Recovery уже разработан для отработки отказа tooa дополнительный ЦОД Azure, в соответствии с приветствия возникает SLA Azure, если требуется hello. Если это происходит, мы гарантируем, метаданные и хранилищ оставаться в пределах hello одной географической области, выбранного в хранилище.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Что произойдет, если при выполнении репликации между двумя центрами обработки данных в основном центре обработки данных неожиданно возникнет сбой?
Вы можете активировать незапланированной отработки отказа от hello вторичного сайта. Site Recovery не требует подключения tooperform hello hello первичного сайта перехода на другой ресурс.

### <a name="is-failover-automatic"></a>Отработка отказа выполняется автоматически?
Отработка отказа не выполняется автоматически. Инициировать переход на другой ресурс с одним щелчком на портале hello, или можно использовать [PowerShell восстановления сайта](/powershell/module/azurerm.siterecovery) tootrigger отработки отказа. Сбоя — простое действие hello портале Site Recovery.

tooautomate, который можно использовать в локальной среде Orchestrator или Operations Manager toodetect сбоя виртуальной машины, а затем триггер hello отработки отказа с помощью пакета SDK "hello".

* Дополнительные сведения о планах восстановления см. [здесь](site-recovery-create-recovery-plans.md).
* [Узнайте больше](site-recovery-failover.md) об отработке отказа.
* [Узнайте больше](site-recovery-failback-azure-to-vmware.md) о восстановлении размещения виртуальных машин VMware и физических серверов.

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Если мой локального узла не отвечает или зависших, можно ли отработка отказа узла различные обратного tooa?
Да, можно использовать hello альтернативное расположение восстановления toofailback tooa другой узел из Azure. Подробнее о параметрах hello hello следующие ссылки для виртуальных машин VMware и Hyper-v.

* [Для виртуальных машин VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Для виртуальных машин Hyper-V](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Поставщики услуг
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Я являюсь поставщиком услуг. Работает ли служба Site Recovery для моделей выделенной и общей инфраструктуры?
Да, Site Recovery поддерживает как выделенную, так и общую модели инфраструктуры.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Для поставщика службы — идентификатор hello моему клиенту, совместно со службой восстановления сайтов hello?
Нет. Клиент остается анонимным. Клиентам не требуется доступ toohello восстановление узла портала. Только администратор службы поставщика hello взаимодействует с портала hello.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Данные клиента приложения никогда не переходят tooAzure?
При репликации между сайтами, принадлежащие поставщика службы данных приложения никогда не передаются tooAzure. Данные шифруются во время передачи и реплицированных напрямую между hello сайтам поставщиков услуг.

Если выполняется репликация tooAzure, данные приложения отправляется tooAzure хранилище, но не toohello службы Site Recovery. Данные шифруются в процессе передачи и остаются зашифрованными в Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>Будут ли клиенты получать счета за какие-либо службы Azure?
Нет. Отношения оплаты Azure — непосредственно с поставщиком услуг hello. Поставщики служб отвечают за создание специальных счетов для своих клиентов.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Если я репликация tooAzure, нам нужно toorun виртуальных машин в Azure все время?
Нет, данные — реплицированные tooan учетной записи хранилища Azure в вашей подписке. При тестовой отработке отказа (отработке аварийного восстановления) или фактической отработке отказа Site Recovery автоматически создает виртуальные машины в вашей подписке.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>Обеспечить изоляцию на уровне клиента при репликации tooAzure?
Да.

### <a name="what-platforms-do-you-currently-support"></a>Какие платформы поддерживаются на данный момент?
Поддерживаются развертывания на основе Azure Pack, системы облачной платформы и System Center 2012 и более поздних версий. [Узнайте больше](https://technet.microsoft.com/library/dn850370.aspx) об интеграции Azure Pack и Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Поддерживаются ли отдельные развертывания Azure Pack или односерверные развертывания VMM?
Да, можно реплицировать tooAzure виртуальных машин Hyper-V, или между сайтами поставщика службы.  Обратите внимание, что при репликации между сайтами поставщика услуг интеграция Runbook Azure недоступна.

## <a name="next-steps"></a>Дальнейшие действия
* Чтение hello [Обзор Site Recovery](site-recovery-overview.md)
* Ознакомьтесь с [архитектурой Site Recovery](site-recovery-components.md).  
