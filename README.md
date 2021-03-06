
## FlexLib2

flexbox最初是web端布局方案，现在已经应用在多个平台。

Android、iOS都有单独的实现，Android的实现是google的[flexbox-layout](https://github.com/google/flexbox-layout.git)，iOS的实现是Facebook的[yoga](https://github.com/facebook/yoga.git)。

这里提供一种方案，使得同一份XML布局文件可以在Android和iOS上跨端使用。


## XML文件语法
完全依照Android写法。只需要添加少量代码，即可在iOS上展示同样的布局。


## 支持的flexbox属性

采用namespace前缀app 双端通用的flexbox属性及值如下
| key                      | value                                                             |
|--------------------------|-------------------------------------------------------------------|
| flexDirection            | row/row\_reverse/column/column\_reverse                           |
| flexWrap                 | nowrap/wrap/wrap\_reverse                                         |
| alignItems               | flex\_start/flex\_end/center/baseline/stretch                     |
| alignContent             | flex\_start/flex\_end/center/space\_between/space\_around/stretch |
| layout\_alignSelf        | auto/flex\_start/flex\_end/center/baseline/stretch                |
| justifyContent           | flex\_start/flex\_end/center/space\_between/spce\_around          |

这几个属性iOS端的yoga不支持：layout_flexBasisPercent，layout_flexGrow，layout_flexShrink


## 宽/高/margin/padding

因为Android和iOS的布局尺寸单位不等同，所以有必要区分双端的相关属性。具体可以参考[这里](https://juejin.im/entry/5a37bd866fb9a04509099d25)。

下列表格展示双端通用的属性名，但使用的namespace不一样，属性值也有一些差异，比如Android值后面加dp，iOS值可以是数字，可以是一个百分数。

特别指出一下，android:width=match_parent相对应ios:width=100%。


| key                  | android            | ios                         |
|----------------------|--------------------|-----------------------------|
| layout\_margin(-/Start/End/Top/Bottom/Left/Right)       | follow Android doc | float num value/percent num |
| padding(-/Start/End/Top/Bottom/Left/Right)              | follow Android doc | float num value/percent num |
| layout\_width        | follow Android doc | float num value/percent num |
| layout\_height     | follow Android doc | float num value/percent num |
| layout\_(min/max)Width        | follow Android doc | float num value/percent num |
| layout\_(min/max)Height    | follow Android doc | float num value/percent num |


## 类定义
对应关系如下
| Android class name                           | iOS class name |
|----------------------------------------------|----------------|
| com\.google\.android\.flexbox\.FlexboxLayout | UIView         |
| TextView                                     | UILabel        |
| HorizontalScrollView                         | UIScrollView   |
| ScrollView                                   | UIScrollView   |
| FrameLayout                                  | UIView         |
| View                                         | UIView         |
| ImageView                                    | UIImageView    |
| EditText                                     | UITextView     |
| ScrollView                                   | UIScrollView   |
| ListView                                     | UITableView    |

其余可以通过更高优先级的ios:class指定。


## iOS特有属性

namespace ios 可以添加以下特有属性

| key                             | value                                                                                                                          |
|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------|
| name                            | 变量名，需要在代码里声明                                                                                                                            |
| onPress                         | 方法名，需要在代码里声明                                                                                                                            |
| class                           | 类名，创建相应类时，优先于XML元素名                                                                                                                             |
| style                           | 参考system.style                                                                                                                         |

其余属性，可以查看ViewExt目录下Category的声明。


## 一些例子
项目Example的界面是通过XML编写的。

另外，flexbox-layout本身有一些测试XML，Example/android_test下面是对这些测试例子进行了适配iOS的结果，除了包含yoga不支持属性的XML，其余的，运行结果跟Android上一致。


## 安装

通过pod方式安装FlexLib2，例子如下:

```ruby
pod 'FlexLib2'
```


## 兼容[FlexLib](https://github.com/zhenglibao/FlexLib.git)
scripts目录提供了转换脚本，使用方法：

转换单个XML文件：
```ruby
 ./scripts/flex_xml_trans.py /path/old_style.xml
```
转换目录下所有XML文件：
```ruby
 ./scripts/flex_xml_trans.py /path
```
该项目Example里的XML文件，皆通过此脚本从FlexLib转换而来。


## 感谢
感谢[FlexLib](https://github.com/zhenglibao/FlexLib.git)作者[zhenglibao](798393829@qq.com)。

本项目基于FlexLib开发，关于基本使用方法、特性、性能，可以移步到[FlexLib](https://github.com/zhenglibao/FlexLib.git)进行了解。

## 联系方式
优先：提issues

email：zionfong@gmail.com


## 版权

FlexLib is available under the MIT license. See the LICENSE file for more info.

---

