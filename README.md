# Lern-Bericht
👤 Dieser Lern-Bericht wurde von mir, Eray Çimen, erfasst und thematisiert ein Anhaltspunkt aus dem Modul 183. In diesem Unterrichtseinheiten werden grundlegende Probleme bezüglich der Applikationssicherheit identifiziert, charakterisiert und behoben.

## Einleitung

👩‍💻 Der sogenannten "Cross-Site-Request-Forgery"-Angriff ermöglicht einem, Funktionen einer Website oder Ähnliches zu bedienen, ohne diese tatsälich zu nutzen. Mit diesem Beitrag möchte ich anhand eines Projekts in die technische Tiefe des CSRF eingehen und diese Schwachstelle beseitigen.

## Was habe ich gelernt?

✍️ Beschreiben Sie in einem Satz **eine** Sache, die Sie bei diesem Projekt gelernt haben und die Sie in diesem Lern-Bericht dokumentieren.

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

❗ Der Admin startet die obrige HTML-Seite auf seinem Computer. Geht er nun wieder auf das News-Portal und ihm fällt auf, dass der News-Eintrag auf einmal fehlt:

![deleted](https://user-images.githubusercontent.com/26624740/205597203-6cd30e88-76e2-4ec5-8256-118c49fa4375.PNG)


✍️ Verwenden Sie drei verschiedene Medien, um zu zeigen, was Sie gelernt haben. Zum Beispiel:

* Eine textliche Beschreibung
* Ein deutliches, aussagekräftiges Bild oder eine kommentierte Bildschirm-Aufnahme
* Ein gut dokumentierter Code-Fetzen
* Ein Link zu einem *selbst aufgenommenen* youtube-Video oder `.gif`.

## Verifikation

✍️ Erklären Sie kurz und bündig, inwiefern die von Ihnen verwendeten Medien zeigen, was Sie gelernt haben.

# Reflektion zum Arbeitsprozess

👍 Überlegen Sie sich jeweils etwas, was gut an Ihrer Arbeit lief; 

👎 und etwas, was nicht gut lief.

**VBV**: ✍️ Formulieren Sie davon ausgehend einen *handelbaren* Verbesserungsvorschlag.
