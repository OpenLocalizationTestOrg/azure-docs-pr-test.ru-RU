---
title: "aaaCreate удостоверение для приложения Azure с помощью Azure CLI | Документы Microsoft"
description: "Описание управления toocreate Azure CLI toouse приложение Azure Active Directory и участника-службы, а также предоставляет доступ к tooresources посредством доступа на основе ролей. Здесь показано, как tooauthenticate приложения с помощью пароля или сертификата."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: c224a189-dd28-4801-b3e3-26991b0eb24d
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 05/15/2017
ms.author: tomfitz
ms.openlocfilehash: 0d693ec801d4f4d6c24ec420580776e73014b325
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-cli-toocreate-a-service-principal-tooaccess-resources"></a><span data-ttu-id="fc1d9-104">Используйте основной tooaccess ресурсов службы toocreate Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc1d9-104">Use Azure CLI toocreate a service principal tooaccess resources</span></span>

<span data-ttu-id="fc1d9-105">При наличии приложения или скрипт, который необходимо tooaccess ресурсов, можно установить удостоверение для приложения hello и проверки подлинности приложения hello в свои собственные учетные данные.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-105">When you have an app or script that needs tooaccess resources, you can set up an identity for hello app and authenticate hello app with its own credentials.</span></span> <span data-ttu-id="fc1d9-106">Этот идентификатор известен как субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-106">This identity is known as a service principal.</span></span> <span data-ttu-id="fc1d9-107">Такой подход позволяет выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-107">This approach enables you to:</span></span>

* <span data-ttu-id="fc1d9-108">Назначение разрешений удостоверение приложения toohello, отличаются от собственных разрешений.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-108">Assign permissions toohello app identity that are different than your own permissions.</span></span> <span data-ttu-id="fc1d9-109">Как правило эти разрешения являются ограниченными tooexactly какие hello приложению toodo.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-109">Typically, these permissions are restricted tooexactly what hello app needs toodo.</span></span>
* <span data-ttu-id="fc1d9-110">Использовать сертификат для аутентификации при выполнении автоматического сценария.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="fc1d9-111">В этой статье показано, как toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset копирование toorun приложения под свои собственные учетные данные и удостоверений.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-111">This article shows you how toouse [Azure CLI 1.0](../cli-install-nodejs.md) tooset up an application toorun under its own credentials and identity.</span></span> <span data-ttu-id="fc1d9-112">Установить hello последнюю версию [Azure CLI 1.0](../cli-install-nodejs.md) toomake должен соответствовать среды hello примеры в этой статье.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-112">Install hello latest version of [Azure CLI 1.0](../cli-install-nodejs.md) toomake sure your environment matches hello examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="fc1d9-113">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="fc1d9-113">Required permissions</span></span>
<span data-ttu-id="fc1d9-114">toocomplete в этом разделе, необходимо иметь достаточные разрешения в Azure Active Directory и вашей подписке Azure.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-114">toocomplete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="fc1d9-115">В частности необходимо быть может toocreate приложение в Azure Active Directory hello и назначить роль участника tooa hello службы.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-115">Specifically, you must be able toocreate an app in hello Azure Active Directory, and assign hello service principal tooa role.</span></span> 

<span data-ttu-id="fc1d9-116">Hello ли ваша учетная запись имеет достаточные разрешения — с помощью портала hello простой toocheck способом.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-116">hello easiest way toocheck whether your account has adequate permissions is through hello portal.</span></span> <span data-ttu-id="fc1d9-117">Ознакомьтесь с [проверкой наличия необходимых разрешений на портале](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="fc1d9-118">Теперь, либо продолжить tooa раздел [пароль](#create-service-principal-with-password) или [сертификат](#create-service-principal-with-certificate) проверки подлинности.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-118">Now, proceed tooa section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="fc1d9-119">Создание субъекта-службы с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="fc1d9-119">Create service principal with password</span></span>
<span data-ttu-id="fc1d9-120">В этом разделе выполняется hello toocreate hello действия приложения AD с помощью пароля и назначить участника службы toohello роль модуля чтения hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-120">In this section, you perform hello steps toocreate hello AD application with a password, and assign hello Reader role toohello service principal.</span></span>

