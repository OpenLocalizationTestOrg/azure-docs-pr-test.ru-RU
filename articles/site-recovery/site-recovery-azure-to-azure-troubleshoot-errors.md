---
title: "Устранение неполадок Site Recovery aaaAzure наличие ошибок и проблем с репликацией Azure в Azure | Документы Microsoft"
description: "Устранение неполадок и ошибок при репликации виртуальных машин Azure для аварийного восстановления"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: bca957dd0f40e6b16e68913caf522f3431c55bd2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-azure-to-azure-vm-replication-issues"></a>Устранение неполадок репликации виртуальных машин из Azure в Azure

В этой статье hello типичные проблемы в Azure Site Recovery при репликации и восстановление виртуальных машин Azure из одного региона tooanother региона и объясняется, каким образом tootroubleshoot их. Дополнительные сведения о поддерживаемых конфигурациях см. в разделе hello [матрицу поддержки для репликации виртуальных машин Azure](site-recovery-support-matrix-azure-to-azure.md).

## <a name="azure-resource-quota-issues-error-code-150097"></a>Проблемы с квотами ресурсов Azure (код ошибки 150097)
Подписки должен быть включен toocreate виртуальных машинах Azure в целевой области hello, планировать toouse в вашем регионе аварийного восстановления. Кроме того, подписки должны иметь достаточно toocreate включены квоты виртуальных машин, определенного размера. По умолчанию получает Site Recovery hello того же размера hello целевой виртуальной Машины как hello исходной виртуальной Машины. Если соответствующий размер hello не поддерживается, автоматически выбирается ближайший возможный размер hello. Если подходящий размер, поддерживающий конфигурацию исходной виртуальной машины, отсутствует, появится следующее сообщение об ошибке:

