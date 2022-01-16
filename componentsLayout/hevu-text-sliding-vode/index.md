# HevuTextSlidingVode 适用于uinapp 验证码生成器，不支持vue3
 验证码生成器，组件名：hevu-text-sliding-vode
本组件目前兼容H5，5+APP，其他平台没试过（大概率不会有太大问题）

## 用法
`<HevuTextSlidingVode identifyCode='13fd' isInsideCode/>`

### 属性
| 名称                        | 类型          | 默认值          | 描述                                               |
| ----------------------------|--------------| -------------  | ---------------------------------------------------|
|isInsideCode                 | Boolean      | fasle          |验证码是否内部更新生成                 |
|codeLength                   | Number       | 4              |验证码长度 最小值位2 最大值位8（isInsideCode位true有效）                 |
|isCodetypeNumber             | Boolean      | false          | 验证码是否位纯数字（isInsideCode位true有效）                 |
|isCodeCasesensitive          | Boolean      | true           |验证码是否区分大小写（isInsideCode位true有效）                 |
|identifyCode                 | String       | 1234           |需要展示的验证码                 |
|fontSizeMin                  | Number       | 35             | 字体大小 最小值|
|fontSizeMax                  | Number       | 35             | 字体大小 最大值              |
|backgroundColor              | String       | --             | 背景颜色          |
|backgroundColorMin           | Number       | 180            | 背景颜色色值最小值          |
|backgroundColorMax           | Number       | 240            | 背景颜色色值最大值              |
|colorMin                     | Number       | 50             |字体颜色色值最小值         |
|colorMax                     | Number       | 160            | 字体颜色色值最大值|
|lineColorMin                 | Number       | 100            | 干扰线颜色色值最小值|
|lineColorMax                 | Number       | 200            | 干扰线颜色色值最大值|
|dotColorMin                  | Number       | 0              | 干扰点颜色色值最小值|
|dotColorMax                  | Number       | 255            | 干扰点颜色色值最大值|
|isDot                        | Boolean      | true           | 是否需要干扰点|
|isLine                       | Boolean      | true           | 是否需要干扰线|
|contentWidth                 | Number       | 120            | 画布宽度|
|contentHeight                | Number       | 40             | 画布高度|

### 方法
| 名称                        | 参数          |返回值                          |描述                         |
|----------------------------|---------------|-------------------------------|-------------------------------|
| verification               | code          |返回布尔值                       | 验证码确认验证方法（isInsideCode位true有效） 

### 事件
| 名称                        | 参数         |描述                            |
|----------------------------|--------------|-------------------------------|


