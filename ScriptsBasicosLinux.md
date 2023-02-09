# Scripts Básicos Linux
## 1. Recibir un número entero por teclado y decir si es positivo
```bash
#!/bin/bash

echo "Introduce un número"
read num

if [ $num -gt -1 ] 
then
	echo "El número introducido es positivo"
else
	echo "El número introducido es negativo"
fi
```

# 2. Recibir un número entero por teclado y decir si es negativo
```bash
#!/bin/bash

echo "Escribe un número"
read num

if [ $num -lt 0 ] 
then
	echo "El número introducido es negativo"
else
	echo "El número introducido es positivo"
fi
```

# 3. Recibir un número por teclado y decir si es igual a 0
```bash
#!/bin/bash

echo "Introduce un número"
read num

if [ $num == 0 ] 
then
	echo "El número introducido es igual a 0"
else
	echo "El número no es igual a 0"
fi
```

# 4. Recibir un número entero por teclado y decir si es positivo, negativo o igual a cero
```bash
#!/bin/bash

echo "Introduce un número"
read num

if [ $num -gt 0 ]
then
	echo "El número introducido es positivo"
elif [ $num -lt 0 ]
then
	echo "El número introducido es negativo"
elif [ $num == 0 ]
then
	echo "EL número es igual a 0"
fi
```

# 5. Comprobar si el número de parámetros introducido es igual a 3, en el caso de que sea otro número mostrará un mensaje de error en la pantalla
```bash
#!/bin/bash

if [ $# != 3 ] 
then 
	echo "El número de parámetros introducidos es menor a 3"
fi
```

# 6. Recibir dos números por parámetros y sumarlos. Si el número de parametros es diferente de 2 mostrar un mensaje de error.
```bash
#!/bin/bash

if [ $# != 2 ]
then
	echo "El número de parámetros introducido es diferente de 2"
elif [ $# == 2 ] 
then
	suma=$(($1 + $2))
	echo "La suma de los 2 parámetros introducidos es ${suma}"
fi
```

# 7. Recibir 3 parámetros. En el caso de que reciba un número diferente mostrará un mensaje de error. Los 2 primeros serán 2 números y el tercer parámetro será uno de estos símbolos +,-,x,/, dependiendo del símbolo realizará una u otra operación. En el caso de introducir otro símbolo dará error mostrando los símbolos disponibles
```bash
#!/bin/bash

if ! [[ $1 =~ ^[0-9]$ ]] 
then
       	echo "error: no es un número"
	exit;
fi

if [ $# != 3 ]
then
	echo "El número de parámetros introducidos es distinto de 3"
	exit;
 fi
	
if [ $3 == "+" ] 
then
	suma=(($1 + $2))
	echo "La suma de los números es ${suma}"

fi
```

# 8. Recibir la ruta de un fichero e indicar si existe
```bash
#!/bin/bash

echo "Introduce una ruta de un fichero para comprobar si esiste"

read ruta

if [ -e $ruta ]
then
	echo "El fichero sí existe"
else
	echo "El fichero no existe"
fi
```

# 9. Recibir la ruta de un fichero e indicar si es un directorio o un fichero.
```bash
#!/bin/bash

echo "Introduce la ruta de un directorio o un fichero"

read ruta

if [ -d $ruta ]
then
	echo "Es un directorio"
if [ -f $ruta ]
then
	echo "Es un fichero"
fi
else
	echo "No existe"
fi
```

# 10. Recibir la ruta de un fichero e indicar los permisos que tiene (escritura, lectura, ejecución)
```bash
#!/bin/bash

echo "Introduce la ruta de un fichero para saber que permisos tiene"

read ruta

if [ -e $ruta ]
then
	if [ -r $ruta ]
	then
		echo "El fichero tiene permisos de lectura"
	fi

	if [ -w $ruta ]
	then
		echo "EL fichero tiene permisos de escritura"
	fi

	if [ -x $ruta ]
	then
		echo "El fichero tiene permisos de ejecución"
	fi

else
	echo "El fichero no existe"
fi
```

# 11. Imprimir por pantalla 50 veces la palabra hola.
```bash
#!/bin/bash

for ((i=0;i<50;i++))
do
	echo $i hola
done
```

# 12. Leer una palabra por teclado y mostrarla por consola. Debe realizar esta operación 10 veces.
```bash
#!/bin/bash

echo "Introduce una palabra a repetir 10 veces"

read palabra

for ((i=0;i<10;i++))
do
	echo $i $palabra
done
```

# 13. Recibir un número por parámetro. El programa imprimirá la palabra “hola” el número de veces indicado por parámetro.
```bash
#!/bin/bash

echo "Introduce un número para escribir hola tantas veces como se indique"

read num

for ((i=0;i<=$num;i++))
do 
	echo $i hola
done
```

# 14. Se debe pasar un número n por parámetro. El programa imprimirá los números del 0 al n por pantalla.
```bash
#!/bin/bash
echo "Introduce un número para imprimir todos los numeros del cero al introducido"

read n

for ((i=0; i<=$n; i++))
do
	echo $i
done
```

# 15. Recibir un número n por parámetro. El programa tendrá que sumar todos los números entre 1 y n. Posteriormente mostrará el resultado de la suma por pantalla
```bash
#!/bin/bash

echo "Introduce un numero para hacer la suma de todos los numeros entre 0 y el introducido"

read n
suma=0
for ((i=0; i<=$n; i=i+1))
do
	suma=$(($i+$suma))
done

echo "La suma es ${suma}"
```

# 16. Recibir dos números por parámetro. El programa deberá hacer que el primer parámetro tome el valor del segundo parámetro y el segundo parámetro tome el valor del primero. Por ejemplo si se introduce el 2 y el 9, en un principio $1 es 1 y $2 es 9. Tras la ejecución del programa $1 valdrá 9 y $2 1.
```bash
#!/bin/bash

echo "El parametro uno introducido es ${1}"
echo "EL parametro dos introducido es ${2}"

num2=$1
num1=$2

echo "El parametro uno cambiado es ${num1}"
echo "EL parametro dos cambiado es ${num2}"
```

# 17. Programa que lea palabras hasta que se escriba “:q”
```bash
#!/bin/bash

echo "Introduce una palabra, cuando quieras finalizar escribe :q"

read palabra

while [ $palabra != :q ]
do
	echo "Introduce otra palabra"
	read palabra
done
```

# 18. Programa que lea palabras y las guarde en un fichero, hasta que se escriba “:q”
```bash
#!/bin/bash

echo "Introduce palabras a guardar en un fichero hasta escribir :q"

read palabra

while [ $palabra != :q ]
do
	echo $palabra >> fichero1.txt
	echo "Escribe otra palabra"
	read palabra
done
```

# 19. Programa que lea palabras y las guarde en un fichero de forma ordenada, hasta que se escriba “:q”
```bash
#!/bin/bash

echo "Escribe palabras para escribir en un fichero de manera ordenada, hasta que escribas :q"
read palabra
while [ $palabra != :q ]
do
	echo $palabra >> archivo2.txt
	sort -o archivo2.txt archivo2.txt
	echo "Escribe otra palabra"
	read palabra
done
```

# 20. Realiza un programa que solicite un número y compruebe si se encuentre en un archivo llamado números.txt
```bash
#!/bin/bash

echo "Escribe un número para comprobar si está en el fichero numeros.txt"

read numero

for i in `cat numeros.txt`
do
	if [ $numero -eq $i ]
	then
		echo "El número introducido se encuentra en el fichero numeros.txt"
		exit 0
	fi
done

echo "El número no existe en el fichero"
```












































