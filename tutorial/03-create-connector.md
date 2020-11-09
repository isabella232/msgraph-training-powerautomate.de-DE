---
ms.openlocfilehash: 90462157024c529a1cf183230298fbf80813b8c9
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829777"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="9aff3-101">In dieser Übung erstellen Sie einen neuen benutzerdefinierten Connector, der in Microsoft Power Automation oder in Azure Logic-Apps verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="9aff3-101">In this exercise, you will create a new custom connector which can be used in Microsoft Power Automate or in Azure Logic Apps.</span></span> <span data-ttu-id="9aff3-102">Die OpenAPI-Definitionsdatei ist mit dem korrekten Pfad für den Microsoft Graph `$batch` -Endpunkt und zusätzlichen Einstellungen für den einfachen Import vordefiniert.</span><span class="sxs-lookup"><span data-stu-id="9aff3-102">The OpenAPI definition file is prebuilt with the correct path for the Microsoft Graph `$batch` endpoint and additional settings to enable simple import.</span></span>

<span data-ttu-id="9aff3-103">Es gibt zwei Optionen zum Erstellen eines benutzerdefinierten Connectors für Microsoft Graph:</span><span class="sxs-lookup"><span data-stu-id="9aff3-103">There are two options to create a custom connector for Microsoft Graph:</span></span>

- <span data-ttu-id="9aff3-104">Erstellen aus leer</span><span class="sxs-lookup"><span data-stu-id="9aff3-104">Create from blank</span></span>
- <span data-ttu-id="9aff3-105">Importieren einer OpenAPI-Datei</span><span class="sxs-lookup"><span data-stu-id="9aff3-105">Import an OpenAPI file</span></span>

## <a name="option-1-create-custom-connector-from-blank-template"></a><span data-ttu-id="9aff3-106">Option 1: Erstellen eines benutzerdefinierten Connectors aus einer leeren Vorlage</span><span class="sxs-lookup"><span data-stu-id="9aff3-106">Option 1: Create custom connector from blank template</span></span>

