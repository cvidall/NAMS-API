






EVOLUTIVOS DE SNSFARMA
Departamento de Desarrollo
Referencia Documento: ET – XXXXX – GUI-1.1.0.docx








Este documento ha sido elaborado en la Dirección General de Salud Digital y Sistemas de Información para el Sistema Nacional de Salud. No está permitida la reproducción total o parcial de esta publicación por cualquier medio, ya sea mecánico o electrónico, fotocopias, etc. incluyendo esta prohibición la traducción, el uso de ilustraciones, y el almacenamiento en bases de datos, sin permiso expreso y por escrito de la Dirección General de Salud Digital y Sistemas de Información para el Sistema Nacional de Salud.
 
Histórico de versiones:

Versión	Descripción cambio	Autor
Fecha	Revisado por
Fecha	Aprobado por
Fecha
1.0	Documento inicial	Getronics
22/05/2025		
1.1	Versión revisada	Getronics
28/05/2025		
1.2	Modificaciones:
2.11.4 Enlaces de interés 
Se añade el enlace de la AEMPS sobre identificadores únicos
2.11.6 Enlace contacto notificaciones.
Se añade el enlace Contacto Notificaciones
He dejado visibles los puntos 2.10 y 2.12 para enviárselos a Jose Antonio Benito	Getronics
29/05/2025		
				
				
				
				
				
				
				
				

 
ÍNDICE

1	INTRODUCCIÓN	5
1.1	OBJETIVO	5
1.2	ALCANCE	5
1.3	RELACIONES CON OTROS DOCUMENTOS	5
1.4	DESTINATARIOS	5
2	RELACIÓN DE EVOLUTIVOS A DESARROLLAR EN LA GUI	6
2.1	MEJORAS PANTALLA INTRODUCCIÓN DATOS ESCÁNER	6
2.1.1	Fecha caducidad	6
2.1.2	Pantalla mensaje Warning	6
2.2	EXPORTAR A EXCEL	7
2.3	EXPORTAR A CSV.	7
2.4	CAMPOS BUSCAR EN LOS LISTADOS.	8
2.5	CONSULTA DE LOS DATOS DE USUARIO	9
2.6	ACTUALIZACIÓN CÓDIGOS ERROR ESPAÑOL.	10
2.7	FECHA ÚLTIMO ACCESO	11
2.8	BAJA USUARIOS SNSFARMA	11
2.9	BÚSQUEDA OPERACIONES REALIZADAS	12
2.10	TRADUCCIÓN APLICACIÓN 4 IDIOMAS OFICIALES	13
2.11	FOOTER (PIE) DE LA APLICACIÓN	13
2.11.1	Mapa web	14
2.11.2	Política privacidad SNSFARMA	14
2.11.3	Política de cookies	14
2.11.4	Enlaces de interés	14
2.11.5	Enlace a requisitos técnicos.	14
2.11.6	Enlace contacto notificaciones	14
2.12	AUDITORÍA DE ACCESOS DE LOS USUARIOS GUI	15
2.13	AYUDA, PREGUNTAS FRECUENTES Y VÍDEOS	16



1	INTRODUCCIÓN
1.1	Objetivo
El objetivo del documento es detallar los evolutivos a desarrollar en la aplicación SNSFARMA-GUI versión 1.1.0 dentro del ET – XXXXXXX.
1.2	Alcance
Departamento de Desarrollo de la SGTI
1.3	Relaciones con otros documentos
No aplica
1.4	Destinatarios
Este documento va dirigido a los responsables funcionales de la aplicación, al equipo de soporte y responsables del proyecto


2	RELACIÓN DE EVOLUTIVOS A DESARROLLAR EN LA GUI

2.1	Traducción aplicación 4 idiomas oficiales
Español, Catalán, Euskera y Gallego.  
A cada usuario se le asignaría un idioma por defecto al darlo de alta. El usuario podría modificar el idioma por defecto. En la cabecera en los datos del usuario se añadiría “Idioma”.
Funcionamiento
-	A cada usuario se le asignará un idioma por defecto al darse de alta. Se modificarán las pantallas de gestión de usuarios en el la aplicación de SNSFARMA-PORTAL para poder gestionar el idioma de cada usuario. 
-	El usuario podrá modificar su idioma por defecto en cualquier momento.
-	En la cabecera, dentro de los datos del usuario, se añadirá el campo "Idioma".

 
Interfaz de cambio de idioma
El campo de idioma contendrá un enlace que, al seleccionarlo, mostrará las opciones disponibles para cambiar el idioma. Al modificarlo, la aplicación se mostrará automáticamente en el nuevo idioma seleccionado.
Alcance de la traducción
Se traducirán únicamente los textos de la interfaz de la aplicación. No se incluyen en esta fase:
-	Los datos de los listados
-	Los mensajes de error

Implementación técnica
Se utilizarán archivos properties para cada idioma:Gui_es.properties
GUI_ca.properties
GUI_xx.properties

