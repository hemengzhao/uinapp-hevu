

# HevuNav 适用于uinapp 项目导航头部，不支持vue3
加载框，组件名：he-loading
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）

## 普通用法
`<HevuLoading type="loading1" />`
## 覆盖dom上
`<HevuLoading type="loading13" :opacity='0.8' :size="150"><image class="logo" src="/static/logo.png"></image></HevuLoading>`

### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| ------------- | ---------------------------------------------------|
|loadingning                  | Boolean      | true          | 控制加载状态开关          |
|fixed                        | Boolean      | false         | 固定定位（相当于加载页）                 |
|zIndex                       | Number       | false         | 定位层级（配合fixed使用）                  |
|opacity                      | Number       | 1             | 背景透明度（0-1之间的数值） |
|backgroundColor              | String       | #fff          | 背景颜色                 |
|loadingText                  | String       | 加载中....     | 加载文字提示              |
|textColor                    | String       | #3375f6       | 加载文字颜色              |
|textSize                     | Number       | 30            | 加载文字大小              |
|textFlicker                  | Boolean      | true          | 加载文字闪动              |
|loadingIconColor             | String       | #3375f6       | 加载图颜色                |
|type                         | String       | loading1      | 加载图类型（loading1 ～ loading13）               |
|size                         | Number       | 120           | 加载图大小                |
