# Función para leer el archivo 'numeros.txt'
leer_numeros <- function(archivo) {
  # Verificar si el archivo existe
  if (!file.exists(archivo)) {
    stop("El archivo no existe.")
  }
  
  # Leer el archivo y convertirlo en un vector de números enteros
  numeros <- as.integer(readLines(archivo))
  return(numeros)
}

# Función principal
procesar_numeros <- function() {
  # Leer el archivo de números
  numeros <- leer_numeros("numeros.txt")
  
  # Calcular los estadísticos
  media <- mean(numeros)
  mediana <- median(numeros)
  desviacion_estandar <- sd(numeros)
  
  # Verificar si hay alta variabilidad
  if (desviacion_estandar > 10) {
    print("Alta variabilidad: la desviación estándar es mayor que 10.")
  }
  
  # Calcular el cuadrado de cada número usando sapply()
  cuadrados <- sapply(numeros, function(x) x^2)
  
  # Escribir los resultados en el archivo 'resultados.txt'
  archivo_resultados <- file("resultados.txt", "w")
  writeLines(c("Estadísticos calculados:", 
               paste("Media:", media), 
               paste("Mediana:", mediana), 
               paste("Desviación estándar:", desviacion_estandar), 
               "Cuadrados de los números:"),
             archivo_resultados)
  writeLines(as.character(cuadrados), archivo_resultados)
  close(archivo_resultados)
  
  # Confirmación de la escritura
  print("Los resultados han sido guardados en 'resultados.txt'.")
}

# Ejecutar la función principal
procesar_numeros()
