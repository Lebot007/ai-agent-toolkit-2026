# JVM Optimization - Otimizacao da JVM

## O que e
Configurar e otimizar a Java Virtual Machine para melhor performance.

## JVM Flags Essenciais

### Heap Memory
-Xms512m              // Initial heap size
-Xmx2g                // Maximum heap size
-Xmn256m              // Young generation size
-XX:NewRatio=2        // Ratio of old/young generation
-XX:SurvivorRatio=8   // Ratio of eden/survivor

### Metaspace (Java 8+)
-XX:MetaspaceSize=128m
-XX:MaxMetaspaceSize=256m

### Stack
-Xss512k              // Thread stack size

## Garbage Collectors

### G1 GC (Default Java 9+)
-XX:+UseG1GC
-XX:MaxGCPauseMillis=200
-XX:G1HeapRegionSize=4m
-XX:InitiatingHeapOccupancyPercent=45

### ZGC (Ultra-low latency)
-XX:+UseZGC
-XX:+ZGenerational
-XX:SoftMaxHeapSize=2g

### Shenandoah (Low latency)
-XX:+UseShenandoahGC
-XX:ShenandoahGCHeuristics=compact

### Parallel GC (High throughput)
-XX:+UseParallelGC
-XX:ParallelGCThreads=4

## Compilation

### Tiered Compilation
-XX:+TieredCompilation
-XX:TieredStopAtLevel=5

### JIT Tuning
-XX:CompileThreshold=10000
-XX:+PrintCompilation
-XX:+PrintInlining

## Performance Flags

### Escape Analysis
-XX:+DoEscapeAnalysis

### String Deduplication
-XX:+UseStringDeduplication

### Compressed Oops
-XX:+UseCompressedOops
-XX:+UseCompressedClassPointers

### Large Pages
-XX:+UseLargePages

## Monitoring Flags

### GC Logging (Java 11+)
-Xlog:gc*:file=gc.log:time,uptime,level,tags:filecount=5,filesize=10M

### GC Logging (Java 8)
-XX:+PrintGCDetails
-XX:+PrintGCDateStamps
-XX:+PrintGCTimeStamps
-Xloggc:gc.log

### Heap Dump on OOM
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/path/to/dumps

## Profiling Tools

### Built-in Tools
- jconsole
- jvisualvm
- jmc (Mission Control)
- jfr (Flight Recorder)

### JFR (Flight Recorder)
-XX:StartFlightRecording=duration=60s,filename=recording.jfr

// Analyze
jfr print recording.jfr

### External Tools
- Async Profiler
- YourKit
- JProfiler

## Best Practices

### Production Settings
// Example production JVM flags
-Xms4g -Xmx4g
-XX:+UseG1GC
-XX:MaxGCPauseMillis=200
-XX:InitiatingHeapOccupancyPercent=45
-XX:+ParallelRefProcEnabled
-XX:+UseStringDeduplication
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=/var/dumps
-Xlog:gc*:file=/var/log/gc.log:time,uptime,level,tags:filecount=5,filesize=10M

### Development Settings
// Example dev JVM flags
-Xms512m -Xmx1g
-XX:+UseG1GC
-XX:MaxGCPauseMillis=500
-XX:+HeapDumpOnOutOfMemoryError
-XX:HeapDumpPath=./dumps

## Monitoring

### JMX
-Dcom.sun.management.jmxremote
-Dcom.sun.management.jmxremote.port=9010
-Dcom.sun.management.jmxremote.authenticate=false
-Dcom.sun.management.jmxremote.ssl=false

### Prometheus JMX Exporter
// jmx_prometheus_javaagent.jar
-javaagent:jmx_prometheus_javaagent.jar=8080:jmx_config.yaml

## Troubleshooting

### High CPU
1. Identificar thread: jstack <pid>
2. Analisar com profiler
3. Verificar loops infinitos
4. Otimizar hot paths

### High Memory
1. Heap dump: jmap -dump:format=b,file=heap.hprof <pid>
2. Analisar com MAT (Memory Analyzer Tool)
3. Identificar memory leaks
4. Ajustar heap size

### GC Pauses
1. Habilitar GC logging
2. Analisar pause times
3. Escolher GC apropriado
4. Tuning de geracoes

## Container Support

### Docker/Kubernetes
-XX:+UseContainerSupport
-XX:MaxRAMPercentage=75.0
-XX:InitialRAMPercentage=50.0

### Java 10+ (automatic)
// Detecta limites do container automaticamente
-XX:MaxRAMPercentage=75.0

## Version-Specific Features

### Java 11+
- ZGC production ready
- Shenandoah GC
- Flight Recorder open source

### Java 17+
- Strong encapsulation
- Sealed classes
- Pattern matching

### Java 21+
- Virtual threads (Project Loom)
- ZGC generational
- Sequenced collections

## Quando Otimizar
- Performance nao atende SLA
- High CPU/memory usage
- GC pauses excessivos
- Latencia alta
- Problemas em producao
