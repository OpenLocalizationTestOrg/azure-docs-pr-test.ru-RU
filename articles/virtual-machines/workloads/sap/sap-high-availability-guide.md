---
title: "Виртуальные машины высокой доступности для SAP NetWeaver aaaAzure | Документы Microsoft"
description: "Руководство по обеспечению высокого уровня доступности для SAP NetWeaver на виртуальных машинах Azure"
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: goraco
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 05/05/2017
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 662dd793390d7f6138b160ed86259d13391336aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-virtual-machines-high-availability-for-sap-netweaver"></a>Руководство по обеспечению высокого уровня доступности SAP NetWeaver на виртуальных машинах Azure

[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2243692]:https://launchpad.support.sap.com/#/notes/2243692

[sap-installation-guides]:http://service.sap.com/instguides

[azure-subscription-service-limits]:../../../azure-subscription-service-limits.md
[azure-subscription-service-limits-subscription]:../../../azure-subscription-service-limits.md

[dbms-guide]:../../virtual-machines-windows-sap-dbms-guide.md

[deployment-guide]:deployment-guide.md

[dr-guide-classic]:http://go.microsoft.com/fwlink/?LinkID=521971

[getting-started]:get-started.md

[ha-guide]:sap-high-availability-guide.md

[planning-guide]:planning-guide.md
[planning-guide-11]:planning-guide.md
[planning-guide-2.1]:planning-guide.md#1625df66-4cc6-4d60-9202-de8a0b77f803
[planning-guide-2.2]:planning-guide.md#f5b3b18c-302c-4bd8-9ab2-c388f1ab3d10

[planning-guide-microsoft-azure-networking]:planning-guide.md#61678387-8868-435d-9f8c-450b2424f5bd
[planning-guide-storage-microsoft-azure-storage-and-data-disks]:planning-guide.md#a72afa26-4bf4-4a25-8cf7-855d6032157f

[sap-ha-guide]:sap-high-availability-guide.md
[sap-ha-guide-2]:#42b8f600-7ba3-4606-b8a5-53c4f026da08
[sap-ha-guide-4]:#8ecf3ba0-67c0-4495-9c14-feec1a2255b7
[sap-ha-guide-8]:#78092dbe-165b-454c-92f5-4972bdbef9bf
[sap-ha-guide-8.1]:#c87a8d3f-b1dc-4d2f-b23c-da4b72977489
[sap-ha-guide-8.9]:#fe0bd8b5-2b43-45e3-8295-80bee5415716
[sap-ha-guide-8.11]:#661035b2-4d0f-4d31-86f8-dc0a50d78158
[sap-ha-guide-8.12]:#0d67f090-7928-43e0-8772-5ccbf8f59aab
[sap-ha-guide-8.12.1]:#5eecb071-c703-4ccc-ba6d-fe9c6ded9d79
[sap-ha-guide-8.12.3]:#5c8e5482-841e-45e1-a89d-a05c0907c868
[sap-ha-guide-8.12.3.1]:#1c2788c3-3648-4e82-9e0d-e058e475e2a3
[sap-ha-guide-8.12.3.2]:#dd41d5a2-8083-415b-9878-839652812102
[sap-ha-guide-8.12.3.3]:#d9c1fc8e-8710-4dff-bec2-1f535db7b006
[sap-ha-guide-9]:#a06f0b49-8a7a-42bf-8b0d-c12026c5746b
[sap-ha-guide-9.1]:#31c6bd4f-51df-4057-9fdf-3fcbc619c170
[sap-ha-guide-9.1.1]:#a97ad604-9094-44fe-a364-f89cb39bf097

[sap-ha-multi-sid-guide]:sap-high-availability-multi-sid.md (SAP multi-SID high-availability configuration)


[sap-ha-guide-figure-1000]:./media/virtual-machines-shared-sap-high-availability-guide/1000-wsfc-for-sap-ascs-on-azure.png
[sap-ha-guide-figure-1001]:./media/virtual-machines-shared-sap-high-availability-guide/1001-wsfc-on-azure-ilb.png
[sap-ha-guide-figure-1002]:./media/virtual-machines-shared-sap-high-availability-guide/1002-wsfc-sios-on-azure-ilb.png
[sap-ha-guide-figure-2000]:./media/virtual-machines-shared-sap-high-availability-guide/2000-wsfc-sap-as-ha-on-azure.png
[sap-ha-guide-figure-2001]:./media/virtual-machines-shared-sap-high-availability-guide/2001-wsfc-sap-ascs-ha-on-azure.png
[sap-ha-guide-figure-2003]:./media/virtual-machines-shared-sap-high-availability-guide/2003-wsfc-sap-dbms-ha-on-azure.png
[sap-ha-guide-figure-2004]:./media/virtual-machines-shared-sap-high-availability-guide/2004-wsfc-sap-ha-e2e-archit-template1-on-azure.png
[sap-ha-guide-figure-2005]:./media/virtual-machines-shared-sap-high-availability-guide/2005-wsfc-sap-ha-e2e-arch-template2-on-azure.png

[sap-ha-guide-figure-3000]:./media/virtual-machines-shared-sap-high-availability-guide/3000-template-parameters-sap-ha-arm-on-azure.png
[sap-ha-guide-figure-3001]:./media/virtual-machines-shared-sap-high-availability-guide/3001-configuring-dns-servers-for-Azure-vnet.png
[sap-ha-guide-figure-3002]:./media/virtual-machines-shared-sap-high-availability-guide/3002-configuring-static-IP-address-for-network-card-of-each-vm.png
[sap-ha-guide-figure-3003]:./media/virtual-machines-shared-sap-high-availability-guide/3003-setup-static-ip-address-ilb-for-ascs-instance.png
[sap-ha-guide-figure-3004]:./media/virtual-machines-shared-sap-high-availability-guide/3004-default-ascs-scs-ilb-balancing-rules-for-azure-ilb.png
[sap-ha-guide-figure-3005]:./media/virtual-machines-shared-sap-high-availability-guide/3005-changing-ascs-scs-default-ilb-rules-for-azure-ilb.png
[sap-ha-guide-figure-3006]:./media/virtual-machines-shared-sap-high-availability-guide/3006-adding-vm-to-domain.png
[sap-ha-guide-figure-3007]:./media/virtual-machines-shared-sap-high-availability-guide/3007-config-wsfc-1.png
[sap-ha-guide-figure-3008]:./media/virtual-machines-shared-sap-high-availability-guide/3008-config-wsfc-2.png
[sap-ha-guide-figure-3009]:./media/virtual-machines-shared-sap-high-availability-guide/3009-config-wsfc-3.png
[sap-ha-guide-figure-3010]:./media/virtual-machines-shared-sap-high-availability-guide/3010-config-wsfc-4.png
[sap-ha-guide-figure-3011]:./media/virtual-machines-shared-sap-high-availability-guide/3011-config-wsfc-5.png
[sap-ha-guide-figure-3012]:./media/virtual-machines-shared-sap-high-availability-guide/3012-config-wsfc-6.png
[sap-ha-guide-figure-3013]:./media/virtual-machines-shared-sap-high-availability-guide/3013-config-wsfc-7.png
[sap-ha-guide-figure-3014]:./media/virtual-machines-shared-sap-high-availability-guide/3014-config-wsfc-8.png
[sap-ha-guide-figure-3015]:./media/virtual-machines-shared-sap-high-availability-guide/3015-config-wsfc-9.png
[sap-ha-guide-figure-3016]:./media/virtual-machines-shared-sap-high-availability-guide/3016-config-wsfc-10.png
[sap-ha-guide-figure-3017]:./media/virtual-machines-shared-sap-high-availability-guide/3017-config-wsfc-11.png
[sap-ha-guide-figure-3018]:./media/virtual-machines-shared-sap-high-availability-guide/3018-config-wsfc-12.png
[sap-ha-guide-figure-3019]:./media/virtual-machines-shared-sap-high-availability-guide/3019-assign-permissions-on-share-for-cluster-name-object.png
[sap-ha-guide-figure-3020]:./media/virtual-machines-shared-sap-high-availability-guide/3020-change-object-type-include-computer-objects.png
[sap-ha-guide-figure-3021]:./media/virtual-machines-shared-sap-high-availability-guide/3021-check-box-for-computer-objects.png
[sap-ha-guide-figure-3022]:./media/virtual-machines-shared-sap-high-availability-guide/3022-set-security-attributes-for-cluster-name-object-on-file-share-quorum.png
[sap-ha-guide-figure-3023]:./media/virtual-machines-shared-sap-high-availability-guide/3023-call-configure-cluster-quorum-setting-wizard.png
[sap-ha-guide-figure-3024]:./media/virtual-machines-shared-sap-high-availability-guide/3024-selection-screen-different-quorum-configurations.png
[sap-ha-guide-figure-3025]:./media/virtual-machines-shared-sap-high-availability-guide/3025-selection-screen-file-share-witness.png
[sap-ha-guide-figure-3026]:./media/virtual-machines-shared-sap-high-availability-guide/3026-define-file-share-location-for-witness-share.png
[sap-ha-guide-figure-3027]:./media/virtual-machines-shared-sap-high-availability-guide/3027-successful-reconfiguration-cluster-file-share-witness.png
[sap-ha-guide-figure-3028]:./media/virtual-machines-shared-sap-high-availability-guide/3028-install-dot-net-framework-35.png
[sap-ha-guide-figure-3029]:./media/virtual-machines-shared-sap-high-availability-guide/3029-install-dot-net-framework-35-progress.png
[sap-ha-guide-figure-3030]:./media/virtual-machines-shared-sap-high-availability-guide/3030-sios-installer.png
[sap-ha-guide-figure-3031]:./media/virtual-machines-shared-sap-high-availability-guide/3031-first-screen-sios-data-keeper-installation.png
[sap-ha-guide-figure-3032]:./media/virtual-machines-shared-sap-high-availability-guide/3032-data-keeper-informs-service-be-disabled.png
[sap-ha-guide-figure-3033]:./media/virtual-machines-shared-sap-high-availability-guide/3033-user-selection-sios-data-keeper.png
[sap-ha-guide-figure-3034]:./media/virtual-machines-shared-sap-high-availability-guide/3034-domain-user-sios-data-keeper.png
[sap-ha-guide-figure-3035]:./media/virtual-machines-shared-sap-high-availability-guide/3035-provide-sios-data-keeper-license.png
[sap-ha-guide-figure-3036]:./media/virtual-machines-shared-sap-high-availability-guide/3036-data-keeper-management-config-tool.png
[sap-ha-guide-figure-3037]:./media/virtual-machines-shared-sap-high-availability-guide/3037-tcp-ip-address-first-node-data-keeper.png
[sap-ha-guide-figure-3038]:./media/virtual-machines-shared-sap-high-availability-guide/3038-create-replication-sios-job.png
[sap-ha-guide-figure-3039]:./media/virtual-machines-shared-sap-high-availability-guide/3039-define-sios-replication-job-name.png
[sap-ha-guide-figure-3040]:./media/virtual-machines-shared-sap-high-availability-guide/3040-define-sios-source-node.png
[sap-ha-guide-figure-3041]:./media/virtual-machines-shared-sap-high-availability-guide/3041-define-sios-target-node.png
[sap-ha-guide-figure-3042]:./media/virtual-machines-shared-sap-high-availability-guide/3042-define-sios-synchronous-replication.png
[sap-ha-guide-figure-3043]:./media/virtual-machines-shared-sap-high-availability-guide/3043-enable-sios-replicated-volume-as-cluster-volume.png
[sap-ha-guide-figure-3044]:./media/virtual-machines-shared-sap-high-availability-guide/3044-data-keeper-synchronous-mirroring-for-SAP-gui.png
[sap-ha-guide-figure-3045]:./media/virtual-machines-shared-sap-high-availability-guide/3045-replicated-disk-by-data-keeper-in-wsfc.png
[sap-ha-guide-figure-3046]:./media/virtual-machines-shared-sap-high-availability-guide/3046-dns-entry-sap-ascs-virtual-name-ip.png
[sap-ha-guide-figure-3047]:./media/virtual-machines-shared-sap-high-availability-guide/3047-dns-manager.png
[sap-ha-guide-figure-3048]:./media/virtual-machines-shared-sap-high-availability-guide/3048-default-cluster-probe-port.png
[sap-ha-guide-figure-3049]:./media/virtual-machines-shared-sap-high-availability-guide/3049-cluster-probe-port-after.png
[sap-ha-guide-figure-3050]:./media/virtual-machines-shared-sap-high-availability-guide/3050-service-type-ers-delayed-automatic.png
[sap-ha-guide-figure-5000]:./media/virtual-machines-shared-sap-high-availability-guide/5000-wsfc-sap-sid-node-a.png
[sap-ha-guide-figure-5001]:./media/virtual-machines-shared-sap-high-availability-guide/5001-sios-replicating-local-volume.png
[sap-ha-guide-figure-5002]:./media/virtual-machines-shared-sap-high-availability-guide/5002-wsfc-sap-sid-node-b.png
[sap-ha-guide-figure-5003]:./media/virtual-machines-shared-sap-high-availability-guide/5003-sios-replicating-local-volume-b-to-a.png

[sap-ha-guide-figure-6003]:./media/virtual-machines-shared-sap-high-availability-guide/6003-sap-multi-sid-full-landscape.png

