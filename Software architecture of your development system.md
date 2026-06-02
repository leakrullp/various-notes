
Our root repository contains the folders frontend and backend. When you run the command XXX, there is a parallel command being executed that runs the client-side application on the best available port and the server runs on port 3000 in the localhost. So client and server are running in parallel on different ports and are talking to each other.

In frontend, we have our application which is a single-page application that springs from a root div being controlled by our `main.tsx` script.

Inside of backend, we have our data stored in a single json file as well as our server, our routes and our controllers, which are simply functions that service the router functions to make them more streamlined.




~~Explaining the overall logical/physical architecture of your software system (components you developed and used third-party components and their roles)~~

~~Software styles/patterns and solutions used in your developed components in both client-side React application and RESTful API application, including your own, bult-in React or Express standard components, third-party frameworks (e.g. react-bootstrap), React patterns and techniques used (e.g. prop drilling, lifted state, Context API), your data storage solution, etc.~~