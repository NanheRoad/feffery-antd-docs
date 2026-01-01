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

## 示例源码（demos）

### `views/AntdHappyProvider/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdHappyProvider(
        fac.AntdSpace([fac.AntdButton(f'Button{i}') for i in range(1, 4)])
    )

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    return [
        {
            'code': """
fac.AntdHappyProvider(
    fac.AntdSpace([fac.AntdButton(f'Button{i}') for i in range(1, 4)])
)
"""
        }
    ]

```

### `views/AntdHappyProvider/demos/other_effects.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdHappyProvider(
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

    return demo_contents


def code_string() -> list:
    """返回当前语种对应的演示代码"""

    return [
        {
            'code': """
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
"""
        }
    ]

```
