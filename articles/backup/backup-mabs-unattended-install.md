---
title: "aaaSilent установки сервер резервного копирования Azure v2 | Документы Microsoft"
description: "Использование сценария PowerShell toosilently установки v2 Azure Backup Server. Этот тип установки также называется \"тихой\" установкой."
services: backup
documentationcenter: " "
author: markgalioto
manager: carmonm
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/30/2017
ms.author: markgal;masaran
ms.openlocfilehash: 6b94b4a278bfcd5f8c5c363cb811bd8eec984243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a>Запуск автоматической установки Azure Backup Server версии 2

Узнайте, как toorun автоматической установки v2 Azure Backup Server. 

Эти действия не применяются, если выполняется установка Azure Backup Server версии 1.

## <a name="install-backup-server-v2"></a>Установка Backup Server версии 2

1. На сервере hello, на котором размещен сервер резервного копирования Azure v2 создайте текстовый файл. (Созданием hello файл в блокноте или другом текстовом редакторе.) Сохранение файла hello MABSSetup.ini. 

2. Вставьте следующий код в файле MABSSetup.ini hello hello. Замените текст hello в скобках hello (\< \>) со значениями из среды. После текста Hello приведен пример:

  ```
  [OPTIONS]
  UserName=administrator
  CompanyName=<Microsoft Corporation>
  SQLMachineName=localhost
  SQLInstanceName=<SQL instance name>
  SQLMachineUserName=administrator
  SQLMachinePassword=<admin password>
  SQLMachineDomainName=<machine domain>
  ReportingMachineName=localhost
  ReportingInstanceName=<reporting instance name>
  SqlAccountPassword=<admin password>
  ReportingMachineUserName=<username>
  ReportingMachinePassword=<reporting admin password>
  ReportingMachineDomainName=<domain>
  VaultCredentialFilePath=<vault credential full path and complete name>
  SecurityPassphrase=<passphrase>
  PassphraseSaveLocation=<passphrase save location>
  UseExistingSQL=<1/0 use or do not use existing SQL>
  ```

3. Сохраните файл hello. Затем в командную строку на сервере установки hello, введите следующую команду:

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

Эти флаги можно использовать для установки hello:</br>
**/f** — путь к файлу.</br>
**/l** — путь к журналу.</br>
**/i** — путь для установки.</br>
**/x** — путь для удаления.</br>

## <a name="next-steps"></a>Дальнейшие действия
После установки сервер резервного копирования, узнайте, как tooprepare сервере или включите защиту рабочей нагрузки.

- [Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server](backup-azure-microsoft-azure-backup.md)
- [Используйте резервное копирование сервера tooback сервер VMware](backup-azure-backup-server-vmware.md)
- [Используйте резервное копирование сервера tooback копирование SQL Server](backup-azure-sql-mabs.md)
- [Добавить tooBackup современных хранилища резервных копий сервера](backup-mabs-add-storage.md)
