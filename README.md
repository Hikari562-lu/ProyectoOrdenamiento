# ProyectoOrdenamiento
Proyecto de Estructura de Datos
import java.io.*;
import java.util.*;

public class proyectoOrdenamiento {

    // Mostrar información sobre el proyecto y el desarrollador
    public static void mostrarInformacion() {
        String universidad = "Universidad Da Vinci de Guatemala";
        String curso = "Estructura de Datos";
        String docente = "Ing. Brandon Chitay";

        // Información del desarrollador
        String nombreDesarrollador = "Luz Castañeda";
        String contacto = "tuemail@example.com";

        // Mostrar la información en consola
        System.out.println("\n========================================");
        System.out.println(universidad);
        System.out.println(curso);
        System.out.println(docente + "\n");
        System.out.println("INFORMACIÓN DEL DESARROLLADOR:");
        System.out.println("Nombre: " + nombreDesarrollador);
        System.out.println("Contacto: " + contacto);
        System.out.println("========================================");

        // Esperar a que el usuario presione Enter antes de continuar
        Scanner scanner = new Scanner(System.in);
        System.out.println("Presione Enter para continuar...");
        scanner.nextLine();
        mostrarMenu(scanner);
    }

    // Mostrar el menú principal
    public static void mostrarMenu(Scanner scanner) {
        List<Integer> listaDatos = new ArrayList<>();
        int opcion;
        do {
            // Mostrar las opciones del menú
            System.out.println("\n========== MENÚ PRINCIPAL ==========");
            System.out.println("1. Cargar datos desde un archivo CSV");
            System.out.println("2. Ordenar datos usando Bubble Sort");
            System.out.println("3. Ordenar datos usando Enhanced Bubble Sort");
            System.out.println("4. Ordenar datos usando Quick Sort");
            System.out.println("5. Ordenar datos usando Selection Sort");
            System.out.println("6. Ordenar datos usando Merge Sort");
            System.out.println("7. Buscar un número con Binary Search");
            System.out.println("8. Salir");
            System.out.print("Ingrese una opción: ");

            // Leer la opción seleccionada
            opcion = scanner.nextInt();
            scanner.nextLine();  // Limpiar el buffer

            switch (opcion) {
                case 1:
                    opcionCargarDatos(scanner, listaDatos);
                    break;
                case 2:
                    BubbleSort.opcionBubbleSort(listaDatos);
                    break;
                case 3:
                    EnhancedBubbleSort.opcionEnhancedBubbleSort(listaDatos);
                    break;
                case 4:
                    System.out.println(" Opción seleccionada: Quick Sort (Pendiente de implementación).");
                    break;
                case 5:
                    System.out.println(" Opción seleccionada: Selection Sort (Pendiente de implementación).");
                    break;
                case 6:
                    System.out.println(" Opción seleccionada: Merge Sort (Pendiente de implementación).");
                    break;
                case 7:
                    System.out.println(" Opción seleccionada: Binary Search (Pendiente de implementación).");
                    break;
                case 8:
                    System.out.println(" Saliendo del programa...");
                    break;
                default:
                    System.out.println(" Opción no válida. Intente de nuevo.");
            }
        } while (opcion != 8);
    }

    // Método para cargar datos desde el archivo CSV
    public static List<Integer> cargarDatos(String nombreArchivo) {
        List<Integer> datos = new ArrayList<>();
        try (BufferedReader br = new BufferedReader(new FileReader(nombreArchivo))) {
            String linea;
            while ((linea = br.readLine()) != null) {
                try {
                    datos.add(Integer.parseInt(linea.trim()));
                } catch (NumberFormatException e) {
                    System.out.println("⚠️ Dato inválido en el archivo: " + linea);
                }
            }
            System.out.println("✅ Datos cargados exitosamente desde " + nombreArchivo);
        } catch (IOException e) {
            System.out.println("❌ Error al leer el archivo: " + e.getMessage());
        }
        return datos;
    }

    // Llamar a la opción de cargar datos
    public static void opcionCargarDatos(Scanner scanner, List<Integer> listaDatos) {
        String nombreArchivo = "datos.csv";
        List<Integer> datosCargados = cargarDatos(nombreArchivo);
        if (!datosCargados.isEmpty()) {
            listaDatos.clear();
            listaDatos.addAll(datosCargados);
        }
    }

    public static void main(String[] args) {
        mostrarInformacion();
    }
}

class BubbleSort {
    public static void ordenar(List<Integer> lista) {
        int n = lista.size();
        for (int i = 0; i < n - 1; i++) {
            for (int j = 0; j < n - i - 1; j++) {
                if (lista.get(j) > lista.get(j + 1)) {
                    int temp = lista.get(j);
                    lista.set(j, lista.get(j + 1));
                    lista.set(j + 1, temp);
                }
            }
        }
        System.out.println(" Lista ordenada con Bubble Sort.");
    }

    public static void opcionBubbleSort(List<Integer> lista) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }
        ordenar(lista);
        System.out.println(" Lista ordenada: " + lista);
    }
}

