---
title: "aaaCreating проекта облачной службы Azure с помощью Visual Studio | Документы Microsoft"
description: "Узнайте, теперь toocreate проекта облачной службы Azure с помощью Visual Studio"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: ec580df7-3dcc-45a9-a1d9-8c110678dfb5
ms.service: multiple
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/21/2017
ms.author: kraigb
ms.openlocfilehash: 3c357016aa423688199a7ab3a670115e33a98fe9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="creating-an-azure-cloud-service-project-with-visual-studio"></a>Создание проекта облачной службы Azure в Visual Studio
Hello Azure Tools для Visual Studio предоставляет шаблон проекта, который позволяет создать облачную службу Azure. После создания проекта hello Visual Studio позволяет tooconfigure, отладки и развертывания службы tooAzure hello облака.

## <a name="steps-toocreate-an-azure-cloud-service-project-in-visual-studio"></a>Действия toocreate проекта облачной службы Azure в Visual Studio
В этом разделе описывается процесс создания проекта облачной службы Azure в Visual Studio с применением одной или нескольких веб-ролей.  

1. Запустите Visual Studio от имени администратора.

1. Hello главного меню, выберите **файл** > **New** > **проекта**.

1. Выберите **облака** из hello Visual C# или Visual Basic узлов проектов шаблонов и выберите **облачной службы Azure** из списка шаблонов hello.

    ![Новая облачная служба Azure](./media/vs-azure-tools-azure-project-create/new-project-wizard-for-cloud-service.png)

1. Укажите, какую версию hello нужно toouse toodevelop проект .NET Framework.

1. Введите имя и расположение проекта и имя решения hello. 

1. Нажмите кнопку **ОК**.

1. В hello **новой облачной службы Microsoft Azure** диалоговое окно, выберите hello роли, что tooadd и задайте tooadd кнопку со стрелкой вправо hello их tooyour решения.

    ![Выбор ролей для новой облачной службы Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service.png)

1. роли, вы добавили, при наведении указателя мыши на роль hello в hello toorename **новой облачной службы Microsoft Azure** диалоговое окно и в контекстном меню hello, выберите **Переименовать**. Можно также переименовать роль в решении (в hello **обозревателе решений**) после его добавления.

    ![Переименование роли облачной службы Azure](./media/vs-azure-tools-azure-project-create/new-cloud-service-rename.png)

Hello проекта Visual Studio Azure содержит связи toohello роли проектов в решении hello. Hello проект также содержит hello *файла определения службы* и *файла конфигурации службы*:

- **Файл определения службы** -определяет hello параметры среды выполнения для приложения, включая какие роли являются обязательными, конечные точки и размер виртуальной машины. 
- **Файл конфигурации службы** -настраивает, сколько экземпляров роли выполняются и hello значения параметров hello, определенных для роли. 

Дополнительные сведения об этих файлах см. в разделе [настроить hello роли для облачной службы Azure с помощью Visual Studio](vs-azure-tools-configure-roles-for-cloud-service.md).

## <a name="next-steps"></a>Дальнейшие действия
- [Управление ролями в проектах облачных служб Azure с помощью Visual Studio](./vs-azure-tools-cloud-service-project-managing-roles.md)
