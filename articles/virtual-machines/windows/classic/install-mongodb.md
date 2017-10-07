---
title: "aaaInstall MongoDB на виртуальной Машине Windows в Azure | Документы Microsoft"
description: "Узнайте, как tooinstall MongoDB на Виртуальной машине Azure создан с hello классической модели развертывания под управлением Windows Server."
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 4095df41-bb69-4bbe-9c1c-70923b0d84ba
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 03/07/2017
ms.author: iainfou
ms.openlocfilehash: aafd86b4c49c6a97ae8a1a2191ae375b6c47483a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="install-mongodb-on-a-windows-vm-in-azure"></a>Установите MongoDB на виртуальную машину Windows в Azure
> [!IMPORTANT]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md).  В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. tooinstall и настроить с помощью модели развертывания диспетчера ресурсов hello MongoDB см. в разделе [в этой статье](../install-mongodb.md).

[MongoDB][MongoDB] — это популярная высокопроизводительная база данных NoSQL с открытым кодом. В этой статье руководство по созданию Windows Server виртуальной машины (VM) с помощью hello [портал Azure][AzurePortal]. Затем создайте и присоединить toohello диска данных виртуальной Машины перед установкой и настройкой MongoDB. При наличии существующей виртуальной Машины в Azure, желательно toouse перехода непосредственно слишком[Установка и настройка MongoDB](#install-and-run-mongodb-on-the-virtual-machine).

## <a name="create-a-virtual-machine-running-windows-server"></a>Создание виртуальной машины под управлением Windows Server
Выполните эти инструкции toocreate виртуальной машины.

[!INCLUDE [virtual-machines-create-WindowsVM](../../../../includes/virtual-machines-create-windowsvm.md)]

> [!NOTE]
> Добавить конечную точку для MongoDB при создании виртуальной машины hello и настроить его следующим образом: имя его как **Mongo**, используйте **TCP** как hello протокола и set обеих hello общие и частные порты слишком**27017**.
>
>

## <a name="attach-a-data-disk"></a>Присоединение диска данных
tooprovide хранилище для hello виртуальной машины, подключить диск данных и затем инициализируйте его, чтобы Windows могла использовать его. Можно подключить существующий диск или пустой диск.

[!INCLUDE [howto-attach-disk-windows-linux](../../../../includes/howto-attach-disk-windows-linux.md)]

Инициализация диска hello инструкции см. в разделе «как: инициализация нового диска с данными в Windows Server» в [как tooattach данных на диске виртуальной машины Windows tooa](attach-disk.md).

## <a name="install-and-run-mongodb-on-hello-virtual-machine"></a>Установить и запустить на виртуальной машине hello MongoDB
[!INCLUDE [install-and-run-mongo-on-win2k8-vm](../../../../includes/install-and-run-mongo-on-win2k8-vm.md)]

## <a name="summary"></a>Сводка
В этом учебнике вы узнали, как toocreate виртуальной машины под управлением Windows Server удаленно подключиться tooit и присоединить диск данных.  Вы также узнали, каким образом tooinstall и настройте MongoDB на основе Windows hello виртуальной машине. Теперь вы можете просматривать MongoDB на hello на основе Windows виртуальной машины с следующие дополнительные разделы в hello hello [документацию MongoDB][MongoDocs].

[MongoDocs]: http://docs.mongodb.org/manual/
[MongoDB]: http://www.mongodb.org/
[AzurePortal]: https://portal.azure.com/

