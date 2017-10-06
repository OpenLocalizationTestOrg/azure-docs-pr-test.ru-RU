---
title: "aaaUpload пользовательского изображения для Azure RemoteApp | Документы Microsoft"
description: "Узнайте, как tooupload пользовательского образа для Azure RemoteApp"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: 299e0510-1a6b-4fdf-914a-3631b061a360
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/23/2016
ms.author: ericor
ms.openlocfilehash: 6ad40fe58795ece37f4c7900be01bc713938da87
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="upload-a-custom-image-for-azure-remoteapp"></a>Отправка пользовательского образа для Azure RemoteApp
> [!IMPORTANT]
> Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года. Чтение hello [объявления](https://go.microsoft.com/fwlink/?linkid=821148) подробные сведения.
> 
> 

Теперь, когда вы создали пользовательский шаблон изображения или были обновлены с изменениями, вы должны tooupload, библиотека изображений Azure RemoteApp tooyour изображения. Выполните следующие действия.

## <a name="before-you-start"></a>Перед началом работы
1. Проверьте настраиваемого образа соответствует hello [требования к изображению](remoteapp-imagereqs.md) и [требования приложения](remoteapp-appreqs.md).
2. Установка hello [модуля Azure PowerShell](/powershell/azure/overview).

## <a name="step-by-step-on-how-tooupload-custom-image"></a>Шаг за шагом о том, как tooupload пользовательского образа
1. Открыть портал управления Azure и перейдите на страницу toohello RemoteApp.
2. На hello **образы шаблонов** щелкните **отправить** hello нижней части страницы приветствия.
3. Введите понятное имя для образа и укажите расположение учетной записи хранения hello. Убедитесь, расположение hello hello местоположения коллекции RemoteApp или место toocreate одно расположение.
4. При появлении соответствующего запроса загрузите tooyour сценария hello локального компьютера.
5. Скопируйте параметры команды hello в текстовом поле hello tooyour-буфер обмена.
6. Откройте окно Windows PowerShell с повышенными привилегиями.
7. Из hello с повышенными правами окно Windows PowerShell перейдите toohello же каталоге, куда был загружен скрипт hello.
8. Вставить hello скопировать команду и нажмите клавишу **ввод**.
   
   начнется процесс передачи Hello и длительность зависит от многих факторов, включая скорость сетевого подключения и размер изображения hello
9. Если подобное вашей передачи завершилась сбоем из-за перебоев в работе сети или вещи, всегда можно возобновить процесс передачи hello, когда вы начали. Здравствуйте tooresume передачи, запустите скрипт hello снова, используя же командной строки.

> [!WARNING]
> Никогда не изменяйте hello загрузки скрипта. Проверках было реализовано tooensure, hello hello образ изображения соответствуют требованиям и требованиям приложения.
> 
> 

## <a name="common-problems"></a>Распространенные проблемы
* Убедитесь, что вы используете Windows PowerShell, а не Azure PowerShell. Так как некоторые модули будут нужны во время процесса отправки hello необходимо модуля Azure PowerShell tooinstall hello.
* Никогда не изменяют hello сценария, проверки существуют для вашего удобства.
* Если hello VHD-файл получает заблокирована во время загрузки, скопируйте файл hello или переместите его новое расположение и попытка передачи tooa еще раз. Возможно, какой-то процесс Windows препятствует отправке.  

