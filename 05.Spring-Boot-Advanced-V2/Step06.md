<!---
Current Directory : /Users/rangakaranam/Ranga/git/00.courses/spring-boot-master-class/05.Spring-Boot-Advanced-V2
-->

## Complete Code Example


### /pom.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<parent>
		<groupId>org.springframework.boot</groupId>
		<artifactId>spring-boot-starter-parent</artifactId>
		<version>3.3.4</version>
		<relativePath/> <!-- lookup parent from repository -->
	</parent>
	<groupId>com.in28minutes.springboot</groupId>
	<artifactId>first-rest-api</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<name>first-rest-api</name>
	<description>Demo project for Spring Boot</description>
	<properties>
		<java.version>21</java.version>
	</properties>
	<dependencies>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-web</artifactId>
		</dependency>

		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-devtools</artifactId>
			<scope>runtime</scope>
			<optional>true</optional>
		</dependency>
		<dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-test</artifactId>
			<scope>test</scope>
		</dependency>
	</dependencies>

	<build>
		<plugins>
			<plugin>
				<groupId>org.springframework.boot</groupId>
				<artifactId>spring-boot-maven-plugin</artifactId>
			</plugin>
		</plugins>
	</build>
	<repositories>
		<repository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</repository>
	</repositories>
	<pluginRepositories>
		<pluginRepository>
			<id>spring-milestones</id>
			<name>Spring Milestones</name>
			<url>https://repo.spring.io/milestone</url>
			<snapshots>
				<enabled>false</enabled>
			</snapshots>
		</pluginRepository>
	</pluginRepositories>

</project>
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/FirstRestApiApplication.java

```java
package com.in28minutes.springboot.firstrestapi;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class FirstRestApiApplication {

	public static void main(String[] args) {
		SpringApplication.run(FirstRestApiApplication.class, args);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/helloworld/HelloWorldBean.java

```java
package com.in28minutes.springboot.firstrestapi.helloworld;

public class HelloWorldBean {

	public HelloWorldBean(String message) {
		super();
		this.message = message;
	}

	private String message;

	public String getMessage() {
		return message;
	}

	@Override
	public String toString() {
		return "HelloWorldBean [message=" + message + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/helloworld/HelloWorldResource.java

```java
package com.in28minutes.springboot.firstrestapi.helloworld;

import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.ResponseBody;
import org.springframework.web.bind.annotation.RestController;

//@Controller
@RestController
public class HelloWorldResource {
	// /hello-world => "Hello World"
	
	@RequestMapping("/hello-world")
	public String helloWorld() {
		return "Hello World";
	}

	
	@RequestMapping("/hello-world-bean")
	public HelloWorldBean helloWorldBean() {
		return new HelloWorldBean("Hello World");
	}
	
	//Path Variable or Path Params
	// /user/Ranga/todos/1
	
	@RequestMapping("/hello-world-path-param/{name}")
	public HelloWorldBean helloWorldPathParam(@PathVariable String name) {
		return new HelloWorldBean("Hello World, " + name);
	}
	
	@RequestMapping("/hello-world-path-param/{name}/message/{message}")
	public HelloWorldBean helloWorldMultiplePathParam
					(@PathVariable String name,
							@PathVariable String message) {
		return new HelloWorldBean("Hello World " + name + "," + message);
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/Question.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.util.List;

public class Question {

	public Question() {

	}

	public Question(String id, String description, List<String> options, String correctAnswer) {
		super();
		this.id = id;
		this.description = description;
		this.options = options;
		this.correctAnswer = correctAnswer;
	}

	private String id;
	private String description;
	private List<String> options;
	private String correctAnswer;

	public String getId() {
		return id;
	}

	public String getDescription() {
		return description;
	}

	public List<String> getOptions() {
		return options;
	}

	public String getCorrectAnswer() {
		return correctAnswer;
	}

	@Override
	public String toString() {
		return "Question [id=" + id + ", description=" + description + ", options=" + options + ", correctAnswer="
				+ correctAnswer + "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/Survey.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.util.List;

public class Survey {

	public Survey() {

	}

	public Survey(String id, String title, String description, List<Question> questions) {
		super();
		this.id = id;
		this.title = title;
		this.description = description;
		this.questions = questions;
	}

	private String id;
	private String title;
	private String description;
	private List<Question> questions;

	public String getId() {
		return id;
	}

	public String getTitle() {
		return title;
	}

	public String getDescription() {
		return description;
	}

	public List<Question> getQuestions() {
		return questions;
	}

	@Override
	public String toString() {
		return "Survey [id=" + id + ", title=" + title + ", description=" + description + ", questions=" + questions
				+ "]";
	}

}
```
---

### /src/main/java/com/in28minutes/springboot/firstrestapi/survey/SurveyService.java

```java
package com.in28minutes.springboot.firstrestapi.survey;

import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

import org.springframework.stereotype.Service;

@Service
public class SurveyService {
	
	private static List<Survey> surveys = new ArrayList<>();
	
	static {
	
		Question question1 = new Question("Question1",
		        "Most Popular Cloud Platform Today", Arrays.asList(
		                "AWS", "Azure", "Google Cloud", "Oracle Cloud"), "AWS");
		Question question2 = new Question("Question2",
		        "Fastest Growing Cloud Platform", Arrays.asList(
		                "AWS", "Azure", "Google Cloud", "Oracle Cloud"), "Google Cloud");
		Question question3 = new Question("Question3",
		        "Most Popular DevOps Tool", Arrays.asList(
		                "Kubernetes", "Docker", "Terraform", "Azure DevOps"), "Kubernetes");

		List<Question> questions = new ArrayList<>(Arrays.asList(question1,
		        question2, question3));

		Survey survey = new Survey("Survey1", "My Favorite Survey",
		        "Description of the Survey", questions);

		surveys.add(survey);

		
	}

}
```
---

### /src/main/resources/application.properties

```properties
logging.level.org.springframework=debug
```
---

### /src/test/java/com/in28minutes/springboot/firstrestapi/FirstRestApiApplicationTests.java

```java
package com.in28minutes.springboot.firstrestapi;

import org.junit.jupiter.api.Test;
import org.springframework.boot.test.context.SpringBootTest;

@SpringBootTest
class FirstRestApiApplicationTests {

	@Test
	void contextLoads() {
	}

}
```
---
