---
title: 'Tutorial: Zugreifen auf Microsoft Graph als App durch eine Web-App | Azure'
description: In diesem Tutorial wird beschrieben, wie Sie über verwaltete Identitäten auf Daten in Microsoft Graph zugreifen.
services: microsoft-graph, app-service-web
author: rwike77
manager: CelesteDG
ms.service: app-service-web
ms.topic: tutorial
ms.workload: identity
ms.date: 11/09/2020
ms.author: ryanwi
ms.reviewer: stsoneff
ms.openlocfilehash: 70b180efa35d6310735f045a85103719b17c8555
ms.sourcegitcommit: 0dcafc8436a0fe3ba12cb82384d6b69c9a6b9536
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/10/2020
ms.locfileid: "94428258"
---
# <a name="tutorial-access-microsoft-graph-from-a-secured-app-as-the-app"></a>Tutorial: Zugreifen auf Microsoft Graph über eine geschützte App als App

Es wird beschrieben, wie Sie über eine Web-App, die in Azure App Service ausgeführt wird, auf Microsoft Graph zugreifen.

:::image type="content" alt-text="Zugriff auf Microsoft Graph" source="./media/scenario-secure-app-access-microsoft-graph/web-app-access-graph.svg" border="false":::

Sie möchten Microsoft Graph im Namen der Web-App aufrufen.  Eine sichere Methode, um Ihrer Web-App den Zugriff auf Daten zu gewähren, ist die Verwendung einer [systemseitig zugewiesenen verwalteten Identität](/azure/active-directory/managed-identities-azure-resources/overview). Mit einer verwalteten Identität über Azure AD können App Services per rollenbasierter Zugriffssteuerung (Role-Based Access Control, RBAC) auf Ressourcen zugreifen, ohne dass die App-Anmeldeinformationen benötigt werden. Nachdem Sie Ihrer Web-App eine verwaltete Identität zugewiesen haben, kümmert sich Azure um die Erstellung und Verteilung eines Zertifikats.  Sie müssen sich keine Gedanken über die Verwaltung von Geheimnissen oder App-Anmeldeinformationen machen.

In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
>
> * Erstellen einer systemseitig zugewiesenen verwalteten Identität in einer Web-App
> * Hinzufügen von Microsoft Graph-API-Berechtigungen zu einer verwalteten Identität
> * Aufrufen von Microsoft Graph über eine Web-App mit verwalteten Identitäten

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prerequisites"></a>Voraussetzungen

* Eine unter Azure App Service ausgeführte Webanwendung, für die das [App Service-Modul für die Authentifizierung/Autorisierung aktiviert ist](scenario-secure-app-authentication-app-service.md).

## <a name="enable-managed-identity-on-app"></a>Aktivieren einer verwalteten Identität für die App

Wenn Sie Ihre Web-App mit Visual Studio erstellen und veröffentlichen, wird die verwaltete Identität für Sie in Ihrer App aktiviert. Wählen Sie auf Ihrer App Service-Instanz im linken Navigationsbereich die Option **Identität** und dann **Vom System zugewiesen** aus.  Vergewissern Sie sich, dass der **Status** auf **Ein** festgelegt ist.  Falls nicht: Klicken Sie auf **Speichern** und dann auf **Ja**, um die systemseitig zugewiesene verwaltete Identität zu aktivieren.  Wenn die verwaltete Identität aktiviert ist, ist der Status auf *Ein* festgelegt, und die Objekt-ID ist verfügbar.

Notieren Sie sich die **Objekt-ID**, da Sie sie im nächsten Schritt benötigen.

:::image type="content" alt-text="Systemzugewiesene Identität" source="./media/scenario-secure-app-access-microsoft-graph/create-system-assigned-identity.png":::

## <a name="grant-access-to-microsoft-graph"></a>Gewähren von Zugriff auf Microsoft Graph

Beim Zugreifen auf Microsoft Graph muss die verwaltete Identität über die entsprechenden Berechtigungen für den Vorgang verfügen, der ausgeführt werden soll. Derzeit gibt es keine Möglichkeit, diese Berechtigungen über das Azure-Portal zuzuweisen. Mit dem folgenden Skript werden die angeforderten Microsoft Graph-API-Berechtigungen dem Dienstprinzipalobjekt der verwalteten Identität hinzugefügt:

