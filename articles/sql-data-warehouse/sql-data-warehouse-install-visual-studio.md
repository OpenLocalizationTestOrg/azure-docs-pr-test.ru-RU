---
title: "aaaInstall Visual Studio и SSDT для хранилища данных SQL | Документы Microsoft"
description: "Установка Visual Studio и SQL Server Data Tools (SSDT) для хранилища данных SQL Azure."
services: sql-data-warehouse
documentationcenter: NA
author: antvgski
manager: jhubbard
editor: 
ms.assetid: 0ed9b406-9b42-4fe6-b963-fe0a5b48aac1
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: connect
ms.date: 03/30/2017
ms.author: anvang;barbkess
ms.openlocfilehash: cf49c13d5cab598ed127f5702c04168b62ede0dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="a572f-103">Установка Visual Studio и SSDT для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="a572f-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="a572f-104">toodevelop приложений для хранилища данных SQL, мы рекомендуем использовать hello самую последнюю версию Visual Studio с последней версией hello из SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="a572f-104">toodevelop applications for SQL Data Warehouse, we recommend using hello most recent version of Visual Studio with hello most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="a572f-105">Также для обратной совместимости поддерживается Visual Studio 2013 Update 5 с SSDT.</span><span class="sxs-lookup"><span data-stu-id="a572f-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="a572f-106">С помощью Visual Studio с помощью SSDT позволит вам toouse hello обозреватель объектов SQL Server toovisually просмотра таблиц, представлений, хранимых процедур и намного больше объектов в хранилище данных SQL, а также для выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="a572f-106">Using Visual Studio with SSDT will allow you toouse hello SQL Server Object Explorer toovisually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="a572f-107">Хранилище данных SQL пока не поддерживает проекты базы данных Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a572f-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="a572f-108">Эта функция будет добавлена в одной из следующих версий.</span><span class="sxs-lookup"><span data-stu-id="a572f-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="a572f-109">Шаг 1. Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a572f-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="a572f-110">Выполните эти ссылки toodownload и установите Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a572f-110">Follow these links toodownload and install Visual Studio.</span></span> <span data-ttu-id="a572f-111">Если у вас уже есть Visual Studio 2013 или более поздней версии, можно пропустить tooStep 2, установите SSDT.</span><span class="sxs-lookup"><span data-stu-id="a572f-111">If you already have Visual Studio 2013 or later installed, you can skip tooStep 2, install SSDT.</span></span>

1. <span data-ttu-id="a572f-112">[Скачайте Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="a572f-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="a572f-113">Выполните hello [установка Visual Studio] [ Installing Visual Studio] руководство по на сайте MSDN и выбрать конфигурации по умолчанию hello.</span><span class="sxs-lookup"><span data-stu-id="a572f-113">Follow hello [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose hello default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="a572f-114">Шаг 2. Установка SSDT</span><span class="sxs-lookup"><span data-stu-id="a572f-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="a572f-115">tooinstall SSDT для Visual Studio просто проверить наличие обновлений SSDT из среды Visual Studio, выполните следующие действия.</span><span class="sxs-lookup"><span data-stu-id="a572f-115">tooinstall SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="a572f-116">В Visual Studio щелкните **Сервис** / **Расширения и обновления…**</span><span class="sxs-lookup"><span data-stu-id="a572f-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="a572f-117"> / **Обновления**</span><span class="sxs-lookup"><span data-stu-id="a572f-117"> / **Updates**</span></span>
2. <span data-ttu-id="a572f-118">Выберите **Обновления продукта** и найдите элемент **Обновление Microsoft SQL Server для средств работы с базами данных**.</span><span class="sxs-lookup"><span data-stu-id="a572f-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="a572f-119">Если обновление не установлено, то должен иметь hello последняя версия.</span><span class="sxs-lookup"><span data-stu-id="a572f-119">If an update is not found, then you should have hello latest version installed.</span></span>  <span data-ttu-id="a572f-120">tooconfirm SSDT установлен, щелкните **справки** / **о Microsoft Visual Studio** и найдите в списке hello SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="a572f-120">tooconfirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in hello list.</span></span>  <span data-ttu-id="a572f-121">Последняя версия SSDT Hello — 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="a572f-121">hello latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="a572f-122">Если параметр tooinstall hello не доступен из Visual Studio, либо можно посетить hello [загрузки SSDT] [ SSDT Download] toodownload и вручную установить SSDT.</span><span class="sxs-lookup"><span data-stu-id="a572f-122">If hello option tooinstall is not available from Visual Studio, alternatively you can visit hello [SSDT Download][SSDT Download] page toodownload and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a572f-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a572f-123">Next steps</span></span>
<span data-ttu-id="a572f-124">Теперь, когда hello последней версии SSDT вы готовы слишком[подключения] [ connect] tooyour хранилище данных SQL.</span><span class="sxs-lookup"><span data-stu-id="a572f-124">Now that you have hello latest version of SSDT, you are ready too[connect][connect] tooyour SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Скачайте Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
