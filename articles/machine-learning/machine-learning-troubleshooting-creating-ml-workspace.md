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
# <a name="troubleshooting-guide-create-and-connect-tooan-machine-learning-workspace"></a><span data-ttu-id="6244d-103">Руководстве по устранению неполадок: создать и присоединить tooan рабочей области машинного обучения</span><span class="sxs-lookup"><span data-stu-id="6244d-103">Troubleshooting guide: Create and connect tooan Machine Learning workspace</span></span>
<span data-ttu-id="6244d-104">В этом руководстве приведены решения некоторых проблем, часто возникающих при настройке рабочих областей для Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="6244d-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="6244d-105">Владелец рабочей области</span><span class="sxs-lookup"><span data-stu-id="6244d-105">Workspace owner</span></span>
<span data-ttu-id="6244d-106">tooopen рабочую область в студии машинного обучения, должен быть вход в учетную запись Майкрософт toohello используется рабочая область toocreate hello, или требуется tooreceive приглашение от toojoin hello hello владельца рабочей.</span><span class="sxs-lookup"><span data-stu-id="6244d-106">tooopen a workspace in Machine Learning Studio, you must be signed in toohello Microsoft Account you used toocreate hello workspace, or you need tooreceive an invitation from hello owner toojoin hello workspace.</span></span> <span data-ttu-id="6244d-107">Из hello портал Azure можно управлять hello рабочая область, которая включает в себя доступ tooconfigure возможность hello.</span><span class="sxs-lookup"><span data-stu-id="6244d-107">From hello Azure portal you can manage hello workspace, which includes hello ability tooconfigure access.</span></span>

<span data-ttu-id="6244d-108">Дополнительные сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure].</span><span class="sxs-lookup"><span data-stu-id="6244d-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

[Управление рабочей областью машинного обучения Azure]: machine-learning-manage-workspace.md

## <a name="allowed-regions"></a><span data-ttu-id="6244d-110">Разрешенные регионы</span><span class="sxs-lookup"><span data-stu-id="6244d-110">Allowed regions</span></span>
<span data-ttu-id="6244d-111">Сейчас машинное обучение доступно только в ограниченном числе регионов.</span><span class="sxs-lookup"><span data-stu-id="6244d-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="6244d-112">Если подписка не включает один из этих областей, может появиться сообщение об ошибке hello, «У вас нет подписок в допускается областей hello.»</span><span class="sxs-lookup"><span data-stu-id="6244d-112">If your subscription does not include one of these regions, you may see hello error message, “You have no subscriptions in hello allowed regions.”</span></span>

<span data-ttu-id="6244d-113">toorequest ее в область добавления подписки tooyour, создать новый запрос поддержки корпорации Майкрософт из hello портал Azure, выберите **выставления счетов** тип проблемы hello и следовать hello предлагает toosubmit ваш запрос.</span><span class="sxs-lookup"><span data-stu-id="6244d-113">toorequest that a region be added tooyour subscription, create a new Microsoft support request from hello Azure portal, choose **Billing** as hello problem type, and follow hello prompts toosubmit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="6244d-114">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="6244d-114">Storage account</span></span>
<span data-ttu-id="6244d-115">Hello службы машинного обучения требуются данные toostore учетной записи хранилища.</span><span class="sxs-lookup"><span data-stu-id="6244d-115">hello Machine Learning service needs a storage account toostore data.</span></span> <span data-ttu-id="6244d-116">Можно использовать существующую учетную запись хранения, или можно создать новую учетную запись хранения, при создании новой рабочей области машинного обучения hello (при наличии квоты toocreate новой учетной записи хранения).</span><span class="sxs-lookup"><span data-stu-id="6244d-116">You can use an existing storage account, or you can create a new storage account when you create hello new Machine Learning workspace (if you have quota toocreate a new storage account).</span></span>

<span data-ttu-id="6244d-117">После создания новой рабочей области машинного обучения hello tooMachine Learning Studio можно войти с помощью учетной записи Майкрософт hello используемых toocreate hello рабочей.</span><span class="sxs-lookup"><span data-stu-id="6244d-117">After hello new Machine Learning workspace is created, you can sign in tooMachine Learning Studio by using hello Microsoft account you used toocreate hello workspace.</span></span> <span data-ttu-id="6244d-118">Если возникнет сообщение об ошибке hello «Рабочей области не найден» (аналогично toohello, следующий снимок экрана), используйте следующие шаги toodelete hello файлы cookie браузера.</span><span class="sxs-lookup"><span data-stu-id="6244d-118">If you encounter hello error message, “Workspace Not Found” (similar toohello following screenshot), please use hello following steps toodelete your browser cookies.</span></span>

![Рабочая область не найдена.][screen3]

<span data-ttu-id="6244d-120">**файлы cookie в браузере toodelete**</span><span class="sxs-lookup"><span data-stu-id="6244d-120">**toodelete browser cookies**</span></span>

1. <span data-ttu-id="6244d-121">При использовании Internet Explorer, нажмите кнопку hello **средства** кнопку в правом верхнем углу hello и выберите **обозревателя**.</span><span class="sxs-lookup"><span data-stu-id="6244d-121">If you use Internet Explorer, click hello **Tools** button in hello upper-right corner and select **Internet options**.</span></span>  

![Свойства браузера][screen4]

2. <span data-ttu-id="6244d-123">В разделе hello **Общие** щелкните **удалить...**</span><span class="sxs-lookup"><span data-stu-id="6244d-123">Under hello **General** tab, click **Delete…**</span></span>

![Вкладка «Общие»][screen5]

3. <span data-ttu-id="6244d-125">В hello **удаление журнала браузера** диалогового окна поле, убедитесь, что **куки-файлы и данные веб-сайта** установлен и нажмите кнопку **удалить**.</span><span class="sxs-lookup"><span data-stu-id="6244d-125">In hello **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Удалить файлы cookie][screen6]

<span data-ttu-id="6244d-127">После удаления файлов "cookie" hello, перезапустите браузер hello, а затем перейдите toohello [машинного обучения Microsoft Azure](https://studio.azureml.net) страницы.</span><span class="sxs-lookup"><span data-stu-id="6244d-127">After hello cookies are deleted, restart hello browser and then go toohello [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="6244d-128">При появлении запроса введите имя пользователя и пароль, hello же учетной записью Майкрософт, используемых рабочей toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="6244d-128">When you are prompted for a user name and password, enter hello same Microsoft account you used toocreate hello workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="6244d-129">Комментарии</span><span class="sxs-lookup"><span data-stu-id="6244d-129">Comments</span></span>

<span data-ttu-id="6244d-130">Наша цель — toomake hello качества машинного обучения, как можно менее заметным.</span><span class="sxs-lookup"><span data-stu-id="6244d-130">Our goal is toomake hello Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="6244d-131">Опубликуйте любые комментарии и вопросы по hello [форум машинного обучения Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp нам, позволяющих повысить качество.</span><span class="sxs-lookup"><span data-stu-id="6244d-131">Please post any comments and issues at hello [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) toohelp us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
