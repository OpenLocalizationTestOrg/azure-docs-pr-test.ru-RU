---
title: "aaaUpload VHD-файл tooAzure DevTest Labs, с помощью обозревателя хранилищ Microsoft Azure | Документы Microsoft"
description: "Отправка toolab файл виртуального жесткого диска учетной записи хранилища с помощью обозревателя хранилищ Microsoft Azure"
services: devtest-lab,virtual-machines
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: 
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/10/2017
ms.author: tarcher
ms.openlocfilehash: 686691e3676cea4b2d7cd8bf045bc43a792c667e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-vhd-file-toolabs-storage-account-using-microsoft-azure-storage-explorer"></a>Отправка toolab файл виртуального жесткого диска учетной записи хранилища с помощью обозревателя хранилищ Microsoft Azure

[!INCLUDE [devtest-lab-upload-vhd-selector](../../includes/devtest-lab-upload-vhd-selector.md)]

В Azure DevTest Labs VHD-файлы могут быть используется toocreate пользовательские образы, которые являются tooprovision используемых виртуальных машин. В этой статье показано, как toouse [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) учетная запись хранения лаборатории tooa файлов tooupload виртуального жесткого диска. После отправки вашего VHD-файла, hello [дальнейшие действия раздела](#next-steps) перечислены некоторые статей, которые показывают, как toocreate пользовательского образа из hello отправили файл виртуального жесткого диска. См. дополнительные сведения [о дисках и виртуальных жестких дисках для виртуальных машин Azure](../virtual-machines/linux/about-disks-and-vhds.md).

## <a name="step-by-step-instructions"></a>Пошаговые инструкции

Здравствуйте следующие обход действия можно выполнить с помощью Отправка VHD файлов tooDevTest лаборатории с использованием [Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md).

1. [Загрузите и установите последнюю версию Microsoft Azure Storage Explorer hello hello](http://www.storageexplorer.com).

1. Получите имя hello hello лаборатории учетной записи хранилища с помощью портала Azure hello:

    1. Войдите в toohello [портал Azure](http://go.microsoft.com/fwlink/p/?LinkID=525040).
    
    1. Выберите **дополнительные службы**, а затем выберите **DevTest Labs** из списка hello.
    
    1. Выберите из списка hello лабораториям hello требуемой лаборатории.  
    
    1. В колонке hello лаборатории выберите **конфигурации**. 
    
    1. В лаборатории hello **конфигурации** колонке выберите **пользовательских изображений (VHD)**.
    
    1. На hello **пользовательских образов** колонке выберите **+ добавить**. 
    
    1. На hello **настраиваемое изображение** колонке выберите **VHD**.
    
    1. На hello **VHD** колонке выберите **отправить VHD с помощью PowerShell**.
    
        ![Отправка VHD с помощью PowerShell][0]
    
    1. Hello **отправить изображение с помощью PowerShell** колонке отображает toohello вызов **Add-AzureVhd** командлета. Здравствуйте, первый параметр (*назначения*) содержит имя учетной записи хранения hello лаборатории hello в hello следующий формат:
    
        https://<имя_учетной_записи_хранения>.blob.core.windows.net/uploads/... 

    1. Запишите имя учетной записи хранения hello как он используется в последующих шагах.
    
1. Подключите tooan учетной записи подписки Azure, с помощью обозревателя хранилищ.

    > [!TIP] 
    > 
    > Обозреватель хранилищ поддерживает несколько вариантов подключения. В этом разделе рассмотрены подключения учетную запись хранения tooa, связанную с подпиской Azure. toosee hello другие параметры соединения, поддерживаемые обозреватель хранилищ см. в статье toohello [Приступая к работе с обозреватель хранилищ](../vs-azure-tools-storage-manage-with-storage-explorer.md).
 
    1. Откройте обозреватель хранилищ.
    
    1. В обозревателе хранилищ выберите раздел **Параметры учетной записи Azure**. 
    
        ![Параметры учетной записи Azure][1]
    
    1. Hello левая панель содержит учетные записи Microsoft hello, вход в систему. Учетная запись tooconnect tooanother, выберите **добавить учетную запись**и выполните toosign hello диалоговых окон, учетную запись Майкрософт, связанный с по крайней мере одну подписку Azure.
    
        ![Добавить учетную запись][2]
    
    1. После успешной регистрации вход с учетной записью Microsoft hello левой заполняет hello Azure подписок, связанных с этой учетной записи. Здравствуйте, выберите подписки Azure, с которыми вы хотите toowork, а затем выберите **применить**. (При выборе **все подписки** переключает hello выделение всех или ни один из hello в списке подписок Azure.)
    
        ![Выбор подписок Azure][3]
    
    1. Hello левая панель отображает связанные с подписками Azure hello выбранные учетные записи хранения hello.
    
        ![Выбранные подписки Azure][4]

1. Найдите учетную запись хранения лаборатории hello:

    1. В левой панели проводника хранилищ hello найдите и разверните узел hello hello подписки Azure, которой принадлежит hello лаборатории.
    
    1. Разверните узел подписки hello **учетные записи хранения**.

    1. Разверните узлы tooreveal узел учетной записи хранилища hello лаборатории для **контейнеров больших двоичных объектов**, **общие файловые ресурсы**, **очереди**, и **таблиц**.
    
    1. Разверните hello **контейнеров больших двоичных объектов** узла.
    
    1. Выберите toodisplay контейнер больших двоичных объектов передачи hello его содержимое в правой области hello.
        
        ![Каталог для отправки][5]

1. Отправьте VHD-файл hello, с помощью обозревателя хранилищ:

    1. В правой панели обозревателя хранилищ hello, вы увидите список больших двоичных объектов hello в hello **отправляет** контейнер BLOB-объектов учетной записи хранения hello лаборатории. На панели инструментов редактора hello больших двоичных объектов, выберите **отправки** 
        
        ![Кнопка "Отправить"][6]
    
    1. Из hello **отправить** раскрывающееся меню, выберите **Отправка файлов...** .
    
    1. На hello **передачи файлов** диалоговое окно, выберите hello кнопку с многоточием.
        
        ![Выбор файла][8]  

    1. На hello **tooupload выберите файлов** диалогового окна обзора toohello требуемого файла виртуального жесткого диска, выберите его, а затем выберите **откройте**.
    
    1. При вернул toohello **передачи файлов** диалогового окна, изменение **больших двоичных объектов типа** слишком**страничного большого двоичного объекта**.
    
    1. Щелкните **Отправить**.

        ![Выбор файла][9]  
    
    1. Обозреватель хранилищ Hello **журнал действий** области отображается состояние загрузки hello (а также отправить hello toocancel ссылки). Hello процесс передачи файла виртуального жесткого диска может быть длительное время, в зависимости от размера hello hello VHD-файл и скорость подключения. 

        ![Статус отправки файлов][10]  

## <a name="next-steps"></a>Дальнейшие действия

- [Создание пользовательского образа в Azure DevTest Labs файла виртуального жесткого диска с помощью портала Azure hello](devtest-lab-create-template.md)
- [Создание пользовательского образа из VHD-файла с помощью PowerShell](devtest-lab-create-custom-image-from-vhd-using-powershell.md)

[0]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-image-using-psh.png
[1]: ./media/devtest-lab-upload-vhd-using-storage-explorer/settings-icon.png
[2]: ./media/devtest-lab-upload-vhd-using-storage-explorer/add-account-link.png
[3]: ./media/devtest-lab-upload-vhd-using-storage-explorer/subscriptions-list.png
[4]: ./media/devtest-lab-upload-vhd-using-storage-explorer/storage-accounts-list.png
[5]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-dir.png
[6]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-button.png
[7]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-files.png
[8]: ./media/devtest-lab-upload-vhd-using-storage-explorer/select-file.png
[9]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-file.png
[10]: ./media/devtest-lab-upload-vhd-using-storage-explorer/upload-status.png
