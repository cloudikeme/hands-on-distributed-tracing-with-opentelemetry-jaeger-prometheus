
```
├── loadgen
│   ├── Dockerfile
│   └── run.sh
├── frontend
│   ├── .gitignore
│   ├── Dockerfile
│   ├── index.js
│   ├── instrument.js
│   ├── package-lock.json
│   ├── package.json
│   └── run.sh
├── backend4-no-instrumentation
│   ├── Dockerfile
│   ├── go.mod
│   ├── go.sum
│   └── main.go
├── backend4
│   ├── Dockerfile
│   ├── go.mod
│   ├── go.sum
│   └── main.go
├── backend3.csproj
├── backend3
│   ├── Properties
│   │   └── launchSettings.json
│   ├── Dockerfile
│   ├── Program.cs
│   └── appsettings.json
├── backend2
│   ├── build
│   │   └── libs
│   │       └── dice-0.0.1-SNAPSHOT.jar
│   ├── gradle
│   │   └── wrapper
│   │       ├── gradle-wrapper.jar
│   │       └── gradle-wrapper.properties
│   ├── src
│   │   └── main
│   │       └── java
│   │           └── io
│   │               └── opentelemetry
│   │                   └── dice
│   │                       ├── DiceApplication.java
│   │                       └── RollController.java
│   ├── resources
│   │   └── application.properties
│   ├── .gitignore
│   ├── Dockerfile
│   ├── build.gradle
│   ├── gradlew
│   ├── gradlew.bat
│   ├── run.sh
│   └── settings.gradle
├── backend1
│   ├── Dockerfile
│   ├── app.py
│   └── requirements.txt
├── app
│   ├── api-server
│   │   └── tracing-config.yaml
│   ├── backend1
│   │   └── run.sh
│   ├── backend2
│   │   └── run.sh
│   ├── backend3
│   │   └── appsettings.Development.json
│   └── backend4-no-instrumentation
│       └── run.sh
├── .github
│   └── workflows
│       └── build_and_push_images.yml
├── otel-env
│   ├── package-lock.json
│   └── backend
│       ├── 01-backend.yaml
│       ├── 03-collector.yaml
│       ├── 05-collector-1.yaml
│       ├── 05-collector-2.yaml
│       ├── 06-backend.yaml
│       ├── 06-collector.yaml
│       └── 07-collector.yaml
├── images
│   ├── api-server.png
│   ├── jaeger-capture-custom-headers.jpg
│   ├── jaeger-spm.png
│   ├── jaeger-tail-sampling.jpg
│   ├── jaeger-trace-detail.jpg
│   ├── jaeger-trace-search.jpg
│   ├── jaeger-with-span.jpg
│   ├── otel-collector.png
│   ├── prometheus_javaagent_metrics_list.jpg
│   ├── prometheus_javaagent_red_metrics.jpg
│   ├── prometheus_spanmetrics.png
│   ├── rolldice-delay.png
│   ├── rolldice-error.png
│   ├── sampling-comparision.jpg
│   ├── sampling-venn.svg
│   ├── scaling-otel-collector.jpg
│   ├── terminated.png
│   └── terminating.png
├── .gitignore
├── collector-docker.yaml
├── instrumentation-head-sampling.yaml
├── instrumentation-java-custom-config.yaml
├── instrumentation-replace-backend2.yaml
├── instrumentation.yaml
├── k8s.yaml
├── otel-daemonset.yaml
├── README.md
├── intro-slides.pdf
├── kind-1.29.yaml
└── tracing-theory.pdf

```

## Description of the structure and content:

This repository structure separates the codebase into distinct components based on function and language, making navigation and maintenance easier. 

**Root Directory:**

* **README.md:**  Provides an overview of the project, installation instructions, and how to run the application.
* **LICENSE:**  Specifies the licensing terms for the codebase.
* **.gitignore:** Defines patterns for files and directories Git should ignore.
* **kind-1.29.yaml**: Configuration file for running Kubernetes locally using kind (Kubernetes in Docker).
* **intro-slides.pdf**: Presentation slides introducing the project and its concepts (likely in PDF format).
* **tracing-theory.pdf**: A document explaining the theory behind distributed tracing (likely in PDF format).

**Core Components:**

