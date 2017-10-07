---
title: "aaaCreate виртуальную Машину с статический общедоступный IP-адрес - портал Azure | Документы Microsoft"
description: "Узнайте, как toocreate ВМ с статических открытый IP адрес с помощью hello портал Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: e9546bcc-f300-428f-b94a-056c5bd29035
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f74d2132785f06148757409ee0a44b98d1e4b98e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-vm-with-a-static-public-ip-address-using-hello-azure-portal"></a>Создайте виртуальную Машину с помощью hello портал Azure статический общедоступный IP-адрес

> [!div class="op_single_selector"]
> * [Портал Azure](virtual-network-deploy-static-pip-arm-portal.md)
> * [PowerShell](virtual-network-deploy-static-pip-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-network-deploy-static-pip-arm-cli.md)
> * [Шаблон](virtual-network-deploy-static-pip-arm-template.md)
> * [PowerShell (классическая модель)](virtual-networks-reserved-public-ip.md)

[!INCLUDE [virtual-network-deploy-static-pip-intro-include.md](../../includes/virtual-network-deploy-static-pip-intro-include.md)]

> [!NOTE]
> В Azure предлагаются две модели развертывания для создания ресурсов и работы с ними: [модель Resource Manager и классическая модель](../resource-manager-deployment-model.md). В этой статье описан с помощью модели развертывания диспетчера ресурсов hello, который рекомендуется в большинстве случаев новый вместо hello классической модели развертывания.

[!INCLUDE [virtual-network-deploy-static-pip-scenario-include.md](../../includes/virtual-network-deploy-static-pip-scenario-include.md)]

## <a name="create-a-vm-with-a-static-public-ip"></a>Создание виртуальной машины со статическим общедоступным IP-адресом

toocreate виртуальную Машину с статический общедоступный IP-адрес адрес в hello портал Azure завершения hello, следующие шаги:

1. В браузере перейдите toohello [портал Azure](https://portal.azure.com) и, при необходимости, выполнить вход с учетной записью Azure.
2. Щелкните hello верхнем левом углу портала hello, **New**>>**вычислений**>**Windows Server 2012 R2 Datacenter**.
3. В hello **выберите модель развертывания** выберите **диспетчера ресурсов** и нажмите кнопку **создать**.
4. В hello **основы** колонки, введите сведения о hello виртуальной Машины, как показано ниже и нажмите кнопку **ОК**.
   
    ![Портал Azure — основы](./media/virtual-network-deploy-static-pip-arm-portal/figure1.png)
5. В hello **выберите размер** колонка, щелкните **A1 Standard** как показано ниже и нажмите кнопку **выберите**.
   
    ![Портал Azure — выбор размера](./media/virtual-network-deploy-static-pip-arm-portal/figure2.png)
6. В hello **параметры** колонка, щелкните **общедоступный IP-адрес**, затем в hello **создать общедоступный IP-адрес** колонки в разделе **назначения**, нажмите кнопку **Статических** как показано ниже. Затем нажмите **ОК**.
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure3.png)
7. В hello **параметры** колонка, щелкните **ОК**.
8. Просмотрите hello **Сводка** колонки, как показано ниже, а затем щелкните **ОК**.
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure4.png)
9. Обратите внимание, hello новую плитку на панели мониторинга.
   
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure5.png)
10. После создания виртуальной Машины hello hello **параметры** колонке будет отображаться, как показано ниже
    
    ![Портал Azure — создание общедоступного IP-адреса](./media/virtual-network-deploy-static-pip-arm-portal/figure6.png)

