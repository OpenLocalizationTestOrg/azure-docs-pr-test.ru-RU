---
title: "Установка Visual Studio и SSDT для хранилища данных SQL | Документация Майкрософт"
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
ms.openlocfilehash: f7023b78c241a7bc8014276cd0bfa455165b42cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a><span data-ttu-id="44652-103">Установка Visual Studio и SSDT для хранилища данных SQL</span><span class="sxs-lookup"><span data-stu-id="44652-103">Install Visual Studio and SSDT for SQL Data Warehouse</span></span>
<span data-ttu-id="44652-104">При разработке приложений для хранилища данных SQL мы рекомендуем использовать последнюю версию Visual Studio с последней версией SQL Server Data Tools (SSDT).</span><span class="sxs-lookup"><span data-stu-id="44652-104">To develop applications for SQL Data Warehouse, we recommend using the most recent version of Visual Studio with the most recent version of SQL Server Data Tools (SSDT).</span></span>  <span data-ttu-id="44652-105">Также для обратной совместимости поддерживается Visual Studio 2013 Update 5 с SSDT.</span><span class="sxs-lookup"><span data-stu-id="44652-105">Visual Studio 2013 Update 5 with SSDT is also supported for backward compatibility.</span></span>  

<span data-ttu-id="44652-106">С помощью Visual Studio с SSDT вы сможете использовать обозреватель объектов SQL Server для визуального исследования таблиц, представлений, хранимых процедур и многих других объектов в хранилище данных SQL, а также выполнения запросов.</span><span class="sxs-lookup"><span data-stu-id="44652-106">Using Visual Studio with SSDT will allow you to use the SQL Server Object Explorer to visually explore tables, views, stored procedures and many more objects in your SQL Data Warehouse as well as run queries.</span></span>

> [!NOTE]
> <span data-ttu-id="44652-107">Хранилище данных SQL пока не поддерживает проекты базы данных Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="44652-107">SQL Data Warehouse does not yet support Visual Studio Database Projects.</span></span>  <span data-ttu-id="44652-108">Эта функция будет добавлена в одной из следующих версий.</span><span class="sxs-lookup"><span data-stu-id="44652-108">This feature will be added in a future version.</span></span>
> 
> 

## <a name="step-1-install-visual-studio"></a><span data-ttu-id="44652-109">Шаг 1. Установка Visual Studio</span><span class="sxs-lookup"><span data-stu-id="44652-109">Step 1: Install Visual Studio</span></span>
<span data-ttu-id="44652-110">Скачайте и установите Visual Studio, используя приведенные ниже ссылки.</span><span class="sxs-lookup"><span data-stu-id="44652-110">Follow these links to download and install Visual Studio.</span></span> <span data-ttu-id="44652-111">Если приложение Visual Studio 2013 или его более поздняя версия уже установлена, можно перейти к шагу 2 и установить SSDT.</span><span class="sxs-lookup"><span data-stu-id="44652-111">If you already have Visual Studio 2013 or later installed, you can skip to Step 2, install SSDT.</span></span>

1. <span data-ttu-id="44652-112">[Скачайте Visual Studio][].</span><span class="sxs-lookup"><span data-stu-id="44652-112">[Download Visual Studio][].</span></span>
2. <span data-ttu-id="44652-113">Выполните установку, следуя инструкциям по [установке Visual Studio][Installing Visual Studio] с сайта MSDN, а затем выберите настройки по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="44652-113">Follow the [Installing Visual Studio][Installing Visual Studio] guide on MSDN and choose the default configurations.</span></span>

## <a name="step-2-install-ssdt"></a><span data-ttu-id="44652-114">Шаг 2. Установка SSDT</span><span class="sxs-lookup"><span data-stu-id="44652-114">Step 2: Install SSDT</span></span>
<span data-ttu-id="44652-115">Чтобы установить SSDT для Visual Studio, проверьте наличие обновления SSDT в Visual Studio, выполнив следующие действия.</span><span class="sxs-lookup"><span data-stu-id="44652-115">To install SSDT for Visual Studio simply check for an SSDT update from within Visual Studio by following these steps.</span></span>

1. <span data-ttu-id="44652-116">В Visual Studio щелкните **Сервис** / **Расширения и обновления…**</span><span class="sxs-lookup"><span data-stu-id="44652-116">In Visual Studio click on **Tools** / **Extensions and Updates…**</span></span><span data-ttu-id="44652-117"> / **Обновления**</span><span class="sxs-lookup"><span data-stu-id="44652-117"> / **Updates**</span></span>
2. <span data-ttu-id="44652-118">Выберите **Обновления продукта** и найдите элемент **Обновление Microsoft SQL Server для средств работы с базами данных**.</span><span class="sxs-lookup"><span data-stu-id="44652-118">Select **Product Updates** and then look for **Microsoft SQL Server Update for database tooling**</span></span>

<span data-ttu-id="44652-119">Если обновление не найдено, у вас установлена последняя версия.</span><span class="sxs-lookup"><span data-stu-id="44652-119">If an update is not found, then you should have the latest version installed.</span></span>  <span data-ttu-id="44652-120">Чтобы убедиться, что компонент SSDT установлен, выберите **Справка** / **О Microsoft Visual Studio** и найдите в списке SQL Server Data Tools.</span><span class="sxs-lookup"><span data-stu-id="44652-120">To confirm SSDT is installed, click on **Help** / **About Microsoft Visual Studio** and look for SQL Server Data Tools in the list.</span></span>  <span data-ttu-id="44652-121">Последняя версия SSDT: 14.0.60525.0.</span><span class="sxs-lookup"><span data-stu-id="44652-121">The latest version of SSDT is 14.0.60525.0.</span></span>  <span data-ttu-id="44652-122">Если команда установки недоступна в Visual Studio, также можно посетить страницу [Скачать SQL Server Data Tools (SSDT)][SSDT Download], чтобы скачать и установить SSDT вручную.</span><span class="sxs-lookup"><span data-stu-id="44652-122">If the option to install is not available from Visual Studio, alternatively you can visit the [SSDT Download][SSDT Download] page to download and install SSDT manually.</span></span>

## <a name="next-steps"></a><span data-ttu-id="44652-123">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="44652-123">Next steps</span></span>
<span data-ttu-id="44652-124">Теперь, когда у вас установлена последняя версия SSDT, можно [подключиться][connect] к хранилищу данных SQL.</span><span class="sxs-lookup"><span data-stu-id="44652-124">Now that you have the latest version of SSDT, you are ready to [connect][connect] to your SQL Data Warehouse.</span></span>

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
<span data-ttu-id="44652-125">[Скачайте Visual Studio]: https://www.visualstudio.com/downloads/</span><span class="sxs-lookup"><span data-stu-id="44652-125">[Download Visual Studio]: https://www.visualstudio.com/downloads/</span></span>
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
