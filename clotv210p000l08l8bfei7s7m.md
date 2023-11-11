---
title: "Create a basic chat app using Socket.io and React"
datePublished: Sat Nov 11 2023 09:45:03 GMT+0000 (Coordinated Universal Time)
cuid: clotv210p000l08l8bfei7s7m
slug: create-a-basic-chat-app-using-socketio-and-react
tags: websockets, socketio, web-development, reactjs, real-time-communication

---

![Create a Secure Chat Application with Socket.IO and React | Okta Developer](https://developer.okta.com/assets-jekyll/blog/socket-io-react-tutorial/socket-io-tutorial-f43fd09682930e21b8d0ce17a788603a5c2d04b685b35bdf46894e9439940440.png align="left")

In this blog, we delve into the core of creating a basic chat application, focusing intently on the foundational aspect: setting up the server for peer-to-peer communication. Join this journey as we decipher the underlying mechanics that power this direct, real-time communication.

Moreover, I've tried to provide comprehensive insights into the functionality of the utilized packages. This addition ensures that the project is a solid entry point for anyone looking to embark on their WebSocket journey. It's designed to offer a robust foundation, making it an excellent starting point for those venturing into the realm of web sockets.

We will start by creating two separate directories in the root directory:

* client
    
* server
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684572959/1718b792-b69b-4f26-8349-77fe9ca707a8.png align="center")

1. First, create the React app.
    

* In the terminal navigate to the client directory.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684633175/5d2c665c-f7b9-41a7-a14e-ccbc70748179.png align="center")

* Now run the following command to create the React app
    

```bash
npx create-react-app .
```

* Now start the react app on port 3000 i.e [`http://localhost:3000/`](http://localhost:3000/)
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684678542/609c230b-608e-4554-8416-ce0a2dddb1f6.png align="center")

1. Now set up the backend
    

* Open a new terminal and navigate to the server directory
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684732494/cc64ce6b-f62e-4bbf-b4f0-7daaa2c650d6.png align="center")

* set up the express js server, we will run the following commands
    

```bash
npm init
```

Press enter for all the questions

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684811704/3d72402c-c2a8-4096-afdc-e39d1d53766f.png align="center")

* Create an ***<mark>index.js</mark>*** file inside the server directory
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699684964356/88e728c2-42e7-44ae-8290-461fd3fc4630.png align="center")

* Now in the terminal, in the server directory, type the following command to install the backend dependencies
    

```bash
npm i express
```

* We further install a few more packages and run the following command to install them.
    

```bash
npm i cors nodemon socket.io
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685024610/59d9dcf7-25a5-4458-932f-6fbcfacca46f.png align="center")

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685041380/ae6c366d-af72-41d7-b050-1ec4343a049d.png align="center")

* **Express**: A flexible Node.js web application framework, Express simplifies the creation of robust APIs and web applications. It provides a set of features for building web applications and APIs.
    
* **Cors**: Short for Cross-Origin Resource Sharing, Cors is a crucial package that ensures secure communication between different domains or origins in a web application. It allows or disallows cross-origin requests, a key aspect for our chat app's functionality.
    
* **Nodemon**: A utility that aids in the development process by monitoring changes in the server-side code. It automatically restarts the server upon detecting modifications, enabling a smoother development experience without manual restarts.
    
* [**Socket.io**](http://Socket.io): This package facilitates real-time, bidirectional communication between the server and the client. It's pivotal for enabling instantaneous and seamless communication in our chat app, forming the backbone of real-time interactions.
    

1. We will set up the express js server, you can copy-paste the following piece of code into index.js file to set up the starter server.
    

```javascript
const express=require('express');
const app=express();

app.listen(3001,()=>{
    console.log('server is running on port 3001');
})
```

* Start the nodemon server in the terminal using the following command
    

```bash
nodemon index.js
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685307626/9e460cac-f874-43c6-97f7-20328b5dcd1e.png align="center")

1. Now we proceed to set the socket server
    

```javascript
const express=require('express');
const http=require('http');
const {Server}=require('socket.io');
const app=express();

server.listen(3001,()=>{
    console.log('server is running on port 3001');
})
```

* The [Socket.io](http://Socket.io) library provides real-time, bidirectional communication between web clients and servers. The `Server` class from [Socket.io](http://Socket.io) is a key component for creating and managing WebSocket connections. It allows you to handle events, manage rooms, and facilitate real-time communication between the server and the connected clients.
    
* We import the built-in HTTP module, providing functionalities to create an HTTP server and handle HTTP-related operations. This module allows you to create server instances, handle incoming HTTP requests, manage responses, and work with the HTTP protocol in Node.js applications.
    

1. Set up the client-side interface
    

* Clear the ***App.js*** file.
    

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685434066/a21ee0e9-6cb2-434d-a345-57385830d1c1.png align="center")

