# 原型物理与试玩交付

原始游戏运行代码来源：`12f6cb006d7119598e3235f4ca4f7323e4c9d092`。Godot：`4.7.2.stable.official.ed1daf0bf`。依赖源账本：`prototype/godot/source_provenance.json`；适配边界：`prototype/godot/ADAPTATION.md`。

交付包含6个case：3条三段连续反冲链、1条钩索挑战、1对共享几何的主路/奖励路。原生最终见证及独立录像执行都为6/6通过。录像的每条轨迹与最终headless见证帧数相同、逐帧最大位置误差0.0；见`recording-comparison.json`。这是存在一条成功输入的证据，不是人类质量或全状态可达证明。

`modules.mp4`为Godot实际渲染1242帧/60fps、20.7秒连续录像，经ffmpeg转码，没有拼接静图。首次算法产出，无before对照。录制27秒，属于离线Movie Maker，不能作为实时性能指标。原始AVI保留在工作区`modules.avi`；原始运行日志`recording.log`与完整轨迹`recording-results.json`可复查。GPU为Mesa llvmpipe OpenGL4.5软件渲染。

Web包在`web/`，用静态服务器打开index.html；包使用单线程wasm，约196MiB（PCK约158MiB、wasm约38MiB）。这是宽静态依赖闭包的研究构建，包体裁剪和目标设备性能尚未优化。公开部署状态由主交付记录另行核实，localhost检查不冒称公开发布。

最终本地Chromium真实GUI检查：21条状态记录，6个模块均经真实鼠标选择与Replay安全到出口；奖励路额外验证落地访问奖励位置后汇流。A/D实际位移、空格跳跃接受、鼠标左键释放射击接受、Retry重置、E释放钩索的cast/contact接受均实际观察。完整数据`browser-final.json`，截图`browser-replay-0.png`至`browser-replay-5.png`。最终console error与pageerror均为空。浏览器观测`window.__pcgLabState`仅由Godot真实状态写出，不控制玩法。

早期失败保留：可选浏览器录屏缺少Playwright自带ffmpeg，尚未打开页，见`browser-initial-failure.txt`；初次GUI脚本的Playwright参数调用错误见`browser-argument-failure.*`。两个工具问题均已处理；前者用实际原生连续视频交付，后者修正包装器再完整重跑。它们不被改记成玩法通过。

危险检查使用完整24×36身体的保守静态扫掠；没有执行正式荆棘伤害、奖励交易、存档、掉落恢复、动态机关/敌人、真人趣味性与实体设备验收。高路的黄色标记是奖励位置访问，界面明确无奖励交易。视觉为原SVG人物加调试几何，不是区域美术成品。

`physics-delivery-identity.json`固定源、适配器、模块、视频、轨迹、浏览器证据与Web文件的SHA和长度，供最终公开包逐字节核对。
