# INTRO #

The ADB port forwarder can be used to connect your local adb client with a remote adb server.

# USAGE #

  * Download the adbportforward.jar from the Downloads section
  * Start the port forwarder on the machine on which the device is connected with the command:
> `java -jar adbportforward.jar server adblocation=[adb location]`
  * Start the port forwader on the remote machine with the command:
> `java -jar adbportforward.jar client adblocation=[adb location] remotehost=[ip of machine to which android device is connected]`

replace `[adb location]` with the location where the android sdk is located on your system.

You can now use adb on the command line and the android plugin in eclipse like  the device is locally connected.

# HOW IT WORKS #

For information about the Android Debug Bridge read: http://developer.android.com/tools/help/adb.html

The ADB server create a server socket at port 5037.  But it only seems to do this on the loopback interface.  When the adb port forwarder is started in server mode, it creates a new server sockets bound to all network interfaces at port 6037, and routes all trafic to the local adb server at port 5037.  When the adb port forwarder is running in server mode it also ensures that the adb server keeps running by executing an adb start-server command every minute.

The adb port forwarder which is running in client mode will connect to the adb port forwarder running in server mode and will route all incoming trafic on port 5037 to the remote host at port 6037.
When the adb port forwarder is started in client mode it will first kill the local adb server if it's running.