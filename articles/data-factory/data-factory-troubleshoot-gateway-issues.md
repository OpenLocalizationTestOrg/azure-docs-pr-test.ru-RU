---
title: "Устранение неполадок шлюза управления данными | Документация Майкрософт"
description: "Эта статья содержит советы по устранению неполадок, связанных со шлюзом управления данными."
services: data-factory
author: nabhishek
manager: jhubbard
editor: monicar
ms.assetid: c6756c37-4e5a-4d1e-ab52-365f149b4128
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: abnarain
published: True
ms.openlocfilehash: b8e50a4e3c0b9c535ccc2344ff22261a356d5acc
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="92115-103">Устранение неполадок в работе шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="92115-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="92115-104">В этой статье приводятся сведения об устранении неполадок в работе шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="92115-105">Подробные сведения о шлюзе см. в статье [Шлюз управления данными](data-factory-data-management-gateway.md).</span><span class="sxs-lookup"><span data-stu-id="92115-105">See the [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about the gateway.</span></span> <span data-ttu-id="92115-106">Сведения о пошаговом перемещении данных из локальной базы данных SQL Server в хранилище BLOB-объектов Microsoft Azure с помощью шлюза см. в статье [Перемещение данных между локальными источниками и облаком с помощью шлюза управления данными](data-factory-move-data-between-onprem-and-cloud.md).</span><span class="sxs-lookup"><span data-stu-id="92115-106">See the [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database to Microsoft Azure Blob storage by using the gateway.</span></span>
>
>

## <a name="failed-to-install-or-register-gateway"></a><span data-ttu-id="92115-107">Не удалось установить и зарегистрировать шлюз</span><span class="sxs-lookup"><span data-stu-id="92115-107">Failed to install or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="92115-108">1. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-108">1. Problem</span></span>
<span data-ttu-id="92115-109">Это сообщение об ошибке отображается при установке и регистрации шлюза, а именно при скачивании файла установки шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-109">You see this error message when installing and registering a gateway, specifically, while downloading the gateway installation file.</span></span>

`Unable to connect to the remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="92115-110">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-110">Cause</span></span>
<span data-ttu-id="92115-111">Компьютеру, на который вы пытаетесь установить шлюз, не удалось скачать последний файл установки шлюза из центра загрузки из-за проблемы в сети.</span><span class="sxs-lookup"><span data-stu-id="92115-111">The machine on which you are trying to install the gateway has failed to download the latest gateway installation file from the download center due to a network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-112">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-112">Resolution</span></span>
<span data-ttu-id="92115-113">Проверьте параметры прокси-сервера брандмауэра, чтобы определить, не блокируют ли эти параметры сетевое подключение компьютера к [центру загрузки](https://download.microsoft.com/), и измените их соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="92115-113">Check your firewall proxy server settings to see whether the settings block the network connection from the computer to the [download center](https://download.microsoft.com/), and update the settings accordingly.</span></span>

<span data-ttu-id="92115-114">Или можно скачать файл установки последнего шлюза из [центра загрузки](https://www.microsoft.com/download/details.aspx?id=39717) на других компьютерах, которые могут подключаться к центру загрузки.</span><span class="sxs-lookup"><span data-stu-id="92115-114">Alternatively, you can download the installation file for the latest gateway from the [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access the download center.</span></span> <span data-ttu-id="92115-115">Затем можно скопировать файл установщика на главный компьютер шлюза и запустить его вручную, чтобы установить и обновить шлюз.</span><span class="sxs-lookup"><span data-stu-id="92115-115">You can then copy the installer file to the gateway host computer and run it manually to install and update the gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="92115-116">2) Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-116">2. Problem</span></span>
<span data-ttu-id="92115-117">Эта ошибка возникает при попытке установить шлюз с помощью ссылки **Установка непосредственно на этот компьютер** на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="92115-117">You see this error when you're attempting to install a gateway by clicking **install directly on this computer** in the Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="92115-118">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-118">Cause</span></span>
<span data-ttu-id="92115-119">Шлюз уже установлен на компьютере.</span><span class="sxs-lookup"><span data-stu-id="92115-119">A gateway is already installed on the machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-120">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-120">Resolution</span></span>
<span data-ttu-id="92115-121">Удалите существующий шлюз на компьютере и снова щелкните ссылку **Установка непосредственно на этот компьютер**.</span><span class="sxs-lookup"><span data-stu-id="92115-121">Uninstall the existing gateway on the machine and click the **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="92115-122">3. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-122">3. Problem</span></span>
<span data-ttu-id="92115-123">Эта ошибка может возникнуть при регистрации нового шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-123">You might see this error when registering a new gateway.</span></span>

`Error: The gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="92115-124">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-124">Cause</span></span>
<span data-ttu-id="92115-125">Это сообщение может отображаться по одной из следующих причин:</span><span class="sxs-lookup"><span data-stu-id="92115-125">You might see this message for one of the following reasons:</span></span>