[sap-templates-3-tier-multisid-xscs-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs%2Fazuredeploy.json
[sap-templates-3-tier-multisid-xscs-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[sap-templates-3-tier-multisid-db-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db-md%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps%2Fazuredeploy.json
[sap-templates-3-tier-multisid-apps-marketplace-image-md]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-apps-md%2Fazuredeploy.json

[virtual-machines-azure-resource-manager-architecture-benefits-arm]:../../../azure-resource-manager/resource-group-overview.md#the-benefits-of-using-resource-manager

[virtual-machines-manage-availability]:../../virtual-machines-windows-manage-availability.md



Виртуальные машины Azure является hello решением для организаций, которым требуется вычислений, хранения и сетевые ресурсы, минимальное время и без длительных процессов поставки. Можно использовать виртуальные машины Azure toodeploy классических приложений на основе SAP NetWeaver ABAP, Java и стек ABAP + Java. Повысьте уровень надежности и доступности без привлечения дополнительных локальных ресурсов. Виртуальные машины Azure поддерживают распределенные подключения. Это позволяет интегрировать их в локальные домены, частные облака и системный ландшафт SAP вашей организации.

В этой статье мы рассмотрим hello действия, которые можно предпринять toodeploy высокого уровня доступности систем SAP в Azure с помощью модели развертывания диспетчера ресурсов Azure hello. Здесь рассматриваются следующие основные задачи:

* Найти hello правой примечания по SAP и установки руководства, перечисленные в hello [ресурсов] [ sap-ha-guide-2] раздела. В этой статье дополняет документацию по установке SAP и примечания по SAP, которые являются hello основными ресурсами, которые могут помочь при установке и развертывании по SAP на конкретных платформах.
* Узнайте различия hello hello модели развертывания диспетчера ресурсов Azure и hello Azure классической модели развертывания.
* Дополнительные сведения о отказоустойчивой кластеризации Windows Server режимы кворума, чтобы вы могли выбрать hello модели, которая подходит для развертывания в Azure.
* Понимание принципов работы общего хранилища отказоустойчивого кластера Windows Server в Azure.
* Узнайте, как toohelp защиты компонентов одной точки из сбоя как расширенный бизнеса приложения программирования (ABAP) SAP центра служб (ASC) или центра служб SAP (SCS) и систем управления базами данных (СУБД) и избыточные компоненты, такие как SAP Сервер приложений в Azure.
* Выполнение пошаговых инструкций по установке и настройке системы SAP с высоким уровнем доступности в отказоустойчивом кластере Windows Server в Azure с помощью Azure Resource Manager.
* Дополнительные сведения о дополнительных шагов требуется toouse отказоустойчивой кластеризации Windows Server в Azure, но не нужны в развертывании на локальном компьютере.

toosimplify развертывания и конфигурации, в этой статье мы используем hello шаблоны диспетчера ресурсов SAP трехуровневой высокого уровня доступности. шаблоны Hello Автоматизация развертывания hello всей инфраструктуры, необходимый для высокого уровня доступности системы SAP. Инфраструктура Hello также поддерживает изменение размеров SAP приложения производительности Standard (SAPS) системы SAP.

## <a name="217c5479-5595-4cd8-870d-15ab00d4f84c"></a> Предварительные требования
Прежде чем начать, убедитесь, что выполнены предварительные требования hello, описанные в следующих разделах hello. Кроме того, следует убедиться, что toocheck все ресурсы, перечисленные в hello [ресурсов] [ sap-ha-guide-2] раздела.

В этой статье мы используем шаблоны Azure Resource Manager для [трехуровневой платформы SAP NetWeaver, использующей управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md/). Обзор шаблонов представлен в статье о [шаблонах Azure Resource Manager для SAP](https://blogs.msdn.microsoft.com/saponsqlserver/2016/05/16/azure-quickstart-templates-for-sap/).

## <a name="42b8f600-7ba3-4606-b8a5-53c4f026da08"></a> Материалы
Дополнительные сведения о развертывании SAP в Azure см. в следующих статьях:

* [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию][deployment-guide]
* [SAP NetWeaver на виртуальных машинах Windows. Руководство по развертыванию СУБД][dbms-guide]
* [Руководство по обеспечению высокого уровня доступности SAP NetWeaver на виртуальных машинах Azure (это руководство)][sap-ha-guide]

> [!NOTE]
> Когда это возможно, мы предоставим вам toohello связи, ссылающиеся на руководство по установке SAP (см. hello [руководства по установке SAP][sap-installation-guides]). Предварительные условия и сведения о процессе установки hello, это всего установки SAP NetWeaver hello tooread рекомендуется тщательно проводит. В этой статье рассматриваются только отдельные задачи для систем на основе SAP NetWeaver, устанавливаемых на виртуальные машины Microsoft Azure.
>
>

Примечания по SAP, связанные toohello тема SAP в Azure:

| Номер примечания | Название |
| --- | --- |
| [1928533] |Приложения SAP в Azure: поддерживаемые продукты и размеры |
| [2015553] |SAP в Microsoft Azure: требования |
| [1999351] |Расширенный мониторинг Azure для SAP |
| [2178632] |Ключевые метрики мониторинга для SAP в Microsoft Azure |
| [1999351] |Виртуализация в Windows: расширенный мониторинг |
| [2243692] |Использование хранилища SSD класса Premium Azure для экземпляра СУБД SAP |

Дополнительные сведения о hello [ограничения подписки Azure][azure-subscription-service-limits-subscription], включая ограничения по умолчанию общие и максимального ограничения.

## <a name="42156640c6-01cf-45a9-b225-4baa678b24f1"></a>Высокого уровня доступности SAP с помощью диспетчера ресурсов Azure и hello Azure классической модели развертывания
в следующих областях hello различаются Hello диспетчера ресурсов Azure и Azure классическое развертывание моделей:

- Группы ресурсов
- Внутренняя Azure загрузить зависимость балансировки группы ресурсов Azure hello
- Поддержка сценариев с несколькими идентификаторами безопасности SAP

### <a name="f76af273-1993-4d83-b12d-65deeae23686"></a> Группы ресурсов
В диспетчере ресурсов Azure можно использовать toomanage группы ресурсов все ресурсы приложения hello в вашей подписке Azure. Комплексный подход, в группе ресурсов, все ресурсы имеют hello же жизненного цикла. Например, все ресурсы создаются в hello же времени и они удаляются при hello то же время. Дополнительная информация о [группах ресурсов](../../../azure-resource-manager/resource-group-overview.md#resource-groups).

### <a name="3e85fbe0-84b1-4892-87af-d9b65ff91860"></a>Внутренняя Azure загрузить зависимость балансировки группы ресурсов Azure hello

В hello Azure классической модели развертывания имеется зависимость между hello Azure внутренней подсистемы балансировки нагрузки (служба балансировки нагрузки Azure) и hello облачной службы. Для каждого внутреннего балансировщика нагрузки требуется одна облачная служба.

В диспетчере ресурсов Azure каждый ресурс Azure должен toobe помещаются в группе ресурсов Azure и это также является допустимым для балансировки нагрузки Azure. Однако группы нет необходимости toohave один ресурс Azure на балансировки нагрузки Azure, например одну группу ресурсов Azure может содержать несколько подсистем балансировки нагрузки Azure. Среда Hello стало проще и гибче. 

### <a name="support-for-sap-multi-sid-scenarios"></a>Поддержка сценариев с несколькими идентификаторами безопасности SAP

В модели Azure Resource Manager в одном кластере можно установить несколько экземпляров SAP ASCS/SCS с системными идентификаторами (идентификаторами безопасности). Это возможно за счет поддержки каждым внутренним балансировщиком нагрузки Azure нескольких IP-адресов.

toouse hello Azure классической модели развертывания, выполните описанные hello в [SAP NetWeaver в Azure: кластеризации SAP ASCS/SCS экземпляров с помощью отказоустойчивой кластеризации Windows Server в Azure с помощью sios DataKeeper](http://go.microsoft.com/fwlink/?LinkId=613056).

> [!IMPORTANT]
> Настоятельно рекомендуется использовать модель развертывания диспетчера ресурсов Azure hello для установленных приложений SAP. Он предлагает множество преимуществ, которые недоступны в hello классической модели развертывания. Дополнительные сведения о моделях развертывания Azure см. [здесь][virtual-machines-azure-resource-manager-architecture-benefits-arm].   
>
>

## <a name="8ecf3ba0-67c0-4495-9c14-feec1a2255b7"></a> Отказоустойчивый кластер Windows Server (WSFC)
Отказоустойчивая кластеризация Windows Server — foundation hello установки SAP ASCS/SCS высокого уровня доступности и СУБД в Windows.

Отказоустойчивый кластер — группу 1 + n независимых серверов (узлов), работающих совместно tooincrease hello доступности приложений и служб. В случае сбоя узла отказоустойчивой кластеризации Windows Server вычисляет hello количество сбоев, которые могут возникнуть при сохранении исправное состояние кластера tooprovide приложений и служб. Можно выбрать другой кворума режимы tooachieve отказоустойчивого кластера.

### <a name="1a3c5408-b168-46d6-99f5-4219ad1b1ff2"></a> Режимы кворума
При использовании WSFC доступно четыре режима кворума.

* **Большинство узлов**. Каждый узел кластера hello может голосовать. функции Hello кластера только с большинством голосов, то есть с более половины hello голоса. Этот вариант рекомендуется при наличии нечетного числа узлов. Например три узла в кластер из семи узлов может завершиться ошибкой, и прежнему hello кластера позволяет достичь большей и по-прежнему toorun.  
* **Большинство узлов и диска**. Каждый узел и указанный диск (диск-свидетель) в хранилище кластера hello смогут проголосовать они становятся доступны и в связи. более половины голоса hello голосов функции Hello кластера только с большинством hello т. е. Этот режим целесообразно использовать в среде кластера с четным числом узлов. Если hello половины узлов и hello диска подключены к сети, кластер hello находится в работоспособном состоянии.
* **Большинство узлов и файлового ресурса**. Каждый узел плюс, назначенный общую папку (файловый ресурс-свидетель), Здравствуйте, администратор создает может голосовать, независимо от того, hello узлов и общую папку доступны ли и доступны для связи. более половины голоса hello голосов функции Hello кластера только с большинством hello т. е. Этот режим целесообразно использовать в среде кластера с четным числом узлов. Аналогичные toohello узла и режим большинства диска, но следящая общая папка используется вместо диска-свидетеля. Данный режим может легко tooimplement, но если hello общая папка сам не обеспечивает высокую доступность, ее можно будет единая точка отказа.
* **Отсутствие большинства — только диск**. Hello кластер имеет кворум, если один узел доступен и в связи с определенным диском в хранилище кластера hello. Только узлы hello, которые также находятся в связи с этого диска можно соединить hello кластера. Использовать этот режим не рекомендуется.
 

## <a name="fdfee875-6e66-483a-a343-14bbaee33275"></a> Отказоустойчивый кластер Windows Server в локальной среде
На рис. 1 показан кластер, состоящий из двух узлов. Если hello сетевого подключения между узлами hello и работать обоих узлов и запущена, диск или файловый ресурс кворума определяет продолжится, какой из узлов кластера hello tooprovide приложений и служб. Hello узел, имеющий доступ toohello кворума диск или общая папка будет hello гарантирует, что службы продолжать.

Поскольку в этом примере используется двухузлового кластера, мы используем hello узла и режим кворума большинства общей папки для файла. Hello узла и большинству дисков также является допустимым параметром. В рабочей среде рекомендуется использовать диск кворума. Можно использовать сети и хранилища toomake технологии системы его высокой доступности.

![Рис. 1. Пример конфигурации отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure][sap-ha-guide-figure-1000]

_**Рис. 1.** Пример конфигурации отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure_

### <a name="be21cf3e-fb01-402b-9955-54fbecf66592"></a> Общее хранилище
На рис. 1 также показано общее хранилище кластера с двумя узлами. В общее хранилище локального кластера все узлы в кластере hello обнаруживает общего хранилища. Механизм блокировки для защиты hello данных от повреждения. Каждый узел может обнаружить отказ другого узла. При сбое одного узла, оставшийся узел hello принимает право на владение ресурсов хранилища hello и гарантирует hello доступность служб.

> [!NOTE]
> В некоторых СУБД, например SQL Server, общие диски не требуются для достижения высокого уровня доступности. SQL Server Always On реплицирует файлы данных и журналов СУБД с локального диска Привет одному кластеру узел toohello локального диска другой узел кластера. В этом случае настройки кластера Windows hello не требуется общий диск.
>
>

### <a name="ff7a9a06-2bc5-4b20-860a-46cdb44669cd"></a> Сетевые подключения и разрешение имен
Клиентские компьютеры достичь hello кластера через виртуальный IP-адрес и имя виртуального узла, DNS-сервер предоставляет приветствия. Hello локальных узлов и hello DNS-сервер может обрабатывать несколько IP-адресов.

В стандартной конфигурации используется от двух сетевых подключений:

* Выделенное соединение toohello хранилища
* Внутренняя кластера сетевое подключение для подтверждения hello
* Общедоступной сети, которую клиенты используют tooconnect toohello кластера

## <a name="2ddba413-a7f5-4e4e-9a51-87908879c10a"></a> Отказоустойчивый кластер Windows Server в Azure
Сравнение развертывания toobare исходного или частного облака, виртуальные машины Azure требуются дополнительные действия tooconfigure отказоустойчивой кластеризации Windows Server. При создании общего диска кластера, необходимо несколько IP-адресов и виртуальный узел имена tooset для экземпляра SAP ASCS/SCS hello.

В этой статье рассматриваются основные понятия и hello toobuild необходимые дополнительные действия кластер служб центра высокой доступности SAP в Azure. Мы покажем, как Подсистема балансировки нагрузки tooset копирование hello стороннего средства SIOS DataKeeper и как tooconfigure hello Azure внутренней. Эти средства toocreate отказоустойчивый кластер Windows можно использовать с файловый ресурс-свидетель в Azure.

![Рис. 2. Конфигурация отказоустойчивого кластера Windows Server в Azure без общего диска][sap-ha-guide-figure-1001]

_**Рис. 2.** Конфигурация отказоустойчивого кластера Windows Server в Azure без общего диска_

### <a name="1a464091-922b-48d7-9d08-7cecf757f341"></a> Создание общего диска в Azure с помощью SIOS DataKeeper
Общее хранилище кластера необходимо для экземпляра SAP ASCS/SCS с высоким уровнем доступности. Как в сентябре 2016 года Azure не предоставляет общее хранилище, можно использовать toocreate кластера общего хранилища. Можно использовать стороннее программное обеспечение SIOS DataKeeper Cluster Edition toocreate зеркальных хранилища, которое имитирует общее хранилище кластера. Hello SIOS решение предоставляет данные в реальном времени синхронной репликации. Вот как можно создать общий дисковый ресурс для кластера.

1. Подключите дополнительный диск tooeach hello виртуальных машин (ВМ) в кластере Windows.
2. Запустите SIOS DataKeeper Cluster Edition на обоих узлах виртуальной машины.
3. Настройте SIOS DataKeeper Cluster Edition, таким образом, чтобы он отражает содержимое hello hello дополнительный диск, подключенный том из hello виртуальной машины toohello дополнительных присоединенного тома hello целевой виртуальной машины. SIOS DataKeeper абстрагирует hello исходных и целевых локальных томов и представляет их tooWindows Server отказоустойчивый кластер в один общий диск.

Дополнительные сведения о SIOS DataKeeper см. [здесь](http://us.sios.com/products/datakeeper-cluster/).

![Рис. 3. Конфигурация отказоустойчивой кластеризации Windows Server в Azure с использованием SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Рис. 3.** Конфигурация отказоустойчивого кластера Windows Server в Azure с использованием SIOS DataKeeper_

> [!NOTE]
> В некоторых СУБД, например SQL Server, общие диски не требуются для достижения высокого уровня доступности. SQL Server Always On реплицирует файлы данных и журналов СУБД с локального диска Привет одному кластеру узел toohello локального диска другой узел кластера. В этом случае настройки кластера Windows hello не требуется общий диск.
>
>

### <a name="44641e18-a94e-431f-95ff-303ab65e0bcb"></a> Разрешение имен в Azure
Hello Azure облачной платформы не предлагает hello параметр tooconfigure виртуальных IP-адресов, например с плавающей запятой IP-адресов. Требуется альтернативное решение tooset копии виртуальных IP адресов tooreach hello ресурса кластера в облаке hello.
Azure имеет внутренний балансировщик нагрузки в hello службы балансировки нагрузки Azure. С hello внутренней подсистемы балансировки нагрузки клиентам подключиться hello кластера через hello кластера виртуального IP-адреса.
Необходимо toodeploy hello внутренней подсистемы балансировки нагрузки в группе ресурсов hello, содержащий hello узлов кластера. Настройте все необходимые правила перенаправления с пробы hello порты hello внутренней подсистемы балансировки нагрузки портов.
Hello клиенты могут подключаться через hello виртуальное имя узла. Hello DNS-сервер разрешает в IP-адрес кластера hello и перенаправления toohello активный узел кластера hello дескрипторы портов hello внутренней нагрузки балансировки.

## <a name="2e3fec50-241e-441b-8708-0b1864f66dfa"></a> Высокий уровень доступности SAP NetWeaver в Azure IaaS
tooachieve SAP высокий уровень доступности приложения, например для компонентов программного обеспечения SAP, должны tooprotect hello следующие компоненты:

* экземпляр сервера приложений SAP;
* экземпляров ASCS/SCS SAP,
* сервер СУБД.

Дополнительные сведения о защите компонентов SAP в сценариях обеспечения высокого уровня доступности см. в статье [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению][planning-guide-11].

### <a name="93faa747-907e-440a-b00a-1ae0a89b1c0e"></a> Высокая доступность серверов приложений SAP
Обычно не требуется конкретного решения высокого уровня доступности для экземпляров сервера приложений SAP и диалоговое окно приветствия. Высокий уровень доступности достигается за счет избыточности, то есть на разных экземплярах виртуальных машин Azure настраивается несколько диалоговых экземпляров. Необходимо установить как минимум два экземпляра приложения SAP на два экземпляра виртуальных машин Azure.

![Рис. 4. Высокая доступность сервера приложений SAP][sap-ha-guide-figure-2000]

_**Рис. 4.** Высокая доступность сервера приложений SAP_

Необходимо разместить все виртуальные машины, hello, экземплярах сервера приложений SAP в одной группе доступности Azure. Группа доступности Azure гарантирует следующее.

* Все виртуальные машины являются частью hello домену обновления. Домен обновления, например, гарантирует, что, hello виртуальных машин не обновляются через hello одновременно во время планового обслуживания.
* Все виртуальные машины являются частью hello одного домена. Домен сбоя, например, гарантирует, что развернуты виртуальные машины, чтобы единственной точки отказа влияет на доступность hello всех виртуальных машин.

Дополнительные сведения о том, как слишком[Управление доступностью виртуальных машин hello][virtual-machines-manage-availability].

Только диск неуправляемые: поскольку hello учетной записи хранилища Azure потенциальных узких мест, является важным toohave по крайней мере две учетные записи хранилища Azure, в которых распределяются по крайней мере два виртуальных машин. В идеале hello дисков каждой виртуальной машины, на котором выполняется экземпляр диалога SAP будет разворачиваться в другую учетную запись хранения.

### <a name="f559c285-ee68-4eec-add1-f60fe7b978db"></a> Высокая доступность экземпляра SAP ASCS/SCS
На рис. 5 приведен пример высокой доступности экземпляра SAP ASCS/SCS

![Рис. 5. Высокая доступность экземпляра SAP ASCS/SCS][sap-ha-guide-figure-2001]

_**Рис. 5.** Высокая доступность экземпляра SAP ASCS/SCS_

#### <a name="b5b1fd0b-1db4-4d49-9162-de07a0132a51"></a> Обеспечение высокого уровня доступности экземпляра SAP ASCS/SCS с помощью отказоустойчивой кластеризации Windows Server в Azure
Сравнение развертывания toobare исходного или частного облака, виртуальные машины Azure требуются дополнительные действия tooconfigure отказоустойчивой кластеризации Windows Server. toobuild отказоустойчивого кластера Windows, требуется общий диск кластера, несколько IP-адресов, несколько имен виртуального узла и Azure внутренний балансировщик нагрузки для кластеризация экземпляра SAP ASCS/SCS. Мы рассмотрим это более подробно далее в статье hello.

![Рис. 6. Конфигурация отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure с использованием SIOS DataKeeper][sap-ha-guide-figure-1002]

_**Рис. 6.** Конфигурация отказоустойчивого кластера Windows Server для SAP ASCS/SCS в Azure с использованием SIOS DataKeeper_

### <a name="ddd878a0-9c2f-4b8e-8968-26ce60be1027"></a> Высокий уровень доступности экземпляра СУБД
Hello СУБД также является единая точка контакта в системе SAP. Требуется tooprotect его с помощью решений высокой доступности. На рисунке 7 показано решение высокой доступности AlwaysOn в SQL Server в Azure, отказоустойчивой кластеризации Windows Server и hello Azure внутренней подсистемы балансировки нагрузки. SQL Server AlwaysOn реплицирует файлы данных и журналов СУБД с помощью собственной функции репликации СУБД. В этом случае вы не требуются общие диски кластера, который упрощает настройку всей hello.

![Рис. 7. Пример высокодоступного сервера СУБД SAP с SQL Server Always On][sap-ha-guide-figure-2003]

_**Рис. 7.** Пример высокодоступного сервера СУБД SAP с SQL Server Always On_

Дополнительные сведения о кластеризации SQL Server в Azure с помощью модели развертывания диспетчера ресурсов Azure hello статьях:

* [Настройка группы доступности AlwaysOn на виртуальных машинах Azure с использованием Resource Manager][virtual-machines-windows-portal-sql-alwayson-availability-groups-manual]
* [Настройка внутреннего балансировщика нагрузки для группы доступности AlwaysOn в Azure][virtual-machines-windows-portal-sql-alwayson-int-listener]

## <a name="045252ed-0277-4fc8-8f46-c5a29694a816"></a> Сценарии комплексного развертывания с высоким уровнем доступности

### <a name="deployment-scenario-using-architectural-template-1"></a>Сценарий развертывания с помощью шаблона 1 архитектуры

На рис. 8 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **одной** системы SAP. В этом сценарии используется следующая конфигурация:

- Один выделенный кластер используется для экземпляра SAP ASCS/SCS hello.
- Один выделенный кластер используется для экземпляра СУБД hello.
- экземпляры сервера приложений SAP развернуты на собственных выделенных виртуальных машинах.

![Рис. 8. Шаблон 1 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД][sap-ha-guide-figure-2004]

_**Рис. 8.** Шаблон 1 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД_

### <a name="deployment-scenario-using-architectural-template-2"></a>Сценарий развертывания с помощью шаблона 2 архитектуры

На рис. 9 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **одной** системы SAP. В этом сценарии используется следующая конфигурация:

- Один выделенный кластер используется для **оба** hello SAP ASCS/SCS экземпляра и hello СУБД.
- экземпляры сервера приложений SAP развернуты на собственных выделенных виртуальных машинах.

![Рис. 9. Шаблон 2 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД][sap-ha-guide-figure-2005]

_**Рис. 9.** Шаблон 2 архитектуры SAP с высоким уровнем доступности с выделенным кластером для ASCS/SCS и СУБД_

### <a name="deployment-scenario-using-architectural-template-3"></a>Сценарий развертывания с помощью шаблона 3 архитектуры

На рис. 10 показан пример архитектуры SAP NetWeaver с высоким уровнем доступности в Azure для **двух** систем SAP с &lt;SID1&gt; и &lt;SID2&gt;. В этом сценарии используется следующая конфигурация:

- Один выделенный кластер используется для **оба** экземпляр hello SAP ASCS/SCS SID1 *и* экземпляра SAP ASCS/SCS SID2 hello (один кластер).
- один выделенный кластер для SID1 СУБД и другой выделенный кластер для SID2 СУБД (два кластера);
- Экземпляры сервера приложений SAP для hello системы SAP SID1 имеют свои собственные выделенных виртуальных машин.
- Экземпляры сервера приложений SAP для hello системы SAP SID2 имеют свои собственные выделенных виртуальных машин.

![Рис. 10. Шаблон 3 архитектуры SAP с высоким уровнем доступности с выделенным кластером для разных экземпляров ASCS/SCS][sap-ha-guide-figure-6003]

_**Рис. 10.** Шаблон 3 архитектуры SAP с высоким уровнем доступности с выделенным кластером для разных экземпляров ASCS/SCS_

## <a name="78092dbe-165b-454c-92f5-4972bdbef9bf"></a>Подготовка инфраструктуры hello

### <a name="prepare-hello-infrastructure-for-architectural-template-1"></a>Подготовка инфраструктуры hello для архитектуры шаблона 1
Шаблоны Azure Resource Manager для SAP помогают упростить развертывание необходимых ресурсов.

шаблоны трехуровневой Hello диспетчера ресурсов Azure также поддерживают сценарии высокой доступности, такие как в архитектуре 1 шаблона, которое имеет два кластера. Каждый кластер является единой точкой отказа SAP для SAP ASCS/SCS и СУБД.

Вот, где можно получить шаблоны Azure Resource Manager hello пример сценария описаны в этой статье.

* [Образ Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image)  
* [Образ Azure Marketplace, использующий управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-md)  
* [Пользовательский образ](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image)
* [Пользовательский образ, использующий управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-md)

Инфраструктура hello tooprepare для архитектуры шаблон 1:

- В hello в hello портала Azure **параметры** колонки в hello **SYSTEMAVAILABILITY** выберите **высокого уровня ДОСТУПНОСТИ**.

  ![Рис. 11. Настройка параметров Azure Resource Manager для SAP с высоким уровнем доступности][sap-ha-guide-figure-3000]

_**Рис. 11.** Настройка параметров Azure Resource Manager для SAP с высоким уровнем доступности_


  Создайте шаблоны Hello:

  * **Виртуальные машины**:
    * виртуальные машины сервера приложений SAP: <*SAPSystemSID*>-di-<*Number*>;
    * виртуальные машины кластера SCS/SCS <*SAPSystemSID*>-ascs-<*Number*>;
    * виртуальные машины кластера СУБД: <*SID_системы_SAP*>-db-<*номер*>.

  * **Сетевые карты для всех виртуальных машин с соответствующими IP-адресами**:
    * <*SAPSystemSID*>-nic-di-<*Number*>;
    * <*SAPSystemSID*>-nic-ascs-<*Number*>;
    * <*SAPSystemSID*>-nic-db-<*Number*>.

  * **Учетные записи хранения (только неуправляемые диски)**

  * **Группы доступности** для:
    * виртуальных машин сервера приложений SAP: <*SAPSystemSID*>-avset-di;
    * виртуальных машин кластера SCS/SCS: <*SAPSystemSID*>-avset-ascs;
    * виртуальных машин кластера СУБД: <*SAPSystemSID*>-avset-db.

  * **Внутренний балансировщик нагрузки Azure**:
    * Все порты для экземпляра ASCS/SCS hello и IP-адрес <*SAPSystemSID*> - балансировки нагрузки - ascs
    * Все порты для hello СУБД SQL Server и IP-адреса <*SAPSystemSID*> - балансировки нагрузки - db

  * **Группа безопасности сети**: <*SAPSystemSID*>-nsg-ascs-0;  
    * С открытым внешних toohello порт протокола удаленного рабочего стола (RDP) <*SAPSystemSID*> - ascs - 0 виртуальной машины

> [!NOTE]
> Все IP-адреса сетевых адаптеров hello и Azure внутренних подсистем балансировки нагрузки, **динамическое** по умолчанию. Изменить их слишком**статических** IP-адресов. Описано, как toodo это hello статьи.
>
>

### <a name="c87a8d3f-b1dc-4d2f-b23c-da4b72977489"></a>Развертывание виртуальных машин с toouse (между организациями) подключения к корпоративной сети в производственной среде
Для рабочих систем SAP виртуальные машины Azure развертываются с [подключением к корпоративной сети (распределенное развертывание)][planning-guide-2.2] с помощью VPN типа "сеть — сеть" Azure или канала Azure ExpressRoute.

> [!NOTE]
> Можно использовать имеющийся экземпляр виртуальной сети Azure. Hello виртуальной сети и подсети уже созданы и подготовлен.
>
>

1.  В hello в hello портала Azure **параметры** колонки в hello **NEWOREXISTINGSUBNET** выберите **существующие**.
2.  В hello **SUBNETID** добавьте полную строку hello сети подготовленный Azure SubnetID, где планируется toodeploy виртуальных машин Azure.
3.  tooget список всех подсетей сети Azure, выполните следующую команду PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets
  ```

  Hello **идентификатор** поле показывает hello **SUBNETID**.
4. список всех tooget **SUBNETID** значения, выполните следующую команду PowerShell:

  ```PowerShell
  (Get-AzureRmVirtualNetwork -Name <azureVnetName>  -ResourceGroupName <ResourceGroupOfVNET>).Subnets.Id
  ```

  Hello **SUBNETID** выглядит следующим образом:

  ```
  /subscriptions/<SubscriptionId>/resourceGroups/<VPNName>/providers/Microsoft.Network/virtualNetworks/azureVnet/subnets/<SubnetName>
  ```

### <a name="7fe9af0e-3cce-495b-a5ec-dcb4d8e0a310"></a> Развертывание облачных экземпляров SAP для тестирования и демонстрации
Систему SAP с высоким уровнем доступности можно развернуть в модели полностью облачного развертывания. Этот тип развертывания больше подходит для демонстрации и тестирования использования. Он не поддерживается для использования в рабочей среде.

- В hello в hello портала Azure **параметры** колонки в hello **NEWOREXISTINGSUBNET** выберите **новый**. Оставьте hello **SUBNETID** пустым.

  шаблон автоматически создает диспетчер ресурсов Azure SAP Hello hello Azure виртуальной сети и подсети.

> [!NOTE]
> Необходимо также toodeploy по крайней мере один выделенных виртуальных машин для Active Directory и DNS-сервер в hello того же экземпляра виртуальной сети Azure. Эти виртуальные машины не приводит к созданию шаблона Hello.
>
>


### <a name="prepare-hello-infrastructure-for-architectural-template-2"></a>Подготовка инфраструктуры hello для архитектуры шаблона 2

Можно использовать этот шаблон диспетчера ресурсов Azure для SAP toohelp упростить развертывание ресурсов инфраструктура, необходимая для архитектуры шаблона 2 SAP.

Шаблоны Azure Resource Manager для сценария развертывания доступны здесь:

* [Образ Azure Marketplace](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged)  
* [Образ Azure Marketplace, использующий управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-marketplace-image-converged-md)  
* [Пользовательский образ](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged)
* [Пользовательский образ, использующий управляемые диски](https://github.com/Azure/azure-quickstart-templates/tree/master/sap-3-tier-user-image-converged-md)


### <a name="prepare-hello-infrastructure-for-architectural-template-3"></a>Подготовка инфраструктуры hello для архитектуры шаблона 3

Можно подготовить инфраструктуру hello и настроить SAP для **multi-SID**. Например, вы можете добавить дополнительный экземпляр SAP ASCS/SCS в *имеющуюся* конфигурацию кластера. Дополнительные сведения см. в разделе [Настройка дополнительного экземпляра SAP ASCS/SCS в существующей конфигурации кластера toocreate multi-SID конфигурации SAP в диспетчере ресурсов Azure][sap-ha-multi-sid-guide].

Если вы хотите toocreate на новый кластер с несколькими SID, можно использовать hello multi-SID [примеры использования шаблонов на GitHub](https://github.com/Azure/azure-quickstart-templates).
toocreate на новый кластер с несколькими SID требуется hello toodeploy следующие три шаблона:

* [шаблон ASCS/SCS](#ASCS-SCS-template);
* [шаблон базы данных](#database-template);
* [шаблон серверов приложений](#application-servers-template).

Hello следующих разделах содержатся дополнительные сведения о шаблонах hello и hello параметрами, необходимыми tooprovide в шаблонах hello.

#### <a name="ASCS-SCS-template"></a> Шаблон ASCS/SCS

шаблон ASCS/SCS Hello развертывает две виртуальные машины, которые можно использовать toocreate отказоустойчивого кластера Windows Server, которая содержит несколько экземпляров ASCS/SCS.

tooset hello ASCS/SCS multi-SID для шаблона, в hello [ASCS/SCS multi-SID шаблона] [ sap-templates-3-tier-multisid-xscs-marketplace-image] или [ASCS/SCS multi-SID шаблона с помощью управляемых дисков] [ sap-templates-3-tier-multisid-xscs-marketplace-image-md], введите значения для hello следующие параметры:

  - **Префикс ресурса.**  Задайте hello ресурсов префикса, используемые tooprefix все ресурсы, которые создаются во время развертывания hello. Поскольку ресурсы hello не принадлежат одной системы SAP tooonly, префикс hello hello ресурса не hello SID из одной системы SAP.  Hello префикс должен быть в диапазоне **трех до шести символов**.
  - **Тип стека.** Выберите тип стека hello hello системы SAP. В зависимости от типа hello стека Подсистема балансировки нагрузки Azure имеет один (ABAP или Java только) или две (ABAP + Java) частных IP-адресов в системе SAP.
  -  **Тип ОС.** Выберите операционную систему hello hello виртуальных машин.
  -  **Количество систем SAP.** Выберите номер hello систем SAP требуется tooinstall в этом кластере.
  -  **Доступность системы.** Выберите **высокую доступность**.
  -  **Имя пользователя и пароль администратора.** Создайте нового пользователя, который может быть используется toosign toohello машине.
  -  **Новая или имеющаяся подсеть.** Определите, следует ли создать виртуальную сеть и подсеть или использовать имеющуюся подсеть. При наличии виртуальной сети, подключенной tooyour локальную сеть, выберите **существующие**.
  -  **Идентификатор подсети.** Задайте идентификатор hello toowhich hello hello подсети, которые должны быть подключены виртуальные машины. Выберите подсеть hello виртуальной частной сети (VPN) или ExpressRoute виртуальной сети tooconnect hello виртуальной машины tooyour локальной сети. Идентификатор Hello обычно выглядит следующим образом:

   /subscriptions/<*идентификатор_подписки*>/resourceGroups/<*имя_группы_ресурсов*>/providers/Microsoft.Network/virtualNetworks/<*имя_виртуальной_сети*>/subnets/<*имя_подсети*>

шаблон Hello развертывает один экземпляр подсистемы балансировки нагрузки Azure, которая поддерживает несколько систем SAP.

- экземпляры ASCS Hello настроены для номера экземпляра 00, 10, 20...
- экземпляры SCS Hello настроены для номера экземпляра 01, 11, 21...
- экземпляры Hello ASCS постановки в очередь репликации сервера (ющих Методов) (Linux) настроены для номера экземпляра 02, 12, 22...
- экземпляры Hello SCS ющих Методов (Linux) настроены для номера экземпляра 03, 13, 23...

Hello балансировки нагрузки содержит 1 (2 для Linux) VIP(s), 1 x виртуальных IP-адресов для ASCS/SCS и 1 x виртуальных IP-адресов для ющих Методов (Linux).

Hello следующий список содержит все правила, (где x — номер hello hello системы SAP, например, 1, 2, 3...) подсистемы балансировки нагрузки.
- порты, связанные с Windows, для каждой системы SAP: 445, 5985;
- порты ASCS (номер экземпляра x0): 32x0, 36x0, 39x0, 81x0, 5x013, 5x014, 5x016;
- порты SCS (номер экземпляра x 1): 32x1, 33x1, 39x1, 81x1, 5x113, 5x114, 5x116;
- порты ASCS ERS на Linux (номер экземпляра x 2): 33x2, 5x213, 5x214, 5x216;
- порты SCS ERS на Linux (номер экземпляра x 3): 33x3, 5x313, 5x314, 5x316.

Подсистема балансировки нагрузки Hello — настроенное toouse hello, следующие порты проверки (где x — номер hello hello системы SAP, например, 1, 2, 3...):
- порт пробы внутреннего балансировщика нагрузки ASCS/SCS: 620x0;
- порт пробы внутреннего балансировщика нагрузки ERS (только Linux): 621x2.

#### <a name="database-template"></a> Шаблон базы данных

Шаблон базы данных Hello развертывает одну или две виртуальные машины, которые можно использовать tooinstall hello система управления реляционными базами данных (RDBMS) для одной системы SAP. Например при развертывании шаблона ASCS/SCS для пяти систем SAP, необходимо toodeploy этот шаблон пять раз.

tooset шаблон multi-SID базы данных hello в hello [шаблона базы данных несколькими SID] [ sap-templates-3-tier-multisid-db-marketplace-image] или [multi-SID шаблона базы данных, с помощью управляемых дисков] [ sap-templates-3-tier-multisid-db-marketplace-image-md], введите значения для hello следующие параметры:

  -  **Идентификатор системы SAP.** Введите идентификатор системы SAP hello hello требуется tooinstall системы SAP. Идентификатор Hello будет использоваться в качестве префикса hello ресурсы, которые развертываются.
  -  **Тип ОС.** Выберите операционную систему hello hello виртуальных машин.
  -  **Тип базы данных.** Выберите тип hello hello базы данных требуется tooinstall на кластере hello. Выберите **SQL** Если tooinstall Microsoft SQL Server. Выберите **HANA** при планировании tooinstall SAP HANA hello виртуальных машин. Убедитесь, что tooselect hello правильный тип операционной системы: выберите **Windows** для SQL, а затем выберите ОС Linux для HANA. Hello подсистемы балансировки нагрузки Azure, подключенной toohello виртуальные машины будут настроены toosupport hello выбранной базы данных типа:
    * **SQL.** Подсистема балансировки нагрузки Hello будет балансировать нагрузку порт 1433. Убедитесь, что toouse этот порт для настройки SQL Server Always On.
    * **HANA.** Подсистема балансировки нагрузки Hello будет балансировать нагрузку порты 35015 и 35017. Убедитесь, что tooinstall SAP HANA с номером экземпляра **50**.
    порт пробы 62550 будет использоваться службой балансировки нагрузки Hello.
  -  **Размер системы SAP.** Предоставляет набор hello число SAPS hello новую систему. Если вы не уверены, сколько SAPS hello систему необходимо, обратитесь к партнеру технологии SAP или системные интеграторы.
  -  **Доступность системы.** Выберите **высокую доступность**.
  -  **Имя пользователя и пароль администратора.** Создайте нового пользователя, который может быть используется toosign toohello машине.
  -  **Идентификатор подсети.** Введите идентификатор hello hello подсети, который использовался во время развертывания hello шаблона ASCS/SCS hello, или идентификатор hello hello подсети, в которой была создана как часть развертывания шаблона ASCS/SCS hello.

#### <a name="application-servers-template"></a> Шаблон серверов приложений

шаблон серверы приложений Hello развертывает два или более виртуальных машин, которые могут использоваться как экземпляры сервера приложений SAP для одной системы SAP. Например при развертывании шаблона ASCS/SCS для пяти систем SAP, необходимо toodeploy этот шаблон пять раз.

tooset hello приложения серверов multi-SID для шаблона, в hello [шаблон SID нескольких серверов приложений] [ sap-templates-3-tier-multisid-apps-marketplace-image] или [шаблон SID нескольких серверов приложений, с помощью управляемых дисков] [ sap-templates-3-tier-multisid-apps-marketplace-image-md], введите значения для hello следующие параметры:

  -  **Идентификатор системы SAP.** Введите идентификатор системы SAP hello hello требуется tooinstall системы SAP. Идентификатор Hello будет использоваться в качестве префикса hello ресурсы, которые развертываются.
  -  **Тип ОС.** Выберите операционную систему hello hello виртуальных машин.
  -  **Размер системы SAP.** предоставляет Hello число SAPS hello новую систему. Если вы не уверены, сколько SAPS hello систему необходимо, обратитесь к партнеру технологии SAP или системные интеграторы.
  -  **Доступность системы.** Выберите **высокую доступность**.
  -  **Имя пользователя и пароль администратора.** Создайте нового пользователя, который может быть используется toosign toohello машине.
  -  **Идентификатор подсети.** Введите идентификатор hello hello подсети, который использовался во время развертывания hello шаблона ASCS/SCS hello, или идентификатор hello hello подсети, в которой была создана как часть развертывания шаблона ASCS/SCS hello.


### <a name="47d5300a-a830-41d4-83dd-1a0d1ffdbe6a"></a> Виртуальная сеть Azure
В нашем примере hello адресное пространство виртуальной сети Azure hello — 10.0.0.0/16. Существует одна подсеть **Subnet** с диапазоном адресов 10.0.0.0/24. Все виртуальные машины и внутренние балансировщики нагрузки развертываются в этой виртуальной сети.

> [!IMPORTANT]
> Не вносите никаких изменений параметров сети toohello внутри hello гостевой операционной системы. Например, IP-адреса, DNS-серверы и подсети. Все параметры сети настраиваются с помощью Azure. Hello протокол динамической настройки узла (DHCP) служба передает параметры.
>
>

### <a name="b22d7b3b-4343-40ff-a319-097e13f62f9e"></a> IP-адреса DNS

tooset hello требуемые DNS IP-адресов, hello следующие шаги.

1.  В hello в hello портала Azure **DNS-серверы** колонки, убедитесь, что виртуальной сети **DNS-серверы** был установлен слишком**настраиваемый DNS**.
2.  Выберите параметры на основе типа сети, к которой у вас есть hello. Дополнительные сведения см. в разделе hello следующие ресурсы:
    * [Подключение к корпоративной сети (между организациями)][planning-guide-2.2]: добавьте hello IP-адреса DNS-серверов в локальной среде hello.  
    Вы можете расширить локальные DNS серверов toohello виртуальных машин, работающих в Azure. В этом случае можно добавить IP-адреса hello hello Azure виртуальные машины, на которых выполняется служба DNS hello.
    * [Развертывание только в облаке][planning-guide-2.1]: развертывание дополнительную виртуальную машину в hello же экземпляр виртуальной сети, который служит в качестве DNS-сервера. Добавление IP-адреса hello hello Azure виртуальных машин, которые вы настроили службу toorun DNS.

    ![Рис. 12. Настройка DNS-серверов для виртуальной сети Azure][sap-ha-guide-figure-3001]

    _**Рис. 12.** Настройка DNS-серверов для виртуальной сети Azure_

  > [!NOTE]
  > При изменении IP-адреса hello hello DNS-серверов необходимо tooapply виртуальных машин Azure hello toorestart Здравствуйте, изменение и распространение hello новый DNS-серверов.
  >
  >

В нашем примере hello служба DNS установлен и настроен на этих виртуальных машинах:

| Роль виртуальной машины | Имя узла виртуальной машины | Имя сетевой карты | Статический IP-адрес |
| --- | --- | --- | --- |
| 1-й DNS-сервер |domcontr-0 |pr1-nic-domcontr-0 |10.0.0.10 |
| 2-й DNS-сервер |domcontr-1 |pr1-nic-domcontr-1 |10.0.0.11 |

### <a name="9fbd43c0-5850-4965-9726-2a921d85d73f"></a>Имена узлов и статические IP-адреса для кластеризованного экземпляра SAP ASCS/SCS hello и кластеризованного экземпляра СУБД

Для локального развертывания необходимы следующие зарезервированные имена узлов и IP-адреса.

| Роль имени виртуального узла | Имя виртуального узла | Виртуальный статический IP-адрес |
| --- | --- | --- |
| Имя 1-го виртуального узла кластера SAP ASCS/SCS (используется для управления кластером) |pr1-ascs-vir |10.0.0.42 |
| Имя виртуального узла экземпляра SAP ASCS/SCS |pr1-ascs-sap |10.0.0.43 |
| Имя 2-го виртуального узла кластера SAP ASCS/SCS (используется для управления кластером) |pr1-dbms-vir |10.0.0.32 |

При создании кластера hello создать hello имена виртуальных узлов **pr1 ascs-vir** и **pr1 СУБД vir** и hello соответствующие IP-адреса, которые управляют самого кластера hello. Сведения о том, как toodo, см. в разделе [сбора узлы кластера в кластере][sap-ha-guide-8.12.1].

Можно вручную создать hello другие два имени виртуального узла **pr1 ascs sap** и **pr1 СУБД sap**, и hello связанные IP-адресов на DNS-сервере hello. Hello кластеризованного экземпляра SAP ASCS/SCS и hello кластеризованный экземпляр СУБД используйте следующие ресурсы. Сведения о том, как toodo, см. в разделе [Создание виртуального имени узла для кластеризованного экземпляра SAP ASCS/SCS][sap-ha-guide-9.1.1].

### <a name="84c019fe-8c58-4dac-9e54-173efd4b2c30"></a>Задать статический IP-адресов для виртуальных машин hello SAP
После развертывания toouse hello виртуальных машин в кластере, необходимо tooset статические IP-адреса для всех виртуальных машин. Для этого в конфигурации виртуальной сети Azure hello, а не в hello гостевой операционной системы.

1.  В hello портал Azure, выберите **группы ресурсов** > **сетевой карты** > **параметры** > **IP-адрес** .
2.  На hello **IP-адреса** колонки в разделе **назначения**выберите **статических**. В hello **IP-адрес** введите hello IP-адреса, которые должны toouse.

  > [!NOTE]
  > При изменении IP-адрес сетевой карты hello hello необходимо tooapply виртуальных машин Azure hello toorestart hello изменений.  
  >
  >

  ![Рис. 13: Задать статический IP-адресов для сетевой карты hello каждой виртуальной машины][sap-ha-guide-figure-3002]

  _**Рис. 13:** набор статических IP-адресов для сетевой карты hello каждой виртуальной машины_

  Повторите этот шаг для всех сетевых интерфейсов, то есть для всех виртуальных машин, включая виртуальные машины, которые требуется toouse для службы DNS и Active Directory.

В нашем примере используются следующие виртуальные машины и статические IP-адреса.

| Роль виртуальной машины | Имя узла виртуальной машины | Имя сетевой карты | Статический IP-адрес |
| --- | --- | --- | --- |
| Первый экземпляр сервера приложений SAP |pr1-di-0 |pr1-nic-di-0 |10.0.0.50 |
| Второй экземпляр сервера приложений SAP |pr1-di-1 |pr1-nic-di-1 |10.0.0.51 |
| ... |... |... |... |
| Последний экземпляр сервера приложений SAP |pr1-di-5 |pr1-nic-di-5 |10.0.0.55 |
| 1-й узел кластера для экземпляра ASCS/SCS |pr1-ascs-0 |pr1-nic-ascs-0 |10.0.0.40 |
| 2-й узел кластера для экземпляра ASCS/SCS |pr1-ascs-1 |pr1-nic-ascs-1 |10.0.0.41 |
| 1-й узел кластера для экземпляра СУБД |pr1-db-0 |pr1-nic-db-0 |10.0.0.30 |
| 2-й узел кластера для экземпляра СУБД |pr1-db-1 |pr1-nic-db-1 |10.0.0.31 |

### <a name="7a8f3e9b-0624-4051-9e41-b73fff816a9e"></a>Задать статический IP-адрес для hello Azure внутренняя Подсистема балансировки нагрузки

шаблон диспетчера ресурсов Azure для SAP Hello создает Azure внутренний балансировщик нагрузки, используемый в кластере экземпляра SAP ASCS/SCS hello и кластеризации СУБД hello.

> [!IMPORTANT]
> Hello именем виртуального узла hello hello SAP ASCS/SCS — это IP-адрес hello же, как IP-адрес hello hello SAP ASCS/SCS внутренней подсистемы балансировки нагрузки: **pr1 балансировки нагрузки ascs**.
> Hello IP-адрес hello виртуальное имя СУБД — hello hello же, как IP-адрес hello hello СУБД внутренней подсистемы балансировки нагрузки: **pr1 балансировки нагрузки СУБД**.
>
>

tooset статический IP-адрес для hello Azure внутренняя Подсистема балансировки нагрузки:

1.  Hello первоначального развертывания задает hello внутренний адрес подсистемы балансировки нагрузки IP слишком**динамическое**. В hello в hello портала Azure **IP-адреса** колонки в разделе **назначения**выберите **статических**.
2.  Задать IP-адрес hello hello внутренней подсистемы балансировки нагрузки **pr1 балансировки нагрузки ascs** toohello IP-адрес hello виртуальное имя узла экземпляра SAP ASCS/SCS hello.
3.  Задать IP-адрес hello hello внутренней подсистемы балансировки нагрузки **pr1 балансировки нагрузки СУБД** toohello IP-адрес hello виртуальное имя узла экземпляра СУБД hello.

  ![Рис. 14: Набор статических IP-адресов для hello внутренней подсистемы балансировки нагрузки для экземпляра SAP ASCS/SCS hello][sap-ha-guide-figure-3003]

  _**Рис. 14:** набор статических IP-адресов для hello внутренней подсистемы балансировки нагрузки для экземпляра SAP ASCS/SCS hello_

В нашем примере есть два внутренних балансировщика нагрузки Azure со следующими статическими IP-адресами.

| Роль внутреннего балансировщика нагрузки Azure | Имя внутреннего балансировщика нагрузки Azure | Статический IP-адрес |
| --- | --- | --- |
| Внутренний балансировщик нагрузки экземпляра SAP ASCS/SCS |pr1-lb-ascs |10.0.0.43 |
| Внутренний балансировщик нагрузки экземпляра СУБД SAP |pr1-lb-dbms |10.0.0.33 |


### <a name="f19bd997-154d-4583-a46e-7f5a69d0153c"></a>По умолчанию правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки ASCS/SCS

шаблон диспетчера ресурсов Azure для SAP Hello создает hello портов:
* Экземпляр ABAP ASCS с номером экземпляра по умолчанию hello **00**
* Экземпляр Java SCS с номера экземпляра по умолчанию hello **01**

При установке экземпляра SAP ASCS/SCS, необходимо использовать номер экземпляра по умолчанию hello **00** для вашей ABAP ASCS экземпляра и hello по умолчанию номер экземпляра **01** для конкретного экземпляра Java SCS.

Создайте необходимые внутренней конечных точек для портов SAP NetWeaver hello балансировки нагрузки.

Обязательные toocreate балансировки нагрузки внутренних конечных точек, сначала создайте эти балансировки конечных точек для hello SAP NetWeaver ABAP ASCS порты:

| Служба, имя правила балансировки нагрузки | Номера портов по умолчанию | Определенные порты для (экземпляра ASCS с номером экземпляра 00) (ERS с номером 10) |
| --- | --- | --- |
| Сервер постановки в очередь, *lbrule3200* |32<*InstanceNumber*> |3200 |
| Сервер сообщений ABAP, *lbrule3600* |36<*InstanceNumber*> |3600 |
| Внутренняя служба сообщений ABAP, *lbrule3900* |39<*InstanceNumber*> |3900 |
| Сервер сообщений (HTTP), *Lbrule8100* |81<*InstanceNumber*> |8100 |
| Служба запуска SAP ASCS (HTTP), *Lbrule50013* |5<*InstanceNumber*>13 |50013 |
| Служба запуска SAP ASCS (HTTPS), *Lbrule50014* |5<*InstanceNumber*>14 |50014 |
| Служба постановки в очередь для репликации, *Lbrule50016* |5<*InstanceNumber*>16 |50016 |
| Служба запуска SAP ERS (HTTP), *Lbrule51013* |5<*InstanceNumber*>13 |51013 |
| Служба запуска SAP ERS (HTTPS), *Lbrule51014* |5<*InstanceNumber*>14 |51014 |
| Win RM, *Lbrule5985* | |5985 |
| Общий доступ к файлам, *Lbrule445* | |445 |

_**Таблица 1:** номера экземпляров SAP NetWeaver ABAP ASCS hello портов_

Затем создайте эти балансировки конечных точек для hello SAP NetWeaver Java SCS порты:

| Служба, имя правила балансировки нагрузки | Номера портов по умолчанию | Определенные порты для (экземпляра SCS с номером экземпляра 01) (ERS с номером 11) |
| --- | --- | --- |
| Сервер постановки в очередь, *lbrule3201* |32<*InstanceNumber*> |3201 |
| Сервер шлюза, *lbrule3301* |33<*InstanceNumber*> |3301 |
| Сервер сообщений Java, *lbrule3900* |39<*InstanceNumber*> |3901 |
| Сервер сообщений (HTTP), *Lbrule8101* |81<*InstanceNumber*> |8101 |
| Служба запуска SAP SCS (HTTP), *Lbrule50113* |5<*InstanceNumber*>13 |50113 |
| Служба запуска SAP SCS (HTTPS), *Lbrule50114* |5<*InstanceNumber*>14 |50114 |
| Служба постановки в очередь для репликации, *Lbrule50116* |5<*InstanceNumber*>16 |50116 |
| Служба запуска SAP ERS (HTTP), *Lbrule51113* |5<*InstanceNumber*>13 |51113 |
| Служба запуска SAP ERS (HTTPS), *Lbrule51114* |5<*InstanceNumber*>14 |51114 |
| Win RM, *Lbrule5985* | |5985 |
| Общий доступ к файлам, *Lbrule445* | |445 |

_**Таблица 2:** номера экземпляров SAP NetWeaver Java SCS hello портов_

![Рис. 15: Правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки по умолчанию ASCS/SCS][sap-ha-guide-figure-3004]

_**Рис. 15:** правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки нагрузки по умолчанию ASCS/SCS_

Задать hello IP-адрес подсистемы балансировки нагрузки hello **pr1 балансировки нагрузки СУБД** toohello IP-адрес hello виртуальное имя узла экземпляра СУБД hello.

### <a name="fe0bd8b5-2b43-45e3-8295-80bee5415716"></a>Изменение правил для hello Azure внутренней подсистемы балансировки нагрузки балансировки нагрузки, по умолчанию hello ASCS/SCS

Следует toouse различное для hello SAP ASCS или экземпляров SCS необходимо изменить hello имена и значения их порты от значений по умолчанию.

1.  В hello портал Azure, выберите  **<* SID*> загрузить ascs - балансировки нагрузки - балансировки ** > **правила балансировки нагрузки**.
2.  Для правил, принадлежащим toohello SAP ASCS или экземпляра SCS балансировки нагрузки, все измените эти значения.

  * Имя
  * Порт
  * Внутренний порт

  Например если номер экземпляра ASCS по умолчанию hello toochange от 00 too31, необходимо toomake hello изменения для всех портов, указанных в таблице 1.

  Ниже приведен пример обновления *lbrule3200*для порта.

  ![На рисунке 16: Изменение правил для hello Azure внутренней подсистемы балансировки нагрузки балансировки нагрузки, по умолчанию hello ASCS/SCS][sap-ha-guide-figure-3005]

  _**На рисунке 16:** изменение hello ASCS/SCS по умолчанию правил балансировки нагрузки, для hello Azure внутренняя Подсистема балансировки нагрузки_

### <a name="e69e9a34-4601-47a3-a41c-d2e11c626c0c"></a>Добавление домена toohello виртуальные машины Windows

После назначения статических IP адрес toohello виртуальных машин, добавьте домен toohello hello виртуальных машин.

![Рисунок 17: Добавление домена tooa виртуальной машины][sap-ha-guide-figure-3006]

_**Рисунок 17:** добавить домен tooa виртуальной машины_

### <a name="661035b2-4d0f-4d31-86f8-dc0a50d78158"></a>Добавление записей реестра на обоих узлах кластера экземпляра SAP ASCS/SCS hello

Подсистема балансировки нагрузки Azure имеет внутренний балансировщик нагрузки, закрытия подключения при бездействии hello соединений, для определенного периода времени (время ожидания простоя). SAP рабочие процессы в диалоговом окне экземпляров открытых соединений toohello SAP постановки в очередь обработки как можно скорее hello первый постановки в очередь и вывода из очереди запросов отправлено toobe потребностей. Эти подключения обычно останется установленным до hello рабочего процесса или hello постановки в очередь перезапускается. Тем не менее если соединение hello простоя в течение времени, hello нагрузки Azure внутренней балансировки закрывает hello подключений. Это не проблема, поскольку hello SAP рабочего процесса восстанавливает время постановки в очередь toohello hello подключения, если он больше не существует. Эти действия описаны в трассировках developer Привет процессов SAP, но они создают большой объем дополнительное содержимое в таких трассировок. Это рекомендуется toochange hello TCP/IP `KeepAliveTime` и `KeepAliveInterval` на обоих узлах кластера. Объединить эти изменения в параметры TCP/IP hello с параметрами профиля SAP, описанные в статье hello.

записи реестра tooadd на обоих узлах кластера экземпляра SAP ASCS/SCS hello, сначала добавьте эти записи реестра Windows на обоих узлах кластера Windows для SAP ASCS/SCS:

| Путь | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Имя переменной |`KeepAliveTime` |
| Тип переменной |REG_DWORD (десятичное) |
| Значение |120000 |
| Toodocumentation связи |[https://technet.microsoft.com/en-us/library/cc957549.aspx](https://technet.microsoft.com/en-us/library/cc957549.aspx) |

_**Таблица 3.** изменение hello первый параметр TCP/IP_

Затем добавьте следующие записи реестра Windows на обоих узлах кластера Windows для SAP ASCS/SCS.

| Путь | HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters |
| --- | --- |
| Имя переменной |`KeepAliveInterval` |
| Тип переменной |REG_DWORD (десятичное) |
| Значение |120000 |
| Toodocumentation связи |[https://technet.microsoft.com/en-us/library/cc957548.aspx](https://technet.microsoft.com/en-us/library/cc957548.aspx) |

_**Таблица 4.** изменение hello второй параметр TCP/IP_

**tooapply hello изменения, перезапустите обоих узлов кластера**.

### <a name="0d67f090-7928-43e0-8772-5ccbf8f59aab"></a> Установка отказоустойчивого кластера Windows Server для экземпляра SAP ASCS/SCS

Настройка отказоустойчивого кластера Windows Server для экземпляра SAP ASCS/SCS состоит из следующих заданий:

- Сбор данных об узлах кластера hello в конфигурации кластера
- настройка файлового ресурса-свидетеля кластера.

#### <a name="5eecb071-c703-4ccc-ba6d-fe9c6ded9d79"></a>Собирать hello узлы кластера в конфигурации кластера

1.  В мастере компонентов и добавить роль hello добавьте функцию отказоустойчивой кластеризации tooboth узлов кластера.
2.  Установка hello отказоустойчивого кластера с помощью диспетчера отказоустойчивости кластеров. В диспетчере отказоустойчивости кластеров выберите **создания кластеров**, а затем добавьте только hello имя hello первый кластер, узел а. Не добавляйте hello второго узла еще; мы добавим второй узел hello позже.

  ![На рисунке 18: Добавление сервера hello или имя виртуальной машины hello первого узла кластера][sap-ha-guide-figure-3007]

  _**На рисунке 18:** добавить hello имя сервера или виртуальной машины hello первого узла кластера_

3.  Введите имя сети hello (имя виртуального узла) hello кластера.

  ![На рисунке 19: Введите имя кластера hello][sap-ha-guide-figure-3008]

  _**На рисунке 19:** введите имя кластера hello_

4.  После создания кластера hello, запустите тест проверки кластера.

  ![Рис. 20: Проверка hello кластера][sap-ha-guide-figure-3009]

  _**Рис. 20:** проверка кластера hello_

  Можно игнорировать любые предупреждения о дисках, на этом этапе в процессе hello. Вам предстоит добавить файловый ресурс-свидетель и hello SIOS общих дисков позже. На этой стадии не требуется tooworry о кворум.

  ![Рис. 21. Предупреждение об отсутствии диска кворума][sap-ha-guide-figure-3010]

  _**Рис. 21.** Предупреждение об отсутствии диска кворума_

  ![Рис. 22. Определение основного ресурса кластера с IP-адресом (требуется новый IP-адрес)][sap-ha-guide-figure-3011]

  _**Рис. 22.** Определение основного ресурса кластера с IP-адресом (требуется новый IP-адрес)_

5.  Изменение IP-адреса hello службы кластеров core hello. Hello кластера не удается запустить пока не изменить IP-адрес hello hello основная служба кластера, поскольку hello IP-адрес сервера hello указывает tooone hello узлов виртуальных машин. Это можно сделать на hello **свойства** страница hello ядра кластера службы IP-ресурс.

  Например, нам нужно tooassign IP-адрес (в нашем примере **10.0.0.42**) для имени виртуального узла кластера hello **pr1 ascs-vir**.

  ![На рисунке 23: В диалоговом окне Свойства hello, изменение hello IP-адреса][sap-ha-guide-figure-3012]

  _**На рисунке 23:** в hello **свойства** диалоговое окно, изменения hello IP-адреса_

  ![Рис. 24: Назначить hello IP-адрес, который зарезервирован для кластера hello][sap-ha-guide-figure-3013]

  _**Рис. 24:** назначения hello IP-адреса, зарезервированные для кластера hello_

6.  Перевести имя виртуального узла кластера hello через Интернет.

  ![Рис. 25: Основная служба кластера запущен и работает, а также hello исправьте IP-адрес][sap-ha-guide-figure-3014]

  _**Рис. 25:** основная служба кластеров работает и запущен и с hello исправьте IP-адрес_

7.  Добавьте второй узел кластера hello.

  Теперь, когда hello основная служба кластеров запущена, можно добавить второй узел кластера hello.

  ![Рис. 26: Добавление второго узла кластера hello][sap-ha-guide-figure-3015]

  _**Рис. 26:** добавить hello второго узла кластера_

8.  Введите имя для hello второй узел узла кластера.

  ![Рис. 27: Введите hello второе имя узла кластера узлов][sap-ha-guide-figure-3016]

  _**Рис. 27:** ввод hello второе имя узла кластера узлов_

  > [!IMPORTANT]
  > Убедитесь, что hello **Добавление всех допустимых хранилищ toohello кластера** флажок **не** выбранных.  
  >
  >

  ![Рис. 28: Не устанавливайте флажок hello][sap-ha-guide-figure-3017]

  _**Рис. 28:** сделать **не** Здравствуйте, установите флажок_

  Предупреждения о кворуме и дисках можно игнорировать. Диск hello hello кворума и общая папка будет установить позже, как описано в [установки SIOS DataKeeper Cluster Edition для диска общего ресурса кластера SAP ASCS/SCS][sap-ha-guide-8.12.3].

  ![Рис. 29: Пропускать предупреждения о hello диска кворума][sap-ha-guide-figure-3018]

  _**Рис. 29:** пропускать предупреждения о hello диска кворума_


#### <a name="e49a4529-50c9-4dcf-bde7-15a0c21d21ca"></a> Настройка файлового ресурса-свидетеля кластера

Настройка файлового ресурса-свидетеля кластера состоит из следующих заданий:

- создание файлового ресурса;
- Настройка следящего сервера кворума hello общих папок в диспетчере отказоустойчивости кластеров

##### <a name="06260b30-d697-4c4d-b1c9-d22c0bd64855"></a> Создание файлового ресурса

1.  Вместо диска кворума нужно выбрать файловый ресурс-свидетель. SIOS DataKeeper поддерживает такой вариант.

  В примерах в этой статье hello hello файловый ресурс-свидетель включен hello Active Directory или DNS-сервера, на котором работает в Azure. Hello файловый ресурс-свидетель называется **domcontr 0**. Так как будут настроены tooAzure подключения VPN (через сеть-сеть VPN или Azure ExpressRoute), ваш DNS Active Directory и службы в локальной среде, не подходящий toorun файл ресурс-свидетель.

  > [!NOTE]
  > Если служба DNS и Active Directory работает только в локальной среде, не настроить файловый ресурс-свидетель в операционной системе Windows Active Directory или DNS-hello, на котором выполняется локально. Задержка сети между узлами кластера, работающими в Azure, и локальной средой служб Active Directory и DNS, может быть слишком большой и вызвать проблемы с подключением. Быть убедиться, что tooconfigure hello файловый ресурс-свидетель на виртуальной машине Azure, на котором выполняется закрыть toohello узла кластера.  
  >
  >

  диск кворума Hello требуется по крайней мере 1 024 МБ свободного места. Мы рекомендуем 2048 МБ свободного места для hello диска кворума.

2.  Добавьте объект имени кластера hello.

  ![Рис. 30: Назначить hello разрешения для общей папки hello для hello объект имени кластера][sap-ha-guide-figure-3019]

  _**Рис. 30:** назначить hello разрешения для общей папки hello для hello объект имени кластера_

  Убедитесь, что разрешения hello входит hello центра toochange данных в общую папку hello для hello объект имени кластера (в нашем примере **pr1 ascs-vir$**).

3.  tooadd hello кластера имя объекта toohello выберите **добавить**. Изменить toocheck hello фильтр для объектов-компьютеров, в добавление toothose показано на рис. 31.

  ![Рис. 31: Изменить компьютеров tooinclude hello типов объектов][sap-ha-guide-figure-3020]

  _**Рис. 31:** изменить tooinclude компьютеров hello типов объектов_

  ![Рис. 32: Флажок hello компьютеров][sap-ha-guide-figure-3021]

  _**Рис. 32:** выберите hello **компьютеров** флажок_

4.  Введите имя объекта hello кластера, как показано на рис. 31. Так как запись hello уже создана, можно изменить разрешения hello, как показано на рисунке 30.

5.  Выберите hello **безопасности** вкладке hello общей папки, а затем задайте более подробные разрешения для hello объект имени кластера.

  ![На рисунке 33: Установить атрибуты безопасности hello для hello объект имени кластера для кворума hello общих папок][sap-ha-guide-figure-3022]

  _**На рисунке 33:** установить атрибуты безопасности hello для hello объект имени кластера для кворума hello общих папок_

##### <a name="4c08c387-78a0-46b1-9d27-b497b08cac3d"></a>Задайте следящий сервер кворума hello общих папок в диспетчере отказоустойчивости кластеров

1.  Откройте hello параметр мастера настройки кворума.

  ![Рисунок 34: Запустите мастер настройки кворума кластера Настройка hello][sap-ha-guide-figure-3023]

  _**Рисунок 34:** начала hello параметр мастером настройки кворума кластера_

2.  На hello **Выбор конфигурации кворума** выберите **Выбор свидетеля кворума hello**.

  ![Рис. 35. Экран выбора различных конфигураций кворума][sap-ha-guide-figure-3024]

  _**Рис. 35.** Экран выбора различных конфигураций кворума_

3.  На hello **Выбор свидетеля кворума** выберите **настроить файловый ресурс-свидетель**.

  ![Рисунок 36: Hello выберите файловый ресурс-свидетель][sap-ha-guide-figure-3025]

  _**Рисунок 36:** выберите hello файловый ресурс-свидетель_

4.  Введите hello UNC путь toohello общей папки (в нашем примере \\domcontr 0\FSW). Список изменений hello, можно делать, выберите toosee **Далее**.

  ![На рисунке 37: Определение общей папки hello в общей папке следящего сервера hello][sap-ha-guide-figure-3026]

  _**На рисунке 37:** определения общей папки hello в общей папке следящего сервера hello_

5.  Выберите изменения hello и установите **Далее**. Требуется toosuccessfully перенастроить hello конфигурации кластера, как показано на рисунке 38.  

  ![Рисунок 38: Подтверждение повторно настроить кластер hello][sap-ha-guide-figure-3027]

  _**На рисунке 38:** подтверждение повторно настроить кластер hello_

Отказоустойчивый кластер Windows hello после успешного завершения установки, изменения должны toobe внесенные toosome пороговые значения tooadapt отработки отказа обнаружения tooconditions в Azure. Hello toobe параметры изменения описаны в этом блоге: https://blogs.msdn.microsoft.com/clustering/2012/11/21/tuning-failover-cluster-network-thresholds/. При условии, что две виртуальные машины сборки hello конфигурации кластера Windows для ASCS/SCS находятся в Здравствуйте одной подсети, hello следующие параметры должны изменить toobe toothese значения:
- SameSubNetDelay = 2
- SameSubNetThreshold = 15

Эти параметры, протестированных с клиентами и предоставляемые toobe объединять, достаточно гибкой на одной стороне hello. На hello другой стороны эти параметры предоставление быстрого достаточно отработки отказа в реальной ошибки при сбое программного обеспечения или узел или ВМ SAP. 

### <a name="5c8e5482-841e-45e1-a89d-a05c0907c868"></a>Установить для диска общего ресурса кластера SAP ASCS/SCS hello SIOS DataKeeper Cluster Edition

Теперь у вас есть рабочая конфигурация отказоустойчивого кластера Windows Server в Azure. Но tooinstall экземпляра SAP ASCS/SCS, необходим общий дисковый ресурс. Не удается создать hello общие дисковые ресурсы, необходимые в Azure. SIOS DataKeeper Cluster Edition — это решение независимых производителей, можно использовать toocreate общие дисковые ресурсы.

Установка SIOS DataKeeper Cluster Edition для hello SAP ASCS/SCS общий ресурс диска кластера включает следующие задачи:

- Добавление hello .NET Framework 3.5
- Установка SIOS DataKeeper
- настройка SIOS DataKeeper.

#### <a name="1c2788c3-3648-4e82-9e0d-e058e475e2a3"></a>Добавить hello .NET Framework 3.5
Hello Microsoft .NET Framework 3.5 автоматически не активирована или установить на Windows Server 2012 R2. Поскольку SIOS DataKeeper требует toobe hello .NET Framework на всех узлах, устанавливающие DataKeeper на, необходимо установить .NET Framework 3.5 hello hello гостевой операционной системе всех виртуальных машин в кластере hello.

Существует два способа tooadd hello .NET Framework 3.5.

- Использование мастера hello добавления ролей и компонентов в Windows, как показано на рисунке 39.

  ![На рисунке 39: Установка hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов][sap-ha-guide-figure-3028]

  _**На рисунке 39:** hello установки .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов_

  ![Рисунок 40: Индикатор установки при установке hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов][sap-ha-guide-figure-3029]

  _**На рисунке 40:** индикатор установки при установке hello .NET Framework 3.5 с помощью мастера hello добавления ролей и компонентов_

- Используйте средство командной строки dism.exe hello. Для этого типа установки потребуется каталогу SxS hello tooaccess на установочном носителе Windows hello. В командной строке с повышенными привилегиями выполните следующую команду:

  ```
  Dism /online /enable-feature /featurename:NetFx3 /All /Source:installation_media_drive:\sources\sxs /LimitAccess
  ```

#### <a name="dd41d5a2-8083-415b-9878-839652812102"></a> Установка SIOS DataKeeper

Установите SIOS DataKeeper Cluster Edition на каждом узле в кластере hello. toocreate виртуального хранилища с помощью sios DataKeeper создания синхронизированных зеркального отображения и затем имитировать общее хранилище кластера.

Прежде чем устанавливать программное обеспечение SIOS hello, создайте пользователя домена hello **DataKeeperSvc**.

> [!NOTE]
> Добавить hello **DataKeeperSvc** toohello пользователя **локального администратора** на обоих узлов кластера.
>
>

tooinstall SIOS DataKeeper:

1.  Установите программное обеспечение hello SIOS на обоих узлах кластера.

  ![Установщик SIOS][sap-ha-guide-figure-3030]

  ![На рисунке 41: Первая страница hello SIOS DataKeeper установки][sap-ha-guide-figure-3031]

  _**На рисунке 41:** первая страница hello установки SIOS DataKeeper_

2.  В диалоговое окно «hello» показано на рисунке 42, выберите **Да**.

  ![Рис. 42. DataKeeper информирует об отключении службы][sap-ha-guide-figure-3032]

  _**Рис. 42.** DataKeeper информирует об отключении службы_

3.  Диалоговое окно «hello» показано на рисунке 43, мы рекомендуем выбрать **учетную запись домена или сервера**.

  ![Рис. 43. Выбор пользователя для SIOS DataKeeper][sap-ha-guide-figure-3033]

  _**Рис. 43.** Выбор пользователя для SIOS DataKeeper_

4.  Введите имя пользователя учетной записи домена hello и пароли, которые созданы для SIOS DataKeeper.

  ![На рисунке 44: Введите hello доменное имя пользователя и пароль для hello установки SIOS DataKeeper][sap-ha-guide-figure-3034]

  _**На рисунке 44:** введите hello доменное имя пользователя и пароль для hello установки SIOS DataKeeper_

5.  Установите hello лицензионный ключ для конкретного экземпляра SIOS DataKeeper, как показано на рисунке 45.

  ![Рис. 45. Указание ключа лицензии на использование SIOS DataKeeper][sap-ha-guide-figure-3035]

  _**Рис. 45.** Указание ключа лицензии на использование SIOS DataKeeper_

6.  При появлении запроса перезапустите виртуальную машину hello.

#### <a name="d9c1fc8e-8710-4dff-bec2-1f535db7b006"></a> Настройка SIOS DataKeeper

После установки SIOS DataKeeper на обоих узлах, необходимо toostart hello конфигурации. Цель Hello hello конфигурации — toohave синхронные данные репликации между дополнительные диски hello присоединен tooeach hello виртуальных машин.

1.  Запуск hello DataKeeper управления и средство настройки, а затем выберите **подключение серверу**. (На рис. 46 эта ссылка обведена красным.)

  ![Рис. 46. Инструмент управления и настройки DataKeeper][sap-ha-guide-figure-3036]

  _**Рис. 46.** Инструмент управления и настройки DataKeeper_

2.  Введите имя hello или адрес TCP/IP hello первый узел hello управление и настройку средства следует установите соединение и на втором шаге hello второй узел.

  ![На рисунке 47: Hello укажите имя или IP-адрес hello первый узел hello управление и настройку средства следует подключаться к, а на втором шаге, а второй узел hello][sap-ha-guide-figure-3037]

  _**На рисунке 47:** hello укажите имя или IP-адрес hello первый узел hello управление и настройку средства следует подключаться к, а на втором шаге, а второй узел hello_

3.  Создание задания hello репликации между двумя узлами hello.

  ![Рис. 48. Создание задания репликации][sap-ha-guide-figure-3038]

  _**Рис. 48.** Создание задания репликации_

  Мастер помогает выполнить процесс создания задания репликации hello.
4.  Укажите имя hello, TCP/IP-адрес и тома hello исходного узла.

  ![Рисунок 49: Определяет имя hello hello задания репликации][sap-ha-guide-figure-3039]

  _**Рисунок 49:** имя hello определение задания репликации hello_

  ![На рисунке 50: Определения hello базовых данных для hello узел, который должен быть hello текущего узла источника][sap-ha-guide-figure-3040]

  _**На рисунке 50:** определения базовых данных hello hello узел, который должен быть hello текущего узла источника_

5.  Укажите имя hello, TCP/IP-адрес и тома hello целевого узла.

  ![Рисунок 51: Определения hello базовых данных для hello узел, который должен быть hello текущего целевого узла][sap-ha-guide-figure-3041]

  _**На рисунке 51:** определить базовые данные hello hello узел, который должен быть hello текущей целевой узел_

6.  Определение алгоритма сжатия hello. В нашем примере мы рекомендуем сжимать hello потока репликации. Особенно в случаях повторная синхронизация hello сжатия потока репликации hello значительно сокращает время повторной синхронизации. Обратите внимание, что сжатие использует ресурсы ЦП и ОЗУ hello виртуальной машины. При увеличении hello степень сжатия, поэтому hello объем ресурсов ЦП, используемых. Этот параметр можно изменить позже.

7.  Требуется другой параметр toocheck является, происходит ли репликация hello синхронно или асинхронно. *Для защиты конфигураций SAP ASCS/SCS требуется синхронная репликация*.  

  ![Рис. 52. Определение сведений о репликации][sap-ha-guide-figure-3042]

  _**Рис. 52.** Определение сведений о репликации_

8.  Указать ли том hello, реплицируется с задания репликации hello представленного tooa отказоустойчивой кластеризации Windows Server конфигурации кластера как общего диска. Конфигурации SAP ASCS/SCS hello, выберите **Да** , чтобы видит кластера Windows hello hello реплицированных том в качестве общего диска, его можно использовать в качестве тома кластера.

  ![На рисунке 53: Hello tooset выберите «Да» репликации тома томом кластера][sap-ha-guide-figure-3043]

  _**На рисунке 53:** выберите **Да** tooset hello реплицируются в качестве тома кластера_

  После создания тома hello hello DataKeeper средство управления и конфигурации показывает задания репликации hello активен.

  ![Рисунок 54: DataKeeper синхронной активен режим зеркального отображения для hello SAP ASCS/SCS общего ресурса диска][sap-ha-guide-figure-3044]

  _**На рисунке 54:** DataKeeper синхронной активен режим зеркального отображения для hello SAP ASCS/SCS папку диска_

  Диспетчер отказоустойчивости кластеров теперь отображает hello диск как диск DataKeeper, как показано на рисунке 55.

  ![На рисунке 55: Hello диска, для которых репликация DataKeeper показано, диспетчера отказоустойчивого кластера][sap-ha-guide-figure-3045]

  _**На рисунке 55:** Диспетчер отказоустойчивости кластеров показывает hello диска, DataKeeper репликации_

## <a name="a06f0b49-8a7a-42bf-8b0d-c12026c5746b"></a>Установка системы SAP NetWeaver hello

Мы не описание настройки СУБД hello, так как параметры настройки зависят от используемой системы СУБД hello. Тем не менее мы предполагаем, что опасения высокого уровня доступности СУБД hello адресуются с возможностями hello hello различных поставщиков СУБД поддержку Azure. Например, AlwaysOn или зеркальное отображение базы данных для SQL Server и Oracle Data Guard для баз данных Oracle. В случае hello мы используем в этой статье мы не добавлять дополнительные toohello защиты СУБД.

Особые рекомендации по взаимодействию различных СУБД с такой кластеризованной конфигурацией SAP ASCS/SCS в Azure отсутствуют.

> [!NOTE]
> процедуры установки Hello систем SAP NetWeaver ABAP, Java систем и систем ABAP + Java практически идентичны. наиболее важное отличие Hello, имеет систему SAP ABAP один экземпляр ASCS. Hello системы SAP Java имеет один экземпляр SCS. Hello системы SAP ABAP + Java имеет один экземпляр ASCS и один экземпляр SCS, работающий в hello же группы отказоустойчивого кластера Майкрософт. Любые отличия в установке для каждого стека установки SAP NetWeaver будут указаны явным образом. Можно предположить, что все остальные элементы являются hello таким же.  
>
>

### <a name="31c6bd4f-51df-4057-9fdf-3fcbc619c170"></a> Установка SAP с высокодоступным экземпляром ASCS/SCS

> [!IMPORTANT]
> Убедитесь, что не tooplace файлов на странице на DataKeeper зеркальных томов. DataKeeper не поддерживает зеркальные тома. Можно оставить файл подкачки на временном диске hello D из виртуальной машины Azure которого — по умолчанию hello. Если он еще не существует, переместите приветствия Windows страницы файла toodrive D: Azure виртуальной машины.
>
>

Установка SAP с высокодоступным экземпляром ASCS/SCS состоит из следующих заданий:

- Создание виртуального имени узла для hello кластеризованного экземпляра SAP ASCS/SCS
- Установка первого узла кластера hello SAP
- Изменение профиля hello SAP ASCS/SCS экземпляра hello
- добавление порта пробы;
- Открытие порта пробы в брандмауэре Windows hello

#### <a name="a97ad604-9094-44fe-a364-f89cb39bf097"></a>Создание виртуального имени узла для hello кластеризованного экземпляра SAP ASCS/SCS

1.  В диспетчере Windows DNS hello создайте запись DNS для имени виртуального узла hello hello ASCS/SCS экземпляра.

  > [!IMPORTANT]
  > Hello IP-адрес, назначьте имя виртуального узла toohello ASCS/SCS экземпляр должен быть hello hello же, как hello IP-адрес, назначенный tooAzure балансировки нагрузки (**<*SID*> - балансировки нагрузки - ascs **).  
  >
  >

  Здравствуйте, IP-адрес hello виртуальное имя узла SAP ASCS/SCS (**pr1 ascs sap**) hello же, как hello IP-адрес подсистемы балансировки нагрузки Azure (**pr1 балансировки нагрузки ascs**).

  ![На рисунке 56: Определение hello DNS-запись для hello SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес][sap-ha-guide-figure-3046]

  _**На рисунке 56:** определить hello DNS-запись для hello SAP ASCS/SCS виртуальное имя кластера и TCP/IP-адрес_

2.  toodefine hello IP-адреса, назначенного toohello виртуальное имя узла, выберите **диспетчер DNS** > **домена**.

  ![Рис. 57. Новое виртуальное имя и TCP/IP-адрес для конфигурации кластера SAP ASCS/SCS][sap-ha-guide-figure-3047]

  _**Рис. 57.** Новое виртуальное имя и TCP/IP-адрес для конфигурации кластера SAP ASCS/SCS_

#### <a name="eb5af918-b42f-4803-bb50-eff41f84b0b0"></a>Установите первый узел кластера hello SAP

1.  Выполните первый вариант узла кластера hello на узле кластера, а. Например, на hello **pr1-ascs-0** узла.
2.  порты по умолчанию hello tookeep для hello Azure внутренняя Подсистема балансировки нагрузки, выберите:

  * для **системы ABAP** — экземпляр **ASCS** с номером **00**;
  * для **системы Java** — экземпляр **SCS** с номером **01**;
  * для **системы ABAP с Java** — экземпляр **ASCS** с номером **00** и экземпляр **SCS** с номером **01**.

  экземпляр toouse цифры, отличный от 00 для hello ABAP ASCS экземпляра и 01 для экземпляра Java SCS hello, сначала необходимо toochange hello Azure внутренней нагрузки подсистемы балансировки нагрузки по умолчанию балансировки правил, описанных в [нагрузки по умолчанию ASCS/SCS hello изменений правила для hello Azure внутренней подсистемы балансировки нагрузки подсистемы балансировки][sap-ha-guide-8.9].

Hello Далее некоторые действия не описаны в hello Стандартная документацию по установке SAP.

> [!NOTE]
> документацию по установке SAP Hello описывает, как tooinstall hello первый узел кластера ASCS/SCS.
>
>

#### <a name="e4caaab2-e90f-4f2c-bc84-2cd2e12a9556"></a>Изменение профиля hello SAP ASCS/SCS экземпляра hello

Необходимо tooadd новый параметр профиля. параметр профиля Hello предотвращает соединения между SAP рабочие процессы и сервер постановки в очередь hello закрытие при бездействии слишком долго. Мы уже упоминали сценарий проблемы hello в [добавления записей реестра на обоих узлах кластера экземпляра SAP ASCS/SCS hello][sap-ha-guide-8.11]. В этом разделе мы также представили два изменения toosome basic TCP/IP параметры соединения. На втором шаге нужно поставить в очередь сервера tooset hello toosend `keep_alive` сигнала, чтобы подключения hello не достигнуть Порог простоя подсистемы балансировки нагрузки Azure внутренней hello.

hello toomodify профиль SAP ASCS/SCS экземпляра hello:

1.  Добавьте этот профиль параметр toohello профиль экземпляра SAP ASCS/SCS.

  ```
  enque/encni/set_so_keepalive = true
  ```
  В нашем примере — hello путь:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_ASCS00_pr1-ascs-sap`

  Например профиль экземпляр toohello SAP SCS и путь к соответствующему:

  `<ShareDisk>:\usr\sap\PR1\SYS\profile\PR1_SCS01_pr1-ascs-sap`

2.  tooapply hello изменения, перезапустите экземпляр SAP ASCS /SCS hello.

#### <a name="10822f4f-32e7-4871-b63a-9b86c76ce761"></a> Добавление порта пробы

Используйте hello внутренней подсистемы балансировки нагрузки проверки функциональности toomake hello весь кластер конфигурации рабочих с подсистемы балансировки нагрузки Azure. Hello Azure внутренней подсистемы балансировки нагрузки обычно распределяет входящие рабочей нагрузки hello поровну между участвующими виртуальных машин. Однако это не будет работать в некоторых конфигурациях кластера, так как активен только один экземпляр. Hello другого экземпляра является пассивным и не может принимать любой рабочей нагрузки hello. Функции проверки помогают при использовании назначает подсистемы балансировки нагрузки Azure внутренней hello работать только tooan активный экземпляр. Возможности проверки hello hello внутренней подсистемы балансировки нагрузки может обнаружить экземпляры, которые активны, а затем выбрать только экземпляр hello hello рабочей нагрузки.

tooadd порт пробы:

1.  Проверьте текущий hello **ProbePort** задание, выполнив следующую команду PowerShell hello. Выполните из в одном hello виртуальных машин в конфигурации кластера hello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter
  ```

2.  Укажите порт пробы. номер порта пробы по умолчанию Hello **0**. В нашем примере мы используем порт пробы **62000**.

  ![На рисунке 58: порт пробы hello кластера конфигурации по умолчанию равно 0][sap-ha-guide-figure-3048]

  _**На рисунке 58:** порт пробы конфигурации кластера по умолчанию hello равно 0_

  номер порта Hello определяется в шаблоны диспетчера ресурсов Azure для SAP. Можно назначить hello номер порта в PowerShell.

  новое значение для hello ProbePort tooset  **SAP <*SID*> IP ** ресурса кластера, запустите следующий сценарий PowerShell hello. Обновите переменные PowerShell hello для вашей среды. После запуска сценария hello, вы будете tooactivate изменения hello SAP кластера запрашиваемые toorestart hello группы.

  ```PowerShell
  $SAPSID = "PR1"      # SAP <SID>
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  Clear-Host
  $SAPClusterRoleName = "SAP $SAPSID"
  $SAPIPresourceName = "SAP $SAPSID IP"
  $SAPIPResourceClusterParameters =  Get-ClusterResource $SAPIPresourceName | Get-ClusterParameter
  $IPAddress = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Address" }).Value
  $NetworkName = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "Network" }).Value
  $SubnetMask = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "SubnetMask" }).Value
  $OverrideAddressMatch = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "OverrideAddressMatch" }).Value
  $EnableDhcp = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "EnableDhcp" }).Value
  $OldProbePort = ($SAPIPResourceClusterParameters | Where-Object {$_.Name -eq "ProbePort" }).Value

  $var = Get-ClusterResource | Where-Object {  $_.name -eq $SAPIPresourceName  }

  Write-Host "Current configuration parameters for SAP IP cluster resource '$SAPIPresourceName' are:" -ForegroundColor Cyan
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter

  Write-Host
  Write-Host "Current probe port property of hello SAP cluster resource '$SAPIPresourceName' is '$OldProbePort'." -ForegroundColor Cyan
  Write-Host
  Write-Host "Setting hello new probe port property of hello SAP cluster resource '$SAPIPresourceName' too'$ProbePort' ..." -ForegroundColor Cyan
  Write-Host

  $var | Set-ClusterParameter -Multiple @{"Address"=$IPAddress;"ProbePort"=$ProbePort;"Subnetmask"=$SubnetMask;"Network"=$NetworkName;"OverrideAddressMatch"=$OverrideAddressMatch;"EnableDhcp"=$EnableDhcp}

  Write-Host

  $ActivateChanges = Read-Host "Do you want tootake restart SAP cluster role '$SAPClusterRoleName', tooactivate hello changes (yes/no)?"

  if($ActivateChanges -eq "yes"){
  Write-Host
  Write-Host "Activating changes..." -ForegroundColor Cyan

  Write-Host
  write-host "Taking SAP cluster IP resource '$SAPIPresourceName' offline ..." -ForegroundColor Cyan
  Stop-ClusterResource -Name $SAPIPresourceName
  sleep 5

  Write-Host "Starting SAP cluster role '$SAPClusterRoleName' ..." -ForegroundColor Cyan
  Start-ClusterGroup -Name $SAPClusterRoleName

  Write-Host "New ProbePort parameter is active." -ForegroundColor Green
  Write-Host

  Write-Host "New configuration parameters for SAP IP cluster resource '$SAPIPresourceName':" -ForegroundColor Cyan
  Write-Host
  Get-ClusterResource -Name $SAPIPresourceName | Get-ClusterParameter
  }else
  {
  Write-Host "Changes are not activated."
  }
  ```

  После переноса hello  **SAP <*SID*> ** роль сети кластера, убедитесь, что **ProbePort** задано новое значение toohello.

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPNetworkIPClusterName = "SAP $SAPSID IP"
  Get-ClusterResource $SAPNetworkIPClusterName | Get-ClusterParameter

  ```

  ![Рисунок 59: Hello кластера порта пробы, задав новое значение hello][sap-ha-guide-figure-3049]

  _**На рисунке 59:** hello кластера порта пробы, задав новое значение hello_

