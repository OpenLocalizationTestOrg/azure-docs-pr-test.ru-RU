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
# <a name="how-tooview-saml-returned-by-hello-azure-access-control-service"></a>Как tooview SAML возвращают hello Azure Access Control Service
В этом руководстве будет показано, как tooview hello базовый Security Assertion Markup Language (SAML) возвращают tooyour приложения hello службы управления доступом Azure (ACS). руководство по Hello лежит hello [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) раздела, предоставив код, отображающий сведения hello SAML. приложение Hello завершения будет выглядеть примерно следующие toohello.

![Пример выходных данных SAML][saml_output]

Дополнительные сведения о ACS см. в разделе hello [дальнейшие действия](#next_steps) раздела.

> [!NOTE]
> Hello фильтр управления служб Azure Access является CTP-версии. Эта предварительная версия программного обеспечения не обеспечивается официальной поддержкой корпорации Майкрософт.
> 
> 

## <a name="prerequisites"></a>Предварительные требования
Здравствуйте, toocomplete hello задачи в данном руководстве, полный пример в [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md) и использовать его в качестве начальной точки для этого учебника hello.

## <a name="add-hello-jspwriter-library-tooyour-build-path-and-deployment-assembly"></a>Добавить hello JspWriter библиотеки tooyour путь и развертывания сборки
Добавить hello библиотеку, содержащую hello **javax.servlet.jsp.JspWriter** tooyour класс сборки пути и развертывания. При использовании Tomcat hello библиотека — **jsp api.jar**, который находится в hello Apache **lib** папки.

1. В обозревателе проектов Eclipse, щелкните правой кнопкой мыши **MyACSHelloWorld**, нажмите кнопку **путь построения**, нажмите кнопку **настроить путь построения**, нажмите кнопку hello **библиотеки** , а затем щелкните **добавить внешний JAR-файлов**.
2. В hello **JAR выбора** диалоговое окно, перейдите toohello необходимые JAR-ФАЙЛ, выберите его и нажмите кнопку **откройте**.
3. С hello **свойства MyACSHelloWorld** диалоговом окне все еще открыто, щелкните **сборку развертывания**.
4. В hello **веб-развертывания сборки** диалоговое окно, нажмите кнопку **добавить**.
5. В hello **новый директива Assembly** диалоговое окно, нажмите кнопку **записи путь построения Java** и нажмите кнопку **Далее**.
6. Выберите соответствующую библиотеку hello и нажмите кнопку **Готово**.
7. Нажмите кнопку **ОК** tooclose hello **свойства MyACSHelloWorld** диалогового окна.

## <a name="modify-hello-jsp-file-toodisplay-saml"></a>Изменение hello JSP файл toodisplay SAML
Изменить **index.jsp** toouse hello, следующий код.

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

## <a name="run-hello-application"></a>Запустите приложение hello
1. Запуск приложения в эмуляторе hello компьютера или развернуть tooAzure, с помощью hello действия, описанные на [как tooAuthenticate веб-пользователей с Azure Access Control Service с помощью Eclipse](active-directory-java-authenticate-users-access-control-eclipse.md).
2. Запустите браузер и откройте в нем свое веб-приложение. После входа в систему tooyour приложения вы увидите сведения SAML, включая hello утверждение безопасности, предоставляемые поставщиком удостоверений hello.

## <a name="next-steps"></a>Дальнейшие действия
toofurther исследовать функциональные возможности службы ACS и tooexperiment с более сложных сценариях см. в разделе [Access Control Service 2.0][Access Control Service 2.0].

[Prerequisites]: #pre
[Modify hello JSP file toodisplay SAML]: #modify_jsp
[Add hello JspWriter library tooyour build path and deployment assembly]: #add_library
[Run hello application]: #run_application
[Next steps]: #next_steps
[Access Control Service 2.0]: http://go.microsoft.com/fwlink/?LinkID=212360
[How tooAuthenticate Web Users with Azure Access Control Service Using Eclipse]: active-directory-java-authenticate-users-access-control-eclipse
[saml_output]: ./media/active-directory-java-view-saml-returned-by-access-control/SAML_Output.png
