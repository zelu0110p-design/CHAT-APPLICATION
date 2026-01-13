# CHAT-APPLICATION

#COMPANY: CODTECH IT SOLUTIONS PRIVATE LIMITED

#NAME: PATEL ZEEL MAHESHBHAI

#INTERN ID: CTIS2480

#DOMAIN: FULL STACK WEB DEVELOPMENT

#DURATION: 4 WEEKS

#MENTOR: NEELA SANTHOSH KUMAR


Chat application 


1 Overview

The `index.js` file is the main server-side entry point of the Chat Application. It sets up an Express web server and integrates Socket.IO to enable real-time, bidirectional communication between clients. This file is responsible for handling user connections, room management, message broadcasting, and maintaining application state for connected users.


2 Server Setup

The file begins by importing required modules such as `express`, `socket.io`, and Node.js utilities for path handling. Since the project uses ES modules, `fileURLToPath` is used to correctly derive the current directory path.

An Express application is created and configured to serve static files from the `public` directory. This enables the browser to load client-side assets, including HTML, CSS, and JavaScript. The server listens on a configurable port (defaulting to `3500`) and logs a confirmation message once it starts successfully.


3 Socket.IO Integration

A Socket.IO server is attached to the Express HTTP server to handle real-time communication. During development, CORS is configured to allow connections from local frontend servers, while production mode restricts external origins for security.

When a client connects, the server logs the socket ID and immediately sends a welcome message from a virtual `Admin` user. This establishes an initial connection acknowledgment.


4 Application State Management

User state is maintained using a simple in-memory object called `UsersState`. This object stores an array of active users, each represented by a unique socket ID, username, and room name. Helper functions are provided to:

  * Add or update users
  * Remove users on disconnect
  * Retrieve a single user
  * Retrieve users in a specific room
  * List all active rooms

This centralized state allows the server to manage rooms and participants efficiently.


5 Room Handling

When a user emits the `enterRoom` event, the server:

  1. Removes the user from any previous room.
  2. Updates the user state with the new room.
  3. Joins the socket to the new room.
  4. Sends confirmation messages to the user and other room members.
  5. Updates the user list for the room.
  6. Broadcasts the list of active rooms to all connected clients.

This ensures seamless room switching and accurate real-time updates.


6 Messaging and Activity

The server listens for `message` events and broadcasts messages only to users within the same room. Each message is formatted using the `buildMsg` function, which attaches a timestamp for display consistency.

Typing indicators are handled through the `activity` event. When a user is typing, their name is broadcast to other users in the same room without storing any persistent state.


7 Disconnection Handling

When a socket disconnects, the server removes the user from the application state, notifies the remaining users in the room, updates user lists, and refreshes the active room list. This prevents stale data and ensures accurate room membership.


8 Conclusion

The `index.js` file acts as the real-time backbone of the Chat Application. By combining Express for server hosting and Socket.IO for live communication, it enables dynamic chat rooms, instant messaging, and real-time user awareness with a clean and maintainable architecture.


9 Output
