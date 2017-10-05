---
title: "Просмотр кода SAML, возвращаемого службой контроля доступа (Java)"
description: "Узнайте, как просматривать SAML, возвращенный службой контроля доступа в приложениях Java, размещенных в Azure."
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
ms.openlocfilehash: 1552e624a4703138ab82f7133ceaec3dbd04e1db
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: ru-RU
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-view-saml-returned-by-the-azure-access-control-service"></a><span data-ttu-id="c2546-103">Как просматривать SAML, возвращенный службой Azure Access Control</span><span class="sxs-lookup"><span data-stu-id="c2546-103">How to view SAML returned by the Azure Access Control Service</span></span>
<span data-ttu-id="c2546-104">В этом руководстве показано, как просмотреть базовый код SAML, который возвращается в ваше приложение службой контроля доступа Azure (ACS).</span><span class="sxs-lookup"><span data-stu-id="c2546-104">This guide will show you how to view the underlying Security Assertion Markup Language (SAML) returned to your application by the Azure Access Control Service (ACS).</span></span> <span data-ttu-id="c2546-105">В этом руководстве используются материалы раздела [Проверка подлинности веб-пользователей с помощью службы контроля доступа Azure и Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md), в частности, код, позволяющий отображать данные SAML.</span><span class="sxs-lookup"><span data-stu-id="c2546-105">The guide builds on the [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) topic, by providing code that displays the SAML information.</span></span> <span data-ttu-id="c2546-106">Ниже приводится пример завершенного приложения.</span><span class="sxs-lookup"><span data-stu-id="c2546-106">The completed application will look similar to the following.</span></span>

![Пример выходных данных SAML][saml_output]

<span data-ttu-id="c2546-108">Дополнительные сведения об ACS см. в разделе [Дальнейшие действия](#next_steps).</span><span class="sxs-lookup"><span data-stu-id="c2546-108">For more information on ACS, see the [Next steps](#next_steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="c2546-109">Фильтр служб управления доступом Azure является CTP-версией.</span><span class="sxs-lookup"><span data-stu-id="c2546-109">The Azure Access Services Control Filter is a community technology preview.</span></span> <span data-ttu-id="c2546-110">Эта предварительная версия программного обеспечения не обеспечивается официальной поддержкой корпорации Майкрософт.</span><span class="sxs-lookup"><span data-stu-id="c2546-110">As pre-release software, it is not formally supported by Microsoft.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c2546-111">Предварительные требования</span><span class="sxs-lookup"><span data-stu-id="c2546-111">Prerequisites</span></span>
<span data-ttu-id="c2546-112">Прежде чем выполнять задачи данного руководства, выполните образец, представленный в разделе [Проверка подлинности веб-пользователей с помощью службы контроля доступа Azure и Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md), и используйте его в качестве отправной точки для дальнейшей работы.</span><span class="sxs-lookup"><span data-stu-id="c2546-112">To complete the tasks in this guide, complete the sample at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) and use it as the starting point for this tutorial.</span></span>

## <a name="add-the-jspwriter-library-to-your-build-path-and-deployment-assembly"></a><span data-ttu-id="c2546-113">Добавление библиотеки JspWriter к пути построения и сборке развертывания</span><span class="sxs-lookup"><span data-stu-id="c2546-113">Add the JspWriter library to your build path and deployment assembly</span></span>
<span data-ttu-id="c2546-114">Добавьте библиотеку, содержащую класс **javax.servlet.jsp.JspWriter** , к пути построения и сборке развертывания.</span><span class="sxs-lookup"><span data-stu-id="c2546-114">Add the library that contains the **javax.servlet.jsp.JspWriter** class to your build path and deployment assembly.</span></span> <span data-ttu-id="c2546-115">Библиотека **jsp-api.jar** для сервера Tomcat размещается в папке Apache **lib**.</span><span class="sxs-lookup"><span data-stu-id="c2546-115">If you are using Tomcat, the library is **jsp-api.jar**, which is located in the Apache **lib** folder.</span></span>

