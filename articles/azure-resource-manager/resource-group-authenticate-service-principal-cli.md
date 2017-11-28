---
title: "Создание удостоверения для приложения Azure с помощью интерфейса командной строки Azure | Документация Майкрософт"
description: "Использование Azure CLI для создания приложения Azure Active Directory и субъекта-службы с последующим предоставлением доступа к ресурсам посредством управления доступом на основе ролей. В статье показано, как выполнять проверку подлинности приложения с помощью пароля или сертификата."
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
ms.openlocfilehash: 3c5826d58887ff1af4df8e66999d9c1a1643bcc7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/03/2017
---
# <a name="use-azure-cli-to-create-a-service-principal-to-access-resources"></a><span data-ttu-id="d6a7d-104">Использование интерфейса командной строки Azure для создания субъекта-службы и доступа к ресурсам</span><span class="sxs-lookup"><span data-stu-id="d6a7d-104">Use Azure CLI to create a service principal to access resources</span></span>

<span data-ttu-id="d6a7d-105">При наличии приложения или сценария, которому требуется доступ к ресурсам, можно настроить удостоверение для приложения и аутентифицировать его с помощью собственных учетных данных.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-105">When you have an app or script that needs to access resources, you can set up an identity for the app and authenticate the app with its own credentials.</span></span> <span data-ttu-id="d6a7d-106">Этот идентификатор известен как субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-106">This identity is known as a service principal.</span></span> <span data-ttu-id="d6a7d-107">Такой подход позволяет выполнить следующие действия:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-107">This approach enables you to:</span></span>

* <span data-ttu-id="d6a7d-108">Назначить удостоверению приложения разрешения, которые отличаются от ваших разрешений.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-108">Assign permissions to the app identity that are different than your own permissions.</span></span> <span data-ttu-id="d6a7d-109">Как правило, приложение получает именно те разрешения, которые требуются для его работы.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-109">Typically, these permissions are restricted to exactly what the app needs to do.</span></span>
* <span data-ttu-id="d6a7d-110">Использовать сертификат для аутентификации при выполнении автоматического сценария.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-110">Use a certificate for authentication when executing an unattended script.</span></span>

