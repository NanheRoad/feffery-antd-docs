# AntdHappyProvider

## 简介源码：`views/AntdHappyProvider/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component

# 国际化
from i18n import translator


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': translator.t('组件介绍')},
                {'title': translator.t('其他')},
                {'title': translator.t('AntdHappyProvider 快乐工作特效')},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle(translator.t('AntdHappyProvider 快乐工作特效'), level=2),
        fac.AntdParagraph(translator.t('为内部组件添加有趣的额外交互特效。')),
    ]

```

## 示例代码片段（仅保留演示内容）

### 基础使用

- 说明：快乐工作特效组件内部的所有`AntdButton`组件，在点击时会附带额外的特效。

#### 代码
```python
fac.AntdHappyProvider(
    fac.AntdSpace([fac.AntdButton(f'Button{i}') for i in range(1, 4)])
)
```

### 其他效果

- 说明：快乐工作特效组件内部其他类型基础组件的交互效果。

#### 代码
```python
fac.AntdHappyProvider(
    fac.AntdSpace(
        [
            fac.AntdSwitch(),
            fac.AntdCheckbox(),
            fac.AntdRadioGroup(
                options=[f'option{i}' for i in range(1, 4)], value='option1'
            ),
        ]
    )
)
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- disabled (boolean; default False):
    是否禁用当前特效  默认值：`False`.
