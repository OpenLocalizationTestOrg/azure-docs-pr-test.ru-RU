---
title: "выдает шлюз управления данными aaaTroubleshoot | Документы Microsoft"
description: "Предоставляет советы tootroubleshoot проблемы связанные tooData Management Gateway."
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
ms.openlocfilehash: 85dacc8a1e8d574d6e7d5b556c995cebdc148fde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-issues-with-using-data-management-gateway"></a><span data-ttu-id="9e715-103">Устранение неполадок в работе шлюза управления данными</span><span class="sxs-lookup"><span data-stu-id="9e715-103">Troubleshoot issues with using Data Management Gateway</span></span>
<span data-ttu-id="9e715-104">В этой статье приводятся сведения об устранении неполадок в работе шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="9e715-104">This article provides information on troubleshooting issues with using Data Management Gateway.</span></span>

> [!NOTE]
> <span data-ttu-id="9e715-105">В разделе hello [шлюз управления данными](data-factory-data-management-gateway.md) статье подробные сведения о шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-105">See hello [Data Management Gateway](data-factory-data-management-gateway.md) article for detailed information about hello gateway.</span></span> <span data-ttu-id="9e715-106">В разделе hello [перемещение данных между локальными и облачными](data-factory-move-data-between-onprem-and-cloud.md) статье пошаговое перемещения данных из tooMicrosoft базы данных SQL Server локального хранилища больших двоичных объектов Azure с помощью шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-106">See hello [Move data between on-premises and cloud](data-factory-move-data-between-onprem-and-cloud.md) article for a walkthrough of moving data from an on-premises SQL Server database tooMicrosoft Azure Blob storage by using hello gateway.</span></span>
>
>

## <a name="failed-tooinstall-or-register-gateway"></a><span data-ttu-id="9e715-107">Не удалось tooinstall или регистрация шлюза</span><span class="sxs-lookup"><span data-stu-id="9e715-107">Failed tooinstall or register gateway</span></span>
### <a name="1-problem"></a><span data-ttu-id="9e715-108">1. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-108">1. Problem</span></span>
<span data-ttu-id="9e715-109">Вы видите это сообщение об ошибке при установке и регистрации шлюза, в частности, при загрузке файла установки шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-109">You see this error message when installing and registering a gateway, specifically, while downloading hello gateway installation file.</span></span>

`Unable tooconnect toohello remote server". Please check your local settings (Error Code: 10003).`

