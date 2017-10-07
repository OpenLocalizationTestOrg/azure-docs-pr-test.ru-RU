---
title: "Устранение неполадок шифрования диска aaaAzure | Документы Microsoft"
description: "В этой статье приведены советы по устранению неполадок в шифровании дисков Microsoft Azure для виртуальных машин IaaS под управлением Windows и Linux."
services: security
documentationcenter: na
author: deventiwari
manager: avibm
editor: yuridio
ms.assetid: ce0e23bd-07eb-43af-a56c-aa1a73bdb747
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: devtiw
ms.openlocfilehash: 2ecb8df1fb869e3bf8f3be4be4494e6485e75695
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-disk-encryption-troubleshooting-guide"></a>Руководство по устранению неполадок шифрования дисков Azure

Это руководство предназначено для ИТ-специалистов, сведения аналитикам в области безопасности и проблем, связанных с администраторов облака, организации которых шифрования диска Azure и требуется руководство tootroubleshoot-шифрование диска.

## <a name="troubleshooting-linux-os-disk-encryption"></a>Устранение неполадок шифрования диска ОС Linux

Шифрование диска операционной системы Linux необходимо отключить toorunning предыдущего диска hello ОС через процесс шифрование всего диска hello.   Если это невозможно, сообщение об ошибке «Ошибка toounmount после...» сообщение об ошибке: вероятно, toooccur.

Это наиболее вероятно при попытке шифрования диска ОС в целевой среде виртуальной машины, чей готовый образ из коллекции был изменен.  Примеры отклонения от hello поддерживается изображения, которое может мешать hello расширение возможности toounmount hello ОС диска.
- Настраиваемые образы, которые больше не соответствуют поддерживаемой файловой системе или схеме секционирования.
- Настроенных образов с приложений, таких как антивирусная программа, Docker, SAP, MongoDB или Cassandra Apache, работающих в предыдущих tooencryption hello ОС.  Эти приложения является сложным tooterminate, и они сохраняют диск toohello ОС дескрипторов открытых файлов, hello диск не может быть отключены, которая привела к отказу.
- Пользовательские скрипты, выполняемые в закройте время шага шифрования toohello близости может повлиять и вызывает эту ошибку. Это может произойти, когда шаблона диспетчера ресурсов одновременно задает несколько расширений tooexecute или расширение пользовательского скрипта или другое действие выполняется одновременно toodisk шифрования.   Hello проблему может решить сериализации и изоляции такого действия.
- Если SELinux не было отключено предыдущих tooenabling шифрования, hello отключите шаг завершается ошибкой.  SELinux можно будет снова включить после завершения шифрования.
- Если диск hello ОС использует схему LVM (несмотря на то, что доступна ограниченная поддержка диск данных LVM, диска ОС LVM не)
- Если минимальные требования к памяти не выполняются (для шифрования диска операционной системы рекомендуется 7 ГБ памяти).
- Когда диски данных рекурсивно подключены в каталоге /mnt/ или любом другом (например, /mnt/data1, /mnt/data2, /data3 + /data3/data4 и т. д.).
- Если другие [предварительные требования](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption) к шифрованию дисков Azure для ОС Linux не выполнены.

## <a name="unable-tooencrypt"></a>Не удается tooencrypt

В некоторых случаях шифрование диска Linux hello появляется toobe застрявшее в «Шифрование диска операционной системы к работе» и SSH отключена. Этот процесс может занять от toocomplete 3-16 часов на стандартных коллекции образов.  При добавлении дисков данных несколькими ТБ размер hello может занять дни. Hello последовательности шифрования диска операционной системы Linux временное отключение диска ОС hello и выполняет шифрование поблочно hello всего диска операционной системы, прежде чем снова подключать его в зашифрованный состоянии.   В отличие от шифрования диска Azure в Windows шифрование диска Linux запрещается совместное использование виртуальных Машин hello hello шифрования во время выполнения.  характеристики производительности Hello hello виртуальной Машины, включая размер hello диска hello и ли учетная запись хранения hello поддерживаемый стандартного или расширенного хранилище (SSD), значительно может влиять на шифрование toocomplete время, необходимое для hello.

