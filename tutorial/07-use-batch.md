---
ms.openlocfilehash: 2d9b6e29a5ddc71b8f7b78b1e2fe035a8fdbddac
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829792"
---
<!-- markdownlint-disable MD002 MD041 -->

Der in der vorherigen Übung erstellte Fluss verwendet die `$batch` API, um zwei einzelne Anforderungen an Microsoft Graph zu stellen. Das Aufrufen des `$batch` Endpunkts auf diese Weise bietet einige Vorteile und Flexibilität, aber die wahre Leistung des `$batch` Endpunkts wird bei der Ausführung mehrerer Anforderungen an Microsoft Graph in einem einzigen `$batch` Aufruf erfüllt. In dieser Übung erweitern Sie das Beispiel zum Erstellen einer einheitlichen Gruppe und zum Verknüpfen eines Teams mit dem Erstellen mehrerer Standardkanäle für das Team in einer einzigen `$batch` Anforderung.

Öffnen Sie [Microsoft Power Automation](https://flow.microsoft.com) in Ihrem Browser, und melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an. Wählen Sie den Fluss aus, den Sie im vorherigen Schritt erstellt haben, und klicken Sie dann auf **Bearbeiten**.

Wählen Sie **neuer Schritt** aus, und geben Sie `Batch` das Suchfeld ein. Fügen Sie die **MS Graph Batch Connector** -Aktion hinzu. Wählen Sie die Auslassungspunkte aus, und benennen Sie diese Aktion um `Batch POST-channels` .

Fügen **Sie den folgenden Code in das Feld** Text der Aktion ein.

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Marketing Collateral",
        "description": "Marketing collateral and documentation."
      }
    },
    {
      "id": 2,
      "dependsOn": [
        "1"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "Vendor Contracts",
        "description": "Vendor documents, contracts, agreements and schedules."
      }
    },
    {
      "id": 3,
      "dependsOn": [
        "2"
      ],
      "url": "/teams/REPLACE/channels",
      "headers": {
        "Content-Type": "application/json"
      },
      "method": "POST",
      "body": {
        "displayName": "General Client Agreements",
        "description": "General Client documents and agreements."
      }
    }
  ]
}
```

Beachten Sie, dass die drei obigen Anforderungen die [dependsOn](https://docs.microsoft.com/graph/json-batching#sequencing-requests-with-the-dependson-property) -Eigenschaft verwenden, um eine Sequenzreihenfolge anzugeben, und jeder wird eine Post-Anforderung ausführen, um einen neuen Kanal im neuen Team zu erstellen.

Wählen Sie jede Instanz des `REPLACE` Platzhalters aus, und wählen Sie dann im Bereich dynamischer Inhalt den **Begriff Ausdruck** aus. Fügen Sie die folgende Formel in den **Ausdruck** ein.

```js
body('Batch_PUT-team').responses[0].body.id
```

![Ein Screenshot des Ausdrucks im Bereich "dynamischer Inhalt"](./images/dynamic-expression.png)

Wählen Sie **Speichern** aus, und wählen Sie dann **Test** aus, um den Fluss auszuführen. Aktivieren Sie das Optionsfeld **Ich werde das Auslösen der Aktion ausführen** , und wählen Sie dann **& Test speichern** aus. Geben Sie einen eindeutigen Gruppennamen in das Feld **Name** ohne Leerzeichen ein, und wählen Sie **Run Flow** aus, um den Fluss auszuführen.

Nachdem der Fluss gestartet wurde, klicken Sie auf die Schaltfläche **Fertig** , um das Aktivitätsprotokoll anzuzeigen. Wenn der Fluss abgeschlossen ist, hat die endgültige Ausgabe für die `Batch POST-channels` Aktion eine 201-HTTP-Status Antwort für jeden erstellten Kanal.

![Ein Screenshot des erfolgreichen Ablauf Aktivitätsprotokolls](./images/batch-success.png)

Wechseln Sie zu [Microsoft Teams](https://teams.microsoft.com) , und melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an. Stellen Sie sicher, dass das soeben erstellte Team angezeigt wird und die drei von der Anforderung erstellten Kanäle enthält `$batch` .

![Ein Screenshot der Teams-App mit dem neuen Team und den Kanälen, die angezeigt werden](./images/team-channels.png)

Während die obige `Batch POST-channels` Aktion in diesem Lernprogramm als separate Aktion implementiert wurde, konnten die Aufrufe zum Erstellen der Kanäle als zusätzliche Aufrufe in der Aktion hinzugefügt werden `Batch PUT-team` . Dadurch hätte das Team und alle Kanäle in einem einzigen Batch Aufruf erstellt. Geben Sie dies auf eigene Faust.

Denken Sie schließlich daran, dass [JSON-Batch](https://docs.microsoft.com/graph/json-batching) Aufrufe einen HTTP-Statuscode für jede Anforderung zurückgeben. In einem Produktionsprozess empfiehlt es sich, die Nachbearbeitung der Ergebnisse mit einer Aktion zu kombinieren [`Apply to each`](https://docs.microsoft.com/power-automate/apply-to-each) und jede einzelne Antwort mit einem 201-Statuscode zu validieren oder andere erhaltene Statuscodes zu kompensieren.
