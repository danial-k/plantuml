FROM adoptopenjdk:8-jre-hotspot-bionic

# Install graphviz for visualising complex diagrams
RUN apt-get update
RUN apt-get install -y graphviz

# Get java binary
ARG PLANTUML_VERSION="1.2020.18"
ENV URL=https://repo1.maven.org/maven2/net/sourceforge/plantuml/plantuml/${PLANTUML_VERSION}/plantuml-${PLANTUML_VERSION}.jar
RUN curl -o /usr/local/lib/plantuml.jar ${URL}

# Copy entrypoint to executable directory
COPY plantuml.sh /usr/local/sbin/plantuml
RUN chmod +x /usr/local/sbin/plantuml

# Create directories for processing files
RUN mkdir -p /plantuml/input
RUN mkdir -p /plantuml/output

# Entrypoint to scan directories and run PlantUML
ENTRYPOINT [ "/usr/local/sbin/plantuml" ]
CMD [ "/plantuml/input/**", "-o", "/plantuml/output" ]
