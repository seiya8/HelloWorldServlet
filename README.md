# HelloWorldServlet
## Environment
- Mac OS
- OpenJDK 17.0.12
- Gradle 8.10
- Tomcat 10.1.28

## Process
```bash
$ mkdir HelloWorldServlet && cd HelloWorldServlet
```

```bash
$ gradle init
Starting a Gradle Daemon (subsequent builds will be faster)

Found existing files in the project directory: '/path/to/HelloWorldServlet'.
Directory will be modified and existing files may be overwritten.  Continue? (default: no) [yes, no] yes

Select type of build to generate:
  1: Application
  2: Library
  3: Gradle plugin
  4: Basic (build structure only)
Enter selection (default: Application) [1..4] 1

Select implementation language:
  1: Java
  2: Kotlin
  3: Groovy
  4: Scala
  5: C++
  6: Swift
Enter selection (default: Java) [1..6] 1

Enter target Java version (min: 7, default: 21): 17

Project name (default: HelloWorldServlet):

Select application structure:
  1: Single application project
  2: Application and library project
Enter selection (default: Single application project) [1..2] 1

Select build script DSL:
  1: Kotlin
  2: Groovy
Enter selection (default: Kotlin) [1..2] 2

Select test framework:
  1: JUnit 4
  2: TestNG
  3: Spock
  4: JUnit Jupiter
Enter selection (default: JUnit Jupiter) [1..4] 4

Generate build using new APIs and behavior (some features may change in the next minor release)? (default: no) [yes, no] no


> Task :init
Learn more about Gradle by exploring our Samples at https://docs.gradle.org/8.10/samples/sample_building_java_applications.html

BUILD SUCCESSFUL in 1m 34s
1 actionable task: 1 executed
```
`./app/src/main/java/org/example/HelloWorldServlet.java`:
```java
package org.example;

import java.io.IOException;
import jakarta.servlet.ServletException;
import jakarta.servlet.annotation.WebServlet;
import jakarta.servlet.http.HttpServlet;
import jakarta.servlet.http.HttpServletRequest;
import jakarta.servlet.http.HttpServletResponse;

@WebServlet("/hello")
public class HelloWorldServlet extends HttpServlet {
    protected void doGet(HttpServletRequest request, HttpServletResponse response)
            throws ServletException, IOException {
        response.setContentType("text/html; charset=UTF-8");
        response.getWriter().println("<h1>Hello, World!</h1>");
    }
}
```
`./app/src/webapp/WEB-INF/web.xml`:
```xml
<web-app xmlns="https://jakarta.ee/xml/ns/jakartaee"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="https://jakarta.ee/xml/ns/jakartaee
                             https://jakarta.ee/xml/ns/jakartaee/web-app_6_0.xsd"
         version="6.0">
</web-app>

```

```bash
$ tree .
.
├── app
│  ├── build.gradle
│  └── src
│     ├── main
│     │  ├── java
│     │  │  └── org
│     │  │     └── example
│     │  │        └── HelloWorldServlet.java
│     │  └── resources
│     └── webapp
│        └── WEB-INF
│           └── web.xml
│     └── test
│        ├── java
│        │  └── org
│        │     └── example
│        │        └── AppTest.java
│        └── resources
├── gradle
│  ├── libs.versions.toml
│  └── wrapper
│     ├── gradle-wrapper.jar
│     └── gradle-wrapper.properties
├── gradlew
├── gradlew.bat
├── README.md
└── settings.gradle
```
Build without test:
```bash
$ gradle build -x test
```
Deploy:
```bash
$ cp ./app/build/libs/helloworld.war /usr/local/Cellar/tomcat/10.1.28/libexec/webapps/
$ catalina start
$ open http://localhost:8080/helloworld/hello
```
