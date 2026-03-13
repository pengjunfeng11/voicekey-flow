# VoiceKey Flow

`VoiceKey Flow` is a Codex skill project for connecting `DJI Mic Mini` with `Typeless` or a macOS dictation workflow.

It is designed to improve office input efficiency by turning a hardware microphone button into a reliable voice-to-text trigger.

## What this project does

- identifies the button event exposed by `DJI Mic Mini`
- uses `Karabiner-Elements` to map that event
- binds the mapping to `Typeless` or dictation shortcuts
- documents the stable path and the device-side limitations

## Core scenario

The skill is built for workflows such as:

1. press the Mic Mini button
2. start voice-to-text or dictation
3. speak instead of typing
4. finish input faster in chat, notes, or office tools

## Files

- `SKILL.md`: trigger description and execution workflow
- `references/manual.md`: detailed setup, installation, IDs, and troubleshooting

## Verified device facts

- Device family: `DJI Mic Mini`
- `vendor_id`: `11427`
- `product_id`: `16401`
- button event: `consumer_key_code: volume_increment`

## Notes

This project intentionally documents that double-click and long-press behaviors are not reliable on this device, because the hardware itself may consume those gestures.

---

## 中文说明

`VoiceKey Flow` 是一个专门用于连接 `DJI Mic Mini`、`Typeless` 和 macOS 听写工作流的 Codex Skill 项目。

它的目标很直接：

- 把麦克风上的实体按键接入电脑端
- 把这个按键映射成稳定可用的语音输入触发器
- 用更自然的语音转文字方式替代一部分手工打字
- 提升聊天、办公、记录和日常输入效率

## 这个项目解决什么问题

- 识别 `DJI Mic Mini` 暴露给 macOS 的按钮事件
- 使用 `Karabiner-Elements` 对该事件进行按键映射
- 将映射结果绑定到 `Typeless` 或 macOS 听写快捷键
- 沉淀安装、排查、设备限制和可复用配置

## 核心使用场景

这个 Skill 适合下面这类工作流：

1. 按下 `DJI Mic Mini` 的按钮
2. 启动语音转文字或系统听写
3. 直接说话，而不是手动长段打字
4. 更快地完成聊天、记录、写提示词或办公输入

## 项目文件

- `SKILL.md`：Skill 的触发说明和执行流程
- `references/manual.md`：详细安装步骤、设备 ID、配置方式和排查手册

## 已确认的设备信息

- 设备类型：`DJI Mic Mini`
- `vendor_id`：`11427`
- `product_id`：`16401`
- 按钮事件：`consumer_key_code: volume_increment`

## 设备限制说明

这个项目明确记录了设备侧限制：

- 双击不适合作为稳定映射手势，因为设备本身可能会把它识别成蓝牙重配对
- 长按也不适合作为稳定映射手势，因为该设备不会持续向电脑上报可靠的 held-down 状态

因此，当前推荐路径是优先使用单击触发语音输入，再由软件侧完成后续工作流。
