---
title: "aaaInstall SAP HANA на HANA SAP в Azure (большие экземпляры) | Документы Microsoft"
description: "Как tooinstall SAP HANA на SAP HANA в Azure (большие экземпляр)."
services: virtual-machines-linux
documentationcenter: 
author: hermanndms
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 12/01/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: b2fe242270a1166cabcfae2f9249a8dd70ff3b93
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinstall-and-configure-sap-hana-large-instances-on-azure"></a>Как tooinstall и настройте SAP HANA (крупных экземпляров) в Azure

Ниже приведены некоторые важные определения tooknow перед прочтением этого руководства. В статье [Обзор и описание архитектуры SAP HANA в Azure (крупные экземпляры)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture) мы представили два разных класса единиц крупных экземпляров HANA с:

- S72, S72m, S144, S144m, S192 и S192m, который мы называем tooas hello «Тип я класса» номеров SKU.
- S384, S384m, S384xm, S576, S768 и S960, который мы называем tooas Здравствуйте, «Type II класс» номеров SKU.

спецификатор класса Hello является постоянной toobe оканчивающимися hello большом экземпляре HANA tooeventually документации ссылаться toodifferent возможностей и требований в зависимости от HANA большого экземпляра SKU.

Кроме того, часто используются следующие определения.
- **Большой экземпляр отметки:** стека инфраструктуры оборудования, SAP HANA TDI сертифицированные и выделенного toorun экземпляров SAP HANA в Azure.
- **SAP HANA в Azure (большие экземпляры):** официальное название для предложения hello в экземплярах Azure toorun HANA в на оборудовании, которое развертывается в большом экземпляре отметки в разных регионах Azure certified TDI HANA SAP. Hello связанных терминов **HANA большом экземпляре** — сокращение для SAP HANA в Azure (большие экземпляры), которая широко использовать это руководство по развертыванию, технические.


Hello установки SAP HANA самостоятельно и запуске действие hello после получения нового SAP HANA на сервере Azure (большие экземпляры). И после установления подключения hello вашей Azure VNet(s) и hello единиц большом экземпляре HANA получен. 

> [!Note]
> Согласно политике SAP hello установки SAP HANA должна быть выполнена пользователем сертифицированные установок SAP HANA tooperform человека. Человек, который прошел hello Сертифицировано SAP связать технологии экзаменов, экзамену установки SAP HANA, или Сертифицировано SAP системные интеграторы (SI).

