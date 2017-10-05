---
title: "Проверка параметров диспетчера трафика Azure | Документация Майкрософт"
description: "В этой статье вы узнаете, как проверить параметры диспетчера трафика."
services: traffic-manager
documentationcenter: 
author: kumudd
manager: timlt
editor: 
ms.assetid: 2180b640-596e-4fb2-be59-23a38d606d12
ms.service: traffic-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/16/2017
ms.author: kumud
ms.openlocfilehash: aadff1806a7cb22347283143563467366e857569
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="verify-traffic-manager-settings"></a><span data-ttu-id="085f3-103">Проверка параметров диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="085f3-103">Verify Traffic Manager settings</span></span>

<span data-ttu-id="085f3-104">Чтобы проверить параметры диспетчера трафика, необходимо иметь несколько клиентов в разных расположениях, из которых можно запускать проверки.</span><span class="sxs-lookup"><span data-stu-id="085f3-104">To test your Traffic Manager settings, you need to have multiple clients, in various locations, from which you can run your tests.</span></span> <span data-ttu-id="085f3-105">Остановите работу конечных точек в профиле диспетчера трафика по одной за раз.</span><span class="sxs-lookup"><span data-stu-id="085f3-105">Then, bring the endpoints in your Traffic Manager profile down one at a time.</span></span>

* <span data-ttu-id="085f3-106">Задайте очень низкое значение срока жизни DNS, чтобы изменения распространялись быстро (например, за 30 секунд).</span><span class="sxs-lookup"><span data-stu-id="085f3-106">Set the DNS TTL value low so that changes propagate quickly (for example, 30 seconds).</span></span>
* <span data-ttu-id="085f3-107">Определите IP-адреса облачных служб Azure и веб-сайтов в проверяемом профиле.</span><span class="sxs-lookup"><span data-stu-id="085f3-107">Know the IP addresses of your Azure cloud services and websites in the profile you are testing.</span></span>
* <span data-ttu-id="085f3-108">Воспользуйтесь средствами, с помощью которых можно разрешить DNS-имя в IP-адрес и отобразить этот адрес.</span><span class="sxs-lookup"><span data-stu-id="085f3-108">Use tools that let you resolve a DNS name to an IP address and display that address.</span></span>

<span data-ttu-id="085f3-109">Это позволяет проверить, происходит ли разрешение DNS-имен в IP-адреса конечных точек в применяемом профиле.</span><span class="sxs-lookup"><span data-stu-id="085f3-109">You are checking to see that the DNS names resolve to IP addresses of the endpoints in your profile.</span></span> <span data-ttu-id="085f3-110">Разрешение имен должно происходить в форме, совместимой с методом маршрутизации трафика, определенном в профиле диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="085f3-110">The names should resolve in a manner consistent with the traffic routing method defined in the Traffic Manager profile.</span></span> <span data-ttu-id="085f3-111">Для разрешения DNS-имен можно использовать такие средства, как **nslookup** или **dig**.</span><span class="sxs-lookup"><span data-stu-id="085f3-111">You can use the tools like **nslookup** or **dig** to resolve DNS names.</span></span>

<span data-ttu-id="085f3-112">Ниже приведены примеры, которые помогут проверить профиль диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="085f3-112">The following examples help you test your Traffic Manager profile.</span></span>

### <a name="check-traffic-manager-profile-using-nslookup-and-ipconfig-in-windows"></a><span data-ttu-id="085f3-113">Проверка профиля диспетчера трафика с помощью команд nslookup и ipconfig в Windows</span><span class="sxs-lookup"><span data-stu-id="085f3-113">Check Traffic Manager profile using nslookup and ipconfig in Windows</span></span>

