# A short workshop on Docker!

When: May 26, 2017, from noon - 1:30pm

Where: Data Science Initiative, UC Davis

Who: [C. Titus Brown](http://ivory.idyll.org/blog/), titus@idyll.org

## Before the workshop

### INSTALL IN ADVANCE

If your laptop has > 20 GB free disk space and > than 4 GB of RAM,
please try to install Docker!

For Mac OS X: https://docs.docker.com/docker-for-mac/install/ -
install the Stable Channel one.

For Windows 10: https://docs.docker.com/docker-for-windows/install/ -
Stable Channel.

If you can't install it, please drop Titus Brown an e-mail with
"Docker tutorial - cannot install" in the subject line and he will set
you up with a remote machine for the workshop.

### DOWNLOAD IN ADVANCE

If you've gotten Docker installed and running, please try to execute the following three commands:

```
docker pull ubuntu:14.04
docker pull rocker/tidyverse
docker pull jupyter/notebook
```

This is network intensive so it'd be nice if you could do it in advance!

----

Titus will also spin up a few instances on Jetstream (see
[boot instructions(https://2017-ucsc-metagenomics.readthedocs.io/en/latest/jetstream/boot.html)) for people to use.  The only trick here is that you need to do give your account permission to run docker, e.g.

```
sudo usermod -aG docker titus
```

## Introducing Docker

Let's start with a demo --

`docker run -it -p 9001:8787 rocker/tidyverse`

This runs RStudio Web on local port 9001.  To connect to it on your
laptop go to `http://localhost:9001`; if you're running in a remote
machine (e.g. Jetstream), connect to `http://149.165.XXX.YYY:9001`.

The username is `rstudio` and the password is `rstudio`.

Try this bit of R code:

```
# Define 2 vectors
cars <- c(1, 3, 6, 4, 9)
trucks <- c(2, 5, 4, 5, 12)

# Graph cars using a y axis that ranges from 0 to 12
plot(cars, type="o", col="blue", ylim=c(0,12))

# Graph trucks with red dashed line and square points
lines(trucks, type="o", pch=22, lty=2, col="red")

# Create a title with a red, bold/italic font
title(main="Autos", col.main="red", font.main=4)
```

A few points to make --

* you had to install the image (that's what the `docker pull` command above
  did for you) but you didn't have to actually install any software other
  than docker -- RStudio is on the image already!
  
* This is running in a completely isolated sandbox, with only network access.
  Any files or data you want have to be added or downloaded explicitly
  (We'll show you how to fix that later.)
  
* Some details (the username and the password; the port 8787 in the run command) are chosen by the people who create the image.  Other details (the port 9001 that we're using to connect to it) are specified by us as our way of connecting into the image. You can change the latter easily, but not the former!

### Docker and isolation

The above is Docker running a container locally, which is a special case that
gives you local access to disk and network.  It's super convenient for
running things in an isolated sandbox but with limited access to your local files.

![Containers running on your own computer](images/isolation-special.png)

More generally, you can have multiple containers running on multiple
machines, but then you don't generally have the nice disk sharing.
On the flip side, you can use more powerful machines than your laptop,
and you still get the benefits of isolation and pre-installed software.

![Containers for isolation](images/isolation.png)

![Dockerfiles / image recipes](images/dockerfiles.png)

![Sharing docker images](images/hub.png)
