# cadena
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        System.out.print("Ingrese una cadena: ");
        String cadena = scanner.nextLine();
        
        int[] frecuenciaCaracteres = new int[256];
        

        int longitud = cadena.length();
        int indice = 0;
        while (indice < longitud) {
            char caracter = cadena.charAt(indice);
            frecuenciaCaracteres[caracter]++;
            indice++;
        }
        

        char caracterMasRepetido = ' ';
        int maxFrecuencia = 0;
        
        for (int i = 0; i < 256; i++) {
            if (frecuenciaCaracteres[i] > maxFrecuencia) {
                maxFrecuencia = frecuenciaCaracteres[i];
                caracterMasRepetido = (char) i;
            }
        }
        

        System.out.println("El caracter que más veces se repite es '" + caracterMasRepetido + "' con " + maxFrecuencia + " repeticiones.");
        
        scanner.close();
    }
}
#notas
import java.util.Scanner;

public class Notas {
    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        
        int cantidadNotas = 0;
        
    }
        System.out.print("Ingrese la cantidad de notas: ");
        while (true) {
            if (scanner.hasNextInt()) {
                cantidadNotas = scanner.nextInt();
                if (cantidadNotas > 0) {
                    break;
                } else {
                    System.out.print("Por favor, ingrese un valor positivo: ");
                }
            } else {
                System.out.print("Entrada no válida. Ingrese un número entero positivo: ");
                scanner.next();
            }
        }
        
        double sumaNotas = 0;
        double notaMayor = Double.MIN_VALUE;
        double notaMenor = Double.MAX_VALUE;
        

        for (int i = 1; i <= cantidadNotas; i++) {
            double nota = -1;
            while (true) {
                System.out.print("Nota# " + i + ": ");
                if (scanner.hasNextDouble()) {
                    nota = scanner.nextDouble();
                    if (nota >= 0 && nota <= 100) {
                        break;
                    } else {
                        System.out.println("Nota fuera del rango 0 a 100. Intente de nuevo.");
                    }
                } else {
                    System.out.println("Entrada no válida. Ingrese un número decimal.");
                    scanner.next(); 
                }
            }
            

            sumaNotas += nota;
            if (nota > notaMayor) {
                notaMayor = nota;
            }
            if (nota < notaMenor) {
                notaMenor = nota;
            }
        }
        
    
        double promedio = sumaNotas / cantidadNotas;
        

        System.out.printf("Promedio: %.2f%n", promedio);
        System.out.printf("Nota mayor: %.2f%n", notaMayor);
        System.out.printf("Nota menor: %.2f%n", notaMenor);
        
        scanner.close();
    }
}
#clases
import java.util.Scanner;

public class InstitutoDeIngles {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);

        System.out.print("Ingrese la fecha actual (día, DD/MM): ");
        String fechaInput = scanner.nextLine();
        String[] fechaPartes = fechaInput.split(", ");

        if (fechaPartes.length != 2) {
            System.out.println("Error: Formato incorrecto.");
            return;
        }

        String diaSemana = fechaPartes[0].toLowerCase();
        String[] fecha = fechaPartes[1].split("/");

        if (fecha.length != 2) {
            System.out.println("Error: Formato incorrecto.");
            return;
        }

        int dia = 0;
        int mes = 0;

        try {
            dia = Integer.parseInt(fecha[0]);
            mes = Integer.parseInt(fecha[1]);
        } catch (NumberFormatException e) {
            System.out.println("Error: El día o el mes no son números válidos.");
            return;
        }

        if (dia < 1 || dia > 31 || mes < 1 || mes > 12) {
            System.out.println("Error: Día o mes fuera de rango.");
            return;
        }

 
        switch (diaSemana) {
            case "lunes":
                procesarClase("nivel inicial", scanner);
                break;
            case "martes":
                procesarClase("nivel intermedio", scanner);
                break;
            case "miércoles":
                procesarClase("nivel avanzado", scanner);
                break;
            case "jueves":
                procesarPracticaHablada(dia, mes, scanner);
                break;
            case "viernes":
                procesarInglesParaViajeros(dia, mes, scanner);
                break;
            default:
                System.out.println("Error: Día de la semana inexistente.");
        }
    }

    private static void procesarClase(String nivel, Scanner scanner) {
        System.out.println("Se dictó la clase de " + nivel + ".");
        System.out.print("¿Hubo exámenes? (sí/no): ");
        String respuesta = scanner.nextLine().toLowerCase();

        if (respuesta.equals("sí")) {
            System.out.print("Ingrese la cantidad de alumnos aprobados: ");
            int aprobados = obtenerNumero(scanner);
            System.out.print("Ingrese la cantidad de alumnos no aprobados: ");
            int noAprobados = obtenerNumero(scanner);

            if (aprobados + noAprobados == 0) {
                System.out.println("Error: No se puede calcular el porcentaje con 0 alumnos.");
                return;
            }

            double porcentajeAprobados = (double) aprobados / (aprobados + noAprobados) * 100;
            System.out.printf("Porcentaje de aprobados: %.2f%%\n", porcentajeAprobados);
        } else if (!respuesta.equals("no")) {
            System.out.println("Error: Respuesta no válida.");
        }
    }

    private static void procesarPracticaHablada(int dia, int mes, Scanner scanner) {
        System.out.println("Se dictó la práctica hablada.");
        System.out.print("Ingrese el porcentaje de asistencia: ");
        double porcentajeAsistencia = obtenerNumero(scanner);

        if (porcentajeAsistencia > 100 || porcentajeAsistencia < 0) {
            System.out.println("Error: Porcentaje de asistencia no válido.");
            return;
        }

        if (porcentajeAsistencia > 50) {
            System.out.println("Asistió la mayoría.");
        } else {
            System.out.println("No asistió la mayoría.");
        }
    }

    private static void procesarInglesParaViajeros(int dia, int mes, Scanner scanner) {
        if ((dia == 1 && (mes == 1 || mes == 7))) {
            System.out.println("Comienzo de nuevo ciclo.");
            System.out.print("Ingrese la cantidad de alumnos del nuevo ciclo: ");
            int cantidadAlumnos = obtenerNumero(scanner);
            System.out.print("Ingrese el precio por cada alumno en $: ");
            double precioPorAlumno = obtenerNumero(scanner);

            double ingresoTotal = cantidadAlumnos * precioPorAlumno;
            System.out.printf("Ingreso total: $%.2f\n", ingresoTotal);
        } else {
            System.out.println("Se dictó inglés para viajeros.");
        }
    }

    private static int obtenerNumero(Scanner scanner) {
        while (!scanner.hasNextInt()) {
            System.out.print("Error: Ingrese un número válido: ");
            scanner.next(); 
        }
        return scanner.nextInt();
    }
}
