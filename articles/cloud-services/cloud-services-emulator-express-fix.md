---
title: "Настройка Emulator Express для отладки приложений облачных служб в Visual Studio | Документация Майкрософт"
description: "Сведения об установке распространяемого компонента C++ для включения Emulator Express в Visual Studio"
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
ms.openlocfilehash: 05d672dcb1335c617bb8d8cae43947bcd5e9ab3d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="use-emulator-express-to-debug-cloud-services-application-in-vs-2017"></a><span data-ttu-id="9ca26-103">Использование Emulator Express для отладки приложений облачных служб в VS 2017</span><span class="sxs-lookup"><span data-stu-id="9ca26-103">Use Emulator Express to debug Cloud Services application in VS 2017</span></span>
<span data-ttu-id="9ca26-104">В этой статье описывается, как использовать Emulator Express для отладки приложений облачных служб в VS 2017.</span><span class="sxs-lookup"><span data-stu-id="9ca26-104">This article explains how to use Emulator Express to debug Cloud Services applications in VS 2017.</span></span>

## <a name="background-context"></a><span data-ttu-id="9ca26-105">Общие сведения</span><span class="sxs-lookup"><span data-stu-id="9ca26-105">Background context</span></span>
<span data-ttu-id="9ca26-106">Emulator Express по умолчанию используется для отладки веб-роли и рабочей роли облачных служб в Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="9ca26-106">Emulator Express is used by default for debugging Cloud Services Web and Worker roles in Visual Studio.</span></span> <span data-ttu-id="9ca26-107">Этот параметр задается на странице свойств проекта облачных служб.</span><span class="sxs-lookup"><span data-stu-id="9ca26-107">This setting is specified in the Cloud Services project properties page.</span></span>

![Открытие свойств проекта][0]

![Emulator Express выбран как параметр по умолчанию][1]

<span data-ttu-id="9ca26-110">[Распространяемый пакет Visual C++] [ Visual C++ Redistributable] для эмулятора требуется Visual Studio express.</span><span class="sxs-lookup"><span data-stu-id="9ca26-110">The [Visual C++ Redistributable][Visual C++ Redistributable] for Visual Studio is required by Emulator express.</span></span> <span data-ttu-id="9ca26-111">В настоящее время он не устанавливается в рамках рабочей нагрузки Azure.</span><span class="sxs-lookup"><span data-stu-id="9ca26-111">Currently it is not installed with the Azure workload.</span></span> <span data-ttu-id="9ca26-112">После того как вы нажмете клавишу F5 для отладки приложений облачных служб, Visual Studio предложит установить этот компонент и перейти к отладке.</span><span class="sxs-lookup"><span data-stu-id="9ca26-112">Upon F5 gesture to debug a Cloud Services applications, Visual Studio would prompt to install this component and proceed with debugging.</span></span>

![Запрос на установку распространяемого компонента C++][2]

<span data-ttu-id="9ca26-114">Нажмите кнопку "Да", чтобы установить распространяемый компонент C++.</span><span class="sxs-lookup"><span data-stu-id="9ca26-114">Click Yes to install C++ Redistributable.</span></span>

![Установка распространяемого компонента C++][3]

<span data-ttu-id="9ca26-116">Нажмите клавишу F5 еще раз, чтобы запустить сеансы отладки.</span><span class="sxs-lookup"><span data-stu-id="9ca26-116">Press F5 again to launch debugging sessions.</span></span>

![Запуск отладки][4]

![Отладка выполнена успешно][5]

> <span data-ttu-id="9ca26-119">Примечание. Установка распространяемого компонента Visual C++ выполняется один раз.</span><span class="sxs-lookup"><span data-stu-id="9ca26-119">Note: Installing Visual C++ Redistributable is a onetime effort.</span></span> <span data-ttu-id="9ca26-120">Если вы обновили старую версию пакета SDK для Azure и установили Emulator Express, вам не потребуется выполнять установку повторно.</span><span class="sxs-lookup"><span data-stu-id="9ca26-120">If you were upgrading from an older version of Azure SDK and have installed Emulator Express, then you won’t encounter this problem.</span></span>
> 
> 

## <a name="manual-workaround"></a><span data-ttu-id="9ca26-121">Установка компонента вручную</span><span class="sxs-lookup"><span data-stu-id="9ca26-121">Manual workaround</span></span>
<span data-ttu-id="9ca26-122">Вы также можете установить [распространяемый пакет Visual C++] [ Visual C++ Redistributable] вручную и эффект будут применяться согласно как Visual Studio он установлен в вашей системе.</span><span class="sxs-lookup"><span data-stu-id="9ca26-122">You can also install the [Visual C++ Redistributable][Visual C++ Redistributable] manually and same effect will be applied as how Visual Studio installed it on your system.</span></span>

<span data-ttu-id="9ca26-123">[vcredist_x86.exe][vcredist_x86.exe]</span><span class="sxs-lookup"><span data-stu-id="9ca26-123">[vcredist_x86.exe][vcredist_x86.exe]</span></span>

<span data-ttu-id="9ca26-124">[vcredist_x64.exe][vcredist_x64.exe]</span><span class="sxs-lookup"><span data-stu-id="9ca26-124">[vcredist_x64.exe][vcredist_x64.exe]</span></span>

## <a name="next-steps"></a><span data-ttu-id="9ca26-125">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="9ca26-125">Next Steps</span></span>
<span data-ttu-id="9ca26-126">Дополнительные сведения об использовании эмулятор вычислений Azure для отладки приложений облачных служб в Visual Studio: [использование Emulator Express для запуска и отладки облачной службы на локальном компьютере][Using Emulator Express to run and debug a cloud service on a local machine]</span><span class="sxs-lookup"><span data-stu-id="9ca26-126">Learn more about using Azure Computer Emulator to debug your Cloud Services applications in Visual Studio: [Using Emulator Express to run and debug a cloud service on a local machine][Using Emulator Express to run and debug a cloud service on a local machine]</span></span>

[Visual C++ Redistributable]:https://www.microsoft.com/en-us/download/details.aspx?id=30679
[vcredist_x86.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x86.exe
[vcredist_x64.exe]:https://download.microsoft.com/download/1/6/B/16B06F60-3B20-4FF2-B699-5E9B7962F9AE/VSU_4/vcredist_x64.exe
[Using Emulator Express to run and debug a cloud service on a local machine]:https://azure.microsoft.com/en-us/documentation/articles/vs-azure-tools-emulator-express-debug-run/

[0]: ./media/cloud-services-emulator-express-fix/vs-05.png
[1]: ./media/cloud-services-emulator-express-fix/vs-06.png
[2]: ./media/cloud-services-emulator-express-fix/vs-01.png
[3]: ./media/cloud-services-emulator-express-fix/vs-02.png
[4]: ./media/cloud-services-emulator-express-fix/vs-03.png
[5]: ./media/cloud-services-emulator-express-fix/vs-04.png
