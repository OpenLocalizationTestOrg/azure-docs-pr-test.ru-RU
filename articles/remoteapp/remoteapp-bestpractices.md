---
title: "Рекомендации по Azure RemoteApp | Документация Майкрософт"
description: "Рекомендации по настройке и использованию Azure RemoteApp."
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: b851865b-bec4-4f29-82c0-7b9770c1a520
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: ab9c2dafc622e9b6f3bcd2767218cdc03e844847
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="33bc8-103">Рекомендации по настройке и использованию Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="33bc8-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="33bc8-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="33bc8-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="33bc8-105">Дополнительные сведения см. в [объявлении](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/).</span><span class="sxs-lookup"><span data-stu-id="33bc8-105">Read the [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="33bc8-106">Приведенные ниже сведения помогут вам эффективно настроить и использовать Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="33bc8-106">The following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="33bc8-107">Соединение</span><span class="sxs-lookup"><span data-stu-id="33bc8-107">Connectivity</span></span>
* <span data-ttu-id="33bc8-108">Всегда используйте клиент последней версии.</span><span class="sxs-lookup"><span data-stu-id="33bc8-108">Always use the latest client version.</span></span> <span data-ttu-id="33bc8-109">Использование устаревших клиентов может привести к проблемам с подключением и другим неудобствам.</span><span class="sxs-lookup"><span data-stu-id="33bc8-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="33bc8-110">Включив автоматическое обновление приложений для своего устройства, вы обеспечите, что всегда установлена последняя версия клиента.</span><span class="sxs-lookup"><span data-stu-id="33bc8-110">Enabling automatic application updates for your device will ensure that the latest client is always installed.</span></span>
* <span data-ttu-id="33bc8-111">Всегда используйте самое стабильное и надежное подключение к Интернету из доступных.</span><span class="sxs-lookup"><span data-stu-id="33bc8-111">Always use the most stable and reliable internet connection available to you.</span></span>  
* <span data-ttu-id="33bc8-112">Используйте только поддерживаемые прокси-соединения, чтобы обеспечить оптимальное подключение.</span><span class="sxs-lookup"><span data-stu-id="33bc8-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="33bc8-113">Прокси SOCKS не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="33bc8-113">The SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="33bc8-114">Приложения</span><span class="sxs-lookup"><span data-stu-id="33bc8-114">Applications</span></span>
* <span data-ttu-id="33bc8-115">Сохраняйте и закрывайте приложения RemoteApp по завершении работы с ними.</span><span class="sxs-lookup"><span data-stu-id="33bc8-115">Save and close RemoteApp applications when you are done with the application.</span></span> <span data-ttu-id="33bc8-116">Если не закрыть приложение, данные могут быть утеряны.</span><span class="sxs-lookup"><span data-stu-id="33bc8-116">Not closing the application might result in data loss.</span></span>
* <span data-ttu-id="33bc8-117">Проверяйте настраиваемые приложения, прежде чем использовать их в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="33bc8-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="33bc8-118">В частности, убедитесь, что они работают на многосеансовой платформе и не потребляют избыточные ресурсы, например память и мощность процессора, ограничивая других пользователей в коллекции.</span><span class="sxs-lookup"><span data-stu-id="33bc8-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in the same collection.</span></span> <span data-ttu-id="33bc8-119">Чтобы получить дополнительную информацию, скачайте и прочитайте документ [Рекомендации по совместимости приложений для служб удаленных рабочих столов](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="33bc8-119">For information, download and review the [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="33bc8-120">Настройка и управление</span><span class="sxs-lookup"><span data-stu-id="33bc8-120">Configuration and management</span></span>
* <span data-ttu-id="33bc8-121">Поддерживайте образы шаблонов в актуальном состоянии, устанавливая обновления ПО и другие критические исправления по мере необходимости.</span><span class="sxs-lookup"><span data-stu-id="33bc8-121">Keep your template images up to date, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="33bc8-122">Это обеспечит обновление каждого экземпляра при автоматическом масштабировании Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="33bc8-122">This ensures that as Azure RemoteApp auto-scales to meet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="33bc8-123">Убедитесь, что развертывание служб федерации Active Directory (AD FS) защищено и надежно.</span><span class="sxs-lookup"><span data-stu-id="33bc8-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="33bc8-124">В противном случае проверка подлинности клиента может завершиться с ошибкой, и пользователи не смогут получить доступ к Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="33bc8-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="33bc8-125">Настройте образы шаблонов с такими установленными приложениями, ролями и функциями, чтобы у них не было состояния.</span><span class="sxs-lookup"><span data-stu-id="33bc8-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="33bc8-126">Они не должны зависеть от того, что какие-либо экземпляры виртуальных машин в службе RemoteApp находятся в устойчивом состоянии.</span><span class="sxs-lookup"><span data-stu-id="33bc8-126">They should not rely on any instances of the virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="33bc8-127">Храните все данные пользователей в профилях пользователей или других хранилищах за пределами службы, например локальных файловых ресурсах или OneDrive.</span><span class="sxs-lookup"><span data-stu-id="33bc8-127">Store all user data in user profiles or other storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="33bc8-128">Храните общие данные в хранилищах за пределами службы, например локальных файловых ресурсах или OneDrive.</span><span class="sxs-lookup"><span data-stu-id="33bc8-128">Store shared data in storage locations external to the service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="33bc8-129">Настраивайте параметры на уровне системы в образе шаблона, а не на отдельных виртуальных машинах в службе.</span><span class="sxs-lookup"><span data-stu-id="33bc8-129">Configure any system-wide settings in the template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="33bc8-130">Отключите автоматические обновления ПО для опубликованных приложений. Вместо этого применяйте их вручную к образу шаблона и тестируйте перед развертыванием из шаблона.</span><span class="sxs-lookup"><span data-stu-id="33bc8-130">Disable automatic software updates for published applications - instead apply them manually to the template image and test them before you deploy  from the template.</span></span>

