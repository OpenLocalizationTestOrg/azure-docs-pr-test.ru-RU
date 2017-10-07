---
title: "aaaUnderstand общих IP-адресов в Azure DevTest Labs | Документы Microsoft"
description: "Узнайте, как Azure DevTest Labs использует общий IP адресов toominimize hello открытый IP адресов требуется tooaccess лаборатории виртуальных машин."
services: devtest-lab
documentationcenter: na
author: camsoper
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/16/2017
ms.author: casoper
ms.openlocfilehash: 8756410117a9d550d567d372174bf1ea96703c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="understand-shared-ip-addresses-in-azure-devtest-labs"></a>Общие IP-адреса в Azure DevTest Labs

Позволяет лаборатории Azure DevTest Labs виртуальные машины общую папку hello же открытый IP-адрес toominimize hello номер открытого IP адресов требуется tooaccess лабораторной отдельных виртуальных машин.  В этой статье описывается принцип работы общих IP-адресов и варианты их настройки.

## <a name="shared-ip-setting"></a>Настройка общих IP-адресов

Когда создается лаборатория, она размещается в подсети виртуальной сети.  По умолчанию, созданными данной подсети **включить общую общедоступный IP-адрес** значение слишком*Да*.  Эта конфигурация создает один общий IP-адрес для hello всей подсети.  Дополнительные сведения о настройке виртуальных сетей и подсетей см. в статье [Настройка виртуальной сети в Azure DevTest Labs](devtest-lab-configure-vnet.md).

![Создание подсети лаборатории](media/devtest-lab-shared-ip/lab-subnet.png)

Вы можете включить этот параметр для всех имеющихся лабораторий, выбрав **Configuration and Policies (Конфигурация и политики) > Virtual Networks (Виртуальные сети)**. Затем выберите виртуальную сеть из списка hello и выберите **ВКЛЮЧИТЬ общие ОБЩЕДОСТУПНЫЙ IP-адрес** для выбранной подсети. Если вы не хотите tooshare общедоступный IP-адрес через лаборатории виртуальных машин, можно также отключить этот параметр в любой лаборатории.

Все виртуальные машины, созданные в этой лаборатории по умолчанию toousing имеет общий IP-адрес.  При создании виртуальной Машины hello, этот параметр можно наблюдать в hello **Дополнительные параметры** колонке под **конфигурацию IP-адресов**.

![Создание виртуальной машины](media/devtest-lab-shared-ip/new-vm.png)

- **Общий.** Все виртуальные машины, созданные в качестве **общедоступных**, помещаются в одну группу ресурсов. Один IP-адрес, назначенный для этой группы Маршрутизации и все виртуальные машины в hello RG будет использовать этот IP-адрес.
- **Общедоступный.** Каждая созданная виртуальная машина имеет личный IP-адрес и создается в собственной группе ресурсов.
- **Частный.** Каждая созданная виртуальная машина использует частный IP-адрес. Не будет возможности tooconnect toothis виртуальную Машину непосредственно из hello Интернета с помощью удаленного рабочего стола.

Виртуальную Машину с общего IP включен при добавлении toohello подсети, DevTest Labs автоматически добавляет подсистему балансировки нагрузки tooa ВМ hello и назначает номер TCP-порта на hello общедоступный IP-адрес пересылки toohello RDP-порту на hello виртуальной Машины.  

## <a name="using-hello-shared-ip"></a>Использование hello общих IP

- **Пользователи Linux:** toohello SSH виртуальной Машины с помощью hello IP-адрес или полное доменное имя, за которым следует двоеточие, следуют hello порта. Например, ниже рисунке hello, hello RDP адресов toohello tooconnect виртуальная машина — `doclab-lab13998814308000.centralus.cloudapp.azure.com:51686`.

  ![Пример виртуальной машины](media/devtest-lab-shared-ip/vm-info.png)

- **Пользователи Windows:** выберите hello **Connect** кнопку hello Azure портала toodownload предварительно настроенных RDP-файл и получить доступ к hello виртуальной Машины.

## <a name="next-steps"></a>Дальнейшие действия

* [Управление всеми политиками лаборатории в Azure DevTest Labs](devtest-lab-set-lab-policy.md)
* [Настройка виртуальной сети в Azure DevTest Labs](devtest-lab-configure-vnet.md)





