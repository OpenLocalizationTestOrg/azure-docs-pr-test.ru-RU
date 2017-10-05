---
title: "Включение прозрачного шифрования данных для базы данных Stretch в Azure | Документация Майкрософт"
description: "Включение прозрачного шифрования данных (TDE) для базы данных SQL Server Stretch в Azure"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="95b63-103">Включение прозрачного шифрования данных (TDE) для базы данных Stretch в Azure</span><span class="sxs-lookup"><span data-stu-id="95b63-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="95b63-104">Портал Azure</span><span class="sxs-lookup"><span data-stu-id="95b63-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="95b63-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="95b63-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="95b63-106">Прозрачное шифрование данных (TDE) помогает защититься от угрозы вредоносных атак за счет шифрования и расшифровки базы данных, связанных резервных копий и файлов журналов транзакций при хранении в реальном времени, не внося изменения в само приложение.</span><span class="sxs-lookup"><span data-stu-id="95b63-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="95b63-107">При использовании TDE хранилище всей базы данных шифруется с помощью симметричного ключа, который называется ключом шифрования базы данных.</span><span class="sxs-lookup"><span data-stu-id="95b63-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="95b63-108">Ключ шифрования базы данных защищается встроенным сертификатом сервера.</span><span class="sxs-lookup"><span data-stu-id="95b63-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="95b63-109">Каждый сервер Azure обладает уникальным встроенным сертификатом.</span><span class="sxs-lookup"><span data-stu-id="95b63-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="95b63-110">Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней.</span><span class="sxs-lookup"><span data-stu-id="95b63-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="95b63-111">Общие сведения о прозрачном шифровании данных см. в [этой статье].</span><span class="sxs-lookup"><span data-stu-id="95b63-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="95b63-112">Включение шифрования</span><span class="sxs-lookup"><span data-stu-id="95b63-112">Enabling Encryption</span></span>
<span data-ttu-id="95b63-113">Чтобы включить прозрачное шифрование для базы данных Azure, где хранятся данные, перенесенные из Базы данных SQL Server Stretch, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="95b63-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="95b63-114">Откройте базу данных на [Портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="95b63-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="95b63-115">В колонке базы данных нажмите кнопку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="95b63-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="95b63-116">Выберите параметр **Прозрачное шифрование данных** . ![][1]</span><span class="sxs-lookup"><span data-stu-id="95b63-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="95b63-117">Выберите параметр **Включить**, а затем — **Сохранить**
   ![][2].</span><span class="sxs-lookup"><span data-stu-id="95b63-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="95b63-118">Отключение шифрования</span><span class="sxs-lookup"><span data-stu-id="95b63-118">Disabling Encryption</span></span>
<span data-ttu-id="95b63-119">Чтобы отключить прозрачное шифрование для базы данных Azure, где хранятся данные, перенесенные из Базы данных SQL Server Stretch, выполните следующее.</span><span class="sxs-lookup"><span data-stu-id="95b63-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="95b63-120">Откройте базу данных на [Портал Azure](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="95b63-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="95b63-121">В колонке базы данных нажмите кнопку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="95b63-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="95b63-122">Выберите параметр **Прозрачное шифрование данных** .</span><span class="sxs-lookup"><span data-stu-id="95b63-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="95b63-123">Выберите параметр **Отключить**, а затем — **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="95b63-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="95b63-124">[этой статье]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="95b63-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
