# 研究试玩包的闭包导出

正式游戏物理、输入、资源、视觉源代码与素材均未修改；原`delivery/web`完整保留。

首轮仅选main场景，得到657,724字节PCK，但真实Web缺玩家场景、类型和字体，启动失败。这说明不能把Godot scene-only的导出选择当作已证明的脚本/动态资源闭包。失败包保留在`web-lean-first-failed`，失败日志另存。

第二轮显式选入所有原始脚本、Scene、Resource、shader，扫描所有literal preload操作数及tscn/tres ext_resource，再保留原JSON/shader include。选集见`prototype/godot/lean-export-closure.json`，新增preset为`Web Lean`，不删除源文件，也不更改导入资产或core。该做法保守保留了仍可能被类型/静态预加载引用的资源，减少的是未选入的研究场景不消费的资产集合。

最终PCK为68,067,452字节（64.914MiB），全部Web顶层文件107,916,843字节（102.918MiB）。WASM和JS与原包字节完全一致。发布身份以`lean-export-report.json`逐文件SHA/长度为准。

真实Chromium重新验证21条状态，6个模块均经鼠标选择和Replay成功；手动A/D、跳跃、射击、真实钩点cast/contact、Retry通过，console/pageerror为空。6条回放动作计数和结束帧与原包相同；5条出口坐标完全一致，第0条观察到0.000193wu浮点差异，仍安全到出口。原生录像与headless的逐帧0误差证据仍属于原验证环境，不被改签为浏览器逐帧一致。

重验初次包装器在鼠标Retry后固定等待120ms，读到旧状态而失败，下一次读数已是正确reset状态；原件保留于`lean-verification-retry-race`。包装器改为等待真实reset状态，使用原10秒UI等待预算，随后从头完整通过；没有修改游戏代码或物理门槛。

此闭包只对研究原型实际6模块、当前手动/回放消费者及测试过的输入成立，不代表完整游戏所有地区、任意装备或未来动态加载均可使用该裁剪包。
