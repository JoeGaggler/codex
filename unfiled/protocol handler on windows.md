a protocol handler is the standard mechanism for a web browser to activate an application.

typical use case: federated login using a web browser

on Windows a new process (previously registered with the OS) is launched with the URL as an argument.

the goal is to notify the original instance of the app, and so the second instance must then use a different mechanism, such as a [[named pipe]].

the second instance then exits, and to the user it looks like the original instance was directly invoked.
