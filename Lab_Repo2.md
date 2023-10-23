# CSE 15L Lab Report 2

*Beijie Cheng | Oct. 20, 2023*

## Part 1

A web server called StringServer that supports the behavior of adding messages.

* StringServer.java
  
```
import java.io.IOException;
import java.net.URI;
import java.util.ArrayList;


class Handler implements URLHandler {
    ArrayList<String> messages = new ArrayList<String>();   // Store messages
    int n;  // Number of the message

    public String handleRequest(URI url) {

        if (url.getPath().contains("/add-message")) {   // Add a message
            String[] parameters = url.getQuery().split("=");

            if (parameters[0].equals("s")) {
                n += 1;
                String message = n + ". " + parameters[1];
                messages.add(message);
            }
        }
        return String.join("\n", messages); // print out messages
    }
}

class StringServer {
    public static void main(String[] args) throws IOException {
        if(args.length == 0){
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}

```

* Server.java

```
// A simple web server using Java's built-in HttpServer

// Examples from https://dzone.com/articles/simple-http-server-in-java were useful references

import java.io.IOException;
import java.io.OutputStream;
import java.net.InetSocketAddress;
import java.net.URI;

import com.sun.net.httpserver.HttpExchange;
import com.sun.net.httpserver.HttpHandler;
import com.sun.net.httpserver.HttpServer;

interface URLHandler {
    String handleRequest(URI url);
}

class ServerHttpHandler implements HttpHandler {
    URLHandler handler;
    ServerHttpHandler(URLHandler handler) {
      this.handler = handler;
    }
    public void handle(final HttpExchange exchange) throws IOException {
        // form return body after being handled by program
        try {
            String ret = handler.handleRequest(exchange.getRequestURI());
            // form the return string and write it on the browser
            exchange.sendResponseHeaders(200, ret.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(ret.getBytes());
            os.close();
        } catch(Exception e) {
            String response = e.toString();
            exchange.sendResponseHeaders(500, response.getBytes().length);
            OutputStream os = exchange.getResponseBody();
            os.write(response.getBytes());
            os.close();
        }
    }
}

public class Server {
    public static void start(int port, URLHandler handler) throws IOException {
        HttpServer server = HttpServer.create(new InetSocketAddress(port), 0);

        //create request entrypoint
        server.createContext("/", new ServerHttpHandler(handler));

        //start the server
        server.start();
        System.out.println("Server Started!");
    }
}

```

<img width="684" alt="Screenshot 2023-10-22 at 22 44 47" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/c88bb2fd-fd69-447f-acf4-411570d2746a">

In this page, the functions for the condition of "add-message" is used. The main function is called, and since argc length is not zero, commands in /*public String handleRequest(URI url)*/ is called. The url is assigned to be 3999 here. As the condition /*(url.getPath().contains("/add-message"))*/ in the first if statement is truth. Then, the following string is spilt into two parts and information after "s=" is stored and printed. In the class, both ArrayList and integer changed. The new message is stored into the ArrayList, and the integer n increased by 1 for the new message.

<img width="584" alt="Screenshot 2023-10-22 at 22 54 51" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/5eb97ce4-5361-4f99-b090-59134c3cac41">

In this page, after the main function is called, the functions for the condition of /*return String.join("\n", messages); // print out messages*/ is also called. The url is also 3999 here. Since there is no new message added, so the if command is not called, and the return function outside the if statement will be called. No variable is changed in the class since there is no change made here. Only the information in ArrayList will be printed without changing anything.

## Part 2

<img width="415" alt="Screenshot 2023-10-22 at 23 11 09" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9c033589-8f0a-4a12-af4e-2b8e79b121fa">


<img width="362" alt="Screenshot 2023-10-22 at 23 12 44" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/99a5a5eb-2e9d-49f4-8728-d266a94dad6f">


<img width="661" alt="Screenshot 2023-10-22 at 23 13 33" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9347eb38-6aad-4943-8fd4-d63c92f865de">

## Part 3
In Lab 2 and Lab 3, I learned how to connect to a remote server with the command ssh. With the help of a ssh key, I can connect to a server without a password. Besides, I learned the consist of a url link, including domain, path, query, and anchor. Likewise, to build a local webpage, the command to run a url link should also consider all its consistent as well.





