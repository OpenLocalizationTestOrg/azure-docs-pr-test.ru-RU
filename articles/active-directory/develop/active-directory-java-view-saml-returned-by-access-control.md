---
title: "aaaView SAML возвращаются по hello Access Control Service (Java)"
description: "Узнайте, как tooview SAML, возвращенный hello службы контроля доступа в Java-приложений, размещенных в Azure."
services: active-directory
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
ms.assetid: 6cd216f9-eb43-46b4-b30d-f194d0ae2d48
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.custom: aaddev
ms.openlocfilehash: b6733bc98b505cfa89a4ce456f368ee15da11427
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a><span data-ttu-id="c31b4-103">Как tooview SAML возвращают hello Azure Access Control Service</span><span class="sxs-lookup"><span data-stu-id="c31b4-103">How tooview SAML returned by hello Azure Access Control Service</span></span>
<span data-ttu-id="c31b4-104">В этом руководстве будет показано, как tooview hello базовый Security Assertion Markup Language (SAML) возвращают tooyour приложения hello службы управления доступом Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="c31b4-104">This guide will show you how tooview hello underlying Security Assertion Markup Language (SAML) returned tooyour application by hello Azure Access Control Service (ACS).</span></span> <span data-ttu-id="c31b4-105">руководство по Hello лежит hello [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) раздела, предоставив код, отображающий сведения hello SAML.</span><span class="sxs-lookup"><span data-stu-id="c31b4-105">hello guide builds on hello [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays hello SAML information.</span></span> <span data-ttu-id="c31b4-106">приложение Hello завершения будет выглядеть примерно следующие toohello.</span><span class="sxs-lookup"><span data-stu-id="c31b4-106">hello completed application will look similar toohello following.</span></span>

![Пример выходных данных SAML][saml_output]

<span data-ttu-id="c31b4-108">Дополнительные сведения о ACS см. в разделе hello [дальнейшие действия](#next_steps) раздела.</span><span class="sxs-lookup"><span data-stu-id="c31b4-108">For more information on ACS, see hello [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="c31b4-109">Hello фильтр управления служб Azure Access является CTP-версии.</span><span class="sxs-lookup"><span data-stu-id="c31b4-109">hello Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="c31b4-110">Эта предварительная версия программного обеспечения не обеспечивается официальной поддержкой корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c31b4-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c31b4-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c31b4-111">Prerequisites</span></span>
<span data-ttu-id="c31b4-112">Здравствуйте, toocomplete hello задачи в данном руководстве, полный пример в [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) и использовать его в качестве начальной точки для этого учебника hello.</span><span class="sxs-lookup"><span data-stu-id="c31b4-112">toocomplete hello tasks in this guide, complete hello sample at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as hello starting point for this tutorial.</span></span>

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a><span data-ttu-id="c31b4-113">Добавить hello JspWriter библиотеки tooyour путь и развертывания сборки</span><span class="sxs-lookup"><span data-stu-id="c31b4-113">Add hello JspWriter library tooyour build path and deployment assembly</span></span>
<span data-ttu-id="c31b4-114">Добавить hello библиотеку, содержащую hello **javax.servlet.jsp.JspWriter** tooyour класс сборки пути и развертывания.</span><span class="sxs-lookup"><span data-stu-id="c31b4-114">Add hello library that contains hello **javax.servlet.jsp.JspWriter** class tooyour build path and deployment assembly.</span></span> <span data-ttu-id="c31b4-115">При использовании Tomcat hello библиотека — **jsp api.jar**, который находится в hello Apache **lib** папки.</span><span class="sxs-lookup"><span data-stu-id="c31b4-115">If you are using Tomcat, hello library is **jsp-api.jar**, which is located in hello Apache **lib** folder.</span></span>

1. <span data-ttu-id="c31b4-116">В обозревателе проектов Eclipse, щелкните правой кнопкой мыши **MyACSHelloWorld**, нажмите кнопку **путь построения**, нажмите кнопку **настроить путь построения**, нажмите кнопку hello **библиотеки** , а затем щелкните **добавить внешний JAR-файлов**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click hello **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="c31b4-117">В hello **JAR выбора** диалоговое окно, перейдите toohello необходимые JAR-ФАЙЛ, выберите его и нажмите кнопку **откройте**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-117">In hello **JAR Selection** dialog, navigate toohello necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="c31b4-118">С hello **свойства MyACSHelloWorld** диалоговом окне все еще открыто, щелкните **сборку развертывания**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-118">With hello **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="c31b4-119">В hello **веб-развертывания сборки** диалоговое окно, нажмите кнопку **добавить**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-119">In hello **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="c31b4-120">В hello **новый директива Assembly** диалоговое окно, нажмите кнопку **записи путь построения Java** и нажмите кнопку **Далее**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-120">In hello **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="c31b4-121">Выберите соответствующую библиотеку hello и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c31b4-121">Select hello appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="c31b4-122">Нажмите кнопку **ОК** tooclose hello **свойства MyACSHelloWorld** диалогового окна.</span><span class="sxs-lookup"><span data-stu-id="c31b4-122">Click **OK** tooclose hello **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-hello-jsp-file-toodisplay-saml"></a><span data-ttu-id="c31b4-123">Изменение hello JSP файл toodisplay SAML</span><span class="sxs-lookup"><span data-stu-id="c31b4-123">Modify hello JSP file toodisplay SAML</span></span>
<span data-ttu-id="c31b4-124">Изменить **index.jsp** toouse hello, следующий код.</span><span class="sxs-lookup"><span data-stu-id="c31b4-124">Modify **index.jsp** toouse hello following code.</span></span>

    <%@ page language="java" contentType="text/html; charset=UTF-8"
        pageEncoding="UTF-8"%>
        <%@ page import="javax.xml.parsers.*"
                 import="javax.xml.transform.*"
                 import="org.w3c.dom.*"
                 import="java.io.*"
                 import="javax.xml.transform.stream.*"
                 import="javax.xml.transform.dom.*"
                 import="javax.xml.xpath.*"
                 import="javax.servlet.jsp.JspWriter" %>
    <!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
    <html>
    <head>
    <meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
    <title>Sample ACS Filter</title>
    </head>
    <body>
        <h3>SAML information from sample ACS program</h3>
        <%!
        void displaySAMLInfo(Node node, String parent, JspWriter out)
        {

            try
            {
                String nodeName;
                int nChild, i;

                nodeName = node.getNodeName();
                out.println("<br>");
                out.println("<u>Examining <b>" + parent + nodeName + "</b></u><br>");

                   // Attributes.
                   NamedNodeMap attribsMap = node.getAttributes();
                   if (null != attribsMap)
                   {
                         for (i=0; i < attribsMap.getLength(); i++)
                         {
                                Node attrib = attribsMap.item(i);
                                out.println("Attribute: <b>" + attrib.getNodeName() + "</b>: " + attrib.getNodeValue()  + "<br>");
                         }
                   }

                   // Child nodes.
                   NodeList list = node.getChildNodes();
                   if (null != list)
                    {
                          nChild = list.getLength();
                          if (nChild > 0)
                          {                    

                                 // If it is a text node, just print hello text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out hello child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate hello names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish hello sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process hello child nodes.
                                     for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);
                                        displaySAMLInfo(temp, parent + nodeName + "\\", out);
                                     }
                               }
                          }
                      }
                  }
                catch (Exception e)
                {
                    System.out.println("Exception encountered.");
                    e.printStackTrace();            
                }
            }
        %>

        <%
        try
        {
            String data  = (String) request.getAttribute("ACSSAML");

            DocumentBuilder docBuilder;
            Document doc = null;
            DocumentBuilderFactory docBuilderFactory = DocumentBuilderFactory.newInstance();
            docBuilderFactory.setIgnoringElementContentWhitespace(true);
            docBuilder = docBuilderFactory.newDocumentBuilder();
            byte[] xmlDATA = data.getBytes();

            ByteArrayInputStream in = new ByteArrayInputStream(xmlDATA);
            doc = docBuilder.parse(in);
            doc.getDocumentElement().normalize();

            // Iterate hello child nodes of hello doc.
            NodeList list = doc.getChildNodes();

            for (int i=0; i < list.getLength(); i++)
            {
                displaySAMLInfo(list.item(i), "", out);
            }
        }
        catch (Exception e)
        {
            out.println("Exception encountered.");
            e.printStackTrace();
        }

        %>
    </body>
    </html>

## <a name="run-hello-application"></a><span data-ttu-id="c31b4-125">Запустите приложение hello</span><span class="sxs-lookup"><span data-stu-id="c31b4-125">Run hello application</span></span>
1. <span data-ttu-id="c31b4-126">Запуск приложения в эмуляторе hello компьютера или развернуть tooAzure, с помощью hello действия, описанные на [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="c31b4-126">Run your application in hello computer emulator or deploy tooAzure, using hello steps documented at [How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="c31b4-127">Запустите браузер и откройте в нем свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="c31b4-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="c31b4-128">После входа в систему tooyour приложения вы увидите сведения SAML, включая hello утверждение безопасности, предоставляемые поставщиком удостоверений hello.</span><span class="sxs-lookup"><span data-stu-id="c31b4-128">After you log on tooyour application, you'll see SAML information, including hello security assertion provided by hello identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c31b4-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c31b4-129">Next steps</span></span>
<span data-ttu-id="c31b4-130">toofurther исследовать функциональные возможности службы ACS и tooexperiment с более сложных сценариях см. в разделе [Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="c31b4-130">toofurther explore ACS's functionality and tooexperiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
