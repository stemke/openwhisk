---

copyright:
  years: 2016, 2018
lastupdated: "2018-02-14"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Einstieg in {{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk}} ist ein verteilter, ereignisgesteuerter Berechnungsservice (auch serverunabhängiges Computing oder Function as a Service (FaaS) bezeichnet). {{site.data.keyword.openwhisk_short}} führt Anwendungslogik als Reaktion auf Ereignisse oder direkte Aufrufe über das Web oder mobile Apps über HTTP aus. Ereignisse können von {{site.data.keyword.Bluemix}}-Services wie Cloudant und von externen Quellen bereitgestellt werden. Entwickler können sich auf das Schreiben von Anwendungslogik sowie auf das Erstellen von Aktionen, die auf Anforderung ausgeführt werden, konzentrieren.
Der Hauptvorteil dieses neuen Konzepts besteht darin, dass Sie keine Server explizit bereitstellen. Auf diese Weise brauchen Sie sich weder um automatische Skalierung noch um hohe Verfügbarkeit, Aktualisierungen und Wartungen zu kümmern, und es fallen keine Kosten für Prozessorzeit an, während deren Ihr Server zwar aktiv ist, jedoch keine Anforderungen verarbeitet.
Ihr Code wird immer ausgeführt, wenn ein HTTP-Aufruf, eine Änderung eines Datenbankstatus oder ein anderer Typ von Ereignis eingeht, der die Ausführung Ihres Codes auslöst.
Die Ausführungszeit wird Ihnen in Millisekunden (aufgerundet auf die nächsten 100 ms) in Rechnung gestellt und nicht pro Stunde VM-Nutzung und völlig ungeachtet dessen, ob VM nützliche Operationen ausgeführt hat oder nicht, berechnet.
{: shortdesc}

