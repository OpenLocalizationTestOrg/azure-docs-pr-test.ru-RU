---
title: "Руководство по устранению неполадок в обозревателе хранилищ Azure | Документы Майкрософт"
description: "Обзор двух функций отладки Azure"
services: virtual-machines
documentationcenter: 
author: Deland-Han
manager: cshepard
editor: 
ms.assetid: 
ms.service: virtual-machines
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/18/2017
ms.author: delhan
ms.openlocfilehash: 470b2d87ffdc4769bb2963df7dea646901469e00
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="bbc04-103">Руководство по устранению неполадок в обозревателе хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="bbc04-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="bbc04-104">Введение</span><span class="sxs-lookup"><span data-stu-id="bbc04-104">Introduction</span></span>

<span data-ttu-id="bbc04-105">Microsoft Azure Storage Explorer (предварительная версия) — это автономное приложение, позволяющее легко работать с данными из службы хранилища Azure на платформе Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="bbc04-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you to easily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="bbc04-106">Приложение может подключаться к учетным записям хранения, размещенным в Azure, Sovereign Clouds и Azure Stack.</span><span class="sxs-lookup"><span data-stu-id="bbc04-106">The app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="bbc04-107">В этом руководстве приведены решения для распространенных проблем, возникающих с обозревателем хранилищ.</span><span class="sxs-lookup"><span data-stu-id="bbc04-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="bbc04-108">Проблемы входа</span><span class="sxs-lookup"><span data-stu-id="bbc04-108">Sign in issues</span></span>

<span data-ttu-id="bbc04-109">Прежде всего, попытайтесь перезапустить приложение: возможно, это поможет решить проблему.</span><span class="sxs-lookup"><span data-stu-id="bbc04-109">Before you continue, try restarting your application and see whether the problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="bbc04-110">Ошибка "Самозаверяющий сертификат в цепочке сертификатов"</span><span class="sxs-lookup"><span data-stu-id="bbc04-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="bbc04-111">Существует несколько причин возникновения этой ошибки, однако наиболее распространены две причины.</span><span class="sxs-lookup"><span data-stu-id="bbc04-111">There are several reasons why you may encounter this error, and the most common two reasons are as follows:</span></span>

1. <span data-ttu-id="bbc04-112">Приложение подключается с помощью "прозрачного прокси-сервера". Это означает, что сервер (например, сервер вашей компании) перехватывает трафик HTTPS, расшифровывает его, а затем шифрует с помощью самозаверяющего сертификата.</span><span class="sxs-lookup"><span data-stu-id="bbc04-112">The app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="bbc04-113">Работающее приложение, такое как антивирусная программа, вставляет самозаверяющий сертификат SSL в получаемые сообщения HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbc04-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into the HTTPS messages that you receive.</span></span>

<span data-ttu-id="bbc04-114">Когда обозреватель хранилищ обнаруживает один из выпусков, он уже не может определить, изменено ли полученное сообщение HTTPS.</span><span class="sxs-lookup"><span data-stu-id="bbc04-114">When Storage Explorer encounters one of the issues, it can no longer know whether the received HTTPS message is tampered.</span></span> <span data-ttu-id="bbc04-115">Если у вас есть копия самозаверяющего сертификата, вы можете настроить доверие к нему в обозревателе хранилищ.</span><span class="sxs-lookup"><span data-stu-id="bbc04-115">If you have a copy of the self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="bbc04-116">Если вы не знаете, какой из компонентов вставляет сертификат, выполните следующие действия, чтобы найти его.</span><span class="sxs-lookup"><span data-stu-id="bbc04-116">If you are unsure of who is injecting the certificate, follow these steps to find it:</span></span>

