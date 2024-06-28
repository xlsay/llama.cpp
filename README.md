Forked 2024-06-28， [orig README](README.md.orig)

### Build

In order to build llama.cpp you have four different options.

- Using `CMake`:
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

    
    ```bash
    cmake -B build
    cmake --build build --config Release
    ```
