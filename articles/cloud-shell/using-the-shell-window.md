---
title: "окна оболочки облако Azure (Предварительная версия) hello aaaUsing | Документы Microsoft"
description: "Окно оболочки облако Azure hello пошагового руководства."
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 07/13/2017
ms.author: juluk
ms.openlocfilehash: 571db3c8e177799a9e05f38a7cf8d2a4d5f8c8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-cloud-shell-window"></a><span data-ttu-id="ce972-103">С помощью окна оболочки облако Azure hello</span><span class="sxs-lookup"><span data-stu-id="ce972-103">Using hello Azure Cloud Shell window</span></span>

<span data-ttu-id="ce972-104">В этом документе объясняется, как toouse hello окна оболочки облака.</span><span class="sxs-lookup"><span data-stu-id="ce972-104">This document explains how toouse hello Cloud Shell window.</span></span>

## <a name="concurrent-sessions"></a><span data-ttu-id="ce972-105">Параллельные сеансы</span><span class="sxs-lookup"><span data-stu-id="ce972-105">Concurrent sessions</span></span>
<span data-ttu-id="ce972-106">Облако оболочки предоставляет несколько одновременных сеансов между вкладки браузера, позволяя tooexist каждого сеанса как отдельный процесс Bash.</span><span class="sxs-lookup"><span data-stu-id="ce972-106">Cloud Shell enables multiple concurrent sessions across browser tabs by allowing each session tooexist as a separate Bash process.</span></span>
<span data-ttu-id="ce972-107">Если выход из сеанса, убедитесь, что tooexit из каждого окна сеанса как каждый процесс выполняется независимо, несмотря на то, что они запущены на hello же машине.</span><span class="sxs-lookup"><span data-stu-id="ce972-107">If exiting a session, be sure tooexit from each session window as each process runs independently although they run on hello same machine.</span></span>

## <a name="restart-cloud-shell"></a><span data-ttu-id="ce972-108">Перезапуск Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ce972-108">Restart Cloud Shell</span></span>
![](media/recycle.png)
> [!WARNING]
> <span data-ttu-id="ce972-109">Перезапуск Cloud Shell сбросит состояние машины, и все файлы, не сохраненные в общей папке, будут утеряны.</span><span class="sxs-lookup"><span data-stu-id="ce972-109">Restarting Cloud Shell will reset machine state and any files not persisted by your file share will be lost.</span></span>

* <span data-ttu-id="ce972-110">Щелкните значок перезапуска hello tooreceive инструментов hello новой оболочки облачной среды.</span><span class="sxs-lookup"><span data-stu-id="ce972-110">Click hello restart icon on hello toolbar tooreceive a new Cloud Shell environment.</span></span>

## <a name="minimize--maximize-cloud-shell-window"></a><span data-ttu-id="ce972-111">Свертывание и развертывание окна Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ce972-111">Minimize & maximize Cloud Shell window</span></span>
![](media/minmax.png)
* <span data-ttu-id="ce972-112">Нажмите кнопку hello свести к минимуму значок hello верхнем правом углу окна toohide hello его.</span><span class="sxs-lookup"><span data-stu-id="ce972-112">Click hello minimize icon on hello top right of hello window toohide it.</span></span> <span data-ttu-id="ce972-113">Снова щелкните hello значок облака оболочки toounhide.</span><span class="sxs-lookup"><span data-stu-id="ce972-113">Click hello Cloud Shell icon again toounhide.</span></span>
* <span data-ttu-id="ce972-114">Нажмите кнопку hello максимальной высоты toomax значок tooset окна.</span><span class="sxs-lookup"><span data-stu-id="ce972-114">Click hello maximize icon tooset window toomax height.</span></span> <span data-ttu-id="ce972-115">окно tooprevious toorestore размер, нажмите "Восстановить".</span><span class="sxs-lookup"><span data-stu-id="ce972-115">toorestore window tooprevious size, click restore.</span></span>

## <a name="copy-and-paste"></a><span data-ttu-id="ce972-116">Копирование и вставка</span><span class="sxs-lookup"><span data-stu-id="ce972-116">Copy and paste</span></span>
* <span data-ttu-id="ce972-117">Windows: `Ctrl-insert` toocopy и `Shift-insert` toopaste.</span><span class="sxs-lookup"><span data-stu-id="ce972-117">Windows: `Ctrl-insert` toocopy and `Shift-insert` toopaste.</span></span> <span data-ttu-id="ce972-118">Чтобы включить копирование и вставку, также можно щелкнуть правой кнопкой мыши раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="ce972-118">Right-click dropdown can also enable copy/paste.</span></span>
  * <span data-ttu-id="ce972-119">Браузеры FireFox и IE могут не поддерживать разрешения буфера обмена корректно.</span><span class="sxs-lookup"><span data-stu-id="ce972-119">FireFox/IE may not support clipboard permissions properly.</span></span>
* <span data-ttu-id="ce972-120">Mac OS: `Cmd-c` toocopy и `Cmd-v` toopaste.</span><span class="sxs-lookup"><span data-stu-id="ce972-120">Mac OS: `Cmd-c` toocopy and `Cmd-v` toopaste.</span></span> <span data-ttu-id="ce972-121">Чтобы включить копирование и вставку, также можно щелкнуть правой кнопкой мыши раскрывающийся список.</span><span class="sxs-lookup"><span data-stu-id="ce972-121">Right-click dropdown can also enable copy/paste.</span></span>

## <a name="resize-cloud-shell-window"></a><span data-ttu-id="ce972-122">Изменение размера окна Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ce972-122">Resize Cloud Shell window</span></span>
* <span data-ttu-id="ce972-123">Щелкните и перетащите hello верхнего края панели инструментов hello вверх или вниз окна оболочки облака tooresize hello.</span><span class="sxs-lookup"><span data-stu-id="ce972-123">Click and drag hello top edge of hello toolbar up or down tooresize hello Cloud Shell window.</span></span>

## <a name="scrolling-text-display"></a><span data-ttu-id="ce972-124">Прокрутка текста</span><span class="sxs-lookup"><span data-stu-id="ce972-124">Scrolling text display</span></span>
* <span data-ttu-id="ce972-125">Прокрутка с текстом терминалов toomove мышь или панель.</span><span class="sxs-lookup"><span data-stu-id="ce972-125">Scroll with your mouse or touchpad toomove terminal text.</span></span>

## <a name="exit-command"></a><span data-ttu-id="ce972-126">Команда выхода</span><span class="sxs-lookup"><span data-stu-id="ce972-126">Exit command</span></span>
<span data-ttu-id="ce972-127">Под управлением `exit` завершает hello активного сеанса.</span><span class="sxs-lookup"><span data-stu-id="ce972-127">Running `exit` terminates hello active session.</span></span> <span data-ttu-id="ce972-128">Это происходит по умолчанию после 20 минут простоя.</span><span class="sxs-lookup"><span data-stu-id="ce972-128">This behavior occurs by default after 20 minutes without interaction.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ce972-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="ce972-129">Next steps</span></span>
[<span data-ttu-id="ce972-130">Краткое руководство по Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="ce972-130">Cloud Shell Quickstart</span></span>](quickstart.md)
