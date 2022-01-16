

# HevuSliderSelector 适用于uinapp 滑块选择器，不支持vue3
加载框，组件名：hevu-slider-selector
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）

## 普通用法
`<HevuSliderSelector />`
## 普通用法
`<HevuSliderSelector :sliderHeight='40' sliderSelectorColor='#0ff' :max='97' company='px' :min='23' :selectorSize='60' selectorColor='#f0f' silderValueShow range/>`

### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| ------------- | ---------------------------------------------------|
|bgColor                      | String       | #eee          | 滑块选择器背景颜色          |
|range                        | Boolean      | false         | 是否为范围选择                 |
|max                          | Number       | 100           | 滑块选择最大值                  |
|min                          | Number       | 0             | 滑块选择最小值 |
|value                        | Array/Number | 0             | 默认选择数值                 |
|company                      | String       | --            | 滑块选择器单位              |
|toFixed                      | Number       | 0             | 滑块选择器数值保留小数位数（小于0按0处理）              |
|sliderHeight                 | Number       | 20            | 滑块选择器滑动条高度             |
|silderValueShow              | Boolean      | false         | 选择器是否显示起始数值              |
|silderValueSize              | Number       | 22            | 选择器显示起始数值字体大小                |
|silderValueColor             | String       | #000          | 选择器显示起始数值字体颜色              |
|selectorSize                 | Number       | 40            | 滑块按钮大小                |
|selectorColor                | String       | #3375f6       | 滑块按钮颜色                |
|selectorValueColor           | String       | #000          | 滑块按钮选择数值颜色               |
|selectorValueSize            | Number       | 30            | 滑块按钮选择数值字体大小                |
|selectorValueShow            | Boolean      | true          | 滑块按钮选择数值是否显示                |
|sliderSelectorColor          | String       | #3375f6       | 滑块选择数据内滑块背景颜色                |

### 方法
| 名称                         | 参数          | 描述                                               |
| ----------------------------|-------------- | ---------------------------------------------------|
|onChange                     | Array         | 返回选择的数值          |