1. <span data-ttu-id="085f3-114">Откройте с правами администратора обычную командную строку или командную строку Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="085f3-114">Open a command or Windows PowerShell prompt as an administrator.</span></span>
2. <span data-ttu-id="085f3-115">Введите `ipconfig /flushdns` для записи кэша сопоставителя DNS на диск.</span><span class="sxs-lookup"><span data-stu-id="085f3-115">Type `ipconfig /flushdns` to flush the DNS resolver cache.</span></span>
3. <span data-ttu-id="085f3-116">Введите `nslookup <your Traffic Manager domain name>`.</span><span class="sxs-lookup"><span data-stu-id="085f3-116">Type `nslookup <your Traffic Manager domain name>`.</span></span> <span data-ttu-id="085f3-117">Например, следующая команда проверяет доменное имя с префиксом *myapp.contoso*.</span><span class="sxs-lookup"><span data-stu-id="085f3-117">For example, the following command checks the domain name with the prefix *myapp.contoso*</span></span>

        nslookup myapp.contoso.trafficmanager.net

    <span data-ttu-id="085f3-118">Типичный результат содержит следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="085f3-118">A typical result shows the following information:</span></span>

    + <span data-ttu-id="085f3-119">DNS-имя и IP-адрес DNS-сервера, доступ к которому получен для разрешения этого доменного имени диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="085f3-119">The DNS name and IP address of the DNS server being accessed to resolve this Traffic Manager domain name.</span></span>
    + <span data-ttu-id="085f3-120">Доменное имя диспетчера трафика, введенное в командной строке после команды nslookup, и IP-адрес, в который происходит разрешение домена диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="085f3-120">The Traffic Manager domain name you typed on the command line after "nslookup" and the IP address to which the Traffic Manager domain resolves.</span></span> <span data-ttu-id="085f3-121">Для проверки важен второй IP-адрес.</span><span class="sxs-lookup"><span data-stu-id="085f3-121">The second IP address is the important one to check.</span></span> <span data-ttu-id="085f3-122">Он должен соответствовать общедоступному виртуальному IP-адресу (VIP) для одной из облачных служб или веб-сайтов в тестируемом профиле диспетчера трафика.</span><span class="sxs-lookup"><span data-stu-id="085f3-122">It should match a public virtual IP (VIP) address for one of the cloud services or websites in the Traffic Manager profile you are testing.</span></span>

## <a name="how-to-test-the-failover-traffic-routing-method"></a><span data-ttu-id="085f3-123">Тестирование метода маршрутизации трафика с отработкой отказа</span><span class="sxs-lookup"><span data-stu-id="085f3-123">How to test the failover traffic routing method</span></span>

1. <span data-ttu-id="085f3-124">Оставьте все конечные точки включенными.</span><span class="sxs-lookup"><span data-stu-id="085f3-124">Leave all endpoints up.</span></span>
2. <span data-ttu-id="085f3-125">Используя один клиент, запросите разрешение DNS для доменного имени компании с помощью средства nslookup или подобной служебной программы.</span><span class="sxs-lookup"><span data-stu-id="085f3-125">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="085f3-126">Убедитесь, что разрешенный IP-адрес совпадает с основной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="085f3-126">Ensure that the resolved IP address matches the primary endpoint.</span></span>
4. <span data-ttu-id="085f3-127">Отключите основную конечную точку или удалите файл мониторинга, чтобы диспетчер трафика считал, что приложение не работает.</span><span class="sxs-lookup"><span data-stu-id="085f3-127">Bring down your primary endpoint or remove the monitoring file so that Traffic Manager thinks that the application is down.</span></span>
5. <span data-ttu-id="085f3-128">Ждите в течение срока жизни DNS, заданного в профиле диспетчера трафика, и еще 2 минуты.</span><span class="sxs-lookup"><span data-stu-id="085f3-128">Wait for the DNS Time-to-Live (TTL) of the Traffic Manager profile plus an additional two minutes.</span></span> <span data-ttu-id="085f3-129">Например, если срок жизни DNS — 300 секунд (5 минут), необходимо ждать 7 минут.</span><span class="sxs-lookup"><span data-stu-id="085f3-129">For example, if your DNS TTL is 300 seconds (5 minutes), you must wait for seven minutes.</span></span>
6. <span data-ttu-id="085f3-130">Очистите кэш DNS-клиента и запросите разрешение DNS с помощью команды nslookup.</span><span class="sxs-lookup"><span data-stu-id="085f3-130">Flush your DNS client cache and request DNS resolution using nslookup.</span></span> <span data-ttu-id="085f3-131">В Windows можно очистить кэш DNS с помощью команды ipconfig /flushdns.</span><span class="sxs-lookup"><span data-stu-id="085f3-131">In Windows, you can flush your DNS cache with the ipconfig /flushdns command.</span></span>
7. <span data-ttu-id="085f3-132">Убедитесь, что разрешенный IP-адрес совпадает с дополнительной конечной точкой.</span><span class="sxs-lookup"><span data-stu-id="085f3-132">Ensure that the resolved IP address matches your secondary endpoint.</span></span>
8. <span data-ttu-id="085f3-133">Повторите этот процесс, остановив работу каждой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="085f3-133">Repeat the process, bringing down each endpoint in turn.</span></span> <span data-ttu-id="085f3-134">Проверяйте, что DNS возвращает IP-адрес следующей конечной точки в списке.</span><span class="sxs-lookup"><span data-stu-id="085f3-134">Verify that the DNS returns the IP address of the next endpoint in the list.</span></span> <span data-ttu-id="085f3-135">Когда все конечные точки перестанут работать, вы снова должны получить IP-адрес основной конечной точки.</span><span class="sxs-lookup"><span data-stu-id="085f3-135">When all endpoints are down, you should obtain the IP address of the primary endpoint again.</span></span>

