<p><a href="https://caffe.berkeleyvision.org" target="_blank"><img src="caffe.png" align="left" width="170" height="90" /></a></p>
</br>
</br>
</br>

# Caffe | Deep Learning Framework - How to install Caffe on Ubuntu 18.04 LTS with CUDA 10.1.
> This repository is just a guide to install the Framework Caffe for Deep Learning in a straight forward way.

### *caffe_requirements.txt*: File that contains some libraries needed to use Caffe and they must be installed. To execute the installation, run the following commands depending on the version of Python that you are using:
```
Python 2: pip install -r caffe_requirements.txt
Python 3: pip3 install -r caffe_requirements.txt
```
### Instructions to Caffe Compilation *from source*:

1. **Adjustments on Linux GPU driver** 
   - **On Software & Updates**
     - On the ***Ubuntu Software*** tab mark the check box **source code** and on *Download from* choose **Main server**.
     - On the ***Developer Options*** tab, mark the check box **Pre-released updates**.
     - On the ***Additional Drivers*** tab, select the most recent graphics card driver and then click on **Apply changes**.
   - **After that, execute the following commands below:** 
     - sudo apt update
     - sudo apt upgrade   

2. **Install the CUDA Toolkit. Download it from Nvidia website in the .run(local) format**.
    - CUDA Toolkit: <span><a href="https://developer.nvidia.com/cuda-toolkit" target="_blank">CUDA Toolkit</a></span>
    - Direct link to CUDA 10.1 version: <span><a href="https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal">CUDA 10.1 version</a></span>
    - Following the installation instructions, in the terminal window when the installation steps starts, **unselect** the option to install the graphics card's driver. This is necessary because the graphics card's driver is already configured and installed on Software & Updates.A guide to this process of installation can be found in the following link:<span><a href="https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions"> Guide to installation(Section 3.6)</a></span>

3. **Edit the *source.list* file adding the following deb-source lines in the end of the file:**
    - Command to access the *source.list* file: *sudo nano /etc/apt/sources.list*
    - Add the following lines bellow:
      - *deb http://ftp.cn.debian.org/debian sid main contrib non-free*
      - *deb-src http://ftp.cn.debian.org/debian sid main contrib non-free*

4. **Access:** <span><a href="https://caffe.berkeleyvision.org/install_apt.html" target="_blank">Caffe Ubuntu Installation</a></span>

5. **Choose and execute:**
    ```
    sudo apt build-dep caffe-cpu        # dependencies for CPU-only version
    sudo apt build-dep caffe-cuda       # dependencies for CUDA version
    ```
        
    - If you receive a file replacement error related to the cublas.h file, run the command below:
      - sudo dpkg -i --force-overwrite /var/cache/apt/archives/cuda-cublas-9-1_9.1.85.3-1_amd64.deb    

6. **Baixar o projeto do Caffe do GitHub da Berkeley**
    > Repositório: https://github.com/BVLC/caffe

7. **Seguir instruções de compilação e de testes**
    > https://caffe.berkeleyvision.org/installation.html#compilation

8. **Configurar o arquivo Makefile.config**
    - Descomentar USE_CUDNN := 1 (Linha 5) 
    - Ajustar versão do OpenCV (Linha 23)
    - Ajustar diretório do CUDA (Linha 30)
    - Comentar as linhas da arquitetura do CUDA dependendo da versão do CUDA (Linhas 39 e 40)
    - BLAS:= open (Linha 53)
    - Ajustar versão do Python (Linhas 81, 82 e 83)
    - Incluir as seguintes linhas nas linhas 97 e 98:
    - INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
    - LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
9. **Instalar OpenBlas**
    - sudo apt install liblapack-dev liblapack3 libopenblas-base libopenblas-dev
10. **Instalar o python-numpy**
    - sudo apt-get install python-numpy
11. **Executar os comandos para compilação e teste:**
    - make all -j8
    - make test
    - make runtest
12. **Executar o comando export abaixo:**
    - export PYTHONPATH=/home/mfcs/caffe/python:$PYTHONPATH
13. **Executar o pycaffe.py**
    - No diretório raiz do projeto do Caffe, executar o seguinte comando: **make pycaffe** 
    
### Comando para monitorar o uso da GPU no terminal:
> *watch -n 1 nvidia-smi*

