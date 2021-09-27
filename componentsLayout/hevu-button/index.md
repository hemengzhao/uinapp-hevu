# HevuButton 适用于uinapp 按钮，不支持vue3
按钮，组件名：hevu-button
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）
按钮组件uinapp已经很方便了，这个只是随手封装一个，可能很少用到吧，

## 用法
`<HevuButton type="brief" borderType='dashed'>简约 虚线</HevuButton>`

### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| ------------- | ---------------------------------------------------|
|width                       | String       | 90%            | 按钮宽度                 |
|height                       | String       | 80rpx         | 按钮高度              |
|radius                     | String        | 5px            | 按钮圆角        |
|type                       | String       | purity           | 按钮类型  purity 纯色  brief 简约  hollow 镂空  none 无边框镂空           |
|borderSize                  | Array｜number  | 1            | 边框大小              |
|borderType                   | String       | solid           | 按钮边框的类型  solid：实线  dashed：虚线  dotted：点阵         |
|disabled                   | Boolean       | fasle             | 是否禁用禁用              |
|loading                     | Boolean       | fasle          | 是否加载状态  |
|boxShadow                   | String      | --              | 按钮阴影 格式同css               |

### 事件
| 名称                        | 参数         |描述                            |
|----------------------------|--------------|-------------------------------|
