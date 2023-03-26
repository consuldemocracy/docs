# Erstellen Ihrer Abspaltung

Das Git-Repository von Consul wird auf Github.com gehostet. Wir empfehlen, es für das Repository Ihrer Abspaltung zu verwenden, um die Dinge zu vereinfachen. Sie können aber auch jeden anderen Dienst wie Bitbucket oder Gitlab verwenden, wenn Sie möchten. Vergessen Sie nur nicht, in der Fußzeile einen Verweis auf CONSUL zu setzen, um der Projektlizenz (GPL Affero 3) zu entsprechen.

1. [Registrieren Sie ein Benutzerkonto auf Github](https://github.com/join), wenn Sie noch keines haben.

2. [Erstellen Sie eine Organisation](https://help.github.com/articles/creating-a-new-organization-from-scratch/) auf Github mit dem Namen Ihrer Stadt oder der Organisation, die Consul verwenden wird. **Dies ist nicht zwingend erforderlich**, hilft aber dabei, den Zweck der Abspaltung und zukünftige Beiträge anderer Benutzer zu verstehen.

3. [Forken Sie Consul](https://help.github.com/articles/fork-a-repo/) über die Schaltfläche **fork** in der oberen rechten Ecke auf https://github.com/consul/consul.

4. [Klonen Sie Ihr Fork-Repository](https://help.github.com/articles/cloning-a-repository/) auf Ihren Computer.

\***\*WICHTIGER HINWEIS**: Forken Sie nicht `https://github.com/AyuntamientoMadrid/consul`, das ist ein weit verbreiteter Fehler, der zu zahlreichen und schwerwiegenden Problemen führt.

## Warum den Code veröffentlichen?

Wir empfehlen dringend, den Code aus mehreren Gründen öffentlich zu machen:

- **Transparenz**: Sie sollte Teil der Kultur von öffentlichen Einrichtungen sein, die Consul einsetzen, sowie von jeder Organisation oder Gruppe.
- **Unterstützung**: Wenn Sie technische Hilfe benötigen, können sowohl die Community als auch das Consul-Kernteam den beteiligten Code einsehen und Sie beraten.
- **Zusammenarbeit**: Mit anderen Fachleuten, Bürgern, usw...
- Nicht zuletzt wird Consul unter der **[AGPLv3](https://github.com/consul/consul/blob/master/LICENSE-AGPLv3.txt) Lizenz** vertrieben, die die Veröffentlichung des Quellcodes erlaubt.
