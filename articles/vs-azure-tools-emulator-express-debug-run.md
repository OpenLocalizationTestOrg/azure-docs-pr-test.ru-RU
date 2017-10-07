---
title: "Emulator Express toorun aaaUsing и отладки Azure облачной службы на локальном компьютере | Документы Microsoft"
description: "С помощью Emulator Express toorun и отладки облачной службы на локальном компьютере"
services: visual-studio-online
documentationcenter: n/a
author: kraigb
manager: ghogen
editor: 
ms.assetid: 73108f98-a552-4817-b7a1-551367b71906
ms.service: visual-studio-online
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: d89a0fc2dce42b4a2d2f93f9c4ff0482af924ad4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-emulator-express-toorun-and-debug-an-azure-cloud-service-on-a-local-machine"></a>С помощью Emulator Express toorun и отладки Azure облачной службы на локальном компьютере
Emulator Express позволяет протестировать и отладить облачную службу, не запуская Visual Studio от имени администратора. Можно задать параметры вашего проекта toouse либо Emulator Express или hello полного эмулятора в зависимости от требований hello облачной службы. Дополнительные сведения о hello полного эмулятора в разделе [запуск приложения Azure в эмуляторе вычислений hello](storage/common/storage-use-emulator.md).

## <a name="using-emulator-express-in-visual-studio"></a>Использование Emulator Express в Visual Studio
При создании проекта Azure в пакете Azure SDK 2.3 или более поздней версии Emulator Express используется автоматически. Для существующих проектов, которые были созданы в более ранней версии hello Azure SDK используйте следующие шаги tooselect Emulator Express hello:

1. Создайте или откройте проект облачной службы Azure в среде Visual Studio.

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.

1. На страницах свойств проектов hello выберите hello **Web** вкладки.

    ![Свойства проекта облачной службы Azure](./media/vs-azure-tools-emulator-express-debug-run/web-properties.png)

1. В разделе **Локальный сервер Development Server** выберите **Использовать IIS Express**.

1. В разделе **Эмулятор** выберите **Использовать Emulator Express**.
   
1. toolaunch hello Emulator Express, запустите следующую команду в командной строке hello: 

    ```
    csrun.exe /useemulatorexpress
    ```

## <a name="emulator-express-limitations"></a>Ограничения Emulator Express
следующие проблемы Hello перечислены известные ограничения Emulator Express. 

- Emulator Express несовместим с веб-сервером IIS.
- Облачная служба может содержать несколько ролей, но каждая роль является ограниченной tooone экземпляра.
- Невозможен доступ к портам с номерами меньше 1000. Если используется поставщик проверки подлинности, обычно использующий порт ниже 1000, может потребоваться toochange этот значение tooa номер порта выше 1000.
- Все ограничения, которые применяются toohello эмулятор вычислений Azure также применить tooEmulator Express. Например, число экземпляров роли в развернутой службе не может быть больше 50. Дополнительные сведения о hello эмулятор вычислений Azure см. в разделе [запуск приложения Azure в эмуляторе вычислений hello](http://go.microsoft.com/fwlink/p/?LinkId=623050).

## <a name="next-steps"></a>Дальнейшие действия
[Отладка облачных служб Azure](https://msdn.microsoft.com/library/azure/ee405479.aspx)
