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
# <a name="install-visual-studio-and-ssdt-for-sql-data-warehouse"></a>Установка Visual Studio и SSDT для хранилища данных SQL
toodevelop приложений для хранилища данных SQL, мы рекомендуем использовать hello самую последнюю версию Visual Studio с последней версией hello из SQL Server Data Tools (SSDT).  Также для обратной совместимости поддерживается Visual Studio 2013 Update 5 с SSDT.  

С помощью Visual Studio с помощью SSDT позволит вам toouse hello обозреватель объектов SQL Server toovisually просмотра таблиц, представлений, хранимых процедур и намного больше объектов в хранилище данных SQL, а также для выполнения запросов.

> [!NOTE]
> Хранилище данных SQL пока не поддерживает проекты базы данных Visual Studio.  Эта функция будет добавлена в одной из следующих версий.
> 
> 

## <a name="step-1-install-visual-studio"></a>Шаг 1. Установка Visual Studio
Выполните эти ссылки toodownload и установите Visual Studio. Если у вас уже есть Visual Studio 2013 или более поздней версии, можно пропустить tooStep 2, установите SSDT.

1. [Скачайте Visual Studio][].
2. Выполните hello [установка Visual Studio] [ Installing Visual Studio] руководство по на сайте MSDN и выбрать конфигурации по умолчанию hello.

## <a name="step-2-install-ssdt"></a>Шаг 2. Установка SSDT
tooinstall SSDT для Visual Studio просто проверить наличие обновлений SSDT из среды Visual Studio, выполните следующие действия.

1. В Visual Studio щелкните **Сервис** / **Расширения и обновления…** / **Обновления**
2. Выберите **Обновления продукта** и найдите элемент **Обновление Microsoft SQL Server для средств работы с базами данных**.

Если обновление не установлено, то должен иметь hello последняя версия.  tooconfirm SSDT установлен, щелкните **справки** / **о Microsoft Visual Studio** и найдите в списке hello SQL Server Data Tools.  Последняя версия SSDT Hello — 14.0.60525.0.  Если параметр tooinstall hello не доступен из Visual Studio, либо можно посетить hello [загрузки SSDT] [ SSDT Download] toodownload и вручную установить SSDT.

## <a name="next-steps"></a>Дальнейшие действия
Теперь, когда hello последней версии SSDT вы готовы слишком[подключения] [ connect] tooyour хранилище данных SQL.

<!--Anchors-->

<!--Image references-->

<!--Articles-->
[connect]: ./sql-data-warehouse-query-visual-studio.md

<!--Other-->
[Скачайте Visual Studio]: https://www.visualstudio.com/downloads/
[Installing Visual Studio]: https://msdn.microsoft.com/library/e2h7fzkw.aspx
[SSDT Download]: https://msdn.microsoft.com/library/mt204009.aspx
