

# 基于PXI的半物理实时仿真平台使用指南




## 1. 主要内容

- 平台介绍与总览
- 安装（按顺序）
  - Visual Studio 2010 32bit
  - Visual Studio 2010 32bit SP1
  - Matlab2016b
  - VeriStand 2017
  - Labview2017 32bit
  - LabVIEW 2017 FPGA Module Xilinx Compilation Tools for Windows
  - SPI模块
  - FlightGear2016
  - 四旋翼FlightGear模型
  - 测试用例数据库
  - 测试用例软件
  - 激活工具
  - 卸载工具（备用）
- 配置与使用
  - PXI机箱与飞控连接
  - Matlab/Simulink模型介绍与编译
  - Labview2017 项目文件配置使用

    - 安装适用于PXI机箱的软件
    - 仿真平台软件介绍
  - 基本使用流程
  - 硬件接口与技术细节
- 卸载

  - 如何干净地卸载NI全家桶
- 已知问题与解决方法
- 更多功能

## 2. 平台介绍与总览

- 平台在Window7下开发完成

- 可以在Windows10上使用

- 后面的介绍全部基于Windows10操作系统。Windows7同样适用

- 该平台主要包括**PXI仿真计算机**（包含RT端**PXIe-8133**和FPGA端**PXIe-7846R**，本指南是基于这两个型号组合编写的，平台也是基于此开发的）、**飞控**、连接线、以及一台配置好的**PC上位机**。

- 本项目全部文档、软件、项目文件全部存放在文件夹`基于PXI的半物理实时仿真平台`中，其中：

  - 文件夹`软件包`中存放了本平台需要的软件平台安装包，使用本平台需要先安装文件夹中的软件，**本软件包不包含Matlab2016b**。
  - 文件夹`项目文件`中存放本平台使用的项目文件，需要安装`软件包`中的软件后才可以使用