* <span data-ttu-id="92115-126">недопустимый формат ключа шлюза;</span><span class="sxs-lookup"><span data-stu-id="92115-126">The format of the gateway key is invalid.</span></span>
* <span data-ttu-id="92115-127">ключ шлюза стал недействительным;</span><span class="sxs-lookup"><span data-stu-id="92115-127">The gateway key has been invalidated.</span></span>
* <span data-ttu-id="92115-128">ключ шлюза создан повторно на портале.</span><span class="sxs-lookup"><span data-stu-id="92115-128">The gateway key has been regenerated from the portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="92115-129">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-129">Resolution</span></span>
<span data-ttu-id="92115-130">Просмотрите сведения на портале, чтобы убедиться, что используется правильный ключ шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-130">Verify whether you are using the right gateway key from the portal.</span></span> <span data-ttu-id="92115-131">При необходимости повторно создайте ключ и зарегистрируйте шлюз с его помощью.</span><span class="sxs-lookup"><span data-stu-id="92115-131">If needed, regenerate a key and use the key to register the gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="92115-132">4. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-132">4. Problem</span></span>
<span data-ttu-id="92115-133">При регистрации шлюза может появиться следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="92115-133">You might see the following error message when you're registering a gateway.</span></span>

`Error: The content or format of the gateway key "{gatewayKey}" is invalid, please go to azure portal to create one new gateway or regenerate the gateway key.`