1. Open a new terminal and run the following commands
    

```markdown
cd client
```

```markdown
npm i socket.io-client
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685526259/33df31cb-635d-4886-90f4-79f8abf7461a.png align="center")

* The primary purpose of `socket.io-client` is to allow your front-end, typically in a web browser, to establish a connection with a [Socket.io](http://Socket.io) server. It provides functionalities for emitting events, receiving data, and handling real-time communication events between the server and the connected clients.
    
* This library enables the web client to establish and manage WebSocket connections with the [Socket.io](http://Socket.io) server, facilitating seamless real-time communication in applications such as chat apps, live updates, or any scenario where instantaneous data exchange is required between the server and the client.
    

1. Connect client to server
    

```javascript
import React, { useEffect, useState } from 'react';
import io from 'socket.io-client';

const socket = io.connect('http://localhost:3001');
const App = () => {
    return(
        <div>App</div>
    )
};

export default App;
```

* When you're developing a real-time application using [Socket.io](http://Socket.io), this line is crucial for establishing a connection between your client-side (front-end, typically a web browser) and the [Socket.io](http://Socket.io) server. This connection allows your client to send and receive real-time events and data.
    

1. Connect server to client
    

```javascript
const express=require('express');
const app=express();
const http=require('http');
const {Server}=require('socket.io');
const cors=require('cors');

app.use(express.json());
app.use(cors());

const server=http.createServer(app);
const io=new Server(server,{
    cors:{
        origin: 'http://localhost:3000',
        methods: ['GET', 'POST']
    }
})





server.listen(3001,()=>{
    console.log('server is running on port 3001');
})
```

* ***<mark>app.use(express.json())</mark>*** is middleware provided by Express. It parses incoming requests with JSON payloads. This middleware extracts the JSON object from the request body, making it accessible in your application via **req.body**.
    
* ***<mark>app.use(cors())</mark>*** integrates Cors into your Express app. Cors is crucial for managing cross-origin HTTP requests, enabling or restricting access from different origins to your server. It facilitates secure communication between different domains, preventing or allowing cross-origin requests.
    
* ***<mark>const server = http.createServer(app)</mark>*** creates an HTTP server using the Express app. This server instance handles the incoming requests.
    
* ***<mark>const io = new Server(server, { cors: { /* configuration */ } })</mark>*** initializes the [Socket.io](http://Socket.io) server. Here, you are providing a configuration object to the [Socket.io](http://Socket.io) server setup, specifying Cors options.
    
* The ***<mark>cors</mark>*** key within the configuration object of [Socket.io](http://Socket.io) helps define the allowed origin and methods. In this case, it allows communication from '[http://localhost:3000](http://localhost:3000)' and only permits 'GET' and 'POST' methods.
    

1. Confirm if the server socket connection is functional
    

```javascript
io.on('connection',(socket)=>{
    console.log('user connected',socket.id)
})
```

![](https://cdn.hashnode.com/res/hashnode/image/upload/v1699685822276/ec29e60b-a580-48a7-9db4-c00c46bcc775.png align="center")

* io: Refers to the instance of the [Socket.io](http://Socket.io) server that has been set up. It represents the main entry point for [Socket.io](http://Socket.io) functionalities on the server side.
    
* The ***<mark>on()</mark>*** method is used to listen for specific events. Here, **'connection'** is a built-in event in [Socket.io](http://Socket.io) that occurs whenever a client connects to the [Socket.io](http://Socket.io) server.
    

## How does socket communicate

[Socket.io](http://Socket.io) is a powerful tool for enabling real-time bidirectional communication between the server (backend) and clients (frontend). It works through a series of events facilitated by the ***<mark>emit</mark>*** and ***<mark>on</mark>*** methods.

* ***emit***: Used to send events. It can be used on both the server and the client. On the server, ***<mark>socket.emit()</mark>*** sends events to specific connected clients or broadcasts to all clients. On the client, ***<mark>socket.emit()</mark>*** sends events back to the server.
    
* ***on***: Used to listen for events. It's used both on the server and the client. On the server, ***<mark>socket.on()</mark>*** listens for events sent from the client. On the client, ***<mark>socket.on()</mark>*** listens for events from the server.
    

### Custom events

Custom events can represent various actions in your application, such as messaging, notifications, updates, or any other specific functionalities required in your real-time application. You define the name of the event and use it to trigger actions and exchange data between the server and clients, tailoring the communication to your application's needs.

example:

* ***<mark>socket.emit('customEvent', data)</mark>***: Emits a custom event from the server to a specific client.
    
* ***<mark>socket.on('customEvent', (data) =&gt; { /* handle data */ })</mark>***: Listens for a custom event on the client side.
    

1. setup the client-side interface to send messages
    

```javascript
import React, { useEffect, useState } from 'react';
import io from 'socket.io-client';

