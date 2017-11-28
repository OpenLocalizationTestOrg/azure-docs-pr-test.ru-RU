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
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="a6499-104">Запуск автоматической установки Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="a6499-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="a6499-105">Узнайте, как toorun автоматической установки v2 Azure Backup Server.</span><span class="sxs-lookup"><span data-stu-id="a6499-105">Learn how toorun an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="a6499-106">Эти действия не применяются, если выполняется установка Azure Backup Server версии 1.</span><span class="sxs-lookup"><span data-stu-id="a6499-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="a6499-107">Установка Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="a6499-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="a6499-108">На сервере hello, на котором размещен сервер резервного копирования Azure v2 создайте текстовый файл.</span><span class="sxs-lookup"><span data-stu-id="a6499-108">On hello server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="a6499-109">(Созданием hello файл в блокноте или другом текстовом редакторе.) Сохранение файла hello MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="a6499-109">(You can create hello file in Notepad or in another text editor.) Save hello file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="a6499-110">Вставьте следующий код в файле MABSSetup.ini hello hello.</span><span class="sxs-lookup"><span data-stu-id="a6499-110">Paste hello following code in hello MABSSetup.ini file.</span></span> <span data-ttu-id="a6499-111">Замените текст hello в скобках hello (\< \>) со значениями из среды.</span><span class="sxs-lookup"><span data-stu-id="a6499-111">Replace hello text inside hello brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="a6499-112">После текста Hello приведен пример:</span><span class="sxs-lookup"><span data-stu-id="a6499-112">hello following text is an example:</span></span>

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

3. <span data-ttu-id="a6499-113">Сохраните файл hello.</span><span class="sxs-lookup"><span data-stu-id="a6499-113">Save hello file.</span></span> <span data-ttu-id="a6499-114">Затем в командную строку на сервере установки hello, введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="a6499-114">Then, at an elevated command prompt on hello installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="a6499-115">Эти флаги можно использовать для установки hello:</span><span class="sxs-lookup"><span data-stu-id="a6499-115">You can use these flags for hello installation:</span></span></br><span data-ttu-id="a6499-116">
**/f** — путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="a6499-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="a6499-117">
**/l** — путь к журналу.</span><span class="sxs-lookup"><span data-stu-id="a6499-117">
**/l**: Log path</span></span></br><span data-ttu-id="a6499-118">
**/i** — путь для установки.</span><span class="sxs-lookup"><span data-stu-id="a6499-118">
**/i**: Installation path</span></span></br><span data-ttu-id="a6499-119">
**/x** — путь для удаления.</span><span class="sxs-lookup"><span data-stu-id="a6499-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="a6499-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a6499-120">Next steps</span></span>
<span data-ttu-id="a6499-121">После установки сервер резервного копирования, узнайте, как tooprepare сервере или включите защиту рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="a6499-121">After you install Backup Server, learn how tooprepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="a6499-122">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="a6499-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="a6499-123">Используйте резервное копирование сервера tooback сервер VMware</span><span class="sxs-lookup"><span data-stu-id="a6499-123">Use Backup Server tooback up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="a6499-124">Используйте резервное копирование сервера tooback копирование SQL Server</span><span class="sxs-lookup"><span data-stu-id="a6499-124">Use Backup Server tooback up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="a6499-125">Добавить tooBackup современных хранилища резервных копий сервера</span><span class="sxs-lookup"><span data-stu-id="a6499-125">Add Modern Backup Storage tooBackup Server</span></span>](backup-mabs-add-storage.md)
