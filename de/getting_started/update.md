# Den Fork auf dem neuesten Stand halten

## Konfigurieren Ihrer Git-Remotes

Wenn Sie Ihren Fork korrekt erstellt und lokal geklont haben, wird er ausgeführt:

```bash
git remote -v
```

Es sollte es etwas Ähnliches ausgeben:

> origin git@github.com:your_user_name/consul.git (fetch)<br/>
> origin git@github.com:your_user_name/consul.git (push)

Jetzt müssen wir CONSULs Github als Upstream-Remote mit hinzufügen:

```bash
git remote add upstream git@github.com:consul/consul.git
```

und um zu prüfen, ob alles in Ordnung ist mit

```bash
git remote -v
```

Sie sollten wieder folgende Ausgabe bekommen:

> upstream git@github.com:consul/consul.git (fetch)<br/>
> upstream git@github.com:consul/consul.git (push)<br/>
> origin git@github.com:your_user_name/consul.git (fetch)<br/>
> origin git@github.com:your_user_name/consul.git (push)

## Änderungen von CONSUL abrufen

Beginnen Sie damit, einen Zweig namens **upstream** von Ihrem **master**-Zweig zu erstellen, um die CONSUL-Änderungen anzuwenden:

```bash
git checkout master
git pull
git checkout -b upstream
```

Dann können wir alle Änderungen von **consul** remote server mit abrufen:

```bash
git fetch upstream
```

Und dann kann man wählen zwischen:

A. Alle aktuellen Änderungen auf CONSULs **Master**-Zweig mit `git merge upstream/master` holen.

B. Nur bis zu einem bestimmten Release-Tag aktualisieren (damit Sie inkrementelle Updates machen können, wenn Sie mehr als eine Version im Rückstand sind). Um zum Beispiel auf die Version [v0.9](https://github.com/consul/consul/releases/tag/v0.9) zu aktualisieren, genügt: `git merge v0.9`.

## Zusammenführen von Änderungen

Nach dem Befehl `merge` im vorherigen Abschnitt gibt es drei mögliche Ergebnisse:

A. Sie erhalten eine nette `Already up-to-date.` Antwort. Das bedeutet, dass Ihr Fork mit consul 😊👌 auf dem neuesten Stand ist.

B. Du bekommst einen Bildschirm in deinem git-konfigurierten Editor, der die Commit-Meldung `Merge remote-tracking branch 'upstream/master' into upstream` anzeigt. Das bedeutet, dass Git in der Lage war, die letzten Änderungen aus dem Master-Zweig von CONSUL zu übernehmen und sie ohne Code-Änderungskonflikte zusammenführen kann. Beenden Sie den Commit.

C. Sie erhalten einige Git-Fehler zusammen mit der Meldung `Automatic merge failed; fix conflicts and then commit the result.`. Das bedeutet, dass es Konflikte zwischen den Codeänderungen, die Sie vorgenommen haben, und denen, die seit der letzten Aktualisierung im CONSUL-Repository vorgenommen wurden, gibt. Das ist der Hauptgrund, warum wir dringend empfehlen, Ihren Fork häufig zu aktualisieren (mindestens monatlich). Lösen Sie Merge-Konflikte sorgfältig auf und übertragen Sie sie.

Jetzt können Sie einfach Ihren **upstream** Branch auf Github pushen und einen Pull Request erstellen, so dass Sie alle Änderungen, die in Ihr Repo einfließen, leicht überprüfen können und sehen, wie Ihre Testsuite läuft.

Denken Sie daran, dass Sie immer schnell die Änderungen überprüfen können, die von CONSUL zu Ihrem Fork kommen, indem Sie **Ihren_Organisationsnamen** in der URL ersetzen: https://github.com/your_org_name/consul/compare/master...consul:master.
