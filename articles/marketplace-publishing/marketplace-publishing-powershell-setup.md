---
title: "aaaSet копирование toocreate PowerShell виртуальной Машины для hello Marketplace | Документы Microsoft"
description: "Инструкции по установке Azure PowerShell и использовать ее в качестве необязательный процесс потока toocreate toodeploy образы виртуальных Машин и продавать, hello Azure Marketplace"
services: marketplace-publishing
documentationcenter: 
author: HannibalSII
manager: hascipio
editor: 
ms.assetid: e19d6cda-76df-4e42-be84-c9fe47a636db
ms.service: marketplace
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/04/2016
ms.author: hascipio
ms.openlocfilehash: cd2ebad7472248b8f921706e1a8c82d41f33b9cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-azure-powershell-toocreate-an-offer-for-hello-azure-marketplace"></a>Настройка Azure PowerShell toocreate предложение hello Azure Marketplace
Подробные сведения о том, как tooset копирование PowerShell в Azure, в разделе [как tooinstall и настройка Azure PowerShell](/powershell/azure/overview). Простой подход — toouse hello сертификат метод, который загружает и импортирует сертификат, необходимый для проверки подлинности. требуется сертификат, используйте hello tooobtain hello **Get-AzurePublishSettingsFile** командлета. Сохраните файл hello, когда появится запрос. сертификат tooimport hello в сеанс PowerShell, используйте hello **команду Import-AzurePublishSettingsFile** командлета.

tooconfigure и хранилище hello общих Microsoft Azure подписки для параметров сеанса PowerShell hello, используется hello **Set-AzureSubscription** и **Select-AzureSubscription** командлетов:

        Set-AzureSubscription -SubscriptionName “mySubName” -CurrentStorageAccountName “mystorageaccount”
        Select-AzureSubscription -SubscriptionName "mySubName" –Current

Первая команда Hello связывает учетную запись хранения по умолчанию с hello подписки (требуется для некоторых операций подготовки виртуальной Машины).  Во-вторых Hello делает подписки hello hello текущим (распознать другими командлетами).

## <a name="see-also"></a>См. также
* [Приступая к работе: как toopublish toohello предложение Azure Marketplace](marketplace-publishing-getting-started.md)
* [Создание образа виртуальной машины для hello Marketplace](marketplace-publishing-vm-image-creation.md)

