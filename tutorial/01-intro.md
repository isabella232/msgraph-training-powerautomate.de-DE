---
ms.openlocfilehash: d628ef3ffff3655bbb15115b6f17726e55185b5b
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829737"
---
<!-- markdownlint-disable MD002 MD041 -->

Es gibt mehr als 230 out-of-Box-Konnektoren für Microsoft Power Automation. Viele dieser Connectors verwenden das Microsoft Graph-Diagramm, um mit bestimmten Endpunkten von Microsoft-Produkten zu kommunizieren. Darüber hinaus gibt es andere Szenarien, in denen wir möglicherweise den Microsoft Graph direkt aus Power Automation mithilfe grundlegender Bausteine des Diensts aufrufen müssen, da es keinen Connector gibt, der direkt mit dem Microsoft Graph kommuniziert, um die gesamte API abzudecken.

Neben den Adressierungs Szenarien für das direkte Aufrufen von Microsoft Graph unterstützen eine Reihe von Microsoft Graph-API-Endpunkten nur [Delegierte Berechtigungen](https://docs.microsoft.com/graph/permissions-reference). Der HTTP-Connector in Microsoft Power Automation ermöglicht sehr flexible Integrationen, einschließlich Aufrufen von Microsoft Graph. Der HTTP-Connector verfügt jedoch nicht über die Möglichkeit zum Zwischenspeichern der Anmeldeinformationen eines Benutzers, um bestimmte Delegierte Berechtigungs Szenarien zu ermöglichen. In diesen Fällen kann ein benutzerdefinierter Connector erstellt werden, um einen Wrapper um die Microsoft Graph-API bereitzustellen und die Verwendung der API mit Delegierten Berechtigungen zu ermöglichen.

In dieser Übungseinheit werden die beiden oben beschriebenen Szenarien behandelt. Zunächst erstellen Sie einen benutzerdefinierten Connector, um Integrationen mit Microsoft Graph zu ermöglichen, für die [Delegierte Berechtigungen](https://docs.microsoft.com/graph/permissions-reference)erforderlich sind. Zweitens verwenden Sie den $Batch- [Anforderungs Endpunkt](https://docs.microsoft.com/graph/json-batching), um Zugriff auf die volle Leistungsfähigkeit von Microsoft Graph bereitzustellen, während die Delegierten Berechtigungen verwendet werden, für die eine APP über einen angemeldeten Benutzer verfügen muss.

> [!NOTE]
> Dies ist ein Lernprogramm zum Erstellen eines benutzerdefinierten Connectors für die Verwendung in Microsoft Power automatisieren und Azure Logic-apps. In diesem Lernprogramm wird davon ausgegangen, dass Sie den [benutzerdefinierten Konnektor](https://docs.microsoft.com/connectors/custom-connectors/) gelesen haben, um den Prozess zu verstehen.

## <a name="prerequisites"></a>Voraussetzungen

Um diese Übung in diesem Beitrag abzuschließen, benötigen Sie Folgendes:

- Administrator Zugriff auf eine Office 365 Mandantschaft. Wenn Sie noch keinen haben, besuchen Sie das [Office 365 Entwicklerprogramm](https://developer.microsoft.com/office/dev-program) , um sich bei einem kostenlosen Entwickler Mandanten anzumelden.
- Zugriff auf [Microsoft Power Automation](https://flow.microsoft.com/).

## <a name="feedback"></a>Feedback

Geben Sie Feedback zu diesem Lernprogramm im [GitHub-Repository](https://github.com/microsoftgraph/msgraph-training-powerautomate)an.