Проверьте еще раз, особенно при планировании tooinstall HANA 2.0 [&#2235581; Примечание поддержки SAP - SAP HANA: поддерживаемые операционные системы](https://launchpad.support.sap.com/#/notes/2235581/E) в порядке toomake убедиться, что hello, поддерживаемые ОС с hello SAP HANA выпуске вы решили tooinstall. Выясняется, что hello, поддерживаемая операционная система для HANA 2.0 имеет больше ограничений, чем hello 1.0 HANA поддерживаемые ОС. 

## <a name="first-steps-after-receiving-hello-hana-large-instance-units"></a>Первые шаги после получения hello больших единиц экземпляр HANA

**Первый шаг** после получения hello HANA большом экземпляре и установленных экземпляров toohello доступа и подключения к, — tooregister hello ОС hello экземпляра с помощью поставщика операционной системы. Этот шаг включает регистрации ОС SUSE Linux в экземпляре SMT SUSE нужны toohave развернуты на виртуальной машине в Azure. Hello большом экземпляре HANA единицы можно подключить экземпляр SMT toothis (см. Далее в этой документации). Или для вашей операционной системы RedHat toobe зарегистрирована Red Hat подписки Manager необходимо tooconnect для hello. Примечания см. в этом [документе](https://docs.microsoft.com/azure/virtual-machines/linux/sap-hana-overview-architecture?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). Этот шаг также является hello может toopatch необходимые toobe ОС. Задача, которая находится в hello обязанностью клиента hello. Поиск документации tooinstall SUSE и настройте SMT [здесь](https://www.suse.com/documentation/sles-12/book_smt/data/smt_installation.html).

**Второй шаг** — toocheck для новых обновлений и исправлений hello конкретного выпуска или версии ОС. Проверьте, является ли уровень исправления hello hello большом экземпляре HANA на hello последнее состояние. На основании времени исправления или выпуски и изменения toohello образа ОС, можно развернуть Microsoft, возможны случаи, когда последние исправления hello не могут быть включены. Поэтому после перевода через единое большом экземпляре HANA toocheck ли исправления, относятся только к безопасности, функциональные возможности, доступности и производительности были выпущены в то же время по поставщикам Linux hello и требуется применить toobe это обязательный шаг.

**Третий шаг** — toocheck out hello SAP предпринятые действия по установке и настройке SAP HANA на hello конкретной версии или версии ОС. Из-за toochanging tooSAP рекомендации или изменения заметки или конфигураций, которые зависят от установки отдельных сценариев, корпорация Майкрософт не всегда будет может toohave единое большом экземпляре HANA полностью настроена. Таким образом является обязательным для вас как клиента, tooread hello примечания по SAP связанные tooSAP HANA на точное выпуска Linux. Конфигурации hello hello операционной системы и версии необходимо проверить и применение параметров конфигурации hello там, где это еще не сделано.

В конкретной hello проверьте следующие параметры и в итоге скорректировать, чтобы:

- net.core.rmem_max = 16777216;
- net.core.wmem_max = 16777216;
- net.core.rmem_default = 16777216;
- net.core.wmem_default = 16777216;
- net.core.optmem_max = 16777216;
- net.ipv4.tcp_rmem = 65536 16777216 16777216;
- net.ipv4.tcp_wmem = 65536 16777216 16777216.

Начиная с SLES12 SP1 и RHEL 7.2, эти параметры задаются в файле конфигурации в каталоге /etc/sysctl.d hello. Например необходимо создать файл конфигурации с именем hello 91-NetApp-HANA.conf. В предыдущих выпусках SLES и RHEL эти параметры необходимо задать в файле /etc/sysctl.conf.

Для всех RHEL выпусков и начиная с SLES12 hello 
- sunrpc.tcp_slot_table_entries = 128

необходимо задать в файле /etc/modprobe.d/sunrpc-local.conf. Если hello файл не существует, он сначала должны быть созданы путем добавления hello следующая запись: 
- options sunrpc tcp_max_slot_table_entries=128.

**Четвертый шаг** — toocheck hello системное время модульного HANA большого экземпляра. экземпляры Hello развертываются вместе в системе часовым поясом представляют Привет расположение hello регион Azure hello больших штамп экземпляра HANA, расположенный в. Вы являетесь свободного toochange hello системного времени или часового пояса hello экземпляров, которыми вы владеете. Это и упорядочение дополнительные экземпляры в клиенте, подготовлены необходимые tooadapt hello часовой пояс hello вновь доставлено экземпляров. Microsoft операции имеют не анализировать hello в системе часовым поясом, которые настроены с экземплярами hello после hello передача в эксплуатацию. Таким образом развернутой экземпляров может не быть настроена в hello же часовой пояс, как изменять для hello. В результате вашей обязанностью является как toocheck клиента и при необходимости адаптировать hello часовой пояс передают экземпляры hello. 

**Пятый шаг** toocheck и т. д/узлы. Как получить переданные колонках hello, они имеют разные IP-адреса, назначенные для разных целей (см. следующий раздел). Проверьте файл hello и узлы, и т. д. В случаях, когда единицы добавляются в существующий клиент не нужна и т. д toohave и узлы hello вновь развертывания систем правильной поддержки с IP-адресами hello ранее доставленный систем. Таким образом это на вас как клиента toocheck hello правильные параметры таким образом, что развернутый экземпляр могут взаимодействовать и разрешения имен hello ранее развернутой единиц в клиенте. 

## <a name="networking"></a>Сеть
Предполагается, что выполнены рекомендации hello в проектировании виртуальных сетей в Azure и подключения этих toohello виртуальных сетей HANA больших экземпляров, как описано в следующих документах:

- [Обзор и описание архитектуры SAP HANA в Azure (крупные экземпляры)](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture)
- [Инфраструктура и возможности подключения SAP HANA в Azure (крупные экземпляры)](hana-overview-infrastructure-connectivity.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Существуют некоторые сведения о стоит toomention о сетевых подключениях hello hello один единиц. Каждой единицы большом экземпляре HANA поставляется с двумя или тремя IP-адресов, назначенных tootwo или три Сетевых портов hello единицы. Три IP-адреса используются в конфигурациях с масштабным развертыванием HANA и сценарий hello HANA системы репликации. Один из IP-адресов hello назначенный Сетевых единицы hello выходит за пределы пула IP-адрес сервера, описанную в hello hello toohello [SAP HANA (большом экземпляре) Обзор и архитектура в Azure](https://docs.microsoft.com/azure/virtual-machines/workloads/sap/hana-overview-architecture).

для единиц с двумя IP-адресами, которые назначены распределения Hello должен выглядеть так:

- eth0.xx должен иметь IP-адрес, выходящее за диапазон адресов пула IP-адресов сервера, что вы отправили tooMicrosoft hello. Этот IP-адрес должен использоваться для обслуживания в/etc/hosts из hello ОС.
- eth1.xx должен иметь IP-адрес, используемый для связи tooNFS. Таким образом, эти адреса выполните **не** требуется toobe сохраняется и т. д/узлов в порядке tooallow экземпляр tooinstance трафика в рамках клиента hello.

При развертывании репликации системы HANA или масштабировании HANA конфигурация колонки с двумя назначенными IP-адресами не подходит. Если наличие двух IP-адресов, назначенных только и Желательное toodeploy такую конфигурацию, обратитесь к SAP HANA на tooget управления службами Azure третий IP-адресов в третью назначен виртуальной локальной сети. Для больших экземпляр HANA единиц с трех IP-адресов, назначенных для трех Сетевых портов hello использования применяются следующие правила.

- eth0.xx должен иметь IP-адрес, выходящее за диапазон адресов пула IP-адресов сервера, что вы отправили tooMicrosoft hello. Поэтому этот IP-адрес не должны использоваться для обслуживания в/etc/hosts из hello ОС.
- eth1.xx должен иметь IP-адрес, используемый для хранения tooNFS связи. Этот тип адресов не нужно указывать в файле etc/hosts.
- eth2.xx должно быть исключительно используемым toobe сохраняется и т. д/узлов для связи между различными экземплярами hello. Эти адреса также будут hello IP-адресов, требующих toobe изменяются в конфигурациях с масштабным развертыванием HANA IP-адресов, используемых HANA для конфигурации hello между узлами.



## <a name="storage"></a>Хранилище

Hello структуры хранения для SAP HANA в Azure (большие экземпляры) настраивается с SAP HANA на управления службами Azure через SAP рекомендуется направляющие линии, как описано в документе [требования к хранилищу SAP HANA](http://go.sap.com/documents/2015/03/74cdb554-5a7c-0010-82c7-eda71af511fa.html) Технический документ. Здравствуйте примерным размеры разных томах hello с hello различных конфигураций экземпляров больших HANA получен описаны в [SAP HANA (большом экземпляре) Обзор и архитектура в Azure](hana-overview-architecture.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

соглашения об именовании Hello hello томов хранилища, указаны в hello в следующей таблице.

| Использование хранилища | Имя подключения | Имя тома | 
| --- | --- | ---|
| Данные HANA | /hana/data/SID/mnt0000<m> | IP хранилища: /hana_data_SID_mnt00001_tenant_vol |
| Журнал HANA | /hana/log/SID/mnt0000<m> | IP хранилища: /hana_log_SID_mnt00001_tenant_vol |
| Резервная копия журнала HANA | /hana/log/backups | IP хранилища: /hana_log_backups_SID_mnt00001_tenant_vol |
| Общий HANA | /hana/shared/SID | IP хранилища: /hana_shared_SID_mnt00001_tenant_vol/shared |
| usr/sap | /usr/sap/SID | IP хранилища: /hana_shared_SID_mnt00001_tenant_vol/usr_sap |

Где SID = hello HANA экземпляр системный идентификатор 

А клиент — это внутреннее перечисление операций при развертывании клиента.

Как видите, общий HANA и usr/sap совместно используют hello одинаковый объем. Спецификация Hello объекта точки подключения hello включают hello системный идентификатор hello HANA экземпляров, а также номер подключения hello. В масштабируемых развертываниях существует только одно подключение, например mnt00001. В масштабируемом развертывании будет отображаться столько подключений, сколько рабочих и главных узлов находится в вашем распоряжении. Hello масштабирования среды, данные журнала журнала резервного копирования томов, общих и вложенных tooeach узел в конфигурации масштабного hello. Для конфигураций с несколькими экземплярами SAP другом наборе томов — единица созданы и вложенных toohello ХАНЬ большом экземпляре.

Прочитайте документ hello и найдите единое HANA большом экземпляре, учтите, что единицы hello входят в состав довольно щедро тома данных HANA или и что у нас есть HANA журналов и резервного копирования или тома. Hello причины, почему мы размера hello HANA или данных настолько большими, — что моментальные снимки хранилища hello, предлагаемых для клиентов, выполняющих использовании hello том же диске. Это означает hello Дополнительные хранилища моментальных снимков, которые можно выполнить, приветствия моментальными снимками в тома хранилища, назначенные потребляется больше места. Hello HANA журналов и резервного копирования или том — не размышления toobe hello том tooput резервные копии баз данных в. Это по размеру toobe используется в качестве резервного копирования тома для резервных копий журналов транзакций HANA hello. В будущих версиях hello хранилища моментальных снимков self службы, мы будет использовать этот конкретный том toohave более частые моментальные снимки. И с, более частая репликациями toohello аварийного восстановления, при желании в toooption для hello инфраструктуры большом экземпляре HANA hello функции аварийного восстановления. Дополнительные сведения см. в статье [Высокий уровень доступности и аварийное восстановление SAP HANA в Azure (крупные экземпляры)](hana-overview-high-availability-disaster-recovery.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). 

Кроме предоставлен toohello хранилища, вы можете приобрести дополнительную емкость с шагом 1 ТБ. Это дополнительное хранилище можно добавить как новый тома tooa HANA крупных экземпляров.

Во время адаптации с SAP HANA на управление службой Azure hello клиент указывает идентификатор пользователя (UID) и идентификатор группы (GID) для группы пользователей и sapsys sidadm hello (например: 1000,500) бывает, что во время установки hello системы SAP HANA, используются эти значения. Необходимо toodeploy нескольких экземпляров HANA на единицу, можно получить несколько наборов томов (один набор для каждого экземпляра). В результате во время развертывания необходимо toodefine:

- Здравствуйте, SID hello различных HANA экземпляров (sidadm является производным от него).
- Объемы памяти различных экземпляров HANA hello. Поскольку размер памяти hello на экземпляры определяет размер hello hello томов в каждом наборе отдельный том.

Согласно рекомендациям поставщика хранилища, hello следующие параметры подключения, настроенных для всех подключенных томов (Кроме загрузки LUN):

- nfs    rw, vers=4, hard, timeo=600, rsize=1048576, wsize=1048576, intr, noatime, lock 0 0

Эти подключения, точек, настроенных в/etc/fstab, как показано в hello следующие графики:

![fstab подключенных томов в единице крупного экземпляра HANA](./media/hana-installation/image1_fstab.PNG)

выходные данные команды hello df -h на устройстве S72m HANA большом экземпляре Hello выглядит следующим образом:

![fstab подключенных томов в единице крупного экземпляра HANA](./media/hana-installation/image2_df_output.PNG)


контроллер хранилища Hello и узлов в большом экземпляре отметки hello — tooNTP синхронизированных серверов. С вас синхронизация hello SAP HANA единиц Azure (большие экземпляры) и виртуальных машинах Azure с NTP-сервером должен быть не происходит смещение значительное время инфраструктуры hello и единицы hello вычислений в Azure или большой экземпляр отметок.

В порядке toooptimize используются под хранения toohello SAP HANA также необходимо задать следующие параметры конфигурации SAP HANA hello:

- max_parallel_io_requests 128;
- async_read_submit on;
- async_write_submit_active on;
- async_write_submit_blocks all.
 
Для версии SAP HANA 1.0 копирование tooSPS12, эти параметры могут быть установлены во время установки hello hello базы данных SAP HANA, как описано в [&#2267798; Примечание SAP - конфигурацию hello база данных SAP HANA](https://launchpad.support.sap.com/#/notes/2267798)

Также можно настроить параметры hello после установки базы данных SAP HANA hello с помощью платформы hdbparam hello. 

С 2.0 SAP HANA hello hdbparam framework рекомендуется к использованию. В результате hello необходимо настроить параметры с помощью команд SQL. Дополнительные сведения см. в [примечании к SAP 2399079 об устранении hdbparam в HANA 2.0](https://launchpad.support.sap.com/#/notes/2399079).


## <a name="operating-system"></a>операционная система

Подкачки из hello доставки образа операционной системы имеет значение too2 ГБ, в соответствии с toohello [&#1999997; Примечание поддержки SAP - часто задаваемые вопросы: памяти SAP HANA](https://launchpad.support.sap.com/#/notes/1999997/E). Любой другой параметр требуемой требуется toobe набор вами клиентом.

[SUSE Linux Enterprise Server 12 SP1 для приложений SAP](https://www.suse.com/products/sles-for-sap/hana) — hello дистрибутив Linux, которые установлены для SAP HANA в Azure (большие экземпляры). Это частичным распределением предоставляет возможности конкретного SAP &quot;стандартной hello&quot; (включая заданные параметры для эффективного выполнения SAP на SLES).

В разделе [ресурсов библиотеки и технические документы](https://www.suse.com/products/sles-for-sap/resource-library#white-papers) на веб-сайте SUSE hello и [SAP в SUSE](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE) на hello сети сообщества SAP (SCN) некоторые полезные ресурсы, связанные с toodeploying SAP HANA на SLES (включая hello установки высокий уровень доступности, операции определенного tooSAP усиление безопасности, и многое другое).

Дополнительные сведения и полезные ссылки по SAP в SUSE:

- [SAP HANA на сайте SUSE Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+SUSE);
- [Best Practice for SAP: Enqueue Replication – SAP NetWeaver on SUSE Linux Enterprise 12](https://www.suse.com/docrepcontent/container.jsp?containerId=9113) (Рекомендации по SAP. Постановка репликации в очередь — SAP NetWeaver в SUSE Linux Enterprise 12).
- [ClamSAP – SLES Virus Protection for SAP](http://scn.sap.com/community/linux/blog/2014/04/14/clamsap--suse-linux-enterprise-server-integrates-virus-protection-for-sap) (ClamSAP – защита от вирусов на сервере SLES для SAP) (включая SLES 12 для приложений SAP).

SAP примечания о поддержке применимо tooimplementing SAP HANA на SLES 12:

- [SAP Support Note #1944799 – SAP HANA Guidelines for SLES Operating System Installation](http://go.sap.com/documents/2016/05/e8705aae-717c-0010-82c7-eda71af511fa.html) (Примечание по поддержке SAP №1944799. Рекомендации по установке SAP HANA в ОС SLES).
- [SAP Support Note #2205917 – SAP HANA DB Recommended OS Settings for SLES 12 for SAP Applications](https://launchpad.support.sap.com/#/notes/2205917/E) (Примечание по поддержке SAP №2205917. База данных SAP HANA: рекомендуемые параметры ОС для SLES 12 для приложений SAP).
- [SAP Support Note #1984787 – SUSE Linux Enterprise Server 12: Installation Notes](https://launchpad.support.sap.com/#/notes/1984787) (Примечание по поддержке SAP №1984787. Заметки об установке SUSE Linux Enterprise Server 12).
- [SAP Support Note #171356 – SAP Software on Linux: General Information](https://launchpad.support.sap.com/#/notes/1984787) (Примечание по поддержке SAP №171356. Общие сведения о ПО SAP на платформе Linux).
- [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Примечание по поддержке SAP №1391070. Решения UUID для Linux).

[Red Hat Enterprise Linux для SAP HANA](https://www.redhat.com/en/resources/red-hat-enterprise-linux-sap-hana) — еще одно решение для запуска SAP HANA на крупных экземплярах HANA. Доступны выпуски RHEL 6.7 и 7.2. 

Дополнительные сведения и полезные ссылки по SAP в Red Hat:
- [Сайт SAP HANA в Red Hat Linux](https://wiki.scn.sap.com/wiki/display/ATopics/SAP+on+Red+Hat).

SAP примечания о поддержке применимо tooimplementing SAP HANA в Red Hat:

- [SAP Support Note #2009879 - SAP HANA Guidelines for Red Hat Enterprise Linux (RHEL) Operating System](https://launchpad.support.sap.com/#/notes/2009879/E) (Примечание по поддержке SAP №2009879. Рекомендации по установке SAP HANA в ОС Red Hat Enterprise Linux (RHEL)).
- [SAP Support Note #2292690 - SAP HANA DB: Recommended OS settings for RHEL 7](https://launchpad.support.sap.com/#/notes/2292690) (Примечание по поддержке SAP №2292690. База данных SAP HANA: рекомендуемые параметры операционной системы для RHEL 7).
- [SAP Support Note #2247020 - SAP HANA DB: Recommended OS settings for RHEL 6.7](https://launchpad.support.sap.com/#/notes/2247020) (Примечание по поддержке SAP №2247020. База данных SAP HANA: рекомендуемые параметры операционной системы для RHEL 6.7).
- [SAP Support Note #1391070 – Linux UUID Solutions](https://launchpad.support.sap.com/#/notes/1391070) (Примечание по поддержке SAP №1391070. Решения UUID для Linux).
- [SAP Support Note #2228351 - Linux: SAP HANA Database SPS 11 revision 110 (or higher) on RHEL 6 or SLES 11](https://launchpad.support.sap.com/#/notes/2228351) (Примечание по поддержке SAP №2228351. Linux: база данных SAP HANA SPS 11, редакция 110 (или более поздняя), в RHEL 6 или SLES 11).
- [SAP Support Note #2397039 - FAQ: SAP on RHEL](https://launchpad.support.sap.com/#/notes/2397039) (Примечание по поддержке SAP №2397039. Часто задаваемые вопросы: SAP в RHEL).
- [SAP Support Note #1496410 - Red Hat Enterprise Linux 6.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/1496410) (Примечание по поддержке SAP №1496410. Установка и обновление Red Hat Enterprise Linux 6.x).
- [SAP Support Note #2002167 - Red Hat Enterprise Linux 7.x: Installation and Upgrade](https://launchpad.support.sap.com/#/notes/2002167) (Примечание по поддержке SAP №2002167. Установка и обновление Red Hat Enterprise Linux 7.x).

## <a name="time-synchronization"></a>Синхронизация времени

Приложения SAP, построенные на hello архитектура SAP NetWeaver вводятся с учетом на разницу во времени для hello различные компоненты, которые составляют hello системы SAP. Дампы коротких ABAP SAP с название ошибки hello ZDATE\_БОЛЬШОЙ\_время\_DIFF, скорее всего, знакомые так, как эти короткие дампы при hello системное время на разных серверах или виртуальных машин drifting слишком далеко друг от друга.

SAP HANA в Azure (большие экземпляры) в Azure &#39; во время синхронизации t применяются единицы toohello вычислений в большом экземпляре отметки hello. Эта синхронизация не относится к приложениям SAP, выполняемым на виртуальных машинах Azure, так как Azure гарантирует правильную синхронизацию системного времени. В результате отдельных времена, когда необходимо настроить сервер может использоваться с серверов приложений SAP, работающих на виртуальных машинах Azure и hello SAP HANA базы данных экземпляров, выполняющихся на HANA крупных экземпляров. Hello инфраструктуры хранения данных в большом экземпляре отметки — время синхронизации с NTP-серверы.

## <a name="setting-up-smt-server-for-suse-linux"></a>Настройка сервера SMT для SUSE Linux
SAP HANA крупных экземпляров нет toohello прямого подключения к Интернету. Поэтому она не простой процесс tooregister единицы с поставщиком ОС hello и toodownload и применении исправлений. В случае hello SUSE Linux одним из решений может быть tooset SMT сервера на виртуальной Машине Azure. В то время как hello виртуальной Машине Azure требуется toobe размещаются в виртуальную сеть Azure, являющийся подключенных toohello HANA большом экземпляре. Такого сервера SMT единицы hello HANA большом экземпляре может зарегистрировать и загрузить исправления. 

SUSE предлагает более объемное руководство по [средству управления подписками для SLES 12 SP2](https://www.suse.com/documentation/sles-12/pdfdoc/book_smt/book_smt.pdf). 

Как предварительное условие для установки hello SMT сервера, который выполняет задачу hello для большого экземпляра HANA потребуются.

- Виртуальная сеть Azure, подключенной toohello HANA больших ER экземпляра канала.
- учетная запись SUSE, связанная с организацией. В то время как hello организации необходимо toohave некоторые действительная подписка SUSE.

### <a name="installation-of-smt-server-on-azure-vm"></a>Установка сервера SMT на виртуальной машине Azure

На этом шаге вы устанавливаете сервер SMT hello на виртуальной Машине Azure. toolog в toohello является первая мера Hello [центр SUSE клиентов](https://scc.suse.com/)

Как вы вошли, перейти tooOrganization--> учетных данных организации. В этом разделе вы должны найти hello учетные данные, необходимые tooset hello SMT сервера.

Третий шаг Hello — tooinstall SUSE Linux виртуальной Машины в виртуальной сети Azure hello. hello toodeploy ВМ, принимают SLES 12 SP2 образ ВМ из Azure. В процессе развертывания hello DNS-имя не был определен и не используйте статические IP-адреса, как показано в этом снимке экрана

![развертывание виртуальной машины для сервера SMT](./media/hana-installation/image3_vm_deployment.png)

Hello развернутой виртуальной Машины было меньшего размера виртуальной Машины и получил hello внутренний IP-адрес в виртуальной сети Azure из 10.34.1.4 hello. Имя виртуальной Машины hello было smtserver. После установки hello hello подключения toohello HANA больших единиц экземпляр был установлен. Зависит от того, как организована разрешение имен может потребоваться разрешение tooconfigure HANA большом экземпляре единиц hello и т. д/узлы hello виртуальной Машине Azure. Добавьте дополнительный диск toohello виртуальной Машине, которая будет toobe используемых toohold hello исправлений. загрузочный диск Hello сам может оказаться слишком маленьким. В случае hello показано hello диска есть подключенного слишком/srv/www/htdocs как показано на следующий снимок экрана приветствия. 100 ГБ дискового пространства должно быть достаточно.

![развертывание виртуальной машины для сервера SMT](./media/hana-installation/image4_additional_disk_on_smtserver.PNG)

Войдите в большом экземпляре HANA toohello единицу (единицы), Ведение/etc/hosts и проверьте, можно ли достичь hello виртуальной Машине Azure, который должен toorun hello SMT сервера по сети hello.

После завершения этой проверки необходимо toolog в toohello ВМ Azure, следует запустить сервер SMT hello. При использовании putty toolog toohello ВМ необходимые tooexecute этой последовательности команд в окне bash.

```
cd ~
echo "export NCURSES_NO_UTF8_ACS=1" >> .bashrc
```

После выполнения этих команд перезапустите параметры hello tooactivate bash. Затем запустите YAST.

В YAST перейдите tooSoftware обслуживания и выполните поиск smt. Выберите smt, который автоматически переключается tooyast2 smt, как показано ниже

![SMT в yast](./media/hana-installation/image5_smt_in_yast.PNG)


Примите Выбор hello для установки на hello smtserver. После установки перейдите toohello SMT сервера конфигурации и ввести учетные данные организации hello hello центр SUSE клиентов, извлеченного ранее. Введите имя узла на виртуальной Машине Azure также в качестве URL-адрес сервера SMT hello. В этой демонстрации было https://smtserver, отображаемый в графике Далее hello.

![Конфигурация сервера SMT](./media/hana-installation/image6_configuration_of_smtserver1.png)

Следующий шаг должен иметь tootest ли работает центр hello подключения toohello SUSE клиентов. Как видно из hello следующие графики в случае демонстрации hello, она работала.

![Тест подключения центр tooSUSE пользователей](./media/hana-installation/image7_test_connect.png)

Один раз запускается программа установки SMT hello, необходимо tooprovide пароль базы данных. Так как это новая установка, toodefine необходимо пароля, как показано в следующем графике hello.

![Определение пароля для базы данных](./media/hana-installation/image8_define_db_passwd.PNG)

сертификат создается при Hello следующего диалога вами. Проходить через диалоговое окно приветствия, как показано далее, и шаг hello следует продолжить.

![Создание сертификата для сервера SMT](./media/hana-installation/image9_certificate_creation.PNG)

Может существовать несколько минут, затраченное на шаге «Проверка выполнения синхронизации» hello в конце hello hello конфигурации. После установки hello и конфигурацию сервера SMT hello, следует найти hello каталога репозитория в разделе подключения hello точке /srv/www/htdocs/плюс некоторые вложенные каталоги в репозитории. 

Перезапустите сервер SMT hello и его связанные службы, с помощью следующих команд.

```
rcsmt restart
systemctl restart smt.service
systemctl restart apache2
```

### <a name="download-of-packages-onto-smt-server"></a>Загрузка пакетов на сервер SMT

После того как все hello перезапуска служб, выберите hello соответствующие пакеты управления SMT с помощью Yast. Выбор пакета Hello зависит от образа ОС hello hello HANA большом экземпляре сервера, а не на приветствия SLES выпуска или версии hello ВМ hello SMT серверу. Ниже показан пример hello выделенной области экрана.

![Выбор пакетов](./media/hana-installation/image10_select_packages.PNG)

После завершения работы с hello Выбор пакета, необходимо toostart hello исходную копию hello Выбор пакетов toohello SMT сервера, который настраивается. Эта копия запускается в оболочке hello, с помощью hello команда smt зеркальные показанной ниже


![Загрузка пакетов tooSMT сервера](./media/hana-installation/image11_download_packages.PNG)

Как показано выше, пакеты hello следует получить копируется hello каталоги, созданные в разделе подключения hello точке /srv/www/htdocs. Этот процесс может занять несколько минут. Зависит от выбора количество пакетов, может занять час tooone или более.
При завершении этого процесса, требуется установка toomove toohello SMT клиента. 

### <a name="set-up-hello-smt-client-on-hana-large-instance-units"></a>Настройка клиента SMT hello на устройствах, HANA большом экземпляре

на данном Hello в данном случае — hello большом экземпляре HANA единицы. программу установки server SMT Hello копируется clientSetup4SMT.sh сценария hello hello виртуальной Машине Azure. Скопируйте этот скрипт toohello HANA большом экземпляре единицу tooconnect tooyour SMT сервера. Запустить сценарий hello hello -h и присвойте ему имени параметра hello SMT сервера. В этом примере используется smtserver.

![Настройка клиента SMT](./media/hana-installation/image12_configure_client.PNG)

Возможны сценарии, где hello загрузка hello сертификата с сервера hello клиентом hello выполнена успешно, но не удалось выполнить регистрацию hello, как показано ниже.

![Ошибка регистрации клиента](./media/hana-installation/image13_registration_failed.PNG)

Если не удалось выполнить регистрацию hello, прочтите это [SUSE поддерживает документ](https://www.suse.com/de-de/support/kb/doc/?id=7006024) и выполнения hello действия, описанные существует.

> [!IMPORTANT] 
> Имя сервера должен иметь имя tooprovide hello hello виртуальной Машины, в этот регистр smtserver без hello полное доменное имя. Просто hello works имя виртуальной Машины. 

После выполнения этих шагов необходимо hello tooexecute следующую команду на большом экземпляре HANA единице hello

```
SUSEConnect –cleanup
```

> [!Note] 
> В наших тестов мы всегда было toowait через несколько минут после выполнения этого шага. Hello clientSetup4SMT.sh немедленного выполнения после hello меры по исправлению описано в статье SUSE hello завершено с hello сертификата является недопустимым, пока в сообщениях. После 5–10-минутного ожидания выполнение clientSetup4SMT.sh завершалось успешной конфигурацией клиента.

В случае hello проблема, которая требуется toofix согласно шагам hello hello SUSE статьи, понадобятся clientSetup4SMT.sh toorestart на большом экземпляре HANA единице hello. Теперь процесс должен завершиться успешно, как показано ниже.

![Регистрация клиента успешно выполнена](./media/hana-installation/image14_finish_client_config.PNG)

На этом шаге вы настроили клиента SMT hello tooconnect единицы hello HANA большом экземпляре на сервере SMT hello, установленных на виртуальной Машине Azure hello. Теперь можно воспользоваться «zypper вверх» или «zypper в» tooinstall ОС исправления tooHANA крупных экземпляров или установить дополнительные пакеты. Понятно, что только можно получить список обновлений, которые был загружен до на сервере SMT hello.


## <a name="example-of-an-sap-hana-installation-on-hana-large-instances"></a>Пример установки SAP HANA на крупных экземплярах HANA
В этом разделе показано, как tooinstall SAP HANA на устройстве HANA большом экземпляре. Начальное состояние Hello, которая у нас есть выглядеть так:

- Предоставленный Майкрософт все toodeploy hello данных вы большого экземпляра SAP HANA.
- Hello большого экземпляра SAP HANA полученные от корпорации Майкрософт.
- Вы создали виртуальной сети Azure, подключенной tooyour в локальной сети.
- Подключение канала ExpressRotue hello для крупных экземпляров HANA toohello одной виртуальной сети Azure.
- Вы установили виртуальную машину Azure, которая будет использоваться в качестве места перехода для крупных экземпляров HANA.
- Внесенные в том, что можно подключаться из единица tooyour HANA большом экземпляре перехода hello и наоборот.
- Установлен ли все hello необходимые пакеты и обновления установлены.
- Прочитать заметки SAP hello и документацию о HANA установки на hello ОС используется и убедитесь, что hello HANA по выбору поддерживается в выпуске hello ОС.

Элементы, отображаемые в следующей последовательности hello загружается hello перехода toohello поля виртуальной Машины, в данном случае под управлением ОС Windows hello копия hello пакеты toohello HANA большом экземпляре устройства и последовательность установки hello hello hello HANA установки пакетов.

### <a name="download-of-hello-sap-hana-installation-bits"></a>Время ожидания загрузки bits установки hello SAP HANA
Так как единицы большом экземпляре HANA hello нет прямой связи с toohello Интернета, не удается загрузить непосредственно hello установочные пакеты из toohello SAP HANA большая экземпляра ВМ. tooovercome hello отсутствует прямое подключение к Интернету, необходимо hello перехода поле. Вы загрузите hello пакеты toohello перехода поле виртуальной Машины.

В порядке toodownload hello HANA установочные пакеты необходимо S-пользователь SAP или другого пользователя, который позволяет вам tooaccess hello SAP Marketplace. После входа выполните следующую последовательность действий:

Go слишком[услугами SAP](https://support.sap.com/en/index.html) > нажмите кнопку загрузить программное обеспечение > установки и обновления > по алфавитный указатель > под H — выпуск платформы SAP HANA > SAP HANA платформа версии 2.0 > Установки > hello загрузки следующие файлы

![Загрузка установочных пакетов HANA](./media/hana-installation/image16_download_hana.PNG)

В случае демонстрации hello мы загрузили установочные пакеты SAP HANA 2.0. В окне Azure перехода hello виртуальной Машины разверните hello архивов в каталог hello, как показано ниже.

![Извлечение установочных пакетов HANA](./media/hana-installation/image17_extract_hana.PNG)

Как hello архивы будут извлечены, скопируйте каталог hello, созданный путем извлечения hello, в случае hello выше 51052030 toohello HANA больших единиц измерения экземпляра на том /hana/shared hello в каталог, созданный.

> [!Important]
> Не копировать пакеты установки hello в корневой hello и загрузки LUN, так как пространство ограничено и должен использоваться другими процессами, а также toobe.


### <a name="install-sap-hana-on-hello-hana-large-instance-unit"></a>Установите на единицы hello большом экземпляре HANA SAP HANA
В порядке tooinstall SAP HANA необходим toolog в пользователя root. Только корень имеет достаточно разрешений tooinstall SAP HANA.
Первое Hello необходимо toodo — tooset разрешения для каталога hello, скопированной в/hana/Общие. Hello разрешения должны tooset как

```
chmod –R 744 <Installation bits folder>
```

Если вы хотите tooinstall SAP HANA с использованием графического hello программой установки, hello gtk2 пакет потребностями toobe установлен на больших экземплярах HANA hello. Проверьте, установлено ли оно, с помощью команды hello

```
rpm –qa | grep gtk2
```

В шагах мы демонстрации установки SAP HANA hello hello графический пользовательский интерфейс. В качестве следующего шага перейдите в каталог установки hello и перейдите в каталог sub hello HDB_LCM_LINUX_X86_64. Начало

```
./hdblcmgui 
```
из этого каталога. Теперь начало выполняются последовательности экранов которых tooprovide hello данных требуется для установки hello. В случае hello показано мы установке сервера базы данных SAP HANA hello и клиентские компоненты SAP HANA hello. Поэтому мы выбираем пункт "База данных SAP HANA", как показано ниже.

![Выбор HANA в ходе установки](./media/hana-installation/image18_hana_selection.PNG)

В следующем экране приветствия варианта hello «Установить систему»

![Выбор новой установки HANA](./media/hana-installation/image19_select_new.PNG)

После выполнения этого шага необходимо tooselect между несколько дополнительных компонентов, которые можно дополнительно установить сервер базы данных SAP HANA toohello.

![Выбор дополнительных компонентов HANA](./media/hana-installation/image20_select_components.PNG)

Для целей hello этой документации мы выбранным hello SAP HANA клиента и hello SAP HANA Studio. Мы также установили вертикально масштабируемый экземпляр. Поэтому в следующий экран приветствия, необходим toochoose «Система одного узла» 

![Выбор вертикально масштабируемой установки](./media/hana-installation/image21_single_host.PNG)

В следующем экране hello необходим tooprovide некоторые данные

![Указание идентификатора SID SAP HANA](./media/hana-installation/image22_provide_sid.PNG)

> [!Important]
> Как идентификатор системы HANA (SID), необходимо tooprovide hello ИД безопасности, как при заказе развертывания больших экземпляров HANA hello, предоставляемых Microsoft. Выбор другой идентификатор безопасности делает hello установки ошибкой из-за проблемы с разрешениями tooaccess на разных томах hello

Как каталог установки используется каталог /hana/shared hello. В следующем шаге hello необходимо tooprovide hello расположения для файлов данных HANA hello и файлы журналов HANA hello


![Указание расположения журнала HANA](./media/hana-installation/image23_provide_log.PNG)

> [!Note]
> Следует определить как файлы данных и журналов hello тома, которые уже входит в комплект hello точек подключения, которые содержат SID, выбранное на выбор экрана приветствия перед этот экран приветствия. Если несоответствие hello SID с hello один ввода, экрана приветствия ранее, вернуться и изменить значение SID toohello вами на точках подключения hello hello.

В следующем шаге hello просмотрите имя узла hello и в конечном счете исправить ее. 

![Проверка имени узла](./media/hana-installation/image24_review_host_name.PNG)

В следующем шаге hello необходимо также tooretrieve данных Вы дали tooMicrosoft при заказе развертывания больших экземпляров HANA hello. 

![Указание ИД пользователя и ИД группы](./media/hana-installation/image25_provide_guid.PNG)

> [!Important]
> Требуется tooprovide hello же системный идентификатор пользователя и идентификатор группы пользователей, оговоренных Microsoft как порядок hello единицу развертывания. Если не очень toogive hello одинаковые коды hello установки SAP HANA на большом экземпляре HANA единицы hello завершается ошибкой.

В следующих двух экраны hello, которые не показаны в этой документации, требуется пароль hello tooprovide для пользователя базы данных SAP HANA hello и hello пароль для пользователя sapadm hello, используемой для hello агента узла SAP, которое устанавливается как часть системы hello экземпляр базы данных SAP HANA Hello.

После определения пароль hello, экран подтверждения присутствует. Проверьте все данные hello в списке и продолжить установку hello. Откроется экран хода выполнения, который документы hello ход выполнения установки, как hello один ниже

![Проверка хода выполнения установки](./media/hana-installation/image27_show_progress.PNG)

При завершении установки hello, следует изображение как одном hello

![Установка завершена](./media/hana-installation/image28_install_finished.PNG)

На этом этапе hello SAP HANA экземпляр должен находиться запущен и работает и готов для использования. Должно быть tooit может tooconnect из среды Studio SAP HANA. Также убедитесь в том, проверьте hello последние обновления системы SAP HANA и применении этих исправлений.
























































 







 