const socket = io.connect('http://localhost:3001');

const App = () => {
  const [message, setMessage] = useState('');

  const handleInputChange = (e) => {
    setMessage(e.target.value);
  };

  return (
    <div className="app">
      <input
        type="text"
        placeholder="message"
        value={message}
        onChange={handleInputChange}
      />
      <button onClick={sendMessage}>Send message</button>
      <h1>Message:</h1>
    </div>
  );
};

export default App;
```

1. emit send message event from frontend
    

```javascript
import React, { useEffect, useState } from 'react';
import io from 'socket.io-client';

const socket = io.connect('http://localhost:3001');

const App = () => {
  const [message, setMessage] = useState('');
  const [messageReceived,setMessageReceived]=useState()

  const sendMessage = () => {
    socket.emit('send_message', { message });
  };

  const handleInputChange = (e) => {
    setMessage(e.target.value);
  };

  return (
    <div className="app">
      <input
        type="text"
        placeholder="message"
        value={message}
        onChange={handleInputChange}
      />
      <button onClick={sendMessage}>Send message</button>
      <h1>Message:</h1>
      {messageReceived}
    </div>
  );
};

export default App;
```

* **socket.emit('send\_message', { message }):**
    
    * This line uses the ***emit*** function provided by the WebSocket library to send a 'send\_message' event to the server.
        
    * It passes an object <mark>{ message } </mark> containing the user's entered message to the server.
        

1. Receive the message in the backend
    

```javascript
const express=require('express');
const app=express();
const http=require('http');
const {Server}=require('socket.io');
const cors=require('cors');

app.use(express.json());
app.use(cors());

const server=http.createServer(app);
const io=new Server(server,{
    cors:{
        origin: 'http://localhost:3000',
        methods: ['GET', 'POST']
    }
})

io.on('connection',(socket)=>{
    console.log('user connected',socket.id)

    socket.on('send_message',(data)=>{
        socket.broadcast.emit('receive_message',data);
    })
})



server.listen(3001,()=>{
    console.log('server is running on port 3001');
})
```

* The ***<mark>io.on('connection', (socket) =&gt; { ... })</mark>*** block represents the server-side code that runs when a client establishes a connection to the [Socket.io](http://Socket.io) server. This block listens for a '***send\_message'*** event from the connected client. The socket variable represents the specific client that just connected, identified by a unique socket.id.
    
* The ***<mark>socket.broadcast.emit</mark>*** line broadcasts the 'receive\_message' event and the accompanying data to all other connected clients except the one that initiated the 'send\_message' event.
    
* So basically, this code snippet receives a 'send\_message' event from the client and then broadcasts a 'receive\_message' event to all other connected clients, effectively sharing the message received from one client with all the others.
    

1. receive the server message in the frontend using hooks
    

```javascript
import React, { useEffect, useState } from 'react';
import io from 'socket.io-client';

const socket = io.connect('http://localhost:3001');

const App = () => {
  const [message, setMessage] = useState('');
  const [messageReceived,setMessageReceived]=useState()

  const sendMessage = () => {
    socket.emit('send_message', { message });
  };

  useEffect(() => {
    socket.on('receive_message', (data) => {
        setMessageReceived(data.message);
    });
  }, []);

  const handleInputChange = (e) => {
    setMessage(e.target.value);
  };

  return (
    <div className="app">
      <input
        type="text"
        placeholder="message"
        value={message}
        onChange={handleInputChange}
      />
      <button onClick={sendMessage}>Send message</button>
      <h1>Message:</h1>
      {messageReceived}
    </div>
  );
};

export default App;
```

* The ***<mark>socket.on('receive_message', (data) =&gt; { ... })</mark>*** code establishes a listener for the '<mark>receive_message</mark>' event. When the 'receive\_message' event is emitted from the server, the client (front-end) receives it.*<mark>setMessageReceived(data.message)</mark>* updates the local state of the component, displaying the received message in the user interface.
    

# The end!

Feel free to add your own CSS...

### Congratulations! You just developed your first chat app using react and socket.io.

In our tutorial, we've concentrated on setting up one-on-one communication between peers. Now, we're advancing to configuring rooms where multiple individuals can create or join via a unique room ID, engaging in group chats. Additionally, we'll implement features like automatic scrolling and message persistence for a more enriched user experience. Stay tuned as we take this next step towards fostering dynamic, multi-user interactions in our chat application!

# Check out socials

# [Twitter](https://twitter.com/Karthikreincar1)

# [Github](https://github.com/karthiknadar1204)

# [LinkedIn](https://www.linkedin.com/in/karthik-nadar-b2155a25b/)