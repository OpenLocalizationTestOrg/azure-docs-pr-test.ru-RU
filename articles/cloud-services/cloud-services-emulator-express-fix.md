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
# <a name="use-emulator-express-toodebug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="59ddc-103">Использование Emulator Express toodebug облачные службы приложения в VS 2017 г.</span><span class="sxs-lookup"><span data-stu-id="59ddc-103">Use Emulator Express toodebug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="59ddc-104">В этой статье объясняется, как toouse Emulator Express toodebug облачные службы приложения в VS 2017 г.</span><span class="sxs-lookup"><span data-stu-id="59ddc-104">This article explains how toouse Emulator Express toodebug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="59ddc-105">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="59ddc-105">Background context</span></span>
<span data-ttu-id="59ddc-106">Emulator Express по умолчанию используется для отладки веб-роли и рабочей роли облачных служб в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="59ddc-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="59ddc-107">Этот параметр задается на странице свойств проекта hello облачных служб.</span><span class="sxs-lookup"><span data-stu-id="59ddc-107">This setting is specified in hello Cloud Services project properties page.</span></span>

![Открытие свойств проекта][0]

![Emulator Express выбран как параметр по умолчанию][1]

<span data-ttu-id="59ddc-110">Hello [распространяемый пакет Visual C++] [ Visual C++ Redistributable] для эмулятора требуется Visual Studio express.</span><span class="sxs-lookup"><span data-stu-id="59ddc-110">hello [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="59ddc-111">В настоящее время он не устанавливается вместе с hello Azure рабочей нагрузки.</span><span class="sxs-lookup"><span data-stu-id="59ddc-111">Currently it is not installed with hello Azure workload.</span></span> <span data-ttu-id="59ddc-112">После F5 жестов toodebug приложений облачных служб, Visual Studio будет запрашивать tooinstall этого компонента и продолжить отладку.</span><span class="sxs-lookup"><span data-stu-id="59ddc-112">Upon F5 gesture toodebug a Cloud Services applications, Visual Studio would prompt tooinstall this component and proceed with debugging.</span></span>

![Запрос на установку распространяемого компонента C++][2]

<span data-ttu-id="59ddc-114">Нажмите кнопку Да tooinstall распространяемый пакет C++.</span><span class="sxs-lookup"><span data-stu-id="59ddc-114">Click Yes tooinstall C++ Redistributable.</span></span>

![Установка распространяемого компонента C++][3]

<span data-ttu-id="59ddc-116">Снова сеансы toolaunch отладки нажмите клавишу F5.</span><span class="sxs-lookup"><span data-stu-id="59ddc-116">Press F5 again toolaunch debugging sessions.</span></span>

![Запуск отладки][4]

![Отладка выполнена успешно][5]

> <span data-ttu-id="59ddc-119">Примечание. Установка распространяемого компонента Visual C++ выполняется один раз.</span><span class="sxs-lookup"><span data-stu-id="59ddc-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="59ddc-120">Если вы обновили старую версию пакета SDK для Azure и установили Emulator Express, вам не потребуется выполнять установку повторно.</span><span class="sxs-lookup"><span data-stu-id="59ddc-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="59ddc-121">Установка компонента вручную</span><span class="sxs-lookup"><span data-stu-id="59ddc-121">Manual workaround</span></span>
<span data-ttu-id="59ddc-122">Вы также можете установить hello [распространяемый пакет Visual C++] [ Visual C++ Redistributable] вручную и эффект будут применяться согласно как Visual Studio он установлен в вашей системе.</span><span class="sxs-lookup"><span data-stu-id="59ddc-122">You can also install hello [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="59ddc-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="59ddc-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="59ddc-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="59ddc-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="59ddc-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="59ddc-125">Next Steps</span></span>
<span data-ttu-id="59ddc-126">Дополнительные сведения об использовании toodebug эмулятор вычислений Azure приложений облачных служб в Visual Studio: [toorun использование Emulator Express и отладка облачной службы на локальном компьютере][Using Emulator Express toorun and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="59ddc-126">Learn more about using Azure Computer Emulator toodebug your Cloud Services applications in Visual Studio: [Using Emulator Express toorun and debug a cloud service on a local machine][Using Emulator Express toorun and debug a cloud service on a local machine]</span></span>

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
