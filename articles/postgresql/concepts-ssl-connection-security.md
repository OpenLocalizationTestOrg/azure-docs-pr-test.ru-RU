---
title: "Настройка SSL-соединения в базе данных Azure для PostgreSQL | Документация Майкрософт"
description: "Инструкции и сведения о настройке базы данных Azure для PostgreSQL и связанных приложений для правильного использования SSL-соединений."
services: postgresql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: postgresql
ms.custom: 
ms.topic: article
ms.date: 05/15/2017
ms.openlocfilehash: 685aa4c2f75b7c3260ca737f7c786157480b2d90
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 08/29/2017
---
# <a name="configure-ssl-connectivity-in-azure-database-for-postgresql"></a><span data-ttu-id="69857-103">Настройка SSL-соединения в базе данных Azure для PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="69857-103">Configure SSL connectivity in Azure Database for PostgreSQL</span></span>
<span data-ttu-id="69857-104">База данных Azure для PostgreSQL предпочитает подключать клиентские приложения к службе PostgreSQL с помощью SSL (Secure Sockets Layer).</span><span class="sxs-lookup"><span data-stu-id="69857-104">Azure Database for PostgreSQL prefers connecting your client applications to the PostgreSQL service using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="69857-105">Применение SSL-соединений между сервером базы данных и клиентскими приложениями обеспечивает защиту от атак "злоумышленник в середине" за счет шифрования потока данных между сервером и приложением.</span><span class="sxs-lookup"><span data-stu-id="69857-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

<span data-ttu-id="69857-106">По умолчанию в службе базы данных PostgreSQL настроено обязательное использование SSL-соединения.</span><span class="sxs-lookup"><span data-stu-id="69857-106">By default, the PostgreSQL database service is configured to require SSL connection.</span></span> <span data-ttu-id="69857-107">При необходимости можно отключить обязательное использование SSL при подключении к службе базы данных, если клиентское приложение не поддерживает SSL-соединения.</span><span class="sxs-lookup"><span data-stu-id="69857-107">Optionally, you can disable requiring SSL for connecting to your database service if your client application does not support SSL connectivity.</span></span> 

## <a name="enforcing-ssl-connections"></a><span data-ttu-id="69857-108">Применение SSL-соединений</span><span class="sxs-lookup"><span data-stu-id="69857-108">Enforcing SSL connections</span></span>
<span data-ttu-id="69857-109">Для всех серверов базы данных Azure для PostgreSQL, подготовленных с помощью портала Azure и интерфейса командной строки, применение SSL-соединений включается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="69857-109">For all Azure Database for PostgreSQL servers provisioned through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="69857-110">Аналогичным образом предопределенные строки подключения в разделе "Строки подключения" в настройках сервера на портале Azure содержат необходимые параметры для распространенных языков, что позволяет подключиться к серверу базы данных с помощью SSL.</span><span class="sxs-lookup"><span data-stu-id="69857-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="69857-111">Значение параметра SSL зависит от соединителя. Например, может использоваться "ssl=true", "sslmode=require", "sslmode=required" или другой вариант.</span><span class="sxs-lookup"><span data-stu-id="69857-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

## <a name="configure-enforcement-of-ssl"></a><span data-ttu-id="69857-112">Настройка применения SSL</span><span class="sxs-lookup"><span data-stu-id="69857-112">Configure Enforcement of SSL</span></span>
<span data-ttu-id="69857-113">При необходимости применение SSL-соединений можно отключить.</span><span class="sxs-lookup"><span data-stu-id="69857-113">You can optionally disable enforcing SSL connectivity.</span></span> <span data-ttu-id="69857-114">Для повышения безопасности Microsoft Azure рекомендует всегда включать параметр **Enforce SSL connection** (Применять SSL-соединение).</span><span class="sxs-lookup"><span data-stu-id="69857-114">Microsoft Azure recommends to always enable **Enforce SSL connection** setting for enhanced security.</span></span>

