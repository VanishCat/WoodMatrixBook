*加工指令`BaseToken`按所属部件(部件如板件`Part`、五金`Hardware`）可分为：*
- 板件机加工指令

![](img\part.png)
- 五金机加工指令`HardwareToken`

*按加工指令的作用范围可分为：*
- 非关联加工指令`UnAssociativeToken`
    >该类型指令只可在指令所在的板件上生成加工,例如CORNERNOTCH直角切口、CUTOUT四面切口等；

    ![](img\非关联加工示意图.png)

- 关联加工指令`AssociativeToken`
    >当指令所属板件的加工面与其他板件的面有关联时，指令可在所属板件和关联板件生成特定加工;  



