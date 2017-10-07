---
title: "toodebug приложений облачных служб в Visual Studio express эмулятора aaaSetup | Документы Microsoft"
description: "Объясняет, как tooinstall hello tooenable распространяемый пакет C++, Emulator Express в Visual Studio"
services: cloud-services
documentationcenter: 
author: cawa
manager: paulyuk
editor: 
ms.assetid: 22b20f7a-23f4-4f7f-b536-3bf1e01adcd1
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 11/02/2016
ms.author: cawa
ms.openlocfilehash: 6fb506f0b1384f2e52310799eb5ae2a102d777bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a>Использование Emulator Express toodebug облачные службы приложения в VS 2017 г.
В этой статье объясняется, как toouse Emulator Express toodebug облачные службы приложения в VS 2017 г.

## <a name="background-context"></a>Общие сведения
Emulator Express по умолчанию используется для отладки веб-роли и рабочей роли облачных служб в Visual Studio. Этот параметр задается на странице свойств проекта hello облачных служб.

![Открытие свойств проекта][0]

![Emulator Express выбран как параметр по умолчанию][1]

Hello [распространяемый пакет Visual C++] [ Visual C++ Redistributable] для эмулятора требуется Visual Studio express. В настоящее время он не устанавливается вместе с hello Azure рабочей нагрузки. После F5 жестов toodebug приложений облачных служб, Visual Studio будет запрашивать tooinstall этого компонента и продолжить отладку.

![Запрос на установку распространяемого компонента C++][2]

Нажмите кнопку Да tooinstall распространяемый пакет C++.

![Установка распространяемого компонента C++][3]

Снова сеансы toolaunch отладки нажмите клавишу F5.

![Запуск отладки][4]

![Отладка выполнена успешно][5]

> Примечание. Установка распространяемого компонента Visual C++ выполняется один раз. Если вы обновили старую версию пакета SDK для Azure и установили Emulator Express, вам не потребуется выполнять установку повторно.
> 
> 

## <a name="manual-workaround"></a>Установка компонента вручную
Вы также можете установить hello [распространяемый пакет Visual C++] [ Visual C++ Redistributable] вручную и эффект будут применяться согласно как Visual Studio он установлен в вашей системе.

[vcredist_x86.exe][vcredist_x86.exe]

[vcredist_x64.exe][vcredist_x64.exe]

## <a name="next-steps"></a>Дальнейшие действия
Дополнительные сведения об использовании toodebug эмулятор вычислений Azure приложений облачных служб в Visual Studio: [toorun использование Emulator Express и отладка облачной службы на локальном компьютере][Using Emulator Express toorun and debug a cloud service on a local machine]

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express toorun and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
