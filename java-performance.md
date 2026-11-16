# Java Performance - Otimizacao de Performance em Java

## O que e
Tecnicas para tornar aplicacoes Java mais rapidas e eficientes.

## Profiling

### JVM Tools
// jstack - ver threads
jstack <pid>

// jmap - heap dump
jmap -dump:format=b,file=heap.hprof <pid>

// jstat - estatisticas GC
jstat -gcutil <pid> 1000

// jconsole - monitoring
jconsole <pid>

// VisualVM
visualvm

### Async Profiler
./profiler.sh -d 30 -f profile.html <pid>

## Memory Optimization

### Heap Sizing
// JVM flags
-Xms512m -Xmx2g  // Min/max heap
-XX:MetaspaceSize=128m -XX:MaxMetaspaceSize=256m

// New generation
-Xmn256m
-XX:NewRatio=2

### Object Pooling
class ObjectPool<T> {
    private final BlockingQueue<T> pool;
    
    public ObjectPool(int size, Supplier<T> factory) {
        pool = new ArrayBlockingQueue<>(size);
        for (int i = 0; i < size; i++) {
            pool.offer(factory.get());
        }
    }
    
    public T acquire() throws InterruptedException {
        return pool.take();
    }
    
    public void release(T obj) {
        pool.offer(obj);
    }
}

### String Optimization
// StringBuilder para concatenacao
StringBuilder sb = new StringBuilder();
for (String s : strings) {
    sb.append(s);
}
String result = sb.toString();

// String.intern() para strings duplicadas
String s1 = new String("hello").intern();
String s2 = new String("hello").intern();
// s1 == s2 (mesma referencia)

## Garbage Collection

### GC Types
// G1 (default Java 9+)
-XX:+UseG1GC
-XX:MaxGCPauseMillis=200

// ZGC (low latency)
-XX:+UseZGC
-XX:+ZGenerational

// Shenandoah (low latency)
-XX:+UseShenandoahGC

// Parallel GC (throughput)
-XX:+UseParallelGC

### Tuning
-XX:G1HeapRegionSize=4m
-XX:InitiatingHeapOccupancyPercent=45
-XX:+ParallelRefProcEnabled
-XX:+UseStringDeduplication

## Collections

### Escolher Collection Certa
// ArrayList vs LinkedList
ArrayList: acesso O(1), insercao O(n)
LinkedList: acesso O(n), insercao O(1)

// HashMap vs TreeMap
HashMap: O(1) lookup, sem ordem
TreeMap: O(log n) lookup, ordenado

// HashSet vs TreeSet
HashSet: O(1) lookup, sem ordem
TreeSet: O(log n) lookup, ordenado

### Initial Capacity
// Evitar resizing
HashMap<String, Integer> map = new HashMap<>(1000);
ArrayList<String> list = new ArrayList<>(1000);

### EnumSet/EnumMap
// Mais eficiente que HashSet/HashMap para enums
EnumSet<Day> days = EnumSet.of(Day.MONDAY, Day.FRIDAY);
EnumMap<Day, String> map = new EnumMap<>(Day.class);

## Streams

### Parallel Streams
List<String> result = list.parallelStream()
    .filter(s -> s.length() > 5)
    .map(String::toUpperCase)
    .collect(Collectors.toList());

// Quando usar:
// - CPU-bound tasks
// - Grande volume de dados
// - Operacoes independentes

// Quando NAO usar:
// - I/O bound
// - Pequenos datasets
// - Operacoes com estado

### Evitar Boxing/Unboxing
// Ruim
Stream<Integer> stream = list.stream();
int sum = stream.mapToInt(i -> i).sum();

// Bom
IntStream stream = list.stream().mapToInt(i -> i);
int sum = stream.sum();

## JIT Compilation

### Tiered Compilation
// Default (Java 8+)
-XX:+TieredCompilation

// Ver metodos compilados
-XX:+PrintCompilation

### Escape Analysis
-XX:+DoEscapeAnalysis

// Permite:
// - Stack allocation
// - Lock elision
// - Scalar replacement

## Best Practices

### Object Creation
- Reutilizar objetos quando possivel
- Usar primitivas ao inves de wrappers
- Evitar autoboxing desnecessario

### Collections
- Escolher tamanho inicial adequado
- Usar collections especializadas
- Evitar criar colecoes intermediarias

### Concurrency
- Usar estruturas concorrentes
- Minimizar secoes criticas
- Preferir imutabilidade

### I/O
- Usar buffering
- NIO para I/O intensivo
- Async I/O quando apropriado

## Monitoring

### Metrics
// Micrometer
MeterRegistry registry = new SimpleMeterRegistry();

Counter counter = registry.counter("requests");
counter.increment();

Timer timer = registry.timer("request.duration");
timer.record(() -> {
    // Operacao
});

### Logging
- Nivel apropriado (DEBUG, INFO, WARN, ERROR)
- Structured logging (JSON)
- Nao logar em hot paths
- Usar slf4j

## Quando Otimizar
- Performance nao atende SLA
- High CPU/memory usage
- GC pauses excessivos
- Latencia alta