Un ejemplo de este fichero para el español sería
menu_home = Inicio
manual_boton_enviar= Enviar
manual_label_producto=Código de producto

Proceso de implementación
Crear todos los archivos properties correspondientes a cada idioma.
Implementar la lógica para obtener el texto en el idioma seleccionado por el usuario.
Recorrer toda la aplicación para sustituir los textos estáticos por llamadas a los archivos properties.

Carmen Pérez comenta: “Opino que hay que comentar con José Antonio Benito si se descartan o se dejan para más adelante, porque en principio no los veo necesarios”

2.2	 Auditoría de accesos de los usuarios GUI
En SNSFARMA-GUI guardamos actualmente en la tabla SNSFGUI_ACCESOS los accesos de un usuario a la aplicación. Por ejemplo, tenemos para un usuario, el día y hora de cada acceso a la aplicación SNSFARMA-GUI. 

 

También guardamos las operaciones Manuales y con Escáner realizadas por cada usuario en una tabla de operaciones.
Se propone registrar además de lo anterior, cada pantalla visitada por el usuario y cada botón pulsado (incluido el cierre de sesión). Con ello se lograría:
-	Analizar el comportamiento del usuario: identificar las funcionalidades más utilizadas y aquellas que no se usan.
-	Mejorar la experiencia de usuario: al conocer qué botones se utilizan con mayor frecuencia, se puede optimizar el diseño de la interfaz.
-	Detectar posibles errores: por ejemplo, si los usuarios acceden repetidamente a una página, pero no interactúan con ella, podría haber un fallo funcional o de usabilidad.
-	Desde el Portal, los administradores de usuarios (GUI/NAMS)  podrían consultar estas estadísticas por usuario para conocer qué funciones se utilizan y con qué frecuencia.

Tendremos una tabla con cada acción posible en cada menú o pantalla
Por ejemplo:
Id_accion. Será el identificador único de una acción. Manual_b_enviar. Las acciones serán de menú: menú_pantalla_manual, etc.
Un botón : manual_b_enviar
Un enlace: manual_e_limpiar
Fecha. Fecha y hora que se ha realizado la operación.
Usuario. Usuario que ha realizado la acción.
Se auditarán tanto los botones que realicen acciones de BackeEnd como de FrontEnd
Estos datos se podrán consultar dese alguna pantalla del portal
Carmen Pérez dice: “Opino que hay que comentar con José Antonio Benito si se descartan o se dejan para más adelante, porque en principio no los veo necesarios”

2.3	 Ayuda, preguntas frecuentes y vídeos
 

Este enlace nos llevará a una página  de preguntas frecuentes, donde se mostrarán las dudas más comunes junto con sus respectivas respuestas.
Además de estas respuestas, la página incluirá videos explicativos   sobre el funcionamiento de las principales funcionalidades de la aplicación, tales como:
-	Introducción manual de datos y ejecución de operaciones, con sus respectivos resultados. Las distintas posibilidades y errores (al menos 3 operaciones + export Excel)

-	Introducción de datos mediante escáner y ejecución de operaciones, también con sus resultados.(6 operaciones)

-	Búsqueda de operaciones. Vídeo de ejemplo de búsqueda de operaciones y el listado obtenido.

-	Otras funcionalidades. Acceso a la aplicación, acceso a los distintos enlaces del footer (pie) de la aplicación.

Al menos 14 vídeos
Manual (4 vídeos: 3 operciones + export excel)
Escaner (6 operaciones: 6 vídeos)
Busqueda operaciones (1 vídeo)
Acceso aplicación, Menú, enlaces pie (3 vídeos)
+-1 día por vídeo
2.4	Cabecera
En la cabecera en los datos del usuario se muestran los siguientes datos:
 
Último acceso, Grupo, Agente y Centro. 
Según el manual de la GUI 
https://snsfarma-guidvd-jee-r01a-iq-vs-1.msc.es/snsfarma-gui-recursos/pdf/SNSFarma_ManualUsuarioGUI.pdf
En el punto 3.3 Grupo-Perfil se indica:
"Solamente accederán al Portal GUI los Usuarios que pertenezcan al Grupo Agentes de verificación Perfil Usuario GUI”. 
Propuesta: Eliminar el campo "Grupo" de los datos de usuario mostrados en la cabecera, al igual que no se muestra el perfil, dado que estos valores siempre serán los mismos para todos los usuarios con acceso a la aplicación.

