---
title: "aaaCreate удостоверением рабочей или учебной в AAD для Windows | Документы Microsoft"
description: "Узнайте, как toocreate использованием рабочей или учебной удостоверения Azure Active Directory toouse с виртуальными машинами Windows."
services: virtual-machines-windows
documentationcenter: 
author: squillace
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: d07dca34-618a-48aa-9971-03d9c1210f4a
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/23/2016
ms.author: rasquill
ms.openlocfilehash: dd6e2381fd0aa503483aa786b36232e557729c4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-a-work-or-school-identity-in-azure-active-directory-toouse-with-windows-vms"></a>Создание рабочего или учебного заведения удостоверения в Azure Active Directory toouse с виртуальными машинами Windows
Если создать личную учетную запись Azure или иметь личные подписки MSDN и создан hello учетная запись Azure tootake деньги на счете MSDN Azure hello--используется *учетную запись Майкрософт* toocreate удостоверение его. Много замечательных функций Azure — [шаблоны группы ресурсов](../../azure-resource-manager/resource-group-overview.md) один пример — требуется рабочая или учебная учетная запись (удостоверение, под управлением Azure Active Directory) toowork. Можно выполнить hello приведенные ниже инструкции toocreate, так как к счастью, одна из наиболее удобных свойств hello личную учетную запись Azure он поставляется с доменом Azure Active Directory по умолчанию, которые можно использовать toocreate новой рабочей или учебной учетной записи новой работы или учебы Учетная запись, можно использовать с компонентами Azure, которые их используют.

Однако последние изменения обеспечивает его возможных toomanage подписки с любым типом учетной записи Azure, с помощью hello `azure login` интерактивного входа в систему из описанных [здесь](../../xplat-cli-connect.md). Вы можете использовать этот механизм, или можно выполнить следующие инструкции hello. Вы также можете [создания рабочей или учебной удостоверения в Azure Active Directory toouse с виртуальными машинами Linux](../linux/create-aad-work-id.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).

[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

[!INCLUDE [virtual-machines-common-create-aad-work-id](../../../includes/virtual-machines-common-create-aad-work-id.md)]

