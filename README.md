## Welcome to the GN parser and code model/browser

This is a parser, code model and browser for the GN meta-build system written in C++ and Qt. See https://gn.googlesource.com/gn for more information about GN. The syntax was retrieved using the command `gn help grammar` and modified for Coco/R compatibility using https://github.com/rochus-keller/EbnfStudio. 

The goal of this project is to build tools to better understand the GN meta-build system used by the Google Dart SDK. My real goal is to understand the Dart Runtime and to be able to integrate Dart as an embedded language into a system I am currently planning. Dart, like the Chromium and V8 projects, uses the GN meta-build system. This build system is very powerful, but also very complex. GN has useful documentation and commands for analyzing a project. But with a build system as big as the one of the Dart SDK, I still lose sight when only using command line tools (there were moments when I began to wonder if "GN" was meant as an abbreviation for "go nuts"). That was the primary reason why I implemented a parser/code model integrated with a navigable GUI based code browser myself. I hope it will be useful for others as well.

### Parser and code model features

- Implements the full GN syntax including the string sub-language
- LL(1) version of the grammar with a couple of LL(2) exceptions
- Syntax and some (static) semantics validation, error reporting
- Parses and analyzes all .gn and .gni files of the source tree regardless of actual imports or refernces
- Static code model with cross-referencing based on direct ident equality without actually running the statements (which seems to work surprisingly well)
- Model keeps track of references which cannot be resolved statically

### Code browser features

- Cross-platform, lean, fast
- Syntax highlighting
- Code navigation; jump to definitions, follow references by clicking on idents or strings
- Crossref for variable, definition and import file use, navigable by clicking on list items
- Browsing history, forward and backward navigation
- Fullscreen mode, movable and sizable docking windows


![GnViewer Screenshot](http://software.rochus-keller.info/GnViewer_Screenshot_1.png)


### Binary version

Here is a binary version of GnViewer for Linux x86: http://software.rochus-keller.info/GnViewer_linux_x86.tar.gz
Just download, unpack and run it; no installer is needed. The Qt core libraries have to be separately installed. The binary was built using Qt 5.4.

### Build Steps

Follow these steps if you want to build GnViewer yourself:

1. Make sure a Qt 5.x (libraries and headers) version compatible with your C++ compiler is installed on your system.
1. Download the source code from https://github.com/rochus-keller/GnTools/archive/master.zip and unpack it.
1. Goto the unpacked directory and execute `QTDIR/bin/qmake GnViewer.pro` (see the Qt documentation concerning QTDIR).
1. Run make; after a couple of seconds you will find the executable in the build directory.

Alternatively you can open GnViewer.pro using QtCreator and build it there.

The library makes use of a parser generated by Coco/R based on input from EbnfStudio. There is no other dependency than the Qt Core library.
The repository already contains the generated files. In order to regenerate GnParser.cpp/h you have to use this version of Coco/R: https://github.com/rochus-keller/Coco .

### To do's

- Add features as required
- Integration of the GN documentation for context sensitive help
- Dynamic evaluation and grey out not active code sections depending on specific argument settings
- Alternative translator to qmake which creates true .pro and .pri files
- Translator to cmake

## Support
If you need support or would like to post issues or feature requests please use the Github issue list at https://github.com/rochus-keller/GnTools/issues or send an email to the author.