# <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

```powershell
# Install the module (You need admin on the machine)
#Install-Module AzureAD 

# Your tenant id (in Azure Portal, under Azure Active Directory -> Overview )
$TenantID="<tenant-id>"
$resourceGroup = "securewebappresourcegroup"
$webAppName="SecureWebApp-20201102125811"

# Get ID of the managed identity for the web app
$spID = (Get-AzWebApp -ResourceGroupName $resourceGroup -Name $webAppName).identity.principalid

# Check the Microsoft Graph documentation for the permission you need for the operation
$PermissionName = "User.Read.All"

Connect-AzureAD -TenantId $TenantID

# Get the service principal for Microsoft Graph
$GraphServicePrincipal = Get-AzureADServicePrincipal -SearchString "Microsoft Graph"

# Assign permissions to managed identity service principal
$AppRole = $GraphServicePrincipal.AppRoles | `
Where-Object {$_.Value -eq $PermissionName -and $_.AllowedMemberTypes -contains "Application"}

New-AzureAdServiceAppRoleAssignment -ObjectId $spID -PrincipalId $spID `
-ResourceId $GraphServicePrincipal.ObjectId -Id $AppRole.Id
```

# <a name="azure-cli"></a>[Azure-Befehlszeilenschnittstelle](#tab/azure-cli)

```azurecli-interactive
az login

webAppName="SecureWebApp-20201106120003"

spId=$(az resource list -n $webAppName --query [*].identity.principalId --out tsv)

graphResourceId=$(az ad sp list --display-name "Microsoft Graph" --query [0].objectId --out tsv)

appRoleId=$(az ad sp list --display-name "Microsoft Graph" --query "[0].appRoles[?value=='User.Read.All' && contains(allowedMemberTypes, 'Application')].id" --output tsv)

uri=https://graph.microsoft.com/v1.0/servicePrincipals/$spID/appRoleAssignments

body="{'principalId':'$spId','resourceId':'$graphResourceId','appRoleId':'$appRoleId'}"

az rest --method post --uri $uri --body $body --headers "Content-Type=application/json"
```

---