1. <span data-ttu-id="bbc04-117">Установите Open SSL.</span><span class="sxs-lookup"><span data-stu-id="bbc04-117">Install Open SSL</span></span>

    - <span data-ttu-id="bbc04-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (любой из облегченных версий должно быть достаточно)</span><span class="sxs-lookup"><span data-stu-id="bbc04-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of the light versions should be sufficient)</span></span>

    - <span data-ttu-id="bbc04-119">MAC и Linux: этот компонент должен быть включен в операционную систему</span><span class="sxs-lookup"><span data-stu-id="bbc04-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="bbc04-120">Запустите Open SSL.</span><span class="sxs-lookup"><span data-stu-id="bbc04-120">Run Open SSL</span></span>

    - <span data-ttu-id="bbc04-121">Windows: откройте каталог установки, щелкните **/bin/**, а затем дважды щелкните **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="bbc04-121">Windows: open the installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="bbc04-122">MAC и Linux: запустите **openssl** из терминала.</span><span class="sxs-lookup"><span data-stu-id="bbc04-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="bbc04-123">Выполните команду s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="bbc04-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="bbc04-124">Найдите самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="bbc04-124">Look for self-signed certificates.</span></span> <span data-ttu-id="bbc04-125">Если вы не знаете, какие из сертификатов являются самозаверяющими, найдите сертификаты, в которых субъект ("s:") и издатель ("i:") совпадают.</span><span class="sxs-lookup"><span data-stu-id="bbc04-125">If you are unsure which are self-signed, look for anywhere the subject ("s:") and issuer ("i:") are the same.</span></span>

5. <span data-ttu-id="bbc04-126">Когда вы найдете самозаверяющие сертификаты, для каждого из них скопируйте и вставьте все содержимое от **---BEGIN CERTIFICATE---** до **---END CERTIFICATE---** включительно в новый CER-файл.</span><span class="sxs-lookup"><span data-stu-id="bbc04-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** to **-----END CERTIFICATE-----** to a new .cer file.</span></span>

6. <span data-ttu-id="bbc04-127">Откройте обозреватель хранилищ, щелкните **Изменить** > **SSL-сертификаты** > **Импорт сертификатов**, а затем с помощью средства выбора файлов найдите, выберите и откройте созданные CER-файлы.</span><span class="sxs-lookup"><span data-stu-id="bbc04-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use the file picker to find, select, and open the .cer files that you created.</span></span>

<span data-ttu-id="bbc04-128">Если вам не удалось найти самозаверяющие сертификаты, используя приведенные выше действия, свяжитесь с нами через средство обратной связи для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="bbc04-128">If you cannot find any self-signed certificates using the above steps, contact us through the feedback tool for more help.</span></span>

### <a name="unable-to-retrieve-subscriptions"></a><span data-ttu-id="bbc04-129">Не удается получить подписки</span><span class="sxs-lookup"><span data-stu-id="bbc04-129">Unable to retrieve subscriptions</span></span>

<span data-ttu-id="bbc04-130">Если не удается получить подписки после успешного входа, выполните следующие действия для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="bbc04-130">If you are unable to retrieve your subscriptions after you successfully sign in, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="bbc04-131">Убедитесь, что учетная запись имеет доступ к подпискам, выполнив вход на портал Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc04-131">Verify that your account has access to the subscriptions by signing into the Azure Portal.</span></span>

- <span data-ttu-id="bbc04-132">Убедитесь, что вы выполнили вход в правильную среду (Azure, Azure для Китая, Azure для Германии, Azure для государственных организаций США, пользовательскую среду или Azure Stack).</span><span class="sxs-lookup"><span data-stu-id="bbc04-132">Make sure that you have signed in using the correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="bbc04-133">При подключении через прокси-сервер убедитесь, что прокси-сервер обозревателя хранилищ настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="bbc04-133">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="bbc04-134">Попробуйте удалить и снова добавить учетную запись.</span><span class="sxs-lookup"><span data-stu-id="bbc04-134">Try removing and readding the account.</span></span>

- <span data-ttu-id="bbc04-135">Попробуйте удалить следующие файлы из корневого каталога (то есть C:\Users\ContosoUser), а затем снова добавить учетную запись:</span><span class="sxs-lookup"><span data-stu-id="bbc04-135">Try deleting the following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding the account:</span></span>

    - <span data-ttu-id="bbc04-136">adalcache-файл;</span><span class="sxs-lookup"><span data-stu-id="bbc04-136">.adalcache</span></span>

    - <span data-ttu-id="bbc04-137">devaccounts-файл;</span><span class="sxs-lookup"><span data-stu-id="bbc04-137">.devaccounts</span></span>

    - <span data-ttu-id="bbc04-138">extaccounts-файл.</span><span class="sxs-lookup"><span data-stu-id="bbc04-138">.extaccounts</span></span>

- <span data-ttu-id="bbc04-139">При выполнении входа проверьте наличие сообщений об ошибках в консоли средств разработчика (нажав клавишу F12):</span><span class="sxs-lookup"><span data-stu-id="bbc04-139">Watch the developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![средства разработчика](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-to-see-the-authentication-page"></a><span data-ttu-id="bbc04-141">Не отображается страница аутентификации</span><span class="sxs-lookup"><span data-stu-id="bbc04-141">Unable to see the authentication page</span></span>

<span data-ttu-id="bbc04-142">Если страница аутентификации не отображается, выполните следующие действия для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="bbc04-142">If you are unable to see the authentication page, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="bbc04-143">В зависимости от скорости подключения загрузка страницы входа может занять некоторое время. Подождите по крайней мере одну минуту, прежде чем закрывать диалоговое окно аутентификации.</span><span class="sxs-lookup"><span data-stu-id="bbc04-143">Depending on the speed of your connection, it may take a while for the sign-in page to load, wait at least one minute before closing the authentication dialog box.</span></span>

- <span data-ttu-id="bbc04-144">При подключении через прокси-сервер убедитесь, что прокси-сервер обозревателя хранилищ настроен правильно.</span><span class="sxs-lookup"><span data-stu-id="bbc04-144">If you are behind a proxy, make sure that you have configured the Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="bbc04-145">Просмотрите консоль разработчика, нажав клавишу F12.</span><span class="sxs-lookup"><span data-stu-id="bbc04-145">View the developer console by pressing the F12 key.</span></span> <span data-ttu-id="bbc04-146">Просмотрите ответы от консоли разработчика: возможно, вам удастся понять, почему страница аутентификации не работает.</span><span class="sxs-lookup"><span data-stu-id="bbc04-146">Watch the responses from the developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="bbc04-147">Невозможно удалить учетную запись</span><span class="sxs-lookup"><span data-stu-id="bbc04-147">Cannot remove account</span></span>

<span data-ttu-id="bbc04-148">Если не удается удалить учетную запись или при щелчке по ссылке повторной аутентификации ничего не происходит, выполните следующие действия для устранения этой проблемы.</span><span class="sxs-lookup"><span data-stu-id="bbc04-148">If you are unable to remove an account, or if the reauthenticate link does not do anything, follow these steps to troubleshoot this issue:</span></span>

- <span data-ttu-id="bbc04-149">Попробуйте удалить следующие файлы из корневого каталога, а затем снова добавить учетную запись:</span><span class="sxs-lookup"><span data-stu-id="bbc04-149">Try deleting the following files from your root directory, and then readding the account:</span></span>

    - <span data-ttu-id="bbc04-150">adalcache-файл;</span><span class="sxs-lookup"><span data-stu-id="bbc04-150">.adalcache</span></span>

    - <span data-ttu-id="bbc04-151">devaccounts-файл;</span><span class="sxs-lookup"><span data-stu-id="bbc04-151">.devaccounts</span></span>

    - <span data-ttu-id="bbc04-152">extaccounts-файл.</span><span class="sxs-lookup"><span data-stu-id="bbc04-152">.extaccounts</span></span>

- <span data-ttu-id="bbc04-153">Если вы хотите удалить подключенные ресурсы хранилища SAS, удалите следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="bbc04-153">If you want to remove SAS attached Storage resources, delete the following files:</span></span>

    - <span data-ttu-id="bbc04-154">папку %AppData%/StorageExplorer в Windows;</span><span class="sxs-lookup"><span data-stu-id="bbc04-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="bbc04-155">/Users/<ваше_имя>/Library/Applicaiton SUpport/StorageExplorer в Mac;</span><span class="sxs-lookup"><span data-stu-id="bbc04-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="bbc04-156">~/.config/StorageExplorer в Linux.</span><span class="sxs-lookup"><span data-stu-id="bbc04-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="bbc04-157">Если вы удалите эти файлы, вам потребуется повторно ввести все учетные данные.</span><span class="sxs-lookup"><span data-stu-id="bbc04-157">You will have to reenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="bbc04-158">Проблемы с прокси-сервером</span><span class="sxs-lookup"><span data-stu-id="bbc04-158">Proxy issues</span></span>

<span data-ttu-id="bbc04-159">Во-первых, убедитесь, что вы правильно указали следующие сведения:</span><span class="sxs-lookup"><span data-stu-id="bbc04-159">First, make sure that the following information you entered are all correct:</span></span>

- <span data-ttu-id="bbc04-160">URL-адрес прокси-сервера и номер порта;</span><span class="sxs-lookup"><span data-stu-id="bbc04-160">The proxy URL and port number</span></span>

- <span data-ttu-id="bbc04-161">имя пользователя и пароль, если этого требует прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="bbc04-161">Username and password if required by the proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="bbc04-162">Распространенные решения</span><span class="sxs-lookup"><span data-stu-id="bbc04-162">Common solutions</span></span>

<span data-ttu-id="bbc04-163">Если у вас по-прежнему возникают проблемы, выполните следующие действия для их устранения.</span><span class="sxs-lookup"><span data-stu-id="bbc04-163">If you are still experiencing issues, follow these steps to troubleshoot them:</span></span>

- <span data-ttu-id="bbc04-164">Если можно подключиться к Интернету без использования прокси-сервера, проверьте, будет ли обозреватель хранилищ работать с отключенными параметрами прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="bbc04-164">If you can connect to the Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="bbc04-165">Если это так, возможно, проблема связана с параметрами прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="bbc04-165">If this is the case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="bbc04-166">Обратитесь к администратору прокси-сервера, чтобы определить проблему.</span><span class="sxs-lookup"><span data-stu-id="bbc04-166">Work with your proxy administrator to identify the problems.</span></span>

- <span data-ttu-id="bbc04-167">Убедитесь, что другие приложения, использующие прокси-сервер, работают корректно.</span><span class="sxs-lookup"><span data-stu-id="bbc04-167">Verify that other applications using the proxy server work as expected.</span></span>

- <span data-ttu-id="bbc04-168">Проверьте, можно ли подключиться к порталу Microsoft Azure с помощью веб-браузера.</span><span class="sxs-lookup"><span data-stu-id="bbc04-168">Verify that you can connect to the Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="bbc04-169">Убедитесь, что вы можете получать ответы от конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="bbc04-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="bbc04-170">Введите один из URL-адресов конечной точки в браузере.</span><span class="sxs-lookup"><span data-stu-id="bbc04-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="bbc04-171">Если вам удается подключиться, вы должны получить ответ InvalidQueryParameterValue или аналогичный XML-ответ.</span><span class="sxs-lookup"><span data-stu-id="bbc04-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="bbc04-172">Если другие пользователи также используют обозреватель хранилищ с вашим прокси-сервером, проверьте, могут ли они подключаться.</span><span class="sxs-lookup"><span data-stu-id="bbc04-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="bbc04-173">Если у них не возникает проблем с подключением, возможно, вам потребуется обратиться к администратору прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="bbc04-173">If they can connect, you may have to contact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="bbc04-174">Инструменты для выявления проблем</span><span class="sxs-lookup"><span data-stu-id="bbc04-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="bbc04-175">Если вы используете средства работы с сетью, такие как Fiddler для Windows, можно попробовать диагностировать проблемы следующим образом.</span><span class="sxs-lookup"><span data-stu-id="bbc04-175">If you have networking tools, such as Fiddler for Windows, you may be able to diagnose the problems as follows:</span></span>

- <span data-ttu-id="bbc04-176">Если вам необходимо подключаться через прокси-сервер, может потребоваться настроить сетевые средства для подключения через прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="bbc04-176">If you have to work through your proxy, you may have to configure your networking tool to connect through the proxy.</span></span>

- <span data-ttu-id="bbc04-177">Проверьте номер порта, используемый средством для работы с сетью.</span><span class="sxs-lookup"><span data-stu-id="bbc04-177">Check the port number used by your networking tool.</span></span>

- <span data-ttu-id="bbc04-178">Введите URL-адрес локального узла и номер порта сетевого средства как параметры прокси-сервера в обозревателе хранилищ.</span><span class="sxs-lookup"><span data-stu-id="bbc04-178">Enter the local host URL and the networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="bbc04-179">Если выполнить эту процедуру правильно, средство для работы с сетью начнет регистрировать сетевые запросы, отправляемые обозревателем хранилищ в конечные точки управления и служб.</span><span class="sxs-lookup"><span data-stu-id="bbc04-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer to management and service endpoints.</span></span> <span data-ttu-id="bbc04-180">Например, введите адрес https://cawablobgrs.blob.core.windows.net/ для конечной точки хранилища BLOB-объектов в браузере и вы получите примерно следующий ответ, который предполагает, что ресурс существует, несмотря на то, что к нему нет доступа.</span><span class="sxs-lookup"><span data-stu-id="bbc04-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles the following, which suggests the resource exists, although you cannot access it.</span></span>

![пример кода](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="bbc04-182">Обратитесь к администратору прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="bbc04-182">Contact proxy server admin</span></span>

<span data-ttu-id="bbc04-183">Если параметры прокси-сервера настроены правильно, обратитесь к администратору прокси-сервера и</span><span class="sxs-lookup"><span data-stu-id="bbc04-183">If your proxy settings are correct, you may have to contact your proxy server admin, and</span></span>

- <span data-ttu-id="bbc04-184">убедитесь, что прокси-сервер не блокирует трафик к конечным точкам управления или ресурсов Azure.</span><span class="sxs-lookup"><span data-stu-id="bbc04-184">Make sure that your proxy does not block traffic to Azure management or resource endpoints.</span></span>

- <span data-ttu-id="bbc04-185">Проверьте протокол аутентификации, используемый прокси-сервером.</span><span class="sxs-lookup"><span data-stu-id="bbc04-185">Verify the authentication protocol used by your proxy server.</span></span> <span data-ttu-id="bbc04-186">Обозреватель хранилищ пока не поддерживает прокси-серверы NTLM.</span><span class="sxs-lookup"><span data-stu-id="bbc04-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-to-retrieve-children-error-message"></a><span data-ttu-id="bbc04-187">Сообщение об ошибке "Не удается получить дочерние элементы"</span><span class="sxs-lookup"><span data-stu-id="bbc04-187">"Unable to Retrieve Children" error message</span></span>

<span data-ttu-id="bbc04-188">Если вы подключаетесь к Azure через прокси-сервер, убедитесь, что его параметры настроены правильно.</span><span class="sxs-lookup"><span data-stu-id="bbc04-188">If you are connected to Azure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="bbc04-189">Если доступ к ресурсу предоставлен вам владельцем подписки или учетной записи, убедитесь, что у вас есть разрешения на чтение или перечисление для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="bbc04-189">If you were granted access to a resource from the owner of the subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="bbc04-190">Проблемы с URL-адресом SAS</span><span class="sxs-lookup"><span data-stu-id="bbc04-190">Issues with SAS URL</span></span>
<span data-ttu-id="bbc04-191">Если вы подключаетесь к службе с помощью URL-адреса SAS и возникает эта ошибка:</span><span class="sxs-lookup"><span data-stu-id="bbc04-191">If you are connecting to a service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="bbc04-192">убедитесь, что URL-адрес предоставляет необходимые разрешения на чтение или перечисление ресурсов.</span><span class="sxs-lookup"><span data-stu-id="bbc04-192">Verify that the URL provides the necessary permissions to read or list resources.</span></span>

- <span data-ttu-id="bbc04-193">Убедитесь, что срок действия URL-адреса не истек.</span><span class="sxs-lookup"><span data-stu-id="bbc04-193">Verify that the URL has not expired.</span></span>

- <span data-ttu-id="bbc04-194">Если URL-адрес основан на политике доступа, убедитесь, что политика доступа не была отозвана.</span><span class="sxs-lookup"><span data-stu-id="bbc04-194">If the SAS URL is based on an access policy, verify that the access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bbc04-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="bbc04-195">Next steps</span></span>

<span data-ttu-id="bbc04-196">Если ни одно из этих решений не помогло, воспользуйтесь средством обратной связи, чтобы отправить сообщение о проблеме через электронную почту. Укажите как можно больше сведений о проблеме, чтобы мы могли связаться с вами и помочь устранить ее.</span><span class="sxs-lookup"><span data-stu-id="bbc04-196">If none of the solutions work for you, submit your issue through the feedback tool with your email and as many details about the issue included as you can, so that we can contact you for fixing the issue.</span></span>

<span data-ttu-id="bbc04-197">Для этого перейдите в меню **Справка** и щелкните пункт **Отправить отзыв**.</span><span class="sxs-lookup"><span data-stu-id="bbc04-197">To do this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Отзыв](./media/storage-explorer-troubleshooting/4022503_en_1.png)
