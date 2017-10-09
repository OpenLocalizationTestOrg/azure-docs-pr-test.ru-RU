---
title: "Поддержка клиентов нижнего уровня хранилища данных aaaSQL аудит данных | Документы Microsoft"
description: "Сведения о поддержке клиентов прежних версий хранилища данных SQL для аудита данных"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: dfe29ff3-dfeb-4309-83c0-c1a300f4f44e
ms.service: sql-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 10/31/2016
ms.author: rortloff;barbkess
ms.openlocfilehash: 377488680eb297c3e9b1dc754c003c5b19b47996
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a><span data-ttu-id="72738-103">Хранилище данных SQL. Поддержка клиентов прежних версий для аудита и динамического маскирования данных</span><span class="sxs-lookup"><span data-stu-id="72738-103">SQL Data Warehouse -  Downlevel clients support for auditing and Dynamic Data Masking</span></span>
<span data-ttu-id="72738-104">[аудита](sql-data-warehouse-auditing-overview.md) работают в клиентах SQL, которые поддерживают перенаправление TDS.</span><span class="sxs-lookup"><span data-stu-id="72738-104">[Auditing](sql-data-warehouse-auditing-overview.md) works with SQL clients that support TDS redirection.</span></span>

<span data-ttu-id="72738-105">Любой клиент, который реализует TDS 7.4, также должен поддерживать перенаправление.</span><span class="sxs-lookup"><span data-stu-id="72738-105">Any client which implements TDS 7.4 should also support redirection.</span></span> <span data-ttu-id="72738-106">Toothis исключения включают JDBC 4.0 в какие функции перенаправления hello поддерживается не полностью и Tedious для Node.JS, в котором перенаправление не был реализован.</span><span class="sxs-lookup"><span data-stu-id="72738-106">Exceptions toothis include JDBC 4.0 in which hello redirection feature is not fully supported and Tedious for Node.JS in which redirection was not implemented.</span></span>

<span data-ttu-id="72738-107">Для «Клиентов нижнего уровня» т. е. который обеспечить поддержку потока табличных данных версии 7.3 и ниже - hello полное доменное имя сервера в строке подключения hello может изменяться:</span><span class="sxs-lookup"><span data-stu-id="72738-107">For "Downlevel clients", i.e. which support TDS version 7.3 and below - hello server FQDN in hello connection string should be modified:</span></span>

<span data-ttu-id="72738-108">Исходное полное доменное имя сервера в строке подключения hello: <*имя сервера*>. database.windows.net</span><span class="sxs-lookup"><span data-stu-id="72738-108">Original server FQDN in hello connection string: <*server name*>.database.windows.net</span></span>

<span data-ttu-id="72738-109">Измененный полное доменное имя сервера в строке подключения hello: <*имя сервера*> .database. **безопасный**. windows.net</span><span class="sxs-lookup"><span data-stu-id="72738-109">Modified server FQDN in hello connection string: <*server name*>.database.**secure**.windows.net</span></span>

<span data-ttu-id="72738-110">Частичный список клиентов прежних версий включает:</span><span class="sxs-lookup"><span data-stu-id="72738-110">A partial list of "Downlevel clients" includes:</span></span>

* <span data-ttu-id="72738-111">.NET 4.0 и ниже</span><span class="sxs-lookup"><span data-stu-id="72738-111">.NET 4.0 and below,</span></span>
* <span data-ttu-id="72738-112">ODBC 10.0 и ниже</span><span class="sxs-lookup"><span data-stu-id="72738-112">ODBC 10.0 and below.</span></span>
* <span data-ttu-id="72738-113">JDBC (хотя JDBC поддерживают TDS 7.4, функция перенаправления потока табличных данных поддерживается не полностью приветствия)</span><span class="sxs-lookup"><span data-stu-id="72738-113">JDBC (while JDBC does support TDS 7.4, hello TDS redirection feature is not fully supported)</span></span>
* <span data-ttu-id="72738-114">Tedious (для Node.JS)</span><span class="sxs-lookup"><span data-stu-id="72738-114">Tedious (for Node.JS)</span></span>

<span data-ttu-id="72738-115">**Замечание:** hello выше FDQN изменения сервера можно использовать также для применения политики аудита уровня SQL Server без потребность в конфигурации шаг в каждой базе данных (временный уменьшение).</span><span class="sxs-lookup"><span data-stu-id="72738-115">**Remark:** hello above server FDQN modification may be useful also for applying a SQL Server Level Auditing policy without a need for a configuration step in each database (Temporary mitigation).</span></span>     

