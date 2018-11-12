关于 CWS
========
CWS 是一个实验项目，用于学习 Wi-Fi 探针相关技术，espressif 的 ESP8266/NoneOS 和 ESP32/IDF，以及基于这两个平台的 NodeMCU。主探针模块来自于 DOIT。

硬件设计
-------
探针产品已经相对成熟，例如我们使用的来自于 DOIT 的模块 ESP-F，基于 espressif 的 ESP8266EX，采集的效果相当不错，并且提供一定的配置项。

我们希望由 DOIT 探针完成主要采集工作，可以通过 UART 传出采集到的数据，并接收配置项（AT 指令）。

我们仍然需要一些其他的采集辅助功能、数据上送功能和灵活的远程管理功能，所以我们使用了第二块 ESP8266EX 模块，并使用了 NodeMCU 固件。

但是 ESP8266EX 只有一个双向 UART，如果两个模块通过 UART 相连，就没有办法方便地对设备进行方便地二次开发。

为此，我们使用了一颗 STM32 103，通过 micro USB 暴露出一个 CDC 接口，并获取电源。而两个 ESP8266EX 模块的 UART 都接在了 103 上。最为一个串口路由器，103 实现以下功能：

* 在 CDC 和 NodeMCU 之间透传所有数据

* 监听来自 CDC 和 NodeMCU 的 AT 指令，并把属于 DOIT 模块的 AT 指令转发给 DOIT 模块

* 将来自于 DOIT 模块的数据转发给 NodeMCU，并提供一个额外的 AT 指令用于 开始/停止 数据转发

固件设计
-------
介绍。

应用逻辑
-------
介绍。

.. toctree::
   :caption:TABLE OF CONTENTS

   快速入门 <get-started/index>
   快速入门 (CMake 预览版本) <get-started-cmake/index>
   API 参考 <api-reference/index>
   H/W 参考 <hw-reference/index>
   API 指南 <api-guides/index>
   贡献代码 <contribute/index>
   版本 <versions>
   相关资源 <resources>
   版权 <COPYRIGHT>
   关于 <about>