1. <span data-ttu-id="fc1d9-121">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-121">Sign in tooyour account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="fc1d9-122">toocreate удостоверение приложения укажите приложение hello hello имя и пароль, как показано в hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-122">toocreate an app identity, provide hello name of hello app and a password, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="fc1d9-123">возвращается Hello нового субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-123">hello new service principal is returned.</span></span> <span data-ttu-id="fc1d9-124">При предоставлении разрешений требуется Hello объекта с идентификатором.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-124">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="fc1d9-125">требуется guid Hello hello имена участника-службы в списке при входе в систему.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-125">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="fc1d9-126">Этот идентификатор guid — hello совпадает со значением идентификатора приложения hello. В примерах приложений hello, это значение является ссылка tooas hello `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-126">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello `Client ID`.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating application exampleapp
     / Creating service principal for application 7132aca4-1bdb-4238-ad81-996ff91d8db+
     data:    Object Id:               ff863613-e5e2-4a6b-af07-fff6f2de3f4e
     data:    Display Name:            exampleapp
     data:    Service Principal Names:
     data:                             7132aca4-1bdb-4238-ad81-996ff91d8db4
     data:                             https://www.contoso.org/example
     info:    ad sp create command OK
   ```

3. <span data-ttu-id="fc1d9-127">Предоставить разрешения участника службы hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-127">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="fc1d9-128">В этом примере добавляется hello службы основной toohello чтения роль, которая предоставляет разрешение tooread все ресурсы в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-128">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="fc1d9-129">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-129">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="fc1d9-130">Параметр objectid hello укажите идентификатор объекта, который использовался при создании приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-130">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="fc1d9-131">Перед выполнением этой команды, необходимо разрешить некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-131">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="fc1d9-132">При выполнении этих команд вручную между задачами обычно проходит достаточно времени.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-132">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="fc1d9-133">В сценарии, следует добавить шаг toosleep между командами hello (например `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-133">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="fc1d9-134">Если вы увидите, что ошибка сообщение о hello участника не существует в каталоге hello, повторно запустите команду hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-134">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="fc1d9-135">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="fc1d9-135">That's it!</span></span> <span data-ttu-id="fc1d9-136">Приложение AD и субъект-служба настроены.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-136">Your AD application and service principal are set up.</span></span> <span data-ttu-id="fc1d9-137">Hello следующем разделе показано, как toolog вход с помощью hello учетных данных через Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-137">hello next section shows you how toolog in with hello credential through Azure CLI.</span></span> <span data-ttu-id="fc1d9-138">Если требуется учетных данных toouse hello в код приложения, не обязательно toocontinue с этим разделом.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-138">If you want toouse hello credential in your code application, you do not need toocontinue with this topic.</span></span> <span data-ttu-id="fc1d9-139">Можно легко toohello [образцы приложений](#sample-applications) примеры вход с помощью идентификатора приложения и пароль.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-139">You can jump toohello [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="fc1d9-140">Предоставление учетных данных через Azure CLI</span><span class="sxs-lookup"><span data-stu-id="fc1d9-140">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="fc1d9-141">Теперь требуется toolog в качестве операции tooperform приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-141">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="fc1d9-142">При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-142">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="fc1d9-143">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-143">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="fc1d9-144">ИД клиента hello tooretrieve для прошедшего подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-144">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="fc1d9-145">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-145">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="fc1d9-146">Если вам требуется идентификатор клиента hello tooget другую подписку, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-146">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="fc1d9-147">Toouse идентификатор клиента hello tooretrieve для входа, используйте:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-147">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="fc1d9-148">toouse значение Hello для входа является hello код guid, указанный в приветствия имен участников-служб.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-148">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
   
   ```azurecli
   [
     {
       "objectId": "ff863613-e5e2-4a6b-af07-fff6f2de3f4e",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "7132aca4-1bdb-4238-ad81-996ff91d8db4",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "7132aca4-1bdb-4238-ad81-996ff91d8db4"
       ]
     }
   ]
   ```
