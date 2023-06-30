# ShellCode-NewInjection
新注入技术的 POC，滥用 windows fork API 来逃避 EDR。

### Usage 
DirtyVanity.exe [TARGET_PID_TO_REFLECT]

### Runtime steps
 * 分配并写入shellcode到[TARGET_PID_TO_REFLECT]
 * 将 [TARGET_PID_TO_REFLECT] 分叉到一个新进程
 * 将分叉进程的起始地址设置为克隆的shellcode
  
### Shellcode
反射的 shellcode 可与 ntdll API 配合使用。它是从包含的生成项目`shellcode_template`生成的，
感谢 https://github.com/rainerzufalldererste/windows_x64_shellcode_template

### Shellcode customization
定制 shellcode：
* 根据 https://github.com/rainerzufalldererste/windows_x64_shellcode_template 中的说明，编辑 `shellcode_template` 项目内的 `shellcode_template` 函数
* 编译
* 使用您最喜欢的 PE 解析工具（例如 IDA）裁剪 `shellcode_template` 函数字节
* 这些字节是与位置无关的 shellcode。将它们放在 `DirtyVanity.cpp` 中
* 执行 DirtyVanity 来观察它们的反射


