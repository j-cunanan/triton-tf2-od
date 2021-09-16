# triton-tf2-od
# Setup on Jetson Xavier AGX
- Download the appropriate binaries from https://github.com/triton-inference-server/server/tags for your system requirements.
  - At the time of writing, I am using `tritonserver2.12.0-jetpack4.6.tgz`.
- Untar in your desired directory. e.g. `mytritonserver`
- Add the `tritonserver` binary to your `PATH`
  ``` 
  echo "export PATH=/PATH_TO_mytritonserver/bin/:$PATH" >> ~/.bashrc
  source ~/.bashrc 
    ```
- Install Triton dependencies
```
apt-get update && \
    apt-get install -y --no-install-recommends \
        software-properties-common \
        autoconf \
        automake \
        build-essential \
        cmake \
        git \
        libb64-dev \
        libre2-dev \
        libssl-dev \
        libtool \
        libboost-dev \
        libcurl4-openssl-dev \
        libopenblas-dev \
        rapidjson-dev \
        patchelf \
        zlib1g-dev
```
- Install the python client.
```
python3 -m pip install --upgrade {mytritonserver}/clients/python/tritonclient-2.12.0-py3-none-linux_aarch64.whl[all]
```

- Download sample Triton ready model files: https://www.dropbox.com/s/232bx8o814z8xqt/tritonmodels.zip?dl=0

# Test the server
```
BACKEND_DIR=/opt/tritonserver/backends
MODEL_DIR=/home/user/tritonmodels

tritonserver --model-repository=$MODEL_DIR --backend-directory=$BACKEND_DIR --backend-config=tensorflow,version=2 --strict-model-config-false
```

# Check server inference statistics
```
perf_analyzer -m cocoD0 --shape input_tensor:1,720,1280,3
```
