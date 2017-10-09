---
title: "руководство по устранению неполадок обозреватель хранилищ aaaAzure | Документы Microsoft"
description: "Общие сведения о функции hello двух отладки Azure"
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
ms.openlocfilehash: 5152f70418707d65c0a4bce9a916336829956219
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-explorer-troubleshooting-guide"></a><span data-ttu-id="888d9-103">Руководство по устранению неполадок в обозревателе хранилищ Azure</span><span class="sxs-lookup"><span data-stu-id="888d9-103">Azure Storage Explorer troubleshooting guide</span></span>

## <a name="introduction"></a><span data-ttu-id="888d9-104">Введение</span><span class="sxs-lookup"><span data-stu-id="888d9-104">Introduction</span></span>

<span data-ttu-id="888d9-105">Обозреватель хранилищ Microsoft Azure (Предварительная версия) представляет собой автономное приложение, позволяющее tooeasily работы с данными хранилища Azure для Windows, macOS и Linux.</span><span class="sxs-lookup"><span data-stu-id="888d9-105">Microsoft Azure Storage Explorer (Preview) is a stand-alone app that enables you tooeasily work with Azure Storage data on Windows, macOS and Linux.</span></span> <span data-ttu-id="888d9-106">приложение Hello можно подключить toStorage учетных записей, размещенных в Azure, Sovereign облаков, а стек Azure.</span><span class="sxs-lookup"><span data-stu-id="888d9-106">hello app can connect toStorage accounts hosted on Azure, Sovereign Clouds, and Azure Stack.</span></span>

<span data-ttu-id="888d9-107">В этом руководстве приведены решения для распространенных проблем, возникающих с обозревателем хранилищ.</span><span class="sxs-lookup"><span data-stu-id="888d9-107">This guide summarizes solutions for common issues seen in Storage Explorer.</span></span>

## <a name="sign-in-issues"></a><span data-ttu-id="888d9-108">Проблемы входа</span><span class="sxs-lookup"><span data-stu-id="888d9-108">Sign in issues</span></span>

<span data-ttu-id="888d9-109">Прежде чем продолжить, перезапустите приложение и разделе, можно ли устранить проблемы hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-109">Before you continue, try restarting your application and see whether hello problems can be fixed.</span></span>

### <a name="error-self-signed-certificate-in-certificate-chain"></a><span data-ttu-id="888d9-110">Ошибка "Самозаверяющий сертификат в цепочке сертификатов"</span><span class="sxs-lookup"><span data-stu-id="888d9-110">Error: Self-Signed Certificate in Certificate Chain</span></span>

<span data-ttu-id="888d9-111">Существует несколько причин, почему эта ошибка возникает, и hello наиболее распространенные причины приведены ниже:</span><span class="sxs-lookup"><span data-stu-id="888d9-111">There are several reasons why you may encounter this error, and hello most common two reasons are as follows:</span></span>

1. <span data-ttu-id="888d9-112">приложение Hello подключен через «прозрачный прокси», что означает перехват трафика HTTPS, нужно их расшифровывать и затем шифрование с помощью самозаверяющего сертификата сервера (например, серверу компании).</span><span class="sxs-lookup"><span data-stu-id="888d9-112">hello app is connected through a “transparent proxy”, which means a server (such as your company server) is intercepting HTTPS traffic, decrypting it, and then encrypting it using a self-signed certificate.</span></span>

2. <span data-ttu-id="888d9-113">Используется приложением, например антивирусное программное обеспечение, которое внедряет самозаверяющий сертификат SSL в получаемых сообщений hello HTTPS.</span><span class="sxs-lookup"><span data-stu-id="888d9-113">You are running an application, such as antivirus software, which is injecting a self-signed SSL certificate into hello HTTPS messages that you receive.</span></span>

<span data-ttu-id="888d9-114">Когда обозреватель хранилищ возникает одна из проблем hello, он больше не известно ли сообщение получено hello HTTPS искажено.</span><span class="sxs-lookup"><span data-stu-id="888d9-114">When Storage Explorer encounters one of hello issues, it can no longer know whether hello received HTTPS message is tampered.</span></span> <span data-ttu-id="888d9-115">Если у вас есть копия hello самозаверяющий сертификат, можно позволить обозреватель хранилища доверия.</span><span class="sxs-lookup"><span data-stu-id="888d9-115">If you have a copy of hello self-signed certificate, you can let Storage Explorer trust it.</span></span> <span data-ttu-id="888d9-116">Если вы не знаете кто внедряет hello сертификата, выполните эти шаги toofind его:</span><span class="sxs-lookup"><span data-stu-id="888d9-116">If you are unsure of who is injecting hello certificate, follow these steps toofind it:</span></span>

