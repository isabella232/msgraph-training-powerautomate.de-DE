---
ms.openlocfilehash: e05217bc33d1cce8bc86ad56a8bd43c4f6b4ef2a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829725"
---
<!-- markdownlint-disable MD002 MD041 -->

Bevor Sie einen Fluss für die Nutzung des neuen Connectors erstellen, können Sie mit dem [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer) einige Funktionen und Features der JSON-Batchverarbeitung in Microsoft Graph ermitteln.

Öffnen Sie den [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer) in Ihrem Browser. Melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an. Suchen Sie in den **Beispielabfragen** nach **Batch** .

Wählen Sie im linken Menü die Beispielabfrage " **paralleles abrufen durchführen** " aus. Klicken Sie oben rechts auf dem Bildschirm auf die Schaltfläche **Abfrage ausführen** .

![Ein Screenshot der Registerkarte "Sample Abfragen" im Graph-Explorer](./images/sample-queries.png)

Der Beispiel Batchvorgang Batches drei HTTP GET-Anforderungen und gibt einen einzelnen http-Beitrag an den `/v1.0/$batch` Graph-Endpunkt aus.

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

Die zurückgegebene Antwort wird unten angezeigt. Beachten Sie das Array von Antworten, die von Microsoft Graph zurückgegeben werden. Die Antworten auf die Batchanforderungen werden möglicherweise in einer anderen Reihenfolge angezeigt als die Reihenfolge der Anforderungen im Beitrag. Die `id` -Eigenschaft sollte verwendet werden, um einzelne Batchanforderungen mit bestimmten Batch Antworten zu korrelieren.

> [!NOTE]
> Die Antwort wurde zur Lesbarkeit gekürzt.

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

Jede Antwort enthält eine `id` , `status` , `headers` und `body` -Eigenschaft. Wenn die `status` Eigenschaft für eine Anforderung einen Fehler angibt, `body` enthält die von der Anforderung zurückgegebene Fehlerinformationen.

Um eine Reihenfolge der Vorgänge für die Anforderungen sicherzustellen, können einzelne Anforderungen mithilfe der [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) -Eigenschaft sequenziert werden.

Zusätzlich zu Sequenzierung und Abhängigkeits Vorgängen nimmt die JSON-Batchverarbeitung einen Basis Pfad an und führt die Anforderungen von einem relativen Pfad aus. Jedes Batch Anforderungselement wird entweder von den `/v1.0/$batch` oder `/beta/$batch` -Endpunkten ausgeführt, wie angegeben. Dies kann erhebliche Unterschiede aufweisen, da der `/beta` Endpunkt möglicherweise zusätzliche Ausgaben zurückgibt, die möglicherweise nicht im Endpunkt zurückgegeben werden `/v1.0` .

Führen Sie beispielsweise die folgenden zwei Abfragen im [Microsoft Graph-Explorer](https://developer.microsoft.com/graph/graph-explorer)aus.

1. Abfragen des `/v1.0/$batch` Endpunkts mithilfe der URL `/me` (Copy-und Paste-Anforderung unten).

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

Verwenden Sie nun die Dropdownliste Versionsauswahl, um zum Endpunkt zu wechseln `beta` , und führen Sie genau die gleiche Anforderung aus.

![Graph-Explore-4](./images/batch-beta.png)

Was sind die Unterschiede der zurückgegebenen Ergebnisse? Versuchen Sie einige andere Abfragen, um einige der Unterschiede zu identifizieren.

Neben unterschiedlichen Antwort Inhalten aus den `/v1.0` und- `/beta` Endpunkten ist es wichtig, die möglichen Fehler zu verstehen, wenn eine Batchanforderung erstellt wird, für die keine Zustimmung erteilt wurde. Im folgenden finden Sie beispielsweise ein Batch Anforderungselement zum Erstellen eines OneNote-Notizbuchs.

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

Wenn jedoch die Berechtigungen zum Erstellen von OneNote-Notizbüchern nicht erteilt wurden, wird die folgende Antwort empfangen. Hinweis der Statuscode `403 (Forbidden)` und die Fehlermeldung, die angibt, dass das angegebene OAuth-Token nicht die zum Abschließen der angeforderten Aktion erforderlichen Bereiche enthält.

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

Jede Anforderung in Ihrem Batch gibt einen Statuscode und Ergebnisse oder Fehlerinformationen zurück. Sie müssen jede der Antworten verarbeiten, um den Erfolg oder Misserfolg der einzelnen Batchvorgänge zu ermitteln.
