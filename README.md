# How to use Valgrind on Catalina, Mojave, or High Sierra OS

Do you love developing C++ applications on your Mac but miss that good old Valgrind to check your program for memory leaks (since there hasn't been a released version of Valgrind supporing High Sierra OS & up)? 

Well look no further because, lo and behold, there is a way.

## Overview

By following these instructions, you'll execute the following.
1. Install Homebrew
2. Install & Launch Docker
3. Create an image of Ubuntu on Docker
4. Create & run a container of that image
5. Update Ubuntu & install relevant components (Git, Valgrind, G++, Nano)
6. Update Ubuntu image with the changes you've made to that container

If you already have Homebrew and Docker installed on your machine, skip to Step 3 of Installation.</br>

Does all this container and image-speak sound like nonsense to you? If so, please read the following. </br>

An image is like a GitHub repository that resides in Github.com. By creating an image, you're cloning a repository of that software on Docker's server (like forking a repository on GitHub).
A container is when you create an instance of that image and run it. Meaning, you've cloned the forked repository to your local machine so you can make changes to it. And like Git, what do you do after you're done working with your container? You update the image with the changes you've made to the container (like pushing the changes you've made to a git repository on your local machine to the repository that resides in Github.com). Therefore, an image is like a frozen instance of your container while a container is like running an editable instance of that image. All this is to say, update your image after working on a container so that you don't lose the changes you've made!

## Installation

1. Install Homebrew
    - open up your Terminal
    - Run the following command `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`
2. Install & Launch Docker
    - `brew cask install docker` to install
    - `open /Applications/Docker.app` to launch
3. Create an image of Ubuntu on Docker
    - `docker pull ubuntu`
    - `docker images` to see your Ubuntu's image id and copy it (henceforward addressed as `yourImageID`)
4. Create & run a container of that image
    - `docker run -it yourImageID`
5. Your containerized Ubuntu should've started. Update it & install relevant components (Git, Valgrind, g++, Nano)
    - `apt-get update`
    - `apt-get install git-core`
    - `apt-get install valgrind`
    - `apt-get install g++`
    - `apt-get install nano`
    - `exit`
6. Update Ubuntu image with the changes you've made to your Ubuntu container
    - `docker ps -a` to see your Ubuntu's container id and copy it (henceforward addressed as `yourContainerID`)
    - `docker commit yourContainerID ubuntu:latest` to update image
    - Now that you've updated the Ubuntu image with the latest changes you've made to your Ubuntu container, you can delete the container `docker rm containerID`

## Operation

Now that you have an updated image of Ubuntu where you can clone git repositories of your C++ applications and run them on Valgrind, the following instructions allow you to do just that.

1. Launch Docker (`open /Applications/Docker.app`)
2. Get `yourImageID` and run its container
    - `docker images`
    - `docker run -it yourImageID`
3. Create a folder in your Ubuntu and go to it
    - `mkdir yourFolderName`
    - `cd yourFolderName`
4. Open up a web browser, go to your GitHub account, copy the clone URL to your repository (henceforward addressed as `yourCloneURL`), and clone the repository to your Ubuntu.
    - `git clone yourCloneURL`
5. `cd` into the local instance of your repo. If you want to open up a file and make changes to it, all you have to do is `nano yourFileName.cpp`. If you've never used a command line text editor before, here's a useful guide for using Nano (https://www.hostinger.com/tutorials/how-to-install-and-use-nano-text-editor)
6. After you're done making changes, `g++ *.cpp` to compile
7. To run Valgrind, `valgrind ./a.out`
8. After you're done working on your C++ application and have pushed your latest changes to GitHub, `exit` to leave Ubuntu.
9. Get your container id, update your image, and delete the container
    - `docker ps -a`
    - `docker commit containerID ubuntu:latest`
    - `docker rm containerID`

## Pros & Cons

After having done or read all of this, you may have realized that there are some advantages and disadvantages to this approach. First, you can finally use Valgrind on your Mac! Well, kind of... You can finally run Valgrind on your Ubuntu which runs on Docker that runs on your Mac! Despite the fact that this approach involves downloading additional software, namely Docker and its Ubuntu container, this approach is alot faster and more space-efficient than deploying a full-on virtual machine to run your programs (https://www.youtube.com/watch?v=0qotVMX-J5s). Of course, this approach also means you'll be missing out on Ubuntu's graphical user interface, but `¯\_(ツ)_/¯`

If you have any thoughts on this apporach or how I can improve it, feel free to let me know! Feel free to add me on GitHub (follow4follow broski or brosephine`:)'), branch, fork, or clone this repo. 
