# Bilder

Wenn Sie ein Bild überschreiben wollen, müssen Sie zunächst den Dateinamen herausfinden, der standardmäßig unter `app/assets/images` zu finden ist. Wenn Sie zum Beispiel das Logo der Kopfzeile (`app/assets/images/logo_header.png`) ändern möchten, müssen Sie eine weitere Datei mit genau demselben Dateinamen im Ordner `app/assets/images/custom` erstellen. Die Bilder und Icons, die Sie höchstwahrscheinlich ändern möchten, sind:

- apple-touch-icon-200.png
- icon_home.png
- logo_email.png
- logo_header.png
- map.jpg
- social_media_icon.png
- social_media_icon_twitter.png

## Stadtplan

Sie finden den Stadtplan unter [`/app/assets/images/map.jpg`](https://github.com/consul/consul/blob/master/app/assets/images/map.jpg), ersetzen Sie ihn einfach durch ein Bild Ihrer Stadtteile ([Beispiel](https://github.com/ayuntamientomadrid/consul/blob/master/app/assets/images/map.jpg)).

Anschließend empfehlen wir Ihnen, ein Online-Tool wie http://imagemap-generator.dariodomi.de/ oder https://www.image-map.net/ zu verwenden, um die Html-Koordinaten zu generieren, mit denen Sie eine [image-map](https://www.w3schools.com/tags/tag_map.asp) für jeden der Stadtteile erstellen können. Diese Koordinaten sollten in die jeweiligen Geozonen im Admin-Geozonen-Panel (`/admin/geozones`) eingetragen werden.
