## Proteger claves y/o rutas

Para proteger claves o variables con información que no se quiere compartir en los repositorios públicos, la información se protege de la siguiente manera:

1. En el `gradle.properties` creamos la variable con la información
```gradle
ApiUrl = http://1xx.xx.x.xxx:xxxx/api/
```
2. En el `build.gradle(Module)` hacemos lo siguiente:
	2.1- Declaramos las variables 
	```gradle
    plugins {
    ...
    }
    
    def API_URL = '"' + ApiUrl + '"'?: '"Message Error"'
	def STRING = 'String'
    
    android {
    ...

    defaultConfig {
        ...
        testInstrumentationRunner "androidx.test.runner.AndroidJUnitRunner"

        each{
            type -> type.buildConfigField STRING, 'ApiUrl', API_URL
        }
        manifestPlaceholders = [
                API_URL : API_URL
        ]
    }
    ...
    ```
 3. En el `AndroidManifest.xml` antes de que del `Activity` debemos crear un `meta-data` así:
 	```xml
    <application
        ...
        <meta-data
            android:name=".com.c2r.delivery.Routes"
            android:value="{$API_URL}" />
        <activity
            ...
    ```
    4. Ahora vamos al lugar donde necesitamos crear la variable con el dato protegido y la declaramos de la siguiente manera:
    
    ```kotlin
    val API_URL = BuildConfig.ApiUrl
    ```
    Se debe tener en cuenta que si el IDE no reconoce la variable, debemos de reconstruir el proyecto con el martillo y problema solucionado.
 
 **Esta es una prueba realizada desde la tablet Lenovo Tab Smart yoga, utilizando termux y vim**
 
