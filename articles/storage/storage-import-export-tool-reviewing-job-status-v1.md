---
title: "состояние задания импорта и экспорта Azure - v1 aaaReviewing | Документы Microsoft"
description: "Узнайте, как файлы журналов hello toouse, созданные при hello импорта или экспорта задания был запущен toosee hello состояние задания импорта и экспорта hello."
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
ms.openlocfilehash: 378bc9a7ef6bfe65209413c8c4134f313a2c0d79
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="4a621-103">Просмотр состояния задания импорта и экспорта Azure с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="4a621-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="4a621-104">Когда hello службы импорта и экспорта Microsoft Azure обрабатывает диски, связанные с заданием импорта или экспорта, она записывает учетной записи копии журнала файлов toohello хранения tooor откуда Импорт или экспорт больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="4a621-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="4a621-105">Hello файл журнала содержит подробное состояние каждого файла, который был импортирован или экспортирован.</span><span class="sxs-lookup"><span data-stu-id="4a621-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="4a621-106">файл журнала копирования tooeach URL-адрес Hello возвращается при запросе hello состояние завершенного задания; в разделе [получения задания](/rest/api/storageservices/Get-Job3) для получения дополнительной информации.</span><span class="sxs-lookup"><span data-stu-id="4a621-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="4a621-107">Примеры URL-адресов</span><span class="sxs-lookup"><span data-stu-id="4a621-107">Example URLs</span></span>

<span data-ttu-id="4a621-108">Hello ниже приведены примеры URL-адресов для копирования файлов журнала для задания импорта с двумя дисками.</span><span class="sxs-lookup"><span data-stu-id="4a621-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="4a621-109">В разделе [службы импорта и экспорта формат файла журнала](storage-import-export-file-format-log.md) hello формата журналов копирования и полный список кодов состояния hello.</span><span class="sxs-lookup"><span data-stu-id="4a621-109">See [Import/Export service Log File Format](storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="4a621-110">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="4a621-110">Next steps</span></span>
 
 * [<span data-ttu-id="4a621-111">Установка hello средство импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="4a621-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="4a621-112">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="4a621-112">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="4a621-113">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="4a621-113">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="4a621-114">Подготовка задания экспорта</span><span class="sxs-lookup"><span data-stu-id="4a621-114">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="4a621-115">Устранение неполадок средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="4a621-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
