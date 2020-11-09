---
ms.openlocfilehash: 1674fb94e1749ad15f8f33f0865ce468f889232a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829835"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="e561b-101">In dieser Übung erstellen Sie einen Fluss für die Verwendung des benutzerdefinierten Konnektors, den Sie in den vorherigen Übungen erstellt haben, um ein Microsoft-Team zu erstellen und zu konfigurieren.</span><span class="sxs-lookup"><span data-stu-id="e561b-101">In this exercise, you will create a flow to use the custom connector you created in previous exercises to create and configure a Microsoft Team.</span></span> <span data-ttu-id="e561b-102">Der Fluss verwendet den benutzerdefinierten Connector zum Senden einer POST-Anforderung, um eine Office 365 Unified Group zu erstellen, wird für eine Verzögerung angehalten, während die Gruppenerstellung abgeschlossen wird, und sendet dann eine PUT-Anforderung, um die Gruppe einem Microsoft-Team zuzuordnen.</span><span class="sxs-lookup"><span data-stu-id="e561b-102">The flow will use the custom connector to send a POST request to create an Office 365 Unified Group, will pause for a delay while the group creation completes, and then will send a PUT request to associate the group with a Microsoft Team.</span></span>

<span data-ttu-id="e561b-103">Am Ende sieht der Fluss ähnlich wie in der folgenden Abbildung aus:</span><span class="sxs-lookup"><span data-stu-id="e561b-103">In the end your flow will look similar to the following image:</span></span>

![Ein Screenshot des abgeschlossenen Flusses](./images/completed-flow.png)

<span data-ttu-id="e561b-105">Öffnen Sie [Microsoft Power Automation](https://flow.microsoft.com) in Ihrem Browser, und melden Sie sich mit Ihrem Office 365 mandantenadministrator Konto an.</span><span class="sxs-lookup"><span data-stu-id="e561b-105">Open [Microsoft Power Automate](https://flow.microsoft.com) in your browser and sign in with your Office 365 tenant administrator account.</span></span> <span data-ttu-id="e561b-106">Wählen Sie **meine Flows** in der linken Navigationsleiste aus.</span><span class="sxs-lookup"><span data-stu-id="e561b-106">Choose **My flows** in the left-hand navigation.</span></span> <span data-ttu-id="e561b-107">Wählen Sie **neu** und dann **sofort--von leer aus**.</span><span class="sxs-lookup"><span data-stu-id="e561b-107">Choose **New** , then **Instant--from blank**.</span></span> <span data-ttu-id="e561b-108">Geben Sie `Create Team` für den **Flussnamen** ein, und wählen Sie dann unter Wählen Sie aus **, wie dieser Fluss ausgelöst** wird **einen Fluss manuell auslösen** aus.</span><span class="sxs-lookup"><span data-stu-id="e561b-108">Enter `Create Team` for **Flow name** , then select **Manually trigger a flow** under **Choose how to trigger this flow**.</span></span> <span data-ttu-id="e561b-109">Klicken Sie auf **Erstellen**.</span><span class="sxs-lookup"><span data-stu-id="e561b-109">Choose **Create**.</span></span>

<span data-ttu-id="e561b-110">Wählen Sie das **manuelle Auslösen eines Fluss** Elements aus, wählen Sie dann **Eingabe hinzufügen** aus, wählen Sie **Text** aus, und geben Sie `Name` als Titel ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-110">Select the **Manually trigger a flow** item, then choose **Add an input** , select **Text** and enter `Name` as the title.</span></span>

![Ein Screenshot des manuellen Triggers eines Fluss Auslösers](./images/manually-trigger.png)

<span data-ttu-id="e561b-112">Wählen Sie **neuer Schritt** aus, und geben Sie `Batch` das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-112">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="e561b-113">Fügen Sie die **MS Graph Batch Connector** -Aktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="e561b-113">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="e561b-114">Wählen Sie die Auslassungspunkte aus, und benennen Sie diese Aktion um `Batch POST-groups` .</span><span class="sxs-lookup"><span data-stu-id="e561b-114">Choose the ellipsis and rename this action to `Batch POST-groups`.</span></span>

<span data-ttu-id="e561b-115">Fügen **Sie den folgenden Code in das Feld** Text der Aktion ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-115">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "url": "/groups",
      "method": "POST",
      "id": 1,
      "headers": { "Content-Type": "application/json" },
      "body": {
        "description": "REPLACE",
        "displayName": "REPLACE",
        "groupTypes": ["Unified"],
        "mailEnabled": true,
        "mailNickname": "REPLACE",
        "securityEnabled": false
      }
    }
  ]
}
```

<span data-ttu-id="e561b-116">Ersetzen Sie die einzelnen `REPLACE` Platzhalter durch Auswählen des `Name` Werts aus dem manuellen Auslöser aus dem Menü **dynamischer Inhalt hinzufügen** .</span><span class="sxs-lookup"><span data-stu-id="e561b-116">Replace each `REPLACE` placeholder by selecting the `Name` value from the manual trigger from the **Add dynamic content** menu.</span></span>

![Ein Screenshot des Menüs für dynamische Inhalte in Microsoft Flow](./images/dynamic-content.png)

<span data-ttu-id="e561b-118">Wählen Sie **neuer Schritt** aus, suchen Sie nach `delay` einer **Verzögerungs** Aktion, und konfigurieren Sie Sie für 1 Minute.</span><span class="sxs-lookup"><span data-stu-id="e561b-118">Choose **New step** , search for `delay` and add a **Delay** action and configure for 1 minute.</span></span>

<span data-ttu-id="e561b-119">Wählen Sie **neuer Schritt** aus, und geben Sie `Batch` das Suchfeld ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-119">Choose **New step** and type `Batch` in the search box.</span></span> <span data-ttu-id="e561b-120">Fügen Sie die **MS Graph Batch Connector** -Aktion hinzu.</span><span class="sxs-lookup"><span data-stu-id="e561b-120">Add the **MS Graph Batch Connector** action.</span></span> <span data-ttu-id="e561b-121">Wählen Sie die Auslassungspunkte aus, und benennen Sie diese Aktion um `Batch PUT-team` .</span><span class="sxs-lookup"><span data-stu-id="e561b-121">Choose the ellipsis and rename this action to `Batch PUT-team`.</span></span>

<span data-ttu-id="e561b-122">Fügen **Sie den folgenden Code in das Feld** Text der Aktion ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-122">Add the following code into the **body** text box of the action.</span></span>

```json
{
  "requests": [
    {
      "id": 1,
      "url": "/groups/REPLACE/team",
      "method": "PUT",
      "headers": {
        "Content-Type": "application/json"
      },
      "body": {
        "memberSettings": {
          "allowCreateUpdateChannels": true
        },
        "messagingSettings": {
          "allowUserEditMessages": true,
          "allowUserDeleteMessages": true
        },
        "funSettings": {
          "allowGiphy": true,
          "giphyContentRating": "strict"
        }
      }
    }
  ]
}
```

<span data-ttu-id="e561b-123">Wählen Sie den `REPLACE` Platzhalter aus, und wählen Sie dann im Bereich dynamischer Inhalt den **Begriff Ausdruck** aus.</span><span class="sxs-lookup"><span data-stu-id="e561b-123">Select the `REPLACE` placeholder, then select **Expression** in the dynamic content pane.</span></span> <span data-ttu-id="e561b-124">Fügen Sie die folgende Formel in den **Ausdruck** ein.</span><span class="sxs-lookup"><span data-stu-id="e561b-124">Add the following formula into the **Expression**.</span></span>

```js
body('Batch_POST-groups').responses[0].body.id
```

![Ein Screenshot des Ausdrucks im Bereich "dynamischer Inhalt"](./images/flow-formula.png)

<span data-ttu-id="e561b-126">Diese Formel gibt an, dass die Gruppen-ID aus dem Ergebnis der ersten Aktion verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="e561b-126">This formula specifies that we want to use the group ID from the result of the first action.</span></span>

![Ein Screenshot des aktualisierten Aktions Texts](./images/updated-body.png)

<span data-ttu-id="e561b-128">Wählen Sie **Speichern** aus, und wählen Sie dann **Test** aus, um den Fluss auszuführen.</span><span class="sxs-lookup"><span data-stu-id="e561b-128">Choose **Save** , then choose **Test** to execute the flow.</span></span>

> [!TIP]
> <span data-ttu-id="e561b-129">Wenn ein Fehler wie angezeigt `The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'` wird, ist der Ausdruck falsch und verweist wahrscheinlich auf eine Fluss Aktion, die nicht gefunden werden kann.</span><span class="sxs-lookup"><span data-stu-id="e561b-129">If you receive an error like `The template validation failed: 'The action(s) 'Batch_POST-groups' referenced by 'inputs' in action 'Batch_2' are not defined in the template'`, the expression is incorrect and likely references a flow action it cannot find.</span></span> <span data-ttu-id="e561b-130">Stellen Sie sicher, dass der Name der Aktion, auf die verwiesen wird, genau übereinstimmt.</span><span class="sxs-lookup"><span data-stu-id="e561b-130">Ensure that the action name you are referencing matches exactly.</span></span>

