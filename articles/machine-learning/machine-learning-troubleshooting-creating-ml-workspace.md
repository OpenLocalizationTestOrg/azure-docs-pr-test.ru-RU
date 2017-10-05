---
title: "Устранение неполадок, связанных с созданием рабочей области машинного обучения и подключением к ней | Документация Майкрософт"
description: "Решения для распространенных проблем с созданием рабочей области Машинного обучения Azure и подключением к ней"
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
ms.openlocfilehash: 398ac3d9c9d32a1ab10413ce0d7ce8d448890409
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="troubleshooting-guide-create-and-connect-to-an-machine-learning-workspace"></a><span data-ttu-id="c4c77-103">Руководство по устранению неполадок: создание рабочей области машинного обучения и подключение к ней</span><span class="sxs-lookup"><span data-stu-id="c4c77-103">Troubleshooting guide: Create and connect to an Machine Learning workspace</span></span>
<span data-ttu-id="c4c77-104">В этом руководстве приведены решения некоторых проблем, часто возникающих при настройке рабочих областей для Машинного обучения Azure.</span><span class="sxs-lookup"><span data-stu-id="c4c77-104">This guide provides solutions for some frequently encountered challenges when you are setting up Azure Machine Learning workspaces.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="workspace-owner"></a><span data-ttu-id="c4c77-105">Владелец рабочей области</span><span class="sxs-lookup"><span data-stu-id="c4c77-105">Workspace owner</span></span>
<span data-ttu-id="c4c77-106">Чтобы открыть рабочую область в Студии машинного обучения, необходимо войти в учетную запись Майкрософт, использованную для создания рабочей области, или получить приглашение присоединиться к рабочей области от владельца.</span><span class="sxs-lookup"><span data-stu-id="c4c77-106">To open a workspace in Machine Learning Studio, you must be signed in to the Microsoft Account you used to create the workspace, or you need to receive an invitation from the owner to join the workspace.</span></span> <span data-ttu-id="c4c77-107">На портале Azure можно управлять рабочей областью, что включает в себя возможность настроить доступ.</span><span class="sxs-lookup"><span data-stu-id="c4c77-107">From the Azure portal you can manage the workspace, which includes the ability to configure access.</span></span>

<span data-ttu-id="c4c77-108">Дополнительные сведения об управлении рабочей областью см. в статье [Управление рабочей областью машинного обучения Azure].</span><span class="sxs-lookup"><span data-stu-id="c4c77-108">For more information on managing a workspace, see [Manage an Azure Machine Learning workspace].</span></span>

<span data-ttu-id="c4c77-109">[Управление рабочей областью машинного обучения Azure]: machine-learning-manage-workspace.md</span><span class="sxs-lookup"><span data-stu-id="c4c77-109">[Manage an Azure Machine Learning workspace]: machine-learning-manage-workspace.md</span></span>

## <a name="allowed-regions"></a><span data-ttu-id="c4c77-110">Разрешенные регионы</span><span class="sxs-lookup"><span data-stu-id="c4c77-110">Allowed regions</span></span>
<span data-ttu-id="c4c77-111">Сейчас машинное обучение доступно только в ограниченном числе регионов.</span><span class="sxs-lookup"><span data-stu-id="c4c77-111">Machine Learning is currently available in a limited number of regions.</span></span> <span data-ttu-id="c4c77-112">Если в вашу подписку не входит один из таких регионов, то может отобразиться сообщение об ошибке "У вас нет подписок в разрешенных регионах".</span><span class="sxs-lookup"><span data-stu-id="c4c77-112">If your subscription does not include one of these regions, you may see the error message, “You have no subscriptions in the allowed regions.”</span></span>

<span data-ttu-id="c4c77-113">Чтобы запросить добавление этого региона в вашу подписку, на портале Azure создайте запрос в службу поддержки Майкрософт, а затем в качестве типа проблемы выберите **Выставление счетов** и следуйте указаниям, чтобы отправить запрос.</span><span class="sxs-lookup"><span data-stu-id="c4c77-113">To request that a region be added to your subscription, create a new Microsoft support request from the Azure portal, choose **Billing** as the problem type, and follow the prompts to submit your request.</span></span>

## <a name="storage-account"></a><span data-ttu-id="c4c77-114">Учетная запись хранения</span><span class="sxs-lookup"><span data-stu-id="c4c77-114">Storage account</span></span>
<span data-ttu-id="c4c77-115">Для хранения данных службе машинного обучения требуется учетная запись хранения.</span><span class="sxs-lookup"><span data-stu-id="c4c77-115">The Machine Learning service needs a storage account to store data.</span></span> <span data-ttu-id="c4c77-116">Можно использовать имеющуюся учетную запись хранения либо создать новую учетную запись хранения при создании новой рабочей области машинного обучения (если имеется квота на ее создание).</span><span class="sxs-lookup"><span data-stu-id="c4c77-116">You can use an existing storage account, or you can create a new storage account when you create the new Machine Learning workspace (if you have quota to create a new storage account).</span></span>