* **app:** Contains the configuration and run scripts for the overall application, including individual backends and the API server.
    * **api-server:**  Houses the API server code and configurations for exposing application endpoints.
        * **tracing-config.yaml:** Defines the tracing configuration for the API server.
    * **backend{1,2,3,4,4-no-instrumentation}:** Separate directories for each backend service implementation, categorized by language or framework. Each backend directory includes:
       * **Dockerfile:**  Instructions for building a Docker image for the backend.
       * **run.sh:**  Shell script to execute the backend service.
       * Language-specific files (e.g., `app.py` for Python, `Program.cs` for C#, `main.go` for Go, etc.)

* **frontend:** Contains the code for the frontend application that interacts with the backend services.
    * **Dockerfile:** Instructions for building a Docker image for the frontend.
    * **index.js:**  Likely the main entry point for the frontend application's JavaScript code.
    * **instrument.js:** This file might contain logic for instrumenting the frontend code for tracing. 
    * **package.json:**  Specifies project dependencies and metadata. 
    * **package-lock.json:** Locks dependency versions for consistency.
    * **run.sh:**  Shell script to execute the frontend application.

* **loadgen:** Contains the load generator that simulates traffic to the system.
    * **Dockerfile:**  Instructions for building a Docker image for the load generator.
    * **run.sh:**  Shell script to execute the load generator.

**Infrastructure and Deployment:**

* **collector-docker.yaml:** A Docker Compose file to easily run an OpenTelemetry Collector.
* **instrumentation-{...}.yaml:** These files likely contain OpenTelemetry Collector configurations for different instrumentation scenarios (head-based sampling, custom Java instrumentation, backend replacement).
* **k8s.yaml:** Kubernetes YAML configurations for deploying the application and its components to a Kubernetes cluster.
* **otel-daemonset.yaml:**  Kubernetes configuration for deploying the OpenTelemetry Collector as a DaemonSet, ensuring it runs on every node in the cluster.
* **otel-env:** Likely contains scripts or configurations related to the OpenTelemetry environment setup.
    * **package-lock.json:** Locks dependency versions for any tools used in this environment.
    * **backend:** Contains Kubernetes YAML files for deploying different versions/configurations of the backend services and collectors.

**Documentation and Images:**

* **images:** A directory containing images (PNGs, JPGs, SVGs) used in the documentation or presentation. These images likely illustrate concepts, architectures, or results.

This structured repository promotes:

* **Modularity:** Each component resides in its own directory, simplifying development and testing.
* **Scalability:** New services and features can be added easily without impacting other parts of the application.
* **Maintainability:**  Clear separation of concerns makes it easier to understand, debug, and enhance the codebase. 
* **Reusability:** Individual components (like the load generator) can be reused in other projects.

This setup is ideal for distributed applications with multiple services and utilizes Docker for containerization, potentially Kubernetes for orchestration, and incorporates best practices for distributed tracing.











project-root/
├── .github/
│   └── workflows/
│       └── build_and_push_images.yml
├── .gitignore
├── LICENSE
├── README.md
├── app/
│   ├── api-server/
│   │   ├── tracing-config.yaml
│   ├── backend1/
│   │   ├── Dockerfile
│   │   ├── app.py
│   │   ├── requirements.txt
│   │   └── run.sh
│   ├── backend2/
│   │   ├── build/
│   │   │   └── libs/
│   │   │       └── dice-0.0.1-SNAPSHOT.jar
│   │   ├── gradle/
│   │   │   └── wrapper/
│   │   │       ├── gradle-wrapper.jar
│   │   │       └── gradle-wrapper.properties
│   │   ├── src/
│   │   │   └── main/
│   │   │       └── java/
│   │   │           └── io/
│   │   │               └── opentelemetry/
│   │   │                   └── dice/
│   │   │                       ├── DiceApplication.java
│   │   │                       └── RollController.java
│   │   ├── resources/
│   │   │   └── application.properties
│   │   ├── .gitignore
│   │   ├── Dockerfile
│   │   ├── build.gradle
│   │   ├── gradlew
│   │   ├── gradlew.bat
│   │   ├── run.sh
│   │   └── settings.gradle
│   ├── backend3/
│   │   ├── Properties/
│   │   │   └── launchSettings.json
│   │   ├── Dockerfile
│   │   ├── Program.cs
│   │   ├── appsettings.Development.json
│   │   ├── appsettings.json
│   │   └── backend3.csproj
│   ├── backend4-no-instrumentation/
│   │   ├── Dockerfile
│   │   ├── go.mod
│   │   ├── go.sum
│   │   └── main.go
│   ├── backend4/
│   │   ├── Dockerfile
│   │   ├── go.mod
│   │   ├── go.sum
│   │   └── main.go
│   └── frontend/
│       ├── .gitignore
│       ├── Dockerfile
│       ├── index.js
│       ├── instrument.js
│       ├── package-lock.json
│       ├── package.json
│       └── run.sh
├── loadgen/
│   ├── Dockerfile
│   └── run.sh
├── docs/
│   ├── .gitignore
│   ├── README.md
│   ├── intro-slides.pdf
│   ├── kind-1.29.yaml
│   └── tracing-theory.pdf
├── instrumentation/
│   ├── collector-docker.yaml
│   ├── instrumentation-head-sampling.yaml
│   ├── instrumentation-java-custom-config.yaml
│   ├── instrumentation-replace-backend2.yaml
│   └── instrumentation.yaml
├── k8s/
│   ├── 01-backend.yaml
│   ├── 03-collector.yaml
│   ├── 05-collector-1.yaml
│   ├── 05-collector-2.yaml
│   ├── 06-backend.yaml
│   ├── 06-collector.yaml
│   └── 07-collector.yaml
├── images/
│   ├── api-server.png
│   ├── jaeger-capture-custom-headers.jpg
│   ├── jaeger-spm.png
│   ├── jaeger-tail-sampling.jpg
│   ├── jaeger-trace-detail.jpg
│   ├── jaeger-trace-search.jpg
│   ├── jaeger-with-span.jpg
│   ├── otel-collector.png
│   ├── prometheus_javaagent_metrics_list.jpg
│   ├── prometheus_javaagent_red_metrics.jpg
│   ├── prometheus_spanmetrics.png
│   ├── rolldice-delay.png
│   ├── rolldice-error.png
│   ├── sampling-comparision.jpg
│   ├── sampling-venn.svg
│   ├── scaling-otel-collector.jpg
│   ├── terminated.png
│   └── terminating.png
└── tutorials/
    ├── 01-welcome-setup.md
    ├── 02-tracing-introduction.md
    ├── 03-auto-instrumentation.md
    ├── 04-manual-instrumentation.md
    ├── 05-sampling.md
    ├── 06-RED-metrics.md
    ├── 07-ottl.md
    └── 08-k8s-tracing.md
