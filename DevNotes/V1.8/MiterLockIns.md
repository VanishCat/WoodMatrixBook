###斜切面关联 DMITERLOCK
**需求背景**
>客户(成都尼奥、郑州欧曼)引进了新的板件连接五金件：三合一丝牙折叠杆。
该连接件可以实现：板件侧边切斜面后与另一片板件形成一定角度连接。
WM的关联中仅有板件常规的6个面关联，需要增加对板件侧边斜切面的关联支持。
[Worktile项目链接](https://dmsoft.worktile.com/mission/projects/5e377e8ae727c16b0f47a3cf/tasks/5ea944c6f8caa41a8d31dec4)
[Worktile项目链接2](https://dmsoft.worktile.com/mission/projects/5e377e8ae727c16b0f47a3cf/tasks/5e9821059a72811632b69ae4)

![三合一丝牙折叠杆](images\三合一丝牙折叠杆.jpg)


<video src="Video\三合一折叠杆安装.mp4" controls="controls" width="400px" height="300px"></video>
<video src="video\转角三合一安装视频.mp4" controls="controls" width="50%"></video>

**功能实现**
- 增加DIMETERLOCK关联加工指令
- MITER斜切指令生效的同时，板件的面集合增加该指令的斜切面用于计算关联

**关联的计算**
<img src="images\MiterLock生成流程.png" />

1. 斜切面的生成
    ```
    斜切面由加工面、斜切角度决定。
    斜切角度范围：-90°~90°
    斜切角度定义：斜切面与板件面5或面6形成的夹角
    当角度大于0时，以板件面5为角点做斜切；
    当角度小于0时，以板件面6为角点做斜切
    ```
    <img src="images\MiterLock斜切面.png" width="60%" />

2. [查找关联面](../../Token/token.AssociateIllu.md)
3. 关联结构与加工
    - 不论斜切面是否存在关联，斜切面始终生成；孔位在斜切面关联的前提下才生成
    - 斜切面与面5面6关联
        ```
        被关联板件生成一组关联垂直孔
        ```

        <img src="images\斜切关联示意图.png" width="50%" title="与面5面6关联" />

    - 斜切面与斜切面关联
        ```
        被关联板件生成水平孔和额外的偏心轮。两板件偏心轮距边Backset一致。
        关联偏心轮所在的面与另一片板件在同一侧。
        ```       
        
        <img src="images\MiterLock关联2.png" width="50%" title="斜切面与斜切面关联"/>

    - 关联偏心轮所在面的计算
        ```
        //两板件夹角向量和与两偏心轮所在面的法向量之和平行
        Vector3d v1;//板件夹角向量v1
        Vector3d v2;//板件夹角向量v2
        Vector3d camV1;//偏心轮1所在面法向量
        Vector3d camV2;//偏心轮2所在面法向量
        v3=v1+v2;//板件夹角向量和
        v4=camV1+camV2;//偏心轮所在面向量和
        v3.IsParallelTo(V4);//向量是否平行
        //特殊的当v1+v2为0长度向量，即两板件成180°摆放时，偏心轮方向需要一致
        camV1.IsEqual(camV2);//判断偏心轮方向是否一致
        ```

