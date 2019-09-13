<p><img src="caffe.png" align="left" width="175" height="90" /></p>

# How to install Caffe - The framework for Deep Learning on Ubuntu 18.04 LTS with CUDA 10.1
This repository is just a guide to install the Framework Caffe for Deep Learning in a straight forward way.


### Comando para monitorar o uso da GPU no terminal
```
watch -n 1 nvidia-smi
```
### Arquivo contendo as bibliotecas para serem instaladas utilizadas pelo Caffe. A instalação é feita utilizando-se o arquivo **caffe_requirements.txt**. Utilize o comando abaixo para executar a instalação:
```
Python 2: pip install -r caffe_requirements.txt
Python 3: pip3 install -r caffe_requirements.txt
```
### Instruções para compilação do Caffe *from source*

1. Ajustar e Executar 
    - Em Software & Updates, na aba “Ubuntu Software” marcar o check box “source code” e em Download from escolher “Main server”. Na aba Developer Options, marcar o check box “Pre-released updates”. Na aba “Additional Drivers” selecionar o driver mais atual da placa de vídeo e clicar em “Apply changes”.
    - sudo apt update
    - sudo apt upgrade

2. Instalar CUDA Toolkit. Baixar do site da NVidia no formato deb(local).
    - CUDA Toolkit: https://developer.nvidia.com/cuda-toolkit
    - Link direto para a versão CUDA 10.1: https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&target_distro=Ubuntu&target_version=1804&target_type=runfilelocal
    - Ao seguir as instruções de instalação, quando abrir a janela no terminal para instalar, DESATIVAR a opção de instalar o DRIVER, pois, o driver já foi setado e instalado no Software & Updates.
    - Tutorial: https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions (Seção 3.6)

3. Acessar o arquivo source.list e adicionar as linhas de deb-source
    - Acessar arquivo: sudo nano /etc/apt/sources.list
    - Adicionar as linhas abaixo:
      - deb http://ftp.cn.debian.org/debian sid main contrib non-free
      - deb-src http://ftp.cn.debian.org/debian sid main contrib non-free

4. Acessar https://caffe.berkeleyvision.org/install_apt.html

5. Executar:
    - sudo apt build-dep caffe-cpu        # dependencies for CPU-only version
    - sudo apt build-dep caffe-cuda       # dependencies for CUDA version
    - Caso dê problema com overwrite do cublas.h executar o comando abaixo:
       - sudo dpkg -i --force-overwrite /var/cache/apt/archives/cuda-cublas-9-1_9.1.85.3-1_amd64.deb You need to remove that package

6. Baixar o projeto do Caffe do GitHub da Berkeley
    - Repositório: https://github.com/BVLC/caffe

7. Seguir instruções de compilação e de testes
    - https://caffe.berkeleyvision.org/installation.html#compilation

8. Configurar o arquivo Makefile.config
    - Descomentar USE_CUDNN := 1 (Linha 5) 
    - Ajustar versão do OpenCV (Linha 23)
    - Ajustar diretório do CUDA (Linha 30)
    - Comentar as linhas da arquitetura do CUDA dependendo da versão do CUDA (Linhas 39 e 40)
    - BLAS:= open (Linha 53)
    - Ajustar versão do Python (Linhas 81, 82 e 83)
    - Incluir as seguintes linhas nas linhas 97 e 98:
    - INCLUDE_DIRS := $(PYTHON_INCLUDE) /usr/local/include /usr/include/hdf5/serial/
    - LIBRARY_DIRS := $(PYTHON_LIB) /usr/local/lib /usr/lib /usr/lib/x86_64-linux-gnu/hdf5/serial/
9. Instalar OpenBlas
    - sudo apt install liblapack-dev liblapack3 libopenblas-base libopenblas-dev
10. Instalar o python-numpy
    - sudo apt-get install python-numpy
11. Executar os comandos para compilação e teste:
    - make all -j8
    - make test
    - make runtest
12. Executar o comando export abaixo:
    - export PYTHONPATH=/home/mfcs/caffe/python:$PYTHONPATH
13. Executar o pycaffe.py
    - No diretório raiz do projeto do Caffe, executar o seguinte comando: **make pycaffe** 

