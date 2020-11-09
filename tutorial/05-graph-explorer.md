---
ms.openlocfilehash: e05217bc33d1cce8bc86ad56a8bd43c4f6b4ef2a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829725"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="6cf30-101">Bevor Sie einen Fluss für die Nutzung des neuen Connectors erstellen, können Sie mit dem [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer) einige Funktionen und Features der JSON-Batchverarbeitung in Microsoft Graph ermitteln.</span><span class="sxs-lookup"><span data-stu-id="6cf30-101">Before creating a Flow to consume the new connector, use [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to discover some of the capabilities and features of JSON batching in Microsoft Graph.</span></span>

<span data-ttu-id="6cf30-102">Öffnen Sie den [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer) in Ihrem Browser.</span><span class="sxs-lookup"><span data-stu-id="6cf30-102">Open the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) in your browser.</span></span> <span data-ttu-id="6cf30-103">Melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an.</span><span class="sxs-lookup"><span data-stu-id="6cf30-103">Sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="6cf30-104">Suchen Sie in den **Beispielabfragen** nach **Batch** .</span><span class="sxs-lookup"><span data-stu-id="6cf30-104">Search for for **Batch** from the **Sample queries**.</span></span>

<span data-ttu-id="6cf30-105">Wählen Sie im linken Menü die Beispielabfrage " **paralleles abrufen durchführen** " aus.</span><span class="sxs-lookup"><span data-stu-id="6cf30-105">Select the **Perform parallel GETs** sample query in the left menu.</span></span> <span data-ttu-id="6cf30-106">Klicken Sie oben rechts auf dem Bildschirm auf die Schaltfläche **Abfrage ausführen** .</span><span class="sxs-lookup"><span data-stu-id="6cf30-106">Choose the **Run Query** button at the top right of the screen.</span></span>

![Ein Screenshot der Registerkarte "Sample Abfragen" im Graph-Explorer](./images/sample-queries.png)

<span data-ttu-id="6cf30-108">Der Beispiel Batchvorgang Batches drei HTTP GET-Anforderungen und gibt einen einzelnen http-Beitrag an den `/v1.0/$batch` Graph-Endpunkt aus.</span><span class="sxs-lookup"><span data-stu-id="6cf30-108">The sample batch operation batches three HTTP GET requests and issues a single HTTP POST to the `/v1.0/$batch` Graph endpoint.</span></span>

```json
{
    "requests": [
        {
            "url": "/me?$select=displayName,jobTitle,userPrincipalName",
            "method": "GET",
            "id": "1"
        },
        {
            "url": "/me/messages?$filter=importance eq 'high'&$select=from,subject,receivedDateTime,bodyPreview",
            "method": "GET",
            "id": "2"
        },
        {
            "url": "/me/events",
            "method": "GET",
            "id": "3"
        }
    ]
}
```

<span data-ttu-id="6cf30-109">Die zurückgegebene Antwort wird unten angezeigt.</span><span class="sxs-lookup"><span data-stu-id="6cf30-109">The response returned is shown below.</span></span> <span data-ttu-id="6cf30-110">Beachten Sie das Array von Antworten, die von Microsoft Graph zurückgegeben werden.</span><span class="sxs-lookup"><span data-stu-id="6cf30-110">Note the array of responses that is returned by Microsoft Graph.</span></span> <span data-ttu-id="6cf30-111">Die Antworten auf die Batchanforderungen werden möglicherweise in einer anderen Reihenfolge angezeigt als die Reihenfolge der Anforderungen im Beitrag.</span><span class="sxs-lookup"><span data-stu-id="6cf30-111">The responses to the batched requests may appear in a different order than the order of the requests in the POST.</span></span> <span data-ttu-id="6cf30-112">Die `id` -Eigenschaft sollte verwendet werden, um einzelne Batchanforderungen mit bestimmten Batch Antworten zu korrelieren.</span><span class="sxs-lookup"><span data-stu-id="6cf30-112">The `id` property should be used to correlate individual batch requests with specific batch responses.</span></span>

