# Design Patterns - Padroes de Projeto

## O que e
Solucoes reutilizaveis para problemas comuns de design de software.

## Creational Patterns

### Singleton
class Singleton {
    private static Singleton instance;
    
    private Singleton() {}
    
    public static synchronized Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}

// Uso
Singleton s = Singleton.getInstance();

### Factory Method
interface Shape {
    void draw();
}

class Circle implements Shape {
    public void draw() { System.out.println("Circle"); }
}

class Square implements Shape {
    public void draw() { System.out.println("Square"); }
}

class ShapeFactory {
    public Shape createShape(String type) {
        if (type.equals("circle")) return new Circle();
        if (type.equals("square")) return new Square();
        throw new IllegalArgumentException();
    }
}

// Uso
ShapeFactory factory = new ShapeFactory();
Shape shape = factory.createShape("circle");
shape.draw();

### Builder
class User {
    private String name;
    private int age;
    private String email;
    
    private User(Builder builder) {
        this.name = builder.name;
        this.age = builder.age;
        this.email = builder.email;
    }
    
    public static class Builder {
        private String name;
        private int age;
        private String email;
        
        public Builder name(String name) {
            this.name = name;
            return this;
        }
        
        public Builder age(int age) {
            this.age = age;
            return this;
        }
        
        public Builder email(String email) {
            this.email = email;
            return this;
        }
        
        public User build() {
            return new User(this);
        }
    }
}

// Uso
User user = new User.Builder()
    .name("John")
    .age(30)
    .email("john@example.com")
    .build();

## Structural Patterns

### Adapter
interface MediaPlayer {
    void play(String filename);
}

class Mp3Player implements MediaPlayer {
    public void play(String filename) {
        System.out.println("Playing MP3: " + filename);
    }
}

class Mp4Player {
    public void playMp4(String filename) {
        System.out.println("Playing MP4: " + filename);
    }
}

class MediaAdapter implements MediaPlayer {
    private Mp4Player mp4Player;
    
    public MediaAdapter() {
        this.mp4Player = new Mp4Player();
    }
    
    public void play(String filename) {
        if (filename.endsWith(".mp4")) {
            mp4Player.playMp4(filename);
        }
    }
}

// Uso
MediaPlayer player = new MediaAdapter();
player.play("video.mp4");

### Decorator
interface Component {
    void operation();
}

class ConcreteComponent implements Component {
    public void operation() {
        System.out.println("Base operation");
    }
}

abstract class Decorator implements Component {
    protected Component component;
    
    public Decorator(Component component) {
        this.component = component;
    }
    
    public void operation() {
        component.operation();
    }
}

class ConcreteDecorator extends Decorator {
    public ConcreteDecorator(Component component) {
        super(component);
    }
    
    public void operation() {
        super.operation();
        System.out.println("Added behavior");
    }
}

// Uso
Component component = new ConcreteDecorator(new ConcreteComponent());
component.operation();

### Facade
class SubsystemA {
    public void operationA() { System.out.println("A"); }
}

class SubsystemB {
    public void operationB() { System.out.println("B"); }
}

class Facade {
    private SubsystemA a;
    private SubsystemB b;
    
    public Facade() {
        this.a = new SubsystemA();
        this.b = new SubsystemB();
    }
    
    public void operation() {
        a.operationA();
        b.operationB();
    }
}

// Uso
Facade facade = new Facade();
facade.operation();

## Behavioral Patterns

### Observer
interface Observer {
    void update(String message);
}

class ConcreteObserver implements Observer {
    public void update(String message) {
        System.out.println("Received: " + message);
    }
}

class Subject {
    private List<Observer> observers = new ArrayList<>();
    
    public void attach(Observer observer) {
        observers.add(observer);
    }
    
    public void detach(Observer observer) {
        observers.remove(observer);
    }
    
    public void notify(String message) {
        for (Observer observer : observers) {
            observer.update(message);
        }
    }
}

// Uso
Subject subject = new Subject();
Observer observer = new ConcreteObserver();
subject.attach(observer);
subject.notify("Hello");

### Strategy
interface Strategy {
    int execute(int a, int b);
}

class AddStrategy implements Strategy {
    public int execute(int a, int b) {
        return a + b;
    }
}

class MultiplyStrategy implements Strategy {
    public int execute(int a, int b) {
        return a * b;
    }
}

class Context {
    private Strategy strategy;
    
    public Context(Strategy strategy) {
        this.strategy = strategy;
    }
    
    public int execute(int a, int b) {
        return strategy.execute(a, b);
    }
}

// Uso
Context context = new Context(new AddStrategy());
int result = context.execute(5, 3);  // 8

context = new Context(new MultiplyStrategy());
result = context.execute(5, 3);  // 15

### Command
interface Command {
    void execute();
    void undo();
}

class LightOnCommand implements Command {
    private Light light;
    
    public LightOnCommand(Light light) {
        this.light = light;
    }
    
    public void execute() {
        light.on();
    }
    
    public void undo() {
        light.off();
    }
}

class RemoteControl {
    private Command command;
    
    public void setCommand(Command command) {
        this.command = command;
    }
    
    public void pressButton() {
        command.execute();
    }
    
    public void pressUndo() {
        command.undo();
    }
}

// Uso
Light light = new Light();
Command lightOn = new LightOnCommand(light);
RemoteControl remote = new RemoteControl();
remote.setCommand(lightOn);
remote.pressButton();

## Quando Usar

### Creational
- Singleton: controle de instancia unica
- Factory: criacao de objetos complexos
- Builder: construcao passo a passo

### Structural
- Adapter: interfaces incompativeis
- Decorator: adicionar comportamento
- Facade: simplificar interface complexa

### Behavioral
- Observer: notificacoes de eventos
- Strategy: algoritmos intercambiaveis
- Command: encapsular requests

## Best Practices
- Escolher padrao apropriado para o problema
- Nao over-engineer
- Documentar decisoes de design
- Considerar trade-offs

## Recursos
- "Design Patterns" (Gang of Four)
- "Head First Design Patterns"
- Refactoring Guru