#### <a name="cause"></a><span data-ttu-id="9e715-110">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-110">Cause</span></span>
<span data-ttu-id="9e715-111">Сбой toodownload hello последний шлюза файл установки из центра загрузки hello из-за проблемы в сети tooa Hello компьютера, на котором вы пытаетесь tooinstall hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-111">hello machine on which you are trying tooinstall hello gateway has failed toodownload hello latest gateway installation file from hello download center due tooa network issue.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-112">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-112">Resolution</span></span>
<span data-ttu-id="9e715-113">Проверьте наличие вашей toosee параметры брандмауэра сервера прокси-сервера hello параметры блокируют hello сетевого подключения от компьютера toohello hello [центре загрузки](https://download.microsoft.com/)и обновите параметры hello соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="9e715-113">Check your firewall proxy server settings toosee whether hello settings block hello network connection from hello computer toohello [download center](https://download.microsoft.com/), and update hello settings accordingly.</span></span>

<span data-ttu-id="9e715-114">Кроме того, можно загрузить последнюю версию шлюза hello в файле установки hello hello [центре загрузки](https://www.microsoft.com/download/details.aspx?id=39717) на других компьютерах, которые могут обращаться к hello центра загрузки.</span><span class="sxs-lookup"><span data-stu-id="9e715-114">Alternatively, you can download hello installation file for hello latest gateway from hello [download center](https://www.microsoft.com/download/details.aspx?id=39717) on other machines that can access hello download center.</span></span> <span data-ttu-id="9e715-115">После этого можно копировать hello установщика toohello шлюза главного компьютера и запустите его вручную tooinstall и обновление шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-115">You can then copy hello installer file toohello gateway host computer and run it manually tooinstall and update hello gateway.</span></span>

### <a name="2-problem"></a><span data-ttu-id="9e715-116">2. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-116">2. Problem</span></span>
<span data-ttu-id="9e715-117">Эта ошибка появляется пытаются tooinstall шлюза, нажав кнопку **установки непосредственно на этом компьютере** в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9e715-117">You see this error when you're attempting tooinstall a gateway by clicking **install directly on this computer** in hello Azure portal.</span></span>

`Error:  Abort installing a new gateway on this computer because this computer has an existing installed gateway and a computer without any installed gateway is required for installing a new gateway.`  

#### <a name="cause"></a><span data-ttu-id="9e715-118">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-118">Cause</span></span>
<span data-ttu-id="9e715-119">Шлюз уже установлен на компьютере hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-119">A gateway is already installed on hello machine.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-120">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-120">Resolution</span></span>
<span data-ttu-id="9e715-121">Удалите существующий шлюз hello на машине hello, нажмите кнопку hello **установки непосредственно на этом компьютере** ссылку еще раз.</span><span class="sxs-lookup"><span data-stu-id="9e715-121">Uninstall hello existing gateway on hello machine and click hello **install directly on this computer** link again.</span></span>

### <a name="3-problem"></a><span data-ttu-id="9e715-122">3. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-122">3. Problem</span></span>
<span data-ttu-id="9e715-123">Эта ошибка может возникнуть при регистрации нового шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-123">You might see this error when registering a new gateway.</span></span>

`Error: hello gateway has encountered an error during registration.`

#### <a name="cause"></a><span data-ttu-id="9e715-124">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-124">Cause</span></span>
<span data-ttu-id="9e715-125">Может появиться это сообщение по одной из следующих причин hello:</span><span class="sxs-lookup"><span data-stu-id="9e715-125">You might see this message for one of hello following reasons:</span></span>

* <span data-ttu-id="9e715-126">Недопустимый формат ключа шлюза hello Hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-126">hello format of hello gateway key is invalid.</span></span>
* <span data-ttu-id="9e715-127">ключ шлюза Hello является недействительным.</span><span class="sxs-lookup"><span data-stu-id="9e715-127">hello gateway key has been invalidated.</span></span>
* <span data-ttu-id="9e715-128">ключ шлюза Hello была повторно создана из портала hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-128">hello gateway key has been regenerated from hello portal.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="9e715-129">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-129">Resolution</span></span>
<span data-ttu-id="9e715-130">Проверьте, используется ли ключ hello правой шлюза с портала hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-130">Verify whether you are using hello right gateway key from hello portal.</span></span> <span data-ttu-id="9e715-131">При необходимости повторно создать ключ и использовать шлюз hello ключа tooregister hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-131">If needed, regenerate a key and use hello key tooregister hello gateway.</span></span>

### <a name="4-problem"></a><span data-ttu-id="9e715-132">4. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-132">4. Problem</span></span>
<span data-ttu-id="9e715-133">Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-133">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello content or format of hello gateway key "{gatewayKey}" is invalid, please go tooazure portal toocreate one new gateway or regenerate hello gateway key.`



![Недопустимое содержимое или формат ключа](media/data-factory-troubleshoot-gateway-issues/invalid-format-gateway-key.png)

#### <a name="cause"></a><span data-ttu-id="9e715-135">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-135">Cause</span></span>
<span data-ttu-id="9e715-136">Hello содержимое или формат ключа шлюза входной hello неверный.</span><span class="sxs-lookup"><span data-stu-id="9e715-136">hello content or format of hello input gateway key is incorrect.</span></span> <span data-ttu-id="9e715-137">Одной из причин hello может быть, что копируются только части ключа hello hello портала или вы используете недопустимый ключ.</span><span class="sxs-lookup"><span data-stu-id="9e715-137">One of hello reasons can be that you copied only a portion of hello key from hello portal or you're using an invalid key.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-138">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-138">Resolution</span></span>
<span data-ttu-id="9e715-139">Создайте ключ шлюза на портале hello и использовать hello копирования кнопки toocopy hello весь ключ.</span><span class="sxs-lookup"><span data-stu-id="9e715-139">Generate a gateway key in hello portal, and use hello copy button toocopy hello whole key.</span></span> <span data-ttu-id="9e715-140">Затем вставьте его в этот шлюз hello tooregister окна.</span><span class="sxs-lookup"><span data-stu-id="9e715-140">Then paste it in this window tooregister hello gateway.</span></span>

### <a name="5-problem"></a><span data-ttu-id="9e715-141">5. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-141">5. Problem</span></span>
<span data-ttu-id="9e715-142">Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-142">You might see hello following error message when you're registering a gateway.</span></span>

`Error: hello gateway key is invalid or empty. Specify a valid gateway key from hello portal.`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-key-is-invalid-or-empty.png)

#### <a name="cause"></a><span data-ttu-id="9e715-144">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-144">Cause</span></span>
<span data-ttu-id="9e715-145">ключ шлюза Hello была повторно создана или hello шлюз был удален в hello портал Azure.</span><span class="sxs-lookup"><span data-stu-id="9e715-145">hello gateway key has been regenerated or hello gateway has been deleted in hello Azure portal.</span></span> <span data-ttu-id="9e715-146">Он также может произойти, если программа установки шлюза управления данными hello не является последней.</span><span class="sxs-lookup"><span data-stu-id="9e715-146">It can also happen if hello Data Management Gateway setup is not latest.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-147">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-147">Resolution</span></span>
<span data-ttu-id="9e715-148">Проверьте, если Настройка шлюза управления данными hello не последнюю версию hello, можно найти последнюю версию hello на hello Microsoft [центре загрузки](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span><span class="sxs-lookup"><span data-stu-id="9e715-148">Check if hello Data Management Gateway setup is hello latest version, you can find hello latest version on hello Microsoft [download center](https://go.microsoft.com/fwlink/p/?LinkId=271260).</span></span>

<span data-ttu-id="9e715-149">Если настройка текущего / последней, и шлюз по-прежнему существует на портале, ключ шлюза hello hello портал Azure, повторно использовать hello копирования кнопки toocopy hello весь ключ и вставьте его в этот шлюз hello tooregister окна.</span><span class="sxs-lookup"><span data-stu-id="9e715-149">If setup is current/ latest and gateway still exists on Portal, regenerate hello gateway key in hello Azure portal, and use hello copy button toocopy hello whole key, and then paste it in this window tooregister hello gateway.</span></span> <span data-ttu-id="9e715-150">В противном случае повторного создания шлюза hello и начать заново.</span><span class="sxs-lookup"><span data-stu-id="9e715-150">Otherwise, recreate hello gateway and start over.</span></span>

### <a name="6-problem"></a><span data-ttu-id="9e715-151">6. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-151">6. Problem</span></span>
<span data-ttu-id="9e715-152">Может появиться следующие сообщение об ошибке, при регистрации шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-152">You might see hello following error message when you're registering a gateway.</span></span>

`Error: Gateway has been online for a while, then shows “Gateway is not registered” with hello status “Gateway key is invalid”`

![Ключ шлюза является недопустимым или пустым](media/data-factory-troubleshoot-gateway-issues/gateway-not-registered-key-invalid.png)

#### <a name="cause"></a><span data-ttu-id="9e715-154">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-154">Cause</span></span>
<span data-ttu-id="9e715-155">Эта ошибка может происходить, когда шлюз hello удален или ключ соответствующего шлюза hello была повторно создана.</span><span class="sxs-lookup"><span data-stu-id="9e715-155">This error might happen because either hello gateway has been deleted or hello associated gateway key has been regenerated.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-156">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-156">Resolution</span></span>
<span data-ttu-id="9e715-157">Hello шлюз удален, повторно создать шлюз hello из портала hello, откройте **зарегистрировать**, скопируйте hello ключ с портала hello, вставьте его и повторите tooregister hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-157">If hello gateway has been deleted, re-create hello gateway from hello portal, click **Register**, copy hello key from hello portal, paste it, and try tooregister hello gateway.</span></span>

<span data-ttu-id="9e715-158">Если шлюз hello по-прежнему существует, но его ключ была повторно создана, используйте hello нового ключа tooregister hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-158">If hello gateway still exists but its key has been regenerated, use hello new key tooregister hello gateway.</span></span> <span data-ttu-id="9e715-159">Если у вас нет ключа hello, повторно создать ключ hello снова с портала hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-159">If you don’t have hello key, regenerate hello key again from hello portal.</span></span>

### <a name="7-problem"></a><span data-ttu-id="9e715-160">7. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-160">7. Problem</span></span>
<span data-ttu-id="9e715-161">При регистрации шлюза может потребоваться tooenter путь и пароль для сертификата.</span><span class="sxs-lookup"><span data-stu-id="9e715-161">When you're registering a gateway, you might need tooenter path and password for a certificate.</span></span>

![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-certificate.png)

#### <a name="cause"></a><span data-ttu-id="9e715-163">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-163">Cause</span></span>
<span data-ttu-id="9e715-164">Hello шлюза на других компьютерах, прежде чем был зарегистрирован.</span><span class="sxs-lookup"><span data-stu-id="9e715-164">hello gateway has been registered on other machines before.</span></span> <span data-ttu-id="9e715-165">Во время первоначальной регистрации hello шлюза сертификат шифрования была связана с hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-165">During hello initial registration of a gateway, an encryption certificate has been associated with hello gateway.</span></span> <span data-ttu-id="9e715-166">Hello сертификата можно самостоятельно созданный hello шлюза или предоставленный пользователем hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-166">hello certificate can either be self-generated by hello gateway or provided by hello user.</span></span>  <span data-ttu-id="9e715-167">Этот сертификат является используется tooencrypt учетные данные хранилища данных hello (связанной службы).</span><span class="sxs-lookup"><span data-stu-id="9e715-167">This certificate is used tooencrypt credentials of hello data store (linked service).</span></span>  

![Экспорт сертификата](media/data-factory-troubleshoot-gateway-issues/export-certificate.png)

<span data-ttu-id="9e715-169">Если восстановление hello шлюза на другой компьютер запрашивает мастер регистрации hello toodecrypt этот сертификат учетных данных для ранее зашифрован с помощью этого сертификата.</span><span class="sxs-lookup"><span data-stu-id="9e715-169">When restoring hello gateway on a different host machine, hello registration wizard asks for this certificate toodecrypt credentials previously encrypted with this certificate.</span></span>  <span data-ttu-id="9e715-170">Без этого сертификата не удалось расшифровать учетные данные hello новый шлюз hello и последующие действия обработка, связанная с этой новый шлюз завершится ошибкой.</span><span class="sxs-lookup"><span data-stu-id="9e715-170">Without this certificate, hello credentials cannot be decrypted by hello new gateway and subsequent copy activity executions associated with this new gateway will fail.</span></span>  

#### <a name="resolution"></a><span data-ttu-id="9e715-171">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-171">Resolution</span></span>
<span data-ttu-id="9e715-172">Если сертификат учетных данных hello были экспортированы из hello исходную машину шлюза с помощью hello **Экспорт** кнопку на hello **параметры** вкладке в данных диспетчера конфигурации шлюза управления, используйте hello сертификат.</span><span class="sxs-lookup"><span data-stu-id="9e715-172">If you have exported hello credential certificate from hello original gateway machine by using hello **Export** button on hello **Settings** tab in Data Management Gateway Configuration Manager, use hello certificate here.</span></span>

<span data-ttu-id="9e715-173">Нельзя пропускать этот шаг при восстановлении шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-173">You cannot skip this stage when recovering a gateway.</span></span> <span data-ttu-id="9e715-174">Если отсутствует сертификат hello, требуется toodelete hello шлюза с портала hello и повторно создать шлюз.</span><span class="sxs-lookup"><span data-stu-id="9e715-174">If hello certificate is missing, you need toodelete hello gateway from hello portal and re-create a new gateway.</span></span>  <span data-ttu-id="9e715-175">Кроме того можно обновите все связанные службы, которые шлюза toohello, связанные с повторный ввод учетных данных.</span><span class="sxs-lookup"><span data-stu-id="9e715-175">In addition, update all linked services that are related toohello gateway by reentering their credentials.</span></span>

### <a name="8-problem"></a><span data-ttu-id="9e715-176">8. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-176">8. Problem</span></span>
<span data-ttu-id="9e715-177">Может появиться сообщение об ошибке после hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-177">You might see hello following error message.</span></span>

`Error: hello remote server returned an error: (407) Proxy Authentication Required.`

#### <a name="cause"></a><span data-ttu-id="9e715-178">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-178">Cause</span></span>
<span data-ttu-id="9e715-179">Эта ошибка возникает, если шлюз в среде, которая требует tooaccess прокси-сервера HTTP Интернет-ресурсов, или изменить пароль для проверки подлинности на прокси-сервера, но не обновляется соответствующим образом в шлюз.</span><span class="sxs-lookup"><span data-stu-id="9e715-179">This error happens when your gateway is in an environment that requires an HTTP proxy tooaccess Internet resources, or your proxy's authentication password is changed but it's not updated accordingly in your gateway.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-180">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-180">Resolution</span></span>
<span data-ttu-id="9e715-181">Следуйте инструкциям hello hello [рекомендации по server прокси](#proxy-server-considerations) раздела этого статей и настройка параметров прокси-сервера с помощью диспетчера шлюза управления данными конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9e715-181">Follow hello instructions in hello [Proxy server considerations](#proxy-server-considerations) section of this article, and configure proxy settings with Data Management Gateway Configuration Manager.</span></span>

## <a name="gateway-is-online-with-limited-functionality"></a><span data-ttu-id="9e715-182">Шлюз находится в сети с ограниченной функциональностью</span><span class="sxs-lookup"><span data-stu-id="9e715-182">Gateway is online with limited functionality</span></span>
### <a name="1-problem"></a><span data-ttu-id="9e715-183">1. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-183">1. Problem</span></span>
<span data-ttu-id="9e715-184">Можно просмотреть состояние hello шлюза hello в оперативном режиме с ограниченной функциональностью.</span><span class="sxs-lookup"><span data-stu-id="9e715-184">You see hello status of hello gateway as online with limited functionality.</span></span>

#### <a name="cause"></a><span data-ttu-id="9e715-185">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-185">Cause</span></span>
<span data-ttu-id="9e715-186">Появится hello состояния hello шлюз в сети с ограниченной функциональностью, по одной из следующих причин hello:</span><span class="sxs-lookup"><span data-stu-id="9e715-186">You see hello status of hello gateway as online with limited functionality for one of hello following reasons:</span></span>

* <span data-ttu-id="9e715-187">Шлюз нельзя подключиться toocloud службы с помощью Azure Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9e715-187">Gateway cannot connect toocloud service through Azure Service Bus.</span></span>
* <span data-ttu-id="9e715-188">Облачная служба не удается подключиться toogateway через служебную шину.</span><span class="sxs-lookup"><span data-stu-id="9e715-188">Cloud service cannot connect toogateway through Service Bus.</span></span>

<span data-ttu-id="9e715-189">Если hello шлюз находится в режиме с ограниченной функциональностью, может оказаться конвейеры может toouse hello мастер копирования фабрики данных toocreate данных для копирования данных tooor из локальных хранилищ данных.</span><span class="sxs-lookup"><span data-stu-id="9e715-189">When hello gateway is online with limited functionality, you might not be able toouse hello Data Factory Copy Wizard toocreate data pipelines for copying data tooor from on-premises data stores.</span></span> <span data-ttu-id="9e715-190">Чтобы избежать этого можно использовать редактор фабрики данных hello портале, Visual Studio или Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9e715-190">As a workaround, you can use Data Factory Editor in hello portal, Visual Studio, or Azure PowerShell.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-191">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-191">Resolution</span></span>
<span data-ttu-id="9e715-192">Для устранения этой ошибки (сети с ограниченной функциональностью) на основе ли hello шлюза не может подключиться toohello облачной службы или hello другим способом.</span><span class="sxs-lookup"><span data-stu-id="9e715-192">Resolution for this issue (online with limited functionality) is based on whether hello gateway cannot connect toohello cloud service or hello other way.</span></span> <span data-ttu-id="9e715-193">Hello в следующих разделах предоставить эти разрешения.</span><span class="sxs-lookup"><span data-stu-id="9e715-193">hello following sections provide these resolutions.</span></span>

### <a name="2-problem"></a><span data-ttu-id="9e715-194">2. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-194">2. Problem</span></span>
<span data-ttu-id="9e715-195">Появится следующая ошибка hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-195">You see hello following error.</span></span>

`Error: Gateway cannot connect toocloud service through service bus`

![Шлюз не удается подключиться к службе toocloud](media/data-factory-troubleshoot-gateway-issues/gateway-cannot-connect-to-cloud-service.png)

#### <a name="cause"></a><span data-ttu-id="9e715-197">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-197">Cause</span></span>
<span data-ttu-id="9e715-198">Шлюз нельзя подключиться toohello облачной службы с помощью Service Bus.</span><span class="sxs-lookup"><span data-stu-id="9e715-198">Gateway cannot connect toohello cloud service through Service Bus.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-199">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-199">Resolution</span></span>
<span data-ttu-id="9e715-200">Выполните эти шаги tooget hello шлюза обратно в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="9e715-200">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="9e715-201">Разрешить IP-адрес правила для исходящих подключений на компьютере шлюза hello и hello корпоративного брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="9e715-201">Allow IP address outbound rules on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="9e715-202">Можно найти IP-адресов из журнала событий Windows hello (идентификатор == 401): попытка внесенные tooaccess сокет образом запрещено XX правами доступа. XX. XX. XX:9350.</span><span class="sxs-lookup"><span data-stu-id="9e715-202">You can find IP addresses from hello Windows Event Log (ID == 401): An attempt was made tooaccess a socket in a way forbidden by its access permissions XX.XX.XX.XX:9350.</span></span>
* <span data-ttu-id="9e715-203">Настройте параметры прокси-сервера на шлюзе hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-203">Configure proxy settings on hello gateway.</span></span> <span data-ttu-id="9e715-204">В разделе hello [рекомендации по server прокси](#proxy-server-considerations) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="9e715-204">See hello [Proxy server considerations](#proxy-server-considerations) section for details.</span></span>
* <span data-ttu-id="9e715-205">Разрешить исходящие порты 5671 и 9350 – 9354 на обоих hello брандмауэра Windows на компьютере шлюза hello и hello корпоративного брандмауэра.</span><span class="sxs-lookup"><span data-stu-id="9e715-205">Enable outbound ports 5671 and 9350-9354 on both hello Windows Firewall on hello gateway machine and hello corporate firewall.</span></span> <span data-ttu-id="9e715-206">В разделе hello [порты и брандмауэр](#ports-and-firewall) подробные сведения см.</span><span class="sxs-lookup"><span data-stu-id="9e715-206">See hello [Ports and firewall](#ports-and-firewall) section for details.</span></span> <span data-ttu-id="9e715-207">Это делать не обязательно, но рекомендуется из соображений производительности.</span><span class="sxs-lookup"><span data-stu-id="9e715-207">This step is optional, but we recommend it for performance consideration.</span></span>

### <a name="3-problem"></a><span data-ttu-id="9e715-208">3. Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-208">3. Problem</span></span>
<span data-ttu-id="9e715-209">Появится следующая ошибка hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-209">You see hello following error.</span></span>

`Error: Cloud service cannot connect toogateway through service bus.`

#### <a name="cause"></a><span data-ttu-id="9e715-210">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-210">Cause</span></span>
<span data-ttu-id="9e715-211">Временная ошибка подключения к сети.</span><span class="sxs-lookup"><span data-stu-id="9e715-211">A transient error in network connectivity.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-212">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-212">Resolution</span></span>
<span data-ttu-id="9e715-213">Выполните эти шаги tooget hello шлюза обратно в оперативный режим.</span><span class="sxs-lookup"><span data-stu-id="9e715-213">Follow these steps tooget hello gateway back online:</span></span>

1. <span data-ttu-id="9e715-214">Подождите несколько минут, hello подключения будут автоматически восстановлены при hello ошибка отсутствует.</span><span class="sxs-lookup"><span data-stu-id="9e715-214">Wait for a couple of minutes, hello connectivity will be automatically recovered when hello error is gone.</span></span>
* <span data-ttu-id="9e715-215">Если hello ошибка будет повторяться, перезапустите службу шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-215">If hello error persists, restart hello gateway service.</span></span>

## <a name="failed-tooauthor-linked-service"></a><span data-ttu-id="9e715-216">Сбой tooauthor связанные службы</span><span class="sxs-lookup"><span data-stu-id="9e715-216">Failed tooauthor linked service</span></span>
### <a name="problem"></a><span data-ttu-id="9e715-217">Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-217">Problem</span></span>
<span data-ttu-id="9e715-218">Эта ошибка может появиться при попытке toouse диспетчер учетных данных учетные данные портала tooinput hello для новой связанной службы, или обновить учетные данные для существующей связанной службы.</span><span class="sxs-lookup"><span data-stu-id="9e715-218">You might see this error when you try toouse Credential Manager in hello portal tooinput credentials for a new linked service, or update credentials for an existing linked service.</span></span>

`Error: hello data store '<Server>/<Database>' cannot be reached. Check connection settings for hello data source.`

<span data-ttu-id="9e715-219">При появлении этой ошибки, страница параметров hello объекта данных диспетчера конфигурации шлюза управления может выглядеть после экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="9e715-219">When you see this error, hello settings page of Data Management Gateway Configuration Manager might look like hello following screenshot.</span></span>

![Не удается получить доступ к базе данных](media/data-factory-troubleshoot-gateway-issues/database-cannot-be-reached.png)

#### <a name="cause"></a><span data-ttu-id="9e715-221">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-221">Cause</span></span>
<span data-ttu-id="9e715-222">Возможно, на компьютере шлюза hello была потеряна Hello SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="9e715-222">hello SSL certificate might have been lost on hello gateway machine.</span></span> <span data-ttu-id="9e715-223">компьютер с установленным шлюзом Hello не удалось загрузить сертификат hello в момент, используемый для шифрования SSL.</span><span class="sxs-lookup"><span data-stu-id="9e715-223">hello gateway computer cannot load hello certificate currently that is used for SSL encryption.</span></span> <span data-ttu-id="9e715-224">Может также появиться сообщение об ошибке в журнал событий hello, аналогичные toohello следующие сообщения.</span><span class="sxs-lookup"><span data-stu-id="9e715-224">You might also see an error message in hello event log that is similar toohello following message.</span></span>

 `Unable tooget hello gateway settings from cloud service. Check hello gateway key and hello network connection. (Certificate with thumbprint cannot be loaded.)`

#### <a name="resolution"></a><span data-ttu-id="9e715-225">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-225">Resolution</span></span>
<span data-ttu-id="9e715-226">Выполните эти шаги toosolve hello проблему.</span><span class="sxs-lookup"><span data-stu-id="9e715-226">Follow these steps toosolve hello problem:</span></span>

1. <span data-ttu-id="9e715-227">Запустите диспетчер конфигураций шлюза управления данными.</span><span class="sxs-lookup"><span data-stu-id="9e715-227">Start Data Management Gateway Configuration Manager.</span></span>
2. <span data-ttu-id="9e715-228">Переключение toohello **параметры** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9e715-228">Switch toohello **Settings** tab.</span></span>  
3. <span data-ttu-id="9e715-229">Нажмите кнопку hello **изменений** кнопку toochange hello SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="9e715-229">Click hello **Change** button toochange hello SSL certificate.</span></span>

   ![Кнопка "Изменить" для сертификата](media/data-factory-troubleshoot-gateway-issues/change-button-ssl-certificate.png)
4. <span data-ttu-id="9e715-231">Выберите новый сертификат как сертификат SSL hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-231">Select a new certificate as hello SSL certificate.</span></span> <span data-ttu-id="9e715-232">Вы можете использовать собственный или корпоративный SSL-сертификат.</span><span class="sxs-lookup"><span data-stu-id="9e715-232">You can use any SSL certificate that is generated by you or any organization.</span></span>

   ![Выбор сертификата](media/data-factory-troubleshoot-gateway-issues/specify-http-end-point.png)

## <a name="copy-activity-fails"></a><span data-ttu-id="9e715-234">Сбой действия копирования</span><span class="sxs-lookup"><span data-stu-id="9e715-234">Copy activity fails</span></span>
### <a name="problem"></a><span data-ttu-id="9e715-235">Проблема</span><span class="sxs-lookup"><span data-stu-id="9e715-235">Problem</span></span>
<span data-ttu-id="9e715-236">Можно заметить hello после сбоя «UserErrorFailedToConnectToSqlserver» после настройки конвейера hello портала.</span><span class="sxs-lookup"><span data-stu-id="9e715-236">You might notice hello following "UserErrorFailedToConnectToSqlserver" failure after you set up a pipeline in hello portal.</span></span>

`Error: Copy activity encountered a user error: ErrorCode=UserErrorFailedToConnectToSqlServer,'Type=Microsoft.DataTransfer.Common.Shared.HybridDeliveryException,Message=Cannot connect tooSQL Server`

#### <a name="cause"></a><span data-ttu-id="9e715-237">Причина:</span><span class="sxs-lookup"><span data-stu-id="9e715-237">Cause</span></span>
<span data-ttu-id="9e715-238">Она может возникнуть по разным причинам, от которых зависят и способы ее устранения.</span><span class="sxs-lookup"><span data-stu-id="9e715-238">This can happen for different reasons, and mitigation varies accordingly.</span></span>

#### <a name="resolution"></a><span data-ttu-id="9e715-239">Способы устранения:</span><span class="sxs-lookup"><span data-stu-id="9e715-239">Resolution</span></span>
<span data-ttu-id="9e715-240">Разрешите исходящие соединения TCP через порт TCP/1433 на hello шлюз управления данными на стороне клиента перед подключением tooan базы данных SQL.</span><span class="sxs-lookup"><span data-stu-id="9e715-240">Allow outbound TCP connections over port TCP/1433 on hello Data Management Gateway client side before connecting tooan SQL database.</span></span>

<span data-ttu-id="9e715-241">Если база данных hello целевой базы данных Azure SQL, проверьте SQL Server параметры брандмауэра для Azure также.</span><span class="sxs-lookup"><span data-stu-id="9e715-241">If hello target database is an Azure SQL database, check SQL Server firewall settings for Azure as well.</span></span>

<span data-ttu-id="9e715-242">В разделе hello, следуя tootest раздел hello toohello подключения к локальному хранилищу данных.</span><span class="sxs-lookup"><span data-stu-id="9e715-242">See hello following section tootest hello connection toohello on-premises data store.</span></span>

## <a name="data-store-connection-or-driver-related-errors"></a><span data-ttu-id="9e715-243">Ошибки, связанные с подключением к хранилищу данных или с драйверами</span><span class="sxs-lookup"><span data-stu-id="9e715-243">Data store connection or driver-related errors</span></span>
<span data-ttu-id="9e715-244">Если вы видите данные хранить соединения или ошибки, связанные с драйвером, выполните hello следующие шаги.</span><span class="sxs-lookup"><span data-stu-id="9e715-244">If you see data store connection or driver-related errors, complete hello following steps:</span></span>

1. <span data-ttu-id="9e715-245">Запустите диспетчер конфигурации шлюза управления данными на компьютере шлюза hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-245">Start Data Management Gateway Configuration Manager on hello gateway machine.</span></span>
2. <span data-ttu-id="9e715-246">Переключение toohello **диагностики** вкладки.</span><span class="sxs-lookup"><span data-stu-id="9e715-246">Switch toohello **Diagnostics** tab.</span></span>
3. <span data-ttu-id="9e715-247">В **проверить подключение**, добавьте значения группы hello шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-247">In **Test Connection**, add hello gateway group values.</span></span>
4. <span data-ttu-id="9e715-248">Нажмите кнопку **тест** toosee при подключении toohello локального источника данных с компьютера hello шлюза с помощью hello сведения о соединении и учетные данные.</span><span class="sxs-lookup"><span data-stu-id="9e715-248">Click **Test** toosee if you can connect toohello on-premises data source from hello gateway machine by using hello connection information and credentials.</span></span> <span data-ttu-id="9e715-249">Если hello проверить подключение по-прежнему происходит сбой в работе драйвера, перезапустите hello шлюза для него toopick копирование hello последнее изменение.</span><span class="sxs-lookup"><span data-stu-id="9e715-249">If hello test connection still fails after you install a driver, restart hello gateway for it toopick up hello latest change.</span></span>

![Раздел "Проверить подключение" на вкладке "Диагностика"](media/data-factory-troubleshoot-gateway-issues/test-connection-in-diagnostics-tab.png)

## <a name="gateway-logs"></a><span data-ttu-id="9e715-251">Журналы шлюза</span><span class="sxs-lookup"><span data-stu-id="9e715-251">Gateway logs</span></span>
### <a name="send-gateway-logs-toomicrosoft"></a><span data-ttu-id="9e715-252">Отправить журналы tooMicrosoft шлюза</span><span class="sxs-lookup"><span data-stu-id="9e715-252">Send gateway logs tooMicrosoft</span></span>
<span data-ttu-id="9e715-253">При обращении в службу технической поддержки Майкрософт tooget справки при устранении неполадок шлюза, вас попросят tooshare журналы шлюза.</span><span class="sxs-lookup"><span data-stu-id="9e715-253">When you contact Microsoft Support tooget help with troubleshooting gateway issues, you might be asked tooshare your gateway logs.</span></span> <span data-ttu-id="9e715-254">В выпуске hello hello шлюза могут совместно использовать журналы требуется шлюз с двумя отдельными щелчками кнопки в данных диспетчера конфигурации шлюза управления.</span><span class="sxs-lookup"><span data-stu-id="9e715-254">With hello release of hello gateway, you can share required gateway logs with two button clicks in Data Management Gateway Configuration Manager.</span></span>    

1. <span data-ttu-id="9e715-255">Переключение toohello **диагностики** вкладку в диспетчера шлюза управления данными конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9e715-255">Switch toohello **Diagnostics** tab in Data Management Gateway Configuration Manager.</span></span>

    ![Вкладка "Диагностика"в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-diagnostics-tab.png)
2. <span data-ttu-id="9e715-257">Нажмите кнопку **отправить журналы** toosee hello следующие диалоговое окно.</span><span class="sxs-lookup"><span data-stu-id="9e715-257">Click **Send Logs** toosee hello following dialog box.</span></span>

    ![Кнопка "Отправить журналы" в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-dialog.png)
3. <span data-ttu-id="9e715-259">(Необязательно) Нажмите кнопку **Просмотр журналов** tooreview журналах в обозревателе событий hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-259">(Optional) Click **view logs** tooreview logs in hello event viewer.</span></span>
4. <span data-ttu-id="9e715-260">(Необязательно) Нажмите кнопку **конфиденциальности** tooreview Microsoft web services заявление о конфиденциальности.</span><span class="sxs-lookup"><span data-stu-id="9e715-260">(Optional) Click **privacy** tooreview Microsoft web services privacy statement.</span></span>
5. <span data-ttu-id="9e715-261">Если вы удовлетворены Каковы о tooupload, нажмите кнопку **отправить журналы** tooactually отправлять журналы hello с hello последние семь дней tooMicrosoft для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e715-261">When you are satisfied with what you are about tooupload, click **Send Logs** tooactually send hello logs from hello last seven days tooMicrosoft for troubleshooting.</span></span> <span data-ttu-id="9e715-262">Вы увидите hello состояние операции отправки журналов hello, как показано на следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="9e715-262">You should see hello status of hello send-logs operation as shown in hello following screenshot.</span></span>

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-status.png)
6. <span data-ttu-id="9e715-264">По завершении операции hello появиться диалоговое окно, как показано в следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="9e715-264">After hello operation is complete, you see a dialog box as shown in hello following screenshot.</span></span>

    ![Состояние отправки журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-result.png)
7. <span data-ttu-id="9e715-266">Сохранить hello **идентификатор отчета** и использовать их совместно со службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e715-266">Save hello **Report ID** and share it with Microsoft Support.</span></span> <span data-ttu-id="9e715-267">Идентификатор отчета Hello — журналы шлюза используется toolocate hello, загруженные для устранения неполадок.</span><span class="sxs-lookup"><span data-stu-id="9e715-267">hello report ID is used toolocate hello gateway logs that you uploaded for troubleshooting.</span></span>  <span data-ttu-id="9e715-268">Идентификатор Hello отчета сохраняется в средстве просмотра событий hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-268">hello report ID is also saved in hello event viewer.</span></span>  <span data-ttu-id="9e715-269">Можно найти его на событие с Идентификатором hello «25» и проверьте hello даты и времени.</span><span class="sxs-lookup"><span data-stu-id="9e715-269">You can find it by looking at hello event ID “25”, and check hello date and time.</span></span>

    ![Идентификатор отчета об отправке журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-send-logs-report-id.png)    

### <a name="archive-gateway-logs-on-gateway-host-machine"></a><span data-ttu-id="9e715-271">Архивация журналов шлюза на хост-компьютере шлюза</span><span class="sxs-lookup"><span data-stu-id="9e715-271">Archive gateway logs on gateway host machine</span></span>
<span data-ttu-id="9e715-272">Существует несколько сценариев, в которых при наличии проблем в работе шлюза вы не можете передать журналы шлюза напрямую:</span><span class="sxs-lookup"><span data-stu-id="9e715-272">There are some scenarios where you have gateway issues and you cannot share gateway logs directly:</span></span>

* <span data-ttu-id="9e715-273">Вручную установите hello шлюза и зарегистрируйте шлюз hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-273">You manually install hello gateway and register hello gateway.</span></span>
* <span data-ttu-id="9e715-274">Попробуйте tooregister hello шлюза с повторно созданный ключ в диспетчера шлюза управления данными конфигурации.</span><span class="sxs-lookup"><span data-stu-id="9e715-274">You try tooregister hello gateway with a regenerated key in Data Management Gateway Configuration Manager.</span></span>
* <span data-ttu-id="9e715-275">Повторите toosend журналы и служба узла шлюза hello не может быть подключен.</span><span class="sxs-lookup"><span data-stu-id="9e715-275">You try toosend logs and hello gateway host service cannot be connected.</span></span>

<span data-ttu-id="9e715-276">В таких случаях можно сохранить журналы шлюза в ZIP-файл и предоставить их при обращении в службу поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e715-276">For these scenarios, you can save gateway logs as a zip file and share it when you contact Microsoft support.</span></span> <span data-ttu-id="9e715-277">Например если произошла ошибка во время регистрации шлюза hello, как показано в следующий снимок экрана приветствия.</span><span class="sxs-lookup"><span data-stu-id="9e715-277">For example, if you receive an error while you register hello gateway as shown in hello following screenshot.</span></span>   

![Ошибка регистрации в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-registration-error.png)

<span data-ttu-id="9e715-279">Нажмите кнопку hello **архивирование журналов шлюза** связать tooarchive и сохранить журналы и совместно использовать hello ZIP-файл со службой поддержки Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="9e715-279">Click hello **Archive gateway logs** link tooarchive and save logs, and then share hello zip file with Microsoft support.</span></span>

![Архивация журналов в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/data-management-gateway-archive-logs.png)

### <a name="locate-gateway-logs"></a><span data-ttu-id="9e715-281">Поиск журналов шлюза</span><span class="sxs-lookup"><span data-stu-id="9e715-281">Locate gateway logs</span></span>
<span data-ttu-id="9e715-282">Шлюз подробные данные журнала можно найти в журналах событий Windows hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-282">You can find detailed gateway log information in hello Windows event logs.</span></span>

1. <span data-ttu-id="9e715-283">Запустите **средство просмотра событий** Windows.</span><span class="sxs-lookup"><span data-stu-id="9e715-283">Start Windows **Event Viewer**.</span></span>
2. <span data-ttu-id="9e715-284">Найдите журналы в hello **журналы приложений и служб** > **шлюз управления данными** папки.</span><span class="sxs-lookup"><span data-stu-id="9e715-284">Locate logs in hello **Application and Services Logs** > **Data Management Gateway** folder.</span></span>

 <span data-ttu-id="9e715-285">При устранении неполадок проблем, связанных с шлюзом, найдите события уровня ошибки в средстве просмотра событий hello.</span><span class="sxs-lookup"><span data-stu-id="9e715-285">When you're troubleshooting gateway-related issues, look for error level events in hello event viewer.</span></span>

![Журналы в средстве просмотра событий в шлюзе управления данными](media/data-factory-troubleshoot-gateway-issues/gateway-logs-event-viewer.png)
