---
title: "aaaAzure образец приложения для использования в сети периметра | Документы Microsoft"
description: "Развертывание этого простого веб-приложения после создания DMZ tootest сценарии потока трафика"
services: virtual-network
documentationcenter: na
author: tracsman
manager: rossort
editor: 
ms.assetid: 60340ab7-b82b-40e0-bd87-83e41fe4519c
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 01/03/2017
ms.author: jonor
ms.openlocfilehash: e0d9cf14590f75b50c64b677efce2c5425b83ec6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="sample-application-for-use-with-dmzs"></a><span data-ttu-id="f4c74-103">Пример приложения для использования с сетями периметра</span><span class="sxs-lookup"><span data-stu-id="f4c74-103">Sample application for use with DMZs</span></span>
<span data-ttu-id="f4c74-104">[Возвращает toohello страница лучшие рекомендации безопасности границ][HOME]</span><span class="sxs-lookup"><span data-stu-id="f4c74-104">[Return toohello Security Boundary Best Practices Page][HOME]</span></span>

<span data-ttu-id="f4c74-105">Эти скрипты PowerShell можно запускать локально на tooinstall серверы IIS01 и AppVM01 hello и настроить HTML-страницу с сервера переднего плана IIS01 hello с содержимым из hello AppVM01 серверных простого веб-приложения.</span><span class="sxs-lookup"><span data-stu-id="f4c74-105">These PowerShell scripts can be run locally on hello IIS01 and AppVM01 servers tooinstall and set up a simple web application that displays an html page from hello front-end IIS01 server with content from hello back-end AppVM01 server.</span></span>

<span data-ttu-id="f4c74-106">Это приложение предоставляет простой тестовой среде для многих примерах DMZ hello и как hello изменения на конечные точки, Nsg, UDR и правила брандмауэра может повлиять на потоки трафика.</span><span class="sxs-lookup"><span data-stu-id="f4c74-106">This application provides a simple testing environment for many of hello DMZ Examples and how changes on hello Endpoints, NSGs, UDR, and Firewall rules can affect traffic flows.</span></span>

## <a name="firewall-rule-tooallow-icmp"></a><span data-ttu-id="f4c74-107">Tooallow правил брандмауэра ICMP</span><span class="sxs-lookup"><span data-stu-id="f4c74-107">Firewall rule tooallow ICMP</span></span>
<span data-ttu-id="f4c74-108">Это простое утверждение PowerShell может выполняться на любой трафик ICMP (Ping) tooallow виртуальной Машины Windows.</span><span class="sxs-lookup"><span data-stu-id="f4c74-108">This simple PowerShell statement can be run on any Windows VM tooallow ICMP (Ping) traffic.</span></span> <span data-ttu-id="f4c74-109">Благодаря данному обновлению брандмауэра для упрощения тестирования и устранения неполадок, позволяя hello ping протокола toopass через брандмауэр windows hello (для большинства дистрибутивы Linux, ICMP включено по умолчанию).</span><span class="sxs-lookup"><span data-stu-id="f4c74-109">This firewall update allows for easier testing and troubleshooting by allowing hello ping protocol toopass through hello windows firewall (for most Linux distros ICMP is on by default).</span></span>

```PowerShell
# Turn On ICMPv4
New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" `
    -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow
