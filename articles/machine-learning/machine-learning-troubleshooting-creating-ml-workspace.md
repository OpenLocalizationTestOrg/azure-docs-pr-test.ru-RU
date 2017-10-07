---
title: "Устранение неполадок: Создать и присоединить рабочей области машинного обучения tooa | Документы Microsoft"
description: "Решения для распространенных проблем в создании и подключении рабочей области машинного обучения Azure tooan"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 1a8aec4b-35f9-44e8-9570-2575b8979ab1
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: 965a0025e85ba4e22c2b037edfa923e7f7599069
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a>Руководстве по устранению неполадок: создать и присоединить tooan рабочей области машинного обучения
В этом руководстве приведены решения некоторых проблем, часто возникающих при настройке рабочих областей для Машинного обучения Azure.

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a>Владелец рабочей области
tooopen рабочую область в студии машинного обучения, должен быть вход в учетную запись Майкрософт toohello используется рабочая область toocreate hello, или требуется tooreceive приглашение от toojoin hello hello владельца рабочей. Из hello портал Azure можно управлять hello рабочая область, которая включает в себя доступ tooconfigure возможность hello.

Дополнительные сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure].

[Управление рабочей областью машинного обучения Azure]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a>Разрешенные регионы
Сейчас машинное обучение доступно только в ограниченном числе регионов. Если подписка не включает один из этих областей, может появиться сообщение об ошибке hello, «У вас нет подписок в допускается областей hello.»

toorequest ее в область добавления подписки tooyour, создать новый запрос поддержки корпорации Майкрософт из hello портал Azure, выберите **выставления счетов** тип проблемы hello и следовать hello предлагает toosubmit ваш запрос.

## <a name="storage-account"></a>Учетная запись хранения
Hello службы машинного обучения требуются данные toostore учетной записи хранилища. Можно использовать существующую учетную запись хранения, или можно создать новую учетную запись хранения, при создании новой рабочей области машинного обучения hello (при наличии квоты toocreate новой учетной записи хранения).

После создания новой рабочей области машинного обучения hello tooMachine Learning Studio можно войти с помощью учетной записи Майкрософт hello используемых toocreate hello рабочей. Если возникнет сообщение об ошибке hello «Рабочей области не найден» (аналогично toohello, следующий снимок экрана), используйте следующие шаги toodelete hello файлы cookie браузера.

![Рабочая область не найдена.][screen3]

**файлы cookie в браузере toodelete**

1. При использовании Internet Explorer, нажмите кнопку hello **средства** кнопку в правом верхнем углу hello и выберите **обозревателя**.  

![Свойства браузера][screen4]

2. В разделе hello **Общие** щелкните **удалить...**

![Вкладка «Общие»][screen5]

3. В hello **удаление журнала браузера** диалогового окна поле, убедитесь, что **куки-файлы и данные веб-сайта** установлен и нажмите кнопку **удалить**.

![Удалить файлы cookie][screen6]

После удаления файлов "cookie" hello, перезапустите браузер hello, а затем перейдите toohello [машинного обучения Microsoft Azure](https://studio.azureml.net) страницы. При появлении запроса введите имя пользователя и пароль, hello же учетной записью Майкрософт, используемых рабочей toocreate hello.

## <a name="comments"></a>Комментарии

Наша цель — toomake hello качества машинного обучения, как можно менее заметным. Опубликуйте любые комментарии и вопросы по hello [форум машинного обучения Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp нам, позволяющих повысить качество.

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
