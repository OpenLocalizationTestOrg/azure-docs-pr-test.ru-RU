---
title: "aaaMonitoring ВМ Linux с расширением ВМ | Документы Microsoft"
description: "Узнайте, как toouse hello производительности hello toomonitor диагностического расширения для Linux и диагностических данных виртуальной машины Linux в Azure."
services: virtual-machines-linux
author: NingKuang
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: f54a11c5-5a0e-40ff-af6c-e60bd464058b
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 12/15/2015
ms.author: Ning
ms.openlocfilehash: cf7bfebca8c0367941f7a975417f60fe2e2dab25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-linux-diagnostic-extension-toomonitor-hello-performance-and-diagnostic-data-of-a-linux-vm"></a>Используйте hello диагностического расширения для Linux toomonitor hello производительности и диагностики данных виртуальной Машины Linux

В этом документе описываются версии 2.3 hello диагностического расширения для Linux.

> [!IMPORTANT]
> Эта версия не рекомендуется к использованию, и ее публикация может быть отменена в любой момент после 30 июня 2018 г. Она была заменена версией 3.0. Дополнительные сведения см. в разделе hello [документации для версии 3.0 hello диагностического расширения для Linux](../diagnostic-extension.md).

## <a name="introduction"></a>Введение

(**Примечание**: hello диагностического расширения для Linux открытый исходный код на [GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) где hello самые последние сведения о расширения hello первой публикации. Может потребоваться toocheck hello [странице GitHub](https://github.com/Azure/azure-linux-extensions/tree/master/Diagnostic) первого.)

Hello диагностического расширения для Linux помогает hello монитор пользователя виртуальных машин Linux, которые работают на платформе Microsoft Azure. Он имеет hello следующие возможности:

* Собирает и отправляет сведения о производительности системы hello из таблицы хранилища пользователя toohello hello виртуальных Машин Linux, включая сведения о диагностике и syslog.
* Позволяет пользователям toocustomize hello данных метрик, которые будут собраны и отправлены.
* Позволяет пользователям tooupload указанного журнала файлов tooa указанного хранилища таблицы.

В текущей версии hello 2.3 hello данные включают следующее:

* все журналы Rsyslog Linux, включая системный журнал, журналы безопасности и приложений;
* Все данные системы, которые указаны на [hello решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders).
* файлы журналов, выбранные пользователем.

Этот модуль работает с классической hello и модели развертывания диспетчера ресурсов.

### <a name="current-version-of-hello-extension-and-deprecation-of-old-versions"></a>Текущая версия расширения hello и прекращении старых версий

Последняя версия расширения hello Hello — **2.3**, и **все старые версии (2.0, 2.1 и 2.2) будут устаревшими и неопубликованных концу этого года (2017 г.)**. При установке расширения диагностики Linux hello автоматического дополнительный номер версии обновления отключена настоятельно рекомендуется удалить расширение hello и переустановите его с включено обновление автоматического дополнительный номер версии. На виртуальных машинах классический (ASM) можно добиться этого, указав «2.*» в качестве hello версию при установке расширения hello с помощью Azure XPLAT-CLI или Powershell. На виртуальных машинах ARM, этого можно достичь, включая "«autoUpgradeMinorVersion»: true" в шаблон развертывания виртуальной Машины hello. Кроме того любой новой установки расширения hello должен иметь дополнительный номер версии hello автоматического обновления включен параметр.

## <a name="enable-hello-extension"></a>Включить расширение hello

Это расширение можно включить с помощью hello [портал Azure](https://portal.azure.com/#), Azure PowerShell или Azure CLI скриптов.

tooview и настроить систему hello и данные о производительности непосредственно из hello портал Azure, выполните [эти действия на hello блог Azure](https://azure.microsoft.com/en-us/blog/windows-azure-virtual-machine-monitoring-with-wad-extension/).

В этой статье основное внимание уделено tooenable и настройка hello расширения с помощью команды Azure CLI. Это позволяет tooread и представление данных hello непосредственно из таблицы хранилища hello.

Обратите внимание, что методы настройки hello, описанные здесь не будет работать для hello портал Azure. tooview и настроить hello производительности системы и данных непосредственно из hello портал Azure, необходимо включить расширение hello через портал hello.

## <a name="prerequisites"></a>Предварительные требования

* **Агент Linux для Azure 2.0.6 или более поздней версии**.

  Обратите внимание на то, что большинство образов в коллекции виртуальных машин Azure на базе Linux включает версию 2.0.6 или более позднюю. Можно запустить **WAAgent-версии** tooconfirm, какая версия установлена на hello виртуальной Машины. Если hello виртуальная машина работает под управлением версии, более ранняя, чем 2.0.6, можно выполнить [эти инструкции на сайте GitHub](https://github.com/Azure/WALinuxAgent "инструкции") tooupdate его.
* **Azure CLI**. Выполните [это руководство по установке CLI](../../../cli-install-nodejs.md) tooset hello Azure CLI среды на компьютере. После установки Azure CLI можно использовать hello **azure** команду из командной строки (Bash, терминалов или командной строки) tooaccess hello Azure CLI команды. Например:

  * Выполните команду **azure vm extension set --help** , чтобы получить более подробные справочные сведения.
  * Запустите **входа azure** toosign в tooAzure.
  * Запустите **список виртуальных машин azure** toolist все hello виртуальных машин, имеющих в Azure.
* Данные учетной записи хранилища toostore hello. Потребуется имя учетной записи хранения, который был создан ранее и хранения данных tooyour доступа ключа tooupload hello.

## <a name="use-hello-azure-cli-command-tooenable-hello-linux-diagnostic-extension"></a>Используйте hello Azure CLI команда tooenable hello диагностического расширения для Linux

### <a name="scenario-1-enable-hello-extension-with-hello-default-data-set"></a>Сценарий 1. Включить расширение hello с набором данных по умолчанию hello

В 2.3 или более поздней версии содержит данные по умолчанию hello, которые будут собираться.

* все данные Rsyslog (включая системный журнал, журналы безопасности и приложений);  
* базовый набор основных данных о системе. Обратите внимание, что hello полный набор данных, описанное на hello [решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders).
  Если требуется, чтобы tooenable дополнительные данные, выполните шаги hello в сценарии 2 и 3.

Шаг 1. Создайте файл privateconfig.JSON с hello после содержимого:

    {
        "storageAccountName" : "hello storage account tooreceive data",
        "storageAccountKey" : "hello key of hello account"
    }

Шаг 2. Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions 2.* --private-config-path PrivateConfig.json**.

### <a name="scenario-2-customize-hello-performance-monitor-metrics"></a>Сценарий 2. Настройка метрик мониторинга производительности hello

В этом разделе описывается, как toocustomize hello производительности и диагностики данных таблицы.

Шаг 1. Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1. Создайте также файл PublicConfig.json. Укажите hello требуется toocollect данных.

Для всех поддерживаемых поставщиков и переменных, ссылки hello [решений Cross платформы System Center сайта](https://scx.codeplex.com/wikipage?title=xplatproviders). Можно иметь несколько запросов и сохранять их в несколько таблиц путем добавления скрипта toohello дополнительные запросы.

По умолчанию hello Rsyslog данных собираются всегда.

    {
          "perfCfg":
          [
              {
                  "query" : "SELECT PercentAvailableMemory, AvailableMemory, UsedMemory ,PercentUsedSwap FROM SCX_MemoryStatisticalInformation",
                  "table" : "LinuxMemory"
              }
          ]
    }


Шаг 2. Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

### <a name="scenario-3-upload-your-own-log-files"></a>Сценарий 3. Передача файлов журнала

В этом разделе описывается, как toocollect и передача определенных журналах tooyour учетной записи хранилища. Требуется toospecify оба hello путь tooyour журнала файла и hello имя таблицы hello место toostore входа. Можно создать несколько файлов журналов, добавив несколько сценариев toohello записи файла или таблицы.

Шаг 1. Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1. Затем создайте другой файл с именем PublicConfig.json с hello после содержимого:

```json
{
    "fileCfg" :
    [
        {
            "file" : "/var/log/mysql.err",
            "table" : "mysqlerr"
            }
    ]
}
```

Шаг 2. Запустите `azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json`.

Обратите внимание, что этот параметр на hello расширение версии предыдущих too2.3, все журналы записываются слишком`/var/log/mysql.err` может дублироваться слишком`/var/log/syslog` (или `/var/log/messages` в зависимости от hello дистрибутив Linux) также. Если вы хотите tooavoid полученную копию ведения журнала, можно исключить ведение журнала `local6` средство входит в конфигурацию rsyslog. Зависит от hello дистрибутив Linux, но системе Ubuntu 14.04 является hello файл toomodify `/etc/rsyslog.d/50-default.conf` и может заменить строку hello `*.*;auth,authpriv.none -/var/log/syslog` слишком`*.*;auth,authpriv,local6.none -/var/log/syslog`. Эта проблема исправлена в hello последние исправления версии 2.3 (2.3.9007), поэтому если у вас есть расширение hello версии 2.3, эта проблема не должно произойти. Если по-прежнему не даже после перезапуска ВМ, свяжитесь с нами и помочь нам определить причину hello последнюю версию исправления не устанавливается автоматически.

### <a name="scenario-4-stop-hello-extension-from-collecting-any-logs"></a>Сценарий 4. Остановить расширения hello сбор никаких записей журнала

В этом разделе описывается, как в журналах расширений hello toostop сбор. Обратите внимание, что процесс агента мониторинга hello будет по-прежнему запущен и работает, даже при наличии перенастройки. Если вы хотите toostop hello полностью контролирует процесс агента, это можно сделать путем отключения расширения hello. — расширение hello Hello команды toodisable `azure vm extension set --disable <vm_name> LinuxDiagnostic Microsoft.OSTCExtensions '2.*'`.

Шаг 1. Создайте файл privateconfig.JSON с содержимым hello, которое было описано в сценарии 1. Создайте другой файл с именем PublicConfig.json с hello после содержимого:

    {
        "perfCfg" : [],
        "enableSyslog" : "false"
    }


Шаг 2. Выполните команду **azure vm extension set vm_name LinuxDiagnostic Microsoft.OSTCExtensions '2.*' --private-config-path PrivateConfig.json --public-config-path PublicConfig.json**.

## <a name="review-your-data"></a>Просмотр данных

производительность Hello и диагностические данные хранятся в таблице хранилища Azure. Просмотрите [как toouse табличного хранилища Azure из Ruby](../../../cosmos-db/table-storage-how-to-use-ruby.md) toolearn как tooaccess hello данных в хранилище hello таблицу с помощью сценариев Azure CLI.

Кроме того можно использовать следующий пользовательский Интерфейс средства tooaccess hello данных:

1. Обозреватель сервера Visual Studio. Go tooyour учетной записи хранилища. После выполнения hello ВМ около пяти минут, вы увидите hello четырех таблиц по умолчанию: «LinuxCpu», «LinuxDisk», «LinuxMemory» и «Linuxsyslog». Дважды щелкните hello таблицы имен tooview hello данных.
1. [Обозреватель хранилищ Azure](https://azurestorageexplorer.codeplex.com/ "Обозреватель хранилищ Azure").

![изображение](./media/diagnostic-extension/no1.png)

Если вы включили функцию fileCfg или perfCfg (как описано в сценарии 2 и 3), можно использовать обозреватель серверов Visual Studio и обозреватель хранилища Azure данные tooview не по умолчанию.

## <a name="known-issues"></a>Известные проблемы

* Здравствуйте, Rsyslog сведения и клиента указан файл журнала может осуществляться только путем выполнения сценария.
