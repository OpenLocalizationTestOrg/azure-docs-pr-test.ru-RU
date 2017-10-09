---
title: "Здравствуйте, aaaCreate в наборе масштабирования виртуальных машин с помощью портала Azure | Документы Microsoft"
description: "Развертывание наборов масштабирования с помощью портала Azure."
keywords: "наборы масштабирования виртуальных машин"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: 9c1583f0-bcc7-4b51-9d64-84da76de1fda
ms.service: virtual-machine-scale-sets
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: negat
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 23c88f4b1ba99994a38f8886f60735da74e5c17e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-hello-azure-portal"></a>Как toocreate в наборе масштабирования виртуальных машин с hello портал Azure
Этот учебник показывает, как просто можно toocreate набора масштабирования виртуальных машин через несколько минут, с помощью портала Azure hello. Если у вас еще нет подписки Azure, [создайте бесплатную учетную запись Azure](https://azure.microsoft.com/free/), прежде чем начинать работу.

## <a name="choose-hello-vm-image-from-hello-marketplace"></a>Выберите образ виртуальной Машины hello из hello marketplace
Из портала hello можно легко развертывать набор масштабирования с CentOS, CoreOS, Debian, откройте Suse, Red Hat Enterprise Linux, SUSE Linux Enterprise Server Ubuntu Server или образов Windows Server.

Во-первых, перейдите toohello [портал Azure](https://portal.azure.com) в веб-браузере. Нажмите кнопку `New`, поиск `scale set`, а затем выберите hello `Virtual machine scale set` запись:

![ScaleSetPortalOverview](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalOverview.PNG)

## <a name="create-hello-scale-set"></a>Создание набора масштабирования hello
Теперь можно использовать параметры по умолчанию hello и быстро создать набор масштабирования hello.

* На hello `Basics` колонки, введите имя для набора масштабирования hello. Это имя становится hello базовый hello полное доменное имя подсистемы балансировки нагрузки hello перед hello масштабного набора, поэтому убедитесь, hello имя является уникальным среди всех Azure.
* Выберите нужный тип ОС, введите имя пользователя и выберите тип проверки подлинности. Если вы выберите пароль, он должен быть не короче 12 символов и удовлетворять трех из четырех следующих требованиям сложности hello: одну строчную букву, одну прописную букву, одну цифру и один специальный символ. См. дополнительные сведения о [требованиях к имени пользователя и паролю](../virtual-machines/windows/faq.md#what-are-the-username-requirements-when-creating-a-vm). При выборе `SSH public key`, быть вставить tooonly убедиться, что открытый ключ, не закрытого ключа:

![ScaleSetPortalBasics](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalBasics.PNG)

* Выберите, будет ли вы, как задать масштаб hello toolimit tooa размещения одной группы или, что оно должно охватывать несколько групп для размещения. Разрешение hello в наборе toospan размещение групп позволяет использовать для масштабирования задает более 100 виртуальных машин в емкости (вверх too1 000) с некоторыми ограничениями. Дополнительные сведения см. в этой [документации](./virtual-machine-scale-sets-placement-groups.md).
* Введите имя и расположение нужной группы ресурсов и щелкните `OK`.
* На hello `Virtual machine scale set service settings` колонки: Введите имя метки нужный домен (основание hello hello полное доменное имя для подсистемы балансировки нагрузки hello перед hello масштабный набор). Эта метка должна быть уникальной в Azure.
* Выберите образ диска требуемой операционной системы, число экземпляров и размер виртуальной машины.
* Выберите нужный тип диска: управляемый или неуправляемый. Дополнительные сведения см. в этой [документации](./virtual-machine-scale-sets-managed-disks.md). Если вы выбрали toohave hello масштабный набор охватывать несколько групп размещения, этот параметр недоступен, так как требуется для групп размещения toospan наборы масштабирования управляемого диска.
* Включите или отключите автомасштабирование и настройте его (если включено):

![ScaleSetPortalService](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalService.PNG)

* На hello `Summary` колонки, по завершении проверки нажмите кнопку `OK` toostart hello в наборе развертывания.


## <a name="connect-tooa-vm-in-hello-scale-set"></a>Подключение tooa виртуальной Машины в наборе масштабирования hello
Если вы выбрали toolimit шкала задайте tooa размещения одной группы, а затем набор масштабирования hello развертывается в составе подключения легко наборе масштабирования toohello toolet настроены правила NAT (если нет, tooconnect toohello виртуальных машин на шкале hello, вы скорее всего, потребуется toocreate jumpbox в hello hello масштабный набор же виртуальной сети). toosee их, перейдите toohello `Inbound NAT Rules` вкладка hello подсистемы балансировки нагрузки для набора масштабирования hello:

![ScaleSetPortalNatRules](./media/virtual-machine-scale-sets-portal-create/ScaleSetPortalNatRules.PNG)

Tooeach набора виртуальных Машин, на шкале hello, с помощью этих правил NAT можно подключиться. Для экземпляра для набора масштабирования Windows, если правило NAT на входящий порт 50000, пригодных для подключения toothat компьютера с помощью протокола удаленного рабочего СТОЛА на `<load-balancer-ip-address>:50000`. Для набора масштабирования Linux для подключения с помощью команды hello `ssh -p 50000 <username>@<load-balancer-ip-address>`.

## <a name="next-steps"></a>Дальнейшие действия
Документацию по как задает масштаб toodeploy из hello CLI см. в разделе [этой документации](virtual-machine-scale-sets-cli-quick-create.md).

Документацию по как задает масштаб toodeploy из PowerShell, в разделе [этой документации](virtual-machine-scale-sets-windows-create.md).

Документацию по каким образом задает масштаб toodeploy из Visual Studio, в разделе [этой документации](virtual-machine-scale-sets-vs-create.md).

Общие документацию извлечь hello [документации страница общих сведений для набора масштабирования](virtual-machine-scale-sets-overview.md).

Для получения общих сведений посетите hello [Главная целевая страница для набора масштабирования](https://azure.microsoft.com/services/virtual-machine-scale-sets/).

