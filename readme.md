# MultiStage Build for a Quarkus and Camel Project

## Configuration
```
$ podman machine init
$ podman machine set --memory 4096
$ podman machine start
```

## Build Command
```
$ podman build -t quarkus-camel-native -f multistage.dockerfile  .
```

## Build Logs
```
[1/8] Initializing...                                                                                   (11.5s @ 0.12GB)
 Java version: 21.0.5+11-LTS, vendor version: Mandrel-23.1.5.0-Final
 Graal compiler: optimization level: 2, target machine: x86-64-v3
 C compiler: gcc (redhat, x86_64, 8.5.0)
 Garbage collector: Serial GC (max heap size: 80% of RAM)
 4 user-specific feature(s):
 - com.oracle.svm.thirdparty.gson.GsonFeature
 - io.quarkus.runner.Feature: Auto-generated class by Quarkus from the existing extensions
 - io.quarkus.runtime.graal.DisableLoggingFeature: Disables INFO logging during the analysis phase
 - org.eclipse.angus.activation.nativeimage.AngusActivationFeature
------------------------------------------------------------------------------------------------------------------------
 4 experimental option(s) unlocked:
 - '-H:+AllowFoldMethods' (origin(s): command line)
 - '-H:BuildOutputJSONFile' (origin(s): command line)
 - '-H:-UseServiceLoaderFeature' (origin(s): command line)
 - '-H:+GenerateBuildArtifactsFile' (origin(s): command line)
------------------------------------------------------------------------------------------------------------------------
Build resources:
 - 2.88GB of memory (75.6% of 3.82GB system memory, determined at start)
 - 4 thread(s) (100.0% of 4 available processor(s), determined at start)
[2/8] Performing analysis...  [******]                                                                  (79.9s @ 1.22GB)
   16,426 reachable types   (84.6% of   19,410 total)
   23,966 reachable fields  (61.2% of   39,141 total)
   81,272 reachable methods (57.6% of  141,118 total)
    5,396 types,   160 fields, and 6,278 methods registered for reflection
       62 types,    67 fields, and    55 methods registered for JNI access
        4 native libraries: dl, pthread, rt, z
[3/8] Building universe...                                                                              (10.2s @ 1.52GB)
[4/8] Parsing methods...      [***]                                                                      (6.9s @ 1.63GB)
[5/8] Inlining methods...     [***]                                                                      (4.7s @ 1.84GB)
[6/8] Compiling methods...    [********]                                                                (71.8s @ 1.30GB)
[7/8] Layouting methods...    [***]                                                                      (9.6s @ 1.40GB)
[8/8] Creating image...       [***]                                                                      (9.0s @ 1.59GB)
  35.03MB (44.86%) for code area:    52,444 compilation units
  42.66MB (54.62%) for image heap:  393,914 objects and 331 resources
 408.95kB ( 0.51%) for other data
  78.09MB in total
------------------------------------------------------------------------------------------------------------------------
Top 10 origins of code area:                                Top 10 object types in image heap:
  12.92MB java.base                                           10.95MB byte[] for code metadata
   3.15MB java.xml                                             9.23MB java.lang.Class
   1.99MB c.f.jackson.core.jackson-databind-2.18.1.jar         5.47MB byte[] for java.lang.String
   1.44MB svm.jar (Native Image)                               3.63MB java.lang.String
   1.15MB quarkus-camel-native-1.0-SNAPSHOT-runner.jar         1.38MB com.oracle.svm.core.hub.DynamicHubCompanion
   1.05MB org.apache.camel.camel-main-4.8.1.jar                1.26MB byte[] for general heap data
   1.03MB org.apache.camel.camel-support-4.8.1.jar             1.16MB byte[] for embedded resources
 992.76kB org.apache.camel.camel-base-engine-4.8.1.jar         1.03MB byte[] for reflection metadata
 921.43kB modified-io.vertx.vertx-core-4.5.10.jar            725.04kB java.lang.String[]
 698.69kB org.apache.camel.camel-core-processor-4.8.1.jar    574.80kB c.o.svm.core.hub.DynamicHub$ReflectionMetadata
   9.37MB for 105 more packages                                7.28MB for 3665 more object types
------------------------------------------------------------------------------------------------------------------------
Recommendations:
 HEAP: Set max heap for improved and more predictable memory usage.
 CPU:  Enable more CPU features with '-march=native' for improved performance.
------------------------------------------------------------------------------------------------------------------------
                      23.1s (11.2% of total time) in 1736 GCs | Peak RSS: 2.58GB | CPU load: 3.12
------------------------------------------------------------------------------------------------------------------------
Produced artifacts:
 /code/target/quarkus-camel-native-1.0-SNAPSHOT-native-image-source-jar/build-artifacts.json (build_info)
 /code/target/quarkus-camel-native-1.0-SNAPSHOT-native-image-source-jar/quarkus-camel-native-1.0-SNAPSHOT-runner (executable)
 /code/target/quarkus-camel-native-1.0-SNAPSHOT-native-image-source-jar/quarkus-camel-native-1.0-SNAPSHOT-runner-build-output-stats.json (build_info)
========================================================================================================================
Finished generating 'quarkus-camel-native-1.0-SNAPSHOT-runner' in 3m 24s.
```