> [!NOTE]
> <span data-ttu-id="6cf30-113">Die Antwort wurde zur Lesbarkeit gekürzt.</span><span class="sxs-lookup"><span data-stu-id="6cf30-113">The response has been truncated for readability.</span></span>

```json
{
  "responses": [
    {
      "id": "1",
      "status": 200,
      "headers": {...},
      "body": {...}
    },
    {
      "id": "3",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
    {
      "id": "2",
      "status": 200,
      "headers": {...},
      "body": {...}
    }
  ]
}
```

<span data-ttu-id="6cf30-114">Jede Antwort enthält eine `id` , `status` , `headers` und `body` -Eigenschaft.</span><span class="sxs-lookup"><span data-stu-id="6cf30-114">Each response contains an `id`, `status`, `headers`, and `body` property.</span></span> <span data-ttu-id="6cf30-115">Wenn die `status` Eigenschaft für eine Anforderung einen Fehler angibt, `body` enthält die von der Anforderung zurückgegebene Fehlerinformationen.</span><span class="sxs-lookup"><span data-stu-id="6cf30-115">If the `status` property for a request indicates a failure, the `body` contains any error information returned from the request.</span></span>

<span data-ttu-id="6cf30-116">Um eine Reihenfolge der Vorgänge für die Anforderungen sicherzustellen, können einzelne Anforderungen mithilfe der [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) -Eigenschaft sequenziert werden.</span><span class="sxs-lookup"><span data-stu-id="6cf30-116">To ensure an order of operations for the requests, individual requests can be sequenced using the [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) property.</span></span>

<span data-ttu-id="6cf30-117">Zusätzlich zu Sequenzierung und Abhängigkeits Vorgängen nimmt die JSON-Batchverarbeitung einen Basis Pfad an und führt die Anforderungen von einem relativen Pfad aus.</span><span class="sxs-lookup"><span data-stu-id="6cf30-117">In addition to sequencing and dependency operations, JSON batching assumes a base path and executes the requests from a relative path.</span></span> <span data-ttu-id="6cf30-118">Jedes Batch Anforderungselement wird entweder von den `/v1.0/$batch` oder `/beta/$batch` -Endpunkten ausgeführt, wie angegeben.</span><span class="sxs-lookup"><span data-stu-id="6cf30-118">Each batch request element is executed from either the `/v1.0/$batch` OR `/beta/$batch` endpoints as specified.</span></span> <span data-ttu-id="6cf30-119">Dies kann erhebliche Unterschiede aufweisen, da der `/beta` Endpunkt möglicherweise zusätzliche Ausgaben zurückgibt, die möglicherweise nicht im Endpunkt zurückgegeben werden `/v1.0` .</span><span class="sxs-lookup"><span data-stu-id="6cf30-119">This can have significant differences as the `/beta` endpoint may return additional output which may NOT be returned in the `/v1.0` endpoint.</span></span>

