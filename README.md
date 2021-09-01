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