Dieses Programmiermodell ist eine perfekte Anpassung an Microservices, mobile Apps, IoT-Apps und viele andere Apps. Sie erhalten sofort nutzbare Auto-Scaling- und Lastverteilungsfunktionen, ohne Cluster, Lastverteilungsfunktionen, HTTP-Plug-ins usw. manuell konfigurieren zu müssen. Wenn Sie dann auch noch in {{site.data.keyword.openwhisk}} arbeiten, haben Sie außerdem den Vorteil, keinen Verwaltungsaufwand treiben zu müssen, da sämtliche Hardware, Netzfunktionalität und Software von IBM gewartet wird. Sie müssen nur noch den Code bereitstellen, den Sie ausführen wollen, und an {{site.data.keyword.openwhisk}} übergeben. Der Rest geht wie von selbst. Eine gute Einführung in das serverunabhängige Programmiermodell finden Sie im [Blog von Martin Fowler](https://martinfowler.com/articles/serverless.html).

Sie können auch den [Apache OpenWhisk-Quellcode](https://github.com/openwhisk/openwhisk) erhalten und das System selbst ausführen.

Weitere Einzelheiten zur Funktionsweise von {{site.data.keyword.openwhisk_short}} finden Sie unter [Informationen zu {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Sie können den Browser oder die CLI (Command-Line Interface) verwenden, um Ihre {{site.data.keyword.openwhisk_short}}-Anwendungen zu entwickeln.
Beide Komponenten haben ein ähnliches Leistungsspektrum in Hinblick auf die Entwicklung von Anwendungen. Die CLI bietet ein höheres Maß an Kontrolle über die Bereitstellung und die Operationen.

## Im eigenen Browser entwickeln
{: #openwhisk_start_editor}

Testen Sie {{site.data.keyword.openwhisk_short}} in Ihrem [Browser](https://console.{DomainName}/openwhisk/actions), um Aktionen zu erstellen, Aktionen durch Auslöser zu automatisieren und öffentliche Pakete zu untersuchen. Besuchen Sie die Seite [Weitere Informationen](https://console.{DomainName}/openwhisk/learn), auf der Sie eine Schnelleinführung zur {{site.data.keyword.openwhisk_short}}-Benutzerschnittstelle finden.

## Über die CLI entwickeln
{: #openwhisk_start_configure_cli}

Sie können Ihren Namensbereich und Ihren Berechtigungsschlüssel über die {{site.data.keyword.openwhisk_short}}-Befehlszeilenschnittstelle einrichten.
Navigieren Sie zu [CLI konfigurieren](https://console.{DomainName}/openwhisk/cli) und gehen Sie gemäß den Anweisungen für die Installation vor.

## Übersicht
{: #openwhisk_start_overview}
- [Funktionsweise von OpenWhisk](./openwhisk_about.html)
- [Häufige Anwendungsfälle für serverunabhängige Anwendungen](./openwhisk_use_cases.html)
- [OpenWhisk-CLI einrichten und verwenden](./openwhisk_cli.html)
- [OpenWhisk über eine iOS-App verwenden](./openwhisk_mobile_sdk.html)
- [Artikel, Beispiele und Lernprogramme](https://github.com/openwhisk/openwhisk-external-resources)
- [Apache OpenWhisk - FAQ](http://openwhisk.org/faq)
- [Preisstruktur](https://console.ng.bluemix.net/openwhisk/learn/pricing)

## Programmiermodell
{: #openwhisk_start_programming}
- [Systemdetails](./openwhisk_reference.html)
- [Katalog der durch OpenWhisk bereitgestellten Services](./openwhisk_catalog.html)
- [Aktionen](./openwhisk_actions.html)
- [Auslöser und Regeln](./openwhisk_triggers_rules.html)
- [Feeds](./openwhisk_feeds.html)
- [Pakete](./openwhisk_packages.html)
- [Annotationen](./openwhisk_annotations.html)
- [Webaktionen](./openwhisk_webactions.html)
- [API-Gateway](./openwhisk_apigateway.html)
- [Entitätsnamen](./openwhisk_reference.html#openwhisk_entities)
- [Aktionssemantik](./openwhisk_reference.html#openwhisk_semantics)
- [Begrenzungen](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}}-Beispiel 'Hello World'
{: #openwhisk_start_hello_world}
Für den Einstieg in {{site.data.keyword.openwhisk_short}} können Sie das folgende Beispiel für JavaScript-Code ausprobieren.

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Führen Sie die folgenden Schritte aus, um dieses Beispiel zu verwenden:

1. Speichern Sie den Code in einer Datei. Beispiel: *hello.js*.

2. Erstellen Sie die Aktion, indem Sie über die Befehlszeile der {{site.data.keyword.openwhisk_short}}-CLI den folgenden Befehl eingeben:
    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Rufen Sie dann die Aktion auf, indem Sie die folgenden Befehle eingeben.
    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Dieser Befehl liefert die folgende Ausgabe:
    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Dieser Befehl liefert die folgende Ausgabe:
    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

Sie können darüber hinaus die ereignisgesteuerten Funktionen in {{site.data.keyword.openwhisk_short}} verwenden, um diese Aktion als Reaktion auf Ereignisse aufzurufen. Gehen Sie wie im [Beispiel für den Alarmservice](./openwhisk_packages.html#openwhisk_package_trigger) beschrieben vor, um eine Ereignisquelle zu konfigurieren, sodass die Aktion `hello` jedes Mal aufgerufen wird, wenn ein regelmäßiges Ereignis generiert wird.

Eine vollständige Liste von [OpenWhisk-Lernprogrammen und -Beispielen finden Sie hier](https://github.com/openwhisk/openwhisk-external-resources#sample-applications). Neben Beispielen enthält dieses Repository auch Links zu Artikeln, Präsentationen, Podcasts, Videos und anderen Ressourcen zu {{site.data.keyword.openwhisk_short}}.

## API-Referenz
{: #openwhisk_start_api notoc}
* [REST-API-Dokumentation](./openwhisk_reference.html#openwhisk_ref_restapi)
* [REST-API](https://console.{DomainName}/apidocs/98)

## Zugehörige Links
{: #general notoc}
* [Entdecken Sie: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/)
* [{{site.data.keyword.openwhisk_short}} auf IBM developerWorks](https://developer.ibm.com/openwhisk/)
* [Apache {{site.data.keyword.openwhisk_short}}-Projektwebsite](http://openwhisk.org)
