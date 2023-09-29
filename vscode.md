# Git Support

Visual Studio Code has Git support built in.  You will need to have Git version 2.0.0 (or newer) installed.
See
* https://git-scm.com/book/en/v2/Appendix-A%3A-Git-in-Other-Environments-Git-in-Visual-Studio-Code
* https://code.visualstudio.com/docs/sourcecontrol/overview

# Interesting extensions

Live Share:

* [Live Share](https://code.visualstudio.com/learn/collaboration/live-share)

SVN:

* [SVN](https://marketplace.visualstudio.com/items?itemName=johnstoncode.svn-scm)

Git:

* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)

CMake:

* [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)

C++:

* [C/C++](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools)
* [C/C++ Extension Pack](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cpptools-extension-pack)<br>
This one installs the C/C++, C/C++ Themes, CMake, CMake Tools extensions.
* [C++ TestMate](https://marketplace.visualstudio.com/items?itemName=matepek.vscode-catch2-test-adapter)

Code coverage:

* [Gcov Viewer](https://marketplace.visualstudio.com/items?itemName=JacquesLucke.gcov-viewer)

Static code analysis:

* [C/C++ Advanced Lint](https://marketplace.visualstudio.com/items?itemName=jbenden.c-cpp-flylint)
* [Cppcheck Plug-in](https://marketplace.visualstudio.com/items?itemName=NathanJ.cppcheck-plugin)
* [cppcheckcmd](https://marketplace.visualstudio.com/items?itemName=ronzhong.cppcheckcmd)
* [cpp-check-lint](https://marketplace.visualstudio.com/items?itemName=QiuMingGe.cpp-check-lint)
* [cpp-checker](https://marketplace.visualstudio.com/items?itemName=eBikeLabs.cpp-checker)
* [Cpp Static Checks](https://marketplace.visualstudio.com/items?itemName=NathanJ.cpp-tools-plugin)

Ruby:

* [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby)
* [VSCode Ruby](https://marketplace.visualstudio.com/items?itemName=wingrunr21.vscode-ruby)
* [Ruby Solargraph](https://marketplace.visualstudio.com/items?itemName=castwide.solargraph)<br>
  (note that on the eng4 machine I had to install it using `sudo gem install solargraph` because the installation from VSCode failed...)
* [Ruby Test Explorer](https://marketplace.visualstudio.com/items?itemName=connorshea.vscode-ruby-test-adapter)<br>
  (TODO: test this one out!)

# Issues I have or had

* On Ubuntu 20.04.5 LTS the 'Go Back' functionality is not working when I press "Ctrl+Shift+-".<br>
  *Solution: don't use the minus character from the numeric keypad, use the other one.*

* Ruby shared examples not working.  
  See https://stackoverflow.com/questions/75756169/how-to-navigate-to-ruby-rspec-shared-examples-in-vscode/