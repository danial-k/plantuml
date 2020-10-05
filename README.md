PlantUML
===
Plant UML is a tool to generate diagrams from text documents.
The documents should be written in the PlantUML reference language.

# Ecosystem
- VSCode [plugin](https://marketplace.visualstudio.com/items?itemName=jebbs.plantuml) available to render simple diagrams (⌥ + D) and complex diagrams if GraphViz is installed.
- Markdown renderer via [python-markdown](https://github.com/mikitex70/plantuml-markdown)
- AWS [icon library](https://github.com/awslabs/aws-icons-for-plantuml) published by awslabs.

# Running locally
Requirements:
- Java only for simple sequence and activity diagrams
- Download jar archive
- GraphViz for more complex diagrams (MacPorts on MacOS)

Once installed, `png` diagrams may be generated with:
```shell
java -jar plantuml.jar simple.txt
```

# Running in Docker
Build an image using [docker/Dockerfile]:
```
cd docker
docker build -t plantuml:1.0.0 .
```

Start up the container, for example processing the `advanced.puml` file, mounting the local `input` and `output` directories to the `/plantuml/input` and `/plantuml/input` directories in the container. The [docker/plantuml.sh](entrypoint) is designed to scan all directories in the `input` directory and populate the `output` directory.
```shell
docker run \
-v $(pwd)/output:/plantuml/output \
-v $(pwd)/input:/plantuml/input \
plantuml:1.0.0
```

# PlantUML Server in Docker
PlantUML server is offered as a [Docker container](https://hub.docker.com/r/plantuml/plantuml-server) that launches a browser-based renderer:
```shell
docker run -d \
-p 8080:8080 \
plantuml/plantuml-server:jetty
```
Scripts should be entered via the browser and the results exported
