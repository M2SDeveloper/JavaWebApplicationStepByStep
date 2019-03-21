Adding new Todo

/JavaWebApplicationStepByStep/src/com/advanceJava/todo/TodoServlet.java
```
package com.advanceJava.todo;

import java.io.IOException;
import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

/**
 * Servlet implementation class TodoServlet
 */
@WebServlet(urlPatterns="/todo.do")
public class TodoServlet extends HttpServlet {
	private static final long serialVersionUID = 1L;
	TodoService todoService = new TodoService();

	/**
	 * @see HttpServlet#doGet(HttpServletRequest request, HttpServletResponse
	 *      response)
	 */
	protected void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		
		System.out.println("In Get Method of todoService");
		
		request.setAttribute("todos", todoService.retriveTodo());
		request.getRequestDispatcher("/WEB-INF/views/todo.jsp").forward(request, response);
	}
	
	@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
System.out.println("In post Method of todoService");
		
		String todo=request.getParameter("todo");
		if("".equals(todo))
		{
			request.setAttribute("errorMessage","Enter a valid todo");
		}
		else
		{
			todoService.addTodo(todo);
		}
		request.setAttribute("todos", todoService.retriveTodo());
		request.getRequestDispatcher("/WEB-INF/views/todo.jsp").forward(request, response);
	}
}
```

/JavaWebApplicationStepByStep/WebContent/WEB-INF/views/todo.jsp 
````
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
   <li>${todo.name}</li>
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
