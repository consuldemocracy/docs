# Javascript

Wenn Sie eigenen Javascript-Code hinzufügen möchten, ist die Datei "app/assets/javascripts/custom.js" die richtige Wahl. Um zum Beispiel einen neuen Alarm zu erstellen, fügen Sie einfach hinzu:

```js
$(function () {
  alert("foobar");
});
```

Wenn Sie mit Coffeescript-Code arbeiten, können Sie ihn mit [coffeelint](http://www.coffeelint.org/) überprüfen (installieren Sie ihn mit `npm install -g coffeelint`) :

```bash
coffeelint .
```
