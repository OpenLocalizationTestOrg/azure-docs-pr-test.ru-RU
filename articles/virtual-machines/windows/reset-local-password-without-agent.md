---
title: "aaaReset локальный пароль Windows без агента Azure | Документы Microsoft"
description: "Как tooreset hello пароль локальной учетной записи пользователя Windows, когда hello Azure гостевой агент не установлен или не работает на виртуальной Машине"
services: virtual-machines-windows
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.assetid: cf353dd3-89c9-47f6-a449-f874f0957013
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/07/2017
ms.author: iainfou
ms.openlocfilehash: c559c31ea142f9cf50d2c5b6182c5355fec9bac5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooreset-local-windows-password-for-azure-vm"></a>Как tooreset локальный пароль Windows для виртуальной Машины Azure
Вы можете сбросить пароль локального Windows hello виртуальной машины в Azure с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) предоставляемых установлен агент Azure guest hello. Этот метод является основным способом hello tooreset пароль для виртуальной Машины Azure. При возникновении проблем с hello гостевой агент Azure не отвечает, было пройдено tooinstall после отправки пользовательского образа, можно вручную сбросить пароль Windows. В этой статье указаны как tooreset пароль локальной учетной записи путем присоединения hello tooanother виртуального диска исходной операционной системы виртуальной Машины. 

> [!WARNING]
> Этот метод следует использовать только в крайнем случае. По возможности используйте tooreset пароля с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) первой.
> 
> 

## <a name="overview-of-hello-process"></a>Общие сведения о процессе hello
Hello основные действия по выполнению локальный пароль, сброс для виртуальной Машины Windows в Azure, если отсутствует агент Azure guest toohello доступа выглядит следующим образом:

* Удалите hello исходной виртуальной Машины. виртуальные диски Hello сохраняются.
* Присоединение tooanother диска ОС ВМ источника hello виртуальной Машины на hello местоположения в подписке Azure. Эта VM является ссылка tooas hello, устранение неполадок виртуальной Машины.
* С помощью hello, устранение неполадок виртуальной Машины, создайте некоторые файлы конфигурации на диске операционной системы виртуальной Машины источника hello.
* Отсоедините диск операционной системы виртуальной Машины hello от hello, устранение неполадок виртуальной Машины.
* Используйте toocreate шаблона диспетчера ресурсов виртуальной Машины, с помощью hello исходный виртуальный диск.
* При hello новой виртуальной Машины загружается, hello файлов конфигурации вы создаете обновления hello пароля пользователя требуется hello.

## <a name="detailed-steps"></a>Подробные инструкции
По возможности используйте tooreset пароля с помощью hello [портал Azure или Azure PowerShell](reset-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) перед попыткой hello следующие шаги. Прежде чем начать, обязательно сохраните резервную копию виртуальной машины. 

1. Удалить hello затронутых ВМ на портале Azure. Удаление hello ВМ только удаляет метаданные hello, ссылку на hello hello ВМ в Azure. виртуальные диски Hello сохраняются при удалении hello виртуальной Машины:
   
   * Выберите hello виртуальной Машины в hello портала Azure щелкните *удалить*:
     
     ![Удаление существующей виртуальной машины](./media/reset-local-password-without-agent/delete_vm.png)
2. Присоедините диск toohello hello исходной Виртуальной машины операционной системы, устранение неполадок виртуальной Машины. Привет, устранение неполадок виртуальной Машины должны находиться в hello же регионе, что диск операционной системы виртуальной Машины источника hello (такие как `West US`):
   
   * Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure. Щелкните *Диски* | *Подключить существующий*:
     
     ![Подключение существующего диска](./media/reset-local-password-without-agent/disks_attach_existing.png)
     
     Выберите *VHD-файл* и выберите учетную запись хранилища hello, который содержит источник виртуальной Машины:
     
     ![Выбор учетной записи хранения](./media/reset-local-password-without-agent/disks_select_storageaccount.PNG)
     
     Выберите исходный контейнер hello. обычно является Hello исходный контейнер *виртуальные жесткие диски*:
     
     ![Выбор контейнера хранилища](./media/reset-local-password-without-agent/disks_select_container.png)
     
     Выберите tooattach виртуального жесткого диска ОС hello. Нажмите кнопку *выберите* toocomplete hello процесс:
     
     ![Выбор исходного виртуального диска](./media/reset-local-password-without-agent/disks_select_source_vhd.png)
3. Подключение toohello Устранение неполадок виртуальной Машины с помощью удаленного рабочего стола и убедитесь, что диск операционной системы виртуальной Машины источника hello отображается:
   
   * Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure и нажмите кнопку *Connect*.
   * Откройте файл RDP hello, загрузки. Введите hello пользователя и пароль для hello, устранение неполадок виртуальной Машины.
   * В проводнике найдите диск данных hello присоединенной. Если hello исходный виртуальный жесткий ДИСК Виртуальной машины находится hello toohello диск, подключенный только данные, устранение неполадок виртуальной Машины, он должен быть hello диска «f:»:
     
     ![Просмотр подключенного диска данных](./media/reset-local-password-without-agent/troubleshooting_vm_fileexplorer.png)
