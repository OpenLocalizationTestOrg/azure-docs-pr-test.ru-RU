---
title: "aaaConfigure частных IP-адресов для виртуальных машин - портал Azure | Документы Microsoft"
description: "Узнайте, как tooconfigure частных IP-адресов для виртуальных машин с помощью hello портал Azure."
services: virtual-network
documentationcenter: na
author: jimdial
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 11245645-357d-4358-9a14-dd78e367b494
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/04/2016
ms.author: jdial
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 474161303cdf8cb98e16ffd7cef6b74debdbc49a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-private-ip-addresses-for-a-virtual-machine-using-hello-azure-portal"></a>Настройка частного IP-адреса для виртуальной машины с помощью портала Azure hello

> [!div class="op_single_selector"]
> * [Портал Azure](virtual-networks-static-private-ip-arm-pportal.md)
> * [PowerShell](virtual-networks-static-private-ip-arm-ps.md)
> * [Интерфейс командной строки Azure](virtual-networks-static-private-ip-arm-cli.md)
> * [Портал Azure (классическая модель)](virtual-networks-static-private-ip-classic-pportal.md)
> * [PowerShell (классическая модель)](virtual-networks-static-private-ip-classic-ps.md)
> * [Интерфейс командной строки Azure (классическая модель)](virtual-networks-static-private-ip-classic-cli.md)


[!INCLUDE [virtual-networks-static-private-ip-intro-include](../../includes/virtual-networks-static-private-ip-intro-include.md)]

[!INCLUDE [azure-arm-classic-important-include](../../includes/azure-arm-classic-important-include.md)]

В этой статье рассматриваются hello модели развертывания диспетчера ресурсов. Вы также можете [управление статический частный IP-адрес в hello классической модели развертывания](virtual-networks-static-private-ip-classic-pportal.md).

[!INCLUDE [virtual-networks-static-ip-scenario-include](../../includes/virtual-networks-static-ip-scenario-include.md)]

следующие действия Образец Hello ожидать простой среде уже создан. Требуется toorun hello действия, показанной в этом документе, вначале построить hello тестовой среде, описанной в [создании виртуальной сети](virtual-networks-create-vnet-arm-pportal.md).

## <a name="how-toocreate-a-vm-for-testing-static-private-ip-addresses"></a>Каким образом соответствие toocreate ВМ для тестирования статических частных IP-адресов
Нельзя задать статический частный IP-адрес во время создания виртуальной Машины в режим развертывания диспетчера ресурсов hello hello, используя hello портал Azure. Необходимо сначала создать hello виртуальной Машины, последующей задан его частного IP toobe статический.

Виртуальную машину с именем toocreate *DNS01* в hello *переднего плана* подсети виртуальной сети с именем *TestVNet*, выполните следующие шаги hello.

1. В браузере перейдите toohttp://portal.azure.com и при необходимости выполните вход с помощью учетной записи Azure.
2. Нажмите кнопку **NEW** > **вычислений** > **Windows Server 2012 R2 Datacenter**, обратите внимание, что hello **выберите модель развертывания** представлен список уже **диспетчера ресурсов**, а затем нажмите кнопку **создать**, как показано в приведенном ниже рисунке hello.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure01.png)
3. В hello **основы** колонки, введите имя hello создан toobe ВМ hello (*DNS01* в нашем сценарии), hello учетной записи локального администратора и пароль, как показано на следующем рисунке hello.
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure02.png)
4. Убедитесь, что hello **расположение** выбранный *центральной части США*, нажмите кнопку **выбрать существующий** под **группы ресурсов**, нажмите кнопку **Группы ресурсов** еще раз, нажмите кнопку *TestRG*, а затем нажмите кнопку **ОК**.
   
    ![Колонка «Основные»](./media/virtual-networks-static-ip-arm-pportal/figure03.png)
5. В hello **выберите размер** колонке выберите **A1 Standard**, а затем нажмите кнопку **выберите**.
   
    ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure04.png)    
6. В **параметры** колонки, убедитесь, что hello следующие свойства задаются задаются со значениями hello и нажмите кнопку **ОК**.
   
    -**Учетная запись**: *vnetstorage*
   
   * **Сеть**: *TestVNet*
   * **Подсеть**: *FrontEnd*
     
     ![Колонка «Выбор размера»](./media/virtual-networks-static-ip-arm-pportal/figure05.png)     
7. В hello **Сводка** колонка, щелкните **ОК**. Обратите внимание hello Плитка ниже отображаются в панели мониторинга.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure06.png)

## <a name="how-tooretrieve-static-private-ip-address-information-for-a-vm"></a>Как статических частных IP-tooretrieve адресов сведения для виртуальной Машины
tooview hello статических частных IP-адресе для hello виртуальных Машин, созданных с hello указанную выше процедуру, выполните следующие действия hello.

1. На портале Azure Azure hello, нажмите кнопку **ПРОСМОТРЕТЬ все** > **виртуальные машины** > **DNS01** > **все Параметры** > **сетевых интерфейсов** и выберите только сетевой интерфейс hello в списке.
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure07.png)
2. В hello **сетевой интерфейс** колонке нажмите кнопку **все параметры** > **IP-адреса** и hello уведомление **назначения** и **IP-адрес** значения.
   
    ![Элемент «Развертывание виртуальной машины»](./media/virtual-networks-static-ip-arm-pportal/figure08.png)

## <a name="how-tooadd-a-static-private-ip-address-tooan-existing-vm"></a>Как tooadd статический частных IP-адрес решения tooan существующей виртуальной Машины
tooadd статические частного IP адрес toohello виртуальной Машины, созданной с помощью hello указанную выше процедуру, следуйте инструкциям hello:

1. Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **статических** под **назначения**.
2. Введите *192.168.1.101* в поле **IP-адрес**, а затем нажмите кнопку **Сохранить**.
   
    ![Создание виртуальной машины на портале Azure](./media/virtual-networks-static-ip-arm-pportal/figure09.png)

> [!NOTE]
> Если после нажатия кнопки **Сохранить** Обратите внимание, что назначение hello по-прежнему задано слишком**динамическое**, это означает, что IP-адрес hello, вы ввели уже используется. Попробуйте другой IP-адрес.
> 
> 

## <a name="how-tooremove-a-static-private-ip-address-from-a-vm"></a>Как tooremove статических частных IP-адресов из виртуальной Машины
tooremove hello статический частный IP-адрес из приветствия созданную виртуальную Машину, выполните даст hello.

Из hello **IP-адреса** колонки, показанном выше, нажмите кнопку **динамическое** под **назначения**и нажмите кнопку **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
* Ознакомьтесь с информацией о [зарезервированных общедоступных IP-адресах](virtual-networks-reserved-public-ip.md) .
* Узнайте об [общедоступных IP-адресах уровня экземпляра (ILPIP)](virtual-networks-instance-level-public-ip.md) .
* Обратитесь к hello [зарезервированные интерфейсы REST API](https://msdn.microsoft.com/library/azure/dn722420.aspx).

