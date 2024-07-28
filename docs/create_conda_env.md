
## if create a new environment on the CUDA 12.1
```shell
conda create -n surfel_splatting python==3.8
conda activate surfel_splatting
git submodule update --remote
pip install -r requirements.txt
pip install torch==2.1.1 torchvision==0.16.1 torchaudio==2.1.1 --index-url https://download.pytorch.org/whl/cu121 
pip install submodules/diff-surfel-rasterization
pip install submodules/simple-knn
```

[Return Main Page](../README.md)