состояние toocheck hello ProgressMessage поля, возвращаемые hello [Get AzureRmVmDiskEncryptionStatus](https://docs.microsoft.com/powershell/module/azurerm.compute/get-azurermvmdiskencryptionstatus) команда может быть запрошено.   Хотя шифруется диск с ОС hello, hello виртуальная машина переходит в состояние обслуживания и SSH также является отключено tooprevent toohello непрерывный процесс любые прерывания в работе.  EncryptionInProgress будет отмечено для hello большую часть времени hello шифрования во время выполнения, следует несколько часов в более поздней версии VMRestartPending сообщение с предложением toorestart hello виртуальной Машины.  Например:


```
PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : EncryptionInProgress
DataVolumesEncrypted       : EncryptionInProgress
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk encryption started

PS > Get-AzureRmVMDiskEncryptionStatus -ResourceGroupName $resourceGroupName -VMName $vmName
OsVolumeEncrypted          : VMRestartPending
DataVolumesEncrypted       : Encrypted
OsVolumeEncryptionSettings : Microsoft.Azure.Management.Compute.Models.DiskEncryptionSettings
ProgressMessage            : OS disk successfully encrypted, please reboot hello VM
```

Один раз на запрос tooreboot hello виртуальной Машины и после перезапуска виртуальной Машины hello и предоставляя 2-3 минуты для hello перезагрузка и выполнена на целевом сервере hello toobe заключительные действия, hello сообщение о состоянии сообщит, что наконец завершено, шифрование.   Это сообщение доступно, hello шифрования диска операционной системы после ожидаемого toobe готова для использования, а также для hello ВМ toobe можно использовать снова.

В случаях, где эта последовательность не найдена или если отчет сбой шифрования ОС в середине hello данного процесса (например, если отображается ошибка «сбой toounmount» hello, описанные в этом руководстве), сведения о загрузке сообщение о ходе выполнения и другие показатели ошибок Рекомендуется моментального снимка обратной toohello toorestore hello ВМ или резервная копия немедленно предыдущих tooencryption.  Предыдущий toohello при следующей попытке, это предлагаемое toore-оценить характеристики hello hello виртуальной Машины и убедитесь, что выполнены все необходимые компоненты.

## <a name="troubleshooting-azure-disk-encryption-behind-a-firewall"></a>Устранение неполадок шифрования диска Azure в связи с брандмауэром
Когда подключение ограничен брандмауэра, требования прокси-сервера или группы (NSG) безопасность сети, hello возможность расширения tooperform hello необходимые задачи может оказаться невозможным.   Это может привести к состояние сообщения, такие как «Состояние расширения доступно не для виртуальной Машины hello» и в планируемых сценариях сбоя toofinish.  Hello разделах имеет некоторые распространенные проблемы брандмауэра, которые может изучить.

### <a name="network-security-groups"></a>Группы безопасности сети
Применения параметров группы безопасности сети по-прежнему необходимо разрешить hello конечной точки toomeet hello задокументированы сетевая конфигурация [необходимые компоненты](https://docs.microsoft.com/azure/security/azure-security-disk-encryption#prerequisites) для шифрования диска.

### <a name="azure-keyvault-behind-firewall"></a>Azure Key Vault под защитой брандмауэра
Hello виртуальной Машины должно быть возможности tooaccess хранилища ключей. Ссылки tooguidance при сбое tookey доступ через брандмауэр, который обслуживается hello [хранилище ключей](https://docs.microsoft.com/azure/key-vault/key-vault-access-behind-firewall) команды.

### <a name="linux-package-management-behind-firewall"></a>Управление пакетами Linux из-за брандмауэра
Во время выполнения шифрование диска Azure для Linux использует hello целевой рассылки пакета управления система tooinstall необходимые необходимых компонентов предыдущих tooenabling шифрования.  Если параметры брандмауэра препятствует возможности toodownload hello ВМ и установить эти компоненты, последующие ошибки ожидаются.    tooconfigure действия Hello, это зависит от распространителя.  В Red Hat, когда требуется прокси-сервер, необходимо обеспечить правильную настройку диспетчера подписок и yum.  Дополнительные сведения о поддержке Red Hat см. в [этой статье](https://access.redhat.com/solutions/189533).  

## <a name="troubleshooting-windows-server-2016-server-core"></a>Устранение неполадок в основных серверных компонентах Windows Server 2016

В Windows Server 2016 Server Core hello bdehdcfg компонент недоступен по умолчанию. Этот компонент требуется для шифрования дисков Azure.

tooworkaround этой проблемы, hello копирования следующие 4 файлы из папки c:\windows\system32 toohello ВМ Windows Server 2016 данных центра изображения hello Server Core:

```
bdehdcfg.exe
bdehdcfglib.dll
bdehdcfglib.dll.mui
bdehdcfg.exe.mui
```

Затем выполните следующую команду hello:

```
bdehdcfg.exe -target default
```

Это создаст системный раздел 550 МБ, а затем после перезагрузки, можно использовать Diskpart toocheck hello тома и продолжить.  

Например:

```
DISKPART> list vol

  Volume ###  Ltr  Label        Fs     Type        Size     Status     Info
  ----------  ---  -----------  -----  ----------  -------  ---------  --------
  Volume 0     C                NTFS   Partition    126 GB  Healthy    Boot
  Volume 1                      NTFS   Partition    550 MB  Healthy    System
  Volume 2     D   Temporary S  NTFS   Partition     13 GB  Healthy    Pagefile
```
## <a name="see-also"></a>См. также
В этом документе вы узнали, Дополнительные сведения о некоторых распространенных проблем при шифровании диска Azure и как tootroubleshoot. Дополнительные сведения об этой службе и ее возможностях см. в статьях:

- [Шифрование диска в центре безопасности Azure](https://docs.microsoft.com/azure/security-center/security-center-apply-disk-encryption)
- [Шифрование виртуальной машины Azure](https://docs.microsoft.com/azure/security-center/security-center-disk-encryption)
- [Шифрование неактивных данных в Azure](https://docs.microsoft.com/azure/security/azure-security-encryption-atrest)