3. <span data-ttu-id="fc1d9-149">Войдите в систему как участник службы hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-149">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="fc1d9-150">Запрашивается пароль hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-150">You are prompted for hello password.</span></span> <span data-ttu-id="fc1d9-151">Укажите пароль hello, указанные при создании приложения hello AD.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-151">Provide hello password you specified when creating hello AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="fc1d9-152">Теперь вы прошли проверку подлинности как субъект-службу hello для hello участника-службы, вы создали.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-152">You are now authenticated as hello service principal for hello service principal that you created.</span></span>

<span data-ttu-id="fc1d9-153">Кроме того могут вызывать операции REST из toolog Командная строка hello в.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-153">Alternatively, you can invoke REST operations from hello command line toolog in.</span></span> <span data-ttu-id="fc1d9-154">Из hello ответ проверки подлинности можно получить маркер доступа hello для использования с другими операциями.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-154">From hello authentication response, you can retrieve hello access token for use with other operations.</span></span> <span data-ttu-id="fc1d9-155">Пример получения токена доступа hello путем вызова операции REST см. в разделе [создания токена доступа](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-155">For an example of retrieving hello access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="fc1d9-156">Создание субъекта-службы с использованием сертификата</span><span class="sxs-lookup"><span data-stu-id="fc1d9-156">Create service principal with certificate</span></span>
<span data-ttu-id="fc1d9-157">В этом разделе необходимо выполнить действия hello для.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-157">In this section, you perform hello steps to:</span></span>

* <span data-ttu-id="fc1d9-158">создать самозаверяющий сертификат;</span><span class="sxs-lookup"><span data-stu-id="fc1d9-158">create a self-signed certificate</span></span>
* <span data-ttu-id="fc1d9-159">Создайте hello приложения AD сертификат hello и hello участника-службы</span><span class="sxs-lookup"><span data-stu-id="fc1d9-159">create hello AD application with hello certificate, and hello service principal</span></span>
* <span data-ttu-id="fc1d9-160">назначить участника службы toohello роль модуля чтения hello</span><span class="sxs-lookup"><span data-stu-id="fc1d9-160">assign hello Reader role toohello service principal</span></span>

<span data-ttu-id="fc1d9-161">toocomplete следующие действия, необходимо иметь [OpenSSL](http://www.openssl.org/) установлен.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-161">toocomplete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="fc1d9-162">Создать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-162">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="fc1d9-163">Здравствуйте, предшествующий шаг создания двух файлов - privkey.pem и cert.pem.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-163">hello preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="fc1d9-164">Открытый и закрытый ключи hello объединить в один файл.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-164">Combine hello public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="fc1d9-165">Откройте hello **examplecert.pem** файл и выполните поиск hello длинную последовательность символов между **---BEGIN CERTIFICATE---** и **---конечный СЕРТИФИКАТ---**.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-165">Open hello **examplecert.pem** file and look for hello long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="fc1d9-166">Скопируйте данные сертификата hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-166">Copy hello certificate data.</span></span> <span data-ttu-id="fc1d9-167">Эти данные можно передать как параметр при создании hello участника-службы.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-167">You pass this data as a parameter when creating hello service principal.</span></span>

4. <span data-ttu-id="fc1d9-168">Войдите в учетную запись tooyour.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-168">Sign in tooyour account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="fc1d9-169">участника-службы toocreate hello, укажите имя hello приложение hello и данные сертификата hello, как показано в hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-169">toocreate hello service principal, provide hello name of hello app and hello certificate data, as shown in hello following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="fc1d9-170">возвращается Hello нового субъекта-службы.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-170">hello new service principal is returned.</span></span> <span data-ttu-id="fc1d9-171">При предоставлении разрешений требуется Hello объекта с идентификатором.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-171">hello Object Id is needed when granting permissions.</span></span> <span data-ttu-id="fc1d9-172">требуется guid Hello hello имена участника-службы в списке при входе в систему.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-172">hello guid listed with hello Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="fc1d9-173">Этот идентификатор guid — hello совпадает со значением идентификатора приложения hello. В примерах приложений hello это значение является ссылка tooas hello идентификатор клиента.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-173">This guid is hello same value as hello app id. In hello sample applications, this value is referred tooas hello Client ID.</span></span> 
     
   ```azurecli
   info:    Executing command ad sp create
     
   Creating service principal for application 4fd39843-c338-417d-b549-a545f584a74+
     data:    Object Id:        7dbc8265-51ed-4038-8e13-31948c7f4ce7
     data:    Display Name:     exampleapp
     data:    Service Principal Names:
     data:                      4fd39843-c338-417d-b549-a545f584a745
     data:                      https://www.contoso.org/example
     info:    ad sp create command OK
   ```
6. <span data-ttu-id="fc1d9-174">Предоставить разрешения участника службы hello в вашей подписке.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-174">Grant hello service principal permissions on your subscription.</span></span> <span data-ttu-id="fc1d9-175">В этом примере добавляется hello службы основной toohello чтения роль, которая предоставляет разрешение tooread все ресурсы в подписке hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-175">In this example, you add hello service principal toohello Reader role, which grants permission tooread all resources in hello subscription.</span></span> <span data-ttu-id="fc1d9-176">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-176">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="fc1d9-177">Параметр objectid hello укажите идентификатор объекта, который использовался при создании приложения hello hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-177">For hello objectid parameter, provide hello Object Id that you used when creating hello application.</span></span> <span data-ttu-id="fc1d9-178">Перед выполнением этой команды, необходимо разрешить некоторое время для hello новой службы основной toopropagate во всей Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-178">Before running this command, you must allow some time for hello new service principal toopropagate throughout Azure Active Directory.</span></span> <span data-ttu-id="fc1d9-179">При выполнении этих команд вручную между задачами обычно проходит достаточно времени.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-179">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="fc1d9-180">В сценарии, следует добавить шаг toosleep между командами hello (например `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-180">In a script, you should add a step toosleep between hello commands (like `sleep 15`).</span></span> <span data-ttu-id="fc1d9-181">Если вы увидите, что ошибка сообщение о hello участника не существует в каталоге hello, повторно запустите команду hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-181">If you see an error stating hello principal does not exist in hello directory, rerun hello command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="fc1d9-182">Предоставление сертификата с помощью автоматизированного сценария для интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="fc1d9-182">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="fc1d9-183">Теперь требуется toolog в качестве операции tooperform приложения hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-183">Now, you need toolog in as hello application tooperform operations.</span></span>

1. <span data-ttu-id="fc1d9-184">При каждом входе в качестве участника-службы для приложения AD необходимо ИД клиента hello tooprovide hello каталога.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-184">Whenever you sign in as a service principal, you need tooprovide hello tenant id of hello directory for your AD app.</span></span> <span data-ttu-id="fc1d9-185">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-185">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="fc1d9-186">ИД клиента hello tooretrieve для прошедшего подписки, используйте:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-186">tooretrieve hello tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="fc1d9-187">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-187">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="fc1d9-188">Если вам требуется идентификатор клиента hello tooget другую подписку, используйте hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-188">If you need tooget hello tenant id of another subscription, use hello following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="fc1d9-189">tooretrieve hello отпечаток сертификата и удалите ненужные символы, используйте:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-189">tooretrieve hello certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="fc1d9-190">Возвращается значение отпечатка следующего вида:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-190">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="fc1d9-191">Toouse идентификатор клиента hello tooretrieve для входа, используйте:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-191">If you need tooretrieve hello client id toouse for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="fc1d9-192">toouse значение Hello для входа является hello код guid, указанный в приветствия имен участников-служб.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-192">hello value toouse for logging in is hello guid listed in hello service principal names.</span></span>
     
   ```azurecli
   [
     {
       "objectId": "7dbc8265-51ed-4038-8e13-31948c7f4ce7",
       "objectType": "ServicePrincipal",
       "displayName": "exampleapp",
       "appId": "4fd39843-c338-417d-b549-a545f584a745",
       "servicePrincipalNames": [
         "https://www.contoso.org/example",
         "4fd39843-c338-417d-b549-a545f584a745"
       ]
     }
   ]
   ```
4. <span data-ttu-id="fc1d9-193">Войдите в систему как участник службы hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-193">Log in as hello service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="fc1d9-194">Теперь вы прошли проверку подлинности как hello субъекта-службы для hello созданное приложение Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-194">You are now authenticated as hello service principal for hello Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="fc1d9-195">Изменение учетных данных</span><span class="sxs-lookup"><span data-stu-id="fc1d9-195">Change credentials</span></span>

<span data-ttu-id="fc1d9-196">использовать учетные данные hello toochange для приложения AD, либо из-за нарушение безопасности или истечения срока действия учетных данных, `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-196">toochange hello credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="fc1d9-197">Используйте toochange пароль:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-197">toochange a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="fc1d9-198">Используйте toochange значение сертификата:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-198">toochange a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="fc1d9-199">Отладка</span><span class="sxs-lookup"><span data-stu-id="fc1d9-199">Debug</span></span>

<span data-ttu-id="fc1d9-200">Возможны следующие ошибки при создании участника службы hello.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-200">You may encounter hello following errors when creating a service principal:</span></span>

* <span data-ttu-id="fc1d9-201">**«Authentication_Unauthorized»** или **«подписка не найден в контексте hello».**</span><span class="sxs-lookup"><span data-stu-id="fc1d9-201">**"Authentication_Unauthorized"** or **"No subscription found in hello context."**</span></span> <span data-ttu-id="fc1d9-202">-Эта ошибка появляется, когда ваша учетная запись не имеет hello [разрешения, необходимые](#required-permissions) на hello Azure Active Directory tooregister приложения.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-202">- You see this error when your account does not have hello [required permissions](#required-permissions) on hello Azure Active Directory tooregister an app.</span></span> <span data-ttu-id="fc1d9-203">Как правило, эта ошибка возникает в тех случаях, когда регистрировать приложения в Azure Active Directory могут только администраторы, а ваша учетная запись не является административной. Попросите вашего администратора tooeither назначить вы tooan роль администратора или tooenable пользователей tooregister приложений.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-203">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin. Ask your administrator tooeither assign you tooan administrator role, or tooenable users tooregister apps.</span></span>

* <span data-ttu-id="fc1d9-204">Ваша учетная запись **«не имеют авторизации tooperform действия «Microsoft.Authorization/roleAssignments/write» с областью «/ subscriptions / {guid}».»**  -Эта ошибка появляется, когда учетная запись имеет достаточные разрешения tooassign удостоверением tooan роли.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-204">Your account **"does not have authorization tooperform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions tooassign a role tooan identity.</span></span> <span data-ttu-id="fc1d9-205">Попросите администратора вашей подписки tooadd вы tooUser доступа к роли администратора.</span><span class="sxs-lookup"><span data-stu-id="fc1d9-205">Ask your subscription administrator tooadd you tooUser Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="fc1d9-206">Примеры приложений</span><span class="sxs-lookup"><span data-stu-id="fc1d9-206">Sample applications</span></span>
<span data-ttu-id="fc1d9-207">Сведения о входе в систему как hello приложения с помощью различных платформ см. в разделе:</span><span class="sxs-lookup"><span data-stu-id="fc1d9-207">For information about logging in as hello application through different platforms, see:</span></span>

* [<span data-ttu-id="fc1d9-208">.NET</span><span class="sxs-lookup"><span data-stu-id="fc1d9-208">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="fc1d9-209">Java</span><span class="sxs-lookup"><span data-stu-id="fc1d9-209">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="fc1d9-210">Node.js</span><span class="sxs-lookup"><span data-stu-id="fc1d9-210">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="fc1d9-211">Python</span><span class="sxs-lookup"><span data-stu-id="fc1d9-211">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="fc1d9-212">Ruby</span><span class="sxs-lookup"><span data-stu-id="fc1d9-212">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="fc1d9-213">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="fc1d9-213">Next steps</span></span>
* <span data-ttu-id="fc1d9-214">Подробные инструкции по установке приложения в Azure для управления ресурсами см. в разделе [tooauthorization руководство разработчика с hello API диспетчера ресурсов Azure](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-214">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide tooauthorization with hello Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="fc1d9-215">см. Дополнительные сведения об использовании сертификатов и Azure CLI tooget [сертификат проверки подлинности на основе субъектов-служб Azure из командной строки Linux](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-215">tooget more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="fc1d9-216">Список доступных действий, которые могут быть предоставлены или запрещены toousers см. в разделе [операций поставщика ресурсов диспетчера ресурсов Azure](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="fc1d9-216">For a list of available actions that can be granted or denied toousers, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