<span data-ttu-id="9aff3-107">Öffnen Sie einen Browser, und navigieren Sie zu [Microsoft Power Automation](https://flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9aff3-107">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="9aff3-108">Melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an.</span><span class="sxs-lookup"><span data-stu-id="9aff3-108">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="9aff3-109">Wählen Sie im linken Menü **Daten** aus, und wählen Sie im Dropdownmenü das Element **benutzerdefinierte Konnektoren** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-109">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

![Ein Screenshot des Dropdownmenüs in Microsoft Power Automation](./images/custom-connectors.png)

<span data-ttu-id="9aff3-111">Klicken Sie auf der Seite **benutzerdefinierte Connectors** auf den Link **neuer benutzerdefinierter Verbinder** in der oberen rechten Ecke, und wählen Sie dann im Dropdownmenü die Option **aus leeres Element erstellen aus** .</span><span class="sxs-lookup"><span data-stu-id="9aff3-111">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Create from blank** item in the drop-down menu.</span></span>

![Ein Screenshot des neuen Dropdownmenüs für benutzerdefinierte Connectors in Microsoft Power Automation](./images/new-connector.png)

<span data-ttu-id="9aff3-113">Geben Sie `MS Graph Batch Connector` in das Textfeld **Connector Name** ein.</span><span class="sxs-lookup"><span data-stu-id="9aff3-113">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="9aff3-114">Choose **Continue**.</span><span class="sxs-lookup"><span data-stu-id="9aff3-114">Choose **Continue**.</span></span>

<span data-ttu-id="9aff3-115">Füllen Sie auf der Seite Connector-Konfigurations **Allgemein** die Felder wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-115">On the connector configuration **General** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="9aff3-116">**Schema** : https</span><span class="sxs-lookup"><span data-stu-id="9aff3-116">**Scheme** : HTTPS</span></span>
- <span data-ttu-id="9aff3-117">**Host** : `graph.microsoft.com`</span><span class="sxs-lookup"><span data-stu-id="9aff3-117">**Host** : `graph.microsoft.com`</span></span>
- <span data-ttu-id="9aff3-118">**Basis-URL** : `/`</span><span class="sxs-lookup"><span data-stu-id="9aff3-118">**Base URL** : `/`</span></span>

<span data-ttu-id="9aff3-119">Klicken Sie auf **Sicherheits** Schaltfläche, um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="9aff3-119">Choose **Security** button to continue.</span></span>

![Ein Screenshot der Registerkarte "Allgemein" in der Connector-Konfiguration](./images/general-tab.png)

<span data-ttu-id="9aff3-121">Füllen Sie auf der Seite **Sicherheit** die Felder wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-121">On the **Security** page, fill in the fields as follows.</span></span>

- <span data-ttu-id="9aff3-122">**Wählen Sie aus, welche Authentifizierung von ihrer API implementiert wird** : `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="9aff3-122">**Choose what authentication is implemented by your API** : `OAuth 2.0`</span></span>
- <span data-ttu-id="9aff3-123">**Identitätsanbieter** : `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="9aff3-123">**Identity Provider** : `Azure Active Directory`</span></span>
- <span data-ttu-id="9aff3-124">**Client-ID** : die Anwendungs-ID, die Sie in der vorherigen Übung erstellt haben</span><span class="sxs-lookup"><span data-stu-id="9aff3-124">**Client id** : the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="9aff3-125">**Geheimer Client** Schlüssel: der Schlüssel, den Sie in der vorherigen Übung erstellt haben</span><span class="sxs-lookup"><span data-stu-id="9aff3-125">**Client secret** : the key you created in the previous exercise</span></span>
- <span data-ttu-id="9aff3-126">**Anmelde-URL** : `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="9aff3-126">**Login url** : `https://login.windows.net`</span></span>
- <span data-ttu-id="9aff3-127">**Mandanten-ID** : `common`</span><span class="sxs-lookup"><span data-stu-id="9aff3-127">**Tenant ID** : `common`</span></span>
- <span data-ttu-id="9aff3-128">**Ressourcen-URL** : `https://graph.microsoft.com` (kein Trailing/)</span><span class="sxs-lookup"><span data-stu-id="9aff3-128">**Resource URL** : `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="9aff3-129">**Bereich** : leer lassen</span><span class="sxs-lookup"><span data-stu-id="9aff3-129">**Scope** : Leave blank</span></span>

<span data-ttu-id="9aff3-130">Klicken Sie auf die Schaltfläche **Definition** , um fortzufahren.</span><span class="sxs-lookup"><span data-stu-id="9aff3-130">Choose **Definition** button to continue.</span></span>

![Ein Screenshot der Registerkarte "Sicherheit" in der Connector-Konfiguration](./images/security-tab.png)

<span data-ttu-id="9aff3-132">Wählen Sie auf der Seite **Definition** die Option **neue Aktion** aus, und füllen Sie die Felder wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-132">On the **Definition** page, select **New Action** and fill in the fields as follows.</span></span>

- <span data-ttu-id="9aff3-133">**Zusammenfassung** : `Batch`</span><span class="sxs-lookup"><span data-stu-id="9aff3-133">**Summary** : `Batch`</span></span>
- <span data-ttu-id="9aff3-134">**Beschreibung** : `Execute Batch with Delegate Permission`</span><span class="sxs-lookup"><span data-stu-id="9aff3-134">**Description** : `Execute Batch with Delegate Permission`</span></span>
- <span data-ttu-id="9aff3-135">**Vorgangs-ID** : `Batch`</span><span class="sxs-lookup"><span data-stu-id="9aff3-135">**Operation ID** : `Batch`</span></span>
- <span data-ttu-id="9aff3-136">**Sichtbarkeit** : `important`</span><span class="sxs-lookup"><span data-stu-id="9aff3-136">**Visibility** : `important`</span></span>

![Ein Screenshot der Registerkarte "Definition" in der Connector-Konfiguration](./images/definition-tab.png)

<span data-ttu-id="9aff3-138">Erstellen Sie eine **Anforderung** durch Auswählen von **Import aus Sample** und füllen Sie die Felder wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-138">Create **Request** by selecting **Import from Sample** and fill in the fields as follows.</span></span>

- <span data-ttu-id="9aff3-139">**Verb** : `POST`</span><span class="sxs-lookup"><span data-stu-id="9aff3-139">**Verb** : `POST`</span></span>
- <span data-ttu-id="9aff3-140">**URL** : `https://graph.microsoft.com/v1.0/$batch`</span><span class="sxs-lookup"><span data-stu-id="9aff3-140">**URL** : `https://graph.microsoft.com/v1.0/$batch`</span></span>
- <span data-ttu-id="9aff3-141">**Kopfzeilen** : leer lassen</span><span class="sxs-lookup"><span data-stu-id="9aff3-141">**Headers** : Leave blank</span></span>
- <span data-ttu-id="9aff3-142">**Body** : `{}`</span><span class="sxs-lookup"><span data-stu-id="9aff3-142">**Body** : `{}`</span></span>

<span data-ttu-id="9aff3-143">Wählen Sie **Importieren** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-143">Select **Import**.</span></span>

![Ein Screenshot des Dialogfelds "aus Beispiel importieren" in der Connector-Konfiguration](./images/import-sample.png)

<span data-ttu-id="9aff3-145">Wählen Sie oben rechts " **Connector erstellen** " aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-145">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="9aff3-146">Nachdem der Connector erstellt wurde, kopieren Sie die generierte **Umleitungs-URL** aus der **Sicherheits** Seite.</span><span class="sxs-lookup"><span data-stu-id="9aff3-146">After the connector has been created, copy the generated **Redirect URL** from **Security** page.</span></span>

![Ein Screenshot der generierten Umleitungs-URL](./images/redirect-url.png)

<span data-ttu-id="9aff3-148">Kehren Sie zur registrierten Anwendung im [Azure-Portal](https://aad.portal.azure.com) zurück, das Sie in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="9aff3-148">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="9aff3-149">Wählen Sie im Menü auf der linken Seite **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-149">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="9aff3-150">Wählen Sie **Plattform hinzufügen** aus, und wählen Sie dann **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-150">Select **Add a platform** , then select **Web**.</span></span> <span data-ttu-id="9aff3-151">Geben Sie die Umleitungs-URL, die aus dem vorherigen Schritt in den **Umleitungs-URIs** kopiert wurde, dann **configure** ein.</span><span class="sxs-lookup"><span data-stu-id="9aff3-151">Enter the redirect URL copied from the previous step in the **Redirect URIs** , then select **Configure**.</span></span>

![Ein Screenshot des Blatts "Antwort-URLs" im Azure-Portal](./images/update-app-reg.png)

## <a name="option-2-create-custom-connector-by-importing-openapi-file"></a><span data-ttu-id="9aff3-153">Option 2: Erstellen eines benutzerdefinierten Connectors durch Importieren der OpenAPI-Datei</span><span class="sxs-lookup"><span data-stu-id="9aff3-153">Option 2: Create custom connector by importing OpenAPI file</span></span>

<span data-ttu-id="9aff3-154">Erstellen Sie mithilfe eines Text-Editors eine neue leere Datei mit dem Namen, `MSGraph-Delegate-Batch.swagger.json` und fügen Sie den folgenden Code hinzu.</span><span class="sxs-lookup"><span data-stu-id="9aff3-154">Using a text editor, create a new empty file named `MSGraph-Delegate-Batch.swagger.json` and add the following code.</span></span>

[!code-json[](../LabFiles/MSGraph-Delegate-Batch.swagger.json)]

<span data-ttu-id="9aff3-155">Öffnen Sie einen Browser, und navigieren Sie zu [Microsoft Power Automation](https://flow.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="9aff3-155">Open a browser and navigate to [Microsoft Power Automate](https://flow.microsoft.com).</span></span> <span data-ttu-id="9aff3-156">Melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an.</span><span class="sxs-lookup"><span data-stu-id="9aff3-156">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="9aff3-157">Wählen Sie im linken Menü **Daten** aus, und wählen Sie im Dropdownmenü das Element **benutzerdefinierte Konnektoren** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-157">Choose **Data** on the left-hand side menu, and select the **Custom Connectors** item in the drop-down menu.</span></span>

<span data-ttu-id="9aff3-158">Klicken Sie auf der Seite **benutzerdefinierte Connectors** auf den Link **neuer benutzerdefinierter Verbinder** in der oberen rechten Ecke, und wählen Sie dann im Dropdownmenü das Element **OpenAPI-Datei importieren** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-158">On the **Custom Connectors** page choose the **New custom connector** link in the top right, then select the **Import an OpenAPI file** item in the drop-down menu.</span></span>

<span data-ttu-id="9aff3-159">Geben Sie `MS Graph Batch Connector` in das Textfeld **Connector Name** ein.</span><span class="sxs-lookup"><span data-stu-id="9aff3-159">Enter `MS Graph Batch Connector` in the **Connector name** text box.</span></span> <span data-ttu-id="9aff3-160">Wählen Sie das Ordnersymbol aus, um die OpenAPI-Datei hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="9aff3-160">Choose the folder icon to upload the OpenAPI file.</span></span> <span data-ttu-id="9aff3-161">Wechseln Sie zu der Datei, die `MSGraph-Delegate-Batch.swagger.json` Sie erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="9aff3-161">Browse to the `MSGraph-Delegate-Batch.swagger.json` file you created.</span></span> <span data-ttu-id="9aff3-162">Wählen Sie **weiter** aus, um die OpenAPI-Datei hochzuladen.</span><span class="sxs-lookup"><span data-stu-id="9aff3-162">Choose **Continue** to upload the OpenAPI file.</span></span>

<span data-ttu-id="9aff3-163">Klicken Sie auf der Seite Connector-Konfiguration im Navigationsmenü auf den Link **Sicherheit** .</span><span class="sxs-lookup"><span data-stu-id="9aff3-163">On the connector configuration page, choose the **Security** link in the navigation menu.</span></span> <span data-ttu-id="9aff3-164">Füllen Sie die Felder wie folgt aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-164">Fill in the fields as follows.</span></span>

- <span data-ttu-id="9aff3-165">**Wählen Sie aus, welche Authentifizierung von ihrer API implementiert wird** : `OAuth 2.0`</span><span class="sxs-lookup"><span data-stu-id="9aff3-165">**Choose what authentication is implemented by your API** : `OAuth 2.0`</span></span>
- <span data-ttu-id="9aff3-166">**Identitätsanbieter** : `Azure Active Directory`</span><span class="sxs-lookup"><span data-stu-id="9aff3-166">**Identity Provider** : `Azure Active Directory`</span></span>
- <span data-ttu-id="9aff3-167">**Client-ID** : die Anwendungs-ID, die Sie in der vorherigen Übung erstellt haben</span><span class="sxs-lookup"><span data-stu-id="9aff3-167">**Client id** : the application ID you created in the previous exercise</span></span>
- <span data-ttu-id="9aff3-168">**Geheimer Client** Schlüssel: der Schlüssel, den Sie in der vorherigen Übung erstellt haben</span><span class="sxs-lookup"><span data-stu-id="9aff3-168">**Client secret** : the key you created in the previous exercise</span></span>
- <span data-ttu-id="9aff3-169">**Anmelde-URL** : `https://login.windows.net`</span><span class="sxs-lookup"><span data-stu-id="9aff3-169">**Login url** : `https://login.windows.net`</span></span>
- <span data-ttu-id="9aff3-170">**Mandanten-ID** : `common`</span><span class="sxs-lookup"><span data-stu-id="9aff3-170">**Tenant ID** : `common`</span></span>
- <span data-ttu-id="9aff3-171">**Ressourcen-URL** : `https://graph.microsoft.com` (kein Trailing/)</span><span class="sxs-lookup"><span data-stu-id="9aff3-171">**Resource URL** : `https://graph.microsoft.com` (no trailing /)</span></span>
- <span data-ttu-id="9aff3-172">**Bereich** : leer lassen</span><span class="sxs-lookup"><span data-stu-id="9aff3-172">**Scope** : Leave blank</span></span>

<span data-ttu-id="9aff3-173">Wählen Sie oben rechts " **Connector erstellen** " aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-173">Choose **Create Connector** on the top-right.</span></span> <span data-ttu-id="9aff3-174">Nachdem der Connector erstellt wurde, kopieren Sie die generierte **Umleitungs-URL**.</span><span class="sxs-lookup"><span data-stu-id="9aff3-174">After the connector has been created, copy the generated **Redirect URL**.</span></span>

![Ein Screenshot der generierten Umleitungs-URL](./images/redirect-url.png)

<span data-ttu-id="9aff3-176">Kehren Sie zur registrierten Anwendung im [Azure-Portal](https://aad.portal.azure.com) zurück, das Sie in der vorherigen Übung erstellt haben.</span><span class="sxs-lookup"><span data-stu-id="9aff3-176">Go back to the registered application in the [Azure Portal](https://aad.portal.azure.com) you created in the previous exercise.</span></span> <span data-ttu-id="9aff3-177">Wählen Sie im Menü auf der linken Seite **Authentifizierung** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-177">Select **Authentication** on the left-hand side menu.</span></span> <span data-ttu-id="9aff3-178">Wählen Sie **Plattform hinzufügen** aus, und wählen Sie dann **Web** aus.</span><span class="sxs-lookup"><span data-stu-id="9aff3-178">Select **Add a platform** , then select **Web**.</span></span> <span data-ttu-id="9aff3-179">Geben Sie die Umleitungs-URL, die aus dem vorherigen Schritt in den **Umleitungs-URIs** kopiert wurde, dann **configure** ein.</span><span class="sxs-lookup"><span data-stu-id="9aff3-179">Enter the redirect URL copied from the previous step in the **Redirect URIs** , then select **Configure**.</span></span>

![Ein Screenshot des Blatts "Antwort-URLs" im Azure-Portal](./images/update-app-reg.png)
