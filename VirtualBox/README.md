# VirtualBox Experiments

## Experiment 1: Installation and Setup of Ubuntu in VirtualBox

### Steps
1. Download and install Oracle VirtualBox on the computer.
2. Download the Ubuntu ISO file.
3. Open VirtualBox and click New.
4. Enter VM name, set type to Linux, and select the downloaded ISO file.
5. Set RAM to 4 GB and select 2 CPU cores.
6. Create a virtual hard disk with 25 GB storage.
7. Click Start to power on the machine.
8. Follow on-screen setup steps to complete the installation.
9. Restart the VM and log in.
10. Install Guest Additions for full screen support.

---

## Experiment 2: Network Setup and Running C Program in Ubuntu

### Steps
1. Go to VM Settings -> Network and make sure Network Adapter 1 is enabled.
2. Start the VM and open terminal (Ctrl + Alt + T).
3. Update package list:
sudo apt update
4. Install GCC compiler:
sudo apt install build-essential
5. Check compiler version:
gcc --version
6. Create and open file:
nano hello.c
7. Write the code:
#include <stdio.h>
int main() {
    printf("Hello");
    return 0;
}
8. Save and exit (Ctrl + O, Enter, Ctrl + X).
9. Compile the program:
gcc hello.c -o hello
10. Run the program:
./hello