#### <a name="4498c707-86c0-4cde-9c69-058a7ab8c3ac"></a>Открытие порта пробы в брандмауэре Windows hello

Необходимо tooopen порта пробы в брандмауэре Windows на обоих узлах кластера. Используйте следующий сценарий tooopen порта пробы в брандмауэре Windows hello. Обновите переменные PowerShell hello для вашей среды.

  ```PowerShell
  $ProbePort = 62000   # ProbePort of hello Azure Internal Load Balancer

  New-NetFirewallRule -Name AzureProbePort -DisplayName "Rule for Azure Probe Port" -Direction Inbound -Action Allow -Protocol TCP -LocalPort $ProbePort
  ```

Hello **ProbePort** задано слишком**62000**. Теперь можно получить доступ к общей папке hello  **\\\ascsha-clsap\sapmnt** от других узлов, например, в **ascsha Администраторы**.

### <a name="85d78414-b21d-4097-92b6-34d8bcb724b7"></a>Установите экземпляр базы данных hello

База данных hello tooinstall экземпляра, выполните hello процесс, описанный в документации по установке SAP hello.

### <a name="8a276e16-f507-4071-b829-cdc0a4d36748"></a>Установка hello второго узла кластера

tooinstall hello второй кластер, повторите шаги hello в руководстве по установке SAP hello.