4. Создание `gpt.ini` в `\Windows\System32\GroupPolicy` на диске hello исходной Виртуальной машины (если существует gpt.ini, переименуйте toogpt.ini.bak):
   
   > [!WARNING]
   > Убедитесь, что не случайно создать hello следующие файлы в C:\Windows, hello диска ОС для hello, устранение неполадок виртуальной Машины. Создайте следующие файлы на диске hello ОС для виртуальной Машины, которой подключен как диск с данными источника hello.
   > 
   > 
   
   * Добавьте следующие строки в hello hello `gpt.ini` созданный файл:
     
     ```
     [General]
     gPCFunctionalityVersion=2
     gPCMachineExtensionNames=[{42B5FAAE-6536-11D2-AE5A-0000F87571E3}{40B6664F-4972-11D1-A7CA-0000F87571E3}]
     Version=1
     ```
     
     ![Создание файла gpt.ini](./media/reset-local-password-without-agent/create_gpt_ini.png)
5. Создайте файл `scripts.ini` в расположении `\Windows\System32\GroupPolicy\Machine\Scripts`. Убедитесь, что отображаются скрытые папки. При необходимости создайте hello `Machine` или `Scripts` папки.
   
   * Добавьте следующие строки hello hello `scripts.ini` созданный файл:
     
     ```
     [Startup]
     0CmdLine=C:\Windows\System32\FixAzureVM.cmd
     0Parameters=
     ```
     
     ![Создание файла scripts.ini](./media/reset-local-password-without-agent/create_scripts_ini.png)
6. Создание `FixAzureVM.cmd` в `\Windows\System32` с hello следующие содержимое, заменив `<username>` и `<newpassword>` собственными значениями:
   
    ```
    net user <username> <newpassword> /add
    net localgroup administrators <username> /add
    net localgroup "remote desktop users" <username> /add

    ```

    ![Создание файла FixAzureVM.cmd](./media/reset-local-password-without-agent/create_fixazure_cmd.png)
   
    При определении нового пароля hello, должен удовлетворять требованиям к сложности пароля hello настроены для виртуальной Машины.
7. На портале Azure отсоедините диск hello от hello, устранение неполадок виртуальной Машины:
   
   * Выберите hello, устранение неполадок виртуальной Машины в hello портал Azure, щелкните *дисков*.
   * Диск данных выберите hello присоединенные на шаге 2, нажмите кнопку *отсоединения*:
     
     ![Отключение диска](./media/reset-local-password-without-agent/detach_disk.png)
8. Перед созданием виртуальной Машины, получите исходный диск hello URI tooyour ОС:
   
   * Выберите hello учетной записи хранилища в hello портала Azure щелкните *большие двоичные объекты*.
   * Выберите контейнер hello. обычно является Hello исходный контейнер *виртуальные жесткие диски*:
     
     ![Выбор большого двоичного объекта учетной записи хранения](./media/reset-local-password-without-agent/select_storage_details.png)
     
     Выберите источник виртуального жесткого диска операционной системы виртуальной Машины и нажмите кнопку hello *копирования* кнопку Далее toohello *URL-адрес* имя:
     
     ![Копирование URI диска](./media/reset-local-password-without-agent/copy_source_vhd_uri.png)
9. Создайте виртуальную Машину с диска ОС ВМ hello источника:
   
   * Используйте [этого шаблона Azure Resource Manager](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-specialized-vhd) toocreate ВМ с специализированные виртуального жесткого диска. Нажмите кнопку hello `Deploy tooAzure` кнопку tooopen hello портал Azure с подробными сведениями шаблонного hello, заполняется автоматически.
   * Tooretain все предыдущие настройки hello для hello виртуальной Машины, установите *изменить шаблон* tooprovide существующей виртуальной сети, подсети, сетевой адаптер или общедоступный IP-адрес.
   * В hello `OSDISKVHDURI` текстовом поле параметра, вставить hello в предшествующих шаг hello получить URI источника данных виртуального жесткого диска:
     
     ![Создание виртуальной машины на основе шаблона](./media/reset-local-password-without-agent/create_new_vm_from_template.png)
10. После hello, Новая виртуальная машина запущена, соединения toohello виртуальную Машину с помощью удаленного рабочего стола с hello новый пароль, указанный в hello `FixAzureVM.cmd` сценария.
11. Из вашего toohello удаленный сеанс новой виртуальной Машины, удалите hello следующие файлы tooclean hello среды:
    
    * Из расположения %windir%\System32
      * удалите файл FixAzureVM.cmd.
    * Из расположения %windir%\System32\GroupPolicy\Machine\
      * удалите файл scripts.ini.
    * Из расположения %windir%\System32\GroupPolicy
      * Удалите gpt.ini (если существовал gpt.ini и вы переименовали ее toogpt.ini.bak задней toogpt.ini .bak hello файл rename)

## <a name="next-steps"></a>Дальнейшие действия
Если вы по-прежнему не удается подключиться с помощью удаленного рабочего стола, см. раздел hello [по устранению неполадок протокола удаленного рабочего СТОЛА](troubleshoot-rdp-connection.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json). Hello [подробное руководство по устранению неполадок протокола удаленного рабочего СТОЛА](detailed-troubleshoot-rdp.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json) рассматривается устранение неполадок методов, а не конкретные действия. Вы также можете [отправить запрос в службу поддержки Azure](https://azure.microsoft.com/support/options/) и получить практическую помощь.

