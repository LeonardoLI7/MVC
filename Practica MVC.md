# Modelo
Define qué datos debe contener la aplicación. Si el estado de estos datos cambia, el modelo generalmente notificará a la vista (para que la pantalla pueda cambiar según sea necesario) y, a veces, el controlador (si se necesita una lógica diferente para controlar la vista actualizada).

# Modelo de representación de los datos
Estructura lógica que adopta la base de base datos, incluyendo las relaciones y limitaciones que determinan cómo se almacenan y organizan y cómo se accede a los datos. Así mismo, un modelo de base de datos también define qué tipo de operaciones se pueden realizar con los datos, es decir, que también determina cómo se manipulan los mismos, proporcionando también la base sobre la que se diseña el lenguaje de consultas.
En general, prácticamente todos los modelos de base de datos pueden representarse a través de un diagrama de base de datos.

El modelo de base de datos relacional es uno de los más comunes. Este modelo es el que emplean las bases de datos relacionales y ordena los datos en tablas (relaciones) compuestas por columnas y filas.
Cada columna alberga un atributo de la entidad (nombre, dirección, fecha de nacimiento); a los atributos de una relación se los llama dominio. Escogiendo un atributo en concreto o una combinación de varios tenemos una clave primaria, a la que se puede hacer referencia en otras tablas, en las que será un clave externa.
En cada fila (tupla) se incluyen datos sobre una instancia específica de la entidad (por ejemplo, un cliente específico). Además, el modelo también representa el tipo de relaciones entre las tablas, que pueden ser uno a uno, uno a muchos o muchos a muchos.

# Funcionalidades de la aplicación
    1. Interfaz simple e intuitiva
    2. Tiempo de respuesta de procesos
    3. Actualización constante de la app
    4. Adaptación a sistemas operativos
    5. Geolocalización
    6. Seguridad y protección de datos
    7. Analítica y seguimiento
    8. Operación sin conexión de la aplicación: Offline
    9. Integración
    10. Personalización

# Infraestructura para el almacenamiento y recuperación de datos
Nos permite acceder a la información utilizando diferentes protocolos y modos de acceso, como pueden ser CIFS y NFS para el acceso a la información a nivel de fichero o FC, iSCSI y FCoE para acceder a la información a nivel de bloque. Esta variedad de protocolos y modos de acceso nos permite ofrecer a los sistemas que acceden al almacenamiento central la solución que mejor se adapta a sus necesidades.

La infraestructura de almacenamiento cuenta con funciones avanzadas de protección y eficiencia que nos permiten:

• Hacer snapshots a nivel de bloque.

• Hacer checkpoints a nivel de sistemas de ficheros.

• Hacer mirrors a nivel de bloque, tanto locales como remotos.

• Hacer réplicas a nivel de sistemas de ficheros, tanto locales como remotas.

• Maximizar la utilización del espacio disponible asignando almacenamiento cuando es necesario (virtual provisioning).

• Reducir el espacio de disco necesario para almacenar la información, comprimiendo los datos y eliminando las copias duplicadas, gracias a las capacidades de compresión y deduplicación.

• Estas medidas de protección se ven complementadas con el servicio de backup a cinta tradicional y el servicio de backup a disco prestado por la infraestructura de backup de la UC3M.

``` 
Modelo                                                             
function getLibro($id)                                                                
{                                                                  
$db = getConnection();                                          
$query = 'SELECT * FROM libros WHERE id = ?';                   
$stmt = $db->prepare($query);                          
$stmt->execute(array($id));                                    
$libro = $stmt->fetch();                                       
return $libro;                                                             
}    

Controlador                                                  
function ver ()                                                                
{                                                                  
if ( !isset ( $_GET [ 'id' ] ) )                                                                 
die("No has especificado un identificador de libro.");                                                                  
$id = $_GET [ 'id' ];                                                                    
//Incluimos el modelo correspondiente                          
require 'models/libros_model.php';                                                               
//Le pide al modelo el libro con id = $id                       
$libro = getLibro($id);                                                                 
if ($libro === null)                                                              
die("Identificador de libro incorrecto");                                                                    
//Pasamos a la vista toda la información que se desea representar                                                       include('views/libros_ver.php');                                  
}                     

Vista                                                          
<html>                                                          
<head>                                                  
<title>LIBRERIA UAZON</title>                                                              
</head>                                                    
<body>                                                             
<h1>Ver datos de un libro</h1>                                  
<table border="1">                                             
<tr>                                                       
<th>TITULO</th>                                           
<th>PRECIO</th>                                                    
</tr>                                                           
<tr>                                                           
<td><?php echo $libro['titulo'] ?></td>                        
<td><?php echo number_format($libro['precio'],2)?></td>            
</tr>                                                              
</table>                                                           
</body>                                                            
</html>                             

Controlador frontal index.php                                       
<?php                                                                
//La carpeta donde buscaremos los controladores                 
define ('CONTROLLERS_FOLDER', "controllers/");                      
//Si no se indica un controlador, este es el controlador que se usará                                                        
define ('DEFAULT_CONTROLLER', "libros");                             
//Si no se indica una acción, esta acción es la que se usará define ('DEFAULT_ACTION', "listar");                                 //Obtenemos el controlador.                                          
//Si el usuario no lo introduce, seleccionamos el de por defecto. $controller = DEFAULT_CONTROLLER;                                  if ( !empty ( $_GET[ 'controller' ] ) )                     
$controller = $_GET [ 'controller' ];                         
$action = DEFAULT_ACTION;                                            
// Obtenemos la acción seleccionada.                               
// Si el usuario no la introduce, seleccionamos la de por defecto.  if ( !empty ( $_GET [ 'action' ] ) )                             $action = $_GET [ 'action' ];                                                                   
//Ya tenemos el controlador y la accion                                                               
//Formamos el nombre del fichero que contiene nuestro controlador                                                   
$controller = CONTROLLERS_FOLDER . $controller . '_controller.php';  
//Si la variable ($controller) es un fichero lo requerimos                                                       
if ( is_file ( $controller ) )                                    
require_once ($controller)                                      
else                                                              
die ('El controlador no existe - 404 not found');                    
//Si la variable $action es una función la ejecutamos o detenemos el script                                                             if ( is_callable ($action) )                                        $action();                                                          else                                                               
die ('La accion no existe - 404 not found') 
```
# Vista
En el patrón de controlador de vista de modelos (MVC), la vista se encarga de la presentación de los datos y de la interacción del usuario. Una vista es una plantilla HTML con marcado incrustadoRazor. Razor el marcado es código que interactúa con el marcado HTML para generar una página web que se envía al cliente.

