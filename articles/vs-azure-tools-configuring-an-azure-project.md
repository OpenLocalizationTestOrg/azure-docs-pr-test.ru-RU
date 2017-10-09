---
title: "aaaConfigure проекта облачной службы Azure с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, как tooconfigure Azure облачной службы в проект в Visual Studio, в зависимости от требований для этого проекта."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 609d6965-05cc-47b1-82dc-c76a92d4f295
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/06/2017
ms.author: kraigb
ms.openlocfilehash: 40eb5eedd6ea23bf03c8707431799be28beae701
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-azure-cloud-service-project-with-visual-studio"></a>Настройка проекта облачной службы в Visual Studio
Проект облачной службы Azure можно настроить в соответствии с вашими требованиями к этому проекту. Можно задать свойства проекта hello для hello, следующие категории:

- **Публикация облачной службы tooAzure** -можно задать свойство toomake, убедиться, что случайного удаления существующей службы, развернутой tooAzure облака.
- **Запуск и отладка облачной службы на локальном компьютере hello** -можно выбрать toouse конфигурации службы и укажите, хотите ли вы toostart hello эмулятор хранилища Azure.
- **Проверить пакет облачной службы при его создании** -принято tootreat все предупреждения как ошибки, чтобы убедитесь, что пакет облачной службы hello развертывает без проблем. 

## <a name="steps-tooconfigure-an-azure-cloud-service-project"></a>Действия tooconfigure проекта облачной службы Azure
1. Открытие или создание проекта облачной службы в Visual Studio

1. В **обозревателе решений**, щелкните правой кнопкой мыши проект hello и hello контекстном меню, выберите **свойства**.
   
1. На странице свойств проекта hello, выберите hello **разработки** вкладки.

    ![Меню свойств проекта](./media/vs-azure-tools-configuring-an-azure-project/solution-explorer-project-properties-menu.png)

1. Задать **выдавать запрос перед удалением существующего развертывания** слишком**True**. Этот параметр помогает tooensure не случайно удалите существующее развертывание в Azure

1. Выберите hello требуемого **конфигурации службы** tooindicate, какую конфигурацию службы требуется toouse при запуске или отладке облачной службы локально. Дополнительные сведения о том, как. в разделе конфигурации службы для роли, toomodify [как tooconfigure hello роли для Azure облачной службы с помощью Visual Studio](./vs-azure-tools-configure-roles-for-cloud-service.md).

1. Задать **Запуск эмулятора хранилища Azure** слишком**True** toostart hello эмулятор хранилища Azure при запуске или отладке облачной службы локально.

1. Задать **обрабатывать предупреждения как ошибки** слишком**True** toomake убедиться, что нельзя публиковать при возникновении ошибки проверки правильности пакета.

1. Задать **использовать порты веб-проекта** слишком**True** toomake том, что веб-роль использует hello же порт каждый раз запускается локально в IIS Express.

1. Hello инструментов Visual Studio, выберите **Сохранить**.

## <a name="next-steps"></a>Дальнейшие действия
- [Настройка проекта Azure с помощью нескольких конфигураций службы](vs-azure-tools-multiple-services-project-configurations.md)