```

<span data-ttu-id="f4c74-110">Если вы используете следующие сценарии hello, это Добавление правила брандмауэра является первой инструкцией hello.</span><span class="sxs-lookup"><span data-stu-id="f4c74-110">If you use hello following scripts, this firewall rule addition is hello first statement.</span></span>

## <a name="iis01---web-application-installation-script"></a><span data-ttu-id="f4c74-111">Сервер IIS01: сценарий установки веб-приложения</span><span class="sxs-lookup"><span data-stu-id="f4c74-111">IIS01 - Web application installation script</span></span>
<span data-ttu-id="f4c74-112">Вот что делает этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="f4c74-112">This script will:</span></span>

1. <span data-ttu-id="f4c74-113">Откройте IMCPv4 (Ping) в брандмауэре windows hello локального сервера для упрощения тестирования</span><span class="sxs-lookup"><span data-stu-id="f4c74-113">Open IMCPv4 (Ping) on hello local server windows firewall for easier testing</span></span>
2. <span data-ttu-id="f4c74-114">Установка служб IIS и hello .net Framework версии 4.5</span><span class="sxs-lookup"><span data-stu-id="f4c74-114">Install IIS and hello .Net Framework v4.5</span></span>
3. <span data-ttu-id="f4c74-115">Создает веб-страницу ASP.NET и файл Web.config.</span><span class="sxs-lookup"><span data-stu-id="f4c74-115">Create an ASP.NET web page and a Web.config file</span></span>
4. <span data-ttu-id="f4c74-116">Изменить hello по умолчанию пула приложений toomake файл доступ проще</span><span class="sxs-lookup"><span data-stu-id="f4c74-116">Change hello Default application pool toomake file access easier</span></span>
5. <span data-ttu-id="f4c74-117">Задание учетной записи администратора tooyour анонимного пользователя hello и пароля</span><span class="sxs-lookup"><span data-stu-id="f4c74-117">Set hello Anonymous user tooyour admin account and password</span></span>

<span data-ttu-id="f4c74-118">Этот сценарий PowerShell нужно запускать локально, удаленно подключившись к серверу IIS01 через протокол RDP.</span><span class="sxs-lookup"><span data-stu-id="f4c74-118">This PowerShell script should be run locally while RDP’d into IIS01.</span></span>

```PowerShell
# IIS Server Post Build Config Script
# Get Admin Account and Password
    Write-Host "Please enter hello admin account information used toocreate this VM:" -ForegroundColor Cyan
    $theAdmin = Read-Host -Prompt "hello Admin Account Name (no domain or machine name)"
    $thePassword = Read-Host -Prompt "hello Admin Password"

# Turn On ICMPv4
    Write-Host "Creating ICMP Rule in Windows Firewall" -ForegroundColor Cyan
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Install IIS
    Write-Host "Installing IIS and .Net 4.5, this can take some time, like 15+ minutes..." -ForegroundColor Cyan
    add-windowsfeature Web-Server, Web-WebServer, Web-Common-Http, Web-Default-Doc, Web-Dir-Browsing, Web-Http-Errors, Web-Static-Content, Web-Health, Web-Http-Logging, Web-Performance, Web-Stat-Compression, Web-Security, Web-Filtering, Web-App-Dev, Web-ISAPI-Ext, Web-ISAPI-Filter, Web-Net-Ext, Web-Net-Ext45, Web-Asp-Net45, Web-Mgmt-Tools, Web-Mgmt-Console

# Create Web App Pages
    Write-Host "Creating Web page and Web.Config file" -ForegroundColor Cyan
    $MainPage = '<%@ Page Language="vb" AutoEventWireup="false" %>
    <%@ Import Namespace="System.IO" %>
    <script language="vb" runat="server">
        Protected Sub Page_Load(ByVal sender As Object, ByVal e As System.EventArgs) Handles Me.Load
            Dim FILENAME As String = "\\10.0.2.5\WebShare\Rand.txt"
            Dim objStreamReader As StreamReader
            objStreamReader = File.OpenText(FILENAME)
            Dim contents As String = objStreamReader.ReadToEnd()
            lblOutput.Text = contents
            objStreamReader.Close()
            lblTime.Text = Now()
        End Sub
    </script>

    <!DOCTYPE html>
    <html xmlns="http://www.w3.org/1999/xhtml">
    <head runat="server">
        <title>DMZ Example App</title>
    </head>
    <body style="font-family: Optima,Segoe,Segoe UI,Candara,Calibri,Arial,sans-serif;">
      <form id="frmMain" runat="server">
        <div>
          <h1>Looks like you made it!</h1>
          This is a page from hello inside (a web server on a private network),<br />
          and it is making its way toohello outside! (If you are viewing this from hello internet)<br />
          <br />
          hello following sections show:
          <ul style="margin-top: 0px;">
            <li> Local Server Time - Shows if this page is or isnt cached anywhere</li>
            <li> File Output - Shows that hello web server is reaching AppVM01 on hello backend subnet and successfully returning content</li>
            <li> Image from hello Internet - Doesnt really show anything, but it made me happy toosee this when hello app worked</li>
          </ul>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Local Web Server Time</b>: <asp:Label runat="server" ID="lblTime" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>File Output from AppVM01</b>: <asp:Label runat="server" ID="lblOutput" /></div>
          <div style="border: 2px solid #8AC007; border-radius: 25px; padding: 20px; margin: 10px; width: 650px;">
            <b>Image File Linked from hello Internet</b>:<br />
            <br />
            <img src="http://sd.keepcalm-o-matic.co.uk/i/keep-calm-you-made-it-7.png" alt="You made it!" width="150" length="175"/></div>
        </div>
      </form>
    </body>
    </html>'

    $WebConfig ='<?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <system.web>
        <compilation debug="true" strict="false" explicit="true" targetFramework="4.5" />
        <httpRuntime targetFramework="4.5" />
        <identity impersonate="true" />
        <customErrors mode="Off"/>
      </system.web>
      <system.webServer>
        <defaultDocument>
          <files>
            <add value="Home.aspx" />
          </files>
        </defaultDocument>
      </system.webServer>
    </configuration>'

    $MainPage | Out-File -FilePath "C:\inetpub\wwwroot\Home.aspx" -Encoding ascii
    $WebConfig | Out-File -FilePath "C:\inetpub\wwwroot\Web.config" -Encoding ascii

