---
title: "шаблоны aaaDeploy вместе с Visual Studio в стек Azure | Документы Microsoft"
description: "Узнайте, как шаблоны toodeploy вместе с Visual Studio в Azure стека."
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.assetid: 628da2ae-64cc-42e0-b8b7-a6a3724cb974
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: aea917b585a30ef4fbe7263db66f0659b56b21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-visual-studio"></a>Развертывание шаблонов в Azure Stack с помощью Visual Studio

Используйте Visual Studio toodeploy диспетчера ресурсов Azure шаблоны toohello стека Azure пакет средств разработки.

1. [Установка и подключение](azure-stack-install-visual-studio.md) tooAzure стека с помощью Visual Studio.
2. Откройте Visual Studio.
3. Нажмите кнопку **файл**, нажмите кнопку **New**и в hello **новый проект** диалоговом окне **группы ресурсов Azure**.
4. Введите **имя** для hello новых проектов, а затем нажмите кнопку **ОК**.
5. В hello **выберите шаблон Azure** диалоговое окно, изменение hello *Показать шаблоны из этого расположения* раскрывающемся слишком**краткое руководство стек Azure**
6. Нажмите кнопку **101-создать storage-account**, а затем нажмите кнопку **ОК**.  
7. В новый проект, вы увидите список доступных шаблонов hello, развернув hello **шаблоны** узел в hello **обозревателе решений** области.
8. В hello **обозревателе решений** hello щелкните правой кнопкой мыши имя проекта, выберите пункт **развернуть**, нажмите кнопку **новое развертывание**.
9. В hello **развернуть группу tooResource** диалогового окна hello **подписки** раскрывающийся список, выберите подписку Microsoft Azure стека.
10. В hello **группы ресурсов** выберите существующую группу ресурсов или создайте новую.
11. В hello **расположение группы ресурсов** список, выберите расположение и нажмите кнопку **развернуть**.
12. В hello **изменение параметров** диалогового окна введите значения для параметров hello (которые зависят от шаблона), а затем нажмите кнопку **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
[Развертывание шаблонов с hello командной строки](azure-stack-deploy-template-command-line.md)

[Разработка шаблонов для Azure Stack](azure-stack-develop-templates.md)