**Код ошибки** | **Возможные причины** | **Рекомендации**
--- | --- | ---
150097<br></br>**Сообщение**: не удалось включить репликацию для виртуальной машины hello VmName. | -Подпиской идентификатор не может быть включена toocreate все виртуальные машины в расположение области целевой hello.</br></br>— Идентификатор подписки не могут быть включены или не имеет достаточно квоты toocreate определенных виртуальной Машины размеров в целевом расположении hello, регион.</br></br>-Подходящий целевой размер виртуальной Машины, который соответствует hello источника число сетевых Адаптеров виртуальной Машины (2) не удается найти для подписки с Идентификатором hello в целевом расположении hello, регион.| Обратитесь к [поддержки по выставлению счетов Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable создания виртуальной Машины для hello необходимые размеры виртуальных Машин в целевом расположении hello для вашей подписки. После включения hello повторных попыток не удалось выполнить операцию.

### <a name="fix-hello-problem"></a>Решить проблему hello
Вы можете связаться [поддержки по выставлению счетов Azure](https://docs.microsoft.com/azure/azure-supportability/resource-manager-core-quotas-request) tooenable вашей подписки toocreate виртуальных машин, требуемый размер: в целевом расположении hello.

Если hello целевое расположение ограничения емкости, отключите репликацию и включить его tooa другое расположение, где подписка имеет достаточные квоты toocreate hello необходимые размеры виртуальных машин.

## <a name="trusted-root-certificates-error-code-151066"></a>Доверенные корневые сертификаты (код ошибки 151066)

Если все последние доверенных корневых сертификатов hello не присутствуют на hello виртуальной Машины, может завершиться сбоем задание «включить репликацию». Без hello сертификаты, hello проверки подлинности и авторизации службы Site Recovery ошибкой вызовы из hello виртуальной Машины. Hello появится сообщение об ошибке для задания Site Recovery «включить репликацию» hello, которые не удалось выполнить:

**Код ошибки** | **Возможная причина** | **рекомендации**;
--- | --- | ---
151066<br></br>**Сообщение**: сбой при выполнении настройки Site Recovery. | Hello требуемые доверенные корневые сертификаты, используемые для авторизации и проверки подлинности не присутствуют на компьютере hello. | -Для виртуальной Машины под управлением операционной системы Windows hello убедитесь, что этот hello доверенные корневые сертификаты присутствуют на компьютере hello. Дополнительные сведения см. в статье [Настройка доверенных корневых сертификатов и запрещенных сертификатов](https://technet.microsoft.com/library/dn265983.aspx).<br></br>-Для виртуальной Машины под управлением операционной системы Linux hello следуйте инструкциям hello для доверенных корневых сертификатов, опубликованный распространитель версии операционной системы Linux hello.

### <a name="fix-hello-problem"></a>Решить проблему hello
**Windows**

Установите последние обновления Windows все hello на hello виртуальной Машины, чтобы все hello доверенные корневые сертификаты присутствуют на компьютере hello. Если вы в отключенной среде, следуйте стандартной процедуры обновления Windows hello в вашей организации tooget hello сертификаты. Если hello необходимые сертификаты не присутствуют на ВМ hello, по соображениям безопасности ошибкой toohello hello вызовов службы Site Recovery.

Следуйте hello типичные управлению центра обновления Windows или сертификат процесс управления обновлениями в вашей организации tooget, все hello последнюю корневых сертификатов и отзыв сертификатов hello обновить список на hello виртуальных машин.

tooverify, hello проблема не будет устранена, перейдите toologin.microsoftonline.com из браузера на виртуальной машине.

**Linux**

Следуйте указаниям hello, предоставляемые Linux распространителя tooget hello последнюю доверенные корневые сертификаты и последний список отзыва сертификатов hello на hello виртуальной Машины.

Поскольку SuSE Linux использует toomaintain символических ссылок список сертификатов, выполните следующие действия.

1.  Войдите как привилегированный пользователь.

2.  Выполните следующую команду:

      ``# cd /etc/ssl/certs``

3.  toosee, если сертификат корневого ЦС hello Symantec присутствует или нет, выполните следующую команду:

      ``# ls VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

4.  Если не найден файл hello, выполните следующие команды:

      ``# wget https://www.symantec.com/content/dam/symantec/docs/other-resources/verisign-class-3-public-primary-certification-authority-g5-en.pem -O VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem``

      ``# c_rehash``

5.  Символьная ссылка с b204d74a.0 toocreate VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem "->", выполните следующую команду:

      ``# ln -s  VeriSign_Class_3_Public_Primary_Certification_Authority_G5.pem b204d74a.0``

6.  Проверьте toosee, если у hello следующие выходные данные этой команды. Если нет, то у вас toocreate символьную ссылку.

      ``# ls -l | grep Baltimore
      -rw-r--r-- 1 root root   1303 Apr  7  2016 Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 04:47 3ad48a91.0 -> Baltimore_CyberTrust_Root.pem
      lrwxrwxrwx 1 root root     29 May 30 05:01 653b494a.0 -> Baltimore_CyberTrust_Root.pem``

7. Если 653b494a.0 Символьная ссылка отсутствует, используйте это команда toocreate символьную ссылку:

      ``# ln -s Baltimore_CyberTrust_Root.pem 653b494a.0``


## <a name="outbound-connectivity-for-site-recovery-urls-or-ip-ranges-error-code-151037-or-151072"></a>Исходящие подключения для URL-адресов Site Recovery или IP-диапазонов (код ошибки 151037 или 151072)

Для восстановления сайта toowork репликации требуется toospecific исходящие подключения, URL-адреса или IP-адрес в диапазоне от hello виртуальной Машины. Если ВМ находится за брандмауэром или использует сетевой безопасности (NSG) группы правил toocontrol исходящие подключения, может появиться одно из следующих сообщений об ошибке:

**Коды ошибок** | **Возможные причины** | **рекомендации**;
--- | --- | ---
151037<br></br>**Сообщение**: не удалось выполнить tooregister виртуальная машина Azure с Site Recovery. | -Используется исходящий доступ toocontrol NSG на hello виртуальной Машины и hello необходимые IP диапазоны не входят для исходящего доступа.</br></br>-Вы используете брандмауэр стороннего средства и hello необходимые диапазоны IP-адреса URL не входят.</br>| — Если вы используете брандмауэр прокси toocontrol исходящего сетевого подключения на hello виртуальной Машины, убедитесь, что hello готовности к установке URL-адреса или диапазоны IP-адресов центра обработки данных являются входят. Дополнительные сведения см. в разделе [Исходящие подключения для URL-адресов Azure Site Recovery](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>— Если вы используете NSG правила toocontrol исходящего сетевого подключения на hello виртуальной Машины, чтобы обеспечить hello необходимых компонентов центра обработки данных, диапазоны IP-адресов входят. Дополнительные сведения см. в статье [Networking guidance for replicating Azure virtual machines](https://aka.ms/a2a-nsg-guidance) (Руководство по настройке сети для репликации виртуальных машин в Azure).
151072<br></br>**Сообщение**: сбой при выполнении настройки Site Recovery. | Соединение не может быть установленного tooSite конечных точек службы восстановления. | — Если вы используете брандмауэр прокси toocontrol исходящего сетевого подключения на hello виртуальной Машины, убедитесь, что hello готовности к установке URL-адреса или диапазоны IP-адресов центра обработки данных являются входят. Дополнительные сведения см. в разделе [Исходящие подключения для URL-адресов Azure Site Recovery](https://aka.ms/a2a-firewall-proxy-guidance).</br></br>— Если вы используете NSG правила toocontrol исходящего сетевого подключения на hello виртуальной Машины, чтобы обеспечить hello необходимых компонентов центра обработки данных, диапазоны IP-адресов входят. Дополнительные сведения см. в статье [Networking guidance for replicating Azure virtual machines](https://aka.ms/a2a-nsg-guidance) (Руководство по настройке сети для репликации виртуальных машин в Azure).

### <a name="fix-hello-problem"></a>Решить проблему hello
toowhitelist [hello требуется URL-адреса](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-urls) или hello [необходимые диапазоны IP-адресов](site-recovery-azure-to-azure-networking-guidance.md#outbound-connectivity-for-azure-site-recovery-ip-ranges), следуйте указаниям hello hello [сети документ руководства по](site-recovery-azure-to-azure-networking-guidance.md).

## <a name="disk-not-found-in-hello-machine-error-code-150039"></a>Диск не найден на компьютере hello (код ошибки 150039)

Новый диск присоединен toohello следует инициализировать виртуальной Машины.

**Код ошибки** | **Возможные причины** | **рекомендации**;
--- | --- | ---
150039<br></br>**Сообщение**: диска данных Azure (DiskName) (DiskURI) с логический номер устройства (LUN) (LUNValue) не было соответствующего диска сопоставленных tooa сообщили в виртуальной Машине с hello hello одинаковое значение LUN. | -Новый диск данных был toohello подключенных виртуальных Машин, но он не был инициализирован.</br></br>-hello диск данных внутри виртуальной Машины hello правильно не передает значение hello LUN, на какие hello диск был toohello подключенных виртуальных Машин.| Убедитесь, что диски с данными hello инициализируются, а затем повторите операцию hello.</br></br>Для Windows. [Вариант 1. Подключение и инициализация нового диска](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).</br></br>Для Linux. [Инициализация нового диска данных в Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

### <a name="fix-hello-problem"></a>Решить проблему hello
Убедитесь, что были инициализированы hello диски с данными и повторите операцию hello:

- Для Windows. [Вариант 1. Подключение и инициализация нового диска](https://docs.microsoft.com/azure/virtual-machines/windows/attach-disk-portal#option-1-attach-and-initialize-a-new-disk).
- Для Linux. [Инициализация нового диска данных в Linux](https://docs.microsoft.com/azure/virtual-machines/linux/classic/attach-disk#initialize-a-new-data-disk-in-linux).

Hello проблема будет повторяться, обратитесь в службу поддержки.


## <a name="unable-toosee-hello-azure-vm-for-selection-in-enable-replication"></a>Не удается toosee hello виртуальной Машины Azure для выбора в «Включение репликации»

Виртуальные машины Azure для выбора могут не отображаться на шаге [включения репликации](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines). Эта проблема может быть вызвано toostale Site Recovery конфигурации на виртуальной Машине Azure hello влево. на Виртуальной машине Azure в следующих случаях hello может остаться Hello устаревшей конфигурации:

- Включить репликацию hello ВМ Azure с помощью восстановления сайта и затем удаляется хранилище Site Recovery hello без явно отключение репликации на hello виртуальной Машины.
- Включить репликацию hello ВМ Azure с помощью восстановления сайта и затем удалить группу ресурсов hello, содержащую хранилище Site Recovery hello без явно отключения репликации для виртуальной Машины hello.

### <a name="fix-hello-problem"></a>Решить проблему hello

Можно использовать [удалить устаревшие сценарий конфигурации ASR](https://gallery.technet.microsoft.com/Azure-Recovery-ASR-script-3a93f412) и удалите hello устаревшей конфигурации Site Recovery на виртуальной Машине Azure hello. Вы увидите hello виртуальной Машины в [включить репликацию: шаг 2](./site-recovery-azure-to-azure.md#step-2-select-virtual-machines) после удаления hello устаревшей конфигурации.


## <a name="next-steps"></a>Дальнейшие действия
[Репликация виртуальных машин Azure](site-recovery-replicate-azure-to-azure.md)
