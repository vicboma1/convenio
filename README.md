# XXXina-suite

# Contribuciones
```
En este pequeño documento se definen el convenio que debe de seguir el desarrollador para que el código 
cumpla con unas métricas mínimas de calidad del software.

Así pues, se atiente a varios aspectos tanto a nivel de arquitectura, comportamiento, estructura...
```

## Arquitectura
```
Todo desarrollo que exponga un endPoint a cliente debe tener la siguiente estructura abstracta dentro de nuesta Api:

XXXXController (Clase):
    - Declaración de un logger
    - Post/Pre Constructor
    - Injección de un XXXXServicio (Interface)

XXXXServicioImpl (Clase):
    - Implementar un XXXXServicio (Interface)
    - Declaración de un logger
    - Post/Pre Constructor
    - Depedencias de la lógica de negocio
        - Injección de un XXXXRepositorio (GenericDao-NativeDao)
            - Declaración de un XXXXXQuery   
	- Injección de cualquier dependencia
	  [...]
		
XXXXXQuery (Clase):
    - Definición de QueryTemplateSpecs para traerno la lógica de negocio de la base de datos
    - Definición de un XXXXDTO

XXXXDTO (Clase):
    - Implementar Serializable
    - Implementar toString(), hashCode() y equals() => Eficiencia para el uso de Map/List...
	
XXXXJPA (Clase)

XXXXFactory (Clase):
    - Implementar método estático para crear 'new XXXX()'

XXXXBuilder (Clase)
    - Implementar método estático para manipular mapas, listas o relleno de objectos/clases...

XXXXConsts
    - Agrupar literales aislados dentro de un paquete
	
XXXXEnums
    - Implementar clase para agrupar literales que tengan cohesión/relación entre ellos mismos
```

## Paquetería
```
	- Definir naming por dominio
		- En caso de servicios
			- Carpeta Impl -> XXXXServicioImpl
			- Carpeta raiz dejamos caer las interfaces
	
```
## Estructurales
```

    - Refactors 'Non compliant' to 'compliant' para elevar el uso de las API's:
        -  @RequestMapping(path = "/XXX", method = RequestMethod.GET)       -> @GetMapping(path = "/XXX")
        -  @RequestMapping(path = "/XXX", method = RequestMethod.PUT)       -> @PutMapping(path = "/XXX")
        -  @RequestMapping(path = "/XXX", method = RequestMethod.DELETE)    -> @DeleteMapping(path = "/XXX")
        -  @RequestMapping(path = "/XXX", method = RequestMethod.POST)      -> @PostMapping(path = "/XXX")
		
	- Evitar usar '@Autowire' en el scope de la clase para las propiedades injectadas
	- Definir constructores '@Autowire' (IoC)
		- Declaraciones en el scope de la clase de tipo 'final'
	- Crear Interfaces de dominio (Segregación)
	- Crear clases abstracta para agrupar funcionalidad y evitar 'copy/pastes' (Dry-Open/Close)
```


 ## Tips
 ```
		- Definir métodos públicos de no más de 5 líneas (Kiss)
			- Definir métodos privados (lanzaderas) que encapsule esta lógica en caso de exceder las 5 líneas
		- Definir métodos privados de no más de 15 líneas
			- Particionar/desacoplar lógica
		- Evitar comentarios en medio del método
			- Creamos nuevo método privado y documentamos las aclaraciones en la cabecera 
		- Evitar acoplar en 15 líneas muchas cosas
			- Creamos métodos privado de dominio buscando el alcance de una sola cosa (Single-Responsability)
		- Parámetros con typeword 'final' en métodos públicos de implementaciones
        - Evitar usar constantes en los parámetros que contengan 'grupalidad', definir enumerados
		- Evitar hardcodear 'Strings', definir constantes aisladas
        - En métodos privados usar primitivas
		- Evitar declaración de 'new' en métodos privados.
			- Esto no se puede testear!!!!
			- Añadir parámetro nuevo en el método privado e injectar la dependencia desde el método superior.
```
