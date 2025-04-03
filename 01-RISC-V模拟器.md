# *RISC-V 模拟器*

## **1. 题目背景**
RISC-V 是一个开源的指令集架构（ISA），广泛应用于嵌入式系统、高性能计算和新兴处理器设计。本次 Hackathon 要求参赛者实现一个 **RISC-V 指令集模拟器**，能够解析并执行 RISC-V 汇编代码，并支持基本的调试功能。

---

## **2. 任务要求**
### **2.1 基础功能（必做）**
- **支持 RV32I 基础指令集**（整数指令集，如 `add`, `sub`, `lw`, `sw`, `beq`, `jal` 等）。
- **实现内存模拟**（支持加载/存储指令）。
- **支持寄存器文件**（32 个通用寄存器 `x0-x31`，`x0` 硬编码为 0）。
- **解析并执行 RISC-V 汇编代码**（可接受 `.s` 或 `.bin` 格式输入）。
- **基本执行模式**：单步执行（step-by-step）或连续执行（run）。

### **2.2 进阶功能（选做，加分项）**
- **支持更多指令集扩展**（如 `M` 扩展（乘除法）、`C` 扩展（压缩指令）、`F` 扩展（单精度浮点））。
- **支持 ELF 文件加载**（直接运行编译后的 RISC-V 程序）。
- **实现调试功能**（如断点调试、寄存器/内存查看、PC 跟踪）。
- **优化性能**（如 JIT 编译、指令缓存）。
- **可视化界面**（如终端 UI 或 Web 界面显示执行过程）。

---

## **3. 输入/输出要求**
### **输入**
- 可以是 **RISC-V 汇编文件**（`.s`）或 **二进制文件**（`.bin`）。
- 示例测试用例。

### **输出**
- 执行结束后，输出 **寄存器的最终状态** 和 **关键内存区域**。
- 支持 **执行日志**（可选，如每执行一条指令后打印 PC 和指令内容）。

---

## **4. 开发约束**
- **语言不限**（推荐 C/C++/Rust/Python，但允许其他语言）。
- **不允许直接使用现有完整模拟器**（如 QEMU、Spike），但可参考其实现。
- **允许使用部分库**（如 ELF 解析库、终端 UI 库）。

---

## **5. 提交要求**
- **代码仓库**（GitHub/GitLab 链接，或压缩包）。
- **README.md**（说明如何编译、运行，以及实现了哪些功能）。
- **演示**（讲解 + 运行示例）。

---

## **6. 示例测试用例**
### **6.1 基础测试（RV32I）**
```asm
# 计算 1+2+3+...+10，结果存入 x10
addi x10, x0, 0   # sum = 0
addi x11, x0, 1   # i = 1
addi x12, x0, 11  # 循环上限
loop:
    add x10, x10, x11  # sum += i
    addi x11, x11, 1   # i++
    blt x11, x12, loop  # if i < 11, jump to loop
```
**预期输出**：`x10 = 55`

### **6.2 进阶测试（RV32IM）**
```asm
# 计算 5! (阶乘)，结果存入 x10
addi x10, x0, 1   # res = 1
addi x11, x0, 5   # n = 5
factorial:
    beq x11, x0, end  # if n == 0, exit
    mul x10, x10, x11 # res *= n
    addi x11, x11, -1 # n--
    jal x0, factorial
end:
```
**预期输出**：`x10 = 120`

---

## **7. 参考资料**
- [RISC-V 官方手册](https://riscv.org/technical/specifications/)
- [RISC-V 汇编入门](https://github.com/riscv/riscv-asm-manual)
- [简单模拟器参考（TinyEMU）](https://bellard.org/tinyemu/)
- [QEMU RISC-V 模拟器](https://github.com/qemu/qemu)
- [spike 模拟器](https://www.github.com/riscv-software-src/riscv-isa-sim)

## **8.参考实现**
PLCT lab 刘阳老师的实现项目。
- [rvemu](https://github.com/ksco/rvemu)
- [nano](https://github.com/ksco/nanoemu)

> **_NOTE:_**  题目框架为AI生成，内容由延迟低部分修改，如有疑问请联系延迟低。