---
title: "Автоматическая установка Azure Backup Server версии 2 | Документация Майкрософт"
description: "Использование скрипта PowerShell для автоматической установки Azure Backup Server версии 2. Этот тип установки также называется \"тихой\" установкой."
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
ms.openlocfilehash: 91778a67f9ef523aa87b7918197e0d0ded0f5702
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="run-an-unattended-installation-of-azure-backup-server-v2"></a><span data-ttu-id="247d7-104">Запуск автоматической установки Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="247d7-104">Run an unattended installation of Azure Backup Server v2</span></span>

<span data-ttu-id="247d7-105">Узнайте, как запустить автоматическую установку Azure Backup Server версии 2.</span><span class="sxs-lookup"><span data-stu-id="247d7-105">Learn how to run an unattended installation of Azure Backup Server v2.</span></span> 

<span data-ttu-id="247d7-106">Эти действия не применяются, если выполняется установка Azure Backup Server версии 1.</span><span class="sxs-lookup"><span data-stu-id="247d7-106">These steps do not apply if you are installing Azure Backup Server v1.</span></span>

## <a name="install-backup-server-v2"></a><span data-ttu-id="247d7-107">Установка Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="247d7-107">Install Backup Server v2</span></span>

1. <span data-ttu-id="247d7-108">Создайте текстовый файл на сервере, на котором размещен Azure Backup Server версии 2.</span><span class="sxs-lookup"><span data-stu-id="247d7-108">On the server that hosts Azure Backup Server v2, create a text file.</span></span> <span data-ttu-id="247d7-109">(Файл можно создать в блокноте или в другом текстовом редакторе.) Сохраните файл как MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="247d7-109">(You can create the file in Notepad or in another text editor.) Save the file as MABSSetup.ini.</span></span> 

2. <span data-ttu-id="247d7-110">Вставьте следующий код в файл MABSSetup.ini.</span><span class="sxs-lookup"><span data-stu-id="247d7-110">Paste the following code in the MABSSetup.ini file.</span></span> <span data-ttu-id="247d7-111">Замените текст в скобках (\< \>) значениями из среды.</span><span class="sxs-lookup"><span data-stu-id="247d7-111">Replace the text inside the brackets (\< \>) with values from your environment.</span></span> <span data-ttu-id="247d7-112">Ниже приведен пример текста.</span><span class="sxs-lookup"><span data-stu-id="247d7-112">The following text is an example:</span></span>

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

3. <span data-ttu-id="247d7-113">Сохраните файл.</span><span class="sxs-lookup"><span data-stu-id="247d7-113">Save the file.</span></span> <span data-ttu-id="247d7-114">Затем в командной строке с повышенными привилегиями на сервере установки введите следующую команду:</span><span class="sxs-lookup"><span data-stu-id="247d7-114">Then, at an elevated command prompt on the installation server, enter this command:</span></span>

  ```
  start /wait <cdlayout path>/Setup.exe /i  /f <.ini file path>/setup.ini /L <log path>/setup.log
  ```

<span data-ttu-id="247d7-115">Для установки можно использовать следующие флаги:</span><span class="sxs-lookup"><span data-stu-id="247d7-115">You can use these flags for the installation:</span></span></br><span data-ttu-id="247d7-116">
**/f** — путь к файлу.</span><span class="sxs-lookup"><span data-stu-id="247d7-116">
**/f**: .ini file path</span></span></br><span data-ttu-id="247d7-117">
**/l** — путь к журналу.</span><span class="sxs-lookup"><span data-stu-id="247d7-117">
**/l**: Log path</span></span></br><span data-ttu-id="247d7-118">
**/i** — путь для установки.</span><span class="sxs-lookup"><span data-stu-id="247d7-118">
**/i**: Installation path</span></span></br><span data-ttu-id="247d7-119">
**/x** — путь для удаления.</span><span class="sxs-lookup"><span data-stu-id="247d7-119">
**/x**: Uninstall path</span></span></br>

## <a name="next-steps"></a><span data-ttu-id="247d7-120">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="247d7-120">Next steps</span></span>
<span data-ttu-id="247d7-121">После установки Backup Server узнайте, как подготовить сервер или обеспечить защиту рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="247d7-121">After you install Backup Server, learn how to prepare your server, or begin protecting a workload.</span></span>

- [<span data-ttu-id="247d7-122">Подготовка к резервному копированию рабочих нагрузок с использованием Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="247d7-122">Prepare Backup Server workloads</span></span>](backup-azure-microsoft-azure-backup.md)
- [<span data-ttu-id="247d7-123">Резервное копирование сервера VMware в Azure</span><span class="sxs-lookup"><span data-stu-id="247d7-123">Use Backup Server to back up a VMware server</span></span>](backup-azure-backup-server-vmware.md)
- [<span data-ttu-id="247d7-124">Архивация баз данных SQL Server в Azure с помощью Azure Backup Server</span><span class="sxs-lookup"><span data-stu-id="247d7-124">Use Backup Server to back up SQL Server</span></span>](backup-azure-sql-mabs.md)
- [<span data-ttu-id="247d7-125">Добавление хранилища на Azure Backup Server версии 2</span><span class="sxs-lookup"><span data-stu-id="247d7-125">Add Modern Backup Storage to Backup Server</span></span>](backup-mabs-add-storage.md)
