
**This file Summarizes the development of a simple Go package from Go website : **

# Workspaces


Go code must be store inside *a workspace*.

**A workspace** is a directory ranking structure with three directories at the root:


**src** contains Go source files organized into packages (one package per directory),

**pkg** contains package objects, and

**bin** contains executable commands.


The *go tool* builds source packages and installs the resulting binaries to the pkg and bin directories.

The src subdirectory typically contains multiple version control repositories (such as for Git or Mercurial) that track the

development of one or more source packages.

To give you an idea of how a workspace looks in practice, here's an example:

    bin/
        hello                          # command executable
        outyet                         # command executable
    pkg/
        linux_amd64/
           github.com/golang/example/
               stringutil.a           # package object
    src/
    github.com/golang/example/
        .git/                      # Git repository metadata
    	hello/
    	    hello.go               # command source
     	outyet/
    	    main.go                # command source
    	    main_test.go           # test source
    	stringutil/
    	    reverse.go             # package source
      	    reverse_test.go        # test source
	    
	    
- This workspace contains **one repository** (example) 

- comprising **two commands** (hello and outyet) and 

- **one library** (stringutil).

usually a workspace has many source repositories containing many packages and commands.

Most Go programmers keep all their Go source code and dependencies in a single workspace.



# The GOPATH environment variable


Here you can state the location of your workspace. 

First, create a workspace directory then set GOPATH accordingly. 

    $ mkdir $HOME/work
    $ export GOPATH=$HOME/work
    
    For convenience, add the workspace's bin subdirectory to your PATH:

    $ export PATH=$PATH:$GOPATH/bin


# Package paths


- If you store your code in a source repository somewhere, then your your base path have to be the root of that source repository.

    For instance, if you have a GitHub account at github.com/user, that should be your base path.

- you can choose any random path name, however, it has to be unique to the standard library and greater Go ecosystem.

- you don't need to publish your code to a remote repository before you can build it. 
but It's better that you keep your code always  arranged in a systematic way , so you ready to publish it any time.

We'll use github.com/user as our base path. Create a directory inside your workspace in which to keep source code:

    $ mkdir -p $GOPATH/src/github.com/user

[Previous] (https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/InstallingGO.md ) - 
[Home] (https://github.com/Afnan-Aldhahri/GO/blob/master/README.md ) -
[ Next](https://github.com/Afnan-Aldhahri/GO/blob/master/Resources/Go%20the%20Basics.md)