<span data-ttu-id="6cf30-120">Führen Sie beispielsweise die folgenden zwei Abfragen im [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer)aus.</span><span class="sxs-lookup"><span data-stu-id="6cf30-120">For example, execute the following two queries in the [Microsoft Graph Explorer](https://developer.microsoft.com/graph/graph-explorer).</span></span>

1. <span data-ttu-id="6cf30-121">Abfragen des `/v1.0/$batch` Endpunkts mithilfe der URL `/me` (Copy-und Paste-Anforderung unten).</span><span class="sxs-lookup"><span data-stu-id="6cf30-121">Query the `/v1.0/$batch` endpoint using the url `/me` (copy and paste request below).</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/me",
      "method": "GET"
    }
  ]
}
```

![Ein Screenshot der Batchabfrage im Graph-Explorer mit ausgewähltem v 1.0](./images/batch-v1.png)

<span data-ttu-id="6cf30-123">Verwenden Sie nun die Dropdownliste Versionsauswahl, um zum Endpunkt zu wechseln `beta` , und führen Sie genau die gleiche Anforderung aus.</span><span class="sxs-lookup"><span data-stu-id="6cf30-123">Now use the version selector drop-down to change to the `beta` endpoint, and make the exact same request.</span></span>

![Graph-Explore-4](./images/batch-beta.png)

<span data-ttu-id="6cf30-125">Was sind die Unterschiede der zurückgegebenen Ergebnisse?</span><span class="sxs-lookup"><span data-stu-id="6cf30-125">What are the differences in the results returned?</span></span> <span data-ttu-id="6cf30-126">Versuchen Sie einige andere Abfragen, um einige der Unterschiede zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="6cf30-126">Try some other queries to identify some of the differences.</span></span>

<span data-ttu-id="6cf30-127">Neben unterschiedlichen Antwort Inhalten aus den `/v1.0` und- `/beta` Endpunkten ist es wichtig, die möglichen Fehler zu verstehen, wenn eine Batchanforderung erstellt wird, für die keine Zustimmung erteilt wurde.</span><span class="sxs-lookup"><span data-stu-id="6cf30-127">In addition to different response content from the `/v1.0` and `/beta` endpoints, it is important to understand the possible errors when a batch request is made for which permission consent has not been granted.</span></span> <span data-ttu-id="6cf30-128">Im folgenden finden Sie beispielsweise ein Batch Anforderungselement zum Erstellen eines OneNote-Notizbuchs.</span><span class="sxs-lookup"><span data-stu-id="6cf30-128">For example, the following is a batch request item to create a OneNote Notebook.</span></span>

```json
{
  "id": 1,
  "url": "/groups/65c5ecf9-3311-449c-9904-29a2c76b9a50/onenote/notebooks",
  "headers": {
    "Content-Type": "application/json"
  },
  "method": "POST",
  "body": {
    "displayName": "Meeting Notes"
  }
}
```

<span data-ttu-id="6cf30-129">Wenn jedoch die Berechtigungen zum Erstellen von OneNote-Notizbüchern nicht erteilt wurden, wird die folgende Antwort empfangen.</span><span class="sxs-lookup"><span data-stu-id="6cf30-129">However, if the permissions to create OneNote Notebooks has not been granted, the following response is received.</span></span> <span data-ttu-id="6cf30-130">Hinweis der Statuscode `403 (Forbidden)` und die Fehlermeldung, die angibt, dass das angegebene OAuth-Token nicht die zum Abschließen der angeforderten Aktion erforderlichen Bereiche enthält.</span><span class="sxs-lookup"><span data-stu-id="6cf30-130">Note the status code `403 (Forbidden)` and the error message which indicates the OAuth token provided does not include the scopes required to completed the requested action.</span></span>

```json
{
  "responses": [
    {
      "id": "1",
      "status": 403,
      "headers": {
        "Cache-Control": "no-cache"
      },
      "body": {
        "error": {
          "code": "40004",
          "message": "The OAuth token provided does not have the necessary scopes to complete the request.
            Please make sure you are including one or more of the following scopes: Notes.ReadWrite.All,
            Notes.Read.All (you provided these scopes: Group.Read.All,Group.ReadWrite.All,User.Read,User.Read.All)",
          "innerError": {
            "request-id": "92d50317-aa06-4bd7-b908-c85ee4eff0e9",
            "date": "2018-10-17T02:01:10"
          }
        }
      }
    }
  ]
}
```

<span data-ttu-id="6cf30-131">Jede Anforderung in Ihrem Batch gibt einen Statuscode und Ergebnisse oder Fehlerinformationen zurück.</span><span class="sxs-lookup"><span data-stu-id="6cf30-131">Each request in your batch will return a status code and results or error information.</span></span> <span data-ttu-id="6cf30-132">Sie müssen jede der Antworten verarbeiten, um den Erfolg oder Misserfolg der einzelnen Batchvorgänge zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="6cf30-132">You must process each of the responses in order to determine success or failure of the individual batch operations.</span></span>
