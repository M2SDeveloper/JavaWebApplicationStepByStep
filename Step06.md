
New Form and doPost

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


@WebServlet(urlPatterns = "/login.do")
public class LoginServlet extends HttpServlet {


	@Override
protected void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
	
	System.out.println("Call comes in get method");
	
	request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
}

@Override
	protected void doPost(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException {
		// TODO Auto-generated method stub
	
	    System.out.println("Call comes in post method");
	    
		request.setAttribute("name", request.getParameter("name"));
		request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
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
	<form action="/login.do" method="POST">
		Name : <input name="name" type="text" /> <input type="submit" />
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
Welcome ${name}
</body>
</html>
```
