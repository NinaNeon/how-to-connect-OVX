FROM pytorch/pytorch:2.1.0-cuda11.8-cudnn8-runtime

# 避免 tzdata 安裝時進入互動模式
ENV DEBIAN_FRONTEND=noninteractive

# 安裝必要的系統工具與 GPU 監控工具（nvidia-smi 來自 nvidia-utils）
RUN apt-get update && apt-get install -y \
    tzdata \
    git \
    wget \
    curl \
    nano \
    unzip \
    libglib2.0-0 \
    libsm6 \
    libxext6 \
    libxrender-dev \
    nvidia-utils-525 \
    && apt-get clean && rm -rf /var/lib/apt/lists/*

# 升級 pip 並安裝 Python 所需套件，包括 diffusers、Pillow、matplotlib、GPUtil
RUN pip install --upgrade pip && \
    pip install \
    torch torchvision torchaudio \
    transformers accelerate \
    pandas openpyxl datasets scikit-learn \
    sentencepiece protobuf \
    diffusers Pillow \
    matplotlib GPUtil

# 複製 Omniverse Farm 所需腳本與工具
COPY thirdparty/omnicli /omnicli
COPY scripts/docker/run.sh /run.sh
RUN chmod +x /omnicli/omnicli && chmod +x /run.sh
RUN sed -i 's/\r$//' /run.sh
