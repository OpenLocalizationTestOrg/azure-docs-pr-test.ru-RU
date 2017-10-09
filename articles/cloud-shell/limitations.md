---
title: "aaaAzure ограничения оболочка облака (Предварительная версия) | Документы Microsoft"
description: "Обзор ограничений Azure Cloud Shell."
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
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 8462b0b9850fcde790a386433009439bbab52c0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="limitations-of-azure-cloud-shell"></a>Ограничения Azure Cloud Shell
Azure облачной оболочки имеет hello следующие известные ограничения.

## <a name="system-state-and-persistence"></a>Состояние системы и сохраняемость
Hello машины, которая предоставляет сеанс оболочки облако временный, и он будет перезапущен после сеанса не используется в течение 20 минут. Облако оболочки требуется подключить toobe папки файла. В результате подписки должен быть может tooset копирование tooaccess ресурсы хранения оболочки облака. Дополнительные рекомендации:
* С подключенным хранилищем сохраняются только изменения в каталоге `$Home` или каталоге `clouddrive`.
* Общие папки можно подключить только в пределах [назначенного региона](persisting-shell-storage.md#mount-a-new-clouddrive).
* Файлы Azure поддерживают только локально избыточное хранилище в геоизбыточные учетные записи.

## <a name="user-permissions"></a>Разрешения пользователя
Разрешения задаются как для обычных пользователей без доступа к sudo. Все, что устанавливается за пределами каталога `$Home`, не сохранится.
Несмотря на то, что hello определенных команд в `clouddrive` каталога, такие как `git clone`, нет необходимых разрешений на `$Home` каталог имеет разрешения.

## <a name="browser-support"></a>Поддержка браузеров
Облако оболочки поддерживает hello последние версии Microsoft Edge, Microsoft Internet Explorer, Google Chrome, Mozilla Firefox и Apple Safari. Использование Safari в режиме защищенного просмотра не поддерживается.

## <a name="copy-and-paste"></a>Копирование и вставка
CTRL + C и Ctrl + V работать скопируйте ярлыки в оболочке облака на компьютерах Windows, используйте сочетание клавиш Ctrl + Insert и Shift + Insert toocopy и вставьте соответственно.

Параметры копирования и вставки контекстного меню также доступны, но функция щелкните правой кнопкой мыши имеет доступ к буферу обмена toobrowser определенного субъекта.

## <a name="editing-bashrc"></a>Изменение файла .bashrc
Будьте внимательны при изменении файла .bashrc, так как некоторые изменения могут привести к непредвиденным ошибкам в Cloud Shell.

## <a name="bashhistory"></a>.bash_history
Журнал команд bash может быть несогласованным из-за перебоев в сеансе Cloud Shell или из-за одновременных сеансов.

## <a name="usage-limits"></a>Ограничения использования
Cloud Shell предназначен для интерактивного использования. В результате любые длительные неинтерактивные сеансы завершаются без предупреждения.

## <a name="network-connectivity"></a>Сетевое подключение
Задержек в оболочке облака подключение к Интернету toolocal субъекта, оболочка облако по-прежнему toocarry tooattempt out инструкции, отправленные.

## <a name="next-steps"></a>Дальнейшие действия
[Краткое руководство по Cloud Shell](quickstart.md)
