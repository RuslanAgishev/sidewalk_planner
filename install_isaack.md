# Pуководство по установке и запкуску Isaac SDK и Isaac Sim
Подразумевается, что система свежая и драйвера отсутствуют.
В конце я приложил ссылку на английское руководство по установке драйвера Nvidia  и CUDA. Если лень следовать по английскому мануалу, то следуй моему:

Для начала зарегистрируйся как разработчик на Nvidia по ссылке [https://developer.nvidia.com/developer-program](https://developer.nvidia.com/developer-program). Это понадобится для загрузки Isaac SDK  позже.

1. Верифицируй GPU, что он поддерживает CUDA
	```bash
	lspci | grep -i nvidia
	```
2. Верифицирую версию Линукса:
	```bash
	uname -m && cat /etc/*release
	```
	Должен выдать архитектуру и вервию 18.04  Линукса
	```bash
	x86_64
	```
3. Проверь, что gcc установлена:
	```bash
	gcc --version
	```
4. Также проверь версию ядра, которую система использует:
	```bash
	uname -r
	```
	Потом установи эту версию, набрав команду:
	```bash
	sudo apt-get install linux-headers-$(uname -r)
	```
5. Скачай .run файл CUDA 10.0 на UBUNTU 18.04 куда по ссылке:
	[https://developer.nvidia.com/compute/cuda/10.0/Prod/local\_installers/cuda\_10.0.130\_410.48\_linux](https://developer.nvidia.com/compute/cuda/10.0/Prod/local_installers/cuda_10.0.130_410.48_linux)
	Эта версия установки включает в себя поддерживаемый драйвер NVIDIA, чтобы не заморачиваться с подборкой подходящей версии драйвера.
	Проверь корректность файла, вставив название скаченного файла .run
	```bash
	md5sum <file>
	```

7.  Дезактивируй  Nouveau  если эта команда что-то показывает
	```bash
	lsmod | grep nouveau
	```
	Далее, создай файл  /etc/modprobe.d/blacklist-nouveau.conf и добавь туда следующие строки
	```python
	blacklist nouveau options 
	nouveau modeset=0
	```
	обнови initramfs
	```bash
	sudo update-initramfs -u
	```
8. перейди в текстовый режим 
	```bash
	sudo init 3
	```
9. Проверь опять Nouveau
	```bash
	lsmod | grep nouveau
	```
10. Если ничего не распечатывает, то запусти установку CUDA
	```bash
	sudo sh cuda_10.0.130_410.48_linux.run
	```
	Далее следуй инструкции установки
11. Перезагрузит компьютер
12. Проверь установку драйверов:
	```bash
	nvidia-smi
	```
Должно выдать что-то вот такое 
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 435.27.08    Driver Version: 435.27.08    CUDA Version: 10.0     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|============================+======================+=====|
|   0  GeForce RTX 2080    Off  | 00000000:01:00.0 Off |                  N/A |
|  0%   34C    P8     1W / 260W |      0MiB /  7982MiB |      0%      Default |
+-------------------------------+----------------------+----------------------+
+-----------------------------------------------------------------------------+
| Processes:                                                       GPU Memory |
|  GPU       PID   Type   Process name                             Usage      |
|=============================================================================|
|  No running processes found                                                 |
+-----------------------------------------------------------------------------+



## Установка Vulkan SDK
1.  Дальше нужно установить Vulkan SDK по ссылке 
	[https://vulkan.lunarg.com/sdk/home#sdk/downloadConfirm/1.1.126.0/linux/vulkansdk-linux-x86\_64-1.1.126.0.tar.gz](https://vulkan.lunarg.com/sdk/home#sdk/downloadConfirm/1.1.126.0/linux/vulkansdk-linux-x86_64-1.1.126.0.tar.gz)
2.  И нажать скачать версию 1.1.126.0. После чего в папке где находится файл нужно пописать следующие команды
	```bash
	mkdir ~/vulkan
	mv vulkansdk-linux-x86_64-1.1.126.0.tar.gz ~/vulkan
	cd ~/vulkan
	tar -xvf vulkansdk-linux-x86_64-1.1.126.0.tar.gz
	echo "source ~/vulkan/1.1.126.0/setup-env.sh" >> ~/.bashrc
	```
3.  После проверь установку 
	```bash
	export | grep VK_LAYER_PATH
	```
	Что должно выдать 
	```python
	declare -x VK_LAYER_PATH="/home/USERNAME/vulkan/1.1.126.0/x86_64/etc/explicit_layer.d"
	```
4. Проверь если вулкан совместим с драйвером нвидиа
	```bash
	sudo vulkaninfo
	```
	не должно выдавать ошибки `failed with VK_ERROR_INITIALIZATION_FAILED`. Если выдает ошибку эту, то напиши мне, будем думать вместе. Если нет, то продолжи установку. 

## Установка `Isaac_Sim_1.2`
1. Скачай `Isaac_Sim_1.2`  по ссылке [https://github.com/NvPhysX/UnrealEngine](https://github.com/NvPhysX/UnrealEngine)
2. Введи мой пароль и логин от gitHub:
	[ks14203@bristol.ac.uk](ks14203@bristol.ac.uk)
	UclUk1991
3. Клонируй копию себе в home папку  и переименуй в `isaacSim`:
	```bash
	git clone <repository_link> isaacSim
	```
4. далее набери в терминале: 
	```bash
	cd ~/isaacSim
	git checkout IsaacSim_1.2
	```
5. Удали в `isaacSim` файл по команде
	```bash
	rm Engine/Build/IsaacSimProject_1.2_Core.gitdeps.xml
	```
6. Перейди по ссылке[ Isaac Sim Content XML](https://developer.nvidia.com/isaac/downloads) и скачай файл нажав третью сверху кнопку _Download_ 
7. Разархивируй файл по команде 
	```bash
	tar -xvzf IsaacSimProject_1.2.1238533.gitdeps.tar.gz -C <ISAAC_SIM_ROOT_PATH>/Engine/Build
	```
	Сюда `<ISAAC_SIM_ROOT_PATH>` вставь локацию, где находится симулятор `isaacSim` твой
8.  Потом прогони 
	```bash
	sudo ./Setup.sh
	```
9.  После 
	```bash
	./GenerateProjectFiles.sh
	```
10.  После 
	```bash
	./GenerateTestRobotPaths.sh
	```
11.  И в конце 
	```bash
	make && make IsaacSimProjectEditor
	```

## Установка  Isaac SDK
1.  Скачай Isaac SDK по ссылке [https://developer.nvidia.com/isaac/downloads](https://developer.nvidia.com/isaac/downloads) и выбери первую кнопку download 
2. Разархивируем в home директорию
	```bash
	tar -xvzf isaac-sdk-2019.2-30e21124.tar.xz 
	```
4. Скачай бейзел версию `bazel-0.19.2-installer-linux-x86_64.sh` по ссылке [https://github.com/bazelbuild/bazel/releases/tag/0.19.2](https://github.com/bazelbuild/bazel/releases/tag/0.19.2)
5. Установи basel:
	```bash
	chmod +x bazel-0.19.2-installer-linux-x86_64.sh
	./bazel-0.19.2-installer-linux-x86_64.sh --user
	export PATH="$PATH:$HOME/bin"
	```
	Можешь добавить последнюю линию в `.bashrc` для автоматизации.
5. Устанавливаем все нужные пакеты из папки где хранится Isaac SDK
	```bash
	engine/build/scripts/install_dependencies.sh
	```
6. Внутри файла `apps/carter/carter_sim/bridge_config/carter_full.json ` в папке Isaac SDK меняешь содержимое на следующее:
	```python
	{
	 "graphs": ["ABSOLUTE_PATH_TO/apps/carter/carter_sim/bridge_config/carter_full_graph.json"],
	 "configs": ["ABSOLUTE_PATH_TO/apps/carter/carter_sim/bridge_config/carter_full_config.json"]
	}
	```
7.  Запускаем картер робота по команде из Isaac SDK папки:
	```bash
	bazel run apps/carter/carter_sim:carter_sim -- --config="apps/assets/maps/carter_warehouse_p.config.json" --graph="apps/assets/maps/carter_warehouse_p.graph.json"
	```
	потом открываем браузер и набираем `localhost:3000 `   и должно появиться следующее:
	 ![](DraggedImage.tiff)
8.  Потом переходишь в Isaac Sim репозиторий и набираешь:
```bash
./Engine/Binaries/Linux/UE4Editor IsaacSimProject CarterWarehouse_P -vulkan -isaac_sim_config_json="<ABSOLUTE_PATH_TO_ISAACSDK>/apps/carter/carter_sim/bridge_config/carter_full.json"
```

** на этом этапе и вылетает ошибка с вулканом `failed with VK_ERROR_INITIALIZATION_FAILED`**

Скачай инструкцию по установке куды с .run файла и следуй ей для установки CUDA 10.0 и Nvidia драйверов :
![](#)
