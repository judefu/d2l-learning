# 1. conda
参考[Installing Miniconda - Anaconda](https://www.anaconda.com/docs/getting-started/miniconda/install/overview)

---
1. 依次输入如下命令
```bash
wget https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh
bash ./Miniconda3-latest-Linux-x86_64.sh
```
 2. review the license agreement，点击一次 `enter`
 3. accept the license terms，输入`yes`
 4. 输入安装路径，默认在当前用户下`/home/test/miniconda3`，可以手动输入指定路径
 5. 是否初始化，输入`yes`
 6. 重新开启终端或者输入以下命令，激活`base`环境
 ```bash
 source ~/.bashrc
 ```
 - **检验是否安装成功：**
 输入：
 ```bash
 conda --version
 ```
 如果输出`conda`版本信息则安装成功
# 2. CUDA
参考
[CUDA on WSL User Guide — CUDA on WSL 13.2 documentation](https://docs.nvidia.com/cuda/wsl-user-guide/index.html)
[CUDA Installation Guide for Linux — Installation Guide for Linux 13.2 documentation](https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#post-installation-actions)
**注意：**
官方文档指出，**users must not install any NVIDIA GPU Linux driver within WSL 2**，并且默认的安装会覆盖WSL 2 NVIDIA 驱动，因此安装官方推荐的WSL-Ubuntu CUDA toolkit。
下载链接：[CUDA Toolkit 13.2 Update 1 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-downloads?target_os=Linux&target_arch=x86_64&Distribution=WSL-Ubuntu&target_version=2.0&target_type=deb_local)
CUDA版本：13.2

---
1. 移除旧的GPG key
```bash
sudo apt-key del 7fa2af80 #新版Ubuntu中没有此命令，可以跳过
```
2. 下载WSL-Ubuntu版安装包，依次输入以下命令：
```bash
1. wget https://developer.download.nvidia.com/compute/cuda/repos/wsl-ubuntu/x86_64/cuda-wsl-ubuntu.pin
2. sudo mv cuda-wsl-ubuntu.pin /etc/apt/preferences.d/cuda-repository-pin-600
3. wget https://developer.download.nvidia.com/compute/cuda/13.2.1/local_installers/cuda-repo-wsl-ubuntu-13-2-local_13.2.1-1_amd64.deb
4. sudo dpkg -i cuda-repo-wsl-ubuntu-13-2-local_13.2.1-1_amd64.deb
5. sudo cp /var/cuda-repo-wsl-ubuntu-13-2-local/cuda-*-keyring.gpg /usr/share/keyrings/
6. sudo apt-get update
7. sudo apt-get -y install cuda-toolkit-13-2
```
3. 配置环境变量，依次输入以下命令：
```bash
echo 'export PATH=${PATH}:/usr/local/cuda-13.2/bin' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=${LD_LIBRARY_PATH}:/usr/local/cuda-13.2/lib64' >> ~/.bashrc
```
4. 重新开启终端或者输入以下命令:
 ```bash
 source ~/.bashrc
 ```
- **检验是否配置成功：**
输入：
```
nvcc --version
```
输出版本信息则配置成功
# 3. cuDNN
下载链接：[cuDNN 9.22.0 Downloads | NVIDIA Developer](https://developer.nvidia.com/cudnn-downloads?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=24.04&target_type=deb_local&Configuration=Full)

---
依次执行以下命令：
```bash
1. wget https://developer.download.nvidia.com/compute/cudnn/9.22.0/local_installers/cudnn-local-repo-ubuntu2404-9.22.0_1.0-1_amd64.deb
2. sudo dpkg -i cudnn-local-repo-ubuntu2404-9.22.0_1.0-1_amd64.deb
3. sudo cp /var/cudnn-local-repo-ubuntu2404-9.22.0/cudnn-*-keyring.gpg /usr/share/keyrings/
4. sudo apt-get update
5. sudo apt-get -y install cudnn9-cuda-13
```