### <a name="094bc895-31d4-4471-91cc-1513b64e406a"></a>Изменить тип запуска hello экземпляра службы SAP ющих Методов Windows hello

Измените тип запуска службы SAP ющих Методов Windows hello hello слишком**автоматически (отложенный запуск)** на обоих узлах кластера.

![Рисунок 60: Изменить тип службы hello для автоматического toodelayed экземпляра SAP ющих Методов hello][sap-ha-guide-figure-3050]

_**На рисунке 60:** hello типа службы для автоматического toodelayed экземпляра SAP ющих Методов hello_

### <a name="2477e58f-c5a7-4a5d-9ae3-7b91022cafb5"></a>Установка hello первичного сервера приложений SAP

Установить экземпляр основного сервера приложений (PAS) hello <*SID*> hello toohost - di - 0 на виртуальной машине hello, назначенный вами PAS. Какие-либо специальные зависимости от параметров Azure или DataKeeper отсутствуют.

### <a name="0ba4a6c1-cc37-4bcf-a8dc-025de4263772"></a>Установка дополнительного сервера приложений SAP hello

Установите SAP дополнительные приложения сервера (Консультанты) на всех виртуальных машин hello, что был указан toohost экземпляр сервера приложений SAP. Например, на <*SID*> - di - 1 слишком <*SID*> - di -&lt;n&gt;.

