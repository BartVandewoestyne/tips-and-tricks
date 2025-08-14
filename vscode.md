# VS Code

## Documentation

* [Visual Studio Code documentation](https://code.visualstudio.com/docs)
* [Visual Studio Code documentation - EDIT CODE - Basic Editing - Search across files](https://code.visualstudio.com/docs/editing/codebasics#_search-across-files)

## Configuration

* User settings are stored in `~/.config/Code/User/settings.json`.
* Workspace settings are stored in the `~/.vscode/settings.json` file in the workspace directory.
* Extensions are installed in `~/.vscode/extensions/`.

## Folding

* Toggle Fold (`Ctrl+K Ctrl+L`) folds or unfolds the region at the cursor.
* Fold All (`Ctrl+K Ctrl+0`) folds all regions in the editor.
* Unfold All (`Ctrl+K Ctrl+J`) unfolds all regions in the editor

See also [Visudo Studio Code documentation - EDIT CODE - Basic Editing - Folding](https://code.visualstudio.com/docs/editing/codebasics#_folding)

## Cache data

Cache data is located under `~/.cache/vscode-cpptools/` and can take up quite some space (I've once had 63 GB of cache data in it...)

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
  Note that this extension does not provide svn blame functionality.  On its [features page](https://marketplace.visualstudio.com/items?itemName=johnstoncode.svn-scm) it recommends SVN Blamer.
* [SVN Blamer](https://marketplace.visualstudio.com/items?itemName=beaugust.blamer-vs)

### Git

* [GitLens](https://marketplace.visualstudio.com/items?itemName=eamodio.gitlens)
* [Git Blame](https://marketplace.visualstudio.com/items?itemName=waderyan.gitblame)

### Remote Development

The [Remote Development](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.vscode-remote-extensionpack) extension pack installs these 4 extensions:

* [WSL](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-wsl)
* [Dev Containers](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)
* [Remote - SSH](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-ssh)
* [Remote - Tunnels](https://marketplace.visualstudio.com/items?itemName=ms-vscode.remote-server)

### CMake

* [CMake Tools](https://marketplace.visualstudio.com/items?itemName=ms-vscode.cmake-tools)
  * [C++ in VS Code: Building your Code with CMake](https://www.youtube.com/watch?v=_BWU5mWqVA4)

* [CMake-Lint](https://marketplace.visualstudio.com/items?itemName=brobeson.vscode-cmake-lint)

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

* <https://clangd.llvm.org/>
* <https://github.com/clangd/clangd>
* <https://github.com/clangd/vscode-clangd>

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
  (See also [Developing inside a Container](https://code.visualstudio.com/docs/devcontainers/containers))

### Ruby

* [Ruby LSP](https://marketplace.visualstudio.com/items?itemName=Shopify.ruby-lsp)
* [Ruby Solargraph](https://marketplace.visualstudio.com/items?itemName=castwide.solargraph)  
  (note that on the eng4 machine I had to install it using `sudo gem install solargraph` because the installation from VSCode failed...)
* [Ruby Test Explorer](https://marketplace.visualstudio.com/items?itemName=connorshea.vscode-ruby-test-adapter)  

The [Ruby](https://marketplace.visualstudio.com/items?itemName=rebornix.Ruby) and [VSCode Ruby](https://marketplace.visualstudio.com/items?itemName=wingrunr21.vscode-ruby) extensions are deprecated and one should use the [Ruby LSP](https://marketplace.visualstudio.com/items?itemName=Shopify.ruby-lsp) extension instead.

Note: Apparently, for the language server, I also had to do `sudo gem install rek` once... don't know exactly in what context anymore.

### Markdown

* [markdownlint](https://marketplace.visualstudio.com/items?itemName=DavidAnson.vscode-markdownlint)

## Issues I have or had

* On Ubuntu 20.04.5 LTS the 'Go Back' functionality is not working when I press "Ctrl+Shift+-".  
  *Solution: don't use the minus character from the numeric keypad, use the other one.*

* Ruby shared examples not working.  
  See <https://stackoverflow.com/questions/75756169/how-to-navigate-to-ruby-rspec-shared-examples-in-vscode/>

* If you get "The "foo" repository has 82 submodules which won't be opened automatically.  You can still open each one individually by opening a file within." from Source: Git, then you can go to your settings for the Git extension and change the "Detect Submodules Limit" from 10 to something higher.  You can also disable "Detect Submodules" if you want.
