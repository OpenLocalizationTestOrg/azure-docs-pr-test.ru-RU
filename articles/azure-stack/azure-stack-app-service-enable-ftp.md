---
title: "aaaEnable FTP в службе приложений Azure стек | Документы Microsoft"
description: "Действия toocomplete tooenable FTP в службе приложений Azure стеке"
services: azure-stack
documentationcenter: 
author: apwestgarth
manager: stefsch
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: app-service
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 4/6/2017
ms.author: anwestg
ms.openlocfilehash: 9c02da6362085fdd9f8d285da04efe85cf352398
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="enable-ftp-in-app-service-on-azure-stack"></a>Включение FTP в службе приложений в Azure Stack

После успешного развертывания службы приложений Azure стек при желании публикации tooenable FTP, чтобы клиенты можно отправить свои файлы приложения и содержимого, существуют некоторые дополнительные действия, требующие toobe завершена.  В будущих выпусках эти действия будут выполняться автоматически.

> [!NOTE]
> Эти шаги должен выполнить администратор службы или предприятия, чтобы настроить службу приложения в поставщике ресурсов Azure Stack.

## <a name="enable-ftp"></a>Включение FTP

1.  Войдите в портал Azure стека toohello под Здравствуйте, администратор службы.
2.  Обзор слишком**сетевых интерфейсов** и выберите hello **FTP-NIC** под **группы ресурсов** - **AppService локальной**. ![Сетевые интерфейсы Azure Stack][1]
3.  Примечание hello **общедоступный IP-адрес** из hello **FTP-NIC**. 
![Сведения о сетевом интерфейсе Azure Stack][2]
4.  Затем найдите слишком**виртуальные машины** и выберите hello **FTP0 ВМ**. ![Виртуальные машины Azure Stack][3]
5.  Откройте сеанс удаленного рабочего стола toohello виртуальной Машины с помощью hello **Connect** сеанса toohello кнопки и входа в систему с использованием учетных данных администратора hello, заданным во время развертывания службы приложений.  
![Сведения о виртуальных машинах Azure Stack][4]
6.  Откройте **Диспетчер Internet Information Service (IIS)** на hello FTP виртуальной Машины (VM для FTP0).
7.  В разделе **Sites** (Узлы) выберите **Hosting FTP Site** (Размещение узла FTP).
8.  Щелкните **FTP Firewall Support** (Поддержка брандмауэра FTP). ![Диспетчер служб IIS на виртуальной машине FTP0-VM][5]
9.  Введите hello общедоступный IP-адрес FTP-NIC hello и нажмите кнопку **применить** ![поддержка брандмауэра FTP диспетчера IIS][6]

## <a name="validate-hello-enabling-of-ftp"></a>Проверка включения hello FTP

1.  Войдите в toohello портала Azure стека либо hello администратором службы или клиента.
2.  Обзор слишком**службы приложений** и выберите Web, мобильных или создания приложения API. ![Службы приложений][7]
3.  В приложении hello сведения Обратите внимание hello **имя узла FTP** и **имя пользователя FTP или развертывание**. ![Сведения о приложении службы приложений][8]
> [!NOTE]
> Если вы не видите запись под **имя пользователя FTP или развертывание**, необходимо иметь учетные данные развертывания tooset hello предварительного использования hello **учетные данные развертывания** колонку.

4.  Откройте проводник Windows, введите имя узла hello FTP в файл hello в адресной строке, например ftp://ftp.appservice.azurestack.local
5.  При появлении запроса введите hello **учетные данные развертывания** записанное на шаге 3, если была включена функция hello вы увидите список каталогов содержимое приложения для hello приложения службы. ![Список файлов FTP][9]
<!--Image references-->
[1]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interfaces.png
[2]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-network-interface-details.png
[3]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines.png
[4]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-virtual-machines-FTP0-VM.png
[5]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager.png
[6]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-IIS-Manager-FTP-Firewall-Support.png
[7]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-services.png
[8]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-app-service-app-detail.png
[9]: ./media/azure-stack-app-service-enable-ftp/azure-stack-app-service-enable-ftp-validate-ftp-file-listing.png
