	Adding a TodoService and Todos to welcome.jsp
  
 ```
\src\main\java\webapp\LoginServlet.java
```
package webapp;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

import com.advanceJava.todo.Todo;
import com.advanceJava.todo.TodoService;

@WebServlet(urlPatterns="/login.do")
public class LoginServlet extends HttpServlet {
	
	LoginService loginService=new LoginService();
	TodoService todoService=new TodoService();
	
@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	
	System.out.println("Call comes in get method");
	
	request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
}

@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
	
	    System.out.println("Call comes in post method");
	    
	    String name=request.getParameter("name");
	    String password=request.getParameter("password");
	    
	    Boolean validateUser=loginService.validateUser(name, password);
	    List<Todo> todos=todoService.retriveTodo();
	    
	    if(validateUser)
	    {
		request.setAttribute("name", name);
		request.setAttribute("password",password);
		request.setAttribute("todos", todos);
		request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
	    }
	    else
	    {
	    	request.setAttribute("errorMessage", "Invalid Credentials");
	    	request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
	    }
	}
}


}
```
\src\main\java\webapp\todo\Todo.java
```
package webapp.todo;

public class Todo {

	public Todo(String name) {
		super();
		this.name = name;
	}

	private String name;

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public String toString() {
		return "Todo [name=" + name + "]";
	}
}
```
\src\main\java\webapp\todo\TodoService.java
```
package webapp.todo;

import java.util.ArrayList;
import java.util.List;

public class TodoService {
	private static List<Todo> todos = new ArrayList();

	static {
		todos.add(new Todo("Learn Web Application"));
		todos.add(new Todo("Learn Spring"));
		todos.add(new Todo("Learn Spring MVC"));
	}

	public List<Todo> retrieveTodos() {
		return todos;
	}
}
```
\\src\main\webapp\WEB-INF\views\login.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
	<p><font color="red">${errorMessage}</font></p>
	<form action="/login.do" method="POST">
		Name : <input name="name" type="text" /> Password : <input name="password" type="password" /> <input type="submit" />
	</form>
</body>
</html>
```
\src\main\webapp\WEB-INF\views\welcome.jsp
```
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
<H1>Welcome ${name}</H2>
<div>
Your Todos are
${todos}
</div>
</body>
</html>
```
\src\main\webapp\WEB-INF\web.xml
```
<!-- webapp/WEB-INF/web.xml -->
<web-app xmlns="http://java.sun.com/xml/ns/javaee" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd"
	version="3.0">

	<display-name>To do List</display-name>

	<welcome-file-list>
		<welcome-file>login.do</welcome-file>
	</welcome-file-list>
</web-app>
```
