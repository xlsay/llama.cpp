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
    cmake -B build_gpu -DLLAMA_CUDA=ON
    cmake --build build_gpu --config Release 
    此外，~/.bashrc 中添加 export LLAMA_CUDA_NVCC=/THE/NVCC/EXE/PATH
    ```
    
    - 编译gpu版server
    
    ```bash
    cd llama.cpp/examples/server
    cmake -B build   
    ```

    Test:  
    ```
    cd llama.cpp/build_gpu/bin
     ./main -m /path/to/llmweights.gguf -n 256 --repeat_penalty 1.0 --color -i -r "User:" -f ../../prompts/chat-with-bob.txt -ngl 30
     
     显存占用测试：
    ggml_cuda_init: found 2 CUDA devices:
      Device 0: NVIDIA GeForce GTX 1080 Ti, compute capability 6.1, VMM: yes
      Device 1: NVIDIA GeForce GTX 1080 Ti, compute capability 6.1, VMM: yes
    
    一层都没加载时，显存占用 372M+152M    
    llama-2-7b-chat.Q8_0                33层全部加载后，3894M+3606M  
    Mistral-7B-Instruct-v0.3.Q8_0       33层全部加载后，372M+152M  

    开启服务：
    ./server -m /path/to/llmweights.gguf -c 2048 --host 0.0.0.0 --port 8081  -ngl 33
    ref: 参数 https://github.com/ggerganov/llama.cpp/tree/master/examples/server
    注：8080会报错 404 page not found

    浏览器地址栏输入： http://IP:8081/
    OR:
    curl --request POST \
    --url http://IP:8081/completion \
    --header "Content-Type: application/json" \
    --data '{"prompt": "Building a website can be done in 10 simple steps:","n_predict": 128}'
    ```
    
