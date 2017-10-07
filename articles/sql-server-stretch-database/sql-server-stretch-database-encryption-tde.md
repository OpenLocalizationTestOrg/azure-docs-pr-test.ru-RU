---
title: "Прозрачное шифрование данных для базы данных Stretch - Azure aaaEnable | Документы Microsoft"
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
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a>Включение прозрачного шифрования данных (TDE) для базы данных Stretch в Azure
> [!div class="op_single_selector"]
> * [Портал Azure](sql-server-stretch-database-encryption-tde.md)
> * [TSQL](sql-server-stretch-database-tde-tsql.md)
>
>

Прозрачное шифрование данных (TDE) защищает от угроз вредоносных действий hello выполняя в реальном времени шифрование и расшифровку hello базы данных, связанных резервных копий и файлов журнала транзакций при этом не требуется toohello изменения приложение.

TDE шифрует hello хранения всей базы данных с помощью ключа шифрования симметричного ключа вызываемой hello базы данных. ключ шифрования базы данных Hello защищен используется встроенный сертификат сервера. Hello встроенный сертификат сервера уникален для каждого сервера Azure. Корпорация Майкрософт автоматически изменяет эти сертификаты не реже, чем раз в 90 дней. Общие сведения о прозрачном шифровании данных см. в [этой статье].

## <a name="enabling-encryption"></a>Включение шифрования
tooenable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:

1. Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)
2. В колонке базы данных hello, щелкните hello **параметры** кнопки
3. Выберите hello **прозрачное шифрование данных** параметр![][1]
4. Выберите hello **на** задание, а затем выберите **сохранить**
   ![][2]

## <a name="disabling-encryption"></a>Отключение шифрования
toodisable прозрачное шифрование данных для базы данных Azure, хранящей hello переноса данных из базы данных SQL Server с поддержкой Stretch, hello следующие действия:

1. Привет открыть базу данных в hello [портал Azure](https://portal.azure.com)
2. В колонке базы данных hello, щелкните hello **параметры** кнопки
3. Выберите hello **прозрачное шифрование данных** параметр
4. Выберите hello **Off** задание, а затем выберите **сохранить**

<!--Anchors-->
[этой статье]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
