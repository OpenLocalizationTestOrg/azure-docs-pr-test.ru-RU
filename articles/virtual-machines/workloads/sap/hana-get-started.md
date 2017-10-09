---
title: "Краткое руководство по установке одного экземпляра SAP HANA вручную на виртуальных машинах Azure | Документация Майкрософт"
description: "Краткое руководство по установке одного экземпляра SAP HANA вручную на виртуальных машинах Azure"
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: c51a2a06-6e97-429b-a346-b433a785c9f0
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 09/15/2016
ms.author: hermannd
ms.openlocfilehash: 57b58b8e07379eed5641f5f89d55b38f52c69e44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="quickstart-manual-installation-of-single-instance-sap-hana-on-azure-vms"></a>Краткое руководство по установке одного экземпляра SAP HANA вручную на виртуальных машинах Azure
## <a name="introduction"></a>Введение
Это руководство поможет вам настроить один экземпляр SAP HANA на виртуальных машинах Azure при установке SAP NetWeaver 7.5 и SAP HANA 1.0 SP12 вручную. Hello в этом руководстве нацелено на развертывание SAP HANA в Azure. Оно не заменяет документацию по SAP. 

>[!Note]
>Это руководство описывает развертывание SAP HANA на виртуальных машинах Azure. Сведения о развертывании HANA SAP на крупных экземплярах HANA см. в статье [Использование SAP на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/get-started).
 
## <a name="prerequisites"></a>Предварительные требования
В руководстве предполагается, что вы знакомы с инфраструктурой как услугой (IaaS), т. е. умеете выполнять такие задачи:
 * Как toodeploy виртуальных машин или виртуальные сети через hello портал Azure или PowerShell.
 * Hello Azure кросс платформенных интерфейс командной строки (CLI), включая шаблоны JavaScript Object Notation (JSON) toouse параметр hello.

В этом руководстве также предполагается, что вы знакомы со следующими технологиями и процедурами:
* SAP HANA и SAP NetWeaver и как tooinstall их локально.
* Установка и эксплуатации SAP HANA и экземпляров приложения SAP в Azure.
* Здравствуйте, следующие основные понятия и процедуры:
   * Планирование развертывания SAP в Azure, в т. ч. планирование виртуальной сети Azure и использование службы хранилища Azure. См. статью [SAP NetWeaver на виртуальных машинах Windows. Руководство по планированию и внедрению](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/planning-guide).
   * Развертывание принципы и способы toodeploy ВМ в Azure. См. статью [Развертывание программного обеспечения SAP на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/deployment-guide).
   * Обеспечение высокого уровня доступности для SAP NetWeaver ASCS (ABAP SAP Central Services), SCS (SAP Central Services) и ERS (расчет оценки поступления) в Azure. См. статью [Высокий уровень доступности SAP NetWeaver на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-guide).
   * Сведения о том, как tooimprove эффективность благодаря использованию для установки нескольких SID ASCS/SCS в Azure. См. статью [Создание конфигурации с несколькими идентификаторами безопасности SAP NetWeaver](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/high-availability-multi-sid). 
   * Принципы работы SAP NetWeaver на виртуальных машинах Linux в Azure. См. статью [Запуск SAP NetWeaver на виртуальных машинах SUSE Linux в Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/suse-quickstart). Это руководство предоставляет определенные параметры для Linux в виртуальных машинах Azure и сведения о как tooproperly присоединять tooLinux хранилища Azure диски виртуальных машин.

Сейчас виртуальные машины Azure сертифицированы SAP только для конфигураций вертикального масштабирования SAP HANA. Конфигурации горизонтального масштабирования при использовании рабочих нагрузок SAP HANA пока не поддерживаются. Сведения об обеспечении высокого уровня доступности SAP HANA для конфигураций вертикального масштабирования см. в статье [Высокий уровень доступности SAP HANA на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-high-availability).

