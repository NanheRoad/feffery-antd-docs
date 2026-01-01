# AntdRate

## 简介源码：`views/AntdRate/intro.py`
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
                {'title': 'AntdRate 评分'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdRate 评分', level=2),
        fac.AntdParagraph('用于为用户提供美观的星级打分功能。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_callbacks

- 说明：演示 basic_callbacks 的用法。

#### 代码
```python
fac.AntdRate(
    id='rate-demo',
    count=10,
    allowHalf=True,
    defaultValue=1
),

fac.AntdParagraph(
    id='rate-demo-output'
)

...

@app.callback(
    Output('rate-demo-output', 'children'),
    Input('rate-demo', 'value')
)
def rate_demo(value):

    return f'value: {value}'
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [fac.AntdRate(), fac.AntdRate(count=10, defaultValue=5)],
    direction='vertical',
)
```

### clear

- 说明：演示 clear 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=True, defaultValue=3),
                fac.AntdText('allowClear：True'),
            ]
        ),
        fac.AntdSpace(
            [
                fac.AntdRate(allowClear=False, defaultValue=3),
                fac.AntdText('allowClear：False'),
            ]
        ),
    ],
    direction='vertical',
)
```

### half_star

- 说明：演示 half_star 的用法。

#### 代码
```python
fac.AntdRate(allowHalf=True, defaultValue=3.5)
```

### read_only_status

- 说明：演示 read_only_status 的用法。

#### 代码
```python
fac.AntdRate(
    count=10, defaultValue=7.5, allowHalf=True, disabled=True
)
```

### star_tooltips

- 说明：演示 star_tooltips 的用法。

#### 代码
```python
fac.AntdRate(
    count=10, tooltips=[f'等级{i + 1}' for i in range(10)]
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

- allowClear (boolean; default True):
    是否允许通过再次点击清除已选分值  默认值：`True`.

- allowHalf (boolean; default False):
    是否允许半星选择  默认值：`False`.

- count (number; default 5):
    总分值  默认值：`5`.

- tooltips (list of strings; optional):
    为各分值设置提示文字信息.

- disabled (boolean; default False):
    是否渲染为只读评分形式  默认值：`False`.

- autoFocus (boolean; default False):
    是否自动获取焦点  默认值：`False`.

- value (number; optional):
    监听或设置已选值.

- defaultValue (number; default 0):
    初始化已选值  默认值：`0`.

- batchPropsNames (list of strings; optional):
    需要纳入[批量属性监听](/batch-props-values)的若干属性名.

- batchPropsValues (dict; optional):
    监听`batchPropsNames`中指定的若干属性值.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.

- persistence (boolean | string | number; optional):
    是否开启[属性持久化](/prop-persistence).

- persisted_props (list of a value equal to: 'value's; default ['value']):
    开启属性持久化功能的若干属性名，可选项有`'value'`  默认值：`['value']`.

- persistence_type (a value equal to: 'local', 'session', 'memory'; default 'local'):
    属性持久化存储类型，可选项有`'local'`（本地持久化），`'session'`（会话持久化），`'memory'`（内存持久化）
    默认值：`'local'`.