### <a name="using-the-azure-portal"></a><span data-ttu-id="69857-115">Использование портала Azure</span><span class="sxs-lookup"><span data-stu-id="69857-115">Using the Azure portal</span></span>
<span data-ttu-id="69857-116">Войдите в сервер базы данных Azure для PostgreSQL и щелкните **Безопасность подключения**.</span><span class="sxs-lookup"><span data-stu-id="69857-116">Visit your Azure Database for PostgreSQL server and click **Connection security**.</span></span> <span data-ttu-id="69857-117">Воспользуйтесь переключателем для включения или отключения параметра **Enforce SSL connection** (Применять SSL-соединение).</span><span class="sxs-lookup"><span data-stu-id="69857-117">Use the toggle button to enable or disable the **Enforce SSL connection** setting.</span></span> <span data-ttu-id="69857-118">Нажмите кнопку **Сохранить**.</span><span class="sxs-lookup"><span data-stu-id="69857-118">Then click **Save**.</span></span> 

![Безопасность подключения: отключить применение SSL](./media/concepts-ssl-connection-security/1-disable-ssl.png)

<span data-ttu-id="69857-120">Чтобы проверить правильность настройки, на странице **Обзор** просмотрите индикатор **SSL enforce status** (Состояние применения SSL).</span><span class="sxs-lookup"><span data-stu-id="69857-120">You can confirm the setting by viewing the **Overview** page to see the **SSL enforce status** indicator.</span></span>

### <a name="using-azure-cli"></a><span data-ttu-id="69857-121">Использование Azure CLI</span><span class="sxs-lookup"><span data-stu-id="69857-121">Using Azure CLI</span></span>
<span data-ttu-id="69857-122">Вы также можете включить или отключить параметр **ssl-enforcement** с помощью Azure CLI, используя значения `Enabled` и `Disabled` соответственно.</span><span class="sxs-lookup"><span data-stu-id="69857-122">You can enable or disable the **ssl-enforcement** parameter using `Enabled` or `Disabled` values respectively in Azure CLI.</span></span>

```azurecli
az postgres server update --resource-group myresourcegroup --name mypgserver-20170401 --ssl-enforcement Enabled
```

## <a name="ensure-your-application-or-framework-supports-ssl-connections"></a><span data-ttu-id="69857-123">Проверка поддержки SSL-соединений в приложении или платформе</span><span class="sxs-lookup"><span data-stu-id="69857-123">Ensure your application or framework supports SSL connections</span></span>
<span data-ttu-id="69857-124">Многие распространенные платформы приложений, использующие PostgreSQL для служб базы данных, такие как Drupal и Django, по умолчанию не включают SSL при установке.</span><span class="sxs-lookup"><span data-stu-id="69857-124">Many common application frameworks that use PostgreSQL for database services, such as Drupal and Django, do not enable SSL by default during installation.</span></span> <span data-ttu-id="69857-125">Включить применение SSL-соединений необходимо после установки с помощью команд интерфейса командной строки, соответствующих конкретному приложению.</span><span class="sxs-lookup"><span data-stu-id="69857-125">Enabling SSL connectivity must be done after installation or through CLI commands specific to the application.</span></span> <span data-ttu-id="69857-126">Если на сервере PostgreSQL применяются SSL-соединения, а связанное приложение не настроено должным образом, то при подключении приложения к серверу базы данных может произойти сбой.</span><span class="sxs-lookup"><span data-stu-id="69857-126">If your PostgreSQL server is enforcing SSL connections and the associated application is not configured properly, the application may fail to connect to your database server.</span></span> <span data-ttu-id="69857-127">Сведения о включении SSL-соединений можно найти в документации приложения.</span><span class="sxs-lookup"><span data-stu-id="69857-127">Consult your application's documentation to learn how to enable SSL connections.</span></span>


