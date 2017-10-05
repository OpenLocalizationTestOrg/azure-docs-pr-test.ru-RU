---
title: "Использование инструмента импорта и экспорта Azure | Документация Майкрософт"
description: "Узнайте, как использовать инструмент импорта и экспорта для подготовки жестких дисков для задания импорта, восстановления задания импорта или восстановления задания экспорта."
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
ms.openlocfilehash: 20a720833842f9579fd4fccaa39e964def48197e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool"></a><span data-ttu-id="5260f-103">Использование средства импорта и экспорта Azure</span><span class="sxs-lookup"><span data-stu-id="5260f-103">Using the Azure Import/Export Tool</span></span> 

<span data-ttu-id="5260f-104">Инструмент импорта и экспорта Azure (WAImportExport.exe) используется для создания заданий службы импорта и экспорта Azure и управления ими, что позволяет передавать большие объемы данных в хранилище BLOB-объектов Azure или из него.</span><span class="sxs-lookup"><span data-stu-id="5260f-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="5260f-105">Данный документ предназначен для самой последней версии средства импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="5260f-105">This documentation is for the most recent version of the Azure Import/Export Tool.</span></span> <span data-ttu-id="5260f-106">Сведения об использовании классической модели развертывания см. в статье [Using the Azure Import/Export Tool (classic deployment model)](storage-import-export-tool-how-to-v1.md) (Использование средства импорта и экспорта Azure (классическая модель развертывания)).</span><span class="sxs-lookup"><span data-stu-id="5260f-106">For information about using the classic deployment model, see [Using the Azure Import/Export Tool v1](storage-import-export-tool-how-to-v1.md).</span></span>

<span data-ttu-id="5260f-107">Из статей в этом разделе вы узнаете, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="5260f-107">The following articles show you how to:</span></span>  

- <span data-ttu-id="5260f-108">Установка и настройка средства импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="5260f-108">Install and set up the Azure Import/Export Tool.</span></span>
- <span data-ttu-id="5260f-109">Подготовка жестких дисков для задания, импортирующего данные с дисков в хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="5260f-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="5260f-110">Просмотр состояния задания с помощью файлов журнала копирования.</span><span class="sxs-lookup"><span data-stu-id="5260f-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="5260f-111">Исправление задания импорта.</span><span class="sxs-lookup"><span data-stu-id="5260f-111">Repair an import job.</span></span> 
- <span data-ttu-id="5260f-112">Исправление задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="5260f-112">Repair an export job.</span></span> 
- <span data-ttu-id="5260f-113">Устранение неполадок средства импорта и экспорта Azure.</span><span class="sxs-lookup"><span data-stu-id="5260f-113">Troubleshoot the Azure Import/Export Tool.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="5260f-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5260f-114">Next steps</span></span>

* <span data-ttu-id="5260f-115">[Using the Azure Import/Export Tool](storage-import-export-tool-setup.md) (Использование средства импорта и экспорта Azure)</span><span class="sxs-lookup"><span data-stu-id="5260f-115">[Setting up the WAImportExport tool](storage-import-export-tool-setup.md)</span></span>