Adding webjars for jquery and bootstrap


```
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
	<modelVersion>4.0.0</modelVersion>
	<groupId>com.in28minutes</groupId>
	<artifactId>in28Minutes-first-webapp</artifactId>
	<version>0.0.1-SNAPSHOT</version>
	<packaging>war</packaging>

	<dependencies>
		<dependency>
			<groupId>javax</groupId>
			<artifactId>javaee-web-api</artifactId>
			<version>6.0</version>
			<scope>provided</scope>
		</dependency>
		<dependency>
			<groupId>javax.servlet</groupId>
			<artifactId>jstl</artifactId>
			<version>1.2</version>
		</dependency>


		<dependency>
			<groupId>org.webjars</groupId>
			<artifactId>bootstrap</artifactId>
			<version>3.3.6</version>
		</dependency>
		<dependency>
			<groupId>org.webjars</groupId>
			<artifactId>jquery</artifactId>
			<version>1.9.1</version>
		</dependency>

	</dependencies>

	<build>
		<pluginManagement>
			<plugins>
				<plugin>
					<groupId>org.apache.maven.plugins</groupId>
					<artifactId>maven-compiler-plugin</artifactId>
					<version>3.2</version>
					<configuration>
						<verbose>true</verbose>
						<source>1.7</source>
						<target>1.7</target>
						<showWarnings>true</showWarnings>
					</configuration>
				</plugin>
				<plugin>
					<groupId>org.apache.tomcat.maven</groupId>
					<artifactId>tomcat7-maven-plugin</artifactId>
					<version>2.2</version>
					<configuration>
						<path>/</path>
						<contextReloadable>true</contextReloadable>
					</configuration>
				</plugin>
			</plugins>
		</pluginManagement>
	</build>
</project>
`````

/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/todo.jsp
`````
<%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c"%>
<!DOCTYPE html>
<html>
<head>
<title>Yahoo!!</title>
<!-- Bootstrap core CSS -->
<link href="/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/css/bootstrap.css"
	rel="stylesheet">
</head>
<body>
	<H1>
		Welcome ${name}
		</H2>
		<div>
			Your Todos are

			<ol>
				<c:forEach items="${todos}" var="todo">
					<li>${todo.name}<a
						href="/JavaWebApplicationStepByStep/deletetodo.do?todo=${todo.name}">Delete</a></li>
				</c:forEach>
			</ol>

			<p>
				<font color="red">${errorMessage}</font>
			</p>
			<form method="POST" action="/JavaWebApplicationStepByStep/todo.do">
				New Todo : <input name="todo" type="text" /> <input name="add"
					type="submit" />
			</form>
		</div>

			<script src="/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/js/bootstrap.min.js"></script>
			<script src="/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/js/jquery-3.3.1.min.js"></script>
</body>
</html>
```
