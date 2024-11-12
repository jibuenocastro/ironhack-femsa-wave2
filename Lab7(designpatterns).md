# Design Problem Solving:


## Design Challenges:

### Global Configuration Management: Design a system that ensures a single, globally accessible configuration object without access conflicts.

Se puede usar el patrón singleton ya que este patrón es de acceso global, y se instancia una sola vez, esto creo que lo he implementado en aplicaciones moniliticas que se contectan a base de datos, el objeto de conexión se hace de tipo singleton.

```bash

    public class dbconection {

        public static conection= null;
        public static Conection getContection(){

            try{    
                if(conection == null){
                    // conection = crear una nueva conexion
                }

            }catch(Exception ex ){
                system.out.println(ex.message)
            }
        }
    }


```


### Dynamic Object Creation Based on User Input: Implement a system to dynamically create various types of user interface elements based on user actions.

Para esto se puede usar el patrón factory ya que este permite la creación de objetos de forma dinamica.

```bash 

public interface IMenu {
    public Menu showMenu()
}

class AdministradorMenu implements Menu{

    public Menu showMenu(){
         return Menu;
    }
}

class usuarioNivel1Menu implements Menu{

    public Menu showMenu(){
        return Menu;
    }

}

public class MenuUserInterfaceFactory {
    public static Menu crearMenu(String tipo) {
        if (tipo == null || tipo.isEmpty()) {
            return null;
        }
        switch (tipo) {
            case "ADMIN":
                return new AdministradorMenu();
            case "USERNIVEL1":
                return new usuarioNivel1Menu();
            default:
                throw new IllegalArgumentException("Tipo de notificación desconocido: " + tipo);
        }
    }
}


public class Main {
    public static void main(String[] args) {
        Menu menu = MenuUserInterfaceFactory.crearMenu("ADMIN");
        menu.showMenu();

        Menu menuUserNevel1 = MenuUserInterfaceFactory.crearMenu("USERNIVEL1");
        menuUserNevel1.showMenu();
    }
}

```

### State Change Notification Across System Components: Ensure components are notified about changes in the state of other parts without creating tight coupling.

Para este escenario es ideal el patrón observador, ya que permite notificar sobre una acción hecha sobre el estado a otros componentes que estan subscritos al componente padre 


Ej: Notificar al componente log que se guardo un registro 

```bash

class GenerateLog {
    List observers = new List();
    Map stockPrices = new Map();
 
    public void guardarRegistro(stock, price) {
        stockPrices.put(stock, price);
        notifyObservers(stock);
    }
 
    method notifyObservers(stock) {
        for each observer in observers {
            observer.update(stock, stockPrices.get(stock));
        }
    }
}


public interface Observer {
    void onRecordSaved(String message);
}

class Member {
    private List<Observer> observers = new ArrayList<>();

    
    public void addObserver(Observer observer) {
        observers.add(observer);
    }

    public void removeObserver(Observer observer) {
        observers.remove(observer);
    }

    public void notifyObservers(String message) {
        for (Observer observer : observers) {
            observer.onRecordSaved(message);
        }
    }
    
    public void saveRecord(String record) {
        System.out.println("Registro guardado: " + record);
        notifyObservers("Registro guardado con éxito: " + record);
    }
}

public class LogObserver implements Observer {
    @Override
    public void onRecordSaved(String message) {
        System.out.println("Log: " + message);
    }
}


public class Main {
    public static void main(String[] args) {
        Subject subject = new Subject();
        LogObserver logObserver = new LogObserver();

        subject.addObserver(logObserver);

        // Guardar un registro, esto disparará el log
        subject.saveRecord("Registro de prueba");
    }
}

```


### Efficient Management of Asynchronous Operations: Manage multiple asynchronous operations like API calls which need to be coordinated without blocking the main application workflow.
 
 Un patron de diseño asincrono puede resulver este problema, el diseño de una api asincrona es fundamentales para mejorar la escalabilidad y la eficiencia de las aplicaciones, permiten una mejor utilización de los recursos del sistema al descargar tareas que, de otro modo, bloquearían el hilo de ejecución principal.

### Ej: en React usando la libreria axios

```bash

const obtenerDatos = async () => {
    try{

        var response = await axios.get(URL);
        //validar response
    }catch(err){
        console.log(err)
    }
}

```
