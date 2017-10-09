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
# <a name="using-hello-azure-cloud-shell-window"></a>С помощью окна оболочки облако Azure hello

В этом документе объясняется, как toouse hello окна оболочки облака.

## <a name="concurrent-sessions"></a>Параллельные сеансы
Облако оболочки предоставляет несколько одновременных сеансов между вкладки браузера, позволяя tooexist каждого сеанса как отдельный процесс Bash.
Если выход из сеанса, убедитесь, что tooexit из каждого окна сеанса как каждый процесс выполняется независимо, несмотря на то, что они запущены на hello же машине.

## <a name="restart-cloud-shell"></a>Перезапуск Cloud Shell
![](media/recycle.png)
> [!WARNING]
> Перезапуск Cloud Shell сбросит состояние машины, и все файлы, не сохраненные в общей папке, будут утеряны.

* Щелкните значок перезапуска hello tooreceive инструментов hello новой оболочки облачной среды.

## <a name="minimize--maximize-cloud-shell-window"></a>Свертывание и развертывание окна Cloud Shell
![](media/minmax.png)
* Нажмите кнопку hello свести к минимуму значок hello верхнем правом углу окна toohide hello его. Снова щелкните hello значок облака оболочки toounhide.
* Нажмите кнопку hello максимальной высоты toomax значок tooset окна. окно tooprevious toorestore размер, нажмите "Восстановить".

## <a name="copy-and-paste"></a>Копирование и вставка
* Windows: `Ctrl-insert` toocopy и `Shift-insert` toopaste. Чтобы включить копирование и вставку, также можно щелкнуть правой кнопкой мыши раскрывающийся список.
  * Браузеры FireFox и IE могут не поддерживать разрешения буфера обмена корректно.
* Mac OS: `Cmd-c` toocopy и `Cmd-v` toopaste. Чтобы включить копирование и вставку, также можно щелкнуть правой кнопкой мыши раскрывающийся список.

## <a name="resize-cloud-shell-window"></a>Изменение размера окна Cloud Shell
* Щелкните и перетащите hello верхнего края панели инструментов hello вверх или вниз окна оболочки облака tooresize hello.

## <a name="scrolling-text-display"></a>Прокрутка текста
* Прокрутка с текстом терминалов toomove мышь или панель.

## <a name="exit-command"></a>Команда выхода
Под управлением `exit` завершает hello активного сеанса. Это происходит по умолчанию после 20 минут простоя.

## <a name="next-steps"></a>Дальнейшие действия
[Краткое руководство по Cloud Shell](quickstart.md)
