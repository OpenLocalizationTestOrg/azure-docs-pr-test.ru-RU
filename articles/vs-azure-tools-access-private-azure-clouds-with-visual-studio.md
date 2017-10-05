---
title: "Доступ к частным облакам Azure с помощью Visual Studio | Документация Майкрософт"
description: "Узнайте, как получить доступ к ресурсам частного облака с помощью Visual Studio."
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
ms.openlocfilehash: b2578c837732ab05d538e9b896ed3a3035075a70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-private-azure-clouds-with-visual-studio"></a><span data-ttu-id="a255b-103">Доступ к частным облакам Azure с помощью Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a255b-103">Accessing private Azure clouds with Visual Studio</span></span>
<span data-ttu-id="a255b-104">По умолчанию Visual Studio поддерживает конечные точки REST общедоступных облаков Azure.</span><span class="sxs-lookup"><span data-stu-id="a255b-104">By default, Visual Studio supports public Azure cloud REST endpoints.</span></span> <span data-ttu-id="a255b-105">В этой статье вы узнаете, как использовать сертификат частного облака для доступа к частному облаку и взаимодействия с ним через Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="a255b-105">In this topic, you learn how to use your private cloud's certificate to access - and interact with - the private cloud from Visual Studio.</span></span>

## <a name="to-access-a-private-azure-cloud-in-visual-studio"></a><span data-ttu-id="a255b-106">Получение доступа к частному облаку Azure из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a255b-106">To access a private Azure cloud in Visual Studio</span></span>
1. <span data-ttu-id="a255b-107">Скачайте файл параметров публикации с [классического портала Azure](http://go.microsoft.com/fwlink/?LinkID=213885) для частного облака или запросите этот файл у администратора.</span><span class="sxs-lookup"><span data-stu-id="a255b-107">In the [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) for the private cloud, download your publish-settings file, or contact your administrator for a publish-settings file.</span></span> <span data-ttu-id="a255b-108">В общедоступной версии Azure скачать файл можно по ссылке [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span><span class="sxs-lookup"><span data-stu-id="a255b-108">On the public version of Azure, the link to download this is [https://manage.windowsazure.com/publishsettings/](https://manage.windowsazure.com/publishsettings/).</span></span> <span data-ttu-id="a255b-109">(Имя скачанного файла должно иметь расширение `.publishsettings`.)</span><span class="sxs-lookup"><span data-stu-id="a255b-109">(The downloaded file should have an extension of `.publishsettings`)</span></span>

1. <span data-ttu-id="a255b-110">Запустите Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a255b-110">Open Visual Studio</span></span>

1. <span data-ttu-id="a255b-111">В **обозревателе сервера** щелкните правой кнопкой мыши узел **Azure**, а затем выберите в контекстном меню пункт **Управление подписками и их фильтрация**.</span><span class="sxs-lookup"><span data-stu-id="a255b-111">In **Server Explorer**, right-click the **Azure** node and, from the context menu, select **Manage and Filter Subscriptions**.</span></span>
   
    ![Команда "Управление подписками"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790778.png)

1. <span data-ttu-id="a255b-113">В диалоговом окне **Управление подписками Microsoft Azure** выберите вкладку **Сертификаты**, а затем нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="a255b-113">In the **Manage Microsoft Azure Subscriptions** dialog, select the **Certificates** tab, and then select **Import**.</span></span>
   
    ![Импорт сертификатов Azure](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790779.png)

1. <span data-ttu-id="a255b-115">В диалоговом окне **Импорт подписок Microsoft Azure** нажмите кнопку **Обзор**.</span><span class="sxs-lookup"><span data-stu-id="a255b-115">In the **Import Microsoft Azure Subscriptions** dialog, select **Browse**.</span></span>

    ![Кнопка "Обзор" в диалоговом окне "Импорт подписок Microsoft Azure"](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/browse-button.png)

1. <span data-ttu-id="a255b-117">В диалоговом окне **Открытие** найдите каталог, в котором вы сохранили PUBLISHSETTINGS-файл, выберите его, а затем нажмите кнопку **Открыть**.</span><span class="sxs-lookup"><span data-stu-id="a255b-117">In the **Open** dialog, browse to the directory where you saved the publish-settings file, select the file, and then select **Open**.</span></span>

    ![Выбор PUBLISHSETTINGS-файла](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/select-publish-settings-file.png)

1. <span data-ttu-id="a255b-119">Вернувшись в диалоговое окно **Импорт подписок Microsoft Azure** нажмите кнопку **Импорт**.</span><span class="sxs-lookup"><span data-stu-id="a255b-119">When returned to the **Import Microsoft Azure Subscriptions** dialog, select **Import**.</span></span>

    ![Импорт PUBLISHSETTINGS-файла](./media/vs-azure-tools-access-private-azure-clouds-with-visual-studio/IC790780.png)

    <span data-ttu-id="a255b-121">Сертификаты импортируются из PUBLISHSETTINGS-файла в Visual Studio, и теперь вы можете работать с ресурсами частного облака.</span><span class="sxs-lookup"><span data-stu-id="a255b-121">The certificates are imported from the publish-settings file into Visual Studio, and you can now interact with your private cloud resources.</span></span>
   
## <a name="next-steps"></a><span data-ttu-id="a255b-122">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="a255b-122">Next steps</span></span>
- [<span data-ttu-id="a255b-123">Публикация в облачной службе Azure из Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a255b-123">Publishing to an Azure Cloud Service from Visual Studio</span></span>](https://msdn.microsoft.com/library/azure/ee460772.aspx)
- <span data-ttu-id="a255b-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx) (Практическое руководство. Скачивание и импорт параметров публикации и информации о подписке)</span><span class="sxs-lookup"><span data-stu-id="a255b-124">[How to: Download and Import Publish Settings and Subscription Information](https://msdn.microsoft.com/library/dn385850\(v=nav.70\).aspx)</span></span>
