#include <stdio.h>
#include <stdlib.h>
#include <string.h>

#define MAX_COMBINACIONES 100
#define MAX_LONGITUD 5

// Mapeo de dígitos a letras (como en un teclado telefónico)
const char *teclado[] = {
    "",     // 0 no tiene letras
    "",     // 1 no tiene letras
    "abc",  // 2
    "def",  // 3
    "ghi",  // 4
    "jkl",  // 5
    "mno",  // 6
    "pqrs", // 7
    "tuv",  // 8
    "wxyz"  // 9
};

// Array para almacenar las combinaciones generadas
char resultado[MAX_COMBINACIONES][MAX_LONGITUD];
int contador = 0;

// Función de backtracking para generar combinaciones
void backtrack(char *digitos, int indice, char *combinacion) {
    int i;  // Declaración externa del índice (compatible con C89)
    
    // Si se alcanzó el final de la cadena de dígitos
    if (digitos[indice] == '\0') {
        strcpy(resultado[contador], combinacion);
        contador++;
        return;
    }

    // Obtener las letras asociadas al dígito actual
    int num = digitos[indice] - '0';
    const char *letras = teclado[num];

    for (i = 0; letras[i] != '\0'; i++) {
        combinacion[indice] = letras[i];
        combinacion[indice + 1] = '\0';

        // Llamada recursiva para el siguiente dígito
        backtrack(digitos, indice + 1, combinacion);
    }
}

// Función para generar las combinaciones
void generarCombinaciones(char *digitos) {
    int i;  // Declaración externa del índice (compatible con C89)
    
    if (digitos == NULL || strlen(digitos) == 0) {
        printf("[]\n");
        return;
    }

    // Inicializar contador y combinación temporal
    contador = 0;
    char combinacion[MAX_LONGITUD] = "";

    // Llamar a la función de backtracking
    backtrack(digitos, 0, combinacion);

    // Mostrar los resultados
    printf("[");
    for (i = 0; i < contador; i++) {
        printf("\"%s\"", resultado[i]);
        if (i < contador - 1) {
            printf(", ");
        }
    }
    printf("]\n");
}

// Función principal
int main() {
    // Casos de prueba
    printf("Entrada: \"23\" ? Salida: ");
    generarCombinaciones("23");

    printf("Entrada: \"\" ? Salida: ");
    generarCombinaciones("");

    printf("Entrada: \"2\" ? Salida: ");
    generarCombinaciones("2");

    return 0;
}

    
       
