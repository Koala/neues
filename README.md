# News-Verwaltung für REDAXO 5 (Aktuelles, Pressemitteilungen, Pressestimmen, ...)

![web_banner_redaxo_addon_neues](https://user-images.githubusercontent.com/3855487/204768778-99b56b18-3997-4466-9ae2-537fd792c521.png)

Mit diesem Addon können News-Beiträge anhand von YForm und YOrm im Backend verwaltet und im Frontend ausgegeben werden. Auf Wunsch auch multidomainfähig und mehrsprachig.

## Features

* Vollständig mit **YForm** umgesetzt: Alle Features und Anpassungsmöglichkeiten von YForm verfügbar
* Einfach: Die Ausgabe erfolgt über [`rex_sql`](https://redaxo.org/doku/master/datenbank-queries) oder objektorientiert über [YOrm](https://github.com/yakamara/redaxo_yform_docs/blob/master/de_de/yorm.md)
* Flexibel: **Zugriff** über die [YForm Rest-API](https://github.com/yakamara/redaxo_yform/blob/master/docs/plugins.md#restful-api-einf%C3%BChrung)
* Sinnvoll: Nur ausgewählte **Rollen**/Redakteure haben Zugriff
* Bereit für Multidomain-Newsverwaltung mit YRewrite
* Bereit für **mehrsprachige** Websites: Reiter für Sprachen auf Wunsch anzeigen oder ausblenden
* Bereit für viel mehr: Kompatibel zum [URL2-Addon](https://github.com/tbaddade/redaxo_url)

> **Hinweis:** Neues benötigt ab Version 3 [`yform_field`](https://github.com/alexplusde/yform_field/) für die Auswahl von (YRewrite-)Domains und Dem Auswahldatum für Veröffentlichungen

> **Tipp:** Neues arbeitet hervorragend zusammen mit den Addons [`yform_usability`](https://github.com/FriendsOfREDAXO/yform_usability/) und [`yform_geo_osm`](https://github.com/FriendsOfREDAXO/yform_geo_osm)

> **Steuere eigene Verbesserungen** dem [GitHub-Repository von neues](https://github.com/alexplusde/neues) bei. Oder **unterstütze dieses Addon:** Mit einer [Beauftragung unterstützt du die Weiterentwicklung dieses AddOns](https://github.com/sponsors/alexplusde)

## Installation

Im REDAXO-Installer das Addon `neues` herunterladen und installieren. Anschließend erscheint ein neuer Menüpunkt `Veranstaltungen` sichtbar.

## Nutzung im Frontend

### Die Klasse `neues_entry`

Typ `rex_yform_manager_dataset`. Greift auf die Tabelle `rex_neues_entry` zu.

#### Beispiel-Ausgabe einer News

```php
$entry = neues_entry::get(3)); // News mit der id=3
// dump($entry);

echo $entry->getName();
echo $entry->getAuthor();
echo $entry->getDomain();
echo $entry->getTeaser();
echo $entry->getImage();
echo $entry->getMedia();
echo $entry->getDescriptionAsPlaintext();
echo $entry->getDescription();
echo $entry->getExternalUrl();
echo $entry->getExternalLabel();
echo $entry->getPublishDate();
echo $entry->getPublishDateTime();
echo $entry->getFormattedPublishDate($format_date = IntlDateFormatter::FULL, $format_time = IntlDateFormatter::NONE, $lang = null);
echo $entry->getStatus();
echo $entry->getUrl();
```

```php
$categories = neues_entry::get(3)->getCategories();
// dump($categories);

foreach($categories as $category) {
// ...
}
```

### Die Klasse `neues_category`

Typ `rex_yform_manager_dataset`. Greift auf die Tabelle `rex_neues_category` zu.

#### Beispiel-Ausgabe einer Kategorie

```php
$category = neues_category::get(3)); // News-Kategorie mit der id=3
// dump($category);

echo $category->getName();

$entries =  $category->getEntries();

foreach($entries as $entry) {
    echo $entry->getName();
// ...
}
```

## URL2-Profile

### News-Einträge

Mit der Methode `getUrl()` kann die URL des aktuellen News-Eintrags geholt werden. Dazu muss URL2 installiert sein und ein Profil mit dem Schlüssel `neues-entry-id` angelegt sein.

## Nutzung im Backend: Die Terminverwaltung

## RESTful API

Die [Rest-API](https://github.com/yakamara/redaxo_yform/blob/master/docs/plugins.md#restful-api-einf%C3%BChrung) ist über das REST-Plugin von YForm umgesetzt.

### Einrichtung

Zunächst das REST-Plugin von YForm installieren und einen Token einrichten. Den Token auf die jeweiligen Endpunkte legen:

```
    /neues/3/entry
    /neues/3/category
    /neues/3/location
```

### Endpunkt `entry`

**Auslesen:** GET `example.org/rest/neues/3/date/?token=###TOKEN###`

**Auslesen einzelner Termin**  GET `example.org/rest/neues/3//entry/7/?token=###TOKEN###` Eintrag der `id=7`

### Endpunkt `category`

**Auslesen:** GET `example.org/rest/neues/3/category/?token=###TOKEN###`

**Auslesen einzelne Kategorie**  GET `example.org/rest/neues/3/category/7/?token=###TOKEN###` Eintrag der `id=7`

### Endpunkt `location`

**Auslesen:** GET `example.org/rest/neues/3/location/?token=###TOKEN###`

**Auslesen einzelner Standort**  GET `example.org/rest/neues/3/location/7/?token=###TOKEN###` Eintrag  der `id=7`

## Import

### Import via CSV

Neues basiert auf YForm. Importiere deine Einträge bequem per CSV, wie du es von YForm kennst.

## Export

### Export via CSV

Neues basiert auf YForm. Exportiere deine Einträge bequem per CSV, wie du es von YForm kennst.

## Lizenz

MIT Lizenz, siehe [LICENSE.md](https://github.com/alexplusde/neues/blob/master/LICENSE.md)  

## Autor

**Alexander Walther**  
<http://www.alexplus.de>
<https://github.com/alexplusde>

**Projekt-Lead**  
[Alexander Walther](https://github.com/alexplusde)

## Credits

neues basiert auf: [YForm](https://github.com/yakamara/redaxo_yform)  
Danke an [Gregor Harlan](https://github.com/gharlan) für die Unterstützung
