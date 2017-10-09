---
title: "в классической виртуальной Машине Linux с помощью aaaCreate hello Azure CLI 1.0 | Документы Microsoft"
description: "Узнайте, как toocreate виртуальной машины Linux с использованием hello Azure CLI 1.0 hello классической модели развертывания"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: f8071a2e-ed91-4f77-87d9-519a37e5364f
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 02/09/2017
ms.author: iainfou
ms.openlocfilehash: 5c3c54e5d1444a79e8e609c76d04a3a621c8d03f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-classic-linux-vm-with-hello-azure-cli-10"></a>Как tooCreate в классической виртуальной Машины Linux с hello Azure CLI 1.0
> [!IMPORTANT] 
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель диспетчера ресурсов и классическая модель](../../../resource-manager-deployment-model.md). В этой статье описан с помощью hello классической модели развертывания. Корпорация Майкрософт рекомендует наиболее новые развертывания модели hello диспетчера ресурсов. Hello диспетчера ресурсов версию в разделе [здесь](../create-cli-complete.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

В этом разделе описывается, как toocreate виртуальной машины (VM) Linux с использованием hello Azure CLI 1.0 hello классической модели развертывания. Мы используем образа Linux из доступных hello **ИЗОБРАЖЕНИЯ** в Azure. команды, Hello Azure CLI 1.0 дают hello следующие варианты конфигурации, в частности:

* Подключение hello ВМ tooa виртуальной сети
* Добавление hello tooan существующие облачная служба виртуальных Машин
* Добавление hello tooan существующего хранилища учетную запись виртуальной Машины
* Добавление группы доступности tooan Виртуальной hello или расположение

> [!IMPORTANT]
> Если вы хотите toouse вашей виртуальной Машины виртуальной сети, для подключения tooit напрямую по имени узла или набор подключений между организациями, убедитесь, что при создании виртуальной Машины hello, укажите hello виртуальной сети. Виртуальная машина может быть настроенный toojoin виртуальной сети только при создании виртуальной Машины hello. Дополнительную информацию о виртуальных сетях см. в разделе [Обзор виртуальных сетей Azure](http://go.microsoft.com/fwlink/p/?LinkID=294063).
> 
> 

## <a name="how-toocreate-a-linux-vm-using-hello-classic-deployment-model"></a>Как toocreate в виртуальной Машине Linux с помощью hello классической модели развертывания
[!INCLUDE [virtual-machines-create-LinuxVM](../../../../includes/virtual-machines-create-linuxvm.md)]