<span data-ttu-id="d6a7d-111">В этой статье показано, как настроить использование собственных учетных данных и удостоверения для приложения с помощью [Azure CLI 1.0](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-111">This article shows you how to use [Azure CLI 1.0](../cli-install-nodejs.md) to set up an application to run under its own credentials and identity.</span></span> <span data-ttu-id="d6a7d-112">Установите последнюю версию интерфейса командной строки [Azure CLI 1.0](../cli-install-nodejs.md), чтобы ваша среда соответствовала примерам в этой статье.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-112">Install the latest version of [Azure CLI 1.0](../cli-install-nodejs.md) to make sure your environment matches the examples in this article.</span></span>

## <a name="required-permissions"></a><span data-ttu-id="d6a7d-113">Необходимые разрешения</span><span class="sxs-lookup"><span data-stu-id="d6a7d-113">Required permissions</span></span>
<span data-ttu-id="d6a7d-114">Для работы с этой статьей у вас должен быть достаточный уровень разрешений в подписке в Azure Active Directory и Azure.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-114">To complete this topic, you must have sufficient permissions in both your Azure Active Directory and your Azure subscription.</span></span> <span data-ttu-id="d6a7d-115">В частности, вы должны иметь право на создание приложения в Azure Active Directory и назначение роли субъекту-службе.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-115">Specifically, you must be able to create an app in the Azure Active Directory, and assign the service principal to a role.</span></span> 

<span data-ttu-id="d6a7d-116">Проверить, есть ли у вас соответствующие разрешения, проще всего на портале.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-116">The easiest way to check whether your account has adequate permissions is through the portal.</span></span> <span data-ttu-id="d6a7d-117">Ознакомьтесь с [проверкой наличия необходимых разрешений на портале](resource-group-create-service-principal-portal.md#required-permissions).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-117">See [Check required permission in portal](resource-group-create-service-principal-portal.md#required-permissions).</span></span>

<span data-ttu-id="d6a7d-118">Теперь перейдите к соответствующему разделу, чтобы выполнить проверку подлинности на основе [пароля](#create-service-principal-with-password) или [сертификата](#create-service-principal-with-certificate).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-118">Now, proceed to a section for either [password](#create-service-principal-with-password) or [certificate](#create-service-principal-with-certificate) authentication.</span></span>

## <a name="create-service-principal-with-password"></a><span data-ttu-id="d6a7d-119">Создание субъекта-службы с использованием пароля</span><span class="sxs-lookup"><span data-stu-id="d6a7d-119">Create service principal with password</span></span>
<span data-ttu-id="d6a7d-120">В этом разделе содержатся инструкции, которые помогут вам создать приложение AD с использованием пароля и назначить роль читателя субъекту-службе.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-120">In this section, you perform the steps to create the AD application with a password, and assign the Reader role to the service principal.</span></span>

1. <span data-ttu-id="d6a7d-121">Войдите в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-121">Sign in to your account.</span></span>
   
   ```azurecli
   azure login
   ```
2. <span data-ttu-id="d6a7d-122">Чтобы создать удостоверение приложения, укажите имя приложения и введите пароль, как показано в следующей команде:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-122">To create an app identity, provide the name of the app and a password, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp -p {your-password}
   ```
     
   <span data-ttu-id="d6a7d-123">Возвращается новый субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-123">The new service principal is returned.</span></span> <span data-ttu-id="d6a7d-124">При предоставлении разрешений требуется идентификатор объекта.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-124">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d6a7d-125">Идентификатор GUID, приведенный в именах субъектов-служб, требуется для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-125">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d6a7d-126">Значение этого идентификатора такое же, как и значение идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-126">This guid is the same value as the app id.</span></span> <span data-ttu-id="d6a7d-127">В примерах приложений это значение называется `Client ID`.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-127">In the sample applications, this value is referred to as the `Client ID`.</span></span> 
     
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

3. <span data-ttu-id="d6a7d-128">Предоставьте субъекту-службе разрешения на вашу подписку.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-128">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="d6a7d-129">В этом примере показано, как назначить субъекту-службе роль читателя, которая дает разрешение на чтение всех ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-129">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="d6a7d-130">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-130">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d6a7d-131">Для параметра objectid укажите значение ObjectId, которое использовалось при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-131">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="d6a7d-132">Перед выполнением этой команды нужно подождать некоторое время, чтобы данные нового субъекта-службы распространились в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-132">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d6a7d-133">При выполнении этих команд вручную между задачами обычно проходит достаточно времени.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-133">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d6a7d-134">В сценарий следует добавить шаг ожидания между этими командами (например, `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-134">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="d6a7d-135">Если отображается ошибка и сообщение о том, что субъект в каталоге не существует, выполните команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-135">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId ff863613-e5e2-4a6b-af07-fff6f2de3f4e -o Reader -c /subscriptions/{subscriptionId}/
   ```
   
<span data-ttu-id="d6a7d-136">Вот и все!</span><span class="sxs-lookup"><span data-stu-id="d6a7d-136">That's it!</span></span> <span data-ttu-id="d6a7d-137">Приложение AD и субъект-служба настроены.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-137">Your AD application and service principal are set up.</span></span> <span data-ttu-id="d6a7d-138">В следующем разделе показано, как выполнить вход с использованием учетных данных с помощью Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-138">The next section shows you how to log in with the credential through Azure CLI.</span></span> <span data-ttu-id="d6a7d-139">Если необходимо использовать учетные данные в коде приложения, выполнять действия, описанные ниже, не требуется.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-139">If you want to use the credential in your code application, you do not need to continue with this topic.</span></span> <span data-ttu-id="d6a7d-140">Вы можете перейти к разделу [Примеры приложений](#sample-applications) , где приведены примеры входа с использованием идентификатора приложения и пароля.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-140">You can jump to the [Sample applications](#sample-applications) for examples of logging in with your application id and password.</span></span> 

### <a name="provide-credentials-through-azure-cli"></a><span data-ttu-id="d6a7d-141">Предоставление учетных данных через Azure CLI</span><span class="sxs-lookup"><span data-stu-id="d6a7d-141">Provide credentials through Azure CLI</span></span>
<span data-ttu-id="d6a7d-142">Теперь следует войти в систему от имени приложения для выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-142">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="d6a7d-143">При каждом входе в приложение AD в качестве субъекта-службы необходимо указать идентификатор клиента каталога.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-143">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d6a7d-144">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-144">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d6a7d-145">Чтобы получить идентификатор клиента для текущей аутентифицированной подписки, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-145">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d6a7d-146">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-146">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
     <span data-ttu-id="d6a7d-147">Если необходимо получить идентификатор клиента другой подписки, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-147">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d6a7d-148">Если необходимо получить идентификатор клиента для входа в систему, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-148">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp --json
   ```
   
     <span data-ttu-id="d6a7d-149">Значение, используемые для входа в систему, — это идентификатор GUID, приведенный в именах субъектов-служб.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-149">The value to use for logging in is the guid listed in the service principal names.</span></span>
   
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
3. <span data-ttu-id="d6a7d-150">Выполните вход как субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-150">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login -u 7132aca4-1bdb-4238-ad81-996ff91d8db4 --service-principal --tenant {tenant-id}
   ```
   
    <span data-ttu-id="d6a7d-151">Появится запрос на ввод пароля.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-151">You are prompted for the password.</span></span> <span data-ttu-id="d6a7d-152">Введите пароль, который вы задали при создании приложения AD.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-152">Provide the password you specified when creating the AD application.</span></span>
   
   ```azurecli
   info:    Executing command login
   Password: ********
   ```

<span data-ttu-id="d6a7d-153">Теперь вы прошли проверку подлинности от имени субъекта-службы для созданного вами приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-153">You are now authenticated as the service principal for the service principal that you created.</span></span>

<span data-ttu-id="d6a7d-154">Кроме того, чтобы выполнить вход, можно вызывать операции REST из командной строки.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-154">Alternatively, you can invoke REST operations from the command line to log in.</span></span> <span data-ttu-id="d6a7d-155">Из ответа службы аутентификации можно получить маркер доступа, пригодный для использования в других операциях.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-155">From the authentication response, you can retrieve the access token for use with other operations.</span></span> <span data-ttu-id="d6a7d-156">Пример получения маркера доступа путем вызова операции REST приведен в разделе [Создание маркера доступа](resource-manager-rest-api.md#generating-an-access-token).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-156">For an example of retrieving the access token by invoking REST operations, see [Generating an Access Token](resource-manager-rest-api.md#generating-an-access-token).</span></span>

## <a name="create-service-principal-with-certificate"></a><span data-ttu-id="d6a7d-157">Создание субъекта-службы с использованием сертификата</span><span class="sxs-lookup"><span data-stu-id="d6a7d-157">Create service principal with certificate</span></span>
<span data-ttu-id="d6a7d-158">В этом разделе содержатся инструкции, которые помогут вам:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-158">In this section, you perform the steps to:</span></span>

* <span data-ttu-id="d6a7d-159">создать самозаверяющий сертификат;</span><span class="sxs-lookup"><span data-stu-id="d6a7d-159">create a self-signed certificate</span></span>
* <span data-ttu-id="d6a7d-160">создать приложение AD с сертификатом и субъектом-службой;</span><span class="sxs-lookup"><span data-stu-id="d6a7d-160">create the AD application with the certificate, and the service principal</span></span>
* <span data-ttu-id="d6a7d-161">назначить роль "Читатель" субъекту-службе.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-161">assign the Reader role to the service principal</span></span>

<span data-ttu-id="d6a7d-162">Для выполнения этих действий в системе должен быть установлен [OpenSSL](http://www.openssl.org/) .</span><span class="sxs-lookup"><span data-stu-id="d6a7d-162">To complete these steps, you must have [OpenSSL](http://www.openssl.org/) installed.</span></span>

1. <span data-ttu-id="d6a7d-163">Создать самозаверяющий сертификат.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-163">Create a self-signed certificate.</span></span>
   
   ```
   openssl req -x509 -days 3650 -newkey rsa:2048 -out cert.pem -nodes -subj '/CN=exampleapp'
   ```

2. <span data-ttu-id="d6a7d-164">На предыдущем шаге были созданы два файла — privkey.pem и cert.pem.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-164">The preceding step created two files - privkey.pem and cert.pem.</span></span> <span data-ttu-id="d6a7d-165">Объедините открытый и закрытый ключи в один файл.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-165">Combine the public and private keys into a single file.</span></span>

   ```
   cat privkey.pem cert.pem > examplecert.pem
   ```

3. <span data-ttu-id="d6a7d-166">Откройте файл **examplecert.pem** и найдите длинную последовательность символов между тегами **-----BEGIN CERTIFICATE-----** и **-----END CERTIFICATE-----**.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-166">Open the **examplecert.pem** file and look for the long sequence of characters between **-----BEGIN CERTIFICATE-----** and **-----END CERTIFICATE-----**.</span></span> <span data-ttu-id="d6a7d-167">Скопируйте данные сертификата.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-167">Copy the certificate data.</span></span> <span data-ttu-id="d6a7d-168">Во время создания субъекта-службы эти данные передаются в качестве параметра.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-168">You pass this data as a parameter when creating the service principal.</span></span>

4. <span data-ttu-id="d6a7d-169">Войдите в свою учетную запись.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-169">Sign in to your account.</span></span>

   ```azurecli
   azure login
   ```
5. <span data-ttu-id="d6a7d-170">Чтобы создать субъект-службу, укажите имя приложения и данные сертификата, как показано в следующей команде:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-170">To create the service principal, provide the name of the app and the certificate data, as shown in the following command:</span></span>
     
   ```azurecli
   azure ad sp create -n exampleapp --cert-value {certificate data}
   ```
     
   <span data-ttu-id="d6a7d-171">Возвращается новый субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-171">The new service principal is returned.</span></span> <span data-ttu-id="d6a7d-172">При предоставлении разрешений требуется идентификатор объекта.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-172">The Object Id is needed when granting permissions.</span></span> <span data-ttu-id="d6a7d-173">Идентификатор GUID, приведенный в именах субъектов-служб, требуется для входа в систему.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-173">The guid listed with the Service Principal Names is needed when logging in.</span></span> <span data-ttu-id="d6a7d-174">Значение этого идентификатора такое же, как и значение идентификатора приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-174">This guid is the same value as the app id.</span></span> <span data-ttu-id="d6a7d-175">В примерах приложений это значение называется идентификатором клиента.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-175">In the sample applications, this value is referred to as the Client ID.</span></span> 
     
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
6. <span data-ttu-id="d6a7d-176">Предоставьте субъекту-службе разрешения на вашу подписку.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-176">Grant the service principal permissions on your subscription.</span></span> <span data-ttu-id="d6a7d-177">В этом примере показано, как назначить субъекту-службе роль читателя, которая дает разрешение на чтение всех ресурсов в подписке.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-177">In this example, you add the service principal to the Reader role, which grants permission to read all resources in the subscription.</span></span> <span data-ttu-id="d6a7d-178">Сведения о других ролях см. в статье [RBAC: встроенные роли](../active-directory/role-based-access-built-in-roles.md).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-178">For other roles, see [RBAC: Built-in roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="d6a7d-179">Для параметра objectid укажите значение ObjectId, которое использовалось при создании приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-179">For the objectid parameter, provide the Object Id that you used when creating the application.</span></span> <span data-ttu-id="d6a7d-180">Перед выполнением этой команды нужно подождать некоторое время, чтобы данные нового субъекта-службы распространились в Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-180">Before running this command, you must allow some time for the new service principal to propagate throughout Azure Active Directory.</span></span> <span data-ttu-id="d6a7d-181">При выполнении этих команд вручную между задачами обычно проходит достаточно времени.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-181">When you run these commands manually, usually enough time has elapsed between tasks.</span></span> <span data-ttu-id="d6a7d-182">В сценарий следует добавить шаг ожидания между этими командами (например, `sleep 15`).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-182">In a script, you should add a step to sleep between the commands (like `sleep 15`).</span></span> <span data-ttu-id="d6a7d-183">Если отображается ошибка и сообщение о том, что субъект в каталоге не существует, выполните команду еще раз.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-183">If you see an error stating the principal does not exist in the directory, rerun the command.</span></span>
   
   ```azurecli
   azure role assignment create --objectId 7dbc8265-51ed-4038-8e13-31948c7f4ce7 -o Reader -c /subscriptions/{subscriptionId}/
   ```
  
### <a name="provide-certificate-through-automated-azure-cli-script"></a><span data-ttu-id="d6a7d-184">Предоставление сертификата с помощью автоматизированного сценария для интерфейса командной строки Azure</span><span class="sxs-lookup"><span data-stu-id="d6a7d-184">Provide certificate through automated Azure CLI script</span></span>
<span data-ttu-id="d6a7d-185">Теперь следует войти в систему от имени приложения для выполнения операций.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-185">Now, you need to log in as the application to perform operations.</span></span>

1. <span data-ttu-id="d6a7d-186">При каждом входе в приложение AD в качестве субъекта-службы необходимо указать идентификатор клиента каталога.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-186">Whenever you sign in as a service principal, you need to provide the tenant id of the directory for your AD app.</span></span> <span data-ttu-id="d6a7d-187">Клиент — это экземпляр Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-187">A tenant is an instance of Azure Active Directory.</span></span> <span data-ttu-id="d6a7d-188">Чтобы получить идентификатор клиента для текущей аутентифицированной подписки, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-188">To retrieve the tenant id for your currently authenticated subscription, use:</span></span>
   
   ```azurecli
   azure account show
   ```
   
   <span data-ttu-id="d6a7d-189">Возвращаемые данные:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-189">Which returns:</span></span>
   
   ```azurecli
   info:    Executing command account show
   data:    Name                        : Windows Azure MSDN - Visual Studio Ultimate
   data:    ID                          : {guid}
   data:    State                       : Enabled
   data:    Tenant ID                   : {guid}
   data:    Is Default                  : true
   ...
   ```
   
   <span data-ttu-id="d6a7d-190">Если необходимо получить идентификатор клиента другой подписки, используйте следующую команду:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-190">If you need to get the tenant id of another subscription, use the following command:</span></span>
   
   ```azurecli
   azure account show -s {subscription-id}
   ```
2. <span data-ttu-id="d6a7d-191">Чтобы получить отпечаток сертификата и удалить ненужные символы, используйте такую команду:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-191">To retrieve the certificate thumbprint and remove unneeded characters, use:</span></span>
   
   ```
   openssl x509 -in "C:\certificates\examplecert.pem" -fingerprint -noout | sed 's/SHA1 Fingerprint=//g'  | sed 's/://g'
   ```
   
   <span data-ttu-id="d6a7d-192">Возвращается значение отпечатка следующего вида:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-192">Which returns a thumbprint value similar to:</span></span>
   
   ```
   30996D9CE48A0B6E0CD49DBB9A48059BF9355851
   ```
3. <span data-ttu-id="d6a7d-193">Если необходимо получить идентификатор клиента для входа в систему, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-193">If you need to retrieve the client id to use for logging in, use:</span></span>
   
   ```azurecli
   azure ad sp show -c exampleapp
   ```
   
   <span data-ttu-id="d6a7d-194">Значение, используемые для входа в систему, — это идентификатор GUID, приведенный в именах субъектов-служб.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-194">The value to use for logging in is the guid listed in the service principal names.</span></span>
     
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
4. <span data-ttu-id="d6a7d-195">Выполните вход как субъект-служба.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-195">Log in as the service principal.</span></span>
   
   ```azurecli
   azure login --service-principal --tenant {tenant-id} -u 4fd39843-c338-417d-b549-a545f584a745 --certificate-file C:\certificates\examplecert.pem --thumbprint {thumbprint}
   ```

<span data-ttu-id="d6a7d-196">После этого субъект-служба для созданного вами приложения Azure Active Directory пройдет проверку подлинности.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-196">You are now authenticated as the service principal for the Azure Active Directory application that you created.</span></span>

## <a name="change-credentials"></a><span data-ttu-id="d6a7d-197">Изменение учетных данных</span><span class="sxs-lookup"><span data-stu-id="d6a7d-197">Change credentials</span></span>

<span data-ttu-id="d6a7d-198">Чтобы изменить учетные данные для приложения AD из-за нарушения безопасности или истечения их срока действия, используйте команду `azure ad app set`.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-198">To change the credentials for an AD app, either because of a security compromise or a credential expiration, use `azure ad app set`.</span></span>

<span data-ttu-id="d6a7d-199">Чтобы изменить пароль, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-199">To change a password, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --password p@ssword
```

<span data-ttu-id="d6a7d-200">Чтобы изменить значение сертификата, используйте следующую команду.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-200">To change a certificate value, use:</span></span>

```azurecli
azure ad app set --applicationId 4fd39843-c338-417d-b549-a545f584a745 --cert-value {certificate data}
```

## <a name="debug"></a><span data-ttu-id="d6a7d-201">Отладка</span><span class="sxs-lookup"><span data-stu-id="d6a7d-201">Debug</span></span>

<span data-ttu-id="d6a7d-202">При создании субъекта-службы могут возникнуть следующие ошибки:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-202">You may encounter the following errors when creating a service principal:</span></span>

* <span data-ttu-id="d6a7d-203">**"Authentication_Unauthorized"** (Аутентификация не выполнена) или **"No subscription found in the context"** (В контексте не удалось найти подписку).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-203">**"Authentication_Unauthorized"** or **"No subscription found in the context."**</span></span> <span data-ttu-id="d6a7d-204">— Эта ошибка может отобразиться, если учетная запись не имеет [необходимых разрешений](#required-permissions) в Azure Active Directory для регистрации приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-204">- You see this error when your account does not have the [required permissions](#required-permissions) on the Azure Active Directory to register an app.</span></span> <span data-ttu-id="d6a7d-205">Как правило, эта ошибка возникает в тех случаях, когда регистрировать приложения в Azure Active Directory могут только администраторы, а ваша учетная запись не является административной.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-205">Typically, you see this error when only admin users in your Azure Active Directory can register apps, and your account is not an admin.</span></span> <span data-ttu-id="d6a7d-206">Попросите администратора назначить вам роль администратора или разрешить пользователям регистрировать приложения.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-206">Ask your administrator to either assign you to an administrator role, or to enable users to register apps.</span></span>

* <span data-ttu-id="d6a7d-207">Ваша учетная запись **"не авторизована для выполнения действия 'Microsoft.Authorization/roleAssignments/write' с областью '/subscriptions/{guid}'."** Эта ошибка возникает, когда учетная запись не имеет достаточно разрешений для назначения роли удостоверению.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-207">Your account **"does not have authorization to perform action 'Microsoft.Authorization/roleAssignments/write' over scope '/subscriptions/{guid}'."** - You see this error when your account does not have sufficient permissions to assign a role to an identity.</span></span> <span data-ttu-id="d6a7d-208">Попросите администратора подписки назначить вам роль администратора доступа пользователей.</span><span class="sxs-lookup"><span data-stu-id="d6a7d-208">Ask your subscription administrator to add you to User Access Administrator role.</span></span>

## <a name="sample-applications"></a><span data-ttu-id="d6a7d-209">Примеры приложений</span><span class="sxs-lookup"><span data-stu-id="d6a7d-209">Sample applications</span></span>
<span data-ttu-id="d6a7d-210">Сведения о входе в систему в качестве приложения с помощью различных платформ см. в следующих разделах:</span><span class="sxs-lookup"><span data-stu-id="d6a7d-210">For information about logging in as the application through different platforms, see:</span></span>

* [<span data-ttu-id="d6a7d-211">.NET</span><span class="sxs-lookup"><span data-stu-id="d6a7d-211">.NET</span></span>](/dotnet/azure/dotnet-sdk-azure-authenticate?view=azure-dotnet)
* [<span data-ttu-id="d6a7d-212">Java</span><span class="sxs-lookup"><span data-stu-id="d6a7d-212">Java</span></span>](/java/azure/java-sdk-azure-authenticate)
* [<span data-ttu-id="d6a7d-213">Node.js</span><span class="sxs-lookup"><span data-stu-id="d6a7d-213">Node.js</span></span>](/nodejs/azure/node-sdk-azure-get-started?view=azure-node-2.0.0)
* [<span data-ttu-id="d6a7d-214">Python</span><span class="sxs-lookup"><span data-stu-id="d6a7d-214">Python</span></span>](/python/azure/python-sdk-azure-authenticate?view=azure-python)
* [<span data-ttu-id="d6a7d-215">Ruby</span><span class="sxs-lookup"><span data-stu-id="d6a7d-215">Ruby</span></span>](https://azure.microsoft.com/documentation/samples/resource-manager-ruby-resources-and-groups/)

## <a name="next-steps"></a><span data-ttu-id="d6a7d-216">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="d6a7d-216">Next steps</span></span>
* <span data-ttu-id="d6a7d-217">Подробные инструкции по интеграции приложения в Azure для управления ресурсами см. в [Управление ресурсами клиента с помощью Azure Active Directory и Resource Manager](resource-manager-api-authentication.md).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-217">For detailed steps on integrating an application into Azure for managing resources, see [Developer's guide to authorization with the Azure Resource Manager API](resource-manager-api-authentication.md).</span></span>
* <span data-ttu-id="d6a7d-218">Дополнительные сведения об использовании сертификатов и Azure CLI см. в статье [Certificate-based auth with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx) (Проверка подлинности на основе сертификата для субъектов-служб Azure из командной строки Linux).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-218">To get more information about using certificates and Azure CLI, see [Certificate-based authentication with Azure Service Principals from Linux command line](http://blogs.msdn.com/b/arsen/archive/2015/09/18/certificate-based-auth-with-azure-service-principals-from-linux-command-line.aspx).</span></span> 
* <span data-ttu-id="d6a7d-219">Список доступных действий, которые можно разрешить или запретить пользователям, см. в разделе [Операции поставщиков ресурсов Azure Resource Manager](../active-directory/role-based-access-control-resource-provider-operations.md).</span><span class="sxs-lookup"><span data-stu-id="d6a7d-219">For a list of available actions that can be granted or denied to users, see [Azure Resource Manager Resource Provider operations](../active-directory/role-based-access-control-resource-provider-operations.md).</span></span>
