---
description: >-
  This page contains the methodology and the journey of selecting the
  Development Environment for The GCS.
---

# Development Enviornment

To start with the development of GCS I had to choose a language for making the GUI application, I has some points that needed to be satisfied:

* [ ] Should be able to communicate with USB Serial and Hardware Attached to Computer
* [ ] Should be Cross platform
* [ ] Should be Memory Safe
* [ ] Should Open Source and not depend on some propitiatory IDE for development even if it is open sources

## Choice of Languages

### C/C++

The first language that came to mind was C/C++, I have used it for development of CLI applications as well as for embedded applications. It provides low level hardware access for accessing USB devices, it is cross platform with enough effort. Memory Safety is a major concern when using C/C++. Libraries like QT can be used for ensuring memory safety and provide cross platform support. However QT requires to use there own QT Creator IDE and for the GUI elements it requires to use there own QML (QT Modelling Language). Technically QT can be used without QT creator but the third party support is not good enough. For these reasons I decided not to use C/C++, also it was the language I used for most of my projects so I decided to not go for it.

* [x] Low Level Access makes it easier to communicate with hardware of the computer
* [ ] Can be made Cross platform with enough effort, or using Libraries like QT
* [ ] Memory leaks in C/C++ are majorly caused by skill issues of the programmer, but they are always going to be there, unless you are may be Linus Torvalds
* [ ] GUI libraries like GTK are a great truly Open Source Choice but they are difficult to use
* [ ] I had made a lot of applications in C/C++ so I wanted to try different language (Bit of a personal goal)

### Python

Python is a great scripting language, it is used in lot of modern application, it is cross platform, and it has many GUI libraries like TKinter or PySide that provides QT Binding for python. It can also interact with hardware like Serial port and IP Protocols. The only down side of Python is its interpreted nature which causes it to hang specially when there is lot of data flowing in from the Serial port.

&#x20;

* [ ] Has some what low level access using libraries provided by python
* [x] It is Cross platform language
* [x] Memory leaks in python are pretty rare and it has a garbage collector
* [x] There are a GUI Libraries like TKinter
* [ ] Python is a slow language, even when using PyPy which is a JIT implementation of python it is still slow, and leads to too much data being piled up in the serial buffer.

### JavaScript

JavaScript is primarily a language for web development and does not supports hardware access in the browser, but things like node.js allow to use JavaScript to access hardware of the Computer, for running back end servers and communicating with the physical layer including USB, thanks to JS nerds who can not comprehend any other language. JS also has a lot of good looking GUI libraries like ChakraUI and MUI. These can be used together with Electron, which is a Framework that bundles a chromium based browser along with node.js for the back end, allowing me to create cross platform desktop application. So even with all the shitty abstraction of JS i am going to use it for creating this application.

* [x] JavaScript with Electron provides access to Serial Port and UDP, TCP connections
* [ ] JavaScript on its own does not create memory leaks, but if some of the library with bindings for C/C++ can cause memory leaks
* [x] Electron application uses Chromium for the GUI and node.js for the main process, so it makes it easy to build a cross platform application
* [x] There are tones of GUI libraries for JavaScript MUI, Chakra UI, Tailwind(CSS but the same thing).(Honestly feels like libraries being taped together)
* [x] Not the fastest language in the world and not the one with the brightest implementation but gets the work done, and I am giving it this point only because it has good GUI components

## Conclusion

So to conclude I am going to use React for the front end and bundle it with Electron to create a cross platform application.

### Why did I choose JavaScript, despite it being shitty?

Majorly because I am lazy and don't want to make my own GUI components, and I hate life.