1. <span data-ttu-id="888d9-117">Установите Open SSL.</span><span class="sxs-lookup"><span data-stu-id="888d9-117">Install Open SSL</span></span>

    - <span data-ttu-id="888d9-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (любой из версий светлой hello должно быть достаточно)</span><span class="sxs-lookup"><span data-stu-id="888d9-118">[Windows](https://slproweb.com/products/Win32OpenSSL.html) (any of hello light versions should be sufficient)</span></span>

    - <span data-ttu-id="888d9-119">MAC и Linux: этот компонент должен быть включен в операционную систему</span><span class="sxs-lookup"><span data-stu-id="888d9-119">Mac and Linux: should be included with your operating system</span></span>

2. <span data-ttu-id="888d9-120">Запустите Open SSL.</span><span class="sxs-lookup"><span data-stu-id="888d9-120">Run Open SSL</span></span>

    - <span data-ttu-id="888d9-121">Windows: откройте каталог установки hello, щелкните **/bin/**, а затем дважды щелкните **openssl.exe**.</span><span class="sxs-lookup"><span data-stu-id="888d9-121">Windows: open hello installation directory, click **/bin/**, and then double-click **openssl.exe**.</span></span>
    - <span data-ttu-id="888d9-122">MAC и Linux: запустите **openssl** из терминала.</span><span class="sxs-lookup"><span data-stu-id="888d9-122">Mac and Linux: run **openssl** from a terminal.</span></span>

3. <span data-ttu-id="888d9-123">Выполните команду s_client -showcerts -connect microsoft.com:443</span><span class="sxs-lookup"><span data-stu-id="888d9-123">Execute s_client -showcerts -connect microsoft.com:443</span></span>

4. <span data-ttu-id="888d9-124">Найдите самозаверяющие сертификаты.</span><span class="sxs-lookup"><span data-stu-id="888d9-124">Look for self-signed certificates.</span></span> <span data-ttu-id="888d9-125">Если вы не уверены, что являются самозаверяющими, найдите в любом hello субъекта («s:») и издателя («i:») являются одинаковыми hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-125">If you are unsure which are self-signed, look for anywhere hello subject ("s:") and issuer ("i:") are hello same.</span></span>

5. <span data-ttu-id="888d9-126">Если будут найдены все самозаверяющие сертификаты, для каждого из них, скопируйте и вставьте все данные из и в том числе **---BEGIN CERTIFICATE---** слишком**---конечный СЕРТИФИКАТ---** tooa новый CER-файл.</span><span class="sxs-lookup"><span data-stu-id="888d9-126">When you have found any self-signed certificates, for each one, copy and paste everything from and including **-----BEGIN CERTIFICATE-----** too**-----END CERTIFICATE-----** tooa new .cer file.</span></span>

6. <span data-ttu-id="888d9-127">Откройте обозреватель хранилищ, щелкните **изменить** > **SSL-сертификаты** > **импорта сертификатов**и затем используйте hello файл выбора toofind, select, и открывать файлы CER-файл hello, которые были созданы.</span><span class="sxs-lookup"><span data-stu-id="888d9-127">Open Storage Explorer, click **Edit** > **SSL Certificates** > **Import Certificates**, and then use hello file picker toofind, select, and open hello .cer files that you created.</span></span>

<span data-ttu-id="888d9-128">Если не удается найти самостоятельно подписанные сертификаты, используя hello выше действия, свяжитесь с нами через hello средства обратной связи для получения дополнительных сведений.</span><span class="sxs-lookup"><span data-stu-id="888d9-128">If you cannot find any self-signed certificates using hello above steps, contact us through hello feedback tool for more help.</span></span>

### <a name="unable-tooretrieve-subscriptions"></a><span data-ttu-id="888d9-129">Не удается tooretrieve подписки</span><span class="sxs-lookup"><span data-stu-id="888d9-129">Unable tooretrieve subscriptions</span></span>

<span data-ttu-id="888d9-130">Не удается tooretrieve подписки по окончании успешно войти в систему, необходимо выполните эти действия tootroubleshoot этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="888d9-130">If you are unable tooretrieve your subscriptions after you successfully sign in, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="888d9-131">Убедитесь, что ваша учетная запись имеет доступ toohello подписок при входе в портал Azure hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-131">Verify that your account has access toohello subscriptions by signing into hello Azure Portal.</span></span>

- <span data-ttu-id="888d9-132">Убедитесь, что вы выполнили вход с использованием среды правильный hello (Azure, Azure China, Германия Azure, правительства США или настраиваемый среде и Azure стека).</span><span class="sxs-lookup"><span data-stu-id="888d9-132">Make sure that you have signed in using hello correct environment (Azure, Azure China, Azure Germany, Azure US Government, or Custom Environment/Azure Stack).</span></span>

- <span data-ttu-id="888d9-133">Если пользователь находится за прокси-сервер, убедитесь, что неправильно настроен прокси-сервера обозревателя хранилищ hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-133">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="888d9-134">Попробуйте удалить и повторное добавление учетной записи hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-134">Try removing and readding hello account.</span></span>

- <span data-ttu-id="888d9-135">Попробуйте удалить hello следующие файлы из корневого каталога (то есть, C:\Users\ContosoUser), а затем снова добавив hello учетной записи:</span><span class="sxs-lookup"><span data-stu-id="888d9-135">Try deleting hello following files from your root directory (that is, C:\Users\ContosoUser), and then re-adding hello account:</span></span>

    - <span data-ttu-id="888d9-136">adalcache-файл;</span><span class="sxs-lookup"><span data-stu-id="888d9-136">.adalcache</span></span>

    - <span data-ttu-id="888d9-137">devaccounts-файл;</span><span class="sxs-lookup"><span data-stu-id="888d9-137">.devaccounts</span></span>

    - <span data-ttu-id="888d9-138">extaccounts-файл.</span><span class="sxs-lookup"><span data-stu-id="888d9-138">.extaccounts</span></span>

- <span data-ttu-id="888d9-139">Консоль средств разработчика hello Контрольные значения (нажав клавишу F12) при входе сообщения об ошибках:</span><span class="sxs-lookup"><span data-stu-id="888d9-139">Watch hello developer tools console (by pressing F12) when you are signing in for any error messages:</span></span>

![средства разработчика](./media/storage-explorer-troubleshooting/4022501_en_2.png)

### <a name="unable-toosee-hello-authentication-page"></a><span data-ttu-id="888d9-141">Страница проверки подлинности не удается toosee hello</span><span class="sxs-lookup"><span data-stu-id="888d9-141">Unable toosee hello authentication page</span></span>

<span data-ttu-id="888d9-142">Страница проверки подлинности не удается toosee hello, необходимо выполните эти действия tootroubleshoot этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="888d9-142">If you are unable toosee hello authentication page, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="888d9-143">В зависимости от скорости подключения к hello она может занять некоторое время tooload hello страницы входа, подождите по крайней мере одну минуту, прежде чем закрыть диалоговое окно проверки подлинности hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-143">Depending on hello speed of your connection, it may take a while for hello sign-in page tooload, wait at least one minute before closing hello authentication dialog box.</span></span>

- <span data-ttu-id="888d9-144">Если пользователь находится за прокси-сервер, убедитесь, что неправильно настроен прокси-сервера обозревателя хранилищ hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-144">If you are behind a proxy, make sure that you have configured hello Storage Explorer proxy properly.</span></span>

- <span data-ttu-id="888d9-145">Представление hello в консоли разработчика, нажав клавишу F12 hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-145">View hello developer console by pressing hello F12 key.</span></span> <span data-ttu-id="888d9-146">Посмотрите hello ответов от консоли разработчика hello и ли можно найти любой выявить причину в разделе проверки подлинности не работает.</span><span class="sxs-lookup"><span data-stu-id="888d9-146">Watch hello responses from hello developer console and see whether you can find any clue for why authentication not working.</span></span>

### <a name="cannot-remove-account"></a><span data-ttu-id="888d9-147">Невозможно удалить учетную запись</span><span class="sxs-lookup"><span data-stu-id="888d9-147">Cannot remove account</span></span>

<span data-ttu-id="888d9-148">При наличии не удается tooremove учетную запись или ссылку hello повторная проверка подлинности не выполняет никаких, выполните эти действия tootroubleshoot этой проблемы:</span><span class="sxs-lookup"><span data-stu-id="888d9-148">If you are unable tooremove an account, or if hello reauthenticate link does not do anything, follow these steps tootroubleshoot this issue:</span></span>

- <span data-ttu-id="888d9-149">Попробуйте удалить hello следующие файлы из корневого каталога, а затем повторное добавление hello учетной записи:</span><span class="sxs-lookup"><span data-stu-id="888d9-149">Try deleting hello following files from your root directory, and then readding hello account:</span></span>

    - <span data-ttu-id="888d9-150">adalcache-файл;</span><span class="sxs-lookup"><span data-stu-id="888d9-150">.adalcache</span></span>

    - <span data-ttu-id="888d9-151">devaccounts-файл;</span><span class="sxs-lookup"><span data-stu-id="888d9-151">.devaccounts</span></span>

    - <span data-ttu-id="888d9-152">extaccounts-файл.</span><span class="sxs-lookup"><span data-stu-id="888d9-152">.extaccounts</span></span>

- <span data-ttu-id="888d9-153">Если вы хотите tooremove SAS присоединенного ресурсов хранения, удалите hello следующие файлы:</span><span class="sxs-lookup"><span data-stu-id="888d9-153">If you want tooremove SAS attached Storage resources, delete hello following files:</span></span>

    - <span data-ttu-id="888d9-154">папку %AppData%/StorageExplorer в Windows;</span><span class="sxs-lookup"><span data-stu-id="888d9-154">%AppData%/StorageExplorer folder for Windows</span></span>

    - <span data-ttu-id="888d9-155">/Users/<ваше_имя>/Library/Applicaiton SUpport/StorageExplorer в Mac;</span><span class="sxs-lookup"><span data-stu-id="888d9-155">/Users/<your_name>/Library/Applicaiton SUpport/StorageExplorer for Mac</span></span>

    - <span data-ttu-id="888d9-156">~/.config/StorageExplorer в Linux.</span><span class="sxs-lookup"><span data-stu-id="888d9-156">~/.config/StorageExplorer for Linux</span></span>

> [!NOTE]
>  <span data-ttu-id="888d9-157">Вы получите tooreenter свои учетные данные при удалении этих файлов.</span><span class="sxs-lookup"><span data-stu-id="888d9-157">You will have tooreenter all your credentials if you delete these files.</span></span>

## <a name="proxy-issues"></a><span data-ttu-id="888d9-158">Проблемы с прокси-сервером</span><span class="sxs-lookup"><span data-stu-id="888d9-158">Proxy issues</span></span>

<span data-ttu-id="888d9-159">Во-первых убедитесь, что hello, что следующие сведения, введенные верны:</span><span class="sxs-lookup"><span data-stu-id="888d9-159">First, make sure that hello following information you entered are all correct:</span></span>

- <span data-ttu-id="888d9-160">Здравствуйте, URL-адрес прокси-сервера и порт номер</span><span class="sxs-lookup"><span data-stu-id="888d9-160">hello proxy URL and port number</span></span>

- <span data-ttu-id="888d9-161">Имя пользователя и пароль, если это требуется для hello прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="888d9-161">Username and password if required by hello proxy</span></span>

### <a name="common-solutions"></a><span data-ttu-id="888d9-162">Распространенные решения</span><span class="sxs-lookup"><span data-stu-id="888d9-162">Common solutions</span></span>

<span data-ttu-id="888d9-163">Если вы по-прежнему возникают проблемы, выполните эти шаги tootroubleshoot их:</span><span class="sxs-lookup"><span data-stu-id="888d9-163">If you are still experiencing issues, follow these steps tootroubleshoot them:</span></span>

- <span data-ttu-id="888d9-164">Если toohello Интернет можно подключиться без использования прокси-сервера, убедиться, что обозреватель хранилищ работает без включены параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="888d9-164">If you can connect toohello Internet without using your proxy, verify that Storage Explorer works without proxy settings enabled.</span></span> <span data-ttu-id="888d9-165">Если это так hello, может быть проблема с параметры прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="888d9-165">If this is hello case, there may be an issue with your proxy settings.</span></span> <span data-ttu-id="888d9-166">Работа с вашей проблемы hello tooidentify администратору прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="888d9-166">Work with your proxy administrator tooidentify hello problems.</span></span>

- <span data-ttu-id="888d9-167">Убедитесь, что другие приложения, использующие hello прокси-сервер работать должным образом.</span><span class="sxs-lookup"><span data-stu-id="888d9-167">Verify that other applications using hello proxy server work as expected.</span></span>

- <span data-ttu-id="888d9-168">Убедитесь, что можно подключиться с помощью веб-браузере портал Microsoft Azure toohello</span><span class="sxs-lookup"><span data-stu-id="888d9-168">Verify that you can connect toohello Microsoft Azure portal using your web browser</span></span>

- <span data-ttu-id="888d9-169">Убедитесь, что вы можете получать ответы от конечных точек службы.</span><span class="sxs-lookup"><span data-stu-id="888d9-169">Verify that you can receive responses from your service endpoints.</span></span> <span data-ttu-id="888d9-170">Введите один из URL-адресов конечной точки в браузере.</span><span class="sxs-lookup"><span data-stu-id="888d9-170">Enter one of your endpoint URLs into your browser.</span></span> <span data-ttu-id="888d9-171">Если вам удается подключиться, вы должны получить ответ InvalidQueryParameterValue или аналогичный XML-ответ.</span><span class="sxs-lookup"><span data-stu-id="888d9-171">If you can connect, you should receive an InvalidQueryParameterValue or similar XML response.</span></span>

- <span data-ttu-id="888d9-172">Если другие пользователи также используют обозреватель хранилищ с вашим прокси-сервером, проверьте, могут ли они подключаться.</span><span class="sxs-lookup"><span data-stu-id="888d9-172">If someone else is also using Storage Explorer with your proxy server, verify that they can connect.</span></span> <span data-ttu-id="888d9-173">Если они могут подключаться, возможно toocontact администратору сервера прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="888d9-173">If they can connect, you may have toocontact your proxy server admin.</span></span>

### <a name="tools-for-diagnosing-issues"></a><span data-ttu-id="888d9-174">Инструменты для выявления проблем</span><span class="sxs-lookup"><span data-stu-id="888d9-174">Tools for diagnosing issues</span></span>

<span data-ttu-id="888d9-175">При наличии сетевых средств, таких как Fiddler для Windows может toodiagnose hello проблемы может быть следующим:</span><span class="sxs-lookup"><span data-stu-id="888d9-175">If you have networking tools, such as Fiddler for Windows, you may be able toodiagnose hello problems as follows:</span></span>

- <span data-ttu-id="888d9-176">Если у вас есть toowork через прокси-сервер, возможно tooconfigure вашей сети tooconnect средство через прокси-сервер hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-176">If you have toowork through your proxy, you may have tooconfigure your networking tool tooconnect through hello proxy.</span></span>

- <span data-ttu-id="888d9-177">Проверьте hello номер порта, используемый средством вашей сети.</span><span class="sxs-lookup"><span data-stu-id="888d9-177">Check hello port number used by your networking tool.</span></span>

- <span data-ttu-id="888d9-178">Введите URL-адрес локального узла hello и hello сети номер порта данного средства, как параметры прокси-сервера в обозревателе хранилищ.</span><span class="sxs-lookup"><span data-stu-id="888d9-178">Enter hello local host URL and hello networking tool's port number as proxy settings in Storage Explorer.</span></span> <span data-ttu-id="888d9-179">Если этот isdone правильно, вашей сети в отобразившемся сетевые запросы, сделанные обозреватель хранилищ toomanagement конечными точками и службы ведения журнала.</span><span class="sxs-lookup"><span data-stu-id="888d9-179">If this isdone correctly, your networking tool starts logging network requests made by Storage Explorer toomanagement and service endpoints.</span></span> <span data-ttu-id="888d9-180">Например, введите https://cawablobgrs.blob.core.windows.net/ для конечной точки большого двоичного объекта в браузере и будет получен ответ, аналогичные ниже hello, т. е. ресурс hello существует, несмотря на то, что они недоступны.</span><span class="sxs-lookup"><span data-stu-id="888d9-180">For example, enter https://cawablobgrs.blob.core.windows.net/ for your blob endpoint in a browser, and you will receive a response resembles hello following, which suggests hello resource exists, although you cannot access it.</span></span>

![пример кода](./media/storage-explorer-troubleshooting/4022502_en_2.png)

### <a name="contact-proxy-server-admin"></a><span data-ttu-id="888d9-182">Обратитесь к администратору прокси-сервера</span><span class="sxs-lookup"><span data-stu-id="888d9-182">Contact proxy server admin</span></span>

<span data-ttu-id="888d9-183">Если правильные параметры прокси-сервера, возможно, toocontact администратору сервера прокси-сервера и</span><span class="sxs-lookup"><span data-stu-id="888d9-183">If your proxy settings are correct, you may have toocontact your proxy server admin, and</span></span>

- <span data-ttu-id="888d9-184">Убедитесь, что прокси-сервер не блокирует трафик tooAzure конечные точки управления или ресурс.</span><span class="sxs-lookup"><span data-stu-id="888d9-184">Make sure that your proxy does not block traffic tooAzure management or resource endpoints.</span></span>

- <span data-ttu-id="888d9-185">Проверьте hello протокол проверки подлинности, используемые прокси-сервер.</span><span class="sxs-lookup"><span data-stu-id="888d9-185">Verify hello authentication protocol used by your proxy server.</span></span> <span data-ttu-id="888d9-186">Обозреватель хранилищ пока не поддерживает прокси-серверы NTLM.</span><span class="sxs-lookup"><span data-stu-id="888d9-186">Storage Explorer does not currently support NTLM proxies.</span></span>

## <a name="unable-tooretrieve-children-error-message"></a><span data-ttu-id="888d9-187">Сообщение об ошибке «Не удается tooRetrieve дочерние элементы»</span><span class="sxs-lookup"><span data-stu-id="888d9-187">"Unable tooRetrieve Children" error message</span></span>

<span data-ttu-id="888d9-188">При наличии подключенных tooAzure через прокси, проверьте правильность параметров прокси-сервера.</span><span class="sxs-lookup"><span data-stu-id="888d9-188">If you are connected tooAzure through a proxy, verify that your proxy settings are correct.</span></span> <span data-ttu-id="888d9-189">Если были предоставлены ресурсов tooa доступ у владельца hello hello подписки или учетной записи, убедитесь, что прочли или список разрешений для этого ресурса.</span><span class="sxs-lookup"><span data-stu-id="888d9-189">If you were granted access tooa resource from hello owner of hello subscription or account, verify that you have read or list permissions for that resource.</span></span>

### <a name="issues-with-sas-url"></a><span data-ttu-id="888d9-190">Проблемы с URL-адресом SAS</span><span class="sxs-lookup"><span data-stu-id="888d9-190">Issues with SAS URL</span></span>
<span data-ttu-id="888d9-191">Если вы подключаетесь tooa службы с помощью URL-адрес SAS и возникновении данной ошибки:</span><span class="sxs-lookup"><span data-stu-id="888d9-191">If you are connecting tooa service using a SAS URL and experiencing this error:</span></span>

- <span data-ttu-id="888d9-192">Убедитесь, hello URL-адрес содержит необходимые разрешения hello tooread или списка ресурсов.</span><span class="sxs-lookup"><span data-stu-id="888d9-192">Verify that hello URL provides hello necessary permissions tooread or list resources.</span></span>

- <span data-ttu-id="888d9-193">Убедитесь, что hello URL-адрес не истек.</span><span class="sxs-lookup"><span data-stu-id="888d9-193">Verify that hello URL has not expired.</span></span>

- <span data-ttu-id="888d9-194">Если hello URL-адрес SAS основана на политику доступа, убедитесь, что политика доступа hello не был отозван.</span><span class="sxs-lookup"><span data-stu-id="888d9-194">If hello SAS URL is based on an access policy, verify that hello access policy has not been revoked.</span></span>

## <a name="next-steps"></a><span data-ttu-id="888d9-195">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="888d9-195">Next steps</span></span>

<span data-ttu-id="888d9-196">Если ни одно из решений hello решить, отправить вашей проблеме с помощью средства обратной связи hello с ваш адрес электронной почты и столько подробные сведения о проблеме hello, включенных в ходе можно так, что мы можем связаться с вами для устранения проблемы с hello.</span><span class="sxs-lookup"><span data-stu-id="888d9-196">If none of hello solutions work for you, submit your issue through hello feedback tool with your email and as many details about hello issue included as you can, so that we can contact you for fixing hello issue.</span></span>

<span data-ttu-id="888d9-197">toodo, нажмите кнопку **справки** меню, а затем нажмите **отправить отзыв**.</span><span class="sxs-lookup"><span data-stu-id="888d9-197">toodo this, click **Help** menu, and then click **Send Feedback**.</span></span>

![Отзыв](./media/storage-explorer-troubleshooting/4022503_en_1.png)
