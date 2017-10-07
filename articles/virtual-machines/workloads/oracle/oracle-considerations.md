---
title: "aaaOracle решений на базе Microsoft Azure | Документы Microsoft"
description: "Узнайте о поддерживаемых конфигурациях и ограничениях решений Oracle в Microsoft Azure."
services: virtual-machines-linux
documentationcenter: 
manager: timlt
author: rickstercdn
tags: azure-resource-management
ms.assetid: 5d71886b-463a-43ae-b61f-35c6fc9bae25
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 06/15/2017
ms.author: rclaus
ms.openlocfilehash: 54dc62e76129535da7fb6f131af90c83adfec6cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="oracle-solutions-and-their-deployment-on-microsoft-azure"></a>Решения Oracle в Microsoft Azure и их развертывание
В этой статье представлены сведения, необходимые toosuccesfully развертывания различных решений Oracle в Microsoft Azure. Эти решения основываются на опубликованный Oracle в hello Azure Marketplace образов виртуальных машин. tooget список доступных образов, запустите следующую команду hello:
```azurecli-interactive
az vm image list --publisher oracle -o table --all
```
На hello 6 16 2017 г. список изображений не hello следующее:
```bash
Offer                   Publisher    Sku                     Urn                                                          Version
----------------------  -----------  ----------------------  -----------------------------------------------------------  -------------
Oracle-Database-Ee      Oracle       12.1.0.2                Oracle:Oracle-Database-Ee:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Database-Se      Oracle       12.1.0.2                Oracle:Oracle-Database-Se:12.1.0.2:12.1.20170202             12.1.20170202
Oracle-Linux            Oracle       6.4                     Oracle:Oracle-Linux:6.4:6.4.20141206                         6.4.20141206
Oracle-Linux            Oracle       6.7                     Oracle:Oracle-Linux:6.7:6.7.20161007                         6.7.20161007
Oracle-Linux            Oracle       6.8                     Oracle:Oracle-Linux:6.8:6.8.20161020                         6.8.20161020
Oracle-Linux            Oracle       6.9                     Oracle:Oracle-Linux:6.9:6.9.20170406                         6.9.20170406
Oracle-Linux            Oracle       7.0                     Oracle:Oracle-Linux:7.0:7.0.20141217                         7.0.20141217
Oracle-Linux            Oracle       7.2                     Oracle:Oracle-Linux:7.2:7.2.20161020                         7.2.20161020
Oracle-Linux            Oracle       7.3                     Oracle:Oracle-Linux:7.3:7.3.20170320                         7.3.20170320
Oracle-WebLogic-Server  Oracle       Oracle-WebLogic-Server  Oracle:Oracle-WebLogic-Server:Oracle-WebLogic-Server:12.1.2  12.1.2
```

