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
# <a name="sql-data-warehouse----downlevel-clients-support-for-auditing-and-dynamic-data-masking"></a>Хранилище данных SQL. Поддержка клиентов прежних версий для аудита и динамического маскирования данных
[аудита](sql-data-warehouse-auditing-overview.md) работают в клиентах SQL, которые поддерживают перенаправление TDS.

Любой клиент, который реализует TDS 7.4, также должен поддерживать перенаправление. Toothis исключения включают JDBC 4.0 в какие функции перенаправления hello поддерживается не полностью и Tedious для Node.JS, в котором перенаправление не был реализован.

Для «Клиентов нижнего уровня» т. е. который обеспечить поддержку потока табличных данных версии 7.3 и ниже - hello полное доменное имя сервера в строке подключения hello может изменяться:

Исходное полное доменное имя сервера в строке подключения hello: <*имя сервера*>. database.windows.net

Измененный полное доменное имя сервера в строке подключения hello: <*имя сервера*> .database. **безопасный**. windows.net

Частичный список клиентов прежних версий включает:

* .NET 4.0 и ниже
* ODBC 10.0 и ниже
* JDBC (хотя JDBC поддерживают TDS 7.4, функция перенаправления потока табличных данных поддерживается не полностью приветствия)
* Tedious (для Node.JS)

**Замечание:** hello выше FDQN изменения сервера можно использовать также для применения политики аудита уровня SQL Server без потребность в конфигурации шаг в каждой базе данных (временный уменьшение).     

