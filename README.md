#!/bin/bash

function script()
    {
        cd /media

        sudo mkdir backup

        # Montamos la memoria externa localizando primero su ubicación:

        ls /dev/sdb*

        # Suponiendo que aparece como sdb1:

        sudo mount /dev/sdb1 /media/backup

        # Creamos el archivo con el script:

        sudo nano / /backup.sh (por ejemplo
        sudo nano /home/USUARIO/backup) y escribimos dentro:


        #fecha de realizacion

        TIME=`date +%b-%d-%y`

        #nombre de archive que contiene el backup

        FILENAME=backup-$TIME.tar.gz

        #carpeta que guardamos (es un ejemplo)

        SRCDIR=/home/nombre_de_usuario

        #lugar donde guardamos el backup (es un ejemplo, a un disco duro externo)

        DESDIR=/media/backup

        #archivo para comparar los cambios de un backup a otro para que sea incremental (es un ejemplo)

        SNF=/media/backup/backup.snar

        #archivo comprimido que contiene el backup

        tar -cvzpf $DESDIR/$FILENAME -g $SNF $SRCDIR

        Guardamos el archivo. A continuación le damos permisos y probamos el script.

        sudo chmod +x backup.sh

        sudo  ./backup.sh
    }

B-

sudo nano /carpeta-usuario/backup.sh 

C-  

#!/bin/bash

FILE=carpeta-elegida

if [ -f "$FILE" ]
    then
        echo "$FILE Se ha comprimido con exito"

    else
        echo "$FILE No se ha conseguido comprimir con exito"
fi

D-

#!/bin/bash

* 2 * * * /home/nombre-del-usuario/backup.sh >/dev/null 2>&1
