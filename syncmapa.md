---
myurl: http://b2bbp.next-level-help.org/b2b_mpid_syncmapa_webservice.html
title: Webservice zur Befüllung der Marktpartner
keywords: mpid, marktparner, energyoperator, webservice, cxf, bdew
tags: [getting_started]
sidebar: nav_home.html
permalink: index.html
summary: internal Informationen
last_committer: ndonthiNLI
last_updated: 2017-10-06:15:14:24
folder: home
disqus: no
permalink: b2b_mpid_syncmapa_webservice.md
---

# Webservice zur Befüllung der Marktpartner

Alternativ zur Befüllung der Marktpartner aus der UI ist es möglich, die Marktpartner über Webser-vice zu befüllen. Dieser Webservice stellt aktuell eine Methode zur Übergabe von einer Liste von Marktpartner zur Verfügung.

## Auslieferung

Der Webservice ist ein Content, welcher durch NLI bereitgestellt werden kann.

## Einrichtung

Die Einrichtung und Konfiguration der Webservices ist in folgender Dokumentation allgemein be-schrieben:
[Webservice (Receiver)](http://b2bbp.next-level-help.org/b2b_cust_CXFDynamicReceiverServlet.html)
Folgende Konfiguration kann benutzt werden:
<table>
  <tr>
    <th>Eigenschaft</th>
    <th>Wert</th>
    <th>Beschreibung</th>
  </tr>
  <tr>
    <td>Provider</td>
    <td>NLI</td>
    <td></td>
  </tr>
  <tr>
    <td>Version</td>
    <td>1.0</td>
    <td></td>
  </tr>
    <tr>
    <td>Typ</td>
    <td>CXF</td>
    <td></td>
  </tr>
    <tr>
    <td>Format</td>
    <td>WebService</td>
    <td></td>
  </tr>
    <tr>
    <td>Fromat Version</td>
    <td>1</td>
    <td></td>
  </tr>
    <tr>
    <td>Zielformat</td>
    <td>syncmapa</td>
    <td></td>
  </tr>
    <tr>
    <td>Document</td>
    <td>Die syncmapa jar</td>
    <td></td>
  </tr>
</table>

### Customizing
Folgende GlobalProperty kann konfiguriert werden
<table>
  <tr>
    <td>B3P_MPID_DATA_FROM_DB</td>
    <td>"true" oder "false" (Default false)</td>
    <td>Ist dieser Wert auf “true“ gesetzt werden die Marktpartner aus der Databanktabelle B2BBP_DATA_MP ermittelt.</td>
  </tr>
</table>

### Overrides & Erweiterungen
Falls die GlobalProperty B3P_MPID_DATA_FROM_DB auf true gesetzt ist, können Marktpartner aus B2BBP nicht mehr editiert werden. Folgende Overrides müssen eingerichtet werden:  
* Löschen Button deaktivieren:  
\* Override={view=MPIDView, type=SetProperty, target=delete_button, name=enabled, value=false