Это образы с использованием собственной лицензии, а значит вы будете оплачивать только использование ресурсов вычислений и хранения, а также сетевых ресурсов, связанных с работой виртуальной машины.  Предполагается, надлежащим образом лицензированной toouse программное обеспечение Oracle и наличие текущего соглашения поддержки на месте с Oracle. Oracle гарантируется лицензий из tooAzure в локальной среде. Hello опубликован в статье [Oracle и Microsoft](http://www.oracle.com/technetwork/topics/cloud/faq-1963009.html) Примечание о мобильности лицензий. 

Пользователям можно также toobase их решений на пользовательских образов их создания с нуля в Azure или передачи пользовательских образов из их в локальных средах.

## <a name="support-for-jd-edwards"></a>Поддержка JD Edwards
Примечание tooOracle поддержки в соответствии с [2178595.1 идентификатор Doc](https://support.oracle.com/epmos/faces/DocumentDisplay?_afrLoop=573435677515785&id=2178595.1&_afrWindowMode=0&_adf.ctrl-state=o852dw7d_4) , JD Edwards EnterpriseOne версиях 9.2 и более поздних версий поддерживаются **любые открытые облачные предложения** , удовлетворяющей их конкретных `Minimum Technical Requirements` (MTR).  Вам потребуется toocreate пользовательские образы, которые соответствуют спецификациям MTR для операционной системы и программного обеспечения совместимости приложений. 

## <a name="oracle-database-virtual-machine-images"></a>Образы виртуальных машин для базы данных Oracle
Oracle поддерживает выполнение выпусков базы данных Oracle 12.1 Standard и Enterprise в Azure с использованием образов виртуальных машин на базе Oracle Linux.  Для hello наилучшей производительности для рабочих нагрузок базы данных Oracle в Azure быть убедиться, что образ виртуальной Машины tooproperly размер hello и использовать диски управляемого резервного хранилища Premium. Инструкции по tooquickly, как получить база данных Oracle работает в Azure с помощью hello Oracle опубликованных образа виртуальной Машины [повторите Пошаговое руководство быстрый запуск базы данных Oracle hello](oracle-database-quick-create.md).

### <a name="attached-disk-configuration-options"></a>Варианты конфигурации подключенного диска

Присоединенные диски используют hello службы хранилища больших двоичных объектов. Теоретически каждый диск уровня "Стандартный" способен выполнять максимум около 500 операций ввода-вывода в секунду (IOPS). Наш предложением высшего диска является предпочтительным для высокопроизводительных рабочих нагрузок баз данных и приемлемое вверх too5000 IOP для дисков. Хотя можно использовать один диск, если удовлетворяет требованиям к производительности требуется - hello эффективной производительности операций ввода-ВЫВОДА можно повысить, если использовать несколько дисков, подключенных распределяться базы данных, а затем с помощью управления автоматического хранения данных Oracle (ASM). Дополнительные сведения об Oracle ASM см. в обзоре [Oracle Automatic Storage](http://www.oracle.com/technetwork/database/index-100339.html). Пример того, как tooinstall и настроить Oracle ASM на виртуальной Машине Linux Azure — вы можете повторить hello [Установка и настройка управления хранением автоматических Oracle](configure-oracle-asm.md) учебника.

### <a name="oracle-realtime-application-cluster-rac"></a>Решение Oracle Real Application Clusters (RAC)
Oracle RAC — спроектированный toomitigate hello сбоя одного узла в кластер с несколькими узлами в локальной конфигурации.  Он основывается на двух локальных технологии, которые не являются собственного toohyper-общедоступных облачных средах: многоадресной рассылки в сети и общий диск. Существуют решения сторонних разработчиков [например FlashGrid](https://www.flashgrid.io/oracle-rac-in-azure/) эмулируют эти технологии, если вам требуется toodeploy Oracle RAC в Azure. 

### <a name="high-availability-and-disaster-recovery-considerations"></a>Рекомендации по высокой доступности и аварийному восстановлению
При использовании баз данных Oracle в Azure, вы несете ответственность для реализации высокого уровня доступности и аварийного восстановления решения tooavoid простоев. 

Высокую доступность и аварийное восстановление в Oracle Database Enterprise Edition (без RAC) в Azure можно реализовать с помощью [Data Guard, Active Data Guard](http://www.oracle.com/technetwork/articles/oem/dataguardoverview-083155.html) или [Oracle Golden Gate](http://www.oracle.com/technetwork/middleware/goldengate), разместив две базы данных в двух отдельных виртуальных машинах. Обе виртуальные машины должны быть в hello же [виртуальной сети](https://azure.microsoft.com/documentation/services/virtual-network/) tooensure, они могли обращаться друг с другом посредством частного IP-адреса постоянного hello.  Кроме того, рекомендуется размещать виртуальные машины hello в hello же доступности задайте tooallow Azure tooplace их в отдельные домены отказоустойчивости и доменах обновления.  Вы хотите toohave геоизбыточность - может иметь эти две базы данных репликации между двух разных регионах и подключения двух экземпляров hello VPN-шлюза.

У нас есть Учебник «[DataGuard Oracle Реализуйте в Azure](configure-oracle-dataguard.md)» которого содержатся пошаговые процедуры tootrial hello базовая настройка это в Azure.  

При использовании Oracle Data Guard высокую доступность можно обеспечить, разместив базу данных источника в одной виртуальной машине и базу данных получателя (резервную) в другой виртуальной машине и настроив одностороннюю репликацию между ними. Hello результат — toohello доступ для чтения, копия базы данных hello. С Oracle GoldenGate можно настроить двунаправленной репликации между двумя базами данных hello. tooset копии решения высокой доступности для баз данных с помощью этих средств. в статье toolearn [Active Data Guard](http://www.oracle.com/technetwork/database/features/availability/data-guard-documentation-152848.html) и [GoldenGate](http://docs.oracle.com/goldengate/1212/gg-winux/index.html) документации на веб-сайте Oracle hello. Если вам требуется чтения и записи toohello доступ, копия базы данных hello, можно использовать [Active Oracle Data Guard](http://www.oracle.com/uk/products/database/options/active-data-guard/overview/index.html).

У нас есть Учебник «[реализуйте Oracle GoldenGate в Azure](configure-oracle-golden-gate.md)» которого расскажет hello seup основные процедуры tootrial это в Azure.

Несмотря на наличие решения высокого уровня ДОСТУПНОСТИ и аварийного восстановления, разработана в Azure, требуется tooensure имеется стратегию резервного копирования в месте toorestore базы данных.  У нас есть Учебник [резервное копирование и восстановление базы данных Oracle](oracle-backup-recovery.md) которого расскажет hello Основная процедура для установления consistant резервной копии.

## <a name="oracle-weblogic-server-virtual-machine-images"></a>Образы виртуальных машин Oracle WebLogic Server
* **Кластеризация поддерживается только в выпуске Enterprise Edition.** Вы можете toouse только при использовании кластеризации WebLogic Enterprise Edition WebLogic Server "hello". Не используйте кластеризацию с выпуском WebLogic Server Standard Edition.
* **Не поддерживается многоадресная рассылка по UDP.** Azure поддерживает одноадресную рассылку по UDP, но не поддерживает ни многоадресную, ни широковещательную рассылку. WebLogic Server — может toorely на возможностях Azure UDP одноадресной рассылки. Для лучше всего результатов, полагаясь на одноадресной рассылки UDP, мы рекомендуем размер кластера WebLogic hello храниться статическим, или сохраняются с не более чем 10 управляемых серверов, входящих в кластер hello.
* **WebLogic Server ожидает, что общие и частные порты toobe hello одинаковы для T3 доступа (например, при использовании Enterprise JavaBeans).** Рассмотрим многоуровневый сценарий, при котором приложение уровня служб (EJB) выполняется в кластере WebLogic Server, состоящем из двух или более виртуальных машин в виртуальной сети с именем **SLWLS**. Hello клиентский уровень находится в другой подсети в hello одной виртуальной сети, простой программы Java попытки toocall EJB слоя служб hello. Так как это уровень службы hello баланс необходимые tooload общедоступную конечную точку с балансировкой нагрузки должен toobe, созданных для hello виртуальных машин в hello кластера WebLogic Server. Если hello частный порт, указываемое отличается от hello открытый порт (например, 7006:7008), возникает ошибка hello ниже:

       [java] javax.naming.CommunicationException [Root exception is java.net.ConnectException: t3://example.cloudapp.net:7006:

       Bootstrap to: example.cloudapp.net/138.91.142.178:7006' over: 't3' got an error or timed out]

   Это так, как при любом удаленном доступе T3 WebLogic Server предполагает, что порт подсистемы балансировки нагрузки hello и toobe порт сервера WebLogic управляемых hello hello таким же. В hello выше случая hello клиент обращается к порту 7006 (порт подсистемы балансировки нагрузки hello) и управляемый сервер Здравствуй прослушивает 7008 (hello частный порт). Это ограничение применяется только для доступа к каналу T3, а не к HTTP.

   tooavoid этой проблемы, используйте один из hello следующие решения:

  * Используйте hello же закрытый и доступа к конечным точкам выделенного tooT3 балансировки открытые порты для загрузки.
  * Включить следующий параметр виртуальной машины Java при запуске сервера WebLogic hello:

         -Dweblogic.rjvm.enableprotocolswitch=true

Дополнительные сведения см. в статье базы знаний **860340.1** по адресу <http://support.oracle.com>.

* **Ограничения для динамической кластеризации и балансировки нагрузки.** Предположим, что требуется toouse динамического кластера в сервера WebLogic и предоставляется через единый, открытые с балансировкой нагрузки конечную точку в Azure. Это можно сделать, пока использовать определенный номер порта для каждого из hello управляемых серверах (назначение не динамически из диапазона) и не запускайте более управляемых серверов, чем число машин отслеживания Здравствуйте, администратор (то есть не более чем один управляемый сервер на virt ual компьютера). Если конфигурация приводит несколько серверов WebLogic выполняется запуск, чем число виртуальных машин (то есть, где несколько экземпляров сервера WebLogic общего ресурса hello одной виртуальной машине), то для более чем одного из этих экземпляров сервера WebLogic невозможно tooa toobind серверы заданный номер порта — hello другим пользователям на этой виртуальной машине, будут завершаться сбоем.

   На hello другой стороны, если настроить hello администратора сервера tooautomatically назначить уникальные номера портов tooits управляемых серверов, то Балансировка нагрузки невозможен, так как Azure не поддерживает сопоставление портов частной один открытый порт toomultiple, как было бы является обязательным для этой конфигурации.
* **Несколько экземпляров сервера Weblogic Server на виртуальной машине.** В зависимости от требований вашего развертывания, следует рассмотреть возможность hello в нескольких экземпляров сервера WebLogic hello одной виртуальной машине, если достаточно большой hello виртуальной машины. Например на виртуальной машине среднего размера, который содержит два ядра ЦП, можно выбрать toorun двух экземпляров сервера WebLogic. Обратите внимание, что по-прежнему рекомендуется избегать введение в архитектуру, которая бы hello случай, если вы использовали только одну виртуальную машину, на котором работает несколько экземпляров сервера WebLogic единых точек отказа. Лучше использовать не менее двух виртуальных машин, на каждой из которых может выполняться несколько экземпляров WebLogic Server. Каждый из этих экземпляров сервера WebLogic все еще может быть частью hello одного кластера. Обратите внимание, однако он в настоящее время не поддерживается hello toouse балансировки Azure tooload конечных точек, предоставляемых развертыванием сервера WebLogic в одной виртуальной машине, так как Подсистема балансировки нагрузки Azure требует toobe hello серверов с балансировкой нагрузки, распределенных между уникальные виртуальные машины.

## <a name="oracle-jdk-virtual-machine-images"></a>Образы виртуальных машин JDK для Oracle
* **Последние обновления JDK 6 и 7.** Хотя рекомендуется использовать hello последний открытый, поддерживаемые версии Java (в настоящее время Java 8), Azure также доступны JDK 6 и 7 изображения. Этот способ предназначен для приложений прежних версий, которые еще не готовы toobe обновления tooJDK 8. Хотя образы JDK tooprevious обновления больше не может быть доступен toohello широкой общественности, данный hello связи с Oracle, hello JDK 6 и 7 образов, предоставляемых Azure, Microsoft предназначены toocontain более новое обновление закрытым, предоставляемая обычно Oracle tooonly группу Oracle поддерживаемых клиентов. Новые версии изображений hello JDK будет предоставляться со временем на обновленные версии JDK 6 и 7.

   Hello JDK, доступных в этом JDK 6 и 7 изображения и hello виртуальных машин и образы, производных от них, может использоваться только в пределах Azure.
* **64-разрядный JDK.** образы виртуальных машин Oracle WebLogic Server Hello и образы виртуальных машин Oracle JDK hello, предоставляемые Azure содержат hello 64-разрядные версии Windows Server и hello JDK.

## <a name="next-steps"></a>Дальнейшие действия
Вы узнали о текущих решениях Oracle в Microsoft Azure. Следующим шагом является toogo и развертывания первой базы данных Oracle в Azure.
- Повторите hello [Создание базы данных Oracle в Azure](oracle-database-quick-create.md) учебника tooget работы.
