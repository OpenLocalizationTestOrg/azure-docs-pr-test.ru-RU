---
title: "подключение SSL aaaConfigure в базе данных Azure для PostgreSQL | Документы Microsoft"
description: "Инструкции и сведения tooconfigure базы данных Azure для PostgreSQL и связанные с ними приложения tooproperly использовать подключения SSL."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 96a68088acd924196701e8d618d9d5edf44cb548
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="b6b70-103">Настройка SSL-соединения в базе данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b6b70-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="b6b70-104">База данных Azure для PostgreSQL является предпочтительным для подключения к toohello приложения клиента службы PostgreSQL, с помощью Secure Sockets Layer (SSL).</span><span class="sxs-lookup"><span data-stu-id="b6b70-104">Azure Database for PostgreSQL prefers connecting your client applications toohello PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="b6b70-105">Принудительное SSL-подключений между сервером базы данных и клиентские приложения помогает защитить от атак «злоумышленник в середине hello» путем шифрования hello потока данных между сервером hello и приложения.</span><span class="sxs-lookup"><span data-stu-id="b6b70-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

<span data-ttu-id="b6b70-106">По умолчанию hello службы базы данных PostgreSQL является настроенным toorequire SSL-подключение.</span><span class="sxs-lookup"><span data-stu-id="b6b70-106">By default, hello PostgreSQL database service is configured toorequire SSL connection.</span></span> <span data-ttu-id="b6b70-107">При необходимости можно отключить для соединения tooyour базы данных службы, если клиентское приложение не поддерживает SSL подключение с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="b6b70-107">Optionally, you can disable requiring SSL for connecting tooyour database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="b6b70-108">Применение SSL-соединений</span><span class="sxs-lookup"><span data-stu-id="b6b70-108">Enforcing SSL connections</span></span>
<span data-ttu-id="b6b70-109">Для всех баз данных Azure для подготовки в рамках hello портал Azure и CLI серверов PostgreSQL принудительное выполнение SSL-соединений включен по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b6b70-109">For all Azure Database for PostgreSQL servers provisioned through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="b6b70-110">Аналогичным образом строки подключения, предварительно определенные в параметрах «Строки соединения» hello в области сервера в hello портал Azure включают hello необходимые параметры для общий языков tooconnect tooyour сервер баз данных с помощью протокола SSL.</span><span class="sxs-lookup"><span data-stu-id="b6b70-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="b6b70-111">Hello SSL параметра различается в зависимости от соединителя hello, например «ssl = true» или «sslmode = требуют» или» sslmode = необходимые» и др..</span><span class="sxs-lookup"><span data-stu-id="b6b70-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="b6b70-112">Настройка применения SSL</span><span class="sxs-lookup"><span data-stu-id="b6b70-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="b6b70-113">При необходимости применение SSL-соединений можно отключить.</span><span class="sxs-lookup"><span data-stu-id="b6b70-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="b6b70-114">Microsoft Azure Корпорация Майкрософт рекомендует включить tooalways **применять SSL-соединение** для повышения безопасности.</span><span class="sxs-lookup"><span data-stu-id="b6b70-114">Microsoft Azure recommends tooalways enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-hello-azure-portal"></a><span data-ttu-id="b6b70-115">С помощью портала Azure hello</span><span class="sxs-lookup"><span data-stu-id="b6b70-115">Using hello Azure portal</span></span>
<span data-ttu-id="b6b70-116">Войдите в сервер базы данных Azure для PostgreSQL и щелкните **Безопасность подключения**.</span><span class="sxs-lookup"><span data-stu-id="b6b70-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="b6b70-117">Используйте tooenable кнопка переключателя hello или отключите hello **применять SSL-соединение** параметр.</span><span class="sxs-lookup"><span data-stu-id="b6b70-117">Use hello toggle button tooenable or disable hello **Enforce SSL connection** setting.</span></span> <span data-ttu-id="b6b70-118">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="b6b70-118">Then click **Save**.</span></span> 

