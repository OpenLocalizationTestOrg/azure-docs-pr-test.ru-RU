---
title: "Проверьте aaaVerify трафика с потоком IP Наблюдатель сети Azure - портал Azure | Документы Microsoft"
description: "В этой статье описывается как toocheck, если разрешен или запрещен трафик tooor из виртуальной машины"
services: network-watcher
documentationcenter: na
author: georgewallace
manager: timlt
editor: 
ms.assetid: e0e3e9a8-70eb-409a-a744-0ce9deb27148
ms.service: network-watcher
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/22/2017
ms.author: gwallace
ms.openlocfilehash: abf639f36d32f3416dd927e66b635267b746e62f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="check-if-traffic-is-allowed-or-denied-tooor-from-a-vm-with-ip-flow-verify-a-component-of-azure-network-watcher"></a>Проверьте, если трафик разрешен или запрещен tooor из виртуальной Машины с IP потока проверить компонент Наблюдатель сети Azure

> [!div class="op_single_selector"]
> - [Портал Azure](network-watcher-check-ip-flow-verify-portal.md)
> - [PowerShell](network-watcher-check-ip-flow-verify-powershell.md)
> - [Интерфейс командной строки 1.0](network-watcher-check-ip-flow-verify-cli-nodejs.md)
> - [CLI 2.0](network-watcher-check-ip-flow-verify-cli.md)
> - [Azure REST API](network-watcher-check-ip-flow-verify-rest.md)


Проверьте IP потока — это функция Наблюдатель сети, который позволяет вам tooverify, если трафик tooor из виртуальной машины. Hello проверку можно провести для входящего и исходящего трафика. Этот сценарий является полезным tooget текущее состояние ли виртуальная машина может обмениваться информацией tooan внешний ресурс или другой ресурс. Проверьте IP потока может быть tooverify используется, если правила группы безопасности сети (NSG) правильно настроены и устранение неполадок потоки, которые заблокированы правила NSG. Кроме того, использует IP-адрес потока проверки tooensure трафика, что требуется заблокированных блокировано правильно hello NSG.

## <a name="before-you-begin"></a>Перед началом работы

Этот сценарий предполагает уже были выполнены шаги hello в [создать Наблюдатель сети](network-watcher-create.md) toocreate Наблюдатель сети или иметь существующий экземпляр Наблюдатель сети. сценарий Hello также предполагается, что группа ресурсов с действительной виртуальной машиной существует toobe используется.

## <a name="scenario"></a>Сценарий

В этом сценарии используется tooverify потока проверьте IP, если виртуальная машина может обмениваться информацией машины tooanother через порт 443. Если трафик hello запрещен, он возвращает hello правило безопасности, блокирующее, трафик. Посетите toolearn Дополнительные сведения о IP потока проверить, [Обзор потока проверьте IP](network-watcher-ip-flow-verify-overview.md)

### <a name="run-ip-flow-verify"></a>Выполнение проверки IP-потока

Найдите tooyour Наблюдатель сети и нажмите кнопку **проверить поток IP**. Выберите виртуальную машину hello и сетевой интерфейс нужные tooverify трафик от. Введите дополнительную информацию для фильтрации и нажмите кнопку **Проверить**.

После нажатия кнопки **проверьте**, проверяется на основе указанных критериев hello потока hello. Hello результатом является либо **разрешенного доступа** или **отказано в доступе**. Если доступ запрещен, hello группы безопасности сети (NSG) и правила безопасности, блокирующих трафик предоставляется. Если отказ hello трафика результат является ожидаемым, hello правила выполнена успешно.

> [!NOTE]
> Проверьте потока IP требует, что выделена hello ресурса виртуальной Машины.

Как видно из hello после изображения, была разрешена hello исходящего трафика HTTPS.

![Обзор результатов проверки потока IP-адресов][1]

По результатам hello после изображения, изменяется трафика tooinbound и hello входящих too123 изменить порт. Теперь запрещен трафик, приветственное сообщение «Доступ запрещен» предоставляется вместе с hello правило сетевой безопасности группы и безопасности, запрещать трафик hello.

![Результаты проверки потока IP-адресов][2]

## <a name="next-steps"></a>Дальнейшие действия

Если трафик блокируется, и его не следует, см. раздел [Управление группами безопасности сети](../virtual-network/virtual-network-manage-nsg-arm-portal.md) tootrack вниз hello правила сетевой безопасности группы и безопасности, определенных.

[1]: ./media/network-watcher-check-ip-flow-verify-portal/figure1.png
[2]: ./media/network-watcher-check-ip-flow-verify-portal/figure2.png