class EnhancedBubbleSort {
    public static void ordenar(List<Integer> lista) {
        int n = lista.size();
        for (int i = 0; i < n - 1; i++) {
            boolean swapped = false;
            for (int j = 0; j < n - i - 1; j++) {
                if (lista.get(j) > lista.get(j + 1)) {
                    int temp = lista.get(j);
                    lista.set(j, lista.get(j + 1));
                    lista.set(j + 1, temp);
                    swapped = true;
                }
            }
            if (!swapped) break;
        }
        System.out.println(" Lista ordenada con Enhanced Bubble Sort.");
    }

    public static void opcionEnhancedBubbleSort(List<Integer> lista) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }
        ordenar(lista);
        System.out.println(" Lista ordenada: " + lista);
    }
}

// Clase con QuickSort
class QuickSort {
    public static void ordenar(List<Integer> lista, int inicio, int fin) {
        if (inicio < fin) {
            int indicePivote = particion(lista, inicio, fin);
            ordenar(lista, inicio, indicePivote - 1);
            ordenar(lista, indicePivote + 1, fin);
        }
    }

    private static int particion(List<Integer> lista, int inicio, int fin) {
        int pivote = lista.get(fin);
        int i = inicio - 1;
        for (int j = inicio; j < fin; j++) {
            if (lista.get(j) <= pivote) {
                i++;
                Collections.swap(lista, i, j);
            }
        }
        Collections.swap(lista, i + 1, fin);
        return i + 1;
    }

    public static void opcionQuickSort(List<Integer> lista) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }
        ordenar(lista, 0, lista.size() - 1);
        System.out.println(" Lista ordenada con Quick Sort.");
        System.out.println(" Lista ordenada: " + lista);
    }
}

// Clase con SelectionSort
class SelectionSort {
    public static void ordenar(List<Integer> lista) {
        int n = lista.size();
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (lista.get(j) < lista.get(minIndex)) {
                    minIndex = j;
                }
            }
            int temp = lista.get(i);
            lista.set(i, lista.get(minIndex));
            lista.set(minIndex, temp);
        }
        System.out.println(" Lista ordenada con Selection Sort.");
    }

    public static void opcionSelectionSort(List<Integer> lista) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }
        ordenar(lista);
        System.out.println(" Lista ordenada: " + lista);
    }
}

// Clase con MergeSort
class MergeSort {
    public static void ordenar(List<Integer> lista) {
        if (lista.size() <= 1) return;
        int mid = lista.size() / 2;
        List<Integer> left = new ArrayList<>(lista.subList(0, mid));
        List<Integer> right = new ArrayList<>(lista.subList(mid, lista.size()));

        ordenar(left);
        ordenar(right);

        merge(lista, left, right);
        System.out.println(" Lista ordenada con Merge Sort.");
    }

    private static void merge(List<Integer> lista, List<Integer> left, List<Integer> right) {
        int i = 0, j = 0, k = 0;
        while (i < left.size() && j < right.size()) {
            if (left.get(i) <= right.get(j)) {
                lista.set(k++, left.get(i++));
            } else {
                lista.set(k++, right.get(j++));
            }
        }
        while (i < left.size()) lista.set(k++, left.get(i++));
        while (j < right.size()) lista.set(k++, right.get(j++));
    }

    public static void opcionMergeSort(List<Integer> lista) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }
        ordenar(lista);
        System.out.println(" Lista ordenada: " + lista);
    }
}

// Clase de búsqueda binaria
class BusquedaBinaria {
    public static boolean estaOrdenada(List<Integer> lista) {
        for (int i = 0; i < lista.size() - 1; i++) {
            if (lista.get(i) > lista.get(i + 1)) {
                return false;
            }
        }
        return true;
    }

    public static int busquedaBinaria(List<Integer> lista, int objetivo) {
        int izquierda = 0;
        int derecha = lista.size() - 1;

        while (izquierda <= derecha) {
            int medio = (izquierda + derecha) / 2;
            int valorMedio = lista.get(medio);

            if (valorMedio == objetivo) {
                return medio;
            } else if (valorMedio < objetivo) {
                izquierda = medio + 1;
            } else {
                derecha = medio - 1;
            }
        }
        return -1;
    }

    public static void opcionBusquedaBinaria(List<Integer> lista, int objetivo) {
        if (lista.isEmpty()) {
            System.out.println(" No hay datos cargados. Cargue datos primero.");
            return;
        }

        if (!estaOrdenada(lista)) {
            System.out.println(" La lista no está ordenada. Se ordenará primero.");
            MergeSort.ordenar(lista);  // Ordenamos la lista antes de la búsqueda binaria
        }

        int resultado = busquedaBinaria(lista, objetivo);
        if (resultado == -1) {
            System.out.println(" Elemento no encontrado.");
        } else {
            System.out.println(" Elemento encontrado en el índice: " + resultado);
        }
    }
}

