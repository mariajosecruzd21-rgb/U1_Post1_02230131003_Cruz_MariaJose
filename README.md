# U1_Post1_02230131003_Cruz_MariaJose

<h1 style="color:#87CEFA;"> U1_Post1_02230131003_Cruz_MariaJose.zip</h1>

<h2 style="color:#4682B4;">VIOLACIONES SOLID</h2>

<h3 style="color:#FBBCF3;"> 1. SRP - Single Responsibility Principle</h3>

```
public void createOrder(String customer, String product,
                            double price, int quantity) {
        double total = price * quantity;
        if (total > 1000) total *= 0.9; // 10% descuento
        if (total > 5000) total *= 0.85; // 15% descuento adicional
        String orderId = "ORD-" + System.currentTimeMillis();
        orders.add(new String[]{orderId, customer, product,
                String.valueOf(total), "PENDING"});
        System.out.println("Orden creada: " + orderId);
        // Guardar en archivo
        try {
            java.io.FileWriter fw = new java.io.FileWriter(
                    "orders.txt", true);
            fw.write(orderId + "," + customer + "," + total + "\n");
            fw.close();
        } catch (Exception e) { e.printStackTrace(); }
        // Enviar notificación
        System.out.println("EMAIL a " + customer +
                ": Su pedido " + orderId + " ha sido creado.");
    } 
   ```
Se viola SRP porque el ```createOrder``` hace diferentes cosas como  crear pedido, guardar archivo, enviar notificaciones,aplicar descuentos. Por eso tiene muchas razones para cambiar, lo cual contradice el principio de la responsabilidad unica.

<h3 style="color:#FBBCF3;">2. OCP - Open/Closed Principle</h3>
```
if (total > 1000) total *= 0.9; // 10% descuento
if (total > 5000) total *= 0.85; // 15% descuento adicional
```
Se viola OCP porque si quiero agregar un nuevo tipo de descuento como VIP o Blanck Friday, tengo que modificar este método y el comportamiento no se puede extender sin tocar el codigo existente.

<h3 style="color:#FBBCF3;">3. DIP - Dependecy Inversion Pirnciple</h3>

```
java.io.FileWriter fw = new java.io.FileWriter(
                    "orders.txt", true);
            fw.write(orderId + "," + customer + "," + total + "\n");
            fw.close();
            
            
            System.out.println("EMAIL a " + customer +
                ": Su pedido " + orderId + " ha sido creado.");
```

Se viola DIP porque ``OrderManager`` depende directamente de detalles concretos como FileWrite y la logica principal queda acoplada a la forma especifica de guardar y notificar, lo que se dificultaria cambiar a base de datos o mensajes/email  sin modifical la clase.

<h3 style="color:#FBBCF3;">4. ISP - Interface Segregation Principle</h3>
```angular2html
public class OrderManager 

  // Crear pedido
  public void createOrder(String customer, String product,
                          double price, int quantity) 

  // Calcular impuestos
  public double calculateTax(String orderId) 

  // Generar reporte
  public String generateReport() 

```
Se viola ISP porque ```OrderManager``` actua como una interfaz muy grande que obliga a los clientes a depender de metodos que ño necesitan.
>>>>>>> de98e39 (Entrega trabajo PATRONES postcontenido1 con todos los pasos<3)
