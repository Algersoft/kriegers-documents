# **Compiling on Linux (Ubuntu)**

Compiling on Linux will generate the binaries for Windows, macOS and Linux.

The miner GUI is built using [Electron](https://electronjs.org) and
[Go](https://golang.org) using the
[Astilectron app framework](https://github.com/asticode/astilectron).

## **Install dependencies**

```shell
sudo apt-get update
sudo apt-get install gcc make python libmicrohttpd10 libnss3 -y
```

- gcc and make are required for go packages  
- python is required for GUI-miner  
- libmicrohttpd is required for xmrig  
- libnss3 is required for electron  

## **Install Go**

1. [https://golang.org/dl/](https://golang.org/dl/)

2. or follow the next lines

download and unpack golang binaries

```shell
cd ~
wget https://dl.google.com/go/go1.11.2.linux-amd64.tar.gz
sudo tar -C /usr/local -xzf go1.11.2.linux-amd64.tar.gz
```

add Go to current $PATH, by editing the current user's `.bashrc`

```shell
nano ~/.bashrc 
```

add the following

```shell
# golang
export PATH=$PATH:/usr/local/go/bin
export PATH=$PATH:~/go/bin
```

run the .bashrc file (otherwise you need to logout and login again for it to get triggered)

```shell
source ~/.bashrc
```

now you could check the go installation by running

```shell
go version
```

## **Clone the app**

```shell
cd ~
git clone https://github.com/furiousteam/KREGR-GUI-Miner.git
```

## **Install required Go packages**

```shell
go get -u github.com/asticode/go-astilectron
go get -u github.com/asticode/go-astilectron-bundler/...
go get -u github.com/asticode/go-astichartjs
go get -u github.com/asticode/go-astilectron-bootstrap
go get -u github.com/google/uuid
go get -u github.com/mitchellh/go-ps
go get -u github.com/furiousteam/KREGR-GUI-Miner/src/gui
go get -u github.com/konsorten/go-windows-terminal-sequences
go get -u github.com/mattn/go-colorable
```

## **Update electron version**

edit `~/go/src/github.com/asticode/go-astilectron/astilectron.go` file

```shell
nano ~/go/src/github.com/asticode/go-astilectron/astilectron.go
```

and change `VersionElectron         = "1.8.1"` to `VersionElectron         = "3.0.8"`

then, recompile go-astilectron-bundler

```shell
cd ~/go/src/github.com/asticode/go-astilectron-bundler
make
```

## **Compile the miner**

```shell
cd ~/KREGR-GUI-Miner
make
```

If all goes well, the binaries for Windows, macOS and Linux will be available in the `bin` folder.

## **Attach the miner**

before you start the GUI-miner, make sure you have copied the binaries of [xmrig](https://github.com/xmrig/xmrig) or [xmr-stak](https://github.com/Algersoft/xmr-stak) into the `miner` subfolder right next to the main GUI-miner executable