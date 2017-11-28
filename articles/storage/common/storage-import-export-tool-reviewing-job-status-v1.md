---
title: "Просмотр состояния задания инструмента импорта и экспорта Azure версии 1 | Документация Майкрософт"
description: "Узнайте, как использовать файлы журнала, созданные при запуске задания импорта или экспорта, для просмотра состояния задания импорта и экспорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: bdb30bc28c36ab9e969efc8be3b87b97e4027b39
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="af34c-103">Просмотр состояния задания импорта и экспорта Azure с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="af34c-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="af34c-104">При обработке дисков, связанных с заданием импорта или экспорта, служба импорта и экспорта Microsoft Azure записывает файлы журнала копирования в учетную запись хранения, в которую импортируются большие двоичные объекты или из которой они экспортируются.</span><span class="sxs-lookup"><span data-stu-id="af34c-104">When the Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files to the storage account to or from which you are importing or exporting blobs.</span></span> <span data-ttu-id="af34c-105">Файл журнала содержит подробные сведения о состоянии каждого импортируемого или экспортируемого файла.</span><span class="sxs-lookup"><span data-stu-id="af34c-105">The log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="af34c-106">При запросе состояния завершенного задания возвращается URL-адрес для каждого файла журнала копирования. Дополнительные сведения см. [здесь](/rest/api/storageservices/Get-Job3).</span><span class="sxs-lookup"><span data-stu-id="af34c-106">The URL to each copy log file is returned when you query the status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="af34c-107">Примеры URL-адресов</span><span class="sxs-lookup"><span data-stu-id="af34c-107">Example URLs</span></span>

<span data-ttu-id="af34c-108">Ниже приведены примеры URL-адресов файлов журнала копирования для задания импорта с двумя дисками.</span><span class="sxs-lookup"><span data-stu-id="af34c-108">The following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="af34c-109">Дополнительные сведения о формате журналов копирования и полный список кодов состояний см. в статье [Формат файла журнала службы импорта и экспорта Azure](../storage-import-export-file-format-log.md).</span><span class="sxs-lookup"><span data-stu-id="af34c-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for the format of copy logs and the full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="af34c-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="af34c-110">Next steps</span></span>
 
 * [<span data-ttu-id="af34c-111">Настройка средства импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="af34c-111">Setting Up the Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="af34c-112">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="af34c-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="af34c-113">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="af34c-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="af34c-114">Подготовка задания экспорта</span><span class="sxs-lookup"><span data-stu-id="af34c-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="af34c-115">Устранение неполадок со средством импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="af34c-115">Troubleshooting the Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
