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

   
