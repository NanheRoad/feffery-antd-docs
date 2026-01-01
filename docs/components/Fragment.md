# Fragment

## 简介源码：`views/Fragment/intro.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染组件介绍内容"""
    return [
        fac.AntdBreadcrumb(
            items=[
                {'title': '组件介绍'},
                {'title': '其他'},
                {'title': 'Fragment 空节点'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('Fragment 空节点', level=2),
        fac.AntdParagraph('承载内部元素且本身不渲染占用DOM节点。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
[
    fac.AntdButton('新通知', id='fragment-demo-trigger', type='primary'),
    fac.Fragment(id='fragment-demo'),
]

...

@app.callback(
    Output('fragment-demo', 'children'),
    Input('fragment-demo-trigger', 'nClicks'),
    prevent_initial_call=True,
)
def fragment_demo(nClicks):
    return fac.AntdMessage(content=f'nClicks: {nClicks}', type='info')
```

### listen_style_token

- 说明：演示 listen_style_token 的用法。

#### 代码
```python
fac.AntdConfigProvider(
    html.Div(
        fac.Fragment(
            [
                fuc.FefferyStyle(id='fragment-token-demo-dynamic-style'),
                fac.AntdSpace(
                    [
                        fac.AntdCenter(
                            fac.AntdSwitch(
                                id='fragment-token-demo-switch-algorithm',
                                checked=True,
                                checkedChildren='🌙',
                                unCheckedChildren='☀️',
                            )
                        ),
                        fac.AntdText('Test' * 1000),
                    ],
                    direction='vertical',
                    style={'width': '100%'},
                ),
            ],
            id='fragment-token-demo',
        ),
        style={'padding': 24},
    ),
    id='fragment-token-demo-config-provider',
)

...

app.clientside_callback(
    '''(checked) => checked ? "dark" : "default"''',
    Output('fragment-token-demo-config-provider', 'algorithm'),
    Input('fragment-token-demo-switch-algorithm', 'checked'),
)

app.clientside_callback(
    '''(token) => {
        let newStyle = `
body {
    background: ${token.colorBgBase} !important;
}`
        console.log(newStyle)
        return newStyle;
    }''',
    Output('fragment-token-demo-dynamic-style', 'rawStyle'),
    Input('fragment-token-demo', 'token'),
)
```
