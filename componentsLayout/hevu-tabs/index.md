# HevuTabs 适用于uinapp tabs选择滑块，不支持vue3
tabs选项卡，滑动效果，组件名：he-tabs
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）

## 用法

<HevuTabs :activeValue='3' :list="['简约 虚线', '镂空  点缀']"/>

### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| -------------  | ---------------------------------------------------|
|type                        | String        | line           | tabs类型  line   back                 |
|list                        | Array         | --             | (必填)tabs数据了列表  数据格式['张三'， '里斯'] 或者 [{name: '张三'}， {name: '里斯'}] name为必需key值 |
|backColor                   | String        | #fff           | tabs背景颜色              |
|activeColor                 | String        | #007aff        | 选中高亮颜色          |
|activeKey                   | String        | --             | 选中高亮key值依据  默认空置以索引为准              |
|activeValue                 | String        |--              |初始选中的值         |
|animated                    | Boolean       | true           | 下划线动画|

### 事件
| 名称                        | 参数         |描述                            |
|----------------------------|--------------|-------------------------------|
| click                      | item(数据信息) index （索引） |	切换点击事件      |
