Delete Todo with equals and hashcode methods

/JavaWebApplicationStepByStep/src/com/advanceJava/todo/DeleteTodoServlet.java
```
package com.advanceJava.todo;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class DeleteTodoServlet
 */
@WebServlet(urlPatterns = "/deletetodo.do")
public class DeleteTodoServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
    TodoService todoService=new TodoService();
  
    public DeleteTodoServlet() {
        super();
    }

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		
		System.out.println("In Get Method of deleteTodoService");
		todoService.deleteTodo(request.getParameter("todo"));
		response.sendRedirect("/JavaWebApplicationStepByStep/todo.do");
	}

}
```

/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/todo.jsp
```
<%@ taglib uri = "http://java.sun.com/jsp/jstl/core" prefix = "c" %>
<html>
<head>
<title>Yahoo!!</title>
</head>
<body>
<H1>Welcome ${name}</H2>
<div>
Your Todos are

<ol>
<c:forEach items="${todos}" var="todo">
   <li>${todo.name} <a href="/JavaWebApplicationStepByStep/deletetodo.do?todo=${todo.name}">Delete</a></li> 
</c:forEach>
</ol>

<p><font color="red">${errorMessage}</font></p>
<form method="POST" action="/JavaWebApplicationStepByStep/todo.do">
New Todo : <input name="todo" type="text" /> <input name="add" type="submit" />
</form>

</div>
</body>
</html>
```
/JavaWebApplicationStepByStep/src/com/advanceJava/todo/Todo.java
```
/**
 * 
 */
package com.advanceJava.todo;

/**
 * @author Mangesh
 *
 */
public class Todo {
	 
	private String name;

	public Todo(String name) {
		super();
		this.name = name;
	}

	public String getName() {
		return name;
	}

	public void setName(String name) {
		this.name = name;
	}

	@Override
	public int hashCode() {
		final int prime = 31;
		int result = 1;
		result = prime * result + ((name == null) ? 0 : name.hashCode());
		return result;
	}

	@Override
	public boolean equals(Object obj) {
		if (this == obj)
			return true;
		if (obj == null)
			return false;
		if (getClass() != obj.getClass())
			return false;
		Todo other = (Todo) obj;
		if (name == null) {
			if (other.name != null)
				return false;
		} else if (!name.equals(other.name))
			return false;
		return true;
	}

	@Override
	public String toString() {
		return "Todo [name=" + name + "]";
	}

}
```
/JavaWebApplicationStepByStep/src/com/advanceJava/todo/TodoService.java
```
package com.advanceJava.todo;

import java.util.ArrayList;
import java.util.List;

public class TodoService {

	private static List<Todo> todos = new ArrayList<>();

	static {
		todos.add(new Todo("Learn Web Application"));
		todos.add(new Todo("Learn Spring"));
		todos.add(new Todo("Learn spring MVC"));
	}

	public List<Todo> retriveTodo()
	{
		return todos;
	}

	public void addTodo(String todo) {
		todos.add(new Todo(todo));
	}

	public void deleteTodo(String parameter) {
		todos.remove(new Todo(parameter));
		
	}
}
```
