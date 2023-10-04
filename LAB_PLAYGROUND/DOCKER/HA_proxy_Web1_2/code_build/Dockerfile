# Use an OpenJDK image version 8
FROM openjdk:8
# Maintainer Info
LABEL maintainer="sofiene"
# Copy the executable into the container at /usr/src/myapp
COPY . /usr/src/myapp
# Set /usr/src/myapp as the working directory
WORKDIR /usr/src/myapp
# Compile the java class
RUN javac hello.java
# Run the java app inside the container
CMD ["java", "Hello"]
