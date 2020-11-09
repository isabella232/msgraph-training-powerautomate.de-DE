---
ms.openlocfilehash: 22c9c7ddd8513d857d96ade608e4b2e4e809dc41
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829768"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="cd609-101">In dieser Übung erstellen Sie eine neue Azure Active Directory-Anwendung, die verwendet wird, um die Delegierten Berechtigungen für den benutzerdefinierten Connector bereitzustellen.</span><span class="sxs-lookup"><span data-stu-id="cd609-101">In this exercise, you will create a new Azure Active Directory Application which will be used to provide the delegated permissions for the custom connector.</span></span>

<span data-ttu-id="cd609-102">Öffnen Sie einen Browser, und navigieren Sie zu [Azure Active Directory Admin Center](https://aad.portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cd609-102">Open a browser and navigate to [Azure Active Directory admin center](https://aad.portal.azure.com).</span></span> <span data-ttu-id="cd609-103">Klicken Sie im linken Navigationsmenü auf den Link **Azure Active Directory** , und wählen Sie dann den Eintrag **App-Registrierungen** im Abschnitt **Manage** des **Azure Active Directory** Blade aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-103">Choose the **Azure Active Directory** link in the left navigation menu, then choose the **App registrations** entry in the **Manage** section of the **Azure Active Directory** blade.</span></span>

![Ein Screenshot des Azure Active Directory Blade im Azure Active Directory Admin Center](./images/app-registrations.png)

<span data-ttu-id="cd609-105">Wählen Sie das **neue Registrierungs** Menüelement oben auf dem Blatt **App-Registrierungen** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-105">Choose the **New registration** menu item at the top of the **App Registrations** blade.</span></span>

![Ein Screenshot des Blatts "App-Registrierungen" im Azure Active Directory Admin Center](./images/new-registration.png)

<span data-ttu-id="cd609-107">Geben Sie `MS Graph Batch App` in das Feld **Name** ein.</span><span class="sxs-lookup"><span data-stu-id="cd609-107">Enter `MS Graph Batch App` in the **Name** field.</span></span> <span data-ttu-id="cd609-108">Wählen Sie im Abschnitt **unterstützte Kontotypen** die Option **Konten in einem beliebigen Organisations Verzeichnis** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-108">In the **Supported account types** section, select **Accounts in any organizational directory**.</span></span> <span data-ttu-id="cd609-109">Lassen Sie den Abschnitt **Umleitungs-URI** leer, und wählen Sie **registrieren** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-109">Leave the **Redirect URI** section blank and choose **Register**.</span></span>

![Ein Screenshot des Registers eines Anwendungs Blatts im Azure Active Directory Admin Center](./images/register-an-app.png)

<span data-ttu-id="cd609-111">Kopieren Sie auf dem Blatt **MS Graph-Batch-App** die **Anwendungs-ID (Client)**.</span><span class="sxs-lookup"><span data-stu-id="cd609-111">On the **MS Graph Batch App** blade, copy the **Application (client) ID**.</span></span> <span data-ttu-id="cd609-112">Sie benötigen diese in der nächsten Übung.</span><span class="sxs-lookup"><span data-stu-id="cd609-112">You'll need this in the next exercise.</span></span>

![Ein Screenshot der registrierten Anwendungsseite](./images/app-id.png)

<span data-ttu-id="cd609-114">Wählen Sie den Eintrag **API-Berechtigungen** im Abschnitt **Verwalten** des **MS Graph-Batch-App** -Blades aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-114">Choose the **API permissions** entry in the **Manage** section of the **MS Graph Batch App** blade.</span></span> <span data-ttu-id="cd609-115">Wählen Sie **Hinzufügen einer Berechtigung** unter **API-Berechtigungen** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-115">Choose **Add a permission** under **API permissions**.</span></span>

![Ein Screenshot des API-Berechtigungs Blatts](./images/api-permissions.png)

<span data-ttu-id="cd609-117">Wählen Sie im Blade **API-Berechtigungen anfordern** die Option **Microsoft Graph** und dann **Delegierte Berechtigungen** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-117">In the **Request API permissions** blade, choose the **Microsoft Graph** , then choose **Delegated permissions**.</span></span> <span data-ttu-id="cd609-118">Suchen `group` Sie nach, und wählen Sie dann die Delegierte Berechtigung **alle Gruppen lesen und schreiben** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-118">Search for `group`, then select the **Read and write all groups** delegated permission.</span></span> <span data-ttu-id="cd609-119">Klicken Sie unten im Blade auf **Berechtigungen hinzufügen** .</span><span class="sxs-lookup"><span data-stu-id="cd609-119">Choose **Add permissions** at the bottom of the blade.</span></span>

 ![Ein Screenshot des Blades für Anforderungs-API-Berechtigungen](./images/select-permissions.png)

<span data-ttu-id="cd609-121">Wählen Sie den Eintrag **Zertifikate und Geheimnisse** im Abschnitt **Verwalten** des **MS Graph-Batch-App** -Blades aus, und wählen Sie dann **neuer geheimer Client Schlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-121">Choose the **Certificates and secrets** entry in the **Manage** section of the **MS Graph Batch App** blade, then choose **New client secret**.</span></span> <span data-ttu-id="cd609-122">Geben Sie `forever` in die **Beschreibung** ein, und wählen Sie **nie** unter **Expires** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-122">Enter `forever` in the **Description** and select **Never** under **Expires**.</span></span> <span data-ttu-id="cd609-123">Wählen Sie **Hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="cd609-123">Choose **Add**.</span></span>

![Ein Screenshot des Blatts "Zertifikat und Geheimnisse"](./images/create-client-secret.png)

<span data-ttu-id="cd609-125">Kopieren Sie den Wert für den neuen geheimen Schlüssel.</span><span class="sxs-lookup"><span data-stu-id="cd609-125">Copy the value for the new secret.</span></span> <span data-ttu-id="cd609-126">Sie benötigen diese in der nächsten Übung.</span><span class="sxs-lookup"><span data-stu-id="cd609-126">You'll need this in the next exercise.</span></span>

![Ein Screenshot des neuen geheimen Client Schlüssels](./images/copy-client-secret.png)

> [!IMPORTANT]
> <span data-ttu-id="cd609-128">Dieser Schritt ist wichtig, da auf den geheimen Zugriff nach dem Schließen dieses Blades nicht zugegriffen werden kann.</span><span class="sxs-lookup"><span data-stu-id="cd609-128">This step is critical as the secret will not be accessible once you close this blade.</span></span> <span data-ttu-id="cd609-129">Speichern Sie diesen Schlüssel in einem Text-Editor zur Verwendung in bevorstehenden Übungen.</span><span class="sxs-lookup"><span data-stu-id="cd609-129">Save this secret to a text editor for use in upcoming exercises.</span></span>

<span data-ttu-id="cd609-130">Um die Verwaltung zusätzlicher Dienste zu ermöglichen, die über Microsoft Graph zugänglich sind, einschließlich der Teams-Eigenschaften, müssen Sie zusätzliche, geeignete Bereiche auswählen, um die Verwaltung bestimmter Dienste zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="cd609-130">To enable management of additional services accessible via the Microsoft Graph, including Teams properties, you would need to select additional, appropriate scopes to enable managing specific services.</span></span> <span data-ttu-id="cd609-131">Um beispielsweise unsere Lösung so zu erweitern, dass OneNote-Notizbücher oder Planner-Pläne, Buckets und Aufgaben erstellt werden, müssen Sie die erforderlichen Berechtigungs Bereiche für die entsprechenden APIs hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="cd609-131">For example, to extend our solution to enable creating OneNote Notebooks or Planner plans, buckets and tasks you would need to add the required permission scopes for the relevant APIs.</span></span>
