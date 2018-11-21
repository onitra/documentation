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
```Override={view=MPIDView, type=SetProperty, target=delete_button, name=enabled, value=false```
* Neuer Eintrag Button deaktivieren:
```Override={view=MPIDView,type=SetProperty,target=new_button,name=enabled,value=false}```
* 1:1 Adresswechsel deaktivieren:
```Override={view=MPIDView,type=SetProperty,target=oneToOneAddresschange,name=enabled,value=false}```
* Export Button deaktivieren:
```Override={view=MPIDView,type=SetProperty,target=export_button,name=enabled,value=false}```

## WSDL
~~~ xml
<?xml version="1.0" encoding="UTF-8"?>
<wsdl:definitions name="SyncMaPaService" targetNamespace="http://nextlevel.com/webservices/syncmapa" xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/" xmlns:tns="http://nextlevel.com/webservices/syncmapa" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/">
    <wsdl:types>
    <xs:schema elementFormDefault="unqualified" targetNamespace="http://nextlevel.com/webservices/syncmapa" version="1.0" xmlns:ns1="http://nextlevel.com/webservices/SyncResponse" xmlns:tns="http://nextlevel.com/webservices/syncmapa" xmlns:xs="http://www.w3.org/2001/XMLSchema">
    <xs:import namespace="http://nextlevel.com/webservices/SyncResponse"/>

    <xs:element name="energyOperator" type="tns:energyOperator"/>
    <xs:element name="addEnergyOperators" type="tns:addEnergyOperators"/>
    <xs:element name="addEnergyOperatorsResponse" type="tns:addEnergyOperatorsResponse"/>

    <xs:complexType name="addEnergyOperators">
      <xs:sequence>
        <xs:element maxOccurs="unbounded" minOccurs="0" name="energyOperators" type="tns:energyOperator"/>
      </xs:sequence>
    </xs:complexType>

    <xs:complexType name="energyOperator">
      <xs:sequence>
        <xs:element name="referenceId" type="xs:int"/>
        <xs:element minOccurs="1" maxOccurs="1" name="name" type="xs:string"/>
        <xs:element minOccurs="0" name="partnerCode" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="systemCode" nillable="true" type="xs:string"/>
        <xs:element minOccurs="0" name="one2oneAddress" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="validFrom" nillable="true" type="xs:dateTime"/>
        <xs:element minOccurs="1" maxOccurs="1" name="validTo" nillable="true" type="xs:dateTime"/>
        <xs:element minOccurs="0" name="role" type="tns:role-type"/>
        <xs:element minOccurs="0" name="sector" type="tns:sector-type"/>
        <xs:element minOccurs="0" name="contact" type="tns:contact"/>
      </xs:sequence>
    </xs:complexType>

    <xs:complexType name="contact">
      <xs:sequence>
        <xs:element minOccurs="0" name="type" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="firstName" nillable="true" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="lastName" nillable="true" type="xs:string"/>
        <xs:element minOccurs="0" name="email" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="telephoneNumber" nillable="true" type="xs:string"/>
        <xs:element minOccurs="1" maxOccurs="1" name="validFrom" nillable="true" type="xs:dateTime"/>
        <xs:element minOccurs="1" maxOccurs="1" name="validTo" nillable="true" type="xs:dateTime"/>
      </xs:sequence>
    </xs:complexType>

    <xs:complexType name="addEnergyOperatorsResponse">
      <xs:sequence>
        <xs:element minOccurs="0" name="return" type="ns1:SyncResponse"/>
      </xs:sequence>
    </xs:complexType>

    <xs:complexType name="energyOperatorSyncResult">
      <xs:sequence>
        <xs:element minOccurs="0" name="faultMessage" type="xs:string"/>
        <xs:element name="referenceId" type="xs:int"/>
        <xs:element minOccurs="0" name="successful" type="xs:boolean"/>
      </xs:sequence>
    </xs:complexType>

    <xs:simpleType name="role-type">
      <xs:restriction base="xs:string">
        <xs:enumeration value="BIKO"/>
        <xs:enumeration value="BKV"/>
        <xs:enumeration value="EIV"/>
        <xs:enumeration value="LF"/>
        <xs:enumeration value="MGV"/>
        <xs:enumeration value="MSB"/>
        <xs:enumeration value="NB"/>
        <xs:enumeration value="RB"/>
        <xs:enumeration value="UNB"/>
      </xs:restriction>
    </xs:simpleType>

    <xs:simpleType name="sector-type">
      <xs:restriction base="xs:string">
        <xs:enumeration value="ELECTRICITY"/>
        <xs:enumeration value="GAS"/>
      </xs:restriction>
    </xs:simpleType>

    </xs:schema>
      <xs:schema targetNamespace="http://nextlevel.com/webservices/SyncResponse" version="1.0" xmlns:ns1="http://nextlevel.com/webservices/syncmapa" xmlns:xs="http://www.w3.org/2001/XMLSchema">

      <xs:import namespace="http://nextlevel.com/webservices/syncmapa"/>

      <xs:complexType name="SyncResponse">
        <xs:sequence>
          <xs:element name="success" type="xs:boolean"/>
          <xs:element minOccurs="0" name="faultMessage" type="xs:string"/>
          <xs:element maxOccurs="unbounded" minOccurs="0" name="syncStatusList" nillable="true" type="ns1:energyOperatorSyncResult"/>
        </xs:sequence>
      </xs:complexType>

    </xs:schema>
    </wsdl:types>
      <wsdl:message name="addEnergyOperatorsResponse">
        <wsdl:part name="parameters" element="tns:addEnergyOperatorsResponse"></wsdl:part>
      </wsdl:message>

      <wsdl:message name="addEnergyOperators">
        <wsdl:part name="parameters" element="tns:addEnergyOperators"></wsdl:part>
      </wsdl:message>

      <wsdl:portType name="SyncMaPa">
        <wsdl:operation name="addEnergyOperators">
          <wsdl:input name="addEnergyOperators" message="tns:addEnergyOperators">
        </wsdl:input>
          <wsdl:output name="addEnergyOperatorsResponse" message="tns:addEnergyOperatorsResponse">
        </wsdl:output>
        </wsdl:operation>
      </wsdl:portType>

      <wsdl:binding name="SyncMaPaServiceSoapBinding" type="tns:SyncMaPa">
        <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
        <wsdl:operation name="addEnergyOperators">
          <soap:operation soapAction="" style="document"/>
          <wsdl:input name="addEnergyOperators">
            <soap:body use="literal"/>
          </wsdl:input>
          <wsdl:output name="addEnergyOperatorsResponse">
            <soap:body use="literal"/>
          </wsdl:output>
        </wsdl:operation>
      </wsdl:binding>
    <wsdl:service name="SyncMaPaService">
      <wsdl:port name="SyncMaPaPort" binding="tns:SyncMaPaServiceSoapBinding">
        <soap:address location="http://localhost:8080/SyncMaPa/services"/>
      </wsdl:port>
    </wsdl:service>

    </wsdl:definitions>