Recibir datos del modelo y los muestra al usuario.

Tienen un registro de su controlador asociado (normalmente porque además lo instancia).

Pueden dar el servicio de "Actualización()", para que sea invocado por el controlador o por el modelo (cuando es un modelo activo que informa de los cambios en los datos producidos por otros agentes).

• El usuario interactúa con la interfaz de usuario de alguna forma (por ejemplo, el usuario pulsa un botón, enlace, etc.)

• El controlador recibe (por parte de los objetos de la interfaz-vista) la notificación de la acción solicitada por el usuario. El controlador gestiona el evento que llega, frecuentemente a través de un gestor de eventos (handler) o callback.

• El controlador accede al modelo, actualizándolo, posiblemente modificándolo de forma adecuada a la acción solicitada por el usuario (por ejemplo, el controlador actualiza el carro de la compra del usuario). Los controladores complejos están a menudo estructurados usando un patrón de comando que encapsula las acciones y simplifica su extensión.

• El controlador delega a los objetos de la vista la tarea de desplegar la interfaz de usuario. La vista obtiene sus datos del modelo para generar la interfaz apropiada para el usuario donde se refleja los cambios en el modelo (por ejemplo, produce un listado del contenido del carro de la compra). El modelo no debe tener conocimiento directo sobre la vista. Sin embargo, se podría utilizar el patrón Observador para proveer cierta indirección entre el modelo y la vista, permitiendo al modelo notificar a los interesados de cualquier cambio. Un objeto vista puede registrarse con el modelo y esperar a los cambios, pero aun así el modelo en sí mismo sigue sin saber nada de la vista. 
El controlador no pasa objetos de dominio (el modelo) a la vista aunque puede dar la orden a la vista para que se actualice. Nota: En algunas implementaciones la vista no tiene acceso directo al modelo, dejando que el controlador envíe los datos del modelo a la vista.

• La interfaz de usuario espera nuevas interacciones del usuario, comenzando el ciclo nuevamente.

• El usuario realiza una solicitud a nuestro sitio web. Generalmente estará desencadenada por acceder a una página de nuestro sitio. Esa solicitud le llega al controlador.

• El controlador comunica tanto con modelos como con vistas. A los modelos les solicita datos o les manda realizar actualizaciones de los datos. A las vistas les solicita la salida correspondiente, una vez se hayan realizado las operaciones pertinentes según la lógica del negocio.

• Para producir la salida, en ocasiones las vistas pueden solicitar más información a los modelos. En ocasiones, el controlador será el responsable de solicitar todos los datos a los modelos y de enviarlos a las vistas, haciendo de puente entre unos y otros. Sería corriente tanto una cosa como la otra, todo depende de nuestra implementación; por eso esa flecha la hemos coloreado de otro color.

• Las vistas envían al usuario la salida. Aunque en ocasiones esa salida puede ir de vuelta al controlador y sería éste el que hace el envío al cliente, por eso he puesto la flecha en otro color.
# Controlador
Un controlador es responsable de controlar la forma en que un usuario interactúa con una aplicación MVC. Un controlador contiene la lógica de control de flujo para una aplicación ASP.NET MVC. Un controlador determina qué respuesta devolver a un usuario cuando un usuario realiza una solicitud del explorador.

• Recibe los eventos de entrada (un clic, un cambio en un campo de texto, etc.).

• Contiene reglas de gestión de eventos, del tipo "SI Evento Z, entonces Acción W". Estas acciones pueden suponer peticiones al modelo o a las vistas. Una de estas peticiones a las vistas puede ser una llamada al método "Actualizar()". Una petición al modelo puede ser "Obtener_tiempo_de_entrega ( nueva_orden_de_venta )". 

# Logica del negocio
La lógica del negocio, aparte de marcar un comportamiento cuando ocurren cosas dentro de un software, también tiene normas sobre lo que se puede hacer y lo que no se puede hacer. Eso también se conoce como reglas del negocio. Bien, pues en el MVC la lógica del negocio queda del lado de los modelos. Ellos son los que deben saber cómo operar en diversas situaciones y las cosas que pueden permitir que ocurran en el proceso de ejecución de una aplicación.

Por ejemplo, pensemos en un sistema que implementa usuarios. Los usuarios pueden realizar comentarios. Pues si en un modelo nos piden eliminar un usuario nosotros debemos borrar todos los comentarios que ha realizado ese usuario también. Eso es una responsabilidad del modelo y forma parte de lo que se llama la lógica del negocio.
