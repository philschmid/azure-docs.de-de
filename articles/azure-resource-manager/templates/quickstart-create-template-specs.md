---
title: Erstellen und Bereitstellen von Vorlagenspezifikationen
description: Erfahren Sie, wie Sie eine Vorlagenspezifikation aus einer ARM-Vorlage erstellen. Stellen Sie dann die Vorlagenspezifikation für eine Ressourcengruppe in Ihrem Abonnement bereit.
author: tfitzmac
ms.date: 11/10/2020
ms.topic: quickstart
ms.author: tomfitz
ms.openlocfilehash: 96ef5796aac1d0ee02e6bbafc40b7d3bcdea4e2f
ms.sourcegitcommit: 4bee52a3601b226cfc4e6eac71c1cb3b4b0eafe2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/11/2020
ms.locfileid: "94506361"
---
# <a name="quickstart-create-and-deploy-template-spec-preview"></a>Schnellstart: Erstellen und Bereitstellen von Vorlagenspezifikationen (Vorschau)

Dieser Schnellstart zeigt Ihnen, wie Sie eine Azure Resource Manager-Vorlage (ARM-Vorlage) in eine [Vorlagenspezifikation](template-specs.md) packen und diese Vorlagenspezifikation dann bereitstellen. Ihre Vorlagenspezifikation enthält eine ARM-Vorlage, mit der ein Speicherkonto bereitgestellt wird.

## <a name="prerequisites"></a>Voraussetzungen

Ein Azure-Konto mit einem aktiven Abonnement. Sie können [kostenlos ein Konto erstellen](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).