<span data-ttu-id="e561b-131">Wählen Sie das Optionsfeld **Ich werde das Trigger** -Aktion ausführen aus, und wählen Sie **& Test speichern** aus.</span><span class="sxs-lookup"><span data-stu-id="e561b-131">Choose the **I'll perform the trigger** action radio button and choose **Save & Test**.</span></span> <span data-ttu-id="e561b-132">Wählen Sie im Dialogfeld **weiter** aus.</span><span class="sxs-lookup"><span data-stu-id="e561b-132">Choose **Continue** in the dialog.</span></span> <span data-ttu-id="e561b-133">Geben Sie einen Namen ohne Leerzeichen ein, und wählen Sie **Lauf Fluss** aus, um ein Team zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="e561b-133">Provide a name without spaces, and choose **Run flow** to create a Team.</span></span>

![Ein Screenshot des Dialogfelds "Ablaufsteuerung"](./images/run-flow.png)

<span data-ttu-id="e561b-135">Klicken Sie abschließend auf **Fertig** , um das Aktivitätsprotokoll anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e561b-135">Finally, choose the **Done** to see the activity log.</span></span> <span data-ttu-id="e561b-136">Nachdem der Fluss abgeschlossen ist, wurden Ihre Office 365 Gruppe und Ihr Team konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="e561b-136">Once the flow completes, your Office 365 Group and Team have been configured.</span></span> <span data-ttu-id="e561b-137">Wählen Sie die Batch Aktionselemente aus, um die Ergebnisse der JSON-Batch Aufrufe anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="e561b-137">Select the Batch action items to view the results of the JSON Batch calls.</span></span> <span data-ttu-id="e561b-138">Die `outputs` der `Batch PUT-team` Aktion sollte den Statuscode 201 für eine erfolgreiche Team Zuordnung ähnlich wie in der Abbildung unten haben.</span><span class="sxs-lookup"><span data-stu-id="e561b-138">The `outputs` of the `Batch PUT-team` action should have a status code of 201 for a successful Team association similar to the image below.</span></span>

![Ein Screenshot des erfolgreichen Ablauf Aktivitätsprotokolls](./images/success.png)
