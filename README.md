Forked 2024-06-28， [orig README](README.orig.md)

### Build
OS: Ubuntu 22.04.3 LTS
cmake version 3.22.1

In order to build llama.cpp you have four different options.

Using `CMake` : 
    ```bash
    sudo apt-get update
    sudo apt-get install build-essential cmake

    如果安装cmake报错“libdvd-pkg: apt-get check failed, you may have broken packages. ”
    sudo dpkg --configure -a  # 修复损坏的包
    sudo apt-get install -f  # 修复依赖关系

    sudo apt-get check # 检查系统中是否还有其他损坏的包
    没错的话，再次尝试安装 build-essential 和 cmake：
    sudo apt-get install build-essential cmake
    还有错的话，或者问问chatgpt
    ```

    - cpu 版本:
    ```bash
    cmake -B build_cpu
    cmake --build build --config Release
    
    ```
    - gpu 版本:
    ```bash
    cmake -B build_gpu -DGGML_CUDA=ON
    cmake --build build_gpu --config Release
    
    ```
Teat:  
     ./main -m /path/to/llmweights.gguf -n 256 --repeat_penalty 1.0 --color -i -r "User:" -f ../../prompts/chat-with-bob.txt