![Безопасность подключения: отключить применение SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="b6b70-120">Приветствия можно проверить, просмотрев hello **Обзор** страницы приветствия toosee **SSL применять состояния** индикатора.</span><span class="sxs-lookup"><span data-stu-id="b6b70-120">You can confirm hello setting by viewing hello **Overview** page toosee hello **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="b6b70-121">Использование Azure CLI</span><span class="sxs-lookup"><span data-stu-id="b6b70-121">Using Azure CLI</span></span>
<span data-ttu-id="b6b70-122">Можно включить или отключить hello **применения ssl** с помощью параметра `Enabled` или `Disabled` значения соответственно в Azure CLI.</span><span class="sxs-lookup"><span data-stu-id="b6b70-122">You can enable or disable hello **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="b6b70-123">Проверка поддержки SSL-соединений в приложении или платформе</span><span class="sxs-lookup"><span data-stu-id="b6b70-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="b6b70-124">Многие распространенные платформы приложений, использующие PostgreSQL для служб базы данных, такие как Drupal и Django, по умолчанию не включают SSL при установке.</span><span class="sxs-lookup"><span data-stu-id="b6b70-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="b6b70-125">Включение SSL-подключения должны выполняться после установки или с помощью приложения toohello конкретных команд CLI.</span><span class="sxs-lookup"><span data-stu-id="b6b70-125">Enabling SSL connectivity must be done after installation or through CLI commands specific toohello application.</span></span> <span data-ttu-id="b6b70-126">Если сервер PostgreSQL вводит SSL-соединений и hello связанное приложение не настроено должным образом, приложение hello может завершиться ошибкой tooconnect tooyour базы данных сервера.</span><span class="sxs-lookup"><span data-stu-id="b6b70-126">If your PostgreSQL server is enforcing SSL connections and hello associated application is not configured properly, hello application may fail tooconnect tooyour database server.</span></span> <span data-ttu-id="b6b70-127">Обратитесь к документации toolearn приложения как tooenable SSL-подключения.</span><span class="sxs-lookup"><span data-stu-id="b6b70-127">Consult your application's documentation toolearn how tooenable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="b6b70-128">Приложения, требующие проверки сертификата для SSL-соединений</span><span class="sxs-lookup"><span data-stu-id="b6b70-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="b6b70-129">В некоторых случаях приложений требуется наличие файла локального сертификата, созданного из доверенных tooconnect CER-файл сертификата центра сертификации (ЦС), безопасно.</span><span class="sxs-lookup"><span data-stu-id="b6b70-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) tooconnect securely.</span></span> <span data-ttu-id="b6b70-130">См. следующие шаги tooobtain hello CER-файл hello, декодировать сертификат hello и привязать его tooyour приложения.</span><span class="sxs-lookup"><span data-stu-id="b6b70-130">See hello following steps tooobtain hello .cer file, decode hello certificate and bind it tooyour application.</span></span>

### <a name="download-hello-certificate-file-from-hello-certificate-authority-ca"></a><span data-ttu-id="b6b70-131">Загрузить файл сертификата hello hello центра сертификации (ЦС)</span><span class="sxs-lookup"><span data-stu-id="b6b70-131">Download hello certificate file from hello Certificate Authority (CA)</span></span> 
<span data-ttu-id="b6b70-132">Hello сертификат требуется toocommunicate по протоколу SSL с базой данных Azure для расположен сервер PostgreSQL [здесь](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="b6b70-132">hello certificate needed toocommunicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="b6b70-133">Загрузите hello файл сертификата локально.</span><span class="sxs-lookup"><span data-stu-id="b6b70-133">Download hello certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="b6b70-134">Скачивание и установка OpenSSL на компьютер</span><span class="sxs-lookup"><span data-stu-id="b6b70-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="b6b70-135">файл сертификата hello toodecode, необходимые для вашего приложения tooconnect безопасно tooyour сервера базы данных, необходимо tooinstall OpenSSL на локальном компьютере.</span><span class="sxs-lookup"><span data-stu-id="b6b70-135">toodecode hello certificate file needed for your application tooconnect securely tooyour database server, you need tooinstall OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="b6b70-136">Для Linux, OS X или Unix</span><span class="sxs-lookup"><span data-stu-id="b6b70-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="b6b70-137">библиотеки OpenSSL Hello предоставляются в исходном коде непосредственно из hello [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="b6b70-137">hello OpenSSL libraries are provided in source code directly from hello [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="b6b70-138">Hello следующим инструкциям tooinstall необходимые шаги hello OpenSSL на Компьютере Linux.</span><span class="sxs-lookup"><span data-stu-id="b6b70-138">hello following instructions guide you through hello steps necessary tooinstall OpenSSL on your Linux PC.</span></span> <span data-ttu-id="b6b70-139">В этой статье используется команды известные toowork на Ubuntu 12.04 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="b6b70-139">This article uses commands known toowork on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="b6b70-140">Откройте сеанс терминала и установите OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="b6b70-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="b6b70-141">Извлеките файлы hello hello пакет</span><span class="sxs-lookup"><span data-stu-id="b6b70-141">Extract hello files from hello download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="b6b70-142">Введите каталог hello, где были извлечены файлы hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-142">Enter hello directory where hello files were extracted.</span></span> <span data-ttu-id="b6b70-143">По умолчанию это должен быть каталог, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="b6b70-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="b6b70-144">Настройте OpenSSL, выполнив следующую команду hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-144">Configure OpenSSL by executing hello following command.</span></span> <span data-ttu-id="b6b70-145">Если требуется hello файлов в папке отличается от /usr/local/openssl, сделайте убедиться, что следующие hello toochange соответствующим образом.</span><span class="sxs-lookup"><span data-stu-id="b6b70-145">If you want hello files in a folder different than /usr/local/openssl, make sure toochange hello following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="b6b70-146">Теперь, когда OpenSSL настроен правильно, необходимо toocompile его tooconvert свой сертификат.</span><span class="sxs-lookup"><span data-stu-id="b6b70-146">Now that OpenSSL is configured properly, you need toocompile it tooconvert your certificate.</span></span> <span data-ttu-id="b6b70-147">toocompile запуска hello следующую команду:</span><span class="sxs-lookup"><span data-stu-id="b6b70-147">toocompile, run hello following command:</span></span>

```bash
make
```
<span data-ttu-id="b6b70-148">После завершения компиляции вы будете готовы tooinstall OpenSSL как EXE-файл, выполнив следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6b70-148">Once compiling is complete, you're ready tooinstall OpenSSL as an executable by running hello following command:</span></span>
```bash
make install
```
<span data-ttu-id="b6b70-149">tooconfirm, что вы успешно установили OpenSSL в вашей системе, выполнения hello следующую команду и проверьте, что вы получаете hello toomake такие же выходные данные.</span><span class="sxs-lookup"><span data-stu-id="b6b70-149">tooconfirm that you've successfully installed OpenSSL on your system, run hello following command and check toomake sure you get hello same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="b6b70-150">В случае успешного выполнения должны появиться следующие сообщения hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-150">If successful you should see hello following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="b6b70-151">Для Windows</span><span class="sxs-lookup"><span data-stu-id="b6b70-151">For Windows</span></span>
<span data-ttu-id="b6b70-152">Установка OpenSSL на ПК с Windows может быть выполнена в hello следующих способов:</span><span class="sxs-lookup"><span data-stu-id="b6b70-152">Installing OpenSSL on a Windows PC can be done in hello following ways:</span></span>
1. <span data-ttu-id="b6b70-153">**(Рекомендуется)**  С помощью встроенных функций Bash Windows hello в Windows 10 и более поздних версий, OpenSSL устанавливается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="b6b70-153">**(Recommended)** Using hello built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="b6b70-154">Инструкции по обнаружение tooenable функциональность Bash Windows в Windows 10 [здесь](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="b6b70-154">Instructions on how tooenable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="b6b70-155">До загрузки приложения Win32/64, предоставленные сообществом hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-155">Through downloading a Win32/64 application provided by hello community.</span></span> <span data-ttu-id="b6b70-156">Hello OpenSSL Software Foundation не предоставляют и не утверждает любого конкретного установщиков Windows, они предоставляют список доступных установщики [здесь](https://wiki.openssl.org/index.php/Binaries)</span><span class="sxs-lookup"><span data-stu-id="b6b70-156">While hello OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="b6b70-157">Декодируйте файл сертификата</span><span class="sxs-lookup"><span data-stu-id="b6b70-157">Decode your certificate file</span></span>
<span data-ttu-id="b6b70-158">Hello загрузить корневой ЦС, файл находится в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="b6b70-158">hello downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="b6b70-159">Используйте файл сертификата hello toodecode OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="b6b70-159">Use OpenSSL toodecode hello certificate file.</span></span> <span data-ttu-id="b6b70-160">toodo таким образом, выполните следующую команду OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="b6b70-160">toodo so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-tooazure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="b6b70-161">Подключение с использованием проверки подлинности сертификата SSL tooAzure базы данных PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="b6b70-161">Connecting tooAzure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="b6b70-162">Теперь, когда успешно декодировать свой сертификат, вы может теперь tooyour сервера базы данных безопасное подключение по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="b6b70-162">Now that you have successfully decoded your certificate, you can now connect tooyour database server securely over SSL.</span></span> <span data-ttu-id="b6b70-163">проверка сертификатов сервера tooallow, hello сертификат необходимо разместить в ~/.postgresql/root.crt hello файл в корневом каталоге пользователя hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-163">tooallow server certificate verification, hello certificate must be placed in hello file ~/.postgresql/root.crt in hello user's home directory.</span></span> <span data-ttu-id="b6b70-164">(В Microsoft Windows hello файл с именем % APPDATA%\postgresql\root.crt.).</span><span class="sxs-lookup"><span data-stu-id="b6b70-164">(On Microsoft Windows hello file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="b6b70-165">Hello ниже приведены инструкции по подключению для PostgreSQL tooAzure базы данных.</span><span class="sxs-lookup"><span data-stu-id="b6b70-165">hello following provides instructions for connecting tooAzure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="b6b70-166">В настоящее время имеется известная проблема, если вы используете «sslmode = проверка full» в службе toohello подключение, подключение hello, будут завершаться hello следующая ошибка: _сертификат сервера для "&lt;области&gt;. Control.Database.Windows.NET» (и 7 имена) не соответствует имени узла "&lt;servername&gt;. postgres.database.azure.com»._</span><span class="sxs-lookup"><span data-stu-id="b6b70-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection toohello service, hello connection will fail with hello following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="b6b70-167">Если «sslmode = проверка полный» — требуется, используйте соглашение об именовании hello server  **&lt;servername&gt;. database.windows.net** как локальное имя строки подключения.</span><span class="sxs-lookup"><span data-stu-id="b6b70-167">If "sslmode=verify-full" is required, please use hello server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="b6b70-168">Мы планируем tooremove это ограничение в будущем hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-168">We plan tooremove this limitation in hello future.</span></span> <span data-ttu-id="b6b70-169">Соединения с использованием других [режимы SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) следует продолжить соглашение об именовании узлов hello предпочитаемый toouse  **&lt;servername&gt;. postgres.database.azure.com**.</span><span class="sxs-lookup"><span data-stu-id="b6b70-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue toouse hello preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="b6b70-170">Использование служебной программы командной строки psql</span><span class="sxs-lookup"><span data-stu-id="b6b70-170">Using psql command-line utility</span></span>
<span data-ttu-id="b6b70-171">Здравствуй, следующий пример показывает, как toosuccessfully подключения сервера tooyour PostgreSQL, с помощью программы командной строки psql hello.</span><span class="sxs-lookup"><span data-stu-id="b6b70-171">hello following example shows you how toosuccessfully connect tooyour PostgreSQL server using hello psql command-line utility.</span></span> <span data-ttu-id="b6b70-172">Используйте hello `root.crt` файл, созданный и hello `sslmode=verify-ca` или `sslmode=verify-full` параметр.</span><span class="sxs-lookup"><span data-stu-id="b6b70-172">Use hello `root.crt` file created and hello `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="b6b70-173">С помощью интерфейса командной строки hello PostgreSQL, выполните следующую команду hello:</span><span class="sxs-lookup"><span data-stu-id="b6b70-173">Using hello PostgreSQL command-line interface, execute hello following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="b6b70-174">В случае успешного выполнения появляется hello следующие выходные данные:</span><span class="sxs-lookup"><span data-stu-id="b6b70-174">If successful, you receive hello following output:</span></span>
```bash
Password for user mylogin@mypgserver-20170401:
psql (9.6.2)
WARNING: Console code page (437) differs from Windows code page (1252)
     8-bit characters might not work correctly. See psql reference
     page "Notes for Windows users" for details.
SSL connection (protocol: TLSv1.2, cipher: ECDHE-RSA-AES256-SHA384, bits: 256, compression: off)
Type "help" for help.

postgres=>
```

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="b6b70-175">Использование инструмента графического пользовательского интерфейса pgAdmin</span><span class="sxs-lookup"><span data-stu-id="b6b70-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="b6b70-176">Настроить tooconnect pgAdmin 4 безопасно по протоколу SSL, необходимо tooset hello `SSL mode = Verify-CA` или `SSL mode = Verify-Full` следующим образом:</span><span class="sxs-lookup"><span data-stu-id="b6b70-176">Configuring pgAdmin 4 tooconnect securely over SSL requires you tooset hello `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Снимок экрана pgAdmin: настройка параметра "SSL mode" (Режим SSL) на вкладке "Connection" (Подключение)](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="b6b70-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="b6b70-178">Next steps</span></span>
<span data-ttu-id="b6b70-179">Сведения о вариантах подключения приложений см. в статье [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="b6b70-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
