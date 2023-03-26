# Beitrag leisten

Wir freuen uns, dass Sie uns helfen wollen, indem Sie zu Consul beitragen. Hier ist ein Leitfaden, der beschreibt, wie Sie Änderungen zum Projekt beitragen können.

## Ein Problem melden

Wenn Sie einen Fehler in der Leistung der Plattform oder direkt im Code entdeckt haben, empfehlen wir Ihnen, [ein Issue im Consul Github Repository zu eröffnen] (https://github.com/consul/consul/issues/new).

Bevor Sie das tun, **bitte nehmen Sie sich etwas Zeit, um die [bestehenden Probleme] (https://github.com/consul/consul/issues) zu überprüfen und sicherzustellen, dass das, was Sie melden wollen, nicht bereits von einer anderen Person gemeldet wurde**. Falls jemand anderes das gleiche Problem schon einmal gemeldet hat, können Sie, wenn Sie mehr Details dazu haben, einen Kommentar auf der Problem-Seite schreiben - ein wenig mehr Hilfe kann einen großen Unterschied machen!

Beachten Sie beim Verfassen einer neuen Meldung die folgenden Tipps, damit sie leicht zu lesen und zu verstehen ist:

- Versuchen Sie, einen beschreibenden und treffenden Titel zu verwenden.
- Es ist eine gute Idee, einige Abschnitte einzuschließen - für den Fall, dass sie benötigt werden - wie z.B.: Schritte zur Reproduktion des Fehlers, erwartetes Verhalten/Reaktion, tatsächliche Reaktion oder Screenshots.
- Es könnte auch hilfreich sein, Ihr Betriebssystem, die Browserversion und die installierten Plugins anzugeben.

## Lösung eines Problems

[Issues in Consul](https://github.com/consul/consul/issues), die mit `PRs-welcome` gekennzeichnet sind, sind gut definierte Funktionen, die von jedem implementiert werden können, der das möchte. Andererseits kennzeichnet die Kennzeichnung `not-ready` Funktionen oder Änderungen, die noch nicht genau definiert sind oder über die noch intern entschieden werden muss, so dass wir empfehlen, nicht zu versuchen, sie zu lösen, bis die Admins eine Lösung gefunden haben.

Wir schlagen vor, die folgenden Schritte zu befolgen, um einen guten Überblick über die Änderungen zu behalten, die Sie vornehmen wollen:

- Fügen Sie zunächst einen Kommentar zu dem Problem hinzu, damit alle wissen, dass Sie daran arbeiten werden. Wenn dem Problem jemand zugewiesen wurde, bedeutet das, dass diese Person bereits an der Lösung des Problems arbeitet.
- Forken Sie das Projekt.
- Erstellen Sie einen Feature-Zweig, der auf dem "Master"-Zweig basiert. Um ihn leichter zu identifizieren, können Sie ihn mit der Nummer des Problems benennen, gefolgt von einem prägnanten und beschreibenden Namen (z.B. `123-fix_proposals_link`).
- Arbeiten Sie in Ihrem Zweig und tragen Sie dort Ihre Änderungen ein.
- Stellen Sie sicher, dass alle Tests erfolgreich sind. Falls Sie eine neue Funktion erweitern oder erstellen, fügen Sie ihr eine eigene Spezifikation hinzu.
- Wenn Sie fertig sind, senden Sie eine **Pull-Anfrage** an das [Consul-Repository] (https://github.com/consul/consul/), in der Sie Ihre Lösung beschreiben, damit wir sie besser verstehen können. Es ist auch wichtig zu sagen, welches Problem Sie angehen, also geben Sie es in der ersten Zeile der Pull Request Beschreibung an (z.B. `Fixes #123`).
- Unser Kernteam wird Ihren PR überprüfen und, falls nötig, Änderungen vorschlagen. Wenn alles gut aussieht, werden Ihre Änderungen zusammengeführt)

> **Wie du an deinem ersten Pull Request arbeitest?** Das kannst du in dieser _kostenlosen_ Serie [How to Contribute to an Open Source Project on GitHub] (https://egghead.io/series/how-to-contribute-to-an-open-source-project-on-github) lernen.

## Andere Möglichkeiten des Beitragens

Wir freuen uns über jede Art von Beitrag zu Consul. Auch wenn Sie nicht zur Programmierung beitragen können, können Sie es trotzdem tun:

- Probleme oder Fehler, auf die Sie gestoßen sind, melden.
- Helfen Sie bei der Übersetzung der Plattform in andere Sprachen, die Sie beherrschen, auf [Consul's Crowdin] (https://crwd.in/consul).
- Helfen Sie bei der [Consul-Dokumentation] (https://github.com/consul/docs).
