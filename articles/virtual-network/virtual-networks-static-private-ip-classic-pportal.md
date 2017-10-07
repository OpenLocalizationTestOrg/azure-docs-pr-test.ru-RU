---
title: "aaaConfigure частных IP-адресов для виртуальных машин (обычная) — портал Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин (классические) с помощью hello портал Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: b8ef8367-58b2-42df-9f26-3269980950b8
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: df4bfa6768fc9e66db89785b633ffdb0274dbc46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-classic-using-hello-azure-portal"></a>Настройка частного IP-адреса для виртуальной машины при помощи hello портал Azure (классические)

[!INCLUDE [virtual-networks-static-private-ip-selectors-classic-include](../../includes/virtual-networks-static-private-ip-selectors-classic-include.md)]

[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello классической модели развертывания. Вы также можете [управление статический частный IP-адрес в модели развертывания диспетчера ресурсов hello](virtual-networks-static-private-ip-arm-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

следующие действия Образец Hello ожидать простой среде уже создан. Требуется toorun hello действия, показанной в этом документе, вначале построить hello тестовой среде, описанной в [создании виртуальной сети](virtual-networks-create-vnet-classic-pportal.md).

## <a name="how-toospecify-a-static-private-ip-address-when-creating-a-vm"></a>Как toospecify статических частных IP-адресов при создании виртуальной Машины
toocreate Виртуальную машину с именем *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet* с статических частного IP-адреса *192.168.1.101*, выполните следующие действия hello.

1. В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.
2. Нажмите кнопку **NEW** > **вычислений** > **Windows Server 2012 R2 Datacenter**, обратите внимание, что hello **выберите модель развертывания** представлен список уже **классический**, а затем нажмите кнопку **создать**.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure01.png)
3. В hello **Создание ВМ** колонки, введите имя hello создан toobe ВМ hello (*DNS01* в нашем сценарии), hello учетной записи локального администратора и пароль.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure02.png)
4. Щелкните **Необязательная конфигурация** > **Сеть** > **Виртуальная сеть**, а затем — **TestVNet**. Если **TestVNet** недоступно, убедитесь, что вы используете hello *центральной части США* расположение и созданы hello тестовой среды, описанные в начале этой статьи hello.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure03.png)
5. В hello **сети** колонки, убедитесь, что hello подсети выбранного в данный момент является *переднего плана*, нажмите кнопку **IP-адреса**в разделе **назначения IP-адресов** щелкните **статических**, а затем введите *192.168.1.101* для **IP-адрес** как показано ниже.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure04.png)    
6. Нажмите кнопку **ОК** в hello **IP-адреса** колонке нажмите кнопку **ОК** в hello **сети** и, при необходимости щелкните **ОК**в hello **необязательная конфигурация** колонку.
7. В hello **Создание ВМ** колонка, щелкните **создать**. Обратите внимание hello Плитка ниже отображаются в панели мониторинга.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure05.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины
tooview hello статических частных IP-адресе для hello виртуальных Машин, созданных с hello указанную выше процедуру, выполните следующие действия hello.

1. На портале Azure Azure hello, нажмите кнопку **ПРОСМОТРЕТЬ все** > **виртуальные машины (классические)** > **DNS01**  >   **Все параметры** > **IP-адреса** и обратите внимание, hello назначения IP-адресов и IP-адрес, как показано ниже.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure06.png)

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Как tooremove статических частных IP-адресов из виртуальной Машины
tooremove hello статический частный IP-адрес из приветствия созданную виртуальную Машину, выполните шаги hello.

1. Из hello **IP-адресов** колонки, показанном выше, нажмите кнопку **динамическое** toohello справа от **назначения IP-адресов**, нажмите кнопку **Сохранить**, а затем Нажмите кнопку **Да**.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-classic-pportal/figure07.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины
tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью hello указанную выше процедуру, следуйте инструкциям hello:

1. Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **статических** toohello справа от **назначения IP-адресов**.
2. Введите *192.168.1.101* в поле **IP-адрес**, нажмите кнопку **Сохранить**, а затем — **Да**.

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

