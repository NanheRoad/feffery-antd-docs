# AntdOTP

## 简介源码：`views/AntdOTP/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '数据录入'},
                {'title': 'AntdOTP 一次性密码框'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdOTP 一次性密码框', level=2),
        fac.AntdParagraph('用于提供验证码等一次性固定位数密码输入功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdOTP(id='otp-demo'),
        fac.AntdText(id='otp-demo-output'),
    ],
    direction='vertical',
    style={
        'width': '100%',
    },
)

...

@app.callback(
    Output('otp-demo-output', 'children'),
    Input('otp-demo', 'value'),
    prevent_initial_call=True,
)
def show_otp_value(value):
    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdOTP()
```

### custom_display_character

- 说明：演示 custom_display_character 的用法。

#### 代码
```python
fac.AntdOTP(mask='🔒')
```

### disabled

- 说明：演示 disabled 的用法。

#### 代码
```python
fac.AntdOTP(disabled=True)
```

### length

- 说明：演示 length 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdOTP(length=i) for i in range(3, 10)], direction='vertical'
)
```

### sizes

- 说明：演示 sizes 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider('size="small"', innerTextOrientation='left'),
        fac.AntdOTP(size='small'),
        fac.AntdDivider(
            'size="middle"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(),
        fac.AntdDivider('size="large"', innerTextOrientation='left'),
        fac.AntdOTP(size='large'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

### status

- 说明：演示 status 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdOTP(status=status) for status in ['warning', 'error']],
    direction='vertical',
)
```

### variant

- 说明：演示 variant 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdDivider(
            'variant="outlined"（默认）', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='outlined'),
        fac.AntdDivider(
            'variant="borderless"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='borderless'),
        fac.AntdDivider('variant="filled"', innerTextOrientation='left'),
        fac.AntdOTP(variant='filled'),
        fac.AntdDivider(
            'variant="underlined"', innerTextOrientation='left'
        ),
        fac.AntdOTP(variant='underlined'),
    ],
    direction='vertical',
    style={'width': '100%'},
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- name (string; optional):
    配合`AntdForm`表单批量值搜集/控制功能使用，充当当前表单项的字段名，以`id`作为缺省值.

- enableBatchControl (boolean; default True):
    控制当前组件是否参与有效的`AntdForm`表单批量值搜集/控制功能  默认值：`True`.

- value (string; optional):
    监听或设置已选值.

- defaultValue (string; optional):
    初始化已选值.

- disabled (boolean; default False):
    是否禁用当前组件  默认值：`False`.

- length (number; default 6):
    单体输入框数量  默认值：`6`.

- mask (boolean | string; default False):
    自定义遮罩字符  默认值：`False`.

- status (a value equal to: 'error', 'warning'; optional):
    控制校验状态，可选项有`'error'`、`'warning'`.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    当前组件尺寸规格，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- variant (a value equal to: 'outlined', 'borderless', 'filled', 'underlined'; default 'outlined'):
    形态变体类型，可选项有`'outlined'`、`'borderless'`、`'filled'`、`'underlined'`，其中`'outlined'`等价于`bordered=True`，但优先级更高.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; optional):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; optional):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