![Недопустимое содержимое или формат ключа](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="92115-135">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-135">Cause</span></span>
<span data-ttu-id="92115-136">Содержимое или формат входного ключа шлюза неправильные.</span><span class="sxs-lookup"><span data-stu-id="92115-136">The content or format of the input gateway key is incorrect.</span></span> <span data-ttu-id="92115-137">Одной из причин может быть копирование части ключа на портале или использование недопустимого ключа.</span><span class="sxs-lookup"><span data-stu-id="92115-137">One of the reasons can be that you copied only a portion of the key from the portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-138">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-138">Resolution</span></span>
<span data-ttu-id="92115-139">Создайте ключ шлюза на портале и скопируйте весь ключ с помощью кнопки копирования.</span><span class="sxs-lookup"><span data-stu-id="92115-139">Generate a gateway key in the portal, and use the copy button to copy the whole key.</span></span> <span data-ttu-id="92115-140">Затем вставьте его в это окно, чтобы зарегистрировать шлюз.</span><span class="sxs-lookup"><span data-stu-id="92115-140">Then paste it in this window to register the gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="92115-141">5. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-141">5. Problem</span></span>
<span data-ttu-id="92115-142">При регистрации шлюза может появиться следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="92115-142">You might see the following error message when you're registering a gateway.</span></span>

`Error: The gateway key is invalid or empty. Specify a valid gateway key from the portal.`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="92115-144">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-144">Cause</span></span>
<span data-ttu-id="92115-145">Ключ шлюза создан повторно или шлюз удален на портале Azure.</span><span class="sxs-lookup"><span data-stu-id="92115-145">The gateway key has been regenerated or the gateway has been deleted in the Azure portal.</span></span> <span data-ttu-id="92115-146">Это также может произойти, если установлена не последняя версия шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-146">It can also happen if the Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-147">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-147">Resolution</span></span>
<span data-ttu-id="92115-148">Проверьте, установлена ли последняя версия шлюза управления данными. Последнюю версию можно найти в [Центре загрузки Майкрософт](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="92115-148">Check if the Data Management Gateway setup is the latest version, you can find the latest version on the Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="92115-149">Если установлена актуальная (последняя) версия и шлюз существует на портале, повторно создайте ключ шлюза на портале Azure, скопируйте весь ключ, нажав кнопку "Копировать", и вставьте его в это окно, чтобы зарегистрировать шлюз.</span><span class="sxs-lookup"><span data-stu-id="92115-149">If setup is current/ latest and gateway still exists on Portal, regenerate the gateway key in the Azure portal, and use the copy button to copy the whole key, and then paste it in this window to register the gateway.</span></span> <span data-ttu-id="92115-150">В противном случае повторно создайте шлюз и начните заново.</span><span class="sxs-lookup"><span data-stu-id="92115-150">Otherwise, recreate the gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="92115-151">6. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-151">6. Problem</span></span>
<span data-ttu-id="92115-152">При регистрации шлюза может появиться следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="92115-152">You might see the following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with the status “Gateway key is invalid”`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="92115-154">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-154">Cause</span></span>
<span data-ttu-id="92115-155">Эта ошибка может возникать из-за удаления шлюза или повторного создания ключа соответствующего шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-155">This error might happen because either the gateway has been deleted or the associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-156">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-156">Resolution</span></span>
<span data-ttu-id="92115-157">Если шлюз был удален, заново создайте его на портале, нажмите кнопку **Зарегистрировать**, скопируйте ключ с портала, вставьте его и попытайтесь зарегистрировать шлюз.</span><span class="sxs-lookup"><span data-stu-id="92115-157">If the gateway has been deleted, re-create the gateway from the portal, click **Register**, copy the key from the portal, paste it, and try to register the gateway.</span></span>

<span data-ttu-id="92115-158">Если шлюз существует, но его ключ был создан повторно, зарегистрируйте шлюз, используя новый ключ.</span><span class="sxs-lookup"><span data-stu-id="92115-158">If the gateway still exists but its key has been regenerated, use the new key to register the gateway.</span></span> <span data-ttu-id="92115-159">Если у вас нет ключа, повторно создайте его на портале.</span><span class="sxs-lookup"><span data-stu-id="92115-159">If you don’t have the key, regenerate the key again from the portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="92115-160">7. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-160">7. Problem</span></span>
<span data-ttu-id="92115-161">При регистрации шлюза может потребоваться ввести путь и пароль к сертификату.</span><span class="sxs-lookup"><span data-stu-id="92115-161">When you're registering a gateway, you might need to enter path and password for a certificate.</span></span>

![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="92115-163">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-163">Cause</span></span>
<span data-ttu-id="92115-164">Этот шлюз ранее зарегистрирован на других компьютерах.</span><span class="sxs-lookup"><span data-stu-id="92115-164">The gateway has been registered on other machines before.</span></span> <span data-ttu-id="92115-165">Во время первоначальной регистрации шлюза с ним связывается сертификат шифрования.</span><span class="sxs-lookup"><span data-stu-id="92115-165">During the initial registration of a gateway, an encryption certificate has been associated with the gateway.</span></span> <span data-ttu-id="92115-166">Сертификат может быть создан шлюзом или предоставлен пользователем.</span><span class="sxs-lookup"><span data-stu-id="92115-166">The certificate can either be self-generated by the gateway or provided by the user.</span></span>  <span data-ttu-id="92115-167">Этот сертификат используется для шифрования учетных данных хранилища данных (связанные службы).</span><span class="sxs-lookup"><span data-stu-id="92115-167">This certificate is used to encrypt credentials of the data store (linked service).</span></span>  

![Экспорт сертификата](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="92115-169">При восстановлении шлюза на другом хост-компьютере мастер регистрации запрашивает этот сертификат для расшифровки учетных данных, зашифрованных с его помощью.</span><span class="sxs-lookup"><span data-stu-id="92115-169">When restoring the gateway on a different host machine, the registration wizard asks for this certificate to decrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="92115-170">Без этого сертификата новому шлюзу не удастся расшифровать учетные данные, а последующие действия копирования, связанные с этим новым шлюзом, будут завершаться ошибкой.</span><span class="sxs-lookup"><span data-stu-id="92115-170">Without this certificate, the credentials cannot be decrypted by the new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="92115-171">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-171">Resolution</span></span>
<span data-ttu-id="92115-172">Если сертификат учетных данных экспортирован с исходного компьютера шлюза с помощью кнопки **Экспорт** на вкладке **Параметры** в диспетчере конфигураций шлюза управления данными, используйте сертификат отсюда.</span><span class="sxs-lookup"><span data-stu-id="92115-172">If you have exported the credential certificate from the original gateway machine by using the **Export** button on the **Settings** tab in Data Management Gateway Configuration Manager, use the certificate here.</span></span>

<span data-ttu-id="92115-173">Нельзя пропускать этот шаг при восстановлении шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="92115-174">Если сертификат отсутствует, необходимо удалить шлюз на портале и заново создать его.</span><span class="sxs-lookup"><span data-stu-id="92115-174">If the certificate is missing, you need to delete the gateway from the portal and re-create a new gateway.</span></span>  <span data-ttu-id="92115-175">Также следует обновить все связанные службы шлюза. Для этого нужно повторно ввести их учетные данные.</span><span class="sxs-lookup"><span data-stu-id="92115-175">In addition, update all linked services that are related to the gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="92115-176">8. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-176">8. Problem</span></span>
<span data-ttu-id="92115-177">Вы можете получить следующее сообщение об ошибке.</span><span class="sxs-lookup"><span data-stu-id="92115-177">You might see the following error message.</span></span>

`Error: The remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="92115-178">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-178">Cause</span></span>
<span data-ttu-id="92115-179">Эта ошибка возникает, если шлюз находится в среде, которой для доступа к интернет-ресурсам требуется прокси-сервер HTTP, или если пароль для аутентификации прокси-сервера изменился, но не обновился соответствующим образом в шлюзе.</span><span class="sxs-lookup"><span data-stu-id="92115-179">This error happens when your gateway is in an environment that requires an HTTP proxy to access Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-180">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-180">Resolution</span></span>
<span data-ttu-id="92115-181">Следуйте инструкциям в разделе [Рекомендации для прокси-сервера](#proxy-server-considerations) в этой статье и настройте параметры прокси-сервера с помощью диспетчера конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-181">Follow the instructions in the [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="92115-182">Шлюз находится в сети с ограниченной функциональностью</span><span class="sxs-lookup"><span data-stu-id="92115-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="92115-183">1. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-183">1. Problem</span></span>
<span data-ttu-id="92115-184">Шлюз находится в состоянии "в сети с ограниченной функциональностью".</span><span class="sxs-lookup"><span data-stu-id="92115-184">You see the status of the gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="92115-185">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-185">Cause</span></span>
<span data-ttu-id="92115-186">Шлюз может находиться в состоянии "в сети с ограниченной функциональностью" по одной из следующих причин:</span><span class="sxs-lookup"><span data-stu-id="92115-186">You see the status of the gateway as online with limited functionality for one of the following reasons:</span></span>

* <span data-ttu-id="92115-187">шлюзу не удается подключиться к облачной службе через служебную шину Azure;</span><span class="sxs-lookup"><span data-stu-id="92115-187">Gateway cannot connect to cloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="92115-188">облачной службе не удается подключиться к шлюзу через служебную шину.</span><span class="sxs-lookup"><span data-stu-id="92115-188">Cloud service cannot connect to gateway through Service Bus.</span></span>

<span data-ttu-id="92115-189">Если шлюз находится в сети с ограниченной функциональностью, вы не сможете использовать мастер копирования фабрики данных, чтобы создавать конвейеры данных для копирования данных между локальными хранилищами данных.</span><span class="sxs-lookup"><span data-stu-id="92115-189">When the gateway is online with limited functionality, you might not be able to use the Data Factory Copy Wizard to create data pipelines for copying data to or from on-premises data stores.</span></span> <span data-ttu-id="92115-190">Для решения проблемы можно использовать редактор фабрики данных на портале, Visual Studio или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="92115-190">As a workaround, you can use Data Factory Editor in the portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-191">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-191">Resolution</span></span>
<span data-ttu-id="92115-192">Устранить эту проблему (состояние "в сети с ограниченной функциональностью") можно, определив ее причину (например, шлюзу не удается подключиться к облачной службе).</span><span class="sxs-lookup"><span data-stu-id="92115-192">Resolution for this issue (online with limited functionality) is based on whether the gateway cannot connect to the cloud service or the other way.</span></span> <span data-ttu-id="92115-193">В следующих разделах описываются эти методы устранения проблемы.</span><span class="sxs-lookup"><span data-stu-id="92115-193">The following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="92115-194">2. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-194">2. Problem</span></span>
<span data-ttu-id="92115-195">Возникла следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="92115-195">You see the following error.</span></span>

`Error: Gateway cannot connect to cloud service through service bus`

![Шлюзу не удается подключиться к облачной службе](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="92115-197">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-197">Cause</span></span>
<span data-ttu-id="92115-198">Шлюзу не удается подключиться к облачной службе через служебную шину.</span><span class="sxs-lookup"><span data-stu-id="92115-198">Gateway cannot connect to the cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-199">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-199">Resolution</span></span>
<span data-ttu-id="92115-200">Выполните следующие действия, чтобы перевести шлюз в состояние "в сети".</span><span class="sxs-lookup"><span data-stu-id="92115-200">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="92115-201">Разрешите правила для исходящих подключений по IP-адресам на компьютере шлюза и в корпоративном брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="92115-201">Allow IP address outbound rules on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="92115-202">IP-адреса можно найти в журнале событий Windows (идентификатор 401): "Попытка доступа к сокету методом, запрещенным его разрешениями на доступ XX.XX.XX.XX:9350".</span><span class="sxs-lookup"><span data-stu-id="92115-202">You can find IP addresses from the Windows Event Log (ID == 401): An attempt was made to access a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="92115-203">Настройте параметры прокси-сервера на шлюзе.</span><span class="sxs-lookup"><span data-stu-id="92115-203">Configure proxy settings on the gateway.</span></span> <span data-ttu-id="92115-204">Дополнительные сведения см. в разделе [Рекомендации для прокси-сервера](#proxy-server-considerations).</span><span class="sxs-lookup"><span data-stu-id="92115-204">See the [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="92115-205">Откройте исходящие порты 5671 и 9350–9354 в брандмауэре Windows на компьютере шлюза и в корпоративном брандмауэре.</span><span class="sxs-lookup"><span data-stu-id="92115-205">Enable outbound ports 5671 and 9350-9354 on both the Windows Firewall on the gateway machine and the corporate firewall.</span></span> <span data-ttu-id="92115-206">Дополнительные сведения см. в разделе [Порты и брандмауэр](#ports-and-firewall).</span><span class="sxs-lookup"><span data-stu-id="92115-206">See the [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="92115-207">Это делать не обязательно, но рекомендуется из соображений производительности.</span><span class="sxs-lookup"><span data-stu-id="92115-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="92115-208">3. Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-208">3. Problem</span></span>
<span data-ttu-id="92115-209">Возникла следующая ошибка:</span><span class="sxs-lookup"><span data-stu-id="92115-209">You see the following error.</span></span>

`Error: Cloud service cannot connect to gateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="92115-210">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-210">Cause</span></span>
<span data-ttu-id="92115-211">Временная ошибка подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="92115-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-212">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-212">Resolution</span></span>
<span data-ttu-id="92115-213">Выполните следующие действия, чтобы перевести шлюз в состояние "в сети".</span><span class="sxs-lookup"><span data-stu-id="92115-213">Follow these steps to get the gateway back online:</span></span>

1. <span data-ttu-id="92115-214">Подождите несколько минут. Подключение восстановится автоматически после устранения ошибки.</span><span class="sxs-lookup"><span data-stu-id="92115-214">Wait for a couple of minutes, the connectivity will be automatically recovered when the error is gone.</span></span>
* <span data-ttu-id="92115-215">Если ошибка не исчезнет, перезапустите службу шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-215">If the error persists, restart the gateway service.</span></span>

## <a name="failed-to-author-linked-service"></a><span data-ttu-id="92115-216">Не удалось создать связанную службу</span><span class="sxs-lookup"><span data-stu-id="92115-216">Failed to author linked service</span></span>
### <a name="problem"></a><span data-ttu-id="92115-217">Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-217">Problem</span></span>
<span data-ttu-id="92115-218">Эта ошибка может возникнуть при попытке использовать диспетчер учетных данных на портале, чтобы ввести учетные данные для новой связанной службы или обновить учетные данные для существующей связанной службы.</span><span class="sxs-lookup"><span data-stu-id="92115-218">You might see this error when you try to use Credential Manager in the portal to input credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: The data store '<Server>/<Database>' cannot be reached. Check connection settings for the data source.`

<span data-ttu-id="92115-219">При появлении этой ошибки страница параметров диспетчера конфигураций шлюза управления данными может выглядеть, как на следующем снимке экрана.</span><span class="sxs-lookup"><span data-stu-id="92115-219">When you see this error, the settings page of Data Management Gateway Configuration Manager might look like the following screenshot.</span></span>

![Не удается получить доступ к базе данных](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="92115-221">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-221">Cause</span></span>
<span data-ttu-id="92115-222">Возможно, SSL-сертификат утерян на компьютере шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-222">The SSL certificate might have been lost on the gateway machine.</span></span> <span data-ttu-id="92115-223">Компьютеру шлюза не удалось загрузить сертификат, используемый для шифрования SSL.</span><span class="sxs-lookup"><span data-stu-id="92115-223">The gateway computer cannot load the certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="92115-224">Кроме того, в журнале событий также может появиться сообщение об ошибке примерно следующего вида.</span><span class="sxs-lookup"><span data-stu-id="92115-224">You might also see an error message in the event log that is similar to the following message.</span></span>

 `Unable to get the gateway settings from cloud service. Check the gateway key and the network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="92115-225">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-225">Resolution</span></span>
<span data-ttu-id="92115-226">Чтобы решить проблему, сделайте следующее:</span><span class="sxs-lookup"><span data-stu-id="92115-226">Follow these steps to solve the problem:</span></span>

1. <span data-ttu-id="92115-227">Запустите диспетчер конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="92115-228">Переключитесь на вкладку **Параметры** .</span><span class="sxs-lookup"><span data-stu-id="92115-228">Switch to the **Settings** tab.</span></span>  
3. <span data-ttu-id="92115-229">Нажмите кнопку **Изменить**, чтобы изменить SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="92115-229">Click the **Change** button to change the SSL certificate.</span></span>

   ![Кнопка "Изменить" для сертификата](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="92115-231">Выберите новый сертификат в качестве SSL-сертификата.</span><span class="sxs-lookup"><span data-stu-id="92115-231">Select a new certificate as the SSL certificate.</span></span> <span data-ttu-id="92115-232">Вы можете использовать собственный или корпоративный SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="92115-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="92115-234">Сбой действия копирования</span><span class="sxs-lookup"><span data-stu-id="92115-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="92115-235">Проблема</span><span class="sxs-lookup"><span data-stu-id="92115-235">Problem</span></span>
<span data-ttu-id="92115-236">После настройки конвейера на портале может возникнуть следующая ошибка UserErrorFailedToConnectToSqlserver.</span><span class="sxs-lookup"><span data-stu-id="92115-236">You might notice the following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in the portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect to SQL Server`

#### <a name="cause"></a><span data-ttu-id="92115-237">Причина:</span><span class="sxs-lookup"><span data-stu-id="92115-237">Cause</span></span>
<span data-ttu-id="92115-238">Она может возникнуть по разным причинам, от которых зависят и способы ее устранения.</span><span class="sxs-lookup"><span data-stu-id="92115-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="92115-239">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="92115-239">Resolution</span></span>
<span data-ttu-id="92115-240">Разрешите исходящие TCP-подключения через порт TCP/1433 на стороне клиента шлюза управления данными перед подключением к базе данных SQL.</span><span class="sxs-lookup"><span data-stu-id="92115-240">Allow outbound TCP connections over port TCP/1433 on the Data Management Gateway client side before connecting to an SQL database.</span></span>

<span data-ttu-id="92115-241">Если в качестве целевой базы данных используется база данных SQL Azure, проверьте также параметры брандмауэра SQL Server для Azure.</span><span class="sxs-lookup"><span data-stu-id="92115-241">If the target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="92115-242">Инструкции по проверке подключения к локальному хранилищу данных см. в следующем разделе.</span><span class="sxs-lookup"><span data-stu-id="92115-242">See the following section to test the connection to the on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="92115-243">Ошибки, связанные с подключением к хранилищу данных или с драйверами</span><span class="sxs-lookup"><span data-stu-id="92115-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="92115-244">Если возникают ошибки, связанные с подключением к хранилищу данных или с драйверами, выполните перечисленные ниже действия.</span><span class="sxs-lookup"><span data-stu-id="92115-244">If you see data store connection or driver-related errors, complete the following steps:</span></span>

1. <span data-ttu-id="92115-245">На компьютере шлюза запустите диспетчер конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-245">Start Data Management Gateway Configuration Manager on the gateway machine.</span></span>
2. <span data-ttu-id="92115-246">Перейдите на вкладку **Диагностика** .</span><span class="sxs-lookup"><span data-stu-id="92115-246">Switch to the **Diagnostics** tab.</span></span>
3. <span data-ttu-id="92115-247">В разделе **Проверка подключения** добавьте значения для группы шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-247">In **Test Connection**, add the gateway group values.</span></span>
4. <span data-ttu-id="92115-248">Нажмите кнопку **Тестировать**, чтобы проверить возможность подключения к локальному источнику данных с компьютера шлюза, используя сведения о подключении и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="92115-248">Click **Test** to see if you can connect to the on-premises data source from the gateway machine by using the connection information and credentials.</span></span> <span data-ttu-id="92115-249">Если после установки драйвера тестовое подключение по-прежнему не работает, перезапустите шлюз для того, чтобы получить последние изменения.</span><span class="sxs-lookup"><span data-stu-id="92115-249">If the test connection still fails after you install a driver, restart the gateway for it to pick up the latest change.</span></span>

![Раздел "Проверить подключение" на вкладке "Диагностика"](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="92115-251">Журналы шлюза</span><span class="sxs-lookup"><span data-stu-id="92115-251">Gateway logs</span></span>
### <a name="send-gateway-logs-to-microsoft"></a><span data-ttu-id="92115-252">Отправка журналов шлюза в корпорацию Майкрософт</span><span class="sxs-lookup"><span data-stu-id="92115-252">Send gateway logs to Microsoft</span></span>
<span data-ttu-id="92115-253">Возможно, при обращении в службу поддержки Майкрософт с проблемами в работе шлюза вас попросят предоставить журналы шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-253">When you contact Microsoft Support to get help with troubleshooting gateway issues, you might be asked to share your gateway logs.</span></span> <span data-ttu-id="92115-254">Выпуск шлюза позволяет предоставить требуемые журналы всего двумя щелчками в диспетчере конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-254">With the release of the gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="92115-255">Перейдите на вкладку **Диагностика** в диспетчере конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="92115-255">Switch to the **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Вкладка "Диагностика"в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="92115-257">Щелкните **Отправить журналы**, чтобы открыть приведенное ниже диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="92115-257">Click **Send Logs** to see the following dialog box.</span></span>

    ![Кнопка "Отправить журналы" в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="92115-259">(Необязательно.) Щелкните **Просмотреть журналы**, чтобы просмотреть журналы в средстве просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="92115-259">(Optional) Click **view logs** to review logs in the event viewer.</span></span>
4. <span data-ttu-id="92115-260">(Необязательно.) Щелкните **Конфиденциальность**, чтобы просмотреть заявление о конфиденциальности веб-служб Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92115-260">(Optional) Click **privacy** to review Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="92115-261">Выбрав все, что нужно передать, щелкните **Отправить журналы**, чтобы отправить журналы за последние семь дней в корпорацию Майкрософт для диагностики и устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="92115-261">When you are satisfied with what you are about to upload, click **Send Logs** to actually send the logs from the last seven days to Microsoft for troubleshooting.</span></span> <span data-ttu-id="92115-262">Вы увидите состояние отправки журналов, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="92115-262">You should see the status of the send-logs operation as shown in the following screenshot.</span></span>

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="92115-264">После завершения отправки появится диалоговое окно, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="92115-264">After the operation is complete, you see a dialog box as shown in the following screenshot.</span></span>

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="92115-266">Сохраните **идентификатор отчета** и передайте его в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92115-266">Save the **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="92115-267">Идентификатор отчета используется для поиска журналов шлюза, которые вы передали для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="92115-267">The report ID is used to locate the gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="92115-268">Кроме того, этот идентификатор сохраняется в средстве просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="92115-268">The report ID is also saved in the event viewer.</span></span>  <span data-ttu-id="92115-269">Его можно найти, просмотрев идентификатор события "25" и проверив дату и время.</span><span class="sxs-lookup"><span data-stu-id="92115-269">You can find it by looking at the event ID “25”, and check the date and time.</span></span>

    ![Идентификатор отчета об отправке журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="92115-271">Архивация журналов шлюза на хост-компьютере шлюза</span><span class="sxs-lookup"><span data-stu-id="92115-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="92115-272">Существует несколько сценариев, в которых при наличии проблем в работе шлюза вы не можете передать журналы шлюза напрямую:</span><span class="sxs-lookup"><span data-stu-id="92115-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="92115-273">вы вручную устанавливаете и регистрируете шлюз;</span><span class="sxs-lookup"><span data-stu-id="92115-273">You manually install the gateway and register the gateway.</span></span>
* <span data-ttu-id="92115-274">вы пытаетесь зарегистрировать шлюз с помощью повторно созданного ключа в диспетчере конфигураций шлюза управления данными;</span><span class="sxs-lookup"><span data-stu-id="92115-274">You try to register the gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="92115-275">вы пытаетесь отправить журналы, но не можете подключиться к службе узла шлюза.</span><span class="sxs-lookup"><span data-stu-id="92115-275">You try to send logs and the gateway host service cannot be connected.</span></span>

<span data-ttu-id="92115-276">В таких случаях можно сохранить журналы шлюза в ZIP-файл и предоставить их при обращении в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92115-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="92115-277">Например, это можно сделать при возникновении ошибки во время регистрации шлюза, как показано на снимке экрана ниже.</span><span class="sxs-lookup"><span data-stu-id="92115-277">For example, if you receive an error while you register the gateway as shown in the following screenshot.</span></span>   

![Ошибка регистрации в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="92115-279">Щелкните ссылку **Архивировать журналы шлюза**, чтобы заархивировать и сохранить журналы, а затем передайте полученный ZIP-файл в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="92115-279">Click the **Archive gateway logs** link to archive and save logs, and then share the zip file with Microsoft support.</span></span>

![Архивация журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="92115-281">Поиск журналов шлюза</span><span class="sxs-lookup"><span data-stu-id="92115-281">Locate gateway logs</span></span>
<span data-ttu-id="92115-282">Подробную информацию о журналах шлюза можно найти в журналах событий Windows.</span><span class="sxs-lookup"><span data-stu-id="92115-282">You can find detailed gateway log information in the Windows event logs.</span></span>

1. <span data-ttu-id="92115-283">Запустите **средство просмотра событий** Windows.</span><span class="sxs-lookup"><span data-stu-id="92115-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="92115-284">Найдите журналы в папке **Журналы приложения и служб** > **Шлюз управления данными**.</span><span class="sxs-lookup"><span data-stu-id="92115-284">Locate logs in the **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="92115-285">Устраняя связанные со шлюзом ошибки, обращайте внимание на события уровня ошибок в средстве просмотра событий.</span><span class="sxs-lookup"><span data-stu-id="92115-285">When you're troubleshooting gateway-related issues, look for error level events in the event viewer.</span></span>

![Журналы в средстве просмотра событий в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
