---
title: "aaaCannot удалить виртуальную сеть в Azure | Документы Microsoft"
description: "Узнайте, как tootroubleshoot hello проблему, в котором не удается удалить виртуальную сеть в Azure."
services: virtual-network
documentationcenter: na
author: chadmath
manager: cshepard
editor: 
tags: azure-resource-manager
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/17/2017
ms.author: genli
ms.openlocfilehash: a9050ab238ccb0380fd46130430222efb8f42388
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-failed-toodelete-a-virtual-network-in-azure"></a>Устранение неполадок: Не удалось выполнить toodelete виртуальной сети в Azure

Могут возникать ошибки, при попытке toodelete виртуальной сети в Microsoft Azure. В этой статье приведены по устранению неполадок toohelp действия при решении этой проблемы. 

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="troubleshooting-guidance"></a>Рекомендации по устранению неполадок 

1. [Проверьте, работает ли шлюз виртуальной сети в виртуальной сети hello](#check-whether-a-virtual-network-gateway-is-running-in-the-virtual-network).
2. [Проверьте, работает ли шлюз приложений в виртуальной сети hello](#check-whether-an-application-gateway-is-running-in-the-virtual-network).
3. [Проверьте, включен ли доменные службы Active Directory Azure в виртуальной сети hello](#check-whether-azure-active-directory-domain-service-is-enabled-in-the-virtual-network).
4. [Проверить, является ли виртуальной сети hello подключенных tooother ресурсов](#check-whether-the-virtual-network-is-connected-to-other-resource).
5. [Проверьте, работает ли по-прежнему виртуальной машины в виртуальной сети hello](#check-whether-a-virtual-machine-is-still-running-in-the-virtual-network).
6. [Проверьте, повторяется ли hello виртуальной сети миграции](#check-whether-the-virtual-network-is-stuck-in-migration).

## <a name="troubleshooting-steps"></a>Действия по устранению неполадок

### <a name="check-whether-a-virtual-network-gateway-is-running-in-hello-virtual-network"></a>Проверьте, работает ли шлюз виртуальной сети в виртуальной сети hello

tooremove hello виртуальной сети, необходимо сначала удалить шлюз виртуальной сети hello.

Для классических виртуальных сетей, go toohello **Обзор** страницы приветствия классической виртуальной сети в hello портал Azure. В hello **VPN-подключений** статьи, если hello шлюз работает в виртуальной сети hello, вы увидите hello IP адрес шлюза hello. 

![Проверка работы шлюза](media/virtual-network-troubleshoot-cannot-delete-vnet/classic-gateway.png)

Для виртуальных сетей go toohello **Обзор** страницы приветствия виртуальной сети. Проверьте **подключенных устройств** для hello шлюза виртуальной сети.

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/vnet-gateway.png)

Перед удалением hello шлюз, сначала удаляйте **подключения** объектов в hello шлюза. 

### <a name="check-whether-an-application-gateway-is-running-in-hello-virtual-network"></a>Проверьте, работает ли шлюз приложений в виртуальной сети hello

Go toohello **Обзор** страницы приветствия виртуальной сети. Проверьте hello **подключенных устройств** для шлюза приложения hello.

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/app-gateway.png)

Если шлюз приложений, необходимо удалить перед удалением виртуальной сети hello.

### <a name="check-whether-azure-active-directory-domain-service-is-enabled-in-hello-virtual-network"></a>Проверьте, включен ли доменные службы Active Directory Azure в виртуальной сети hello

Если включен и подключен toohello виртуальной сети hello доменные службы Active Directory, нельзя удалить эту виртуальную сеть. 

![Проверьте hello подключенного устройства](media/virtual-network-troubleshoot-cannot-delete-vnet/enable-domain-services.png)

toodisable Здравствуйте службы, выполните следующие действия:

1. Go toohello [классический портал Azure](https://manage.windowsazure.com).
2. Выберите в левой области hello **Active Directory**.
3. Выберите каталог hello Azure Active Directory (Azure AD), который имеет доменные службы Active Directory включена.
4. Выберите hello **Настройка** вкладки.
5. В разделе **доменных служб**, измените hello **Включение доменных служб для этого каталога** параметр слишком**нет**.  

### <a name="check-whether-hello-virtual-network-is-connected-tooother-resource"></a>Проверить, является ли виртуальной сети hello подключенных tooother ресурсов

Проверьте наличие каналов связи, соединений и пирингов виртуальных сетей. Любой из них может привести к toofail удаления виртуальной сети. 

Hello удаления Рекомендуемый порядок выглядит следующим образом:

1. Подключения шлюза.
2. Шлюзы
3. IP-адреса.
4. Пиринги виртуальных сетей.
5. Среда службы приложений (ASE).

### <a name="check-whether-a-virtual-machine-is-still-running-in-hello-virtual-network"></a>Проверьте, работает ли по-прежнему виртуальной машины в виртуальной сети hello

Убедитесь, что виртуальные машины не находится в виртуальной сети hello.

### <a name="check-whether-hello-virtual-network-is-stuck-in-migration"></a>Проверьте, повторяется ли hello виртуальной сети миграции

Если виртуальная сеть hello застряла в состоянии миграции, его нельзя удалить. Запустите hello, следующая команда tooabort hello миграции, а затем удалите hello виртуальной сети.

    Move-AzureVirtualNetwork -VirtualNetworkName "Name" -Abort

## <a name="next-steps"></a>Дальнейшие действия

- [Виртуальная сеть Azure](virtual-networks-overview.md)
- [Виртуальная сеть Azure: часто задаваемые вопросы](virtual-networks-faq.md)