# Guía de instalación

## Descargas

 - [Python](https://www.python.org/) (las versiones 2 y 3 son compatibles)
 - [SuperCollider 3.8](http://supercollider.github.io/download) y posteriores
 - [SC3 plugins](http://sc3-plugins.sourceforge.net/) (Algunas características interesantes adicionales para SuperCollider – recomendado pero no necesario)

## Instalación

Siga las instrucciones de instalación para descargar Python y SuperCollider. Al instalar Python, haga clic en **Sí** cuando se le pregunte si desea agregar Python a la ruta de su sistema y **sí**, si desea instalar *pip*: éste es usado para descargar/instalar automáticamente bibliotecas de Python, como FoxDot.

Instala la última versión de FoxDot desde el Python Package Index usando *pip* desde la línea de comandos (símbolo del sistema en Windows, terminal en MacOS y Linux) ejecutando:

`pip install FoxDot`

Alternativamente, puedes compilar desde el código fuente en GitHub y mantenerse, así, actualizado con la versión de desarrollo:

```
git clone https://github.com/Qirky/FoxDot.git
cd FoxDot
python setup.py install
```

Abre SuperCollider e instala `FoxDot Quark` (permite que FoxDot se comunique con SuperCollider -  requiere que Git esté instalado) escribiendo lo siguiente en el editor y presionando `Ctrl+Return` que "ejecuta" la línea de código:

`Quarks.install("FoxDot")`

Vuelve a compilar la biblioteca de clases SuperCollider yendo a Language -> Recompile Class Library o presionando `Ctrl+Shift+L`.

Si no está instalado Git, puedes descargar e instalar los Quarks necesarios de SuperCollider directamente desde GitHub ejecutando las 2 líneas de código a continuación en SuperCollider:

```Quarks.install("https://github.com/Qirky/FoxDotQuark.git")
Quarks.install("https://github.com/supercollider-quarks/BatLib.git")```

## Inicio

Abre SuperCollider y ejecuta lo siguiente (esto debe hacerse antes de abrir FoxDot), presionando `Ctrl+Return`:

`FoxDot.start`

SuperCollider está escuchando, ahora, mensajes de FoxDot. Para iniciar FoxDot desde la línea de comandos simplemente escribe:

`python -m FoxDot`

La interfaz de FoxDot debería abrirse y ¡ya estás listo para comenzar a practicar! Consulta la guía de inicio para obtener algunos consejos útiles sobre los conceptos básicos de FoxDot. Happy coding!

## Instalación de los SC3 Plugins

Los *Plugins SC3* son una colección de clases que amplían la ya enorme biblioteca de SuperCollider. Algunos de estos se utilizan para ciertos "efectos" en FoxDot (como bitcrush) y le darán un error en SuperCollider si intentas usarlos sin instalar los *plugins*. Los *Plugins SC3* se pueden descargar desde [aquí](http://sc3-plugins.sourceforge.net/). Una vez descargado, coloca la carpeta en la carpeta "Extensions" de SuperCollider y luego reinicia SuperCollider. Para encontrar la ubicación de la carpeta "Extensions", abre SuperCollider y ejecuta la siguiente línea de código:

`Platform.userExtensionDir`

Esto mostrará la ubicación de la carpeta "Extensions" en la "post window" de SuperCollider, que generalmente se sitúa en el lado derecho de la pantalla. Si este directorio no existe, crealo y coloca los *SC3 Plugins* allí y reinicia SuperCollider. La próxima vez que abras FoxDot, ves al menú desplegable "Idioma" y marca "Use SC3 Plugins". ¡Reinicia FoxDot y listo!

## Instalación con SuperCollider 3.7 o anterior

Si tienes problemas para instalar FoxDot Quark en SuperCollider, suele deberse, generalmente a que la versión de SuperCollider es antigua y no tiene la funcionalidad para instalar Quarks o no funciona correctamente. Si éste es el caso, puedes descargarlos desde el siguiente script de SuperCollider: [foxdot.scd](http://foxdot.org/wp-content/uploads/foxdot.scd). Una vez descargado, abre el archivo en SuperCollider y presione `Ctrl+Return` para ejecutarlo. Esto hará que SuperCollider empiece a escuchar mensajes de FoxDot.

## Instalación en GNU/Linux

Gran parte de la instalación (incluida Python y SuperCollider) se ha automatizado en un sencillo *script* de shell escrito por [Noisk8](https://github.com/Noisk8). Puedes descargar el *script* desde su GitHub, dónde además encontrás una explicación paso a paso del script y cómo ejecutarlo. Enlace aquí: <https://github.com/Noisk8/InstalandoFoxDot-En-linux> (**nota**:está en español)

Para obtener más respuestas a otras preguntas frecuentes, puedes consultar la [FAQ](http://foxdot.org/forum/?view=thread&id=1) en el [foro](http://foxdot.org/forum/) de FoxDot.

Puedes informar de cualquier problema o error en el [GitHub](https://github.com/Qirky/FoxDot/issues) del proyecto o si tienes alguna pregunta, siéntase libre en dejar un mensaje en el [foro](http://foxdot.org/forum/) de la web.
