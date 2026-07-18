---
title: Cardputer-Adv 小智运动陪伴 / AI Sport Companion
version: v0.14.8
status: experimental-prototype
---

# 使用指南 / User Guide

> 会聊天、看 GPS、画简易轨迹并保存运动记录的 Cardputer-Adv 实验原型。
> An experimental Cardputer-Adv companion for voice chat, GPS status, route preview and workout records.

## 1. 主要功能 / Features

- 小智联网语音对话。/ Online XiaoZhi voice chat.
- 按键或语音开始、暂停、继续及结束记录。/ Start, pause, resume and finish by key or voice.
- GPS 卫星页：卫星数、HDOP、GSV 方位和定位状态。/ GPS view: satellites, HDOP, GSV positions and fix status.
- 轨迹页：距离、时间、速度和本次路线示意。/ Route view: distance, time, speed and route preview.
- 距离或时间目标、进度节点及手动打点。/ Distance or time goals, milestones and manual marks.
- 结束后保存 CSV、TXT 摘要和 GPX。/ Export CSV, TXT summary and GPX after finishing.

## 2. 硬件与烧录 / Hardware & Flash

| 项目 / Item | 要求 / Value |
| --- | --- |
| 主机 / Device | M5Stack Cardputer-Adv, ESP32-S3, 8MB Flash |
| GNSS | ATGM336H, RX 15 / TX 13, 115200 baud |
| 存储 / Storage | 可写 FAT32 microSD / Writable FAT32 microSD |
| 网络 / Network | 2.4GHz Wi-Fi 或手机热点 / Wi-Fi or phone hotspot |
| 公开固件 / Firmware | `Cardputer-Adv-Sport-v0.14.8.bin` |
| 烧录地址 / Address | `0x0` |
| Flash 设置 / Settings | ESP32-S3, 8MB, DIO, 80MHz |

这是完整直刷固件，会覆盖当前 Launcher。需要恢复 Launcher 时，请重新烧录官方固件。
This full-flash image replaces the current Launcher. Flash the official image again if you need to restore it.

命令行示例 / Command-line example:

```bash
python3 -m esptool --chip esp32s3 --port /dev/cu.usbmodem1101 \
  --baud 460800 --before default_reset --after hard_reset \
  write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB \
  0x0 "Cardputer-Adv-Sport-v0.14.8.bin"
```

## 3. 第一次使用 / First Start

1. 插入 GNSS 扩展和 FAT32 microSD。/ Insert the GNSS module and FAT32 microSD.
2. 开机并连接 2.4GHz Wi-Fi；iPhone 热点建议开启“最大兼容性”。/ Connect to 2.4GHz Wi-Fi; enable Maximize Compatibility on iPhone.
3. 按小智流程绑定设备并设置角色。/ Bind the device and configure the XiaoZhi agent.
4. 进入主界面后等待约 30 秒，再测试 SD 保存。/ Wait about 30 seconds before the first SD export test.
5. 到户外开阔位置等待定位。/ Wait for a GPS fix in an open outdoor area.

## 4. 按键 / Keys

| 按键 / Key | 功能 / Action |
| --- | --- |
| `S` | 开始、暂停、继续 / Start, pause, resume |
| `M` | 手动打点 / Add a mark |
| `E` | 结束并排队保存 / Finish and queue export |
| `G` | GPS 卫星页 / GPS satellite view |
| `R` | 本次轨迹页 / Current route view |
| `Enter` | 开始或结束小智对话 / Toggle XiaoZhi chat |
| `↑ / ↓` | 音量 / Volume |
| `← / →` | 屏幕亮度 / Brightness |
| Wi-Fi 页 `W` | 键盘配网 / Wi-Fi setup |
| Wi-Fi 页 `S` | 已保存网络 / Saved networks |

GPS 和轨迹页约 8 秒后自动关闭。/ GPS and route views close automatically after about 8 seconds.

## 5. 语音示例 / Voice Examples