- 文件夹`软件包`中文件关系说明如下，[软件版本兼容性请点此查看](www.ni.com/product-documentation/54028/en/)

  <style type="text/css">
  .tg  {border-collapse:collapse;border-spacing:0;border-color:#aaa;}
  .tg td{font-family:Arial, sans-serif;font-size:14px;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#aaa;color:#333;background-color:#fff;}
  .tg th{font-family:Arial, sans-serif;font-size:14px;font-weight:normal;padding:10px 5px;border-style:solid;border-width:1px;overflow:hidden;word-break:normal;border-color:#aaa;color:#fff;background-color:#f38630;}
  .tg .tg-g6ne{background-color:#FCFBE3;border-color:inherit;text-align:center}
  .tg .tg-s6z2{text-align:center}
  .tg .tg-c3ow{border-color:inherit;text-align:center;vertical-align:top}
  .tg .tg-uys7{border-color:inherit;text-align:center}
  .tg .tg-lyaj{background-color:#FCFBE3;text-align:center}
  </style>
  <table class="tg">
    <tr>
      <th class="tg-c3ow">安装顺序</th>
      <th class="tg-c3ow">软件名</th>
      <th class="tg-c3ow">文件名</th>
      <th class="tg-c3ow">用途</th>
      <th class="tg-c3ow">备注</th>
    </tr>
    <tr>
      <td class="tg-g6ne">1</td>
      <td class="tg-g6ne">Visual Studio 2010 32bit</td>
      <td class="tg-g6ne">VS2010_x86.iso</td>
      <td class="tg-g6ne" rowspan="2">用来编译Simulink模型的工具链</td>
      <td class="tg-g6ne"></td>
    </tr>
    <tr>
      <td class="tg-uys7">2</td>
      <td class="tg-uys7">Visual Studio 2010 32bit SP1</td>
      <td class="tg-uys7">VS2010SP1dvd1.iso</td>
      <td class="tg-uys7"></td>
    </tr>
    <tr>
      <td class="tg-g6ne">3</td>
      <td class="tg-g6ne">Matlab2016b</td>
      <td class="tg-g6ne"></td>
      <td class="tg-g6ne">修改、编译模型</td>
      <td class="tg-g6ne">从实验室网盘获取</td>
    </tr>
    <tr>
      <td class="tg-uys7">4</td>
      <td class="tg-uys7">VeriStand 2017</td>
      <td class="tg-uys7">VeriStand2017.iso</td>
      <td class="tg-uys7">为Matlab/Simulink 提供适用于PXI和Labview的TLC文件<br>Simulink使用该TLC文件编译生成的模型（*.dll）文件<br>才能供Labview以及PXI机箱使用</td>
      <td class="tg-uys7"></td>
    </tr>
    <tr>
      <td class="tg-lyaj">5</td>
      <td class="tg-lyaj">Labview2017 32bit</td>
      <td class="tg-lyaj">LVPLAT2017.iso</td>
      <td class="tg-lyaj">用于运行仿真平台</td>
      <td class="tg-lyaj"></td>
    </tr>
    <tr>
      <td class="tg-s6z2">6</td>
      <td class="tg-s6z2">LabVIEW 2017 FPGA Module<br> Xilinx Compilation Tools for Windows</td>
      <td class="tg-s6z2">2017FPGA-WinVivado2015.4.iso</td>
      <td class="tg-s6z2">Labview FPGA编译工具链</td>
      <td class="tg-s6z2"></td>
    </tr>
    <tr>
      <td class="tg-lyaj">7</td>
      <td class="tg-lyaj">SPI模块</td>
      <td class="tg-lyaj">IEDriver.rar</td>
      <td class="tg-lyaj">NI提供的用于Labview FPGA使用的SPI底层模块</td>
      <td class="tg-lyaj"></td>
    </tr>
    <tr>
      <td class="tg-s6z2">8</td>
      <td class="tg-s6z2">FlightGear2016</td>
      <td class="tg-s6z2">FlightGear-2016.1.2.exe</td>
      <td class="tg-s6z2">可视化软件，仅仅显示功能</td>
      <td class="tg-s6z2"></td>
    </tr>
    <tr>
      <td class="tg-lyaj">9</td>
      <td class="tg-lyaj">四旋翼FlightGear模型</td>
      <td class="tg-lyaj">F450.zip</td>
      <td class="tg-lyaj">四旋翼的模型，用于FlightGear中显示</td>
      <td class="tg-lyaj"></td>
    </tr>
    <tr>
      <td class="tg-s6z2">10</td>
      <td class="tg-s6z2">TestCase数据库</td>
      <td class="tg-s6z2">TestCase数据库安装.zip</td>
      <td class="tg-s6z2">测试用例数据库，用来自动化测试使用</td>
      <td class="tg-s6z2"></td>
    </tr>
    <tr>
      <td class="tg-lyaj">11</td>
      <td class="tg-lyaj">TestCases</td>
      <td class="tg-lyaj">TestCases.zip</td>
      <td class="tg-lyaj">测试用例注入程序</td>
      <td class="tg-lyaj"></td>
    </tr>
    <tr>
      <td class="tg-s6z2">12</td>
      <td class="tg-s6z2">NI License Activator V1.1</td>
      <td class="tg-s6z2">NI License Activator V1.1.exe</td>
      <td class="tg-s6z2">用来激活Labview、VeriStand等NI出品的软件</td>
      <td class="tg-s6z2"></td>
    </tr>
    <tr>
      <td class="tg-lyaj">13</td>
      <td class="tg-lyaj">卸载工具</td>
      <td class="tg-lyaj">卸载工具.rar</td>
      <td class="tg-lyaj">卸载NI软件</td>
      <td class="tg-lyaj">卸载不干净时尝试使用<br>正常请从控制面板卸载</td>
    </tr>
  </table>

- `项目文件`中主要包含SImulink模型文件以及Labview2017项目文件用于运行仿真平台

- 硬件布局如下图（白色机箱就是PXI**仿真计算机**，图中笔记本称之为PC**上位机**）：

  ![1542693580615](assets/仿真平台实物图.png)

- 使用该平台，首先需要将硬件搭建好，效果见上图。硬件的搭建需要将飞控与PXI机箱连接（见第四章）。还应该将PXI机箱与PC机都连接在**同一个局域网中**。软件部分则需要在PC机中安装好对应的软件（见第三章），另外PXI机箱可能也需要通过PC机安装对应的软件（见第四章）。这些在下文中有详细介绍。

- 本指南以**Pixhawk飞控**和**PX4 1.6.5版本固件**为准编写。

## 3. 安装（安装软件过程中请`关闭杀毒软件`）

### 3.1 Visual Studio 2010 32bit

进入文件夹`软件包`找到文件`VS2010_x86.iso`解压后，（**或者用虚拟光驱挂载镜像，下同；WIn10可以直接打开ISO文件,下同**），后进入解压后的文件夹运行其中的`setup.exe`程序，之后按照弹出的界面提示安装。

> - 尽量将所有软件安装在同一个盘符中，比如都放在`C`盘或者放在`D`盘等，否则可能会在编译模型的时候出现找不到文件的问题。
> - 如果有的话，请安装所有可以选择的组件



### 3.2 Visual Studio 2010 32bit SP1

进入文件夹`软件包`找到文件 `VS2010SP1dvd1.iso`解压后，进入解压后的文件夹，运行 `Setup.exe`然后按照提示安装。

> - 尽量将所有软件安装在同一个盘符中，否则使用时可能出错。
> - 如果有的话，请安装所有可以选择的组件。



### 3.3 Matlab2016b

从实验室网盘或者其他位置，找到`Matlab2016b`的安装包，安装即可。

> - 如果是人生第一次安装，请自行网上找教程



### 3.4 VeriStand 2017

进入文件夹 `软件包`找到文件 `VeriStand2017.iso`解压后，进入解压后的文件夹 $\rightarrow$ 进入路径 `\2017\17.0.0\VERISTAND`找到文件 `autorun.exe`运行后，按照下面***图示***的步骤操作即可。

> - 将本软件安装在与`Visual Studio 2010 32bit`相同的盘符中

![VeriStand2017_1](assets/VeriStand2017_1.png)

![VeriStand2017_2](assets/VeriStand2017_2.png)

![VeriStand2017_3](assets/VeriStand2017_3.png)

![VeriStand2017_4](assets/VeriStand2017_4.png)

![VeriStand2017_5](assets/VeriStand2017_5.png)

![VeriStand2017_6](assets/VeriStand2017_6.png)

> **选中上图中所有组件**

![VeriStand2017_7](assets/VeriStand2017_7.png)

![VeriStand2017_8](assets/VeriStand2017_8.png)

![VeriStand2017_9](assets/VeriStand2017_9.png)

![VeriStand2017_10](assets/VeriStand2017_10.png)

![VeriStand2017_11](assets/VeriStand2017_11.png)

![VeriStand2017_12](assets/VeriStand2017_12.png)

![VeriStand2017_13](assets/VeriStand2017_13.png)

![VeriStand2017_14](assets/VeriStand2017_14.png)

![VeriStand2017_15](assets/VeriStand2017_15.png)

![VeriStand2017_16](assets/VeriStand2017_16.png)

![VeriStand2017_17](assets/VeriStand2017_17.png)

重启后完成安装。



### 3.5 Labview2017 32bit

进入文件夹 `软件包`找到文件 `LVPLAT2017.iso`解压后进入解压后的文件夹，找到安装程序 `autorun.exe` 运行后，按照下面***图示***以及***提示***操作即可

![Labview2017_1](assets/Labview2017_1.png)

![Labview2017_2](assets/Labview2017_2.png)

![Labview2017_3](assets/Labview2017_3.png)

![Labview2017_4](assets/Labview2017_4.png)

![Labview2017_5](assets/Labview2017_5.png)

![Labview2017_6](assets/Labview2017_6.png)

在接下来弹出的界面中，选择需要的组件，如下几幅图：

![Labview2017_8](assets/Labview2017_8.png)

![Labview2017_9](assets/Labview2017_9.png)

> 在选择 `FPGA模块`的时候回提示你是否安装依赖的产品，如下图，这里选择 `否`。这里询问的其实是FPGA所需要的编译工具，这个工具稍后我们另行安装。

![Labview2017_9_1](assets/Labview2017_9_1.png)

![Labview2017_10](assets/Labview2017_10.png)

![Labview2017_11](assets/Labview2017_11.png)

![Labview2017_12](assets/Labview2017_12.png)

> 记得勾选上图中的`设备驱动程序`

![Labview2017_13](assets/Labview2017_13.png)

![Labview2017_14](assets/Labview2017_14.png)

![Labview2017_15](assets/Labview2017_15.png)

![Labview2017_16](assets/Labview2017_16.png)

![Labview2017_17](assets/Labview2017_17.png)

> 路径盘符请选择前面软件安装时所使用的盘符，也就是所有软件安装在同一盘符中

![Labview2017_18](assets/Labview2017_18.png)

![Labview2017_19](assets/Labview2017_19.png)

![Labview2017_20](assets/Labview2017_20.png)

![Labview2017_21](assets/Labview2017_21.png)

> 等待安装完成即可。

![Labview2017_22](assets/Labview2017_22.png)

![Labview2017_23](assets/Labview2017_23.png)

![Labview2017_24](assets/Labview2017_24.png)

重启以完成安装。



### 3.6 LabVIEW 2017 FPGA Module Xilinx Compilation Tools for Windows

在文件夹 `软件包`中找到`2017FPGA-WinVivado2015.4.iso`解压后，进入解压后的文件夹，找到`autorun.exe` 运行。之后按照下面**图示**和**提示**操作即可。

![FPGA_1](assets/FPGA_1.png)

![FPGA_2](assets/FPGA_2.png)

![FPGA_3](assets/FPGA_3.png)

![FPGA_4](assets/FPGA_4.png)

![FPGA_5](assets/FPGA_5.png)

![FPGA_6](assets/FPGA_6.png)

![FPGA_7](assets/FPGA_7.png)

![FPGA_8](assets/FPGA_8.png)

![FPGA_9](assets/FPGA_9.png)

![FPGA_10](assets/FPGA_10.png)

完成安装。



### 3.7 SPI模块

**方法一**、在文件夹 `软件包`中找到 `IEDriver.rar` 解压，将解压后的文件夹复制到Labview安装目录中，也就是路径 `.\National Instruments\LabVIEW 2017\vi.lib\` 。复制后的效果如下图：

![SPI_1](assets/SPI_1.png)

> 举例：如果在安装Labview的时候只修改了默认路径的盘符，那么应该复制到这个目录中 `X:\Program Files (x86)\National Instruments\LabVIEW 2017\vi.lib\`，`X`表示Labview的安装盘符。

**方法二**、

> 使用该方法前，请先激活NI所有软件，激活方法参见下文中 `3.12 NI License Activator V1.1`

1. 在开始菜单中找到 `VI Package Manager`打开，如下图：

![SPI_2](assets/SPI_2.png)

2. 稍等片刻

![SPI_3](assets/SPI_3.png)

3. 第一次打开需要等待较长时间。等待其完成刷新列表。

![SPI_4](assets/SPI_4.png)

4. 按照下图所示顺序，操作。

![SPI_5](assets/SPI_5.png)

5. 如果出现图示对话框，按照下图操作：

![SPI_6](assets/SPI_6.png)

6. 又出现下图提示，如图，选择接受。

![SPI_7](assets/SPI_7.png)

7. 之后可能会弹出Labview2017的启动界面，不用理会。等待直到出现下图内容，表示安装完成。

![SPI_8](assets/SPI_8.png)

8. 到这里SPI模块就安装完成了。



### 3.8 FlightGear2016

进入文件夹 `软件包`找到文件 `FlightGear-2016.1.2.exe`双击运行后，按照下面**图示**和**提示**操作即可：

![FlightGear_1](assets/FlightGear_1.png)

![FlightGear_2](assets/FlightGear_2.png)

![FlightGear_3](assets/FlightGear_3.png)

![FlightGear_4](assets/FlightGear_4.png)

![FlightGear_5](assets/FlightGear_5.png)

![FlightGear_6](assets/FlightGear_6.png)

![FlightGear_7](assets/FlightGear_7.png)

![FlightGear_8](assets/FlightGear_8.png)

![FlightGear_9](assets/FlightGear_9.png)

> 安装过程会弹出下图，安装界面点击 `OK`继续安装即可。

![FlightGear_10](assets/FlightGear_10.png)

![FlightGear_10_1](assets/FlightGear_10_1.png)

![FlightGear_11](assets/FlightGear_11.png)

到这里就安装完成了。



### 3.9 四旋翼FlightGear模型

安装完成 `FlightGear`后需要将我们的旋翼无人机模型手动导入，用以显示仿真效果。

进入 文件夹`软件包`找到文件 `F450.zip`将其解压后，放到FlightGear的安装目录中去，具体路径是 `.\FlightGear 2016.1.2\data\Aircraft`

> 举例：比如FlightGear安装在了默认路径中，即 `C:\Program Files\FlightGear 2016.1.2`那么将**解压后**的`F450.zip`即文件夹 `F450`复制到`C:\Program Files\FlightGear 2016.1.2\data\Aircraft`中，复制后的目录结构如下图，请复制后与下图比对，检查路径结构是否与图中一致。
>
> ![FlightGear_12](assets/FlightGear_12.png)

安装好模型后如何启动？可以在电脑桌面上，`右键`$\rightarrow$ `快捷菜单`$\rightarrow$ `新建`$\rightarrow$ `文本文档`，打开新建的文本文档后复制粘贴以下内容：

```bat
C:
cd C:\Program Files\FlightGear 2016.1.2

SET FG_ROOT=C:\Program Files\FlightGear 2016.1.2\data
.\\bin\fgfs --aircraft=F450 --fdm=null --native-fdm=socket,in,30,192.168.199.129,5502,udp --native-ctrls=socket,out,30,192.168.199.129,5505,udp --fog-fastest --disable-clouds --start-date-lat=2017:06:01:21:00:00 --disable-sound --in-air --disable-freeze --airport=KSF0 --runway=10L --altitude=0 --heading=0 --offset-distance=0 --offset-azimuth=0 --timeofday=noon
```

> 代码说明：上面代码中
>
> - 第一行：请将 `C`修改为`FlightGear`软件的安装盘符
> - 第二行：将 `C:\Program Files\FlightGear 2016.1.2`替换为自己的`FlightGear`安装路径，建议安装时使用默认路径，或者只修改盘符，这样第二行代码你只需要修改对应的**盘符**即可
> - 第四行：同样将其中的 `C:\Program Files\FlightGear 2016.1.2`修改为自己的 `FlightGear`的安装路径，如果只是盘符不同，修改**盘符**即可。
> - 第五行以及后面：将第五行以及后面的IP地址（显然一共有两个IP地址）修改为自己电脑所在局域网的IP地址， 即，将**两个**`192.168.199.129` **都修改为自己的局域网IP，这两个一定要相同**，如何查看自己的局域网IP请网上搜索，有很多方法。
> - 全部修改完成后，保存退出。修改文件的后缀名为 `.bat`，然后起一个自己喜欢的名字。双击运行即可。
>
> ![FlightGear_13](assets/FlightGear_13.png)



### 3.10 TestCase数据库

1. 进入文件夹 `软件包`找到文件 `TestCase数据库安装.zip` 后解压，进入解压后的文件夹

![TestCase数据库_1](assets/TestCase数据库_1.png)

2. 进入解压后的文件夹后看到下图中内容，将图中红框中的文件件夹复制到自己喜欢的位置，复制的路径最好不要有中文。复制后，进入该文件夹即 `Navicat for MySQL`内，里面还有一个文件夹也是 `Navicat for MySQL`，进入。也就是路径 `.\Navicat for MySQL\Navicat for MySQL`中，在里面找到程序文件 `navicat.exe`，这个文件就是执行程序，这是一个绿色软件不需要安装，为了方便起见，**在桌面创建一个快捷方式**。

![TestCase数据库_2](assets/TestCase数据库_2.png)

3. 回到文件夹 `TestCase数据库安装`中， 选择下图中红色框中的软件，运行之。

![TestCase数据库_3](assets/TestCase数据库_3.png)

4. 出现下面安装界面，之后按照后面图示操作，

![TestCase数据库_4](assets/TestCase数据库_4.png)

![TestCase数据库_5](assets/TestCase数据库_5.png)

![TestCase数据库_6](assets/TestCase数据库_6.png)

![TestCase数据库_7](assets/TestCase数据库_7.png)

![TestCase数据库_8](assets/TestCase数据库_8.png)

![TestCase数据库_9](assets/TestCase数据库_9.png)

5. 安装过程中会弹出下面对话框，直接选择 `打开`即可。

![TestCase数据库_10](assets/TestCase数据库_10.png)

6. 这里直接点 `Next`。再点击 `Finish`。

![TestCase数据库_11](assets/TestCase数据库_11.png)

![TestCase数据库_12](assets/TestCase数据库_12.png)

7. 安装完成后，回到电脑桌面，找到前面创建的快捷方式，双击运行。

![TestCase数据库_14](assets/TestCase数据库_14.png)

8. 出现下图软件界面，菜单中选择`文件`$\rightarrow$ `新建连接...`如图：

![TestCase数据库_15](assets/TestCase数据库_15.png)

9. 在弹出的界面中，按照下图所示输入图中内容 `localhost`和`3306`，最后点击 `确定`。

![TestCase数据库_16](assets/TestCase数据库_16.png)

10. 如下图，**双击**图示连接 `localhost_3306`，之后，**右键**出现快捷菜单中，选择 `新建数据库...`：

![TestCase数据库_17](assets/TestCase数据库_17.png)

如图：

![TestCase数据库_18](assets/TestCase数据库_18.png)

如图：

![TestCase数据库_19](assets/TestCase数据库_19.png)

11. 在弹出的对话框中，输入下图中所示内容 `sddata`，然后点击 `确定`

![TestCase数据库_20](assets/TestCase数据库_20.png)

12. 然后在==**双击**==新建的数据库 `sddata` ，然后**右键**在快捷菜单中选择 `运行SQL文件...` :

![TestCase数据库_21](assets/TestCase数据库_21.png)

如图：

![TestCase数据库_22](assets/TestCase数据库_22.png)

13. 在弹出的对话框中，点击右侧的按钮（图中红框标出的按钮）

![TestCase数据库_23](assets/TestCase数据库_23.png)

14. 导航到 `软件包` $\rightarrow$ `TestCase数据库安装`，选择文件 `sddata.sql`，然后点击打开，如图所示：

![TestCase数据库_24](assets/TestCase数据库_24.png)

15. 随后回到下图界面，点击 `开始`按钮，

![TestCase数据库_25](assets/TestCase数据库_25.png)

16. 出现下图，进度条走完后，点击关闭。就完成了测试用例数据库的安装。之后关闭该软件。

![TestCase数据库_26](assets/TestCase数据库_26_1.png)



### 3.11 TestCases

进入文件夹 `软件包` 找到文件 `TestCases.zip`。

![TeatCase_1](assets/TeatCase_1.png)

解压后复制到自己喜欢的路径中，路径中最好不要包含中文。依然是绿色软件，不需要安装。复制后，进入文件夹内，找到可执行程序 `testcases.exe`，这就是本软件的执行程序。方便起见，请创建桌面快捷方式。

### 3.12 NI License Activator V1.1

在文件夹 `软件包`中找到 `NI License Activator V1.1.exe`，右键以管理员身份运行，出现

![激活_1](assets/激活_1.png)

将鼠标放在需要激活的软件名字前，右键。如下图：

![激活_2](assets/激活_2.png)

![激活_3](assets/激活_3.png)

选择 `Active`完成激活。之后将所有软件按照这个方法激活，完成后如下图：

![激活_4](assets/激活_4.png)

关闭软件完成激活。

> 卸载这些软件前先使用激活工具反激活，和激活操作相同。



### 3.13 卸载工具

在文件夹 `软件包`中找到 `卸载工具.rar`解压，进入解压后的文件夹，里面就是卸载工具。具体用法和说明请看下文中 `5. 卸载`。



## 4. 配置与使用

### 4.1 PXI机箱与飞控接口

本节内容暂时只针对四旋翼X型布局介绍

使用到的PXI机箱上接口以及作用见下表

|    接口     |               用途                |
| :---------: | :-------------------------------: |
|   PWM输入   |   接收来自飞控的PWM电机控制信号   |
|     SPI     | 飞控与PXI机箱进行传感器数据的通信 |
|     CS      |       模拟传感器的片选引脚        |
| GPS（UART） |       向飞控发送GPS原始数据       |
|   PPM输出   |    PXI向飞控发送遥控器PPM信号     |
|   PPM输入   |    接收来自遥控接收机的PPM信号    |

下面是具体的介绍：

1. **PWM输入（电机接口）**

   本仿真平台所用的Simulink模型以及Pixhawk全部按照下面图示电机序号统一设置，这也是一种通用的设置方案：

   ![四旋翼Pixhawk连接图1](assets/四旋翼Pixhawk连接图1.jpg)

   PXI机箱引出的四条PWM信号输入线（用于接收飞控发出的电机驱动信号）线序是

   | 线序 | 含义 | 电平  |
   | :--: | :--: | :---: |
   |  1   | PWM1 | +3.3V |
   |  2   | PWM2 | +3.3V |
   |  3   | PWM3 | +3.3V |
   |  4   | PWM4 | +3.3V |

   对应的飞控Pixhawk上顺序如下图：

   ![四旋翼Pixhawk连接图2](assets/四旋翼Pixhawk连接图2.jpg)

   上图中**彩色箭头**标出的1、2、3、4 信号接口分别对应PXI机箱的PWM1、PWM2、PWM3、PWM4四条线。将他们对应连接即可。需要注意的是上图中从上数，第一排针脚是GND，第二排是VCC，第三排是信号，对于PWM自然就是PWM输出信号。

   > - **PXI机箱上的PWM四条信号线上在接口处标有序号**

2. **SPI（传感器通信接口）**

   这部分分为两部分：

   - SPI接口
   - 传感器片选CS接口

   PXI机箱：

   机箱上的SPI接口共有四根线，线序和意义如下

   | 线序 |   含义    | 电平  |
   | :--: | :-------: | :---: |
   |  1   |    SCL    | +3.3V |
   |  2   | MISO(OUT) | +3.3V |
   |  3   | MOSI(IN)  | +3.3V |
   |  4   |    GND    | +3.3V |

   > **注：PXI一侧为SPI从机**

   机箱上的CS接口共有四根线，线序和对应的传感器如下

   | 线序 |  含义   | 电平  |          备注          |
   | :--: | :-----: | :---: | :--------------------: |
   |  1   | LSM303D | +3.3V | 磁力计和加速度计、温度 |
   |  2   | MS5611  | +3.3V |      气压计、温度      |
   |  3   | MPU6000 | +3.3V | 加速度计和陀螺仪、温度 |
   |  4   | L3GD20  | +3.3V |      陀螺仪、温度      |

   Pixhawk：

   对于新的飞控板需要将自有传感器取下，将**SPI**线和**CS**线引出，然后按照前面所述对应连接即可。如果手里已有做好接口的飞控，那么接口处应该标出了对应线序，按照接口处的标记连接即可。也可以做成防反插类型接口。

   > **注：SPI不同于串口，SPI通信是自身MOSI引脚与对方MOSI引脚连接，自身MISO引脚与对方MISO引脚连接，SCK引脚与SCK引脚连接**
   >
   > **串口则是，自身RX引脚与对方TX引脚连接，自身TX引脚与对方RX引脚连接**

3. **GPS串口**

   PXI机箱的GPS（串口）接口线序以及含义如下：

   | 线序 |  含义   | 电平  |
   | :--: | :-----: | :---: |
   |  1   | RX(IN)  | +3.3V |
   |  2   | TX(OUT) | +3.3V |
   |  3   |   GND   |  GND  |

   Pixhawk上的GPS接口按照其外壳上的标注连接，如下图红框所选就是GPS接口，红点一侧为1号引脚，每个引脚含义下表列出：

   ![Pixhawk正面](assets/Pixhawk正面.jpg)

   | 序号 |       含义        | 电平  |
   | :--: | :---------------: | :---: |
   |  1   |  VCC（没有用到）  |  +5V  |
   |  2   |      TX(OUT)      | +3.3V |
   |  3   |      RX(IN)       | +3.3V |
   |  4   | CAN2 TX(没有用到) | +3.3V |
   |  5   | CAN2 RX(没有用到) | +3.3V |
   |  6   |        GND        |  GND  |

   根据以上说明连接飞控与PXI机箱即可。如果已有做好接线的飞控，请按照接线接口处的标识连接。

4. **PPM输出**

   > 此接口是用来做接收机故障测试时使用的，如果不做这方面的测试，可以将遥控接收机信号线直接连接到飞控上，无需使用该接口。

   该接口只有两根线（口），一个是地线，一个是信号线，这里的信号线用来发送PPM信号给飞控。根据接口具体情况，将该接口与飞控上对应的RC口连接即可。对于Pixhawk如下图，位于红框位置，从上向下三个针脚分别是 GND、+5V、PPM。将接口与对应的PXI机箱上的PPM输出接口连接即可。**机箱上的PPM接口有响应的标记。**

   ![RCin](assets/RCin.jpg)

5. **PPM输入**

   > 同样，如果不是使用接收机故障测试功能，不需要使用该接口，直接将接收机与飞控连接即可。

   该接口只有两根线（口），一个是地线，一个是信号线。这里的信号线用来接收来自接收机发出的PPM信号。具体接收机上的PPM信号接口，一般需要转接模块转换才能得到PPM信号，转接模块上清楚地标出PPM信号针脚的位置。请具体查看转接模块上标记。

这里给出连接实物图，后期看到的可能与本图有出入，以实物为准。

![PXI与飞控连接实物图](assets/PXI与飞控连接实物图.jpg)

![PXI与飞控连接实物图_2](assets/PXI与飞控连接实物图_2.jpg)




### 4.2 Matlab/Simulink模型介绍与编译

下面介绍Simulink模型编译。

首先，`项目文件`中存放了我们需要的Simulink模型。Simulink模型共三个（在其中两个压缩包中 `MulticopterModel.zip`，`FlightGearPackaging.zip`）：

- 多旋翼模型（核心）位于 `MulticopterModel.zip`中；
- 执行校准模型（用来模拟多旋翼的校准过程，使得飞控可以通过校准流程）位于 `MulticopterModel.zip`中；
- FlightGear显示数据打包模型（用来将需要发送给FlightGear的数据打包）位于 `FlightGearPackaging.zip`中。

编译原理：

- 利用Simulink生成代码的功能，Simulink会将我们提供的模型编译生成适用于Labview的代码（需要VeriStand2017提供支持，已经安装）；
- 调用VS2010提供的编译工具链，将生成的代码编译成 `*.dll`文件。

上面两条都是Simulink自动完成的，过程不需要人为干预。生成的 `*.dll`文件才可以由Labview调用（如何调用见下一节）。本节介绍如何编译模型最后生成 `*.dll`文件。

1. 进入文件夹 `项目文件`里面有三个压缩包，如下图。找到图中标出的文件，将其复制到另外的地方（路径中不要有中文名）。

   ![Simulink_1](assets/Simulink_1.png)

2. 将复制后的两个压缩包，**分别解压缩到不同的文件夹中**，操作类似下图：

   ![Simulink_2](assets/Simulink_2.png)

3. 解压后， 先进入文件夹`MulticopterModel`，如下图，可以看到里面有两个 `.slx`的模型文件，这两个文件就是我们需要的模型：

   ![Simulink_3](assets/Simulink_3.png)

   > - 文件 `Init.m`是模型默认参数配置文件
   >
   > - 文件 `MavLinkStruct.mat`是模型总线定义文件

4. 首先用**Matlab2016b**打开文件 `Multicopter_vPC.slx`（多旋翼模型），

   > 打开Matlab2016b时，等待初始化完成后，应该看到下图中的两行内容，说明Matlab2016b已经成功加载VeriStand2017的支持文件：
   >
   > ![Simulink_4](assets/Simulink_4.png)

   请将Matlab工作文件夹导航到打开的模型所在的文件夹，如下图：

   ![Simulink_5](assets/Simulink_5.png)

5. 视线转移到打开的模型中，编译前请确认几点注意事项（提供的模型默认情况下，可以直接编译），见下图

   ![Simulink_6](assets/Simulink_6.png)

   之后点开下图中的设置按钮

   ![Simulink_7](assets/Simulink_7.png)

   在弹出的设置窗口中，选择左侧的 `solver`，然后确认右侧的内容与下图标红的内容是一致的。

   ![Simulink_8](assets/Simulink_8.png)

   下图同理，确认设置内容与下图相同：

   ![Simulink_9](assets/Simulink_9.png)

   确认设置内容与下图相同，这里是要确保生成模型文件参数是可调的：

   ![Simulink_10](assets/Simulink_10.png)

   下图中`NIVeriStand.tlc`就是前面提到的，VeriStand2017支持文件。确认图中标记处与设置相同

   ![Simulink_11](assets/Simulink_11.png)

   确认设置内容与下图一致。

   ![Simulink_12](assets/Simulink_12.png)

   确认无误后，点击 `OK`完成退出。

   ![Simulink_13](assets/Simulink_13.png)

6. 然后编译：点击下图中所示按钮，编译模型。

   ![Simulink_14](assets/Simulink_14.png)

   可以点开模型下面的蓝色提示查看编译进度，如下图

   ![Simulink_15](assets/Simulink_15.png)

   下图中就是编译进度：

   > 如果编译失败，其中的错误也会在里面显示，可以根据错误细节解决问题

   ![Simulink_16](assets/Simulink_16.png)

   编译完成后，会弹出编译报告（也可以在设置中关闭，建议开启）

   ![Simulink_17](assets/Simulink_17.png)

   关闭报告后，查看Maltab资源管理器中出现了新生成的文件夹，如下图，里面就包含了生成的 `*.dll`文件,双击进入该文件夹：

   ![Simulink_18](assets/Simulink_18.png)

   下图中标出的就是生成的模型

   ![Simulink_19](assets/Simulink_19.png)

7. 回到上一级目录，找到另外一个模型文件 `Eular2IMU.slx` （执行校准模型），如下图，执行类似上面的操作，编译生成模型

   ![Simulink_20](assets/Simulink_20.png)

   ![Simulink_21](assets/Simulink_21.png)

   ![Simulink_22](assets/Simulink_22.png)

   ![Simulink_23](assets/Simulink_23.png)

8. 然后在进入之前解压的另外一个文件夹 `FlightGearPackaging`。如下图：

   ![Simulink_24](assets/Simulink_24.png)

   类似的，检查模型设置，需要的注意的是这个模型（FlightGear显示数据打包模型）的步长是`0.01`

   ![Simulink_25](assets/Simulink_25.png)

   ![Simulink_26](assets/Simulink_26.png)

   点击编译：

   ![Simulink_27](assets/Simulink_27.png)

   编译成功后，依然是在生成的文件夹中（见下图）找到对应的`.dll`文件。

   ![Simulink_28](assets/Simulink_28.png)

   至此，三个模型都已经编译完成。

   > 模型的仿真步长实际是可以修改的：
   >
   > - 仿真步长过短，仿真平台无法按照指定时间完成。仿真平台执行一次模型所需的时间与该平台CPU运算能力有关。按照模型默认设置的步长，设定的周期是200us，仿真平台测试的可以达到的最短周期在100us以上。所以默认使用的仿真步长是0.0002s。
   > - 对于**FlightGear显示数据打包模型**的步长不建议设置太短，会增加仿真平台的负担，对于单纯的显示功能也没有必要。建议不要小于0.01



### 4.3 Labview2017 项目文件配置使用

#### 4.3.1 安装适用于PXI机箱的软件

在开始使用平台进行仿真之前，需要为PXI机箱安装软件。可能已经提前安装好了，就不需要安装了。

- **用网线将PXI机箱与局域网连接，这里需要用到PXI机箱上的1号网口（机箱上有标记，一看便知），将网线插入即可，打开PXI机箱电源**，稍等片刻，等它启动完成。
- 在之后的使用过程中，都要保持PXI机箱处于局域网中。

首先到开始菜单中找到下图中的软件 `NI MAX`：打开

![HIL_1](assets/HIL_1.png)

![HIL_2](assets/HIL_2.png)

打开软件后，点开远程系统。检索过后，就会出现，目标机箱

![HIL_3](assets/HIL_3.png)

> 如果打开软件之后，没有出现上图中 `远程系统`那么可以尝试如下操作： `工具`  $\rightarrow$  `重置配置数据`
>
> ![HIL_4](assets/HIL_4.png)
>
> 然后会出现要求重启等，对话框。按照提示操作即可。重启后再次打开该软件，问题应该可以得到修复。

> 有时点开 `远程系统`后，并没有出现目标机箱，或者 `远程系统`下面什么都没有。这通常是防火墙造成的问题。如有，按照下面的方法解决。
>
> 如下图，选择远程系统后，到右侧上点击 `故障排查远程系统发现`：
>
> ![HIL_5](assets/HIL_5.png)
>
> 然后会出现下图，设置成下图所示的选项，点击下一步：
>
> ![HIL_6](assets/HIL_6.png)
>
> 由于使用的是2017版本，所以按照下图选择Labview2017，之后点击下一步：
>
> ![HIL_7](assets/HIL_7.png)
>
> 然后会看到下图，图中也显示该软件被防火墙阻挡，点击图中的 `Add Rules`添加规则，然后会弹出用户账户控制询问是否通过防火墙，选择是即可（其他时间弹出的对话框同样要选择是，不然会被防火墙阻挡，出现问题）
>
> ![HIL_8](assets/HIL_8.png)
>
> 允许通过防火墙后，变成下图的样子，点击下一步：
>
> ![HIL_9](assets/HIL_9.png)
>
> 接着会自动搜索，搜索完成后会出现下图的目标终端，如下图，然后点击下一步，之后就可以在远程系统下看到目标终端了，也就是我们的仿真计算机。
>
> ![HIL_10](assets/HIL_10.png)

下图中是搜索到的仿真计算机，如下图。点击左侧红色框中远程（局域网）计算机，看到右侧有机箱在局域网中的IP地址等信息。

![HIL_11](assets/HIL_11.png)

之后点开远程计算机，选择`软件`右键选择`添加删除软件`，

![HIL_12](assets/HIL_12.png)

在弹出的界面中，选择要安装的软件（**软件列表名字前面小图标上单击，可看到安装选项，选择安装即可**），除了下图中标出的软件不选，其他的全部选择安装，之后点击下一步

> 如果你完全熟悉这些软件的用途，也可以只选择必要的软件安装。

![HIL_13](assets/HIL_13.png)

再次点击下一步：

![HIL_14](assets/HIL_14.png)

等待安装完成：

![HIL_15](assets/HIL_15.png)

![HIL_16](assets/HIL_16.png)

点击完成后，退回到软件主界面，按照下图标记步骤操作，点击保存后确认是否重启，选择是：

![HIL_17](assets/HIL_17.png)

![HIL_18](assets/HIL_18.png)

等待重启完成，至此机箱内的软件安装完成。完成后将`NI MAX`关闭即可。



#### 4.3.2 仿真平台软件介绍

进入文件夹 `项目文件`，找到 `HIL on PXI.zip`，如下图：

![HIL_19](assets/HIL_19.png)

将其复制到其他路径中，**路径中不要有中文名**，解压

![HIL_20](assets/HIL_20.png)

进入解压后的文件夹，找到下图中的 `HIL on PXI.lvproj`,双击打开：

![HIL_21](assets/HIL_21.png)

打开过程中，出现需要确认的对话框一律点确认通过（用户账户控制、防火墙等），打开后出现下图所示，**项目浏览器**，并按照下图所示，打开 `属性`：

![HIL_22](assets/HIL_22.png)

打开后，单击窗口左侧 `常规`。，然后确认窗口右侧的IP地址是目前PXI机箱在当前局域网中的地址，确认之后点确定关闭即可。

> PXI机箱在局域网中的地址，在上文 `4.3.1 安装适用于PXI机箱的软件 `中有介绍。

![HIL_23](assets/HIL_23.png)

接着，按照下图打开 `FPGA终端`的 `属性`：

![HIL_24](assets/HIL_24.png)

在刚打开的窗口左侧单击 `常规`，确认窗口右侧 `资源`名称与实际是对应的。如果有疑问请继续往下看：

![HIL_25](assets/HIL_25.png)

接着上图，如何查看上图中 `资源`一项的内容？如下图，打开 `NI MAX`软件（不知道从哪里找这个软件请看前文）按照下图指示操作，就可以看到上图中 `资源`一栏需要填写的内容。

![HIL_26](assets/HIL_26.png)

回到项目浏览器中，按照下图操作：

![HIL_27](assets/HIL_27.png)

下图，这里打开的就是FPGA中用来模拟传感器、串口、PWM、PPM的程序。按照下图点击运行，尝试运行（确认此时机箱已经打开，并且正确接入局域网中）

![HIL_28](assets/HIL_28.png)

这时通常需要重新编译一次，期间弹出的任何对话框，都要点击确认或者保存（总之不要点取消）。

![HIL_29](assets/HIL_29.png)

![HIL_30](assets/HIL_30.png)

最后会进入编译界面，编译时间会比较长至少10分钟。

![HIL_31](assets/HIL_31.png)

编译完成后，之前的程序框图会自动弹出，并自动运行，如下图：

![HIL_32](assets/HIL_32.png)

单机下图中的红色按钮，停止运行。然后关闭该程序。

> 该FPGA程序，实际使用中不需要直接操作，而是通过其他VI程序调用实现的，这里只是确认该程序是否需要重新编译，且可以运行。

![HIL_33](assets/HIL_33.png)

再将刚才的编译窗口关闭，如下图：

![HIL_34](assets/HIL_34.png)

接下来要介绍运行仿真平台的主程序。但是在这之前，我们需要将之前编译好的三个Simulink模型（见上文中 `4.2 Matlab/Simulink模型介绍与编译`）也就是 `*.dll`文件，存放到正确的位置。如下图，打开 `NI MAX`软件，按照下图打开 `文件传输`：

![HIL_34_1](assets/HIL_34_1.png)

在刚打开的文件夹中，进入文件夹 `ni-rt`，如下图：

![HIL_34_2](assets/HIL_34_2.png)

将`4.2节`中编译好的三个模型文件复制到这个文件夹中，复制完成后关闭即可，如下图：

![HIL_34_3](assets/HIL_34_3.png)

放置好模型文件后，视线回到项目浏览器中，双击打开下图中所示文件，这个就是整个仿真平台的 **主程序**：

> **主程序**的名字、版本在后面可能会有变化，请以实际为准。后面会起一个一看便知的文件名。

![HIL_35](assets/HIL_35.png)

打开后就看到下图中的程序主界面，单机下图中红框标记的运行按钮（白色的箭头）。运行

![HIL_36](assets/HIL_36.png)

第一次点击运行后，可能会弹出很多对话框，一律点确定一类的按钮，如下图

> 由于这是用来开发的项目，Labview会检测到一些变化，然后提示是否保存。实际上并没有什么变化，所以一律点保存或者确定等。弹出的对话框可能千遍万化，这里不能穷举。

![HIL_37](assets/HIL_37.png)



![HIL_38](assets/HIL_38.png)



![HIL_39](assets/HIL_39.png)

最后就可以看到运行中的仿真平台主程序了，如下图：

> 主程序布局后期会有变化，请以实际为准。

![HIL_40](assets/HIL_40.png)

**熟悉主界面之后**，先停止该程序，见下图，之后关闭程序文件。

![HIL_41](assets/HIL_41.png)

到这里，整个仿真平台的安装配置简单运行已经通过，接下来就是具体的使用方法了。



### 4.4 基本使用流程

**阅读本章需要熟悉前面所有章节内容**

本仿真平台用途，主要分为两类：**常规测试**和**故障测试**。故障测试分为两种，一种是**手动故障测试**，另一种是**自动化故障测试**。

1. 常规测试：

   准备工作：

   - 确认**飞控**与PXI**仿真计算机**已经连接完好。
   - 确认PXI仿真计算机和PC上位机接入**同一局域网中**
   - 确认PC上位机，PXI仿真计算机**软件都已配置完好**。

   第一步：打开仿真计算机电源，等待其启动完成，（类似于PC开机时间）；

   第二步：确认模型文件 `*.dll`已经放置在仿真计算机中正确的位置；

   第三步：打开FlightGear；

   第四步：打开PC上位机上的Labview项目，即打开项目文件 `HIL on PXI.lvproj`出现**项目浏览器**窗口；

   ![基本流程_2](assets/基本流程_2.png)

   第五步：在**项目浏览器**中打开仿真平台**主程序**，并点击**运行按钮**运行仿真程序；

   第六步：接通飞控电源，等待10s左右的的时间，观察仿真平台**主程序**主界面上的传感器工作状态指示灯是否全部**闪烁**或者**接近常亮**。如果某几个传感器出现不闪烁的状态，说明飞控与仿真计算机建立连接失败，这时请断开飞控电源，重新上电。如果反复出现该问题，请检查连线；

   > 事实上，飞控每向仿真计算机发送一字节数据，指示灯都会闪烁一下，如果数据量很大就会接近常亮。如下图：
   >
   > ![基本流程_1](assets/基本流程_1.png)

   第七步：操作飞控安全开关，用遥控器解锁，或者安装地面站（地面站安装不做介绍，网上有教程），设置飞行任务等常规操作。可以在FlightGear中看到飞行状态。

   > 执行第七步时就像正常操作真机飞控一样操作即可。包括但不限于，手动模式、定点、任务等。

2. 手动故障测试：

   准备工作以及第一步至第六步与**常规测试**相同。这里省略。需要遥控器。

   第七步：解锁，启动飞控，使用遥控起飞（可以切换为定点定高模式等）

   第八步：打开`TestCases`软件，如下图，按照图中说明操作即可将故障注入到模型中，在FlightGear中可以看到效果。图中注入的是螺旋桨的故障，也可以注入其他的故障。

   ![基本流程_3](assets/基本流程_3.png)

3. 自动化故障测试：

   准备工作以及第一步至第六步与**常规测试**相同。**但是需要注意的是，请在接通飞控电源前连接数传**。数传提前配对好，一边接PC上位机，一边接飞控。不需要遥控器

   第七步：打开软件 `WampServer64`如下图，也可以从开始菜单找到该程序，打开后在后台运行：

   ![基本流程_4](assets/基本流程_4.png)

   第八步：打开`TestCases`软件，按照图中标注操作

   ![基本流程_5](assets/基本流程_5.png)

   弹出新的窗口中，单击开始即可开始自动化测试，测试用例全部测试完成后，可以点击窗口右下侧 `生成报表`以生成Word报告。后面按照弹出的对话框提示操作即可。

   ![基本流程_6](assets/基本流程_6.png)

   生成的报告在TestCases软件（不是桌面快捷方式）目录下的 `outputReport`文件夹中，可参考下图：

   ![基本流程_7](assets/基本流程_7.png)


### 4.5 硬件接口与技术细节




## 5. 卸载

Labview软件套件内容庞大，容易卸载不干净，导致无法重新安装，严重的导致重装系统。

0. 先使用激活工具`NI License Activator V1.1`反激活所有激活的软件

1. 使用软件自身卸载程序卸载

   打开`控制面板`$\rightarrow$`程序和功能` 

   ![1](assets/1.png)

   双击上图中红色框中的项目，稍等片刻，出现下图内容：

   ![2](assets/2.png)

   选择上图中红色框中的`删除全部`。

   > 注：如果提示确认是否删除，选择确认即可。

   ![3](assets/3.png)

   接着出现上图内容，需要等待很久的时间。**不管提示与否，卸载完成后请重启。**

   ![4](assets/4.png)

   如果遇到无法再次安装Labview组件的问题，可以尝试运行`软件包`中的如下软件，具体位置详见 `3.13 卸载工具`一节：

   ![5](assets/5.png)

   > 注：这个软件在Windows7下成功使用过，但是有时会出现点击`是`之后无反应的情况。所以这个方法作为最后尝试。如果点击是后有反应，那么尝试再次卸载全部内容。Windows10测试时是没有反应的。

## 6. 已知问题与解决方法

1. 如果需要重新安装测试用例数据库，那么在卸载软件 `WampServer64`后，请**重启电脑**后再安装。否则数据库卸载不干净，那么在重新加载数据库文件 `sddata.sql`时，可能会报错,**如下图**，出现测试用例软件不显示测试用例的问题。

![TestCase数据库_26](assets/TestCase数据库_26.png)

## 7. 更多功能

