Given that we want to install go version 1.8.3 in an Ubuntu environment

And to import a package from the github.com/l3x repo

    GOVERSION: 1.8.3
    GITREPO: github.com/l3x

We run the following commands:

    sudo apt-get update
    sudo apt-get -y upgrade
    sudo curl -O https://storage.googleapis.com/golang/go1.8.3.linux-amd64.tar.gz
    sudo tar -xvf go1.8.3.linux-amd64.tar.gz
    sudo mv go /usr/local
    
    sudo nano ~/.profile
    export GOROOT=/usr/local/go
    export GOPATH=$HOME/go
    export GOPATH_ORIG=$GOPATH
    export GOBIN=$GOPATH/bin
    export PATH=$PATH:$GOROOT/bin:$GOBIN
    source ~/.profile
    
    mkdir $HOME/go
    cd $HOME/go
    
    PROJECT=hey-project
    mkdir $HOME/go/$PROJECT
    cd $HOME/go/$PROJECT
    export GOPATH=$GOPATH_ORIG:$HOME/go/$PROJECT
    go get $GITREPO/hey/...

We edit the following file:

    nano main.go
    --------------------------
    package main
    
    import . "github.com/l3x/hey"
    
    func main() {
        Hey()
    }
    --------------------------

We run the following to install the app:

    $ go install
    
And we run the binary to see its output:    

    $ hey-project
    Hey!
    
To see the directory structure and files:

    $ tree ~/go
    /home/lex/go
    ├── bin
    │   └── hey-project
    ├── hey-project
    │   └── main.go
    ├── pkg
    │   └── linux_amd64
    │       └── github.com
    │           └── l3x
    │               └── hey.a
    └── src
        └── github.com
            └── l3x
                └── hey
                    ├── hey.go
                    └── README.md

To see a vendoring example, we go to https://github.com/l3x/hi 