# Lern-Bericht
👤 Dieser Lern-Bericht wurde von mir, Eray Çimen, erfasst und thematisiert ein Anhaltspunkt aus dem Modul 183. In diesem Unterrichtseinheiten werden grundlegende Probleme bezüglich der Applikationssicherheit identifiziert, charakterisiert und behoben.

## Einleitung

👩‍💻 Der sogenannten "Cross-Site-Request-Forgery"-Angriff ermöglicht einem, Funktionen einer Website oder Ähnliches zu bedienen, ohne diese tatsälich zu nutzen. Mit diesem Beitrag möchte ich anhand eines Projekts in die technische Tiefe des CSRF eingehen und diese Schwachstelle beseitigen.

## Was habe ich gelernt?

📕 Ich habe gelernt, wie man CRSF Attacken vermeiden kann.

## Beschreibung

### Problem:

Angenommen, bei einem News-Portal ist es nur für den Admin möglich, Beiträge zu entfernen. Öffnet er das Webinterface und meldet sich an, wird er von der Startseite begrüsst und hat als einziger Zugriff auf den "delete-Knopf", der sich auf jeden Beitrag befindet:

![delete-Knopf](https://user-images.githubusercontent.com/26624740/205594750-94c59fd5-5969-4b5e-a59b-11d8c63b729b.PNG)

Der Admin wird neugierig und sieht sich mit den Devtools von seinem Browser diesen Knopf genauer an und findet dabei dieses HTML-Element:

```html
<a href="news/delete.xhtml;jsessionid=171e6617771813258487394e19df?id=1" class="btn btn-danger btn-xs">delete</a>
```

Der Admin, der sich zwar kaum mit HTML auskennt, versucht nun eine Seite zu erstellen, worin der Endpunkt vom oben zusehendem Element ausgeführt wird. Er kommt auf folgendes Resultat:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <img src="http://localhost:8080/InsecureApp/faces/secured/news/delete.xhtml?id=1" />
</body>
</html>
```

❗ Der Admin startet die obige HTML-Seite auf seinem Computer. Geht er nun wieder auf das News-Portal und ihm fällt auf, dass der News-Eintrag auf einmal fehlt:

![deleted](https://user-images.githubusercontent.com/26624740/205597203-6cd30e88-76e2-4ec5-8256-118c49fa4375.PNG)

Diese Sicherheitslücke ist darum da, weil es sich um einen "GET-Request" handelt. Das muss jetzt im JSF behoben werden.

### Lösung:

✔Hier müssen folgende Schritte gemacht werden: Die Frontendseite "delete.xhtml" entfernen, das HTML-Element des Deleteknopfs zu einem XHTML-Commandbutton umstellen und die Löschmethode mit einer Backendfunktion verknüpfen. Der XHTML-Tag sollte nun so aussehen:

```html
<h:commandButton value="delete" action="#{newsController.delete(newsitem)}" class="btn btn-danger btn-xs"></h:commandButton>
```

Wenn jetzt auf dem Portal ein News-Beitrag gelöscht wird, kann man unter den Devtools beobachten, dass es sich inzwischen um ein "POST-Request" handelt. Externe Quellen können diese Aktion nicht mehr durchführen aufgrund der CORS-Policy:

![POST](https://user-images.githubusercontent.com/26624740/205603205-eba4c8a2-ba63-4454-bd65-ee9436ef0b62.PNG)

Der Admin versucht die Attacke nochmals durchzuführen und kann bestätigen, dass das Problem beseitigt wurde.

## Verifikation

📊 Der Screenshot, worin die HTTP-Requests aufgezeichnet werden, verifiziert zusammen mit den Codeausschnitten und dem dazugehörigen Text, dass die Löschmethode nun unter einem "POST-Request" läuft und durch das "strict-origin-when-cross-origin" von externen Angreifern geschützt wird.

# Reflektion zum Arbeitsprozess

👍 Das formale Arbeiten am Lern-Bericht lief gut ab: Es wurden verschiedene Medien benutzt, eine klare Dokumentation des Projekts wurde geliefert und ein sinnvolles Fazit konnte eingeleitet werden.

👎 Während des Moduls habe ich es versäumt, den Ablauf der Lernaufträge gut zu dokumentieren. Dadurch musste ich mich in das Thema wie von vorne einarbeiten, da mir die Lösungen dazu fehlten.

**VBV**: ✍️ Im nächsten Modul werde ich Lernaufträge und Projekte so führen, dass mir die Arbeitsschritte beim Einlesen sofort klar werden.
