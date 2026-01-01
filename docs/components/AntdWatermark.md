# AntdWatermark

## 简介源码：`views/AntdWatermark/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据展示'},
                {'title': 'AntdWatermark 水印'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdWatermark 水印', level=2),
        fac.AntdParagraph('用于在指定内容上叠加水印内容。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdWatermark(
    html.Div(
        style={
            'height': '500px',
            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
            'marginBottom': '25px'
        }
    ),
    content='水印内容测试',
    fontSize=28
),

fac.AntdWatermark(
    html.Div(
        fac.AntdForm(
            [
                fac.AntdFormItem(
                    fac.AntdInput(
                        autoComplete='off'
                    ),
                    label='用户名'
                ),
                fac.AntdFormItem(
                    fac.AntdInput(
                        mode='password'
                    ),
                    label='密码'
                ),
                fac.AntdFormItem(
                    fac.AntdCheckbox(
                        label='记住密码'
                    ),
                    wrapperCol={
                        'offset': 4
                    }
                ),
                fac.AntdFormItem(
                    fac.AntdButton(
                        '登录',
                        type='primary'
                    ),
                    wrapperCol={
                        'offset': 4
                    }
                )
            ],
            labelCol={
                'span': 4
            },
            wrapperCol={
                'span': 8
            }
        ),
        style={
            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
            'padding': '25px'
        }
    ),
    content='水印内容测试',
    fontSize=22,
    rotate=22,
    gapX=50,
    gapY=50
)
```

### image_watermark

- 说明：演示 image_watermark 的用法。

#### 代码
```python
fac.AntdWatermark(
    html.Div(
        style={
            'height': '500px',
            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
            'marginBottom': '25px'
        }
    ),
    image='assets/imgs/fac-logo.svg',
    width=48,
    height=48,
    rotate=0
)
```

### multiline_text

- 说明：演示 multiline_text 的用法。

#### 代码
```python
fac.AntdWatermark(
    html.Div(
        style={
            'height': '500px',
            'boxShadow': '0 6px 16px rgb(107 147 224 / 14%)',
            'marginBottom': '25px'
        }
    ),
    content=[
        '第一行水印',
        '第二行水印',
        '第三行水印'
    ],
    fontSize=28
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string; optional):
    当前组件css类名.

- markClassName (string; optional):
    水印层css类名.

- markStyle (dict; optional):
    水印层css样式.

- content (string | list of strings; optional):
    配置水印内容，传入数组时渲染多行水印.

- rotate (number; default -22):
    水印旋转角度  默认值：`-22`.

- zIndex (number; optional):
    水印z-index.

- fontColor (string; optional):
    文字水印颜色.

- fontSize (number; default 16):
    文字水印字体大小  默认值：`16`.

- gapX (number; default 212):
    水印之间的水平像素间距  默认值：`212`.

- gapY (number; default 222):
    水印之间的垂直像素间距  默认值：`222`.

- image (string; optional):
    图片水印地址.

- width (number; optional):
    图片水印像素宽度.

- height (number; optional):
    图片水印像素高度.

- inherit (boolean; default True):
    是否将水印传导给`AntdModal`、`AntdDrawer`等弹出类组件  默认值：`True`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
