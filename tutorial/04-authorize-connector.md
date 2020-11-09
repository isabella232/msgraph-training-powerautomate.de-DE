---
ms.openlocfilehash: bf83723de025f3e1f6bde5b4226fc8966dff6b9a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829736"
---
<!-- markdownlint-disable MD002 MD041 -->

Der abschließende Konfigurationsschritt, um sicherzustellen, dass der Connector einsatzfähig ist, besteht darin, den benutzerdefinierten Connector zu autorisieren und zu testen, um eine zwischengespeicherte Verbindung zu erstellen.

> [!IMPORTANT]
> Für die folgenden Schritte müssen Sie mit Administratorrechten angemeldet sein.

Wechseln Sie in [Microsoft Power automatisieren](https://flow.microsoft.com)zum Menüelement **Daten** auf der linken Seite, und wählen Sie die Seite **Verbindungen** aus. Klicken Sie auf den Link **neue Verbindung** .

![Ein Screenshot der Schaltfläche "neue Verbindung"](./images/new-connection.png)

Suchen Sie Ihren benutzerdefinierten Connector, und schließen Sie die Verbindung ab, indem Sie auf die Schaltfläche Plus klicken. Melden Sie sich mit dem Azure Active Directory-Konto des Office 365 Mandanten Administrators an.

![Ein Screenshot der Liste "Verbindungen"](./images/connection-sign-in.png)

Wenn Sie zur Eingabe der erforderlichen Berechtigungen aufgefordert werden, überprüfen Sie die **Zustimmung im Namen Ihrer Organisation** , und wählen Sie dann **akzeptieren** aus, um Berechtigungen zu autorisieren.

![Ein Screenshot der Zustimmungsaufforderung](./images/consent-prompt.png)

Nachdem Sie die Berechtigungen autorisiert haben, wird eine Verbindung in Power Automation erstellt.

Der benutzerdefinierte Connector ist jetzt konfiguriert und aktiviert. Es kann eine Verzögerung bei der Anwendung und Verfügbarkeit von Berechtigungen geben, aber der Connector ist jetzt konfiguriert.
