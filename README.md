First, you need to install [Ratchet](http://socketo.me/)

~~~
composer require cboden/ratchet
~~~
or
~~~
php ~/composer.phar require cboden/ratchet
~~~

Then you can start the WebSocket server:

~~~
php artisan websockets:run
~~~


You can specify a `--port` if you want to, default is **8080**.

Then add the client component on your page/layout. You can set an `uri` property if you are running on a different port. Default is `ws://localhost:8080/`.

~~~
[websocket]
~~~

It uses an AJAX framework-like API, is familiar for OctoberCMS developers

~~~
data-websocket-event="name"
~~~
It fires up `send()` method with the specified event name.

~~~
data-websocket-oneventname="console.log(event)"
~~~
It evals the informed script, just like AJAX framework with a data argument.

**You are ready to rock on sockets. Build a chat app!**

Don't forget to add [jQuery](http://jquery.com/) and `{% scripts %}` placeholder.

    url = "websockets"
    [websocket]
    ==
    <!DOCTYPE html>
    <html>
        <head>
            <meta charset="utf-8">
            <title>Web Sockets</title>
        </head>
        <body>
            <ul data-websocket-onmessage="$(this).append('<li>'+event.payload.text+'</li>')"></ul>

            <form role="form" data-websocket-event="message">
                <input type="text" name="text">
                <button type="submit">Send</button>
            </form>

            <script src="//code.jquery.com/jquery-1.12.0.min.js"></script>
            {% scripts %}
        </body>
    </html>
