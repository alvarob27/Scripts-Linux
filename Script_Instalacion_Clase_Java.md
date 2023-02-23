# Actividad de evaluación UD6
#### Este script permite instalar, ejecutar y desinstalar una clase java dentro de un directorio
```bash
#!/bin/bash


creardirectorio(){
	mkdir "$directorio"
}

permisosusuario(){
	sudo chown -R $usuario $directorio
}

permisosgrupo(){
	sudo chgrp -R $grupo $directorio
}

copiarprograma(){
	sudo cp pizarra.java $directorio
}

instalarjre(){
sudo apt install default-jre
}

guardardirectorio(){
	touch .directoriocnfg
	echo $directorio > .directoriocnfg
}

eliminardirectorio(){
	rm -r $dir
}


informe="";

if [ $# -eq 1 ]
then

case $1 in
	"instalar")
		echo "Introduce el nombre del directorio a instalar el programa"
		read directorio
		if [ -d $directorio ]
		then
			informe="El directorio ${directorio} existía"
		else
			informe="El directorio no existía se ha creado el directorio ${directorio}"
			creardirectorio
		fi	
			echo "Introduce el usuario y el grupo que tendran los permisos sobre el directorio"
			read usuario
			read grupo 

			id $usuario &> /dev/null

			if [ $? -eq 0 ]
			then
				informe="$informe\nEl usuario ${usuario} ya existe, se aplicaron permisos al usuario ${usuario}"
				permisosusuario

			else
				informe="$informe\nEl usuario ${usuario} se ha creado y se han aplicado permisos"
				adduser $usuario
				permisosusuario
				
			fi

			if  grep -i "$grupo" /etc/group 
			then
				informe="$informe\nEl grupo ${grupo} ya existe, se aplicaron permisos al grupo ${grupo}"
				permisosgrupo
			else
				informe="$informe\nEl grupo ${grupo} se ha creado y se han aplicado permisos"
				groupadd $grupo
				permisosgrupo
			fi

			informe="$informe\nSe ha copiado el programa en el directorio ${directorio}"
			copiarprograma

			if [ -h /usr/bin/java ]
			then
				informe="$informe\nEl jre ya estaba instalado, no ha habido cambios"
			else
				informe="$informe\nEl jre se ha instalado correctamente en /usr/bin/java"
			instalarjre
			fi	

			echo -e $informe
			guardardirectorio

		;;
	"ejecutar")

		echo "Ejecutando programa"
		dir=$(cat .directoriocnfg)
		cd $dir
		echo "Introduce el archivo a ejecutar"
		read archivo
		echo "Introduce el color a ejecutar el archivo, las opciones son R G Y"
		read color
		java pizarra.java $archivo $color

		;;
	"desinstalar")
		echo "Está seguro que quiere continuar (S/n)"
		read respuesta

		if [ $respuesta == S ]
		then
			echo "Desinstalando programa"
			dir=$(cat .directoriocnfg)
			eliminardirectorio


		else 
			echo "No se desinstalará nada"
		fi
		;;
esac

else
	echo "Error, necesitas meter el parametro instalar, ejecutar o desinstalar"
fi
```












































