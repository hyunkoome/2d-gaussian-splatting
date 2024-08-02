## Training
To train a scene, simply use
```bash
python train.py -s <path to COLMAP or NeRF Synthetic dataset>
```
Commandline arguments for regularizations
```bash
--lambda_normal  # hyperparameter for normal consistency
--lambda_distortion # hyperparameter for depth distortion
--depth_ratio # 0 for mean depth and 1 for median depth, 0 works for most cases
```
**Tips for adjusting the parameters on your own dataset:**
- For unbounded/large scenes, we suggest using mean depth, i.e., ``depth_ratio=0``,  for less "disk-aliasing" artifacts.


## Testing
### Bounded Mesh Extraction
To export a mesh within a bounded volume, simply use
```bash
python render.py -m <path to pre-trained model> -s <path to COLMAP dataset> 
```
Commandline arguments you should adjust accordingly for meshing for bounded TSDF fusion, use
```bash
--depth_ratio # 0 for mean depth and 1 for median depth
--voxel_size # voxel size
--depth_trunc # depth truncation
```
If these arguments are not specified, the script will automatically estimate them using the camera information.
### Unbounded Mesh Extraction
To export a mesh with an arbitrary size, we devised an unbounded TSDF fusion with space contraction and adaptive truncation.
```bash
python render.py -m <path to pre-trained model> -s <path to COLMAP dataset> --mesh_res 1024
```

### 1. Link data directory for Mip-NeRF360
```shell
mkdir data && cd data
ln -s <path to m360> m360

# for example 
ln -s ~/GaussianSplatting/Mip-NeRF360 m360
cd ..
```

### 1. Training for Mip-NeRF360  
 
```shell
python train.py -s <path to m360>/<garden> -m output/m360/garden

python train.py -s data/m360/garden  -m output/m360/garden
```

### 2. Testing: Unbounded Mesh Extraction for Mip-NeRF360  
```shell
# use our unbounded mesh extraction!!
python render.py -s <path to m360>/<garden> -m output/m360/garden --unbounded --skip_test --skip_train --mesh_res 1024

python render.py -s data/m360/garden -m output/m360/garden --unbounded --skip_test --skip_train --mesh_res 1024
```

### 3. Testing: Bounded Mesh Extraction for Mip-NeRF360  
```shell
# or use the bounded mesh extraction if you focus on foreground
python render.py -s <path to m360>/<garden> -m output/m360/garden --skip_test --skip_train --mesh_res 1024

python render.py -s data/m360/garden -m output/m360/garden --skip_test --skip_train --mesh_res 1024
```