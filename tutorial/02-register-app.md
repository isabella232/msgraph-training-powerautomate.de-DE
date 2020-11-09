---
ms.openlocfilehash: 22c9c7ddd8513d857d96ade608e4b2e4e809dc41
ms.sourcegitcommit: 64947f11d367ffbebbafb700fdfdc20617275f35
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/30/2020
ms.locfileid: "48829768"
---
<!-- markdownlint-disable MD002 MD041 -->

In dieser Übung erstellen Sie eine neue Azure Active Directory-Anwendung, die verwendet wird, um die Delegierten Berechtigungen für den benutzerdefinierten Connector bereitzustellen.

Öffnen Sie einen Browser, und navigieren Sie zu [Azure Active Directory Admin Center](https://aad.portal.azure.com). Klicken Sie im linken Navigationsmenü auf den Link **Azure Active Directory** , und wählen Sie dann den Eintrag **App-Registrierungen** im Abschnitt **Manage** des **Azure Active Directory** Blade aus.

![Ein Screenshot des Azure Active Directory Blade im Azure Active Directory Admin Center](./images/app-registrations.png)

Wählen Sie das **neue Registrierungs** Menüelement oben auf dem Blatt **App-Registrierungen** aus.

![Ein Screenshot des Blatts "App-Registrierungen" im Azure Active Directory Admin Center](./images/new-registration.png)

Geben Sie `MS Graph Batch App` in das Feld **Name** ein. Wählen Sie im Abschnitt **unterstützte Kontotypen** die Option **Konten in einem beliebigen Organisations Verzeichnis** aus. Lassen Sie den Abschnitt **Umleitungs-URI** leer, und wählen Sie **registrieren** aus.

![Ein Screenshot des Registers eines Anwendungs Blatts im Azure Active Directory Admin Center](./images/register-an-app.png)

Kopieren Sie auf dem Blatt **MS Graph-Batch-App** die **Anwendungs-ID (Client)**. Sie benötigen diese in der nächsten Übung.

![Ein Screenshot der registrierten Anwendungsseite](./images/app-id.png)

Wählen Sie den Eintrag **API-Berechtigungen** im Abschnitt **Verwalten** des **MS Graph-Batch-App** -Blades aus. Wählen Sie **Hinzufügen einer Berechtigung** unter **API-Berechtigungen** aus.

![Ein Screenshot des API-Berechtigungs Blatts](./images/api-permissions.png)

Wählen Sie im Blade **API-Berechtigungen anfordern** die Option **Microsoft Graph** und dann **Delegierte Berechtigungen** aus. Suchen `group` Sie nach, und wählen Sie dann die Delegierte Berechtigung **alle Gruppen lesen und schreiben** aus. Klicken Sie unten im Blade auf **Berechtigungen hinzufügen** .

 ![Ein Screenshot des Blades für Anforderungs-API-Berechtigungen](./images/select-permissions.png)

Wählen Sie den Eintrag **Zertifikate und Geheimnisse** im Abschnitt **Verwalten** des **MS Graph-Batch-App** -Blades aus, und wählen Sie dann **neuer geheimer Client Schlüssel** aus. Geben Sie `forever` in die **Beschreibung** ein, und wählen Sie **nie** unter **Expires** aus. Wählen Sie **Hinzufügen** aus.

![Ein Screenshot des Blatts "Zertifikat und Geheimnisse"](./images/create-client-secret.png)

Kopieren Sie den Wert für den neuen geheimen Schlüssel. Sie benötigen diese in der nächsten Übung.

![Ein Screenshot des neuen geheimen Client Schlüssels](./images/copy-client-secret.png)

> [!IMPORTANT]
> Dieser Schritt ist wichtig, da auf den geheimen Zugriff nach dem Schließen dieses Blades nicht zugegriffen werden kann. Speichern Sie diesen Schlüssel in einem Text-Editor zur Verwendung in bevorstehenden Übungen.

Um die Verwaltung zusätzlicher Dienste zu ermöglichen, die über Microsoft Graph zugänglich sind, einschließlich der Teams-Eigenschaften, müssen Sie zusätzliche, geeignete Bereiche auswählen, um die Verwaltung bestimmter Dienste zu ermöglichen. Um beispielsweise unsere Lösung so zu erweitern, dass OneNote-Notizbücher oder Planner-Pläne, Buckets und Aufgaben erstellt werden, müssen Sie die erforderlichen Berechtigungs Bereiche für die entsprechenden APIs hinzufügen.
