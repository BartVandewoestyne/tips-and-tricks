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