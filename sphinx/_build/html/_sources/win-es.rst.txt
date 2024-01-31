==============
Español v0.1.0
==============

Crear y activar un entorno virtual
----------------------------------

* Crear una carpeta de trabajo y cambiar de directorio con ``cd /path/my_folder``
* Con **pip**:
    * ``python -m venv <my_venv>``
    * ``<my_venv>\Scripts\activate``
* Con **conda**:
    * ``conda create --name <my_venv>``
    * ``activate ./<my_env>``


Clonar con GIT
--------------

* Crear una carpeta de trabajo **<my_library>**
* Abrir **cmd** y cambiar al directorio creado con ``cd /path/<my_library>``
* ``git clone https://github.com/user/repository_name.git``


Instalación local de una librería
---------------------------------

* Descargar la librería deseada en una carpeta **/path/<my_library>**
* En **cmd** cambiar al directorio con ``cd /path/<my_library>``
* Para **pip**:
    * Primero desinstalar si ya está instalada con ``pip uninstall <my_library>``
    * Instalar con ``python setup.py install``
* Para **conda**:
    * ``conda remove <my_library>``
    * ``conda install /path/library-filename.tar.bz2``


Publicar en conda-forge
-----------------------

* Primero clonar el **feedstock** de **conda-forge** en GitHub
* Clonarlo en tu PC con ``git clone https://github.com/user/repository_name.git``
* En Anaconda Prompt:
    * ``conda activate demo``
    * ``conda skeleton pypi <my_library>`` (primero descargar esto en cualquier directorio)
    * ``conda install conda-build`` (solo si no está instalado)

* Modificar el archivo **meta** según corresponda en la carpeta **recipies** en **stage-recipe**
* Subir a GitHub, seguir “Actualizar Repositorio en GitHub”


Actualizar conda-forge
----------------------

* Primero, la librería necesita ser publicada en **PyPi**
* En Anaconda Prompt, cambiar de directorio a la carpeta de la librería con ``cd /path/<my_library>``
* ``conda install conda-build`` (si no está instalado)
* ``conda activate <venv>`` (si es necesario)
* ``conda skeleton pypi <my_library>`` <diferente directorio> 
* Si conda skeleton no funciona, usar ``grayskull pypi <my_library>`` (también extrae de **PyPi**), primero cambiar a un directorio diferente
* Hacer un fork del **<my_library>-feedstock** a tu PC/perfil (si no está hecho)
* Actualizar el repositorio personal o hacer un **git pull**. Normalmente si intentas hacer **push** primero, obtendrás un error
* Cambiar el **sha256** y la **versión** en el archivo **meta.yaml** de la carpeta **recipe** con el creado (descargado). Esto debería estar dentro de las primeras 10 líneas.
* Cambiar la **versión** a la nueva y restablecer el **número de build** a **0**
* NO CAMBIAR EL HOST, solo los requisitos bajo **run:** si hay cambios
* Si se hace desde la carpeta local, actualizar el repositorio de GitHub con **git**, debe ser exitoso sin errores (seguir “Actualizar GitHub”)
* Hacer una solicitud de pull para la actualización: **Título: Actualizar <my_library>-feedstock a vX.X.X**
* Recordar comentar en la solicitud de pull para rehacer como ``@conda-forge-admin, please rerender``
* Una vez que todas las pruebas estén bien, hacer clic en **Merge pull request**
* Esperar un tiempo para la actualización


Actualizar librería con Pip
---------------------------

* ``pip install --upgrade <my_library>``


Reformatear a PEP8
------------------

* ``autopep8 --in-place --aggressive --aggressive <filename>.py``


Actualizar Repositorio en GitHub
--------------------------------

* Hacer clic derecho en la carpeta > Git Bash Here
* ``git branch``
* ``git checkout main`` (o master)
* ``git branch``
* ``git add *``
* ``git status``
* ``git commit -m “nota de actualización”``
* ``git push origin main`` (o master)


Subir a PyPi
------------

* En **cmd** como Administrador
* ``cd /path/<my_library>``
* ``pip install –r requirements_dev.txt`` (solo la primera vez o si cambia)
* ``python setup.py sdist``
* Ir a GitHub > Releases > New Releases y añadir un **tag** y **Release title** como **vx.x.x**, alguna descripción, y publicar release (no subir el zip).
* ``twine upload .\dist\<package-x.x.x.tar.gz>``
* ``twine upload -u <username> -p <password> - repository-url https://pypi.org/manage/project/<my_library>/dist/<my_library>-x.x.x.tar.gz``
* Ingresar usuario y contraseña de **PyPi**


Actualizar versión
------------------

* En **cmd** como Administrador
* ``cd /path/<my_library>``
* ``bumpversion patch/minor/mayor`` (seleccionar uno)
* ``git add *``
* ``git commit -m “nota de commit”``
* ``git push origin main`` (o master)
* ``git push --tags``
* Si esto no funciona, puedes cambiar la versión manualmente en los archivos **setup.py**, **setup.cfg**, y **__init__.py**.


Documentación con Sphinx
------------------------

* En **cmd** como Administrador
* Instalar **Sphinx** con ``pip install sphinx``
* Crear una carpeta llamada **sphinx**
* Cambiar directorio de trabajo a la carpeta **sphinx** con ``cd /path/<my_library>/sphinx``
* Descargar la plantilla con el comando ``sphinx-quickstart`` y seguir las instrucciones de instalación. Configúralo según necesites, si tienes dudas, ve con las opciones predeterminadas.
* Cambiar y añadir archivos **.rst** según necesites
* Antes de crear los archivos HTML, siempre hacer ``make clean``
* Crear los nuevos archivos HTML con ``make html``
* Crear un directorio llamado **/path/<my_library>/docs**
* Copiar los archivos bajo **/path/<my_library>/sphinx/_build/html** al directorio **/path/<my_library>/docs**, reemplazar todo pero no eliminar ningún archivo.
* Actualizar el repositorio con **git** 
* En GitHub ir a **Settings > Pages** y bajo **Branch** seleccionar la carpeta **docs** donde se empujaron los archivos **html**.
* Si los archivos html no se visualizan bien, añadir un archivo vacío **.nojekkyll** en la carpeta **docs**.


Ignorar archivos ya comprometidos
---------------------------------

* Actualizar **.gitignore** si es necesario
* ``git rm -r --cached .``
* ``git add .``
* ``git commit –m “comentario de commit”``
* ``git push origin main``


Cobertura
---------

* Instalar **coverage** si no está instalado con ``pip install coverage``
* Cambiar de directorio a la carpeta de pruebas de la librería con ``cd /path/<my_library>/tests``
* Ejecutar el archivo de prueba con ``python –m unittest test_package.py``
* Ejecutar pruebas con **coverage** con ``coverage run –m unittest <test_package>.py``
* Generar reporte de cobertura con ``coverage report``. Para leer incluir ``-m`` al final. Si hay error, usar ``-i`` al final
* Generar el archivo **xml** con ``coverage xml``
* Si el comando ``coverage`` no funciona, entonces usar ``python -m coverage <test_package>.py``


Contar líneas con cloc
----------------------

* Descargar **cloc** de su repositorio en GitHub
* En **cmd**, cambiar al directorio donde está el ejecutable de **cloc**
* Para contar líneas, escribir el nombre del .exe y luego la ubicación/nombre del directorio/archivo
* Ejemplo: ``cloc-1.96.1.exe <my_file>.py``

