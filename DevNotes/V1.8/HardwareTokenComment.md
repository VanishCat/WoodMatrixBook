**需求背景**
>添加某类五金时五金指令所关联的板件需要显示特定备注，现在的做法是通过添加板件备注的方式，比较麻烦且容易遗漏。
[Worktile项目链接](https://dmsoft.worktile.com/mission/projects/5e377e8ae727c16b0f47a3cf/tasks/5ea4e27bc5de12753c09f176)

**功能实现**
- 五金加工指令增加解析规则:```()```中的内容解析为关联板件备注
    ```
    指令名[描述](关联板件备注)
    例:ROUTE[直线立铣](开槽)
    ```
- 将解析的备注写入五金指令所关联的板件备注1中
    ```备注信息见处理报表后生成的OverdrivePro.mdb文件中CombinedParts表的Comments1字段```

<img src="images\五金指令备注.png" width="80%"/>

