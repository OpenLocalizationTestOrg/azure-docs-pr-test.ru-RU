---
title: "Использование инструмента импорта и экспорта Azure версии 1 | Документация Майкрософт"
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
ms.date: 1/15/2017
ms.author: muralikk
ms.openlocfilehash: 4ce2273cc0dcc456c2edc8c5dd2fc22496f20380
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="using-the-azure-importexport-tool-classic-deployment-model"></a><span data-ttu-id="ac08b-103">Использование средства импорта и экспорта Azure (классическая модель развертывания)</span><span class="sxs-lookup"><span data-stu-id="ac08b-103">Using the Azure Import/Export Tool (classic deployment model)</span></span>

<span data-ttu-id="ac08b-104">Инструмент импорта и экспорта Azure (WAImportExport.exe) используется для создания заданий службы импорта и экспорта Azure и управления ими, что позволяет передавать большие объемы данных в хранилище BLOB-объектов Azure или из него.</span><span class="sxs-lookup"><span data-stu-id="ac08b-104">The Azure Import/Export Tool (WAImportExport.exe) is used to create and manage jobs for the Azure Import/Export service, enabling you to transfer large amounts of data into or out of Azure Blob Storage.</span></span>

<span data-ttu-id="ac08b-105">Эта документация предназначена для версии средства импорта и экспорта Azure, которая используется в классической модели развертывания.</span><span class="sxs-lookup"><span data-stu-id="ac08b-105">This documentation is for the classic deployment model of the Azure Import/Export Tool.</span></span> <span data-ttu-id="ac08b-106">Сведения об использовании самой последней версии средства см. в статье [Использование средства импорта и экспорта Azure (классическая модель развертывания)](../storage-import-export-tool-how-to.md).</span><span class="sxs-lookup"><span data-stu-id="ac08b-106">For information about using the most recent version of the tool, see [Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md).</span></span>

<span data-ttu-id="ac08b-107">Из статей в этом разделе вы узнаете, как выполнять следующие операции:</span><span class="sxs-lookup"><span data-stu-id="ac08b-107">The following articles show you how to:</span></span>

- <span data-ttu-id="ac08b-108">Установка и настройка средства импорта и экспорта.</span><span class="sxs-lookup"><span data-stu-id="ac08b-108">Install and set up the Import/Export Tool.</span></span>
- <span data-ttu-id="ac08b-109">Подготовка жестких дисков для задания, импортирующего данные с дисков в хранилища BLOB-объектов Azure.</span><span class="sxs-lookup"><span data-stu-id="ac08b-109">Prepare your hard drives for a job where you import data from your drives to Azure Blob Storage.</span></span>
- <span data-ttu-id="ac08b-110">Просмотр состояния задания с помощью файлов журнала копирования.</span><span class="sxs-lookup"><span data-stu-id="ac08b-110">Review the status of a job with Copy Log Files.</span></span> 
- <span data-ttu-id="ac08b-111">Исправление задания импорта.</span><span class="sxs-lookup"><span data-stu-id="ac08b-111">Repair an import job.</span></span> 
- <span data-ttu-id="ac08b-112">Исправление задания экспорта.</span><span class="sxs-lookup"><span data-stu-id="ac08b-112">Repair an export job.</span></span> 
- <span data-ttu-id="ac08b-113">Устранение неполадок средства импорта и экспорта Azure, возникающих при его использовании.</span><span class="sxs-lookup"><span data-stu-id="ac08b-113">Troubleshoot the Azure Import/Export Tool, in case you had a problem during process.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ac08b-114">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ac08b-114">Next steps</span></span>

* <span data-ttu-id="ac08b-115">[Using the Azure Import/Export Tool](../storage-import-export-tool-how-to.md) (Использование средства импорта и экспорта Azure)</span><span class="sxs-lookup"><span data-stu-id="ac08b-115">[Setting up the WAImportExport tool](../storage-import-export-tool-how-to.md)</span></span>