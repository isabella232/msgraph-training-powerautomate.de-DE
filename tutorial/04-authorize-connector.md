---
ms.openlocfilehash: bf83723de025f3e1f6bde5b4226fc8966dff6b9a
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829736"
---
<!-- markdownlint-disable MD002 MD041 -->

<span data-ttu-id="20e31-101">Der abschließende Konfigurationsschritt, um sicherzustellen, dass der Connector einsatzfähig ist, besteht darin, den benutzerdefinierten Connector zu autorisieren und zu testen, um eine zwischengespeicherte Verbindung zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="20e31-101">The final configuration step to ensure the connector is ready for use is to authorize and test the custom connector to create a cached connection.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="20e31-102">Für die folgenden Schritte müssen Sie mit Administratorrechten angemeldet sein.</span><span class="sxs-lookup"><span data-stu-id="20e31-102">The following steps requires that you are logged in with administrator privileges.</span></span>

<span data-ttu-id="20e31-103">Wechseln Sie in [Microsoft Power automatisieren](https://flow.microsoft.com)zum Menüelement **Daten** auf der linken Seite, und wählen Sie die Seite **Verbindungen** aus.</span><span class="sxs-lookup"><span data-stu-id="20e31-103">In [Microsoft Power Automate](https://flow.microsoft.com), go to the **Data** menu item on the left and choose the **Connections** page.</span></span> <span data-ttu-id="20e31-104">Klicken Sie auf den Link **neue Verbindung** .</span><span class="sxs-lookup"><span data-stu-id="20e31-104">Choose the **New Connection** link.</span></span>

![Ein Screenshot der Schaltfläche "neue Verbindung"](./images/new-connection.png)

<span data-ttu-id="20e31-106">Suchen Sie Ihren benutzerdefinierten Connector, und schließen Sie die Verbindung ab, indem Sie auf die Schaltfläche Plus klicken.</span><span class="sxs-lookup"><span data-stu-id="20e31-106">Find your custom connector and complete the connection by clicking the plus button.</span></span> <span data-ttu-id="20e31-107">Melden Sie sich mit dem Azure Active Directory-Konto des Office 365 Mandanten Administrators an.</span><span class="sxs-lookup"><span data-stu-id="20e31-107">Sign in with your Office 365 tenant administrator's Azure Active Directory account.</span></span>

![Ein Screenshot der Liste "Verbindungen"](./images/connection-sign-in.png)

<span data-ttu-id="20e31-109">Wenn Sie zur Eingabe der erforderlichen Berechtigungen aufgefordert werden, überprüfen Sie die **Zustimmung im Namen Ihrer Organisation** , und wählen Sie dann **akzeptieren** aus, um Berechtigungen zu autorisieren.</span><span class="sxs-lookup"><span data-stu-id="20e31-109">When prompted for the requested permissions, check **Consent on behalf of your organization** and then choose **Accept** to authorize permissions.</span></span>

![Ein Screenshot der Zustimmungsaufforderung](./images/consent-prompt.png)

<span data-ttu-id="20e31-111">Nachdem Sie die Berechtigungen autorisiert haben, wird eine Verbindung in Power Automation erstellt.</span><span class="sxs-lookup"><span data-stu-id="20e31-111">After you authorize the permissions, a connection is created in Power Automate.</span></span>

<span data-ttu-id="20e31-112">Der benutzerdefinierte Connector ist jetzt konfiguriert und aktiviert.</span><span class="sxs-lookup"><span data-stu-id="20e31-112">The custom connector is now configured and enabled.</span></span> <span data-ttu-id="20e31-113">Es kann eine Verzögerung bei der Anwendung und Verfügbarkeit von Berechtigungen geben, aber der Connector ist jetzt konfiguriert.</span><span class="sxs-lookup"><span data-stu-id="20e31-113">There may be a delay in permissions being applied and available, but the connector is now configured.</span></span>
