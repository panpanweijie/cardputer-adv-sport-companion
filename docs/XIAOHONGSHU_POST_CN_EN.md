# 小红书发布文案 / Social Post

## 标题 / Title

**我把小智装进 Cardputer，做了一个会聊天的运动搭子**
**I built a tiny AI sport companion with Cardputer-Adv**

## 中文正文

最近做了一个 Cardputer-Adv 小智运动陪伴原型。一个人跑步、骑行、徒步时，可以直接和小智聊天，也可以说“开始记录”“走了多远”“现在有几颗卫星”。

目前 v0.14.8 支持：

- 语音或按键开始、暂停、继续、结束
- 查看卫星数、HDOP 和 GPS 状态
- 显示本次距离、时间、速度和简易轨迹
- 设置距离或时间目标、记录打点
- 结束后在 microSD 保存 CSV、TXT 摘要和 GPX

按键很直接：`S` 开始/暂停，`M` 打点，`E` 结束，`G` 看 GPS，`R` 看轨迹，`Enter` 和小智对话。

它还是实验性原型：轨迹只是过滤后的折线示意，没有道路底图，也不是专业运动手表、导航或救援设备。更适合 M5Stack、ESP32、小智和 AI 硬件爱好者体验及二次开发。

## English

I built a small AI sport companion with Cardputer-Adv and XiaoZhi. During a run, ride or hike, you can chat with it or ask it to start recording, report distance and check GPS satellites.

Version v0.14.8 supports:

- Voice or key control for start, pause, resume and finish
- Satellite count, HDOP and GPS status
- Distance, time, speed and a simple route preview
- Distance/time goals and manual marks
- CSV, TXT summary and GPX export to microSD

Keys: `S` start/pause, `M` mark, `E` finish, `G` GPS, `R` route and `Enter` for XiaoZhi chat.

This is an experimental prototype. The route is only a filtered visual preview without road maps. It is not a professional sports watch, navigator or rescue device, but it is a fun platform for M5Stack, ESP32 and AI hardware experiments.

## 标签 / Tags

#M5Stack #Cardputer #ESP32 #小智AI #AIHardware #OpenSourceHardware #GPS #跑步 #骑行 #徒步 #SportTech
