---
title: "hello aaaUsing средство импорта и экспорта Azure | Документы Microsoft"
description: "Узнайте, как toouse hello средство импорта и экспорта tooprepare жесткие диски для задания импорта, восстановить задание импорта или экспорта."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: f77535bb-d577-438a-bdd3-e15a82e0c543
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: f5403ad482cfefbf099dbd06bf96edf8540fe51b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-tool"></a><span data-ttu-id="a3b42-103">С помощью средства импорта и экспорта Azure hello</span><span class="sxs-lookup"><span data-stu-id="a3b42-103">Using hello Azure Import/Export Tool</span></span> 

<span data-ttu-id="a3b42-104">Hello средство импорта и экспорта Azure (WAImportExport.exe) — используется toocreate задания и управлять ими для службы импорта и экспорта Azure hello, позволяя tootransfer больших объемов данных в таблицу или из хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a3b42-104">hello Azure Import/Export Tool (WAImportExport.exe) is used toocreate and manage jobs for hello Azure Import/Export service, enabling you tootransfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="a3b42-105">Данная документация является самой последней версии hello hello средство импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="a3b42-105">This documentation is for hello most recent version of hello Azure Import/Export Tool.</span></span> <span data-ttu-id="a3b42-106">Сведения об использовании hello классической модели развертывания см. в разделе [hello с помощью средства импорта и экспорта Azure v1](storage-import-export-tool-how-to-v1.md).</span><span class="sxs-lookup"><span data-stu-id="a3b42-106">For information about using hello classic deployment model, see [Using hello Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="a3b42-107">Hello следующих статьях показано, как для:</span><span class="sxs-lookup"><span data-stu-id="a3b42-107">hello following articles show you how to:</span></span>  

- <span data-ttu-id="a3b42-108">Установка и настройка hello средство импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="a3b42-108">Install and set up hello Azure Import/Export Tool.</span></span>
- <span data-ttu-id="a3b42-109">Подготовьте жесткие диски для задания, где импорт данных из вашего tooAzure дисков хранилища больших двоичных объектов.</span><span class="sxs-lookup"><span data-stu-id="a3b42-109">Prepare your hard drives for a job where you import data from your drives tooAzure Blob Storage.</span></span>
- <span data-ttu-id="a3b42-110">Просмотрите hello состояния задания с помощью файлов журнала копирования.</span><span class="sxs-lookup"><span data-stu-id="a3b42-110">Review hello status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="a3b42-111">Исправление задания импорта.</span><span class="sxs-lookup"><span data-stu-id="a3b42-111">Repair an import job.</span></span> 
- <span data-ttu-id="a3b42-112">Исправление задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="a3b42-112">Repair an export job.</span></span> 
- <span data-ttu-id="a3b42-113">Устранение неполадок средства импорта и экспорта Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a3b42-113">Troubleshoot hello Azure Import/Export Tool.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="a3b42-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a3b42-114">Next steps</span></span>

* [<span data-ttu-id="a3b42-115">Настройка средства WAImportExport hello</span><span class="sxs-lookup"><span data-stu-id="a3b42-115">Setting up hello WAImportExport tool</span></span>](storage-import-export-tool-setup.md)
