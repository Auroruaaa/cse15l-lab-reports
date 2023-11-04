# CSE 15L Lab Report 2

*Beijie Cheng | Nov. 4, 2023 | Resubmission*

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

In the first case, I added “/add-message?s=a” at the end of the link.

In this page, the Class “StringServer” is called to start the Server. After that, I called the method “class Handler implements URLHandler” inside the main functuion. Since I add `/add-message` to the url, the function “public String handleRequest(URI url)” will process my request with the condition of `/add-message`.

In the main funciton, the argument is the port number which is used to start the server. The value of this argument is 3999. In the function “handleRequest”, the argument is “URI url”. In Class “URLHandler”, the integer `num` and String `old_s` will record my request. If I input the request “/add-message” and the query after it, the parameters[1] will record the string message. The `num` will record the number of the query I input and `old_s` will record my previous input and output to the screen. Here, the value of `num` is {1} and the value of `old_s` is {“a”}.

The value `num` and `old_s` changed if I request to “/add-messge” to the Server. `num` changes from 0 to 1 since there was 0 message in Server and my request will add 1 to num. `old_s` was empty as the server started. After I add the query to the url, it will change to `old_s` = “1. a\n”.

<img width="659" alt="Screenshot 2023-11-04 at 15 07 56" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/785f562b-db4c-401c-be24-932ac60178e8">

In this page, I use the link "localhost:3999/add-message?s=abc". Similarly, the Class “StringServer” is called to start the Server, and the method “class Handler implements URLHandler” is called inside the main functuion. Since I also use `/add-message` to the url, the function “public String handleRequest(URI url)” will process my request with the condition of `/add-message`.

In the main funciton, the argument is the port number which is used to start the server. The value of this argument is 3999. In the function “handleRequest”, the argument is “URI url”. And the function "handleRequest" is called just like the previous case. This time, the integer `num` increases to 2 since this is the second time processing this request. The String old_s will be used to memorize my previous input as well as the record this time. The parameters[1] will record the string message, which is "abc" here.

The value of `num` changes from 1 to 2 since I made a new request. `old_s` was "1. a\n" and changed to “1. a\n2. abd\n”, meaning that it stores the history of my requests.


## Part 2

The path to the private key for my SSH key on my Computer is `/Users/jessicacheng/.ssh`.

<img width="357" alt="Screenshot 2023-11-04 at 15 15 28" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/c69dc78d-2b93-4fda-948e-71bf83853a93">


The path to the public key for my SSH key for login ieng6 in my account is `/home/linux/ieng6/cs151fa23/cs151fa23sv/ssh`.

<img width="415" alt="Screenshot 2023-10-22 at 23 11 09" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9c033589-8f0a-4a12-af4e-2b8e79b121fa">

To access the server:

<img width="661" alt="Screenshot 2023-10-22 at 23 13 33" src="https://github.com/Auroruaaa/cse15l-lab-reports/assets/116754028/9347eb38-6aad-4943-8fd4-d63c92f865de">

## Part 3
In Lab 2 and Lab 3, I learned how to connect to a remote server with the command ssh. With the help of a ssh key, I can connect to a server without a password. Besides, I learned the consist of a url link, including domain, path, query, and anchor. Likewise, to build a local webpage, the command to run a url link should also consider all its consistent as well.





