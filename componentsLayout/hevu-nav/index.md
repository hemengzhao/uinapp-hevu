
# HevuNav 适用于uinapp 项目导航头部，不支持vue3
导航栏组件，主要用于头部导航，组件名：he-nav
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）

## 普通导航用法
`<HevuNav title='导航头' fixed :fixedTop='0' :extraHeight='40'/>`
## 搜索导航用法
`<HevuNav title='导航头' fixed :fixedTop='0' :extraHeight='0' search searchPlaceholderStyle='color:red'/>`

按钮的icon属性 大于 按钮文字
### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| ------------- | ---------------------------------------------------|
|title                       | String       | --             | 导航标题                 |
|color                       | String       | #fff           | 导航文字颜色              |
|bgColor                     | String       | #3375f6        | 导航背景颜色              |
|leftIcon                    | String       | back           | 导航左侧icon图标          |
|leftText                    | String       | --             | 导航左侧文字              |
|rightIcon                   | String       | scan           | 导航右侧icon图标          |
|rightText                   | String       | --             | 导航右侧文字              |
|opacity                     | Number       | 1              | 导航背景颜色图明度（0-1之间的数值）|
|fixed                       | Boolean      | false          | 导航是否固定上方                 |
|fixedTop                    | Number       | 0              | 导航固定上方位置                 |
|extraHeight                 | Number       | 0              | 文字上方是否增加额外的高度(包含在导航头内部)|

### 事件
| 名称                        | 参数         |描述                            |
|----------------------------|--------------|-------------------------------|
| leftTag                    | 参数         |左侧点击事件                      |
| contTag                    | 参数         |中间点击事件                      |
| rightTag                   | 参数         |右侧点击事件                      |

### 搜索导航属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ---------------------------|---------------| ------------- | ---------------------------------------------------|
|search                      | Boolean      | fasle          | 是否为搜索导航头                 |
|confirmType                 | String       | search         | 键盘右下角按钮文字 有效值send: 发送, search: 搜索, next: 下一个, go: 前往,  done: 完成|
|searchPlaceholder           | String       | 请输入搜索内容   | 输入框为空时占位符              |
|searchPlaceholderStyle      | String       | --             | 指定搜索框为 placeholder 的样式          |
|searchStyle                 | Object       | {}             | 指定搜索框样式              |


### 搜索导航事件
| 名称                        | 参数         |描述                            |
|----------------------------|--------------|-------------------------------|
| searchInput                | value        |搜索导航输入框输入变化事件 返回输入框值   |
| searchConfirm              | value        |搜索导航输入框点击搜索事件 返回输入框值   |