> [!NOTE]
> Это завершает установку hello в системе SAP NetWeaver высокого уровня доступности. Затем перейдите к тестированию отработки отказа.
>


## <a name="18aa2b9d-92d2-4c0e-8ddd-5acaabda99e9"></a>Тестирование отработки отказа экземпляра SAP ASCS/SCS hello и SIOS репликации
Он просто tootest и мониторинг экземпляра SAP ASCS/SCS перехода на другой ресурс и SIOS репликации дисков с помощью диспетчера отказоустойчивости кластеров и средства настройки и управления SIOS DataKeeper hello.

### <a name="65fdef0f-9f94-41f9-b314-ea45bbfea445"></a> Экземпляр SAP ASCS/SCS выполняется на узле A кластера

Hello **SAP PR1** группы кластера выполняется на узле кластера, а. Например, на **pr1-ascs-0**. Назначить hello общий диск S, который является частью hello **SAP PR1** кластера группы и использует какой экземпляр ASCS/SCS hello, а toocluster узла.

![На рисунке 61: Диспетчер отказоустойчивости кластеров: hello SAP < SID > Кластерная группа работает на узле кластера A][sap-ha-guide-figure-5000]

_**На рисунке 61:** Диспетчер отказоустойчивости кластеров: hello SAP <*SID*> группы кластера выполняется на узле кластера A_

