	Adding Password, validation of userid/password

package com.advanceJava.Login;

```
\src\main\java\webapp\LoginService.java
```
public class LoginService {
	
	public boolean validateUser(String user, String password) {
		return user.equalsIgnoreCase("mangesh") && password.equals("dummy");
	}
}

```
\src\main\java\webapp\LoginServlet.java
```
package com.advanceJava.Login;

import java.io.IOException;

import javax.servlet.ServletException;
import javax.servlet.annotation.WebServlet;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

@WebServlet(urlPatterns="/login.do")
public class LoginServlet extends HttpServlet {
	
	LoginService service=new LoginService();
	
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
	    
	    Boolean validateUser=service.validateUser(name, password);
	    
	    if(validateUser)
	    {
		request.setAttribute("name", name);
		request.setAttribute("password",password);
		request.getRequestDispatcher("/WEB-INF/views/welcome.jsp").forward(request, response);
	    }
	    else
	    {
	    	request.setAttribute("errorMessage", "Invalid Credentials");
	    	request.getRequestDispatcher("/WEB-INF/views/login.jsp").forward(request, response);
	    }
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
	<form action="/JavaWebApplicationStepByStep/login.do" method="POST">
		UserName : <input  name="name" type="text" />
		Password : <input  name="password" type="password" />
		 <input type="submit" />
		 ${errorMessage}
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

