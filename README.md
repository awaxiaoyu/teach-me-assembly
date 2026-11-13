# Teach Me Assembly

Teach Me Assembly 是一个适用于 IDA Pro 9.5 的纯本地 IDAPython 插件。它根据单条汇编指令和操作数添加中文语义注释，不使用 AI、网络服务，也不依赖相邻指令或函数上下文。

## 安装

将 `zh_semantic.py` 和 `zh_semantic_rules.json` 复制到 IDA 的 `plugins` 目录，然后重启 IDA。

在反汇编视图中将光标放到目标函数，使用 **Edit > Plugins > Teach Me Assembly**，或按 **Ctrl+Alt+Shift+S**。插件会为光标所在函数中的指令添加或更新 `【语义】` 注释，并保留其他现有注释。

## 功能

- 根据 IDA 解码结果说明寄存器、立即数、内存和代码地址操作数。
- 解释常见 x86 条件跳转、`cmovcc`、`setcc`、循环、栈操作、调用和算术标志位。
- 提供 ARM、MIPS、RISC-V 常见数据传送、算术、移位和分支指令的本地规则。
- 根据处理器和操作数顺序说明数据传送方向。
- 通过本地 JSON 文件覆盖或添加助记符说明。

每条指令独立解释；插件不会推断跨指令的数据流或函数意图。未覆盖的助记符会显示通用说明。

## 自定义规则

编辑 `zh_semantic_rules.json` 中的 `mnemonics` 映射。键使用小写助记符，描述可使用 `{mnemonic}` 和 `{operands}` 占位符。自定义规则优先于内置规则，每次运行时重新读取。

```json
{
  "mnemonics": {
    "my_custom_opcode": "项目自定义语义：{operands}"
  }
}
```

## 开发与许可

插件使用 IDA 自带的 IDAPython API，不需要额外 Python 依赖。项目使用 MIT License，详见 [LICENSE](LICENSE)。
