FROM pytorch/pytorch:1.10.0-cuda11.3-cudnn8-runtime AS multitask

RUN apt-get update && apt-get install -y git gcc g++

RUN . /root/.bashrc && conda init bash && . /root/.bashrc && conda create -n multitask python=3.8 anaconda && conda activate multitask

#RUN conda activate multitask

RUN conda install torchvision=0.11.2 cudatoolkit=11.3 -c pytorch

RUN pip install --no-cache-dir \
    'opencv-python>=4.2.0.34' \
    torchmetrics==0.6.2 \
    wandb==0.12.8
    
RUN conda install 'protobuf<=3.19.1' && pip install onnx==1.11.0

RUN pip install git+https://github.com/cocodataset/panopticapi.git

# -> for ./external only
# see: https://detectron2.readthedocs.io/en/latest/tutorials/install.html)
RUN python -m pip install detectron2 -f https://dl.fbaipublicfiles.com/detectron2/wheels/cpu/torch1.10/index.html


# dataset package
COPY ./lib/ ./
RUN pip install scipy && pip install -e ./nicr-scene-analysis-datasets

# multitask scene analysis package
RUN pip install -e ./nicr-multitask-scene-analysis
