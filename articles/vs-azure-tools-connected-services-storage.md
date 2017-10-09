---
title: "aaaAdd хранилища Azure с помощью подключенных служб в Visual Studio | Документы Microsoft"
description: "Добавить приложение tooyour хранилища Azure с помощью диалогового окна Visual Studio Добавление подключенных служб hello"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 521ec044-ad4b-4828-8864-01decde2e758
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/26/2017
ms.author: kraigb
ms.openlocfilehash: 56b42063d86510b330e405108e28d50e6ba4da05
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="adding-azure-storage-by-using-visual-studio-connected-services"></a>Добавление хранилища Azure с использованием подключенных служб Visual Studio
С помощью Visual Studio можно подключиться любой из следующих tooAzure хранилища с помощью hello hello **Добавление подключенных служб** диалогового окна:

- облачную службу C#;
- серверную мобильную службу .NET;
- веб-сайт или службу ASP.NET;
- службу ASP.NET Core;
- службу веб-заданий Azure. 

Hello подключенной службы функции добавляет все hello необходимые ссылки и проект tooyour кода подключения и соответствующим образом изменяет файлы конфигурации. 

После завершения hello **Добавление подключенных служб** автоматически отображает диалоговое окно открытия документации с подробными сведениями о необходимых toostart hello действия работа с хранилище больших двоичных объектов, очередей и таблиц.

## <a name="connect-tooazure-storage-using-hello-connected-services-dialog"></a>Подключения tooAzure хранилища hello подключенных служб с помощью диалогового окна
1. Откройте проект в Visual Studio.

1. В **обозреватель решений**, щелкните правой кнопкой мыши hello **подключенные службы** узел и из hello контекстное меню и выберите **добавление подключенной службы**.
   
    ![Добавление подключенной службы Azure](./media/vs-azure-tools-connected-services-storage/IC796702.png)

1. В hello **подключенные службы** выберите **облачного хранилища с хранилищем Azure**.
   
    ![Добавление учетной записи хранения Azure](./media/vs-azure-tools-connected-services-storage/add-azure-storage.png)

1. В hello **хранилища Azure** диалоговое окно, выберите существующую учетную запись хранилища и выберите **добавить**.
   
    Если вам требуется toocreate учетной записи хранилища, перейдите toohello следующий шаг. В противном случае пропустите toostep 6.
    
    ![Добавление существующих tooproject учетной записи хранилища](./media/vs-azure-tools-connected-services-storage/select-azure-storage-account.png)

1. toocreate учетную запись хранилища: 
   
   1. Выберите **создать новую учетную запись хранения** внизу hello диалогового окна "hello".

   1. Заполните hello **создать учетную запись хранилища** диалогового окна, а затем выберите **создать**.
      
       ![Новая учетная запись хранения Azure](./media/vs-azure-tools-connected-services-storage/create-storage-account.png)
      
   1. Здравствуйте, когда **хранилища Azure** отображается диалоговое окно, hello новой учетной записи хранения отображается в списке hello. Выберите новую учетную запись хранения hello hello списка и выберите **добавить**.

1. Здравствуйте, подключенная служба хранилища отображается под hello **ссылки на службу** узле проекта.
   
## <a name="how-your-project-is-modified"></a>Какие изменения произойдут в проекте
Завершив диалоговое окно приветствия, Visual Studio добавляет ссылки и изменяет определенные файлы конфигурации. Hello конкретные изменения зависят от типа проекта hello: 

- Проекты ASP.NET: ознакомьтесь со статьей [Приступая к работе с хранилищем BLOB-объектов Azure и подключенными службами Visual Studio (ASP.NET)](http://go.microsoft.com/fwlink/p/?LinkId=513126).
- Проекты ASP.NET Core: ознакомьтесь со статьей [Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (ASP.NET 5)](http://go.microsoft.com/fwlink/p/?LinkId=513124). 
- Проекты облачной службы (веб-роли и рабочие роли): ознакомьтесь со статьей [Начало работы с хранилищем больших двоичных объектов Azure и подключенными службами Visual Studio (проектами облачных служб)](http://go.microsoft.com/fwlink/p/?LinkId=516965).
- Проекты веб-заданий: ознакомьтесь со статьей [Что произошло с моим проектом веб-заданий (подключенными к службе хранилища Azure службами Visual Studio)?](visual-studio/vs-storage-webjobs-what-happened.md)

## <a name="next-steps"></a>Дальнейшие действия
- [Форум MSDN: хранилище Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=windowsazuredata)
- [Блог команды разработчиков службы хранилища Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/)
- [Документация по службе хранилища Azure](https://docs.microsoft.com/azure/storage/)
