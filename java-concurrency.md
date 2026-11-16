# Java Concurrency - Programacao Concorrente em Java

## O que e
Executar multiplos threads/processos simultaneamente para melhor performance.

## Threads

### Criando Threads
// Estendendo Thread
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread running: " + Thread.currentThread().getName());
    }
}

MyThread t = new MyThread();
t.start();

// Implementando Runnable
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Runnable running");
    }
}

Thread t = new Thread(new MyRunnable());
t.start();

// Lambda (Java 8+)
Thread t = new Thread(() -> {
    System.out.println("Lambda thread");
});
t.start();

## Executor Framework

### ExecutorService
ExecutorService executor = Executors.newFixedThreadPool(10);

// Submeter tarefas
for (int i = 0; i < 100; i++) {
    executor.submit(() -> {
        // Tarefa
        return result;
    });
}

executor.shutdown();

### Tipos de Thread Pools
// Fixed pool
ExecutorService fixed = Executors.newFixedThreadPool(10);

// Cached pool (cria threads sob demanda)
ExecutorService cached = Executors.newCachedThreadPool();

// Single thread
ExecutorService single = Executors.newSingleThreadExecutor();

// Scheduled (tarefas periodicas)
ScheduledExecutorService scheduled = Executors.newScheduledThreadPool(5);
scheduled.scheduleAtFixedRate(() -> {
    System.out.println("Executando a cada 5 segundos");
}, 0, 5, TimeUnit.SECONDS);

## Callable e Future

### Callable
Callable<Integer> task = () -> {
    Thread.sleep(1000);
    return 42;
};

ExecutorService executor = Executors.newSingleThreadExecutor();
Future<Integer> future = executor.submit(task);

// Bloqueia ate resultado
Integer result = future.get();

// Com timeout
try {
    Integer result = future.get(5, TimeUnit.SECONDS);
} catch (TimeoutException e) {
    System.out.println("Timeout!");
}

### CompletableFuture
CompletableFuture<String> future = CompletableFuture.supplyAsync(() -> {
    return "Hello";
}).thenApply(s -> s + " World")
  .thenApply(String::toUpperCase);

String result = future.join();

// Combinar futures
CompletableFuture<String> f1 = CompletableFuture.supplyAsync(() -> "Hello");
CompletableFuture<String> f2 = CompletableFuture.supplyAsync(() -> "World");

CompletableFuture<String> combined = f1.thenCombine(f2, (s1, s2) -> s1 + " " + s2);

## Sincronizacao

### synchronized
class Counter {
    private int count = 0;
    
    public synchronized void increment() {
        count++;
    }
    
    public synchronized int getCount() {
        return count;
    }
}

// Bloco sincronizado
synchronized (obj) {
    // Codigo critico
}

### Locks
Lock lock = new ReentrantLock();

lock.lock();
try {
    // Codigo critico
} finally {
    lock.unlock();
}

// TryLock
if (lock.tryLock(1, TimeUnit.SECONDS)) {
    try {
        // Codigo critico
    } finally {
        lock.unlock();
    }
}

## Estruturas Concorrentes

### ConcurrentHashMap
ConcurrentHashMap<String, Integer> map = new ConcurrentHashMap<>();
map.put("key", 1);
map.get("key");
map.computeIfAbsent("key", k -> 1);

### ConcurrentLinkedQueue
Queue<String> queue = new ConcurrentLinkedQueue<>();
queue.offer("item");
String item = queue.poll();

### BlockingQueue
BlockingQueue<String> queue = new ArrayBlockingQueue<>(10);
queue.put("item");  // Bloqueia se cheia
String item = queue.take();  // Bloqueia se vazia

## Atomic Variables

AtomicInteger count = new AtomicInteger(0);
count.incrementAndGet();
count.decrementAndGet();
count.compareAndSet(expected, newValue);

## Volatile

class SharedData {
    private volatile boolean flag = false;
    
    public void setFlag(boolean value) {
        flag = value;
    }
    
    public boolean getFlag() {
        return flag;
    }
}

## Best Practices

### Thread Safety
- Usar estruturas concorrentes (ConcurrentHashMap, etc)
- Minimizar estado compartilhado
- Preferir imutabilidade
- Usar locks apropriados

### Deadlocks
- Adquirir locks em ordem consistente
- Usar tryLock com timeout
- Evitar locks aninhados

### Performance
- Usar thread pools (nao criar threads manualmente)
- Dimensionar pool corretamente
- Evitar bloqueios desnecessarios

## Java 21 Virtual Threads

// Virtual threads (Project Loom)
Thread.startVirtualThread(() -> {
    System.out.println("Virtual thread");
});

// Executor
ExecutorService executor = Executors.newVirtualThreadPerTaskExecutor();
executor.submit(() -> {
    // Tarefa
});

## Quando Usar
- Processamento paralelo
- I/O bound tasks
- Servidores web
- Aplicacoes reativas