В hello SIOS DataKeeper управления и средство настройки вы увидите этому общему диску hello синхронно репликации данных из источника hello тома диск S на узле кластера toohello целевой том диск S на узле б. Например, реплицированных с **pr1-ascs-0 [10.0.0.40]** слишком**pr1-ascs-1 [10.0.0.41]**.

![На рисунке 62: В SIOS DataKeeper реплицировать hello локального тома с узла кластера узла toocluster B][sap-ha-guide-figure-5001]

_**На рисунке 62:** в SIOS DataKeeper реплицировать hello локального тома с узла кластера узла toocluster B_

### <a name="5e959fa9-8fcd-49e5-a12c-37f6ba07b916"></a>Переход с узла A toonode B

1.  Выберите один из этих параметров tooinitiate отработку отказа hello SAP <*SID*> группы кластера из кластера узел A toocluster б.
  - воспользовавшись диспетчером отказоустойчивости кластеров;  
  - воспользовавшись командами PowerShell отказоустойчивого кластера;

  ```PowerShell
  $SAPSID = "PR1"     # SAP <SID>

  $SAPClusterGroup = "SAP $SAPSID"
  Move-ClusterGroup -Name $SAPClusterGroup

  ```
2.  Перезапустите объект узла кластера в hello Windows гостевой операционной системы (при этом инициируется автоматический переход hello SAP <*SID*> группы кластера из узла A toonode B).  
3.  Перезапустите A узел кластера от hello портал Azure (это инициирует автоматический переход из hello SAP <*SID*> группы кластера из узла A toonode B).  
4.  Перезапустите объект узла кластера с помощью Azure PowerShell (при этом инициируется автоматический переход hello SAP <*SID*> группы кластера из узла A toonode B).

  После отработки отказа hello SAP <*SID*> группы кластера выполняется на кластерном узле б. Например, он выполняется **pr1-ascs-1**.

  ![На рисунке 63: В диспетчере отказоустойчивости кластеров hello SAP < SID > Кластерная группа работает на узле кластера B][sap-ha-guide-figure-5002]

  _**На рисунке 63**: В диспетчере отказоустойчивости кластеров, hello SAP <*SID*> группы кластера выполняется на кластерном узле B_

  Hello общий диск теперь смонтирована в кластере узла B. SIOS DataKeeper является репликация данных из исходного тома диска S на диске кластера, узел B tootarget тома S на узле кластера, а. Например, он осуществляет репликацию с **pr1-ascs-1 [10.0.0.41]** слишком**pr1-ascs-0 [10.0.0.40]**.

  ![На рисунке 64: SIOS DataKeeper реплицирует hello локального тома из кластера узел B toocluster A][sap-ha-guide-figure-5003]

  _**На рисунке 64:** SIOS DataKeeper реплицирует hello локального тома из кластера узел B toocluster A_
