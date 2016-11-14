# SOSE-WSDL

## Tutorial files
You wan find here the source code for each step of the tutorial.
The final wsdl file is `weather.wsdl`

### Step 1: root definition

```xml
<?xml version="1.0" encoding="UTF-8" standalone="no"?>
<wsdl:definitions
 					name="weather"
					xmlns:soap="http://schemas.xmlsoap.org/wsdl/soap/"
					xmlns:tns="http://www.example.org/weather/"
					xmlns:wsdl="http://schemas.xmlsoap.org/wsdl/"
					xmlns:xsd="http://www.w3.org/2001/XMLSchema"
					targetNamespace="http://www.example.org/weather/">

  <!-- Definitions go here -->
</wsdl:definitions>
```

### Step 2: types definition
```xml
  <wsdl:types>
    <xsd:schema targetNamespace="http://www.example.org/weather/">
      <!-- Date -->
    <xs:element name="date" type="xs:date"/>
      <!-- Location (GPS) -->
      <xs:element name="location">
  	<xs:complexType>
  	  <xs:sequence>
  		<xs:element name="longitude" type="xs:decimal"/>
  		<xs:element name="latitude" type="xs:decimal"/>
  	  </xs:sequence>
  	</xs:complexType>
    </xs:element>
    <!-- Temperature (°C) -->
      <xs:element name="temperature" type="xs:decimal"/>
      <!-- Wind Speed (km/h) -->
      <xs:element name="wind" type="xs:decimal"/>
      <!-- Humidity (%) -->
      <xs:element name="humidity" type="xs:decimal"/>
      <!-- Sky = {sunny, cloudy, fog} -->
    <xs:element name="sky">
  	<xs:simpleType>
  	  <xs:restriction base="xs:string">
  		  <xs:enumeration value="sunny"/>
  		  <xs:enumeration value="cloudy"/>
  	    <xs:enumeration value="fog"/>
  	  </xs:restriction>
  	</xs:simpleType>
    </xs:element>
            <xsd:element name="getWeatherFault" type="xsd:string"></xsd:element>
        </xsd:schema>
  </wsdl:types>
```

### Step 3: messages definition
```xml
  <!-- LocationMessage -->
  <wsdl:message name="locationMessage">
    <wsdl:part name="arg" type="tns:location"/>
  </wsdl:message>
  <!-- WeatherMessage -->
  <wsdl:message name="weatherMessage">
    <wsdl:part name="date" type="tns:date"/>
    <wsdl:part name="temperature" type="tns:temperature"/>
    <wsdl:part name="wind" type="tns:wind"/>
    <wsdl:part name="humidity" type="tns:humidity"/>
    <wsdl:part name="sky" type="tns:sky"/>
  </wsdl:message>
```

### Step 4: port type and operations definition
```xml
  <wsdl:portType name="WeatherPortType">
    <!-- Subscribe -->
    <wsdl:operation name="subscribeWeather">
      <wsdl:input message="tns:weatherMessage"/>
    </wsdl:operation>
    <!-- Get -->
    <wsdl:operation name="getWeather">
      <wsdl:input message="tns:locationMessage"/>
      <wsdl:output message="tns:weatherMessage"/>
    </wsdl:operation>
    <!-- Sensing -->
    <wsdl:operation name="updateWeather">
  	  <wsdl:output message="tns:locationMessage"/>
      <wsdl:input message="tns:weatherMessage"/>
    </wsdl:operation>
    <!-- Alert -->
  	<wsdl:operation name="alertWeather">
  	  <wsdl:output message="tns:weatherMessage"/>
    </wsdl:operation>
  </wsdl:portType>
```

### Step 5: binding definition (without extensibility elements)
```xml
  <wsdl:binding type="tns:WeatherPortType" name="WeatherBinding">
      <!-- extensibility element 0 -->
      <wsdl:operation name="subscribeWeather">
        <!-- extensibility element 1 -->
        <wsdl:input>
          <!-- extensibility element 1.1 -->
        </wsdl:input>
      </wsdl:operation>
      <wsdl:operation name="getWeather">
        <!-- extensibility element 2 -->
        <wsdl:input>
          <!-- extensibility element 2.1 -->
        </wsdl:input>
        <wsdl:output>
          <!-- extensibility element 2.2 -->
        </wsdl:output>
      </wsdl:operation>
      <wsdl:operation name="updateWeather">
        <!-- extensibility element 3 -->
        <wsdl:output>
          <!-- extensibility element 3.1 -->
        </wsdl:output>
        <wsdl:input>
          <!-- extensibility element 3.2 -->
        </wsdl:input>
      </wsdl:operation>
      <wsdl:operation name="alertWeather">
        <!-- extensibility element 4 -->
        <wsdl:output>
          <!-- extensibility element 4.1 -->
        </wsdl:output>
      </wsdl:operation>
  </wsdl:binding>
```

### Step 6: service definition
```xml
  <wsdl:service name="weather">
    <wsdl:port binding="tns:WeatherBinding" name="WeatherService">
      <soap:address location="http://www.example.org/"/>
    </wsdl:port>
  </wsdl:service>
 ``` 
### Step 7: SOAP binding
```xml
  <wsdl:binding type="tns:WeatherPortType" name="WeatherBinding">
      <soap:binding style="document" transport="http://schemas.xmlsoap.org/soap/http"/>
      <wsdl:operation name="subscribeWeather">
        <soap:operation soapAction="http://www.example.org/weather/subscribeWeather"/>
        <wsdl:input>
          <soap:body use="literal"/>
        </wsdl:input>
      </wsdl:operation>
      <wsdl:operation name="getWeather">
        <soap:operation soapAction="http://www.example.org/weather/getWeather"/>
        <wsdl:input>
          <soap:body use="literal"/>
        </wsdl:input>
        <wsdl:output>
          <soap:body use="literal"/>
        </wsdl:output>
      </wsdl:operation>
      <wsdl:operation name="updateWeather">
        <soap:operation soapAction="http://www.example.org/weather/updateWeather"/>
        <wsdl:output>
          <soap:body use="literal"/>
        </wsdl:output>
        <wsdl:input>
          <soap:body use="literal"/>
        </wsdl:input>
      </wsdl:operation>
      <wsdl:operation name="alertWeather">
        <soap:operation soapAction="http://www.example.org/weather/alertWeather"/>
        <wsdl:output>
          <soap:body use="literal"/>
        </wsdl:output>
      </wsdl:operation>
  </wsdl:binding>
   ``` 

