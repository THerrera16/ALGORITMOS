#include <stdio.h>
#include <limits.h>

/**
 * Función que divide dos enteros sin usar multiplicación, división o módulo.
 * Se usa resta repetida y desplazamientos de bits para optimizar.
 */
int dividir(int dividendo, int divisor) {
    // Manejo del caso especial donde el resultado excede los límites de 32 bits con signo.
    if (dividendo == INT_MIN && divisor == -1) {
        return INT_MAX;
    }

    // Determinar el signo del resultado (positivo o negativo)
    int signo = (dividendo < 0) ^ (divisor < 0) ? -1 : 1;

    // Convertir a valores absolutos para facilitar el cálculo
    long long dividendo_abs = llabs((long long)dividendo);
    long long divisor_abs = llabs((long long)divisor);

    long long cociente = 0;
   // Algoritmo de resta repetitiva optimizado con desplazamientos de bits
    while (dividendo_abs >= divisor_abs) {
        long long temp = divisor_abs, multiplo = 1;
  // Duplicar el divisor hasta que sea menor o igual al dividendo
        while (dividendo_abs >= (temp << 1)) {
            temp <<= 1;       // Multiplicar por 2 usando desplazamiento de bits
            multiplo <<= 1;   // Multiplicar por 2
        }
 // Restar el valor encontrado del dividendo
        dividendo_abs -= temp;
        cociente += multiplo;
    }
 return signo * (int)cociente; // Aplicar el signo y devolver el resultado
}
int main() {
    int dividendo, divisor;

    // Entrada de usuario
    printf("Ingrese el dividendo: ");
    scanf("%d", &dividendo);
    printf("Ingrese el divisor (distinto de 0): "); 
    scanf("%d", &divisor);

    // Verificar que el divisor no sea 0
    if (divisor == 0) {
        printf("Error: No se puede dividir por 0.\n");
        return 1;
    }
// Realizar la división e imprimir el resultado
    int resultado = dividir(dividendo, divisor);
    printf("Resultado de la división truncada: %d\n", resultado);

    return 0;
}

    
       