# Set App Pool tooClasic Pipeline tooremote file access will work easier
    Write-Host "Updaing IIS Settings" -ForegroundColor Cyan
    c:\windows\system32\inetsrv\appcmd.exe set app "Default Web Site/" /applicationPool:".NET v4.5 Classic"
    c:\windows\system32\inetsrv\appcmd.exe set config "Default Web Site/" /section:system.webServer/security/authentication/anonymousAuthentication /userName:$theAdmin /password:$thePassword /commit:apphost

# Make sure hello IIS settings take
    Write-Host "Restarting hello W3SVC" -ForegroundColor Cyan
    Restart-Service -Name W3SVC

    Write-Host
    Write-Host "Web App Creation Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="appvm01---file-server-installation-script"></a><span data-ttu-id="f4c74-119">Сервер AppVM01: сценарий установки файлового сервера</span><span class="sxs-lookup"><span data-stu-id="f4c74-119">AppVM01 - File server installation script</span></span>
<span data-ttu-id="f4c74-120">Этот сценарий настраивает hello серверной стороне для этого простого приложения.</span><span class="sxs-lookup"><span data-stu-id="f4c74-120">This script sets up hello back-end for this simple application.</span></span> <span data-ttu-id="f4c74-121">Вот что делает этот сценарий:</span><span class="sxs-lookup"><span data-stu-id="f4c74-121">This script will:</span></span>

1. <span data-ttu-id="f4c74-122">Откройте IMCPv4 (Ping) на брандмауэре hello для упрощения тестирования</span><span class="sxs-lookup"><span data-stu-id="f4c74-122">Open IMCPv4 (Ping) on hello firewall for easier testing</span></span>
2. <span data-ttu-id="f4c74-123">Создайте каталог для hello веб-сайта</span><span class="sxs-lookup"><span data-stu-id="f4c74-123">Create a directory for hello web site</span></span>
3. <span data-ttu-id="f4c74-124">Создайте текстовый файл toobe удаленно получить доступ к веб-страницы приветствия</span><span class="sxs-lookup"><span data-stu-id="f4c74-124">Create a text file toobe remotely access by hello web page</span></span>
4. <span data-ttu-id="f4c74-125">Задать разрешения для каталогов и файлов tooAnonymous hello tooallow доступа</span><span class="sxs-lookup"><span data-stu-id="f4c74-125">Set permissions on hello directory and file tooAnonymous tooallow access</span></span>
5. <span data-ttu-id="f4c74-126">Отключить усиленной безопасности IE tooallow упрощает просмотр с этого сервера</span><span class="sxs-lookup"><span data-stu-id="f4c74-126">Turn off IE Enhanced Security tooallow easier browsing from this server</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="f4c74-127">**Рекомендация**: никогда не выключайте усиленной безопасности IE на рабочем сервере, а также, как правило, не рекомендуются toosurf hello веб-сайт с рабочего сервера.</span><span class="sxs-lookup"><span data-stu-id="f4c74-127">**Best Practice**: Never turn off IE Enhanced Security on a production server, plus it's generally a bad idea toosurf hello web from a production server.</span></span> <span data-ttu-id="f4c74-128">Мы также не рекомендуем предоставлять анонимный доступ к файловым ресурсам. В нашем случае это сделано для простоты.</span><span class="sxs-lookup"><span data-stu-id="f4c74-128">Also, opening up file shares for anonymous access is a bad idea, but done here for simplicity.</span></span>
> 
> 

<span data-ttu-id="f4c74-129">Этот сценарий PowerShell следует запускать локально, удаленно подключившись к серверу AppVM01 через протокол RDP.</span><span class="sxs-lookup"><span data-stu-id="f4c74-129">This PowerShell script should be run locally while RDP’d into AppVM01.</span></span> <span data-ttu-id="f4c74-130">PowerShell — необходимые toobe Запуск от имени администратора tooensure успешного выполнения.</span><span class="sxs-lookup"><span data-stu-id="f4c74-130">PowerShell is required toobe run as Administrator tooensure successful execution.</span></span>