| 中文 | English |
| --- | --- |
| “开始记录” | “Start recording” |
| “暂停一下 / 继续记录” | “Pause / Resume recording” |
| “结束本次运动” | “Finish this workout” |
| “现在走了多远？” | “How far have I gone?” |
| “现在有几颗卫星？” | “How many satellites are visible?” |
| “显示 GPS / 看一下轨迹” | “Show GPS / Show my route” |
| “目标 3 公里 / 30 分钟” | “Set a 3 km / 30 minute goal” |
| “帮我打个点” | “Add a mark here” |
| “SD 保存成功了吗？” | “Was the workout saved to SD?” |

语音结果取决于小智模型和角色配置；短句通常更可靠。
Voice results depend on the XiaoZhi model and agent prompt; short commands work best.

## 6. 页面信息 / Screen Guide

运动状态 / Workout state:

- `RDY`：未开始 / Ready
- `REC`：记录中 / Recording
- `PAU`：已暂停 / Paused
- `DONE`：已结束 / Finished

GPS 页 / GPS view:

- `SAT`：定位语句报告的卫星数 / Satellites reported by the fix.
- `DOT`：最近收到、可绘制方位的 GSV 卫星点 / Recent drawable GSV points.
- `HD`：HDOP，通常越低越好 / HDOP; lower is generally better.
- `AGE`：定位数据新鲜度 / Age of the latest fix.
- `GPS OK / FAIR / WAIT / LOST`：定位质量状态 / Fix quality state.

轨迹页 / Route view:

- `DIST / TIME / SPD`：距离、有效时间、GPS 速度 / Distance, active time and GPS speed.
- `S`：起点 / Start.
- `ME`：过滤后路线的最后有效点 / Last valid filtered route point.
- `200m`：视觉参考比例，不是测绘比例尺 / Visual reference, not a survey scale.

## 7. microSD 文件 / Saved Files

正常结束后，文件写入 `/sport/`：
After finishing, files are written to `/sport/`:

| 文件 / File | 用途 / Purpose |
| --- | --- |
| `logNNN.csv` | 结构化运动数据 / Structured workout data |
| `sumNNN.txt` | 本轮摘要 / Workout summary |
| `trkNNN.gpx` | 导入外部地图查看 / Route for external map apps |

按 `E` 后等待 5–15 秒再关机或拔卡。/ Wait 5–15 seconds after pressing `E` before power-off or card removal.

## 8. 局限与安全 / Limits & Safety

- 轨迹页只有过滤后的折线，没有道路或地图底图；最多缓存 96 点。/ The route is a filtered 96-point preview without roads or map tiles.
- 室内、树林和高楼间可能定位漂移。/ GPS may drift indoors, under trees or between buildings.
- 它不是专业运动手表、导航、医疗或救援设备。/ It is not a professional sports watch, navigator, medical or rescue device.
- 当前没有心率、血氧、卡路里、离线地图、IMU 姿态指导或本地唤醒词。/ No heart rate, SpO2, calories, offline maps, IMU coaching or local wake word.
- 小智对话需要网络，AI 回答可能不准确。/ XiaoZhi requires network access and AI answers may be inaccurate.
- 运动和过马路时不要持续看屏幕。/ Do not watch or operate the screen while moving through traffic.

## 9. 快速排查 / Quick Troubleshooting

| 现象 / Issue | 处理 / Action |
| --- | --- |
| `GPS FAIR` | 卫星数量不是唯一条件；到户外等待 HDOP 下降。/ Wait outdoors for a better HDOP. |
| `DOT 0` | 已定位但暂未收到完整 GSV 方位数据。/ A fix may exist before GSV points arrive. |
| `MAP LOW` | 退出页面，避免快速连续按 `G/R`，必要时重启。/ Exit the view, stop rapid `G/R` switching and reboot if needed. |
| 没有 SD 文件 / No files | 等待导出，检查 FAT32、写保护和插卡状态。/ Wait, then check FAT32, write access and card seating. |
| Wi-Fi 循环 / Wi-Fi loop | 使用稳定 2.4GHz 网络并重新启动。/ Use stable 2.4GHz Wi-Fi and restart. |

## 10. 版本 / Release

- Version: `v0.14.8`
- Firmware: `Cardputer-Adv-Sport-v0.14.8.bin`
- Status: Experimental open prototype
- License: Public distribution must follow upstream licenses and service terms.