Nachdem Sie das Skript ausgeführt haben, können Sie im [Azure-Portal](https://portal.azure.com) überprüfen, ob die angeforderten API-Berechtigungen der verwalteten Identität zugewiesen wurden.  Navigieren Sie zu **Azure Active Directory**, und wählen Sie die Option **Unternehmensanwendungen** aus.  Auf diesem Blatt werden alle Dienstprinzipale Ihres Mandanten angezeigt.  Wählen Sie unter **Alle Anwendungen** den Dienstprinzipal für die verwaltete Identität aus.  In diesem Tutorial werden zwei Dienstprinzipale genutzt, die den gleichen Anzeigenamen haben (z. B. „SecureWebApp2020094113531“).  Der Dienstprinzipal mit einer *URL für Startseite* steht für die Web-App Ihres Mandanten.  Der Dienstprinzipal ohne *URL für Startseite* steht für die systemseitig zugewiesene verwaltete Identität Ihrer Web-App. Die Objekt-ID für die verwaltete Identität stimmt mit der Objekt-ID der Identität überein, die Sie weiter oben erstellt haben.  

Wählen Sie den Dienstprinzipal für die verwaltete Identität aus.

:::image type="content" alt-text="Alle Anwendungen" source="./media/scenario-secure-app-access-microsoft-graph/enterprise-apps-all-applications.png":::

Wenn Sie unter **Übersicht** die Option **Berechtigungen** auswählen, werden die hinzugefügten Berechtigungen für Microsoft Graph angezeigt.

:::image type="content" alt-text="Berechtigungen" source="./media/scenario-secure-app-access-microsoft-graph/enterprise-apps-permissions.png":::

## <a name="call-microsoft-graph-net"></a>Aufrufen von Microsoft Graph (.NET)

Die Klasse [DefaultAzureCredential](/dotnet/api/azure.identity.defaultazurecredential) wird zum Abrufen von Tokenanmeldeinformationen für Ihren Code verwendet, um Anforderungen für Azure Storage zu autorisieren.  Erstellen Sie eine Instanz der Klasse [DefaultAzureCredential](/dotnet/api/azure.identity.defaultazurecredential), bei der die verwaltete Identität zum Abrufen von Token verwendet wird, und fügen Sie diese dem Dienstclient hinzu. Im folgenden Codebeispiel werden die authentifizierten Tokenanmeldeinformationen abgerufen und zum Erstellen eines Dienstclientobjekts verwendet, mit dem die Benutzer der Gruppe abgerufen werden.  

### <a name="install-microsoftgraph-client-library-package"></a>Installieren des Pakets mit der Microsoft.Graph-Clientbibliothek

Installieren Sie das [Microsoft.Graph-NuGet-Paket](https://www.nuget.org/packages/Microsoft.Graph) in Ihrem Projekt, indem Sie die .NET Core-Befehlszeilenschnittstelle oder die Paket-Manager-Konsole in Visual Studio verwenden.

# <a name="command-line"></a>[Befehlszeile](#tab/command-line)

Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.

Führen Sie die Installationsbefehle aus:

```dotnetcli
dotnet add package Microsoft.Graph
```

# <a name="package-manager"></a>[Paket-Manager](#tab/package-manager)

Öffnen Sie das Projekt bzw. die Projektmappe in Visual Studio und dann die Konsole mit dem Befehl **Extras** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole**.

Führen Sie die Installationsbefehle aus:
```powershell
Install-Package Microsoft.Graph
```

---

### <a name="example"></a>Beispiel

```csharp
using System;
using System.Collections.Generic;
using System.Threading.Tasks;
using Microsoft.AspNetCore.Mvc.RazorPages;
using Azure.Identity;
using Microsoft.Graph.Core;
using System.Net.Http.Headers;

...

public IList<MSGraphUser> Users { get; set; }

public async Task OnGetAsync()
{
    // Create the Graph service client with a DefaultAzureCredential which gets an access token using the available Managed Identity
    var credential = new DefaultAzureCredential();
    var token = credential.GetToken(
        new Azure.Core.TokenRequestContext(
            new[] { "https://graph.microsoft.com/.default" }));

    var accessToken = token.Token;
    var graphServiceClient = new GraphServiceClient(
        new DelegateAuthenticationProvider((requestMessage) =>
        {
            requestMessage
            .Headers
            .Authorization = new AuthenticationHeaderValue("bearer", accessToken);

            return Task.CompletedTask;
        }));

    List<MSGraphUser> msGraphUsers = new List<MSGraphUser>();
    try
    {
        var users =await graphServiceClient.Users.Request().GetAsync();
        foreach(var u in users)
        {
            MSGraphUser user = new MSGraphUser();
            user.userPrincipalName = u.UserPrincipalName;
            user.displayName = u.DisplayName;
            user.mail = u.Mail;
            user.jobTitle = u.JobTitle;

            msGraphUsers.Add(user);
        }
    }
    catch(Exception ex)
    {
        string msg = ex.Message;
    }

    Users = msGraphUsers;
}
```

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Wenn Sie dieses Tutorial abgeschlossen haben und die Web-App und die zugehörigen Ressourcen nicht mehr benötigen, sollten Sie [die von Ihnen erstellten Ressourcen bereinigen](scenario-secure-app-clean-up-resources.md).

## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie Folgendes gelernt:

> [!div class="checklist"]
>
> * Erstellen einer systemseitig zugewiesenen verwalteten Identität in einer Web-App
> * Hinzufügen von Microsoft Graph-API-Berechtigungen zu einer verwalteten Identität
> * Aufrufen von Microsoft Graph über eine Web-App mit verwalteten Identitäten

Informieren Sie sich darüber, wie Sie für eine [.NET Core-App](tutorial-dotnetcore-sqldb-app.md), [Python-App](tutorial-python-postgresql-app.md), [Java-App](tutorial-java-spring-cosmosdb.md) oder [Node.js-App](tutorial-nodejs-mongodb-app.md) eine Verbindung mit einer Datenbank herstellen.