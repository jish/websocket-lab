## Build a websocket echo server

Go to http://websocketd.com/, scroll all the way down to the bottom of the page, and download `websocketd`.

### Write a simple echo server

`websocketd` writes to your program on standard input and reads whatever you write out on standard output.

Let's write a simple Ruby script to echo back the message it received:

```ruby
#!/usr/bin/env ruby

while message = STDIN.gets
  puts "Echo: #{message}"
  STDOUT.flush
end
```

### Create an HTML page to interact with your websocket server

The `ws` protocol, just like `http` can be transfered over a secure channel, (`wss` or `https`) or an insecure channel. Since we're just creating a test server, we're going to use the `ws://` protocol. In production you'll want to use `wss://`.

Let's use this example HTML page:

```html
<html>
  <head>
    <title>Websocket test</title>
  </head>

  <body>
    <h1>Websocket test</h1>

    <script type="text/javascript">
      var ws = new WebSocket('ws://localhost:8080/');

      ws.onmessage = function(event) {
        console.log('Message from server: ' + event.data);
      };

      ws.onopen = function() {
        ws.send('Hello World!');
      }
    </script>
  </body>
</html>
```

### Start it up!

Let's start our websocket server with the following command:

    websocketd --staticdir=. --port=8080 ./echo_server.rb

Now open your browser to http://localhost:8080/ and interact with your server in the developer console:

    ws.send('Hello World!');
