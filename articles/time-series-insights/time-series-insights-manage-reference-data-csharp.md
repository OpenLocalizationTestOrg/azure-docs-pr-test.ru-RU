---
title: "Управление эталонными данными для среды Azure Time Series Insights с помощью C# | Документация Майкрософт"
description: "Это руководство содержит сведения об управлении эталонными данными для среды Time Series Insights с помощью C#."
keywords: 
services: time-series-insights
documentationcenter: 
author: venkatgct
manager: almineev
editor: cgronlun
ms.assetid: 
ms.service: tsi
ms.devlang: na
ms.topic: how-to-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: venkatja
ms.openlocfilehash: 528a33cf01b2a0a07880dad62ba6bbaf4a605153
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: ru-RU
ms.lasthandoff: 10/11/2017
---
# <a name="manage-reference-data-for-an-azure-time-series-insights-environment-by-using-c"></a>Управление эталонными данными для среды Azure Time Series Insights с помощью C#

В этом примере C# демонстрируется, как управлять эталонными данными для среды Time Series Insights.
Перед выполнением примера убедитесь, что были выполнены следующие действия.
1. Набор эталонных данных создан в соответствии с инструкциями в [этой статье](time-series-insights-add-reference-data-set.md).
2. Маркер доступа, используемый при выполнении приложения, получен с помощью API Azure Active Directory. Этот маркер должен передаваться в заголовке `Authorization` каждого запроса API запроса. Сведения о настройке приложений с неинтерактивной проверкой подлинности см. в статье [Аутентификация и авторизация](time-series-insights-authentication-and-authorization.md).
3. Все константы, определенные в начале примера, указаны правильно.

## <a name="c-sample"></a>Пример на языке C#

```csharp
// Copyright (c) Microsoft Corporation.  All rights reserved.

using System;
using System.IO;
using System.Net;
using System.Threading.Tasks;
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using Newtonsoft.Json;
using Newtonsoft.Json.Linq;

namespace TimeSeriesInsightsReferenceDataSampleApp
{
    public static class Program
    {
        // SET the environment fqdn.
        private static string EnvironmentFqdn = "#DUMMY#.env.timeseries.azure.com";

        // SET the environment reference data set name used when creating it.
        private static string EnvironmentReferenceDataSetName = "#DUMMY#";

        // For automated execution under application identity,
        // use application created in Active Directory.
        // To create the application in AAD, follow the steps provided here:
        // https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization

        // SET the application ID of application registered in your Azure Active Directory
        private static string ApplicationClientId = "#DUMMY#";

        // SET the application key of the application registered in your Azure Active Directory
        private static string ApplicationClientSecret = "#DUMMY#";

        // SET the Azure Active Directory tenant.
        private static string Tenant = "#DUMMY#.onmicrosoft.com";

        private static async Task DemoReferenceDataAsync()
        {
            // 1. Acquire an access token.
            string accessToken = await AcquireAccessTokenAsync();

            // 2. Put a new reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""put"": [{
        ""DeviceId"": ""Fan1"",
        ""Type"": ""Fan"",
        ""BladeCount"": ""3""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Put", input: input, output: output);
            }

            // 3. Get reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""get"": [{
        ""DeviceId"": ""Fan1""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Get", input: input, output: output);
            }

            // 4. Patch an existing reference data item.
            // Update BladeCount and add Colour.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""patch"": [{
        ""DeviceId"": ""Fan1"",
        ""BladeCount"": ""4"",
        ""Colour"": ""Brown""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Patch", input: input, output: output);
            }

            // 5. Delete a property from an existing reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""deleteproperties"": [{
        ""key"": {
            ""DeviceId"": ""Fan1""
        },
        ""properties"": [""BladeCount""]
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "DeleteProperties", input: input, output: output);
            }

            // 6. Delete an existing reference data item.
            {
                HttpWebRequest request = CreateWebRequest(accessToken);
                string input = @"
{
    ""delete"": [{
        ""DeviceId"": ""Fan1""
    }]
}";
                await SendRequestAsync(request, input);
                string output = await GetResponseAsync(request);
                PrintInputOutput(action: "Delete", input: input, output: output);
            }
        }

        private static async Task<string> AcquireAccessTokenAsync()
        {
            if (ApplicationClientId == "#DUMMY#" || ApplicationClientSecret == "#DUMMY#" || Tenant.StartsWith("#DUMMY#"))
            {
                throw new Exception(
                    $"Use the link {"https://docs.microsoft.com/en-us/azure/time-series-insights/time-series-insights-authentication-and-authorization"} to update the values of 'ApplicationClientId', 'ApplicationClientSecret' and 'Tenant'.");
            }

            var authenticationContext = new AuthenticationContext(
                $"https://login.windows.net/{Tenant}",
                TokenCache.DefaultShared);

            AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
                resource: "https://api.timeseries.azure.com/",
                clientCredential: new ClientCredential(
                    clientId: ApplicationClientId,
                    clientSecret: ApplicationClientSecret));

            // Show interactive logon dialog to acquire token on behalf of the user.
            // Suitable for native apps, and not on server-side of a web application.
            //AuthenticationResult token = await authenticationContext.AcquireTokenAsync(
            //    resource: "https://api.timeseries.azure.com/",
            //    // Set well-known client ID for Azure PowerShell
            //    clientId: "1950a258-227b-4e31-a9cf-717495945fc2",
            //    // Set redirect URI for Azure PowerShell
            //    redirectUri: new Uri("urn:ietf:wg:oauth:2.0:oob"),
            //    parameters: new PlatformParameters(PromptBehavior.Auto));

            return token.AccessToken;
        }

        private static HttpWebRequest CreateWebRequest(string accessToken)
        {
            Uri uri = new UriBuilder("https", EnvironmentFqdn)
            {
                Path = $"referencedatasets/{EnvironmentReferenceDataSetName}/$batch",
                Query = "api-version=2016-12-12"
            }.Uri;
            HttpWebRequest request = WebRequest.CreateHttp(uri);
            request.Method = "POST";
            request.Headers.Add("x-ms-client-application-name", "TimeSeriesInsightsReferenceDataSample");
            request.Headers.Add("Authorization", "Bearer " + accessToken);
            return request;
        }

        private static async Task SendRequestAsync(HttpWebRequest request, string json)
        {
            using (var stream = await request.GetRequestStreamAsync())
            using (var streamWriter = new StreamWriter(stream))
            {
                await streamWriter.WriteAsync(json);
                await streamWriter.FlushAsync();
                streamWriter.Close();
            }
        }

        private static async Task<string> GetResponseAsync(HttpWebRequest request)
        {
            using (WebResponse webResponse = await request.GetResponseAsync())
            using (var sr = new StreamReader(webResponse.GetResponseStream()))
            {
                string result = await sr.ReadToEndAsync();
                return result;
            }
        }

        private static void PrintInputOutput(string action, string input, string output)
        {
            Console.WriteLine("=== {0} request ===", action);
            Console.WriteLine("Input: {0}", JsonConvert.SerializeObject(JsonConvert.DeserializeObject<JObject>(input), Formatting.Indented));
            Console.WriteLine("Output: {0}", JsonConvert.SerializeObject(JsonConvert.DeserializeObject<JObject>(output), Formatting.Indented));
            Console.WriteLine();
        }

        static void Main(string[] args)
        {
            Task.Run(async () => await DemoReferenceDataAsync()).Wait();
        }
    }
}
```

## <a name="next-steps"></a>Дальнейшие действия

Полный справочник по API см. [здесь](/rest/api/time-series-insights/time-series-insights-reference-reference-data-api).