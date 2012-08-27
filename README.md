## This Fork:

#### JSONRPC 2.0 Compatibility
Added `jsonrpc: "2.0"`, the required field to jsonrpc header, to enable compatibility with new jsonrpc 2.0 client libraries like [jquery-jsonrpc](https://github.com/datagraph/jquery-jsonrpc)

- - - 

#### The original thorough [documentation](http://jsonrpcphp.org/?page=crashcourse&lang=en)

----

#### Here it goes anyways for quick reference:

On the server side, the *jsonRPCServer* class has simply one static method. So, no objects have to be instanced. However, the object animating the service must be instanced, since the creation normally establishes the interaction of the object with the local enviroment (the database connection, some filesystem path, some configuration parameter, etc.)


The server is prepared by:



    <?php

        include 'jsonRPCServer.php;

        $myObject = new myClass($params);

        jsonRPCServer::handle($myObject);

    ?>



As you can see, the object is passed to the server in its current state. So, it is possible to give the server an object with a previuos life longer than a fresh created object, that is an object with an internal state more sofisticated than a new object.

Once the object is given to the server, all its methods will be available as JSON-RPC requests.


On the client-side, things are even more easy.

Once known the existence of a service at a given URL, it is simply necessary to create a *jsonRPCClient* object, instanced passing the server URL to the constructor.



    <?php

        include 'jsonRPCClient.php;

        $myObject = new jsonRPCClient('http://servername/path/serverJSONRPC');

    ?>



The object `$myObject` so created in the C host will behave _exactly_ like the `$myObject` object of the S host.


If the jsonRPCServer and jsonRPCClient classes are used separately (i.e. to serve or consume functionality exchange with remote systems) these basic principles don't change.
