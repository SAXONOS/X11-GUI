# X11-GUI
Very simple X11 GUI to learn C

sudo apt-get update
sudo apt-get install libx11-dev

To ensure that package is correctly installed:  dpkg -l | grep libx11-dev


#include <X11/Xlib.h>  X11 library header file which provides necessary functions and types for interacting with the X server.

#include <X11/Xatom.h  X11 library header file is necessary for handling window manager protocols, specifically for defining atoms like WM_DELETE_WINDOW, which is used to properly handle the window close event. Without this header, you won't be able to define or use atoms like WM_DELETE_WINDOW.


To handle Window Close Event:

wmDeleteMessage = XInternAtom(display, "WM_DELETE_WINDOW", False);
XSetWMProtocols(display, window, &wmDeleteMessage, 1);

This code sets up a mechanism to handle the window close event. WM_DELETE_WINDOW is an atom that represents the window manager's close event. By setting this protocol, the program can catch the event when the user attempts to close the window.


Check for ClientMessage Events:

else if (event.type == ClientMessage) {
    if (event.xclient.data.l[0] == wmDeleteMessage) {
        break;
    }
}

This checks for ClientMessage events, and if the message corresponds to WM_DELETE_WINDOW, it breaks out of the event loop, allowing the program to exit cleanly.


To cleanup resources, below code ensures that the graphics context, window and display are properly cleaned up when the program exits.

XFreeGC(display, gc);
XDestroyWindow(display, window);
XCloseDisplay(display);


Compile code with following command:  gcc X11gui.c -o X11gui -lX11

and run executable:  ./X11gui


