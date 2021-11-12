# rest-server-mycloud
Cross compile restic's rest-server for the original wd mycloud on a Fedora 35 install. You can skip the [toolbox](https://github.com/containers/toolbox) setup part, if you want to install golang onto your machine

# Prerequisites:
- Original WD Mycloud. Mine is running firmware version ``v04.05.00-342``. You can try this guide with any other version, but ymmv.
- ssh access enabled through web ui to run the rest server

## Install toolbox and create build container. This can be skipped
````
sudo dnf install toolbox
````
````
toolbox create golang-f35
````
````
toolbox enter golang-f35
````

## Install golang
````
sudo dnf install golang
````

## Clone rest-server and cross compile for WD Mycloud
````
git clone https://github.com/restic/rest-server.git
````
````
cd rest-server/
````
````
GOOS=linux GOARCH=arm CGO_ENABLED=0 go build -o rest-server ./cmd/rest-server
````

You can check the platform of the resulting binary
````
file rest-server
````
which should output something like that
````
rest-server: ELF 32-bit LSB executable, ARM, EABI5 version 1 (SYSV), statically linked, Go BuildID=XYZ, not stripped
````

After the build you can copy the binary ``rest-server`` to you mycloud by any means (e.g. public share)
