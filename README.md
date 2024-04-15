# Commit 1 Reflection notes

The ```handle_connection``` method is fundamental in processing incoming TCP connections. It reads, processes, and prints the HTTP request efficiently.

1. ```mut stream: TcpStream``` The function takes a mutable reference to a TcpStream. This allows the function to read from and write to the stream.
2. ```BufReader::new(&mut stream)``` This wraps the stream in a BufReader, optimizing reading operations by buffering them.
3. ```let http_request: Vec<_> =``` Creates a new variable named http_request. The use of ```Vec<_>``` indicates that this variable will be a vector.
4. ```lines()``` Converts the buffered stream into an iterator over lines.
5. ```map(|result| result.unwrap())``` Processes each line. The unwrap() method is used here to extract the line from the result.
6. ```take_while(|line| !line.is_empty())``` Continues to take lines from the iterator until an empty line is encountered. In HTTP requests, an empty line indicates the end of the headers section.
7. ```collect()``` Gathers all processed lines into the http_request vector.
8. ```println!("Request: {:#?}", http_request)``` Prints out the entire HTTP request.


# Commit 2 Reflection notes
The new ```handle_connection``` method serves an HTTP response based on a fixed HTML file.
1. ```status_line``` For the HTTP response indicating that the request was successful ("HTTP/1.1 200 OK").
2. ```contents``` Reads and unwraps the content of "hello.html".
3. ```length``` Calculates the length of the response content.
4. ```response``` Formats a complete HTTP response string. 
5. ```stream.write_all(response.as_bytes()).unwrap()``` Sends the complete HTTP response including headers and the HTML content.


![image](https://github.com/tvadhisti/advprog-module6/assets/127074983/885b17bc-7ed5-4aab-a756-bbdff3137918) 
![image](https://github.com/tvadhisti/advprog-module6/assets/127074983/7faf516e-6574-44de-b9b6-63c7c37fd54e)

# Commit 3 Reflection notes
The ```handle_connection``` method has been upgraded to better manage different kinds of website requests. When the function gets a request, it first reads the top line to see what the visitor is asking for. If the request is for the main page, marked by ```GET / HTTP/1.1```, the server sends back a positive response with the ```hello.html``` page, telling the visitor everything is okay (200 OK). However, if the request is for a page or resource that isn't available, the server sends back an error page, ```404.html```. This setup helps the server respond correctly depending on what the visitor is looking for.

# Commit 4 Reflection notes
The ```handle_connection``` method now includes more advanced handling of HTTP requests. 

The method first sets up a reader to fetch the first line from the incoming request to understand what the visitor is looking for. Based on this first line:
1. If the visitor requests the main page ("GET / HTTP/1.1"), the server immediately responds with the ```hello.html``` page.
2. If the request is for the "/sleep" page ("GET /sleep HTTP/1.1"), the server waits for 5 seconds before responding with the same ```hello.html``` page.
3. For any other requests that don't match the above patterns, the server responds with the "404.html" error page.

This setup helps the server to not only direct users to the correct content based on their request but also to handle requests that simulate longer processing times.