~~~

## XML Aufruf Bespiel
~~~ xml
<soapenv:Envelope xmlns:soapenv="http://schemas.xmlsoap.org/soap/envelope/" xmlns:syn="http://nextlevel.com/webservices/syncmapa">
<soapenv:Header/>
<soapenv:Body>
  <syn:addEnergyOperators>
    <!--Zero or more repetitions:-->
    <energyOperators>
      <referenceId>1</referenceId>
      <name>Markpartner Name</name>
      <!--Optional:-->
      <partnerCode>1234567890123</partnerCode>
      <systemCode>3210987654321</systemCode>
      <!--Optional:-->
      <one2oneAddress>o@o.de</one2oneAddress>

      <!--Optional:-->
      <role>BIKO</role>
      <!--Optional:-->
      <sector>ELECTRICITY</sector>
      <!--Optional:-->
      <contact>
        <!--Optional:-->
        <type>CIN</type>
        <firstName>Ionut</firstName>
        <lastName>Popescu</lastName>
        <!--Optional:-->
        <email>i@p.ro</email>
        <telephoneNumber>03213551651</telephoneNumber>
        <validFrom>2001-10-26T19:32:52Z</validFrom>
        <validTo>2020-10-26T19:32:52Z</validTo>
      </contact>
    </energyOperators>
  </syn:addEnergyOperators>
</soapenv:Body>
</soapenv:Envelope>
~~~
