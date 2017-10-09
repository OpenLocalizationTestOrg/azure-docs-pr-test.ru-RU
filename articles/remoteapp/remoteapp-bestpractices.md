---
title: "рекомендации по RemoteApp aaaAzure | Документы Microsoft"
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
ms.openlocfilehash: f4d09ef30816eaebb74b69f26f3242c69ea27591
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="best-practices-for-configuring-and-using-azure-remoteapp"></a><span data-ttu-id="b6604-103">Рекомендации по настройке и использованию Azure RemoteApp</span><span class="sxs-lookup"><span data-stu-id="b6604-103">Best practices for configuring and using Azure RemoteApp</span></span>
> [!IMPORTANT]
> <span data-ttu-id="b6604-104">Мы выводим службу Azure RemoteApp из эксплуатации 31 августа 2017 года.</span><span class="sxs-lookup"><span data-stu-id="b6604-104">Azure RemoteApp is being discontinued on August 31, 2017.</span></span> <span data-ttu-id="b6604-105">Чтение hello [объявления](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) подробные сведения.</span><span class="sxs-lookup"><span data-stu-id="b6604-105">Read hello [announcement](https://blogs.technet.microsoft.com/enterprisemobility/2016/08/12/application-remoting-and-the-cloud/) for details.</span></span>
> 
> 

<span data-ttu-id="b6604-106">Hello следующие сведения помогут вам настроить и использовать Azure RemoteApp продуктивно.</span><span class="sxs-lookup"><span data-stu-id="b6604-106">hello following information can help you configure and use Azure RemoteApp productively.</span></span>

## <a name="connectivity"></a><span data-ttu-id="b6604-107">Соединение</span><span class="sxs-lookup"><span data-stu-id="b6604-107">Connectivity</span></span>
* <span data-ttu-id="b6604-108">Всегда используйте последнюю версию клиента hello.</span><span class="sxs-lookup"><span data-stu-id="b6604-108">Always use hello latest client version.</span></span> <span data-ttu-id="b6604-109">Использование устаревших клиентов может привести к проблемам с подключением и другим неудобствам.</span><span class="sxs-lookup"><span data-stu-id="b6604-109">Using older clients might result in connectivity issues and other degraded experiences.</span></span> <span data-ttu-id="b6604-110">Включить автоматическое применение обновлений для устройства обеспечит последнюю версию клиента, hello всегда устанавливается.</span><span class="sxs-lookup"><span data-stu-id="b6604-110">Enabling automatic application updates for your device will ensure that hello latest client is always installed.</span></span>
* <span data-ttu-id="b6604-111">Всегда используйте hello наиболее нестабильной или ненадежной Интернет соединения доступных tooyou.</span><span class="sxs-lookup"><span data-stu-id="b6604-111">Always use hello most stable and reliable internet connection available tooyou.</span></span>  
* <span data-ttu-id="b6604-112">Используйте только поддерживаемые прокси-соединения, чтобы обеспечить оптимальное подключение.</span><span class="sxs-lookup"><span data-stu-id="b6604-112">Use only supported proxy connections for optimal connectivity performance.</span></span>  <span data-ttu-id="b6604-113">прокси-сервера SOCKS Hello не поддерживается.</span><span class="sxs-lookup"><span data-stu-id="b6604-113">hello SOCKS proxy is not supported.</span></span>

## <a name="applications"></a><span data-ttu-id="b6604-114">Приложения</span><span class="sxs-lookup"><span data-stu-id="b6604-114">Applications</span></span>
* <span data-ttu-id="b6604-115">Сохраните и закройте приложения RemoteApp, завершении приложения hello.</span><span class="sxs-lookup"><span data-stu-id="b6604-115">Save and close RemoteApp applications when you are done with hello application.</span></span> <span data-ttu-id="b6604-116">Не закрывает приложение hello может привести к потере данных.</span><span class="sxs-lookup"><span data-stu-id="b6604-116">Not closing hello application might result in data loss.</span></span>
* <span data-ttu-id="b6604-117">Проверяйте настраиваемые приложения, прежде чем использовать их в Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b6604-117">Validate custom applications before using them in Azure RemoteApp.</span></span> <span data-ttu-id="b6604-118">Это включает в себя обеспечение они работают на платформе нескольких сеансов и не занимают ненужных ресурсов, например памяти и ЦП, который может препятствовать работе другим пользователем в hello одной коллекции.</span><span class="sxs-lookup"><span data-stu-id="b6604-118">This includes ensuring they work on a multi-session platform and don’t consume unnecessary resources such as memory and CPU that might starve another user in hello same collection.</span></span> <span data-ttu-id="b6604-119">Сведения, загрузки и просмотрите hello [совместимости рекомендации приложений для служб удаленных рабочих столов](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span><span class="sxs-lookup"><span data-stu-id="b6604-119">For information, download and review hello [Application Compatibility Best Practices for Remote Desktop Services](http://www.dabcc.com/resources/Application%20Compatibility%20Best%20Practices%20for%20Remote%20Desktop%20Services.pdf).</span></span>

## <a name="configuration-and-management"></a><span data-ttu-id="b6604-120">Настройка и управление</span><span class="sxs-lookup"><span data-stu-id="b6604-120">Configuration and management</span></span>
* <span data-ttu-id="b6604-121">Сохраните шаблон изображений вверх toodate, установки обновлений программного обеспечения и другие важные исправления, при необходимости.</span><span class="sxs-lookup"><span data-stu-id="b6604-121">Keep your template images up toodate, installing software updates and other critical fixes as needed.</span></span> <span data-ttu-id="b6604-122">Это гарантирует, что как Azure RemoteApp auto шкал toomeet емкость, каждый экземпляр будет заполнена.</span><span class="sxs-lookup"><span data-stu-id="b6604-122">This ensures that as Azure RemoteApp auto-scales toomeet your capacity, each instance is patched.</span></span>  
* <span data-ttu-id="b6604-123">Убедитесь, что развертывание служб федерации Active Directory (AD FS) защищено и надежно.</span><span class="sxs-lookup"><span data-stu-id="b6604-123">Make sure your Active Directory Federation Services (AD FS) deployment is secure and reliable.</span></span> <span data-ttu-id="b6604-124">В противном случае проверка подлинности клиента может завершиться с ошибкой, и пользователи не смогут получить доступ к Azure RemoteApp.</span><span class="sxs-lookup"><span data-stu-id="b6604-124">Otherwise client authentications might fail, preventing users from accessing Azure RemoteApp.</span></span>
* <span data-ttu-id="b6604-125">Настройте образы шаблонов с такими установленными приложениями, ролями и функциями, чтобы у них не было состояния.</span><span class="sxs-lookup"><span data-stu-id="b6604-125">Configure template images with installed applications, roles, or features such that they are stateless.</span></span> <span data-ttu-id="b6604-126">Они не следует полагаться на все экземпляры hello виртуальные машины в службе RemoteApp, находится в состоянии постоянного.</span><span class="sxs-lookup"><span data-stu-id="b6604-126">They should not rely on any instances of hello virtual machines in a RemoteApp service being in a persistent state.</span></span>
  * <span data-ttu-id="b6604-127">Хранить все данные пользователя в профили пользователей или другой службы внешнего toohello расположения хранилища, например локального файла, папки или OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b6604-127">Store all user data in user profiles or other storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="b6604-128">Хранить общие данные в службу внешней toohello расположения хранилища, например локального файла, папки или OneDrive.</span><span class="sxs-lookup"><span data-stu-id="b6604-128">Store shared data in storage locations external toohello service, such as on-premises file shares or OneDrive.</span></span>
  * <span data-ttu-id="b6604-129">Настройте параметры всей системы в образе шаблона hello, а не на отдельные виртуальные машины в службе.</span><span class="sxs-lookup"><span data-stu-id="b6604-129">Configure any system-wide settings in hello template image rather than on individual virtual machines in a service.</span></span>
  * <span data-ttu-id="b6604-130">Отключить автоматические обновления программного обеспечения для опубликованных приложений — вместо этого применить их вручную toohello образ шаблона и проверить их, прежде чем развертывать из шаблона hello.</span><span class="sxs-lookup"><span data-stu-id="b6604-130">Disable automatic software updates for published applications - instead apply them manually toohello template image and test them before you deploy  from hello template.</span></span>

