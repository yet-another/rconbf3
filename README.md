rconbf3
=======

This module provides an interface to interact with a Battlefield 3 game server
over the rcon protocol.


Functions:
    connect
        Attempts to connect to the server - returns a connection object or
        False

    close
        Closes the connection - returns True

    authenticate
        Attempts to authenticate with the server - returns True or False or
        None

    invoke
        Attempts to send a message to the server and receive its response -
        returns True or False or None

    start_update
        Creates a thread which updates the connection object with any received
        data - returns True


Example usage:
    Simple prompt
        connection = rconbf3.connect("IP", <port>)
        rconbf3.start_update(connection)

        result = rconbf3.authenticate(connection, "password")
        if result and result == ["OK"]:
            while 1:
                print rconbf3.invoke(connection,
                    raw_input("Send command to server: "))

    Event viewer
        connection = rconbf3.connect("IP", <port>, callback=lambda x: print x)
        rconbf3.start_update(connection)

        result = rconbf3.authenticate(connection, "password")
        if result and result == ["OK"]:
            if rconbf3.invoke(connection, "admin.eventsenabled true"):
                raw_input("Waiting for events")

