# dirtypipe

Thank you Max Kellerman!  https://dirtypipe.cm4all.com/  

Make sure you have a buggy kernel.  They patched the mainlines 5 days ago, so you have to dig.  

My Ubuntu 20.04 did not, so I had to get the Host machine on which I am running Docker to have the buggy kernel.  
It originall had 5.04 and the POC did not work. So here is how we upgraded the kernel to 5.10.0 which should have the bug:  

```py
mkdir kernelfun  
cd kernelfun  
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.10/amd64/linux-headers-5.10.0-051000_5.10.0-051000.202012132330_all.deb  
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.10/amd64/linux-headers-5.10.0-051000-generic_5.10.0-051000.202012132330_amd64.deb  
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.10/amd64/linux-image-unsigned-5.10.0-051000-generic_5.10.0-051000.202012132330_amd64.deb  
wget -c https://kernel.ubuntu.com/~kernel-ppa/mainline/v5.10/amd64/linux-modules-5.10.0-051000-generic_5.10.0-051000.202012132330_amd64.deb  
sudo dpkg -i *.deb  
reboot  
```

Profit!  

Note I used a version from Docker Hub that took me almost a half hour to find which had a buggy kernel:  

```py
docker run -it ubuntu:impish-20220105 /bin/bash  
apt-get update && apt install vim -y  
apt install dnsutils -y
apt install build-essential -y
```

![DirtyPipe](https://user-images.githubusercontent.com/4404271/157334089-2122780b-b5c4-4f98-bd5c-bd93b7ce5155.gif)