## <a name="applications-that-require-certificate-verification-for-ssl-connectivity"></a><span data-ttu-id="69857-128">Приложения, требующие проверки сертификата для SSL-соединений</span><span class="sxs-lookup"><span data-stu-id="69857-128">Applications that require certificate verification for SSL connectivity</span></span>
<span data-ttu-id="69857-129">В некоторых случаях для безопасного подключения приложениям требуется локальный файл сертификата, созданный из файла сертификата (CER-файла) доверенного центра сертификации.</span><span class="sxs-lookup"><span data-stu-id="69857-129">In some cases, applications require a local certificate file generated from a trusted Certificate Authority (CA) certificate file (.cer) to connect securely.</span></span> <span data-ttu-id="69857-130">Ниже описывается, как получить этот CER-файл, декодировать сертификат и привязать его к приложению.</span><span class="sxs-lookup"><span data-stu-id="69857-130">See the following steps to obtain the .cer file, decode the certificate and bind it to your application.</span></span>

### <a name="download-the-certificate-file-from-the-certificate-authority-ca"></a><span data-ttu-id="69857-131">Скачивание файла сертификата из центра сертификации</span><span class="sxs-lookup"><span data-stu-id="69857-131">Download the certificate file from the Certificate Authority (CA)</span></span> 
<span data-ttu-id="69857-132">Сертификат, необходимый для подключения к серверу базы данных Azure для PostgreSQL по протоколу SSL, находится [здесь](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span><span class="sxs-lookup"><span data-stu-id="69857-132">The certificate needed to communicate over SSL with your Azure Database for PostgreSQL server is located [here](https://www.digicert.com/CACerts/BaltimoreCyberTrustRoot.crt).</span></span> <span data-ttu-id="69857-133">Скачайте файл сертификата и сохраните его локально.</span><span class="sxs-lookup"><span data-stu-id="69857-133">Download the certificate file locally.</span></span>

### <a name="download-and-install-openssl-on-your-machine"></a><span data-ttu-id="69857-134">Скачивание и установка OpenSSL на компьютер</span><span class="sxs-lookup"><span data-stu-id="69857-134">Download and install OpenSSL on your machine</span></span> 
<span data-ttu-id="69857-135">Чтобы декодировать файл сертификата, необходимый для безопасного подключения приложения к серверу базы данных, установите на своем локальном компьютере OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="69857-135">To decode the certificate file needed for your application to connect securely to your database server, you need to install OpenSSL on your local computer.</span></span>

#### <a name="for-linux-os-x-or-unix"></a><span data-ttu-id="69857-136">Для Linux, OS X или Unix</span><span class="sxs-lookup"><span data-stu-id="69857-136">For Linux, OS X, or Unix</span></span>
<span data-ttu-id="69857-137">Библиотеки OpenSSL предоставляются в виде исходного кода непосредственно от [OpenSSL Software Foundation](http://www.openssl.org).</span><span class="sxs-lookup"><span data-stu-id="69857-137">The OpenSSL libraries are provided in source code directly from the [OpenSSL Software Foundation](http://www.openssl.org).</span></span> <span data-ttu-id="69857-138">Приведенные ниже инструкции помогут вам установить OpenSSL на компьютер под управлением Linux.</span><span class="sxs-lookup"><span data-stu-id="69857-138">The following instructions guide you through the steps necessary to install OpenSSL on your Linux PC.</span></span> <span data-ttu-id="69857-139">В этой статье используются команды, которые гарантированно поддерживают работу с Ubuntu 12.04 и более поздних версий.</span><span class="sxs-lookup"><span data-stu-id="69857-139">This article uses commands known to work on Ubuntu 12.04 and higher.</span></span>

<span data-ttu-id="69857-140">Откройте сеанс терминала и установите OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="69857-140">Open a terminal session and install OpenSSL</span></span>
```bash
wget http://www.openssl.org/source/openssl-1.1.0e.tar.gz
``` 
<span data-ttu-id="69857-141">Извлеките файлы из скачанного пакета.</span><span class="sxs-lookup"><span data-stu-id="69857-141">Extract the files from the download package</span></span>
```bash
tar -xvzf openssl-1.1.0e.tar.gz
```
<span data-ttu-id="69857-142">Укажите каталог, в который были извлечены файлы.</span><span class="sxs-lookup"><span data-stu-id="69857-142">Enter the directory where the files were extracted.</span></span> <span data-ttu-id="69857-143">По умолчанию это должен быть каталог, показанный ниже.</span><span class="sxs-lookup"><span data-stu-id="69857-143">By default, it should be as follows.</span></span>

```bash
cd openssl-1.1.0e
```
<span data-ttu-id="69857-144">Настройте OpenSSL, выполнив приведенную ниже команду.</span><span class="sxs-lookup"><span data-stu-id="69857-144">Configure OpenSSL by executing the following command.</span></span> <span data-ttu-id="69857-145">Если вы хотите, чтобы файлы хранились в папке, отличной от /usr/local/openssl, то укажите соответствующее значение.</span><span class="sxs-lookup"><span data-stu-id="69857-145">If you want the files in a folder different than /usr/local/openssl, make sure to change the following as appropriate.</span></span>

```bash
./config --prefix=/usr/local/openssl --openssldir=/usr/local/openssl
```
<span data-ttu-id="69857-146">Теперь, когда библиотека OpenSSL настроена должным образом, необходимо скомпилировать ее для преобразования сертификата.</span><span class="sxs-lookup"><span data-stu-id="69857-146">Now that OpenSSL is configured properly, you need to compile it to convert your certificate.</span></span> <span data-ttu-id="69857-147">Для выполнения компиляции выполните следующую команду.</span><span class="sxs-lookup"><span data-stu-id="69857-147">To compile, run the following command:</span></span>

```bash
make
```
<span data-ttu-id="69857-148">После завершения компиляции можно установить OpenSSL как исполняемый файл, выполнив следующую команду.</span><span class="sxs-lookup"><span data-stu-id="69857-148">Once compiling is complete, you're ready to install OpenSSL as an executable by running the following command:</span></span>
```bash
make install
```
<span data-ttu-id="69857-149">Чтобы убедиться, что компонент OpenSSL успешно установлен в системе, выполните приведенную ниже команду. Убедитесь, чтобы отображаются такие же выходные данные.</span><span class="sxs-lookup"><span data-stu-id="69857-149">To confirm that you've successfully installed OpenSSL on your system, run the following command and check to make sure you get the same output.</span></span>

```bash
/usr/local/openssl/bin/openssl version
```
<span data-ttu-id="69857-150">В случае успешного выполнения отобразится следующее сообщение:</span><span class="sxs-lookup"><span data-stu-id="69857-150">If successful you should see the following message.</span></span>
```bash
OpenSSL 1.1.0e 7 Apr 2014
```

#### <a name="for-windows"></a><span data-ttu-id="69857-151">Для Windows</span><span class="sxs-lookup"><span data-stu-id="69857-151">For Windows</span></span>
<span data-ttu-id="69857-152">Установить OpenSSL на компьютере Windows можно следующими способами:</span><span class="sxs-lookup"><span data-stu-id="69857-152">Installing OpenSSL on a Windows PC can be done in the following ways:</span></span>
1. <span data-ttu-id="69857-153">**(Рекомендуется.)** При использовании встроенных функций Bash для Windows в Windows 10 и более поздних версиях OpenSSL устанавливается по умолчанию.</span><span class="sxs-lookup"><span data-stu-id="69857-153">**(Recommended)** Using the built-in Bash for Windows functionality in Window 10 and above, OpenSSL is installed by default.</span></span> <span data-ttu-id="69857-154">Инструкции по включению функций Bash для Windows в Windows 10 можно найти [здесь](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span><span class="sxs-lookup"><span data-stu-id="69857-154">Instructions on how to enable Bash for Windows functionality in Windows 10 can be found [here](https://msdn.microsoft.com/en-us/commandline/wsl/install_guide).</span></span>
2. <span data-ttu-id="69857-155">Можно скачать приложение для Win32 или Win64, предоставляемое сообществом.</span><span class="sxs-lookup"><span data-stu-id="69857-155">Through downloading a Win32/64 application provided by the community.</span></span> <span data-ttu-id="69857-156">Хотя OpenSSL Software Foundation не предоставляет и не одобряет какие-либо определенные установщики Windows, [здесь](https://wiki.openssl.org/index.php/Binaries) приводится список доступных установщиков.</span><span class="sxs-lookup"><span data-stu-id="69857-156">While the OpenSSL Software Foundation does not provide or endorse any specific Windows installers, they provide a list of available installers [here](https://wiki.openssl.org/index.php/Binaries)</span></span>

### <a name="decode-your-certificate-file"></a><span data-ttu-id="69857-157">Декодируйте файл сертификата</span><span class="sxs-lookup"><span data-stu-id="69857-157">Decode your certificate file</span></span>
<span data-ttu-id="69857-158">Файл из корневого центра сертификации скачивается в зашифрованном виде.</span><span class="sxs-lookup"><span data-stu-id="69857-158">The downloaded Root CA file is in encrypted format.</span></span> <span data-ttu-id="69857-159">Чтобы декодировать файл сертификата, воспользуйтесь OpenSSL.</span><span class="sxs-lookup"><span data-stu-id="69857-159">Use OpenSSL to decode the certificate file.</span></span> <span data-ttu-id="69857-160">Для этого выполните следующую команду OpenSSL:</span><span class="sxs-lookup"><span data-stu-id="69857-160">To do so, run this OpenSSL command:</span></span>

```dos
OpenSSL>x509 -inform DER -in BaltimoreCyberTrustRoot.cer -text -out root.crt
```

### <a name="connecting-to-azure-database-for-postgresql-with-ssl-certificate-authentication"></a><span data-ttu-id="69857-161">Подключение к базе данных Azure для PostgreSQL с использованием проверки подлинности на основе SSL-сертификата</span><span class="sxs-lookup"><span data-stu-id="69857-161">Connecting to Azure Database for PostgreSQL with SSL certificate authentication</span></span>
<span data-ttu-id="69857-162">Теперь, когда вы успешно декодировали сертификат, можно безопасно подключиться к серверу базы данных по протоколу SSL.</span><span class="sxs-lookup"><span data-stu-id="69857-162">Now that you have successfully decoded your certificate, you can now connect to your database server securely over SSL.</span></span> <span data-ttu-id="69857-163">Чтобы выполнить проверку сертификата сервера, необходимо поместить сертификат в файл ~/.postgresql/root.crt в основном каталоге пользователя.</span><span class="sxs-lookup"><span data-stu-id="69857-163">To allow server certificate verification, the certificate must be placed in the file ~/.postgresql/root.crt in the user's home directory.</span></span> <span data-ttu-id="69857-164">(В Microsoft Windows этот файл имеет имя %APPDATA%\postgresql\root.crt).</span><span class="sxs-lookup"><span data-stu-id="69857-164">(On Microsoft Windows the file is named %APPDATA%\postgresql\root.crt.).</span></span> <span data-ttu-id="69857-165">Ниже приводятся инструкции по подключению к базе данных Azure для PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="69857-165">The following provides instructions for connecting to Azure Database for PostgreSQL.</span></span>

> [!NOTE]
> <span data-ttu-id="69857-166">Сейчас при подключении к службе с использованием sslmode=verify-full может возникать известная проблема, из-за которой происходит сбой подключения со следующей ошибкой: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"_ (Сертификат сервера для "Регион.control.database.windows.net" (и 7 других имен) не соответствует имени узла "Имя_узла.postgres.database.azure.com").</span><span class="sxs-lookup"><span data-stu-id="69857-166">Currently, there is a known issue if you use "sslmode=verify-full" in your connection to the service, the connection will fail with the following error: _server certificate for "&lt;region&gt;.control.database.windows.net" (and 7 other names) does not match host name "&lt;servername&gt;.postgres.database.azure.com"._</span></span>
> <span data-ttu-id="69857-167">Если параметр sslmode=verify-full требуется, используйте соглашение об именовании серверов (**&lt;Имя_сервера&gt;.database.windows.net**) в качестве имени узла строки подключения.</span><span class="sxs-lookup"><span data-stu-id="69857-167">If "sslmode=verify-full" is required, please use the server naming convention **&lt;servername&gt;.database.windows.net** as your connection string host name.</span></span> <span data-ttu-id="69857-168">Мы планируем устранить это ограничение в будущем.</span><span class="sxs-lookup"><span data-stu-id="69857-168">We plan to remove this limitation in the future.</span></span> <span data-ttu-id="69857-169">Для подключений, использующих другие [режимы SSL](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS), по прежнему используйте предпочитаемое соглашение об именовании узла (**&lt;Имя_узла&gt;.postgres.database.azure.com**).</span><span class="sxs-lookup"><span data-stu-id="69857-169">Connections using other [SSL modes](https://www.postgresql.org/docs/9.6/static/libpq-ssl.html#LIBPQ-SSL-SSLMODE-STATEMENTS) should continue to use the preferred host naming convention **&lt;servername&gt;.postgres.database.azure.com**.</span></span>

#### <a name="using-psql-command-line-utility"></a><span data-ttu-id="69857-170">Использование служебной программы командной строки psql</span><span class="sxs-lookup"><span data-stu-id="69857-170">Using psql command-line utility</span></span>
<span data-ttu-id="69857-171">В следующем примере показано, как подключиться к серверу PostgreSQL с помощью служебной программы командной строки psql,</span><span class="sxs-lookup"><span data-stu-id="69857-171">The following example shows you how to successfully connect to your PostgreSQL server using the psql command-line utility.</span></span> <span data-ttu-id="69857-172">используя созданный файл `root.crt` и параметр `sslmode=verify-ca` или `sslmode=verify-full`.</span><span class="sxs-lookup"><span data-stu-id="69857-172">Use the `root.crt` file created and the `sslmode=verify-ca` or `sslmode=verify-full` option.</span></span>

<span data-ttu-id="69857-173">С помощью интерфейса командной строки PostgreSQL выполните следующую команду:</span><span class="sxs-lookup"><span data-stu-id="69857-173">Using the PostgreSQL command-line interface, execute the following command:</span></span>
```bash
psql "sslmode=verify-ca sslrootcert=root.crt host=mypgserver-20170401.postgres.database.azure.com dbname=postgres user=mylogin@mypgserver-20170401"
```
<span data-ttu-id="69857-174">В случае успешного выполнения отобразится следующий результат:</span><span class="sxs-lookup"><span data-stu-id="69857-174">If successful, you receive the following output:</span></span>
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

#### <a name="using-pgadmin-gui-tool"></a><span data-ttu-id="69857-175">Использование инструмента графического пользовательского интерфейса pgAdmin</span><span class="sxs-lookup"><span data-stu-id="69857-175">Using pgAdmin GUI tool</span></span>
<span data-ttu-id="69857-176">Чтобы pgAdmin 4 мог безопасно подключаться по протоколу SSL, необходимо настроить параметр `SSL mode = Verify-CA` или `SSL mode = Verify-Full`, как показано ниже.</span><span class="sxs-lookup"><span data-stu-id="69857-176">Configuring pgAdmin 4 to connect securely over SSL requires you to set the `SSL mode = Verify-CA` or `SSL mode = Verify-Full` as follows:</span></span>

![Снимок экрана pgAdmin: настройка параметра "SSL mode" (Режим SSL) на вкладке "Connection" (Подключение)](./media/concepts-ssl-connection-security/2-pgadmin-ssl.png)

## <a name="next-steps"></a><span data-ttu-id="69857-178">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="69857-178">Next steps</span></span>
<span data-ttu-id="69857-179">Сведения о вариантах подключения приложений см. в статье [Библиотеки подключений для базы данных Azure для PostgreSQL](concepts-connection-libraries.md).</span><span class="sxs-lookup"><span data-stu-id="69857-179">Review various application connectivity options following [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
