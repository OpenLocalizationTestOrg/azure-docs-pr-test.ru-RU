---
title: "Частные облака Azure aaaAccessing вместе с Visual Studio | Документы Microsoft"
description: "Узнайте, как tooaccess частные облачные ресурсы с помощью Visual Studio."
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 9d733c8d-703b-44e7-a210-bb75874c45c8
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 03/19/2017
ms.author: kraigb
ms.openlocfilehash: 5cfd6439afdcf98c6f7d7f29ab6c4256ed02533a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a>Доступ к частным облакам Azure с помощью Visual Studio
По умолчанию Visual Studio поддерживает конечные точки REST общедоступных облаков Azure. В этом разделе вы узнаете, как toouse вашего частного облака, сертификат tooaccess - и взаимодействовать с - hello частного облака из Visual Studio.

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a>облако tooaccess закрытый Azure в Visual Studio
1. В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) для hello частного облака, загрузите файл параметров публикации или обратитесь к администратору для файла параметров публикации. На hello общедоступной версии Azure, hello toodownload ссылки, это [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/). (hello скачанный файл должен иметь расширение `.publishsettings`)

1. Запустите Visual Studio

1. В **обозревателя серверов**, щелкните правой кнопкой мыши hello **Azure** узел и в контекстном меню hello, выберите **управление подписками и их фильтрация**.
   
    ![Команда "Управление подписками"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. В hello **управление подписками Microsoft Azure** диалоговое окно, выберите hello **сертификаты** , а затем выберите **импорта**.
   
    ![Импорт сертификатов Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. В hello **Импорт подписок Microsoft Azure** диалогового окна выберите **Обзор**.

    ![Кнопка в диалоговом окне приветствия Импорт подписок Microsoft Azure "Обзор"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. В hello **откройте** диалогового окна обзора toohello каталог, где вы hello сохраненный файл параметров публикации, выберите hello файла, а затем выберите **откройте**.

    ![Выберите файл настроек публикации hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. Если возвращается toohello **Импорт подписок Microsoft Azure** диалогового окна выберите **импорта**.

    ![Импорт файла настроек публикации hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    Hello сертификаты импортированы из файла настроек публикации hello в Visual Studio, и теперь можно взаимодействовать с ресурсами частного облака.
   
## <a name="next-steps"></a>Дальнейшие действия
- [Tooan публикации облачной службы Azure из Visual Studio](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- [How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx) (Практическое руководство. Скачивание и импорт параметров публикации и информации о подписке)
