# RAN 结构

## 5GC 到 RAN侧

在5G RAN架构中，BBU功能分为两个功能单元：负责处理对实时性较高的分布式单元（DU），以及负责处理非实时，RRC，PDCP等高层协议的中央单元（CU）。

在5G C-RAN中，DU的服务器和相关软件可以托管在站点本身，也可以托管在边缘云（数据中心或中央办公室）中，具体取决于传输的可用性和前传接口。CU的服务器和相关软件可以与DU放在同一位置，也可以托管在区域云数据中心中。DU和RU之间的实际划分可能会根据具体的用例和实现而有所不同。

![O-RAN](https://pic4.zhimg.com/80/v2-bea53891209082f4721c36e6321f4bdb_720w.webp)

RU：一个负责处理DFE和部分PHY层功能的无线电单元，其设计的关键考虑因素是尺寸、重量和功耗。

DU：靠近RU的分布式单元，主要处理RLC、MAC和部分PHY层功能。该逻辑节点包括eNB/gNB功能的子集，具体取决于功能拆分选项，其操作由CU控制。

CU：负责处理RRC、PDCP等高层协议的中央单元。gNB由一个CU和一个DU组成，分别通过CP和UP的Fs-C和Fs-U接口连接到CU。具有多个DU的CU将支持多个gNB。分离架构使5G网络能够根据中传可用性和网络设计，在CU和DU之间利用不同的协议栈分布。CU可以通过中传接口对多个DU进行集中式管理。

4G / 5G核心通过回传（Backhaul）连接到CU，5G核心距离CU最多可以200公里。

![5GC--gNB](https://pic3.zhimg.com/v2-6095fa97483e738b7c7766fd1f52013e_r.jpg)

## D-RAN

基站一般可分为三部分：BBU（基带处理单元）、RRU（射频拉远单元）和天线。

![D-RAN](https://img-blog.csdnimg.cn/20201012234758910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTYyOTg0OA==,size_16,color_FFFFFF,t_70#pic_center)

## C-RAN

1. RRU 拉远：
RRU拉远是根据建网需求在某地建站时不再在站址建设BBU机房，而是通过附近其他站点（信源站点）机房拉出光纤到本站的方式组网。这是对D-RAN改造最少的方式，兼顾了成本和效率，技术上也较成熟。
![RRU拉远](https://img-blog.csdnimg.cn/20201020113156565.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTYyOTg0OA==,size_16,color_FFFFFF,t_70#pic_center)
2. BBU 集中化
BBU集中是RRU拉远的进一步演进，更加强调BBU的集中部署。中心机房将部署更多的BBU，形成BBU池，可以支持更多站点。
![BBU集中](https://img-blog.csdnimg.cn/20201020115022864.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTYyOTg0OA==,size_16,color_FFFFFF,t_70#pic_center)
3. BBU虚拟化
BBU虚拟化意味着不需要专用的BBU基带处理单元，使用通用服务器就可以虚拟出BBU来完成大部分的BBU日常功能处理。这种虚拟化的方式简化了网络管理，并使得资源池和无线资源得到了有效协调。
![BBU虚拟化](https://img-blog.csdnimg.cn/20201020120312804.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80MTYyOTg0OA==,size_16,color_FFFFFF,t_70#pic_center)

CU：集中单元，非实时的慢速处理模块（比如切换、RRC连接管理），Non Realtime；这个模块有可能进行集中云化。
DU：分布单元，实时的快速处理模块（比如编解码、快速调度），Realtime， 这部分功能很难云化，仍然放在接近站点的位置
