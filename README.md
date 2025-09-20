#include <stdio.h>

#define TAMANO 10

// --- Prototipos de Funciones ---
void desplegarMenu();
void ingresarTiempos(int arr[], int tam);
void imprimirArreglo(const int arr[], int tam, const char* titulo);
void copiarArreglo(int destino[], const int fuente[], int tam);
void ordenarPorSeleccion(int arr[], int tam);
void ordenarPorInsercion(int arr[], int tam);

// --- Función Principal ---
int main() {
    int tiempos[TAMANO];
    int copia[TAMANO];
    int opcion;
    int datosListos = 0; // 0 = no, 1 = si

    while (1) {
        desplegarMenu();
        scanf("%d", &opcion);

        if (opcion > 1 && opcion < 5 && !datosListos) {
            printf("\n>> Error: Primero debe ingresar los tiempos (Opcion 1).\n");
            continue;
        }

        if (opcion == 1) {
            ingresarTiempos(tiempos, TAMANO);
            datosListos = 1;
        } else if (opcion == 2) {
            imprimirArreglo(tiempos, TAMANO, "Arreglo Original");
        } else if (opcion == 3) {
            copiarArreglo(copia, tiempos, TAMANO);
            ordenarPorSeleccion(copia, TAMANO);
        } else if (opcion == 4) {
            copiarArreglo(copia, tiempos, TAMANO);
            ordenarPorInsercion(copia, TAMANO);
        } else if (opcion == 5) {
            printf("\nPrograma finalizado.\n");
            break;
        } else {
            printf("\n>> Opcion no valida.\n");
        }
    }
    return 0;
}

// --- Implementación de Funciones ---

void desplegarMenu() {
    printf("\n\n--- MENU ---\n");
    printf("1. Ingresar Tiempos\n");
    printf("2. Mostrar Originales\n");
    printf("3. Ordenar Menor a Mayor (Seleccion)\n");
    printf("4. Ordenar Mayor a Menor (Insercion)\n");
    printf("5. Salir\n");
    printf("Opcion: ");
}

void ingresarTiempos(int arr[], int tam) {
    printf("\n--- Ingrese %d tiempos positivos ---\n", tam);
    for (int i = 0; i < tam; i++) {
        do {
            printf("Tiempo #%d: ", i + 1);
            scanf("%d", &arr[i]);
        } while (arr[i] <= 0);
    }
    printf("Tiempos guardados.\n");
}

void imprimirArreglo(const int arr[], int tam, const char* titulo) {
    printf("\n--- %s ---\n[ ", titulo);
    for (int i = 0; i < tam; i++) {
        printf("%d ", arr[i]);
    }
    printf("]\n");
}

void copiarArreglo(int destino[], const int fuente[], int tam) {
    for (int i = 0; i < tam; i++) {
        destino[i] = fuente[i];
    }
}

void ordenarPorSeleccion(int arr[], int tam) {
    printf("\n--- Proceso Seleccion (Menor a Mayor) ---\n");
    for (int i = 0; i < tam - 1; i++) {
        int min_idx = i;
        for (int j = i + 1; j < tam; j++) {
            if (arr[j] < arr[min_idx]) {
                min_idx = j;
            }
        }
        if (min_idx != i) {
            int temp = arr[i];
            arr[i] = arr[min_idx];
            arr[min_idx] = temp;
        }
        printf("Paso %d: [ ", i + 1);
        for(int k = 0; k < tam; k++) printf("%d ", arr[k]);
        printf("]\n");
    }
    imprimirArreglo(arr, tam, "Resultado Final (Seleccion)");
}

void ordenarPorInsercion(int arr[], int tam) {
    printf("\n--- Proceso Insercion (Mayor a Menor) ---\n");
    for (int i = 1; i < tam; i++) {
        int clave = arr[i];
        int j = i - 1;
        while (j >= 0 && arr[j] < clave) {
            arr[j + 1] = arr[j];
            j--;
        }
        arr[j + 1] = clave;

        printf("Paso %d: [ ", i);
        for(int k = 0; k < tam; k++) printf("%d ", arr[k]);
        printf("]\n");
    }
    imprimirArreglo(arr, tam, "Resultado Final (Insercion)");

    
}
