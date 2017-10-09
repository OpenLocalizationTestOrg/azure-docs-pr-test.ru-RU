---
title: "aaaHow перенаправления USB-устройства в Azure RemoteApp? | Документация Майкрософт"
description: "Узнайте, как toouse перенаправления для USB-устройства в Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: 191d98af-2f5a-4307-9042-aae0e4049f9f
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 661b90c0910167d76ac3886b5af7a32d00b3943f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-redirect-usb-devices-in-azure-remoteapp"></a>Перенаправление USB-устройств в удаленном приложении Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Перенаправление устройств позволяет пользователям использовать компьютера tootheir присоединенные устройства USB hello или планшет с приложениями hello в Azure RemoteApp. Например если общие Скайп через Azure RemoteApp, вашим пользователям требуется может toouse toobe их камеры устройства.

Прежде чем продолжить, убедитесь, что прочитать сведения о перенаправлении USB hello в [использование перенаправления в Azure RemoteApp](remoteapp-redirection.md). Однако hello рекомендуется nusbdevicestoredirect:s: * не будет работать для веб-камер USB и могут не работать некоторые принтеры USB или многофункциональные устройства USB. Намеренно и в целях безопасности hello Azure RemoteApp администратор tooenable перенаправления GUID класса устройства или устройства идентификатор экземпляра, прежде чем пользователи могут использовать эти устройства.

Несмотря на то, что в данной статье рассмотрен web камеры перенаправления, можно использовать аналогичный принтеры USB tooredirect подход и многофункциональные другие USB-устройства, не будут перенаправляться по hello **nusbdevicestoredirect:s:*** команды.

## <a name="redirection-options-for-usb-devices"></a>Параметры перенаправления для USB-устройств
Azure RemoteApp использует очень похожими механизмами для перенаправления USB-устройства, как hello те, которые доступны для служб удаленных рабочих столов. Hello базовая технология позволяет выбрать метод hello правильные перенаправления для данного устройства, tooget hello наиболее обоих высокого уровня и перенаправление устройства RemoteFX USB, с помощью hello **usbdevicestoredirect:s:** команды. Существует четыре элемента toothis команды:

| Порядок обработки | Параметр | Описание |
| --- | --- | --- |
| 1 |* |Выбирает все устройства, которые не выбраны перенаправлением высокого уровня. Примечание: * намеренно не работает для веб-камер USB. |
| {Device class GUID} |Выбирает все устройства, которые соответствуют hello указан класс установки устройства. | |
| USB\InstanceID |Выбирает устройство USB, указанное для hello заданному идентификатору экземпляра. | |
| 2 |-USB\Instance ID |Удаляет параметры перенаправления hello для заданного устройства hello. |

## <a name="redirecting-a-usb-device-by-using-hello-device-class-guid"></a>Перенаправление USB-устройство с помощью GUID класса устройства hello
Существует два способа toofind hello устройства класс GUID, который может использоваться для перенаправления. 

Hello первый вариант — toouse hello [доступные классы установки устройств системных tooVendors](https://msdn.microsoft.com/library/windows/hardware/ff553426.aspx). Выберите класс hello, наиболее точно соответствующий hello устройства вложенного toohello локального компьютера. Для цифровых камер это может быть класс устройств обработки изображений или класс устройств видеозахвата. Вам потребуется toodo некоторые эксперимент с hello устройства классы toofind hello правильный класс GUID, который работает с локально hello присоединен USB-устройство (в наш веб-камеры вариантов hello).

Лучший способ или второй параметр hello, является toofollow GUID класса эти toofind действия hello конкретного устройства:

1. Откройте диспетчер устройств hello, найдите hello устройство, которое будет перенаправлен и щелкните его правой кнопкой мыши и откройте свойства hello.
   ![Привет открыть диспетчер устройств](./media/remoteapp-usbredir/ra-devicemanager.png)
2. На hello **сведения** выберите свойство hello **Guid класса**. значение Hello, появляющийся — hello GUID класса для данного типа устройства.
   ![Свойства камеры](./media/remoteapp-usbredir/ra-classguid.png)
3. Используйте устройства tooredirect значение Guid класса hello, совпадающие с ней.

Например:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s:<Class Guid value>"

Можно объединить несколько перенаправлений устройства в hello того же командлета. Например: tooredirect локальное хранилище и USB-устройство веб-камеры, командлет выглядит следующим образом:

        Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "drivestoredirect:s:*`nusbdevicestoredirect:s:<Class Guid value>"

При установке перенаправление устройств классом GUID перенаправляются все устройства, которые соответствуют, что GUID класса hello указанную коллекцию. Например, при наличии нескольких компьютеров в локальной сети hello, имеющих hello же веб-камер USB, выполнением tooredirect одного командлета все hello веб-камеры.

## <a name="redirecting-a-usb-device-by-using-hello-device-instance-id"></a>Перенаправление с помощью идентификатора экземпляра hello устройства USB-устройство
Если требуется более точное управление, а необходимо toocontrol перенаправление на устройство, можно использовать hello **USB\InstanceID** параметр перенаправления.

сложная часть Hello этот метод находит экземпляр кода hello устройства USB. Компьютер toohello и hello определенным USB-устройством будет иметь доступа. Затем выполните следующие действия.

1. Включение перенаправления hello в сеансе удаленного рабочего стола, как описано в [использование устройства и ресурсы в сеансе удаленного рабочего стола?](http://windows.microsoft.com/en-us/windows7/How-can-I-use-my-devices-and-resources-in-a-Remote-Desktop-session)
2. Откройте подключение к удаленному рабочему столу и щелкните **Показать параметры**.
3. Нажмите кнопку **сохранение** toosave hello текущего подключения параметры tooan RDP-файл.  
    ![Сохранить параметры hello в виде файла RDP](./media/remoteapp-usbredir/ra-saveasrdp.png)
4. Выберите имя файла и расположение, например MyConnection.rdp и этот PC\Documents и сохраните файл hello.
5. Откройте hello MyConnection.rdp файл в текстовом редакторе и найдите идентификатор экземпляра hello hello устройства требуется tooredirect.

Теперь можно используйте идентификатор экземпляра hello в hello, выполнив командлет:

    Set-AzureRemoteAppCollection -CollectionName <collection name> -CustomRdpProperty "nusbdevicestoredirect:s: USB\<Device InstanceID value>"



### <a name="help-us-help-you"></a>Помогите нам помочь вам
Знали ли вы, что в toorating сложения в этой статье и создания примечаний вниз ниже, можно внести самой статье toohello изменения? Чего-то не хватает? Что-то неправильно? Что-то изложено непонятно? Прокрутка вверх и нажмите кнопку **изменить на GitHub** изменения toomake - те поступит toous для просмотра и, когда мы выйдите из системы на них, вы увидите, изменения и усовершенствования здесь.