Если вы ищете tooget экземпляра SAP HANA или S/4HANA или система BW/4HANA, развертывание очень быстро времени, следует рассмотреть использование hello [устройство библиотеки SAP облака](http://cal.sap.com). Документацию по развертыванию системы S/4HANA с использованием клиентской лицензии SAP в Azure см. в статье [Развертывание SAP S/4HANA или BW/4HANA в Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h). Все необходимые toohave — подписка Azure и пользователь SAP, могут быть зарегистрированы с SAP облачной устройства библиотеки.

## <a name="additional-resources"></a>Дополнительные ресурсы
### <a name="sap-hana-backup"></a>Резервное копирование SAP HANA
Сведения о резервном копировании баз данных SAP HANA на виртуальных машинах Azure см. в следующих статьях:
* [Руководство по резервному копированию SAP HANA на виртуальных машинах Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-guide)
* [Резервное копирование SAP HANA в Azure на уровне файлов](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-file-level)
* [Резервное копирование SAP HANA на основе моментальных снимков хранилища](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/sap-hana-backup-storage-snapshots)

### <a name="sap-cloud-appliance-library"></a>Библиотека SAP Cloud Appliance Library
Сведения об использовании библиотеки устройства облака SAP toodeploy S/4HANA или BW/4HANA см. в разделе [развертывания SAP S/4HANA или BW/4HANA в Microsoft Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/cal-s4h).

### <a name="sap-hana-supported-operating-systems"></a>Операционные системы, поддерживаемые платформой SAP HANA
Сведения о поддерживаемых операционных системах для SAP HANA см. в [примечании по поддержке SAP № 2235581](https://launchpad.support.sap.com/#/notes/2235581/E). На виртуальных машинах Azure поддерживаются только эти операционные системы. Hello следующих операционных систем, поддерживаемых toodeploy HANA SAP в Azure: 

* SUSE Linux Enterprise Server 12.x;
* Red Hat Enterprise Linux 7.2

Дополнительную документацию SAP по платформе SAP HANA и разным дистрибутивах Linux см. по ссылкам ниже.

* [SAP Support Note #171356 – SAP Software on Linux: General Information](https://launchpad.support.sap.com/#/notes/1984787) (Примечание по поддержке SAP №171356. Общие сведения о ПО SAP на платформе Linux).
* [SAP Support Note #1944799 – SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html) (Примечание по поддержке SAP №1944799. Рекомендации по установке SAP HANA в ОС SLES).
* [SAP Support Note #2205917 – SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E) (Примечание по поддержке SAP №2205917. База данных SAP HANA: рекомендуемые параметры ОС для SLES 12 для приложений SAP).
* [SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: Installation Notes](https://launchpad.support.sap.com/#/notes/1984787) (Примечание по поддержке SAP №1984787. Заметки об установке SUSE Linux Enterprise Server 12).
* [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Примечание по поддержке SAP №1391070. Решения UUID для Linux).
* [SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879) (Примечание по поддержке SAP № 2009879. Рекомендации для установки SAP HANA на ОС Red Hat Enterprise Linux (RHEL));
* [2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690/E) (Примечание по поддержке SAP № 2292690. База данных SAP HANA: рекомендуемые параметры операционной системы для RHEL 7).

### <a name="sap-monitoring-in-azure"></a>Мониторинг SAP в Azure
Сведения о мониторинге SAP в Azure см. по ссылкам ниже.

* [Примечание к SAP № 2191498](https://launchpad.support.sap.com/#/notes/2191498/E) — сведения о расширенном мониторинге с помощью виртуальных машин Linux в Azure. 
* [Примечание к SAP № 1102124](https://launchpad.support.sap.com/#/notes/1102124/E) — сведения о SAPOSCOL в Linux. 
* [Примечание к SAP № 2178632](https://launchpad.support.sap.com/#/notes/2178632/E) — ключевые метрики мониторинга для SAP в Microsoft Azure.

### <a name="azure-vm-types"></a>Типы виртуальных машин Azure
Типы виртуальных машин Azure и поддерживаемые сценарии рабочих нагрузок SAP, используемых с SAP HANA, описаны на [странице сертифицированных платформ IaaS](https://www.sap.com/dmc/exp/2014-09-02-hana-hardware/enEN/iaas.html). 

Azure типы ВМ, сертифицирован SAP SAP NetWeaver или S/4HANA уровня приложения hello описаны в [SAP Примечание 1928533 — приложения SAP в Azure: поддерживаемые продукты и виртуальной Машины Azure типы](https://launchpad.support.sap.com/#/notes/1928533/E).

>[!Note]
>Интеграция с SAP Linux Azure поддерживается только для диспетчера ресурсов Azure и не hello классической модели развертывания. 

## <a name="manual-installation-of-sap-hana"></a>Установка SAP HANA вручную
В этом руководстве описывается toomanually установки SAP HANA на виртуальных машинах Azure двумя способами:

* С помощью диспетчера подготовки по SAP (SWPM) как часть распределенной установке NetWeaver в действии «установить экземпляр базы данных» hello
* С помощью hello SAP HANA базы данных диспетчера жизненного цикла, HDBLCM и последующая установка NetWeaver

Также можно SWPM tooinstall все компоненты (SAP HANA, сервера приложений SAP hello и экземпляр ASCS hello) в одной виртуальной Машине, как описано в этом [объявления блог SAP HANA](https://blogs.saphana.com/2013/12/31/announcement-sap-hana-and-sap-netweaver-as-abap-deployed-on-one-server-is-generally-available/). Этот параметр, не описанные в этом руководстве краткое руководство, но hello проблемы, которые необходимо принимать во внимание: hello таким же.

Прежде чем начать установку, мы рекомендуем прочитать hello «Подготовка Azure виртуальные машины для ручной установки SAP HANA» данного руководства. Это поможет предотвратить несколько основных ошибок, которые могут возникнуть при использовании только конфигурации виртуальной машины Azure по умолчанию.

## <a name="key-steps-for-sap-hana-installation-when-you-use-sap-swpm"></a>Основные шаги по установке SAP HANA при использовании SAP SWPM
В этом разделе перечислены hello основные шаги для установки вручную, экземпляра SAP HANA, при использовании установки SAP SWPM tooperform распределенных 7.5 SAP NetWeaver. Hello отдельные действия описаны более подробно на снимках экрана данного руководства.

1. Создайте виртуальную сеть Azure с двумя тестовыми виртуальными машинами.
2. Развертывание hello две виртуальные машины Azure с операционными системами (в нашем примере SUSE Linux Enterprise Server (SLES) и SLES для SP1 12 приложения SAP), модели toohello диспетчера ресурсов Azure в соответствии с.
3. Присоедините два Azure standard или premium хранилища диски (например, 75 ГБ или 500 ГБ) toohello ВМ сервера приложений.
4. Присоединение сервера базы данных HANA toohello дисков хранилища premium виртуальной Машины. Дополнительные сведения см. в разделе hello раздел «Диск установки» далее в этом руководстве.
5. В зависимости от требований размер или пропускной способности присоединить несколько дисков и создайте чередующиеся тома с помощью управления логический том или средство администрирования нескольких устройств (MDADM) на уровне hello ОС внутри hello виртуальной Машины.
6. Создайте XFS файловых систем на hello присоединенных дисков или логических томах.
7. Подключите hello новые XFS файловые системы на уровне hello ОС. Используйте одну файловую систему для всего программного обеспечения SAP hello. Используйте hello других файловой системы для каталога /sapmnt hello и резервные копии, например. На сервере базы данных SAP HANA hello подключите hello XFS файловые системы на дисках хранилища premium hello как /hana и /usr/sap. Этот процесс является необходимые tooprevent hello корневой файловой системы, который не является большой на виртуальных машинах Azure Linux, переполнения.
8. Введите hello локальных IP-адресов hello тестирования виртуальных машин в файле hello/etc/hosts.
9. Введите hello **nofail** параметр в файле hello/etc/fstab.
10. Задайте параметры ядра Linux, версия ОС Linux toohello, которую вы используете в соответствии с. Дополнительные сведения см. соответствующий SAP примечания hello, посвященные HANA и hello раздел «Ядра параметров» в данном руководстве.
11. Добавьте область буфера.
12. Дополнительно можно установите графического рабочего стола на тест hello виртуальных машин. В противном случае используйте удаленную установку SAPinst.
13. Загрузите программное обеспечение SAP hello из hello услугами SAP.
14. Установите экземпляр SAP ASCS hello на сервере приложения hello виртуальной Машины.
15. Общий каталог /sapmnt hello среди hello проверить виртуальные машины с помощью NFS. сервер приложений Hello виртуальной Машины — hello NFS-сервера.
16. Установите экземпляр hello базы данных, включая HANA, с помощью SWPM на сервере DB hello виртуальной Машины.
17. Установите сервер основного приложения hello (PAS) на сервере приложений hello виртуальной Машины.
18. Запустите консоль управления SAP (SAP MC). Подключитесь к консоли с помощью графического пользовательского интерфейса SAP или HANA Studio.

## <a name="key-steps-for-sap-hana-installation-when-you-use-hdblcm"></a>Основные шаги по установке SAP HANA при использовании HDBLCM
В этом разделе перечислены hello основные шаги для установки вручную, экземпляра SAP HANA, при использовании установки SAP HDBLCM tooperform распределенных 7.5 SAP NetWeaver. Hello отдельные шаги описаны более подробно в снимки экрана в этом руководстве.

1. Создайте виртуальную сеть Azure с двумя тестовыми виртуальными машинами.
2. Две виртуальные машины Azure с операционными системами (в нашем примере SLES и SLES для SP1 12 приложения SAP) развертывание согласно модели toohello диспетчера ресурсов Azure.
3. Присоедините два Azure стандартной или сервер приложений toohello диски (например, 75 ГБ или 500 ГБ) хранилища premium виртуальной Машины.
4. Присоединение сервера базы данных HANA toohello дисков хранилища premium виртуальной Машины. Дополнительные сведения см. в разделе hello раздел «Диск установки» далее в этом руководстве.
5. В зависимости от требований размер или пропускной способности присоединить несколько дисков и создать чередующиеся тома с помощью управления логический том или средство администрирования нескольких устройств (MDADM) на уровне hello ОС внутри hello виртуальной Машины.
6. Создайте XFS файловых систем на hello присоединенных дисков или логических томах.
7. Подключите hello новые XFS файловые системы на уровне hello ОС. Использовать одну файловую систему для всего программного обеспечения SAP hello и второй для каталога /sapmnt hello и резервные копии, например hello использования. На сервере базы данных SAP HANA hello подключите hello XFS файловые системы на дисках хранилища premium hello как /hana и /usr/sap. Этот процесс необходим toohelp допустить hello корневой файловой системы, который не является большой на виртуальных машинах Azure Linux, переполнения.
8. Введите hello локальных IP-адресов hello тестирования виртуальных машин в файле hello/etc/hosts.
9. Введите hello **nofail** параметр в файле hello/etc/fstab.
10. Задайте параметры ядра, версия ОС Linux toohello, которую вы используете в соответствии с. Дополнительные сведения см. соответствующий SAP примечания hello, посвященные HANA и hello раздел «Ядра параметров» в данном руководстве.
11. Добавьте область буфера.
12. Дополнительно можно установите графического рабочего стола на тест hello виртуальных машин. В противном случае используйте удаленную установку SAPinst.
13. Загрузите программное обеспечение SAP hello из hello услугами SAP.
14. Создайте группу, sapsys, с группой Идентификатором 1001 на сервере базы данных HANA hello виртуальной Машины.
15. Установите SAP HANA на сервере DB hello виртуальной Машины с помощью диспетчера жизненного цикла базы данных HANA (HDBLCM).
16. Установите экземпляр SAP ASCS hello на сервере приложения hello виртуальной Машины.
17. Общий каталог /sapmnt hello среди hello проверить виртуальные машины с помощью NFS. сервер приложений Hello виртуальной Машины — hello NFS-сервера.
18. Установите экземпляр hello базы данных, включая HANA, с помощью SWPM на сервере базы данных HANA hello виртуальной Машины.
19. Установите сервер основного приложения hello (PAS) на сервере приложений hello виртуальной Машины.
20. Запустите консоль управления SAP. Подключитесь к консоли с помощью графического пользовательского интерфейса SAP или HANA Studio.

## <a name="preparing-azure-vms-for-a-manual-installation-of-sap-hana"></a>Подготовка виртуальных машин Azure к установке SAP HANA вручную
В этом разделе рассматриваются следующие вопросы hello:

* Обновления ОС
* настройка диска;
* параметры ядра;
* Файловые системы
* файл Hello/etc/hosts
* Hello/etc/fstab файла

### <a name="os-updates"></a>Обновления ОС
Перед установкой дополнительного программного обеспечения проверьте наличие обновлений и исправлений для ОС Linux. Установив исправление, может быть tooavoid возможности поддержки toohello вызова.

Убедитесь, что вы используете следующие операционные системы:
* SUSE Linux Enterprise Server for SAP Applications;
* Red Hat Enterprise Linux for SAP Applications или Red Hat Enterprise Linux for SAP HANA. 

Если это еще не сделано, зарегистрируйте hello развертывание операционной системы в своей подписке Linux от поставщика Linux hello. Обратите внимание, что для SUSE есть также образы ОС для приложений SAP, которые уже содержат службы и зарегистрированы автоматически.

Ниже приведен пример проверки наличия доступных исправлений для SUSE Linux с помощью hello **zypper** команды:

 `sudo zypper list-patches`

В зависимости от типа hello проблему исправления классифицируются по категории и серьезности. Часто используемые значения категорий: **security** (Безопасность), **recommended** (Рекомендуемое), **optional** (Необязательное), **feature** (Компонент), **document** (Документ) или **yast** (Еще один инструмент установки).
Часто используемые значения уровней серьезности: **critical** (Критическое), **important** (Важное), **moderate** (Средней важности), **low** (Низкой важности) или **unspecified** (Не указано).

Hello **zypper** команда находит только необходимые hello обновлений, установленных пакетов. Например, можно использовать эту команду:

`sudo zypper patch  --category=security,recommended --severity=critical,important`

Можно добавить параметр hello `--dry-run` tootest hello обновления без фактического обновления системы hello.


### <a name="disk-setup"></a>настройка диска;
Hello корневой файловой системы на виртуальной машине Linux в Azure имеет ограничение по размеру. Таким образом это необходимые tooattach дополнительное дисковое пространство tooan виртуальной Машины Azure для выполнения SAP. Для сервера приложений SAP виртуальных машинах Azure hello использование дисков Azure стандартное хранилище может быть достаточно. Однако для ВМ Azure СУБД SAP HANA, hello использовать диски хранилища Azure Premium для реализации производственных и нерабочей является обязательным.

В зависимости от hello [требования к хранилищу SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html), рекомендуется следующая конфигурация хранилища Azure Premium hello: 

| SKU виртуальной машины | ОЗУ |  /hana/data и /hana/log, <br /> чередующиеся с диспетчером логических томов или MDADM | /hana/shared | том /root | /usr/sap |
| --- | --- | --- | --- | --- | --- |
| GS5 | 448 ГБ | 2 x P30 | 1 x P20 | 1 x P10 | 1 x P10 | 

В конфигурации диска предлагаемые hello hello HANA данных и журнала тома помещаются в же набор дисков хранилища Azure premium, которые чередуются с LVM или MDADM hello. Нет необходимости toodefine любой избыточности RAID уровня, так как хранилище Azure класса Premium сохраняет три образа hello дисков для обеспечения избыточности. toomake следует настроить достаточный объем хранилища, обратитесь к hello [требования к хранилищу SAP HANA TDI](https://www.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) и [установки сервера SAP HANA и руководство по обновлению](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm). Учитывать hello другой виртуальный жесткий диск (VHD) пропускной способности объемов hello другой Azure premium дисков, описанные в [хранилище Premium высокой производительности и управляемых диски для виртуальных машин](https://docs.microsoft.com/azure/storage/storage-premium-storage). 

Можно добавить дополнительные хранилища premium диски ВМ СУБД HANA toohello для хранения резервных копий журнала транзакций или базы данных.

Дополнительные сведения о tooconfigure две основные средства, используемые hello чередование дисков см. следующие статьи hello:

* [Настройка программного RAID-массива в Linux](../../linux/configure-raid.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Настройка диспетчера логических томов на виртуальной машине Linux в Azure](../../linux/configure-lvm.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Дополнительные сведения о присоединении дисков tooAzure виртуальные машины под управлением Linux в качестве гостевой ОС, см. в разделе [добавить диск tooa ВМ Linux](../../linux/add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

Хранилище Azure Premium позволяет кэширования режимы toodefine диска. Для hello чередующийся набор удерживая /hana/data и /hana/log кэширование диска должна быть отключена. Для hello других томов (дисков), hello кэширование режима должно быть установлено слишком**ReadOnly**.

Дополнительные сведения см. в статье [Хранилище класса "Премиум": высокопроизводительная служба хранилища для рабочих нагрузок виртуальных машин Azure](../../../storage/common/storage-premium-storage.md).

toofind образца JSON шаблоны для создания виртуальных машин, перейдите в слишком[шаблоны быстрый запуск Azure](https://github.com/Azure/azure-quickstart-templates).
Шаблон виртуальной машины simple-sles Hello — базовый шаблон. Оно содержит раздел хранилища с дополнительным диском данных размером 100 ГБ. Этот шаблон можно использовать в качестве базы. Вы можете адаптировать hello шаблона tooyour конкретной конфигурации.

>[!Note]
>Это важные tooattach hello хранилища Azure диск с помощью UUID, как описано в документе [под управлением SAP NetWeaver на виртуальных машинах Linux SUSE Azure Майкрософт](suse-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

В тестовой среде hello два стандартных хранилища Azure диски были сервера приложений SAP вложенного toohello виртуальной Машины, как показано на следующий снимок экрана приветствия. Один диск сохраняются все программное обеспечение SAP hello (включая NetWeaver 7.5 SAP GUI и SAP HANA) для установки. Hello второго диска обеспечивал, что достаточно свободного места были бы доступны дополнительные требования (например, данные резервного копирования и тестирования) и для каталога (то есть профили SAP) toobe hello /sapmnt, общими для всех виртуальных машин, которые принадлежат toohello ландшафт SAP же.

![Окно дисков сервера приложений SAP HANA, отображающее два диска данных и их размеры](./media/hana-get-started/image003.jpg)


### <a name="kernel-parameters"></a>параметры ядра;
SAP HANA требуются определенные параметры ядра Linux, которые не являются частью изображения стандартной коллекции Azure hello и должен быть установлен вручную. В зависимости от того, используются ли SUSE или Red Hat, hello параметры могут отличаться. Примечания по SAP Hello перечисленных выше предоставляют сведения об этих параметрах. Hello снимках экрана показано использовался SUSE Linux 12 SP1. 

SLES для общедоступной версии 12 приложений SAP и SLES для SP1 12 приложений SAP имеют новое средство, **настраиваемых adm**, что заменяет hello старый **sapconf** средство. Для средства **tuned-adm** существует специальный профиль SAP HANA. tootune hello системы SAP HANA, введите в качестве пользователя root hello следующее:

   `tuned-adm profile sap-hana`

Дополнительные сведения о **настраиваемых adm**, в разделе hello [SUSE документацию по настройке adm](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip).

В следующий снимок экрана приветствия, можно просмотреть как **настраиваемых adm** измененные hello `transparent_hugepage` и `numa_balancing` значения в соответствии с toohello обязательные параметры SAP HANA.

![средство настройки adm Hello изменяет значения в соответствии с toorequired параметров SAP HANA](./media/hana-get-started/image005.jpg)

toomake hello SAP HANA ядра параметры постоянными, используйте **grub2** на SLES 12. Дополнительные сведения о **grub2**, go toohello [структура файла конфигурации](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) раздел hello документации SUSE.

Hello следующем снимке экрана показано, как параметры ядра hello были изменены в файле конфигурации hello и затем скомпилировать с помощью **grub2 mkconfig**:

![Параметры ядра изменено в файле конфигурации hello и скомпилировать с помощью grub2 mkconfig](./media/hana-get-started/image006.jpg)

Другой вариант — toochange hello параметры с помощью YaST и hello **загрузчик** > **параметры ядра** параметры:

![Вкладка параметров параметры ядра Hello в YaST загрузчика](./media/hana-get-started/image007.jpg)

### <a name="file-systems"></a>Файловые системы
Hello следующем снимке экрана показаны два файловых систем, которые были созданы на сервер приложений SAP hello виртуальной Машины на основе двух дисков вложенного хранилища Azure Стандартная hello. Файловых систем относятся к типу XFS и подключенных слишком/sapdata и /sapsoftware.

Он является не обязательным toostructure вашей файловых систем, таким образом. У вас есть другие параметры для структурирования hello дискового пространства. Hello наиболее важным аспектом является tooprevent hello корневой файловой системы нехваткой свободного места.

![Два файловых систем, созданные на сервере приложений SAP hello виртуальной Машины](./media/hana-get-started/image008.jpg)

В отношении hello виртуальной Машины базы данных SAP HANA, во время установки базы данных, при использовании SAPinst (SWPM) и hello **типичные** вариант установки, все, что был установлен для /hana и /usr/sap. расположение по умолчанию Hello резервного копирования журнала SAP HANA hello находится под /usr/sap. Опять же поскольку важные tooprevent hello корневой файловой системы из хранилища переполнения, убедитесь, что имеется достаточно свободного места в разделе /hana и /usr/sap перед установкой SAP HANA с помощью SWPM.

Описание hello макет стандартной файловой системы SAP HANA см. в разделе hello [установки сервера SAP HANA и руководство по обновлению](http://help.sap.com/saphelp_hanaplatform/helpdata/en/4c/24d332a37b4a3caad3e634f9900a45/frameset.htm).

![Дополнительные файловые системы, созданные на сервере приложений SAP hello виртуальной Машины](./media/hana-get-started/image009.jpg)

При установке SAP NetWeaver на стандартный SLES/SLES для образа из коллекции Azure 12 приложений SAP, отображается сообщение о том, что нет пространства подкачки, как показано на следующий снимок экрана приветствия. toodismiss это сообщение, можно вручную добавить в файл подкачки с помощью **дд**, **mkswap**, и **swapon**. toolearn, как это сделать, поиск «Добавление в файл подкачки вручную» в hello [hello использование модуля разделения YaST](https://www.suse.com/documentation/sles-for-sap-12/pdfdoc/sles-for-sap-12-sp1.zip) раздел hello документации SUSE.

Другой вариант — tooconfigure подкачки с помощью hello агент виртуальной Машины Linux. Дополнительные сведения см. в разделе hello [руководство пользователя агента Azure Linux](../../linux/agent-user-guide.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

![Всплывающее сообщение, предупреждающее о том, что в области буфера недостаточно места](./media/hana-get-started/image010.jpg)


### <a name="hello-etchosts-file"></a>файл Hello/etc/hosts
Прежде чем начать tooinstall SAP, убедитесь, что включены приветствия имен узлов и IP-адреса hello ВМ SAP в файл/etc/hosts hello. Развернуть все ВМ SAP hello в одной виртуальной сети Azure, а затем использовать hello внутренних IP-адресов, как показано ниже:

![Имена узлов и IP-адресов ВМ SAP hello перечислены в файле/etc/hosts hello](./media/hana-get-started/image011.jpg)

### <a name="hello-etcfstab-file"></a>Hello/etc/fstab файла

Это полезно tooadd hello **nofail** файла fstab toohello параметров. Таким образом, если что-то пойдет не так с дисками hello hello виртуальной Машины не зависания в процессе загрузки hello. Однако следует помнить, что дополнительное место на диске могут оказаться недоступными процессов может заполнить hello корневой файловой системы. Если /hana отсутствует, SAP HANA не запустится.

![Добавление файла fstab toohello параметр nofail hello](./media/hana-get-started/image000c.jpg)

## <a name="graphical-gnome-desktop-on-sles-12sles-for-sap-applications-12"></a>Графический рабочий стол GNOME в SLES 12 или SLES for SAP Applications 12
В этом разделе рассматриваются следующие вопросы hello:

* Установка hello GNOME desktop и xrdp на SLES 12/SLES 12 приложений SAP
* Запуск консоли управления SAP на основе Java с помощью Firefox в SLES 12 или SLES for SAP Applications 12.

Можно также использовать альтернативные варианты, например Xterminal или VNC (не описанные в этом руководстве).

### <a name="installing-hello-gnome-desktop-and-xrdp-on-sles-12sles-for-sap-applications-12"></a>Установка hello GNOME desktop и xrdp на SLES 12/SLES 12 приложений SAP
При наличии фон Windows, можно легко использовать графический рабочий стол непосредственно в toorun виртуальных машин Linux SAP hello Firefox, SAPinst, SAP GUI, SAP MC или HANA Studio и toohello виртуальной Машины будут подключаться hello удаленного рабочего стола (RDP) с компьютера Windows. Зависит от политики вашей компании о добавлении графические интерфейсы пользователя tooproduction и нерабочей систем под управлением Linux, может потребоваться tooinstall GNOME на сервере. desktop GNOME hello tooinstall на Azure SLES 12/SLES для виртуальной Машины 12 приложений SAP:

1. Установка hello GNOME desktop, введя следующую команду (например, в PuTTY окне) hello:

   `zypper in -t pattern gnome-basic`

2. Установка xrdp tooallow toohello подключения ВМ с помощью протокола удаленного рабочего СТОЛА:

   `zypper in xrdp`

3. Измените /etc/sysconfig/windowmanager и задайте tooGNOME диспетчера окна по умолчанию hello:

   `DEFAULT_WM="gnome"`

4. Запустите **chkconfig** toomake том, что xrdp запускается автоматически после перезагрузки:

   `chkconfig -level 3 xrdp on`

5. Если имеется проблема с hello RDP-подключение, попробуйте toorestart (из PuTTY окна, например).

   `/etc/xrdp/xrdp.sh restart`

6. Если перезапуску xrdp упоминалось в предыдущем hello что шага не работает, проверьте файл .pid:

   `check /var/run` 

   Поищите `xrdp.pid`. Если обнаружится, удалите его и повторите попытку toorestart.

### <a name="starting-sap-mc"></a>Запуск консоли управления SAP
После установки hello GNOME desktop начиная hello графический на языке Java SAP MC из Firefox во время выполнения в Azure SLES 12/SLES для виртуальной Машины 12 приложений SAP может отображаться ошибка из-за отсутствующих Java-подключаемый модуль для браузера hello.

hello toostart URL-адрес приветствия, SAP MC — `<server>:5<instance_number>13`.

Дополнительные сведения см. в разделе [hello запуск веб-консоли управления SAP](https://help.sap.com/saphelp_nwce10/helpdata/en/48/6b7c6178dc4f93e10000000a42189d/frameset.htm).

Hello следующем снимке экрана показано сообщение об ошибке hello, которое отображается при отсутствии hello Java-подключаемый модуль для браузера:

![Сообщение об ошибке, указывающее на отсутствие в браузере подключаемого модуля Java](./media/hana-get-started/image013.jpg)

Одним из способов toosolve hello проблема заключается в tooinstall hello отсутствием подключаемого модуля с помощью YaST, как показано на следующий снимок экрана приветствия:

![С помощью tooinstall YaST отсутствием подключаемого модуля](./media/hana-get-started/image014.jpg)

При вводе повторно hello URL-адрес консоли управления SAP, на экран выводится запросом вы tooactivate hello подключаемого модуля:

![Диалоговое окно с запросом на активацию подключаемого модуля](./media/hana-get-started/image015.jpg)

Также может появиться сообщение об отсутствующем файле javafx.properties. Это требование связанные toohello Oracle Java 1.8 для 7.4 графического интерфейса SAP. (См. [примечание к SAP 2059429](https://launchpad.support.sap.com/#/notes/2059424)). Hello версии Java для IBM ни пакета openjdk hello, присутствующие в SLES/SLES 12 приложений SAP включает файл необходимые javafx.properties hello. решение Hello toodownload и установить из Oracle Java SE 8.

Дополнительные сведения о подобной проблеме с openjdk openSUSE см. обсуждение hello [Leap SAPGui 7.4 Java для openSUSE 42.1](https://scn.sap.com/thread/3908306).

## <a name="manual-installation-of-sap-hana-swpm"></a>Установка SAP HANA вручную: SWPM
Hello снимки экрана в этом разделе, показывающие hello основные действия по установке SAP NetWeaver 7.5 и SAP HANA SP12, при использовании SWPM (SAPinst). В составе установки NetWeaver 7.5 SWPM также hello HANA базу данных можно установить как единственный экземпляр.

В примере со средой тестирования мы установили только один сервер приложений Advanced Business Application Programming (ABAP). Как показано на следующий снимок экрана приветствия, мы использовали hello **распределенной системы** параметр tooinstall hello ASCS и экземпляры основного приложения в одной виртуальной Машине Azure и SAP HANA как hello систему баз данных в другой виртуальной Машиной Azure.

![ASCS и экземпляры основного приложения server, установленные с помощью параметра распределенной системы hello](./media/hana-get-started/image012.jpg)

После экземпляра ASCS hello установлена на сервере приложения hello ВМ и установить слишком «зеленый» в hello (показано на следующий снимок экрана приветствия) консоли управления SAP hello /sapmnt каталога (включая каталог профиля hello SAP) требуется предоставить общий доступ ВМ сервера базы данных SAP HANA hello. Hello DB шага установки требуется доступ к сведениям toothis. Hello оптимальным способом tooprovide доступом является toouse NFS, которые могут быть настроены с помощью YaST.

![Экземпляр SAP консоли управления отображением hello ASCS следует установить на сервере приложения hello виртуальной Машины и слишком «зеленый»](./media/hana-get-started/image016.jpg)

На сервере приложения hello виртуальной Машины, hello/sapmnt directory делиться через NFS с помощью hello **rw** и **no_root_squash** параметры. Hello значения по умолчанию: **ro** и **root_squash**, что могло tooproblems при установке экземпляра базы данных hello.

![Общий доступ к каталогу /sapmnt hello через NFS с помощью параметров rw и no_root_squash hello](./media/hana-get-started/image017b.jpg)

Как показано на следующем снимке экрана приветствия, из сервера приложения hello виртуальной Машины общую папку /sapmnt hello необходимо настроить на сервере базы данных SAP HANA hello виртуальной Машины с помощью **клиент NFS** (и YaST).

![Общая папка /sapmnt Hello, настроена с помощью NFS-клиента](./media/hana-get-started/image018b.jpg)

Установка tooperform распределенных 7.5 NetWeaver (**экземпляр базы данных**), как показано в hello следующий снимок экрана, войдите в сервер базы данных SAP HANA toohello виртуальной Машины, и запустите SWPM.

![Установка экземпляра базы данных, вход в ВМ сервера базы данных SAP HANA toohello и запустив SWPM](./media/hana-get-started/image019.jpg)

После выбора **типичный** установки и hello путь toohello установочного носителя ввод DB SID, имя узла hello, номер экземпляра hello и hello DB пароль системного администратора.

![Страница приветствия SAP HANA базы данных системы администратора войдите](./media/hana-get-started/image035b.jpg)

Введите пароль hello hello DBACOCKPIT схемы:

![поле ввода пароля Hello hello DBACOCKPIT схемы](./media/hana-get-started/image036b.jpg)

Введите вопрос hello SAPABAP1 схемы пароль:

![Введите вопрос пароля схемы SAPABAP1 hello](./media/hana-get-started/image037b.jpg)

После завершения каждой задачи Зеленый флажок отображается следующий этап tooeach hello процесс установки базы данных. приветственное сообщение «выполнение из... Database Instance has completed" (Выполнение экземпляра базы данных (...) завершено).

![Окно выполнения задачи, содержащее сообщение с подтверждением](./media/hana-get-started/image023.jpg)

После успешной установки hello SAP консоли управления также должен hello DB экземпляр отображается как «зеленый» и отобразить полный список hello процессов SAP HANA (hdbindexserver, hdbcompileserver и т. д.).

![Окно консоли управления SAP со списком процессов SAP HANA](./media/hana-get-started/image024.jpg)

Hello следующем снимке экрана показаны hello части hello структура файла в каталоге /hana/shared hello, SWPM создается во время установки HANA hello. Так как нет параметр toospecify другой путь, с помощью SWPM это важно toomount дополнительное место на диске в каталоге /hana hello перед hello установки SAP HANA. Это предотвращает нехватки свободного места hello корневой файловой системы.

![создается во время установки HANA файл Hello /hana/shared каталогов](./media/hana-get-started/image025.jpg)

На этом снимке экрана показана структура файла hello hello /usr/sap каталога.

![Структура файла каталога /usr/sap Hello](./media/hana-get-started/image026.jpg)

Последний шаг Hello hello распределенных ABAP установки — экземпляр сервера основного приложения hello tooinstall:

![ABAP установки отображение основного экземпляра сервера приложений в последнем этапе hello](./media/hana-get-started/image027b.jpg)

После установки экземпляра сервера основного приложения hello и графического интерфейса SAP, использовать hello **панель DBA** tooconfirm транзакции, hello SAP HANA установки завершил правильно:

![Окно DBACockpit с подтверждением успешной установки](./media/hana-get-started/image028b.jpg)

В качестве последнего шага может требуется установка toofirst HANA Studio в ВМ сервера приложений SAP hello, а затем подключите экземпляр SAP HANA toohello, который выполняется на сервере DB hello виртуальной Машины:

![Установка SAP HANA Studio в ВМ сервера приложений SAP hello](./media/hana-get-started/image038b.jpg)

## <a name="manual-installation-of-sap-hana-hdblcm"></a>Установка SAP HANA вручную: HDBLCM
В дополнение tooinstalling SAP HANA как часть распределенной установки с помощью SWPM можно установить автономный HANA hello во-первых, с помощью HDBLCM. Затем можно установить SAP NetWeaver 7.5. снимки экрана приветствия в этом разделе показывают, как работает этот процесс.

Дополнительные сведения о hello HANA HDBLCM средство см.:

* [Выбрав hello исправьте SAP HANA HDBLCM свои задачи](https://help.sap.com/saphelp_hanaplatform/helpdata/en/68/5cff570bb745d48c0ab6d50123ca60/content.htm)
* [SAP HANA Lifecycle Management Tools (Средства управления жизненным циклом SAP Hana)](http://saphanatutorial.com/sap-hana-lifecycle-management-tools/)
* [SAP HANA Server Installation and Update Guide (Руководство по установке и обновлению сервера SAP Hana)](http://help.sap.com/hana/SAP_HANA_Server_Installation_Guide_en.pdf)

Параметр ID для hello групповой tooavoid проблем со значением по умолчанию `\<HANA SID\>adm user` (создан средством HDBLCM hello), определение новой группы с именем `sapsys` по идентификатору группы `1001` перед установкой SAP HANA через HDBLCM:

![Новая группа sapsys, определенная с использованием идентификатора группы 1001](./media/hana-get-started/image030.jpg)

При запуске HDBLCM hello первый раз появится меню простой start. Выберите элемент 1, **установки новой системы**, как показано в следующих экрана приветствия:

![Параметр «Установка новой системы» в окне запуска HDBLCM hello](./media/hana-get-started/image031.jpg)

Hello следующий снимок экрана отображаются все ранее выбранные ключевые параметры hello.

> [!IMPORTANT]
> Каталоги, которые были указаны HANA журнала и объемов данных, а также путь установки hello (/ hana/совместно в этом примере) и /usr/sap, не должно быть частью hello корневой файловой системы. Эти каталоги принадлежат toohello диски данных Azure, которые были toohello подключенных виртуальных Машин (описано в разделе hello «диск установки»). Такой подход помогает предотвратить hello корневой файловой системы нехватки места. В следующий снимок экрана приветствия, можно увидеть, что администратор системы HANA hello имеет идентификатор пользователя `1005` и является частью hello `sapsys` группы (ID `1001`), был определен перед установкой hello.

![Список всех выбранных ранее основных компонентов SAP HANA](./media/hana-get-started/image032.jpg)

Вы можете проверить hello `\<HANA SID\>adm user` (`azdadm` в следующий снимок экрана приветствия) сведения о в hello/etc/directory паролей:

![HANA \<HANA SID\>adm сведения о пользователе, перечисленные в каталог паролей hello/etc /](./media/hana-get-started/image033.jpg)

После установки с помощью HDBLCM SAP HANA, вы увидите структура файла hello в SAP HANA Studio, как показано на следующий снимок экрана приветствия. Hello SAPABAP1 схему, которая содержит все таблицы SAP NetWeaver hello, еще не доступна.

![Структура файла SAP HANA в SAP HANA Studio](./media/hana-get-started/image034.jpg)

После установки SAP HANA на его основе можно установить SAP NetWeaver. Как показано в hello следующий снимок экрана, hello была выполнена установка как распределенная Установка с помощью SWPM (как описано в предыдущем разделе hello). При установке экземпляра hello базы данных с помощью SWPM вводе hello и тех же данных с помощью HDBLCM (например, имя узла, HANA SID и номера экземпляра). Затем SWPM использует существующую установку HANA hello и добавляет дополнительные схемы.

![Распределенная установка, выполненная с помощью SWPM](./media/hana-get-started/image035b.jpg)

Hello следующем снимке экрана показан этап установки SWPM hello вводятся данные о схеме DBACOCKPIT hello:

![Когда вводится данные схемы DBACOCKPIT шага установки SWPM Hello](./media/hana-get-started/image036b.jpg)

Введите данные о схеме SAPABAP1 hello:

![Ввод данных о схеме SAPABAP1 hello](./media/hana-get-started/image037b.jpg)

После завершения установки экземпляр базы данных SWPM hello можно просмотреть схемы SAPABAP1 hello в SAP HANA Studio:

![Схема Hello SAPABAP1 в SAP HANA Studio](./media/hana-get-started/image038b.jpg)

Наконец, после завершения сервера приложений SAP hello и графического интерфейса SAP установок можно проверить экземпляр базы данных HANA hello с помощью hello **панель DBA** транзакции:

![экземпляр базы данных HANA Hello проверена с помощью hello транзакции панель администратор базы данных](./media/hana-get-started/image039b.jpg)


## <a name="sap-software-downloads"></a>Скачивания программного обеспечения SAP
Программное обеспечение можно загрузить из hello услугами SAP, как показано на следующих снимках экрана приветствия.

Скачивание NetWeaver 7.5 для Linux и HANA.

 ![Окно установки и обновления службы SAP для скачивания NetWeaver 7.5](./media/hana-get-started/image001.jpg)

Скачивание выпуска HANA SP12 Platform.

 ![Окно установки и обновления службы SAP для скачивания выпуска HANA SP12 Platform](./media/hana-get-started/image002.jpg)