## <a name="how-to-test-the-weighted-traffic-routing-method"></a><span data-ttu-id="085f3-136">Тестирование метода маршрутизации трафика по приоритетам</span><span class="sxs-lookup"><span data-stu-id="085f3-136">How to test the weighted traffic routing method</span></span>

1. <span data-ttu-id="085f3-137">Оставьте все конечные точки включенными.</span><span class="sxs-lookup"><span data-stu-id="085f3-137">Leave all endpoints up.</span></span>
2. <span data-ttu-id="085f3-138">Используя один клиент, запросите разрешение DNS для доменного имени компании с помощью средства nslookup или подобной служебной программы.</span><span class="sxs-lookup"><span data-stu-id="085f3-138">Using a single client, request DNS resolution for your company domain name using nslookup or a similar utility.</span></span>
3. <span data-ttu-id="085f3-139">Убедитесь, что разрешенный IP-адрес совпадает с одной из конечных точек.</span><span class="sxs-lookup"><span data-stu-id="085f3-139">Ensure that the resolved IP address matches one of your endpoints.</span></span>
4. <span data-ttu-id="085f3-140">Очистите кэш клиента DNS и повторяйте шаги 2 и 3 для каждой конечной точки.</span><span class="sxs-lookup"><span data-stu-id="085f3-140">Flush your DNS client cache and repeat steps 2 and 3 for each endpoint.</span></span> <span data-ttu-id="085f3-141">Вы должны видеть разные IP-адреса, относящиеся ко всем вашим конечным точкам.</span><span class="sxs-lookup"><span data-stu-id="085f3-141">You should see different IP addresses returned for each of your endpoints.</span></span>

## <a name="how-to-test-the-performance-traffic-routing-method"></a><span data-ttu-id="085f3-142">Тестирование метода маршрутизации трафика производительности</span><span class="sxs-lookup"><span data-stu-id="085f3-142">How to test the performance traffic routing method</span></span>

<span data-ttu-id="085f3-143">Для эффективной проверки метода маршрутизации трафика по производительности клиенты должны быть расположены в различных частях мира.</span><span class="sxs-lookup"><span data-stu-id="085f3-143">To effectively test a performance traffic routing method, you must have clients located in different parts of the world.</span></span> <span data-ttu-id="085f3-144">Клиенты, которые будут использоваться для проверки служб, можно создавать в разных регионах Azure.</span><span class="sxs-lookup"><span data-stu-id="085f3-144">You can create clients in different Azure regions that can be used to test your services.</span></span> <span data-ttu-id="085f3-145">При наличии глобальной сети можно удаленно войти в клиенты в других регионах мира и выполнять проверки из них.</span><span class="sxs-lookup"><span data-stu-id="085f3-145">If you have a global network, you can remotely sign in to clients in other parts of the world and run your tests from there.</span></span>

<span data-ttu-id="085f3-146">Кроме того, есть бесплатные веб-службы поиска и проверки DNS.</span><span class="sxs-lookup"><span data-stu-id="085f3-146">Alternatively, there are free web-based DNS lookup and dig services available.</span></span> <span data-ttu-id="085f3-147">Некоторые из этих инструментов предоставляют возможность проверить разрешение DNS-имен из различных расположений по всему миру.</span><span class="sxs-lookup"><span data-stu-id="085f3-147">Some of these tools give you the ability to check DNS name resolution from various locations around the world.</span></span> <span data-ttu-id="085f3-148">Например, выполните поиск по запросу "поиск DNS".</span><span class="sxs-lookup"><span data-stu-id="085f3-148">Do a search on "DNS lookup" for examples.</span></span> <span data-ttu-id="085f3-149">Сторонние службы типа Gomez или Keynote можно использовать, чтобы убедиться в том, что ваши профили распределяют трафик надлежащим образом.</span><span class="sxs-lookup"><span data-stu-id="085f3-149">Third-party services like Gomez or Keynote can be used to confirm that your profiles are distributing traffic as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="085f3-150">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="085f3-150">Next steps</span></span>

* [<span data-ttu-id="085f3-151">О методах маршрутизации трафика в диспетчере трафика</span><span class="sxs-lookup"><span data-stu-id="085f3-151">About Traffic Manager traffic routing methods</span></span>](traffic-manager-routing-methods.md)
* [<span data-ttu-id="085f3-152">Рекомендации по безопасности для диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="085f3-152">Traffic Manager performance considerations</span></span>](traffic-manager-performance-considerations.md)
* [<span data-ttu-id="085f3-153">Устранение неполадок, связанных со сбоем диспетчера трафика</span><span class="sxs-lookup"><span data-stu-id="085f3-153">Troubleshooting Traffic Manager degraded state</span></span>](traffic-manager-troubleshooting-degraded.md)