<span data-ttu-id="c4c77-117">После создания новой рабочей области машинного обучения вы сможете войти в Студию машинного обучения, используя учетную запись Майкрософт, примененную для создания рабочей области.</span><span class="sxs-lookup"><span data-stu-id="c4c77-117">After the new Machine Learning workspace is created, you can sign in to Machine Learning Studio by using the Microsoft account you used to create the workspace.</span></span> <span data-ttu-id="c4c77-118">При появлении сообщения об ошибке «Рабочая область не найдена» (как на следующем снимке экрана) выполните следующие действия, чтобы удалить файлы cookie браузера.</span><span class="sxs-lookup"><span data-stu-id="c4c77-118">If you encounter the error message, “Workspace Not Found” (similar to the following screenshot), please use the following steps to delete your browser cookies.</span></span>

![Рабочая область не найдена.][screen3]

<span data-ttu-id="c4c77-120">**Удаление файлов cookie браузера**</span><span class="sxs-lookup"><span data-stu-id="c4c77-120">**To delete browser cookies**</span></span>

1. <span data-ttu-id="c4c77-121">Если вы используете Internet Explorer, нажмите кнопку **Сервис** в правом верхнем углу и выберите **Свойства браузера**.</span><span class="sxs-lookup"><span data-stu-id="c4c77-121">If you use Internet Explorer, click the **Tools** button in the upper-right corner and select **Internet options**.</span></span>  

![Свойства браузера][screen4]

2. <span data-ttu-id="c4c77-123">На вкладке **Общие** нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="c4c77-123">Under the **General** tab, click **Delete…**</span></span>

![Вкладка «Общие»][screen5]

3. <span data-ttu-id="c4c77-125">В диалоговом окне **Удаление истории обзора** установите флажок **Файлы cookie и данные веб-сайтов** и нажмите кнопку **Удалить**.</span><span class="sxs-lookup"><span data-stu-id="c4c77-125">In the **Delete Browsing History** dialog box, make sure **Cookies and website data** is selected, and click **Delete**.</span></span>

![Удалить файлы cookie][screen6]

<span data-ttu-id="c4c77-127">После удаления файлов cookie перезапустите браузер и перейдите на страницу [Машинного обучения Microsoft Azure](https://studio.azureml.net) .</span><span class="sxs-lookup"><span data-stu-id="c4c77-127">After the cookies are deleted, restart the browser and then go to the [Microsoft Azure Machine Learning](https://studio.azureml.net) page.</span></span> <span data-ttu-id="c4c77-128">Введите данные той же учетной записи Майкрософт, использованной для создания рабочей области.</span><span class="sxs-lookup"><span data-stu-id="c4c77-128">When you are prompted for a user name and password, enter the same Microsoft account you used to create the workspace.</span></span>

## <a name="comments"></a><span data-ttu-id="c4c77-129">Комментарии</span><span class="sxs-lookup"><span data-stu-id="c4c77-129">Comments</span></span>

<span data-ttu-id="c4c77-130">Наша цель — сделать работу с машинным обучением как можно более удобной.</span><span class="sxs-lookup"><span data-stu-id="c4c77-130">Our goal is to make the Machine Learning experience as seamless as possible.</span></span> <span data-ttu-id="c4c77-131">Публикуйте свои комментарии и описывайте проблемы на [форуме по  Машинному обучению Azure](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) , чтобы мы смогли эффективнее помочь вам.</span><span class="sxs-lookup"><span data-stu-id="c4c77-131">Please post any comments and issues at the [Azure Machine Learning forum](http://social.msdn.microsoft.com/Forums/windowsazure/home?forum=MachineLearning) to help us serve you better.</span></span>

[screen1]:media/machine-learning-troubleshooting-creating-ml-workspace/screen1.png
[screen2]:media/machine-learning-troubleshooting-creating-ml-workspace/screen2.png
[screen3]:media/machine-learning-troubleshooting-creating-ml-workspace/screen3.png
[screen4]:media/machine-learning-troubleshooting-creating-ml-workspace/screen4.png
[screen5]:media/machine-learning-troubleshooting-creating-ml-workspace/screen5.png
[screen6]:media/machine-learning-troubleshooting-creating-ml-workspace/screen6.png
