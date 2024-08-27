# VS Code

## Configuration

* User settings are stored in `~/.config/Code/User/settings.json`.
* Workspace settings are stored in the `~/.vscode/settings.json` file in the workspace directory.
* Extensions are installed in `~/.vscode/extensions/`.

## Git Support

Visual Studio Code has Git support built in.  You will need to have Git version 2.0.0 (or newer) installed.
See

* <https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Visual-Studio-Code>
* <https://code.visualstudio.com/docs/sourcecontrol/overview>

## Interesting extensions

### Live Share

* [Live Share](https://code.visualstudio.com/learn/collaboration/live-share)

### SVN

* [SVN](https://marketplace.visualstudio.com/items?itemName=johnstoncode.svn-scm)

### Git

* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)

### CMake

* [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
  * [C++ in VS Code: Building your Code with CMake](https://www.youtube.com/watch?v=_BWU5mWqVA4)

### Makefile Tools

* [Makefile Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.makefile-tools)

### C++

#### [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)

* Logging level can be changed via `C_Cpp.loggingLevel`, see also [C/C++ extension logging](https://code.visualstudio.com/docs/cpp/enable-logging-cpp)
* View output via *View/Output* and then select *C/C++* or *cpptools*.
* To reset your IntelliSense database, open the Command Palette (`Ctrl+Shift+P`) and choose **C/C++: Reset Intellisense Database** command.
* [Attaching debugger to cpptools or cpptools‐srv](https://github.com/microsoft/vscode-cpptools/wiki/Attaching-debugger-to-cpptools-or-cpptools%E2%80%90srv)

#### [C/C++ Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack)

This one installs the C/C++, C/C++ Themes, CMake, CMake Tools extensions.

#### [clangd](https://marketplace.visualstudio.com/items?itemName=llvm-vs-code-extensions.vscode-clangd)

#### [C++ TestMate](https://marketplace.visualstudio.com/items?itemName=matepek.vscode-catch2-test-adapter)

### Code coverage

* [Gcov Viewer](https://marketplace.visualstudio.com/items?itemName=JacquesLucke.gcov-viewer)

### Static code analysis

* [C/C++ Advanced Lint](https://marketplace.visualstudio.com/items?itemName=jbenden.c-cpp-flylint)
* [Cppcheck Plug-in](https://marketplace.visualstudio.com/items?itemName=NathanJ.cppcheck-plugin)
* [cppcheckcmd](https://marketplace.visualstudio.com/items?itemName=ronzhong.cppcheckcmd)
* [cpp-check-lint](https://marketplace.visualstudio.com/items?itemName=QiuMingGe.cpp-check-lint)
* [cpp-checker](https://marketplace.visualstudio.com/items?itemName=eBikeLabs.cpp-checker)
* [Cpp Static Checks](https://marketplace.visualstudio.com/items?itemName=NathanJ.cpp-tools-plugin)
* [SonarLint](https://marketplace.visualstudio.com/items?itemName=SonarSource.sonarlint-vscode)

### Docker

* [Docker](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-docker)
* [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

### Ruby

* [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)
* [VSCode Ruby](https://marketplace.visualstudio.com/items?itemName=wingrunr21.vscode-ruby)
* [Ruby Solargraph](https://marketplace.visualstudio.com/items?itemName=castwide.solargraph)  
  (note that on the eng4 machine I had to install it using `sudo gem install solargraph` because the installation from VSCode failed...)
* [Ruby Test Explorer](https://marketplace.visualstudio.com/items?itemName=connorshea.vscode-ruby-test-adapter)  
  (TODO: test this one out!)

### Markdown

* [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

## Issues I have or had

* On Ubuntu 20.04.5 LTS the 'Go Back' functionality is not working when I press "Ctrl+Shift+-".  
  *Solution: don't use the minus character from the numeric keypad, use the other one.*

* Ruby shared examples not working.  
  See <https://stackoverflow.com/questions/75756169/how-to-navigate-to-ruby-rspec-shared-examples-in-vscode/>