> [!NOTE]
> Vorlagenspezifikationen befinden sich derzeit in der Vorschauversion. Um sie zu verwenden, müssen Sie sich [für die Warteliste registrieren](https://aka.ms/templateSpecOnboarding).
>
> Nachdem Sie von der Warteliste genehmigt wurden, erhalten Sie Anweisungen zur Installation des PowerShell-Vorschaumoduls und des CLI-Vorschaumoduls.

## <a name="create-template-spec"></a>Erstellen von Vorlagenspezifikationen

Die Vorlagenspezifikation ist ein Ressourcentyp namens **Microsoft.Resources/templateSpecs**. Sie können zur Erstellung Ihrer Vorlagenspezifikation Azure PowerShell, die Azure CLI oder eine ARM-Vorlage verwenden. Bei allen Optionen benötigen Sie ein ARM-Vorlage, die in der Vorlagenspezifikation verpackt ist.

Bei PowerShell und der CLI wird die ARM-Vorlage als Parameter an den Befehl übergeben. Bei der ARM-Vorlage wird die ARM-Vorlage, die innerhalb der Vorlagenspezifikation verpackt werden soll, in die Definition der Vorlagenspezifikation eingebettet.

Diese Optionen werden nachstehend vorgestellt.

# <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

1. Wenn Sie eine Vorlagenspezifikation mit PowerShell erstellen, können Sie eine lokale Vorlage übergeben. Kopieren Sie die folgende Vorlage, und speichern Sie sie lokal in einer Datei namens **azuredeploy.json**. In dieser Schnellstartanleitung wird davon ausgegangen, dass die Speicherung im Pfad **c:\Templates\azuredeploy.json** erfolgt ist, aber Sie können einen beliebigen Pfad verwenden.

    :::code language="json" source="~/quickstart-templates/101-storage-account-create/azuredeploy.json":::

1. Erstellen Sie eine neue Ressourcengruppe, die die Vorlagenspezifikation enthält.

    ```azurepowershell
    New-AzResourceGroup `
      -Name templateSpecRG `
      -Location westus2
    ```

1. Erstellen Sie dann die Vorlagenspezifikation in dieser Ressourcengruppe. Sie weisen der neuen Vorlagenspezifikation den Namen **storageSpec** zu.

    ```azurepowershell
    New-AzTemplateSpec `
      -Name storageSpec `
      -Version "1.0" `
      -ResourceGroupName templateSpecRG `
      -Location westus2 `
      -TemplateFile "c:\Templates\azuredeploy.json"
    ```

# <a name="cli"></a>[BEFEHLSZEILENSCHNITTSTELLE (CLI)](#tab/azure-cli)

1. Wenn Sie eine Vorlagenspezifikation mit der CLI erstellen, können Sie eine lokale Vorlage übergeben. Kopieren Sie die folgende Vorlage, und speichern Sie sie lokal in einer Datei namens **azuredeploy.json**. In dieser Schnellstartanleitung wird davon ausgegangen, dass die Speicherung im Pfad **c:\Templates\azuredeploy.json** erfolgt ist, aber Sie können einen beliebigen Pfad verwenden.

    :::code language="json" source="~/quickstart-templates/101-storage-account-create/azuredeploy.json":::

1. Erstellen Sie eine neue Ressourcengruppe, die die Vorlagenspezifikation enthält.

    ```azurecli
    az group create \
      --name templateSpecRG \
      --location westus2
    ```

1. Erstellen Sie dann die Vorlagenspezifikation in dieser Ressourcengruppe. Sie weisen der neuen Vorlagenspezifikation den Namen **storageSpec** zu.

    ```azurecli
    az ts create \
      --name storageSpec \
      --version "1.0" \
      --resource-group templateSpecRG \
      --location "westus2" \
      --template-file "c:\Templates\azuredeploy.json"
    ```

# <a name="arm-template"></a>[ARM-Vorlage](#tab/azure-resource-manager)

1. Wenn Sie eine ARM-Vorlage zum Erstellen der Vorlagenspezifikation verwenden, wird die Vorlage in die Ressourcendefinition eingebettet. Kopieren Sie die folgende Vorlage, und speichern Sie sie lokal als **azuredeploy.json**. In dieser Schnellstartanleitung wird davon ausgegangen, dass die Speicherung im Pfad **c:\Templates\azuredeploy.json** erfolgt ist, aber Sie können einen beliebigen Pfad verwenden.

    > [!NOTE]
    > In der eingebetteten Vorlage müssen alle [Vorlagenausdrücke](template-expressions.md) eine zweite linke eckige Klammer als Escapezeichen verwenden. Verwenden Sie `"[[` anstelle von `"[`. JSON-Arrays verwenden weiterhin eine einzelne linke eckige Klammer.

    ```json
    {
      "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "functions": [],
      "variables": {},
      "resources": [
        {
          "type": "Microsoft.Resources/templateSpecs",
          "apiVersion": "2019-06-01-preview",
          "name": "storageSpec",
          "location": "westus2",
          "properties": {
            "displayName": "Storage template spec"
          },
          "tags": {},
          "resources": [
            {
              "type": "versions",
              "apiVersion": "2019-06-01-preview",
              "name": "1.0",
              "location": "westus2",
              "dependsOn": [ "storageSpec" ],
              "properties": {
                "template": {
                  "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
                  "contentVersion": "1.0.0.0",
                  "parameters": {
                    "storageAccountType": {
                      "type": "string",
                      "defaultValue": "Standard_LRS",
                      "allowedValues": [
                        "Standard_LRS",
                        "Standard_GRS",
                        "Standard_ZRS",
                        "Premium_LRS"
                      ],
                      "metadata": {
                        "description": "Storage Account type"
                      }
                    },
                    "location": {
                      "type": "string",
                      "defaultValue": "[[resourceGroup().location]",
                      "metadata": {
                        "description": "Location for all resources."
                      }
                    }
                  },
                  "variables": {
                    "storageAccountName": "[[concat('store', uniquestring(resourceGroup().id))]"
                  },
                  "resources": [
                    {
                      "type": "Microsoft.Storage/storageAccounts",
                      "apiVersion": "2019-04-01",
                      "name": "[[variables('storageAccountName')]",
                      "location": "[[parameters('location')]",
                      "sku": {
                        "name": "[[parameters('storageAccountType')]"
                      },
                      "kind": "StorageV2",
                      "properties": {}
                    }
                  ],
                  "outputs": {
                    "storageAccountName": {
                      "type": "string",
                      "value": "[[variables('storageAccountName')]"
                    }
                  }
                }
              },
              "tags": {}
            }
          ]
        }
      ],
      "outputs": {}
    }
    ```

1. Verwenden Sie die Azure CLI oder PowerShell, um eine neue Ressourcengruppe zu erstellen.

    ```azurepowershell
    New-AzResourceGroup `
      -Name templateSpecRG `
      -Location westus2
    ```

    ```azurecli
    az group create \
      --name templateSpecRG \
      --location westus2
    ```

1. Stellen Sie Ihre Vorlage mit der Azure CLI oder mit PowerShell bereit.

    ```azurepowershell
    New-AzResourceGroupDeployment `
      -ResourceGroupName templateSpecRG `
      -TemplateFile "c:\Templates\azuredeploy.json"
    ```

    ```azurecli
    az deployment group create \
      --name templateSpecRG \
      --template-file "c:\Templates\azuredeploy.json"
    ```

---

## <a name="deploy-template-spec"></a>Bereitstellen der Vorlagenspezifikationen

Jetzt können Sie die Vorlagenspezifikation bereitstellen. Das Bereitstellen der Vorlagenspezifikation gestaltet sich genauso wie die Bereitstellung der enthaltenen Vorlage, mit der Ausnahme, dass Sie die Ressourcen-ID der Vorlagenspezifikation übergeben. Sie verwenden dieselben Bereitstellungsbefehle und übergeben bei Bedarf Parameterwerte für die Vorlagenspezifikation.

# <a name="powershell"></a>[PowerShell](#tab/azure-powershell)

1. Erstellen Sie eine Ressourcengruppe, die das neue Speicherkonto enthält.

    ```azurepowershell
    New-AzResourceGroup `
      -Name storageRG `
      -Location westus2
    ```

1. Rufen Sie die Ressourcen-ID der Vorlagenspezifikation ab.

    ```azurepowershell
    $id = (Get-AzTemplateSpec -ResourceGroupName templateSpecRG -Name storageSpec -Version "1.0").Versions.Id
    ```

1. Stellen Sie die Vorlagenspezifikation bereit.

    ```azurepowershell
    New-AzResourceGroupDeployment `
      -TemplateSpecId $id `
      -ResourceGroupName storageRG
    ```

1. Sie geben die Parameter genau wie bei einer ARM-Vorlage an. Stellen Sie die Vorlagenspezifikation mit einem Parameter für den Speicherkontotyp erneut bereit.

    ```azurepowershell
    New-AzResourceGroupDeployment `
      -TemplateSpecId $id `
      -ResourceGroupName storageRG `
      -storageAccountType Standard_GRS
    ```

# <a name="cli"></a>[BEFEHLSZEILENSCHNITTSTELLE (CLI)](#tab/azure-cli)

1. Erstellen Sie eine Ressourcengruppe, die das neue Speicherkonto enthält.

    ```azurecli
    az group create \
      --name storageRG \
      --location westus2
    ```

1. Rufen Sie die Ressourcen-ID der Vorlagenspezifikation ab.

    ```azurecli
    id = $(az ts show --name storageSpec --resource-group templateSpecRG --version "1.0" --query "id")
    ```

    > [!NOTE]
    > Es gibt ein bekanntes Problem beim Abrufen der Vorlagenspezifikations-ID und deren Zuweisung zu einer Variablen in Windows PowerShell.

1. Stellen Sie die Vorlagenspezifikation bereit.

    ```azurecli
    az deployment group create \
      --resource-group storageRG \
      --template-spec $id
    ```

1. Sie geben die Parameter genau wie bei einer ARM-Vorlage an. Stellen Sie die Vorlagenspezifikation mit einem Parameter für den Speicherkontotyp erneut bereit.

    ```azurecli
    az deployment group create \
      --resource-group storageRG \
      --template-spec $id \
      --parameters storageAccountType='Standard_GRS'
    ```

# <a name="arm-template"></a>[ARM-Vorlage](#tab/azure-resource-manager)

1. Kopieren Sie die folgende Vorlage, und speichern Sie sie lokal in einer Datei namens **storage.json**.

    ```json
       {
      "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {},
      "functions": [],
      "variables": {},
      "resources": [
        {
          "type": "Microsoft.Resources/deployments",
          "apiVersion": "2020-06-01",
          "name": "demo",
          "properties": {
            "templateLink": {
              "id": "[resourceId('templateSpecRG', 'Microsoft.Resources/templateSpecs/versions', 'storageSpec', '1.0')]"
            },
            "parameters": {
            },
            "mode": "Incremental"
          }
        }
      ],
      "outputs": {}
    }
    ```

1. Verwenden Sie die Azure CLI oder PowerShell, um eine neue Ressourcengruppe für das Speicherkonto zu erstellen.

    ```azurepowershell
    New-AzResourceGroup `
      -Name storageRG `
      -Location westus2
    ```

    ```azurecli
    az group create \
      --name storageRG \
      --location westus2
    ```

1. Stellen Sie Ihre Vorlage mit der Azure CLI oder mit PowerShell bereit.

    ```azurepowershell
    New-AzResourceGroupDeployment `
      -ResourceGroupName storageRG `
      -TemplateFile "c:\Templates\storage.json"
    ```

    ```azurecli
    az deployment group create \
      --name storageRG \
      --template-file "c:\Templates\storage.json"
    ```

---

## <a name="grant-access"></a>Gewähren von Zugriff

Wenn Sie anderen Benutzern in Ihrer Organisation die Bereitstellung Ihrer Vorlagenspezifikation gestatten möchten, müssen Sie ihnen Lesezugriff gewähren. Sie können die Rolle „Leser“ einer Azure AD-Gruppe für die Ressourcengruppe zuweisen, die freizugebende Vorlagenspezifikationen enthält. Weitere Informationen finden Sie im [Tutorial: Gewähren des Zugriffs auf Azure-Ressourcen für eine Gruppe mithilfe von Azure PowerShell](../../role-based-access-control/tutorial-role-assignments-group-powershell.md).

## <a name="clean-up-resources"></a>Bereinigen von Ressourcen

Löschen Sie zum Bereinigen der in dieser Schnellstartanleitung bereitgestellten Ressource beide Ressourcengruppen, die Sie erstellt haben.

1. Wählen Sie im Azure-Portal im linken Menü die Ressourcengruppe aus.

1. Geben Sie den Ressourcengruppennamen (templateSpecRG und storageRG) in das Feld „Nach Name filtern“ ein.

1. Klicken Sie auf den Namen der Ressourcengruppe.

1. Wählen Sie im Menü ganz oben den Befehl zum Löschen der Ressourcengruppe aus.

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zum Erstellen einer Vorlagenspezifikation, die verknüpfte Vorlagen umfasst, finden Sie unter [Erstellen einer Vorlagenspezifikation einer verknüpften Vorlage](template-specs-create-linked.md).