1. <span data-ttu-id="c2546-116">В обозревателе проектов Eclipse щелкните правой кнопкой мыши проект **MyACSHelloWorld**, выберите **Build Path** (Путь сборки), затем щелкните **Configure Build Path** (Настроить путь сборки), откройте вкладку **Libraries** (Библиотеки) и выберите **Add External JARs** (Добавить внешние JAR-файлы).</span><span class="sxs-lookup"><span data-stu-id="c2546-116">In Eclipse's Project Explorer, right-click **MyACSHelloWorld**, click **Build Path**, click **Configure Build Path**, click the **Libraries** tab, and then click **Add External JARs**.</span></span>
2. <span data-ttu-id="c2546-117">В диалоговом окне **JAR Selection** (Выбор JAR-файла) выберите нужный JAR-файл и нажмите кнопку **Open** (Открыть).</span><span class="sxs-lookup"><span data-stu-id="c2546-117">In the **JAR Selection** dialog, navigate to the necessary JAR, select it, and then click **Open**.</span></span>
3. <span data-ttu-id="c2546-118">Не закрывайте диалоговое окно **Свойства MyACSHelloWorld** и щелкните **Deployment Assembly** (Сборка развертывания).</span><span class="sxs-lookup"><span data-stu-id="c2546-118">With the **Properties for MyACSHelloWorld** dialog still open, click **Deployment Assembly**.</span></span>
4. <span data-ttu-id="c2546-119">В диалоговом окне **Web Deployment Assembly** (Сборка веб-развертывания) нажмите кнопку **Add** (Добавить).</span><span class="sxs-lookup"><span data-stu-id="c2546-119">In the **Web Deployment Assembly** dialog, click **Add**.</span></span>
5. <span data-ttu-id="c2546-120">В диалоговом окне **New Assembly Directive** (Новая директива сборки) щелкните **Java Build Path Entries** (Записи пути сборки Java) и нажмите кнопку **Next** (Далее).</span><span class="sxs-lookup"><span data-stu-id="c2546-120">In the **New Assembly Directive** dialog, click **Java Build Path Entries** and then click **Next**.</span></span>
6. <span data-ttu-id="c2546-121">Выберите соответствующую библиотеку и нажмите кнопку **Готово**.</span><span class="sxs-lookup"><span data-stu-id="c2546-121">Select the appropriate library and click **Finish**.</span></span>
7. <span data-ttu-id="c2546-122">Нажмите кнопку **ОК**, чтобы закрыть диалоговое окно **Свойства MyACSHelloWorld**.</span><span class="sxs-lookup"><span data-stu-id="c2546-122">Click **OK** to close the **Properties for MyACSHelloWorld** dialog.</span></span>

## <a name="modify-the-jsp-file-to-display-saml"></a><span data-ttu-id="c2546-123">Изменение JSP-файла для отображения кода SAML</span><span class="sxs-lookup"><span data-stu-id="c2546-123">Modify the JSP file to display SAML</span></span>
<span data-ttu-id="c2546-124">Измените файл **index.jsp** , используя следующий код.</span><span class="sxs-lookup"><span data-stu-id="c2546-124">Modify **index.jsp** to use the following code.</span></span>

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

                                 // If it is a text node, just print the text.
                                 if (list.item(0).getNodeName() == "#text")
                                 {
                                     out.println("Text value: <b>" + list.item(0).getTextContent() + "</b><br>");
                                 }
                                 else
                                 {
                                     // Print out the child node names.
                                     out.print("Contains " + nChild + " child node(s): ");   
                                        for (i=0; i < nChild; i++)
                                     {
                                        Node temp = list.item(i);

                                        out.print("<b>" + temp.getNodeName() + "</b>");
                                        if (i < nChild - 1)
                                        {
                                            // Separate the names.
                                            out.print(", ");
                                        }
                                        else
                                        {
                                            // Finish the sentence.
                                            out.print(".");
                                        }

                                     }
                                     out.println("<br>");

                                     // Process the child nodes.
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

            // Iterate the child nodes of the doc.
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

## <a name="run-the-application"></a><span data-ttu-id="c2546-125">Выполнение приложения</span><span class="sxs-lookup"><span data-stu-id="c2546-125">Run the application</span></span>
1. <span data-ttu-id="c2546-126">Запустите свое приложение в эмуляторе среды выполнения приложений или разверните его в среде Azure, следуя инструкциям раздела [Проверка подлинности веб-пользователей с помощью службы контроля доступа Azure и Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span><span class="sxs-lookup"><span data-stu-id="c2546-126">Run your application in the computer emulator or deploy to Azure, using the steps documented at [How to Authenticate Web Users with Azure Access Control Service Using Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).</span></span>
2. <span data-ttu-id="c2546-127">Запустите браузер и откройте в нем свое веб-приложение.</span><span class="sxs-lookup"><span data-stu-id="c2546-127">Launch a browser and open your web application.</span></span> <span data-ttu-id="c2546-128">После того, как вы войдете в приложение, будут показаны данные SAML, включая утверждения безопасности, предоставляемые поставщиком удостоверений.</span><span class="sxs-lookup"><span data-stu-id="c2546-128">After you log on to your application, you'll see SAML information, including the security assertion provided by the identity provider.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2546-129">Дальнейшие действия</span><span class="sxs-lookup"><span data-stu-id="c2546-129">Next steps</span></span>
<span data-ttu-id="c2546-130">Чтобы продолжить изучение функций ACS и поэкспериментировать с более сложными сценариями, см. документ [Служба Access Control Service 2.0][Access Control Service 2.0].</span><span class="sxs-lookup"><span data-stu-id="c2546-130">To further explore ACS's functionality and to experiment with more sophisticated scenarios, see [Access Control Service 2.0][Access Control Service 2.0].</span></span>

[Prerequisites]: #pre
[Modify the JSP file to display SAML]: #modify_jsp
[Add the JspWriter library to your build path and deployment assembly]: #add_library
[Run the application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How to Authenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
