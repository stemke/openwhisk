---

copyright:
  years: 2016, 2018
lastupdated: "2018-01-09"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete Weather
{: #openwhisk_catalog_weather}

El paquete `/whisk.system/weather` ofrece una forma cómoda de invocar la API de Weather Company Data para {{site.data.keyword.Bluemix}}.
{: shortdesc}

El paquete incluye la acción siguiente.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/weather` | Paquete | usuario, contraseña | Servicios de la API de Weather Company Data para {{site.data.keyword.Bluemix_notm}}  |
| `/whisk.system/weather/forecast` | Acción | latitude, longitude, timePeriod | Previsión para el periodo de tiempo indicado|

Se recomienda la creación de un enlace de paquete con los valores de `username` y `password`. Así, no necesita especificar las credenciales cada vez que invoque las acciones del paquete.

## Configuración del paquete de Weather en {{site.data.keyword.Bluemix_notm}}

Si utiliza OpenWhisk desde {{site.data.keyword.Bluemix_notm}}, OpenWhisk crea automáticamente enlaces de paquete para sus instancias de servicio de {{site.data.keyword.Bluemix_notm}} Weather.

1. Cree una instancia de servicio de Weather Company Data en su [panel de control](http://console.ng.Bluemix.net) de {{site.data.keyword.Bluemix_notm}}.
  
  Asegúrese de recordar el nombre de la instancia de servicio y la organización y el espacio de
{{site.data.keyword.Bluemix_notm}} en el que se encuentra.
  
2. Actualizar los paquetes de su espacio de nombres. La renovación crea automáticamente un enlace de paquete para la instancia de servicio de Weather Company Data que ha creado.
  
  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_Weather_Company_Data_Credentials-1
  ```
  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Weather Bluemix_Weather_Company_Data_Credentials-1 private
  ```
  
 
## Configuración de un paquete de Weather fuera de {{site.data.keyword.Bluemix_notm}}

Si no utiliza OpenWhisk en {{site.data.keyword.Bluemix_notm}} o si quiere configurar el servicio Weather Company Data fuera de {{site.data.keyword.Bluemix_notm}}, debe crear manualmente un enlace de paquete para el servicio Weather Company Data. Necesita el nombre de usuario del servicio del servicio Weather Company Data y la contraseña.

- Cree un enlace de paquete configurado para el servicio de Watson Translator.

  ```
  wsk package bind /whisk.system/weather myWeather -p username MYUSERNAME -p password MYPASSWORD
  ```
  {: pre}


## Obtención de la previsión meteorológica para una ubicación
{: #openwhisk_catalog_weather_forecast}

La acción `/whisk.system/weather/forecast` devuelve una previsión meteorológica para un lugar,
invocando la API de The Weather Company. Los parámetros son según se indica a continuación:

- `username`: nombre de usuario de The Weather Company Data para {{site.data.keyword.Bluemix_notm}} que tiene autorización para invocar la API de previsión meteorológica.
- `password`: contraseña de The Weather Company Data para {{site.data.keyword.Bluemix_notm}} que tiene autorización para invocar la API de previsión meteorológica.
- `latitude`: la coordenada de latitud de la ubicación.
- `longitude`: la coordenada de longitud de la ubicación.
- `timePeriod`: periodo de tiempo de la previsión. Las opciones válidas son:
  - `10day` - (predeterminado) Devuelve una previsión diaria de 10 días.
  - `48hour` - Devuelve una previsión horaria de 2 días.
  - `current` - Devuelve las condiciones meteorológicas actuales.
  - `timeseries` - Devuelve tanto observaciones actuales como observaciones pasadas para un máximo de 24 horas a partir de la fecha y hora actuales.


El siguiente ejemplo muestra cómo crear un enlace de paquete y luego obtener de una previsión a 10 días.

- Invocar la acción `forecast` en su enlace de paquete para obtener la previsión meteorológica.
  ```
  wsk action invoke myWeather/forecast --result \
  --param latitude 43.7 \
  --param longitude -79.4
  ```
  {: pre}
  
  ```json
  {
      "forecasts": [
          {
              "dow": "Wednesday",
              "max_temp": -1,
              "min_temp": -16,
              "narrative": "Chance of a few snow showers. Highs -2 to 0C and lows -17 to -15C.",
              ...
          },
          {
              "class": "fod_long_range_daily",
              "dow": "Thursday",
              "max_temp": -4,
              "min_temp": -8,
              "narrative": "Mostly sunny. Highs -5 to -3C and lows -9 to -7C.",
              ...
          },
          ...
      ],
  }
  ```
  
