## Create `GaussianSplatting` folder as your root folder for datasets
```shell
mkdir GaussianSplatting && cd GaussianSplatting
```

### 1. Download datasets of Mip-NeRF360  
```shell
#mkdir Mip-NeRF360 && cd Mip-NeRF360
wget http://storage.googleapis.com/gresearch/refraw360/360_v2.zip && unzip -d Mip-NeRF360 360_v2.zip && rm 360_v2.zip
wget https://storage.googleapis.com/gresearch/refraw360/360_extra_scenes.zip && unzip -d Mip-NeRF360 360_extra_scenes.zip && rm 360_extra_scenes.zip 
```
