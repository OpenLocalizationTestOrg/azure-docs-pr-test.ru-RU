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
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="5b24f-103">Доступ к частным облакам Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b24f-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="5b24f-104">По умолчанию Visual Studio поддерживает конечные точки REST общедоступных облаков Azure.</span><span class="sxs-lookup"><span data-stu-id="5b24f-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="5b24f-105">В этом разделе вы узнаете, как toouse вашего частного облака, сертификат tooaccess - и взаимодействовать с - hello частного облака из Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5b24f-105">In this topic, you learn how toouse your private cloud's certificate tooaccess - and interact with - hello private cloud from Visual Studio.</span></span>

## <a name="tooaccess-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="5b24f-106">облако tooaccess закрытый Azure в Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b24f-106">tooaccess a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="5b24f-107">В hello [классический портал Azure](http://go.microsoft.com/fwlink/?LinkID=213885) для hello частного облака, загрузите файл параметров публикации или обратитесь к администратору для файла параметров публикации.</span><span class="sxs-lookup"><span data-stu-id="5b24f-107">In hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for hello private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="5b24f-108">На hello общедоступной версии Azure, hello toodownload ссылки, это [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="5b24f-108">On hello public version of Azure, hello link toodownload this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="5b24f-109">(hello скачанный файл должен иметь расширение `.publishsettings`)</span><span class="sxs-lookup"><span data-stu-id="5b24f-109">(hello downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="5b24f-110">Запустите Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b24f-110">Open Visual Studio</span></span>

1. <span data-ttu-id="5b24f-111">В **обозревателя серверов**, щелкните правой кнопкой мыши hello **Azure** узел и в контекстном меню hello, выберите **управление подписками и их фильтрация**.</span><span class="sxs-lookup"><span data-stu-id="5b24f-111">In **Server Explorer**, right-click hello **Azure** node and, from hello context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Команда "Управление подписками"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="5b24f-113">В hello **управление подписками Microsoft Azure** диалоговое окно, выберите hello **сертификаты** , а затем выберите **импорта**.</span><span class="sxs-lookup"><span data-stu-id="5b24f-113">In hello **Manage Microsoft Azure Subscriptions** dialog, select hello **Certificates** tab, and then select **Import**.</span></span>
   
    ![Импорт сертификатов Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="5b24f-115">В hello **Импорт подписок Microsoft Azure** диалогового окна выберите **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="5b24f-115">In hello **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Кнопка в диалоговом окне приветствия Импорт подписок Microsoft Azure "Обзор"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="5b24f-117">В hello **откройте** диалогового окна обзора toohello каталог, где вы hello сохраненный файл параметров публикации, выберите hello файла, а затем выберите **откройте**.</span><span class="sxs-lookup"><span data-stu-id="5b24f-117">In hello **Open** dialog, browse toohello directory where you saved hello publish-settings file, select hello file, and then select **Open**.</span></span>

    ![Выберите файл настроек публикации hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="5b24f-119">Если возвращается toohello **Импорт подписок Microsoft Azure** диалогового окна выберите **импорта**.</span><span class="sxs-lookup"><span data-stu-id="5b24f-119">When returned toohello **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Импорт файла настроек публикации hello](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="5b24f-121">Hello сертификаты импортированы из файла настроек публикации hello в Visual Studio, и теперь можно взаимодействовать с ресурсами частного облака.</span><span class="sxs-lookup"><span data-stu-id="5b24f-121">hello certificates are imported from hello publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="5b24f-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="5b24f-122">Next steps</span></span>
- [<span data-ttu-id="5b24f-123">Tooan публикации облачной службы Azure из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="5b24f-123">Publishing tooan Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="5b24f-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx) (Практическое руководство. Скачивание и импорт параметров публикации и информации о подписке)</span><span class="sxs-lookup"><span data-stu-id="5b24f-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
