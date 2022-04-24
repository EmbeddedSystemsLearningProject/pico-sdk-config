# Instalación de SDK RaspberryPi pico

Instalar dependencias

```sh
sudo apt update
sudo apt upgrade
sudo apt install git cmake gcc-arm-none-eabi gcc g++ libstdc++-arm-none-eabi-newlib libnewlib-arm-none-eabi
sudo apt install automake autoconf build-essential texinfo libtool libftdi-dev libusb-1.0-0-dev
sudo apt install doxygen
```

Crear una carpeta para almacenar todas las dependencias, en este caso se utiliza la carpeta `pico` en el directorio home

```sh
mkdir ~/pico
```

Descargar repositorios

```sh
cd ~/pico
git clone -b master https://github.com/raspberrypi/pico-examples.git
git clone -b master https://github.com/raspberrypi/pico-sdk.git
git clone -b master https://github.com/raspberrypi/pico-extras.git
cd pico-sdk
sudo git submodule update --init
```

Añadir el toolchain al PATH

```sh
# Añadir las siguientes linea a ~/.bashrc
export PICO_SDK_PATH=/home/camilo/pico/pico-sdk
export PICO_EXAMPLES_PATH=/home/camilo/pico/pico-examples
export PICO_EXTRAS_PATH=/home/camilo/pico/pico-extras
export PICO_PLAYGROUND_PATH=/home/camilo/pico/pico-playground
# Recargar el PATH
source ~/bashrc
```

Compilar los ejemplos

```sh
sudo mkdir ~/pico/pico-examples/build
sudo chmod 777 ~/pico/pico-examples/build
cd ~/pico/pico-examples/build
cmake ..
```

Ingresar a ejemplo especifico y compilarlo con make, si hay un .utf es que todo salio bien.

```sh
cd blink
make
```

# Picoprobe para debug

## Configuración de USB en WSL (USBIP)

### Configuración en Linux

```sh
sudo apt install linux-tools-virtual hwdata
sudo update-alternatives --install /usr/local/bin/usbip usbip /usr/lib/linux-tools/*/usbip 20
```

### Configuración en Windows

En powershell

```powershell
winget install --interactive --exact dorssel.usbipd-win
```

Listar dispositivos usb y ver ID con lo siguiente

```powershell
usbipd wsl list
```

Conectar el dispositivo USB a Linux y desconectarlo de Windows

```powershell
usbipd wsl attach -b 1-12 -d Ubuntu-USBIP
# Remplazar "1-12" por el ID del USB
# Remplazar "Ubuntu-USBIP" por la distribución utilizada, o dejar en blanco en caso de que se quiera usar la distribución por defecto
```

## Configuración compatible con Linux

