เพิ่มไฟล์ `.gitignore` ใน esp-idf project เพื่อป้องกันไม่ให้ส่งไฟล์ที่ไม่จำเป็นขึ้น remote repo


```
# ESP-IDF build output
/build/
/sdkconfig
/sdkconfig.old

# CMake cache
CMakeFiles/
CMakeCache.txt
cmake_install.cmake
install_manifest.txt

# Ninja build files
.ninja_deps
.ninja_log

# VSCode
.vscode/

# CLion / JetBrains
.idea/

# Python virtual environment
venv/
.env/

# Logs
*.log

# Generated binaries
*.bin
*.elf
*.map

# ESP-IDF Python tools cache
__pycache__/
*.pyc

# Partition table auto-generated
partition_table/

# ESP-IDF component manager
dependencies.lock
managed_components/

# Temporary files
*.tmp
*.bak

```