```PowerShell
# AppVM01 Server Post Build Config Script
# PowerShell must be run as Administrator for Net Share commands toowork

# Turn On ICMPv4
    New-NetFirewallRule -Name Allow_ICMPv4 -DisplayName "Allow ICMPv4" -Protocol ICMPv4 -Enabled True -Profile Any -Action Allow

# Create Directory
    New-Item "C:\WebShare" -ItemType Directory

# Write out Rand.txt
    $FileContent = "Hello, I'm hello contents of a remote file on AppVM01."
    $FileContent | Out-File -FilePath "C:\WebShare\Rand.txt" -Encoding ascii

# Set Permissions on share
    $Acl = Get-Acl "C:\WebShare"
    $AccessRule = New-Object system.security.accesscontrol.filesystemaccessrule("Everyone","ReadAndExecute, Synchronize","ContainerInherit, ObjectInherit","InheritOnly","Allow")
    $Acl.SetAccessRule($AccessRule)
    Set-Acl "C:\WebShare" $Acl

# Create network share
    Net Share WebShare=C:\WebShare "/grant:Everyone,READ"

# Turn Off IE Enhanced Security Configuration for Admins
    Set-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Active Setup\Installed Components\{A509B1A7-37EF-4b3f-8CFC-4F3A74704073}" -Name "IsInstalled" -Value 0

    Write-Host
    Write-Host "File Server Set up Successfull!" -ForegroundColor Green
    Write-Host
```

## <a name="dns01---dns-server-installation-script"></a><span data-ttu-id="f4c74-131">DNS01: сценарий установки DNS-сервера</span><span class="sxs-lookup"><span data-stu-id="f4c74-131">DNS01 - DNS server installation script</span></span>
<span data-ttu-id="f4c74-132">Отсутствует скрипт включен в tooset приложения этот образец hello DNS сервера.</span><span class="sxs-lookup"><span data-stu-id="f4c74-132">There is no script included in this sample application tooset up hello DNS server.</span></span> <span data-ttu-id="f4c74-133">Если тестирование hello правила брандмауэра, NSG или UDR tooinclude трафик DNS, сервер hello DNS01 должно toobe ручной настройки.</span><span class="sxs-lookup"><span data-stu-id="f4c74-133">If testing of hello firewall rules, NSG, or UDR needs tooinclude DNS traffic, hello DNS01 server needs toobe set up manually.</span></span> <span data-ttu-id="f4c74-134">XML-файл конфигурации сети Hello и шаблона диспетчера ресурсов для обоих примерах включает DNS01 как hello основной DNS-сервер и hello поддерживаемого уровня 3, как резервное копирование сервера DNS hello общедоступный сервер DNS.</span><span class="sxs-lookup"><span data-stu-id="f4c74-134">hello Network Configuration xml file and Resource Manager Template for both examples includes DNS01 as hello primary DNS server and hello public DNS server hosted by Level 3 as hello backup DNS server.</span></span> <span data-ttu-id="f4c74-135">Hello DNS-3 уровня сервера следует быть hello DNS сервер, используемый для нелокальных трафика и с DNS01 не программой установки, нет локальной сети, будет возникать DNS.</span><span class="sxs-lookup"><span data-stu-id="f4c74-135">hello Level 3 DNS server would be hello actual DNS server used for non-local traffic, and with DNS01 not setup, no local network DNS would occur.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f4c74-136">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="f4c74-136">Next steps</span></span>
* <span data-ttu-id="f4c74-137">Запустите сценарий IIS01 hello на сервере IIS</span><span class="sxs-lookup"><span data-stu-id="f4c74-137">Run hello IIS01 script on an IIS server</span></span>
* <span data-ttu-id="f4c74-138">Запуск сценария файлового сервера на сервере AppVM01</span><span class="sxs-lookup"><span data-stu-id="f4c74-138">Run File Server script on AppVM01</span></span>
* <span data-ttu-id="f4c74-139">Обзор toohello общедоступный IP-адрес на IIS01 toovalidate сборки</span><span class="sxs-lookup"><span data-stu-id="f4c74-139">Browse toohello Public IP on IIS01 toovalidate your build</span></span>

<!--Link References-->
[HOME]: ../best-practices-network-security.md