## Application Logs
```
podman run -p 8080:8080 localhost/quarkus-camel-native:latest
__  ____  __  _____   ___  __ ____  ______
 --/ __ \/ / / / _ | / _ \/ //_/ / / / __/
 -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \
--\___\_\____/_/ |_/_/|_/_/|_|\____/___/
2024-11-15 16:57:52,248 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.qua.cor.CamelBootstrapRecorder] (main) Apache Camel Quarkus 3.16.0 is starting
2024-11-15 16:57:52,248 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.mai.MainSupport] (main) Apache Camel (Main) 4.8.1 is starting
2024-11-15 16:57:52,253 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.imp.eng.AbstractCamelContext] (main) Apache Camel 4.8.1 (camel-1) is starting
2024-11-15 16:57:52,253 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.imp.eng.AbstractCamelContext] (main) Routes startup (total:1 rest-dsl:1)
2024-11-15 16:57:52,253 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.imp.eng.AbstractCamelContext] (main)     Started hello-world-api (rest://get:/api:/hello-world)
2024-11-15 16:57:52,253 d0630f68edc5 /work/application[1] INFO  [org.apa.cam.imp.eng.AbstractCamelContext] (main) Apache Camel 4.8.1 (camel-1) started in 0ms (build:0ms init:0ms start:0ms)
2024-11-15 16:57:52,257 d0630f68edc5 /work/application[1] INFO  [io.quarkus] (main) quarkus-camel-native 1.0-SNAPSHOT native (powered by Quarkus 3.16.3) started in 0.027s. Listening on: http://0.0.0.0:8080
2024-11-15 16:57:52,258 d0630f68edc5 /work/application[1] INFO  [io.quarkus] (main) Profile prod activated.
2024-11-15 16:57:52,258 d0630f68edc5 /work/application[1] INFO  [io.quarkus] (main) Installed features: [camel-attachments, camel-core, camel-direct, camel-jackson, camel-platform-http, camel-rest, cdi, smallrye-context-propagation, vertx]
```

## API Simulation
```
$ for i in (seq 1 1000);curl -s -k http://localhost:8080/api/hello-world ;end
```

## Statistics
```
$ podman stats -a
ID            NAME               CPU %       MEM USAGE / LIMIT  MEM %       NET IO      BLOCK IO      PIDS        CPU TIME    AVG CPU %
f8745a7b7ce2  gracious_goldberg  0.01%       37.86MB / 4.097GB  0.92%       0B / 0B     0B / 12.29kB  12          1.155723s   0.41%
```