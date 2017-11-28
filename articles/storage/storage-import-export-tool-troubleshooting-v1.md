---
title: "hello aaaTroubleshooting средство импорта и экспорта Azure | Документы Microsoft"
description: "Дополнительные сведения о некоторых распространенных проблем hello видели, когда с помощью средства импорта и экспорта Azure hello и как toohandle их."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="35494-103">Устранение неполадок средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="35494-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="35494-104">Средство импорта и экспорта Microsoft Azure Hello возвращает сообщения об ошибках, если возникли проблемы.</span><span class="sxs-lookup"><span data-stu-id="35494-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="35494-105">В этом разделе приведены некоторые распространенные проблемы, с которыми могут столкнуться пользователи.</span><span class="sxs-lookup"><span data-stu-id="35494-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="35494-106">Сеанс копирования завершается ошибкой, что мне делать?</span><span class="sxs-lookup"><span data-stu-id="35494-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="35494-107">Если сеанс копирования завершается ошибкой, существует два варианта.</span><span class="sxs-lookup"><span data-stu-id="35494-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="35494-108">Если ошибка hello повторить, например, если общий сетевой ресурс hello находился в автономном режиме для короткий период и теперь является вернется в оперативный режим, можно возобновить сеанс копирования hello.</span><span class="sxs-lookup"><span data-stu-id="35494-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="35494-109">Если ошибка hello не повторить, например, если указано hello неверный исходный файл каталог в параметрах командной строки hello, требуется сеанс копирования tooabort hello.</span><span class="sxs-lookup"><span data-stu-id="35494-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="35494-110">В разделе [Подготовка жестких дисков для задания импорта](storage-import-export-tool-preparing-hard-drives-import-v1.md) приведены дополнительные сведения о возобновлении и прерывании сеансов копирования.</span><span class="sxs-lookup"><span data-stu-id="35494-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="35494-111">Не удается возобновить или прервать сеанс копирования.</span><span class="sxs-lookup"><span data-stu-id="35494-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="35494-112">Если сеанс копирования hello hello первого сеанса копирования для диска, то сообщение об ошибке hello должна выглядеть следующим образом: «hello первого сеанса копирования, нельзя возобновлять или прервана.»</span><span class="sxs-lookup"><span data-stu-id="35494-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="35494-113">В этом случае можно удалить старый файл журнала hello и повторно выполните команду hello.</span><span class="sxs-lookup"><span data-stu-id="35494-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="35494-114">Если сеанс копирования является hello не первый для диске, его можно всегда возобновлять или прервана.</span><span class="sxs-lookup"><span data-stu-id="35494-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="35494-115">Я потерял hello файла журнала, можно ли создать задание hello?</span><span class="sxs-lookup"><span data-stu-id="35494-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="35494-116">файл журнала Hello для диска содержит hello полную информацию о копировании toothis диска с данными, и он tooadd необходимые дополнительные файлы toohello диска и будет использоваться toocreate задания импорта.</span><span class="sxs-lookup"><span data-stu-id="35494-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="35494-117">В случае утери hello файла журнала будет иметь tooredo всех сеансов копирования hello hello диска.</span><span class="sxs-lookup"><span data-stu-id="35494-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="35494-118">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="35494-118">Next steps</span></span>
 
* [<span data-ttu-id="35494-119">Настройка средства импорта и экспорта azure hello</span><span class="sxs-lookup"><span data-stu-id="35494-119">Setting up hello azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="35494-120">Подготовка жестких дисков для задания импорта</span><span class="sxs-lookup"><span data-stu-id="35494-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="35494-121">Просмотр состояния задания с помощью файлов журнала копирования</span><span class="sxs-lookup"><span data-stu-id="35494-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="35494-122">Подготовка задания импорта</span><span class="sxs-lookup"><span data-stu-id="35494-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="35494-123">Подготовка задания экспорта</span><span class="sxs-lookup"><span data-stu-id="35494-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