2.5	Pantalla introducción datos manual
2.5.1	Mejora fichero Excel
Propuesta: Inmovilizar la primera fila del fichero Excel exportado.
La inmovilización de filas en Microsoft Excel es una funcionalidad que permite mantener visible una o más filas (típicamente encabezados) mientras se desplaza el contenido del documento. A continuación se detallan las ventajas de esta práctica:
-	Al mantener los encabezados visibles de forma constante, se elimina la necesidad de desplazarse continuamente hacia arriba para verificar el significado de cada columna.
-	En documentos con cientos o miles de filas, la inmovilización de encabezados resulta esencial para mantener el contexto durante el análisis de datos situados en posiciones alejadas del inicio del documento.
-	Los archivos con filas inmovilizadas demuestran atención al detalle y consideración hacia otros usuarios que deban trabajar con el documento, mejorando la calidad y usabilidad de los entregables.
2.5.2	Nuevo diseño para mostrar resultados de una operación
En la pantalla se distinguen 2 partes:
1.Introducción de datos: Formulario para introducción de datos del producto y botones de acciones. Además cuando se realiza una operación los resultados de la operación se muestran dentro del formulario de introducción de datos, no se muestra qué operación se ha realizado. En la imagen se resalta esta parte con el cuadrado en rojo.

2.Listado de Operaciones. Listado con las operaciones realizadas (en cuadrado verde)

 

Propuesta. Lo que se propone es modificar el diseño para tener 3 partes mejor diferenciadas para el usuario. Las 3 partes serían :
1.Introducción de datos: Formulario para introducción de datos del producto y botones de acciones. En rojo en la imagen. 
2. Resultado operación. Se indicaría el nombre de la operación que se ha realizado, su resultado y su subcódigo si ha habido. En azul en la imagen
3. Listado de Operaciones. En verde en la imagen
El diseño quedaría como la imagen siguiente:

 

Con esta división en tres partes el usuario puede ver más claramente la operación realizada y su resultado.
Al pulsar Limpiar en el formulario de introducción de datos se quitaría la parte de Resultado.
2.5.3	Mejora campo CITE
El CITE es el identificador de una Comunidad, cada comunidad tiene el suyo. Al seleccionar el check CIPA/CITE se muestra el campo CITE para introducirlo. En el caso de las Oficinas de Farmacia si la operación es Desactivar este campo es obligatorio.
Se puede ver este campo en la siguiente imagen:
 

Propuesta. Se modificará el campo CITE para que por defecto muestre el CITE de la Comunidad Autónoma del centro del usuario. 
Se añade al lado del campo CITE el enlace Buscar CITE.
 
Al pulsar este enlace se muestra una pantalla modal con las Comunidades autónomas y su CITE. Al seleccionar uno de los CITE se introducirá en el campo CITE.
 

Al pulsar en el Check seleccionamos el CITE y se pone en el campo CITE.
Para que esto funcione tenemos en base de datos una tabla que relaciona el CITE con su Comunidad Autónoma. 
  
2.6	Pantalla introducción datos escáner
2.6.1	Mejora fichero Excel
Propuesta: Inmovilizar la primera fila del fichero Excel exportado.
La inmovilización de filas en Microsoft Excel es una funcionalidad que permite mantener visible una o más filas (típicamente encabezados) mientras se desplaza el contenido del documento. A continuación se detallan las ventajas de esta práctica:
-	Al mantener los encabezados visibles de forma constante, se elimina la necesidad de desplazarse continuamente hacia arriba para verificar el significado de cada columna.
-	En documentos con cientos o miles de filas, la inmovilización de encabezados resulta esencial para mantener el contexto durante el análisis de datos situados en posiciones alejadas del inicio del documento.
-	Los archivos con filas inmovilizadas demuestran atención al detalle y consideración hacia otros usuarios que deban trabajar con el documento, mejorando la calidad y usabilidad de los entregables.

2.6.2	Nuevo diseño para mostrar resultados de una operación
Mismo cambio de diseño que en la pantalla de Introducción datos manual indicado en el punto 2.5.2 Nuevo diseño para mostrar resultados operación
2.6.3	Añadir campo CIPSNS / CIPA-CITE
Poner el CIPSNS en la pantalla de introducción datos escáner. En la de manual está. Creemos que sería necesario al igual que en la de manual ponerlo. En la operación de Desactivar que sea Obligatorio para la OF y opcional para las SF . Esto implica poner el CIPA y CITE en esta pantalla.
2.6.4	Mejora campo CITE
Si se añade el campo CIPSNS / CIPA-CITE entonces se puede hacer un desplegable en el campo CITE como en la pantalla Introducción datos manual – 2.5.3 Mejora campo CITE

2.7	Pantalla Búsqueda operaciones 
2.7.1	Mejora fichero Excel
Propuesta: Inmovilizar la primera fila del fichero Excel exportado.
La inmovilización de filas en Microsoft Excel es una funcionalidad que permite mantener visible una o más filas (típicamente encabezados) mientras se desplaza el contenido del documento. A continuación se detallan las ventajas de esta práctica:
-	Al mantener los encabezados visibles de forma constante, se elimina la necesidad de desplazarse continuamente hacia arriba para verificar el significado de cada columna.
-	En documentos con cientos o miles de filas, la inmovilización de encabezados resulta esencial para mantener el contexto durante el análisis de datos situados en posiciones alejadas del inicio del documento.
-	Los archivos con filas inmovilizadas demuestran atención al detalle y consideración hacia otros usuarios que deban trabajar con el documento, mejorando la calidad y usabilidad de los entregables..

