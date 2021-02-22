# RenodeSTM32

## Initial Considerations
When facing this practical challeng, I looked over the options and found one that I thought would be interesting and hopefully I could learn something. With that in mind, I chose the Renode simulation of a HelloWorld project.
I'd never used renode so my first step was to read the documentation it provided as well as search for any tutorial. Looking around I found an excellent article on [memfault.com](https://interrupt.memfault.com/blog/intro-to-renode).
This repo is a combination of the what I learned researching and the article.

## Environment
I chose to run Renode using Docker. To install docker in an Ubuntu distro, run ```sudo apt install docker.io```.
The code also needs to be cross-compied. To install the cross compiler, run ```sudo apt install gcc-arm-none-eabi```.

## The code
I copied thee example code provided by the memfault article to this repository. Clone this repository using ```git clone https://github.com/pksublime/RenodeSTM32.git```.

## Building
Simply run ```make``` to produce the ```renode-example.elf``` file.

## Simulating
### Docker Container
As I'm using docker, I needed to ensure my local directory so mounted the PWD at a known location inside the container.
To run the Renode environment, run ```sudo docker run -ti -e DISPLAY -v $XAUTHORITY:/home/developer/.Xauthority -v $PWD:/tmp/elf --net=host antmicro/renode```.
### Within Renode
Run the following commands to create the machine, load the binary, and observe the output.
```
mach create
machine LoadPlatformDescription @platforms/boards/stm32f4_discovery-kit.repl
sysbus LoadELF @/tmp/elf/renode-example.elf
machine LoadPlatformDescription @/tmp/elf/add-ccm.repl
showAnalyzer sysbus.uart2
start
```
