# Riscv-VSD mini reaserch intership

## This repositiry is intended to document the learning outcomes and experience of a 4-week workshop on RISC-V using Open source tools like yosys and Skywater 130nm PDK.

### TASK 0

<details>
 <summary> Summary </summary>
	
Installed all required tools.
</details>	
	<details>
    <summary> Riscv GNU Toolchain</summary>

  ```bash 
    git clone https://github.com/riscv/riscv-gnu-toolchain
    sudo apt-get install autoconf automake autotools-dev curl python3 python3-pip libmpc-dev libmpfr-dev libgmp-dev gawk build-essential bison flex texinfo gperf libtool   
    patchutils bc zlib1g-dev libexpat-dev ninja-build git cmake libglib2.0-dev
    ./configure --prefix=/opt/riscv
    make
  ```
    
 ![screen 1](https://github.com/Narendran040/RISCV/assets/157210399/db9eaf8a-81f8-4223-ab89-273b0b598f02)

  ![Screenshot 2024-02-21 181550](https://github.com/Narendran040/RISCV/assets/157210399/8d5b6f8a-650a-41aa-b3e3-696b1f2068f0)
  </details>
 <details>
 <summary> Yosys </summary>
   
```bash
git clone https://github.com/YosysHQ/yosys.git
cd yosys 
sudo apt install make 
sudo apt-get install build-essential clang bison flex \
    libreadline-dev gawk tcl-dev libffi-dev git \
    graphviz xdot pkg-config python3 libboost-system-dev \
    libboost-python-dev libboost-filesystem-dev zlib1g-dev
make config-gcc
make 
sudo make install
```
![Screenshot 2024-02-21 182022](https://github.com/Narendran040/RISCV/assets/157210399/ab73fc91-e123-47ea-baf3-5705efcfed98)


</details>
<details>
<summary> Iverilog </summary>
  
  ```bash
sudo apt-get install iverilog
 ```
![Screenshot 2024-02-21 182736](https://github.com/Narendran040/RISCV/assets/157210399/d147a3f7-43a1-4832-9e76-e045e4d289ef)

</details>
<details>
 <summary> gtkwave </summary>
  
  ```bash
sudo apt-get install gtkwave
 ```
![Screenshot 2024-02-21 183202](https://github.com/Narendran040/RISCV/assets/157210399/8b052bb8-a3e5-4a2a-bd7a-be6c6cde457e)
</details>
<details>
 <summary> OpenSTA </summary>

 ```bash
git clone https://github.com/The-OpenROAD-Project/OpenSTA.git
cd OpenSTA
mkdir build
cd build
cmake ..
make
```
![Screenshot 2024-02-21 185458](https://github.com/Narendran040/RISCV/assets/157210399/067a5790-087d-4a22-8e1f-ade07bca4b74)
</details>
<details>
  <summary> Ngspice </summary>

 ```bash
tar -zxvf ngspice-37.tar.gz
cd ngspice-37
mkdir release
cd release
../configure  --with-x --with-readline=yes --disable-debug
make
sudo make install
 ```

</details>
<details>
<summary> Magic </summary>
  
  ```bash
sudo apt-get install m4
sudo apt-get install tcsh
sudo apt-get install csh
sudo apt-get install libx11-dev
sudo apt-get install tcl-dev tk-dev
sudo apt-get install libcairo2-dev
sudo apt-get install mesa-common-dev libglu1-mesa-dev
sudo apt-get install libncurses-dev
 ```

</details>
<details>
<summary> OpenLane </summary>
  
```bash
sudo apt-get update
sudo apt-get upgrade
sudo apt install -y build-essential python3 python3-venv python3-pip make git
sudo apt install apt-transport-https ca-certificates curl software-properties-common
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=amd64 signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
sudo apt update
sudo apt install docker-ce docker-ce-cli containerd.io
sudo docker run hello-world
sudo groupadd docker
sudo usermod -aG docker $USER
sudo reboot
```

</details>
<details>
  <summary> PDKs </summary>

```bash
cd $HOME
git clone https://github.com/The-OpenROAD-Project/OpenLane
cd OpenLane
make
make test
```

</details>

### TASK 1
	
 <details>
 <summary> Instructions </summary>
 Instructions: Instructions are the basic operations that a processor can perform. These instructions can include arithmetic and logic operations, data movement operations (such as load and store), control transfer instructions (like branches and jumps), and special-purpose instructions for system control and communication.
<details>
 <summary> Types of Instructions </summary>
 
