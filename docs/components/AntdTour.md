# AntdTour

## 简介源码：`views/AntdTour/intro.py`
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
                {'title': 'AntdTour 漫游式引导'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdTour 漫游式引导', level=2),
        fac.AntdParagraph('用于分步引导用户了解产品功能的气泡组件。'),
    ]

```

## 示例代码片段（仅保留演示内容）

### arrow_placement

- 说明：演示 arrow_placement 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '开始placement引导',
            type='primary',
            id='start-placement-tour-demo',
        ),
        fac.AntdButton(
            '开始arrow引导', type='primary', id='start-arrow-tour-demo'
        ),
        fac.AntdDivider(),
        fac.AntdSpace(
            [
                fac.AntdButton(i, id=f'placement-{i}-btn-tour-demo')
                for i in [
                    'center',
                    'left',
                    'leftTop',
                    'leftBottom',
                    'right',
                    'rightTop',
                    'rightBottom',
                    'top',
                    'topLeft',
                    'topRight',
                    'bottom',
                    'bottomLeft',
                    'bottomRight',
                    'arrowPointAtCenter',
                    'arrowIsFalse',
                ]
            ],
            wrap=True,
        ),
        fac.AntdDivider(),
        fac.AntdSpace(
            [
                fac.AntdButton(i, id=f'arrow-{index}-btn-tour-demo')
                for index, i in enumerate(
                    [
                        '有箭头',
                        '无箭头',
                        '箭头指向元素中心',
                        '箭头不指向元素中心',
                    ]
                )
            ],
            wrap=True,
        ),
        fac.AntdTour(
            # 全局配置placement为center，即所有步骤的弹框默认位置为居中
            placement='center',
            # 全局配置arrow为pointAtCenter: False，即所有步骤的弹框箭头不需要指向元素中心
            arrow={'pointAtCenter': False},
            steps=[
                {
                    'title': i,
                    'description': f'弹框相对元素位置：{i}',
                    'targetId': f'placement-{i}-btn-tour-demo',
                    # 单独配置不同step的placement，优先级高于全局placement
                    'placement': i,
                }
                for i in [
                    'center',
                    'left',
                    'leftTop',
                    'leftBottom',
                    'right',
                    'rightTop',
                    'rightBottom',
                    'top',
                    'topLeft',
                    'topRight',
                    'bottom',
                    'bottomLeft',
                    'bottomRight',
                ]
            ],
            id='tour-demo',
        ),
        fac.AntdTour(
            placement='topRight',
            # 全局配置arrow为True
            arrow=True,
            steps=[
                {
                    'title': k,
                    'description': f'{k}的弹框示例',
                    'targetId': f'arrow-{index}-btn-tour-demo',
                    # 单独配置不同step的arrow，优先级高于全局arrow
                    'arrow': v,
                }
                for index, (k, v) in enumerate(
                    {
                        '有箭头': True,
                        '无箭头': False,
                        '箭头指向元素中心': {'pointAtCenter': True},
                        '箭头不指向元素中心': {'pointAtCenter': False},
                    }.items()
                )
            ],
            id='arrow-tour-demo',
        ),
    ],
    direction='vertical',
)


@app.callback(
    [
        Output('placement-tour-demo', 'current'),
        Output('placement-tour-demo', 'open'),
    ],
    Input('start-placement-tour-demo', 'nClicks'),
    prevent_initial_call=True,
)
def start_placement_tour_demo(nClicks):
    # 清空Tour step序号回归0，并打开Tour
    return 0, True


@app.callback(
    [
        Output('arrow-tour-demo', 'current'),
        Output('arrow-tour-demo', 'open'),
    ],
    Input('start-arrow-tour-demo', 'nClicks'),
    prevent_initial_call=True,
)
def start_arrow_tour_demo(nClicks):
    # 清空Tour step序号回归0，并打开Tour
    return 0, True
```

### basic_usage

- 说明：演示 basic_usage 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '开始引导', type='primary', id='start-tour-demo-1'
        ),
        fac.AntdDivider(),
        fac.AntdSpace(
            [
                fac.AntdButton('上传', id='upload-btn-tour-demo-1'),
                fac.AntdButton(
                    '保存', type='primary', id='save-btn-tour-demo-1'
                ),
                fac.AntdButton('···', id='more-btn-tour-demo-1'),
            ]
        ),
        fac.AntdTour(
            steps=[
                {
                    'title': '欢迎',
                    'description': '欢迎使用 Feffery Antd Tour 组件！',
                    # 可配置封面图，可传入多个Dash组件
                    'cover': fac.AntdImage(
                        src='assets/imgs/fac-logo.svg',
                        preview=False,
                        height=100,
                        width=100,
                    ),
                },
                {
                    'title': '上传文件',
                    'description': '点击此按钮上传文件',
                    'targetId': 'upload-btn-tour-demo-1',
                },
                {
                    'title': '保存文件',
                    'description': '点击此按钮保存文件',
                    'targetId': 'save-btn-tour-demo-1',
                },
                {
                    'title': '更多功能',
                    'description': '点击此按钮查看更多功能',
                    'targetId': 'more-btn-tour-demo-1',
                },
            ],
            id='tour-demo-1',
        ),
    ],
    direction='vertical',
)


@app.callback(
    [
        Output('tour-demo-1', 'current'),
        Output('tour-demo-1', 'open'),
    ],
    Input('start-tour-demo-1', 'nClicks'),
    prevent_initial_call=True,
)
def start_tour_demo-1(nClicks):
    # 清空Tour step序号回归0，并打开Tour
    return 0, True
```

### buttons

- 说明：演示 buttons 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '开始引导', type='primary', id='start-tour-buttons-demo'
        ),
        fac.AntdDivider(),
        fac.AntdSpace(
            [
                fac.AntdButton(
                    '上传', id='upload-btn-tour-buttons-demo'
                ),
                fac.AntdButton(
                    '保存',
                    type='primary',
                    id='save-btn-tour-buttons-demo',
                ),
                fac.AntdButton('···', id='more-btn-tour-buttons-demo'),
            ]
        ),
        fac.AntdTour(
            steps=[
                {
                    'title': '欢迎',
                    'description': '欢迎使用 fac.AntdTour 组件！',
                    # 可配置封面图，可传入多个Dash组件
                    'cover': fac.AntdImage(
                        src='assets/imgs/fac-logo.svg',
                        preview=False,
                        height=100,
                        width=100,
                    ),
                    'nextButtonProps': {'children': '第2步 👉🏻'},
                },
                {
                    'title': '上传文件',
                    'description': '点击此按钮上传文件',
                    'targetId': 'upload-btn-tour-buttons-demo',
                    'prevButtonProps': {'children': '👈🏻 第1步'},
                    'nextButtonProps': {'children': '第3步 👉🏻'},
                },
                {
                    'title': '保存文件',
                    'description': '点击此按钮保存文件',
                    'targetId': 'save-btn-tour-buttons-demo',
                    'prevButtonProps': {'children': '👈🏻 第2步'},
                    'nextButtonProps': {'children': '第4步 👉🏻'},
                },
                {
                    'title': '更多功能',
                    'description': '点击此按钮查看更多功能',
                    'targetId': 'more-btn-tour-buttons-demo',
                    'prevButtonProps': {'children': '👈🏻 第3步'},
                    'nextButtonProps': {'children': '结束🔚'},
                },
            ],
            id='tour-buttons-demo',
        ),
    ],
    direction='vertical',
)


@app.callback(
    [
        Output('tour-buttons-demo', 'current'),
        Output('tour-buttons-demo', 'open'),
    ],
    Input('start-tour-buttons-demo', 'nClicks'),
    prevent_initial_call=True,
)
def start_tour_demo(nClicks):
    # 清空Tour step序号回归0，并打开Tour
    return 0, True
```

### mask

- 说明：演示 mask 的用法。

#### 代码
```python
fac.AntdSpace(
    [
        fac.AntdButton(
            '开始引导', type='primary', id='start-tour-demo-2'
        ),
        fac.AntdDivider(),
        fac.AntdSpace(
            [
                fac.AntdButton('上传', id='upload-btn-tour-demo-2'),
                fac.AntdButton(
                    '保存', type='primary', id='save-btn-tour-demo-2'
                ),
                fac.AntdButton('···', id='more-btn-tour-demo-2'),
            ]
        ),
        fac.AntdTour(
            # 统一配置mask，灰色，不透明度20%
            mask={'color': 'gray', 'style': {'opacity': '0.2'}},
            # 统一配置type
            type='default',
            steps=[
                {
                    'title': '欢迎',
                    'description': '欢迎使用 Feffery Antd Tour 组件！',
                    # 单独配置不同step的mask，优先级高于全局mask
                    'mask': False,
                    # 单独配置不同step的type，优先级高于全局type
                    'type': 'primary',
                },
                {
                    'title': '上传文件',
                    'description': '点击此按钮上传文件',
                    'targetId': 'upload-btn-tour-demo-2',
                },
                {
                    'title': '保存文件',
                    'description': '点击此按钮保存文件',
                    'targetId': 'save-btn-tour-demo-2',
                },
                {
                    'title': '更多功能',
                    'description': '点击此按钮查看更多功能',
                    'targetId': 'more-btn-tour-demo-2',
                },
            ],
            id='tour-demo-2',
        ),
    ],
    direction='vertical',
)


@app.callback(
    [
        Output('tour-demo-2', 'current'),
        Output('tour-demo-2', 'open'),
    ],
    Input('start-tour-demo-2', 'nClicks'),
    prevent_initial_call=True,
)
def start_tour_demo(nClicks):
    # 清空Tour step序号回归0，并打开Tour
    return 0, True
```

## API 参数说明



- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- steps (list of dicts; optional):
    配置引导步骤.

    `steps` is a list of dicts with keys:

    - targetId (string; optional):
        当前步骤目标元素id，优先级高于`targetSelector`.

    - targetSelector (string; optional):
        定位当前步骤目标元素的javascript代码字符串.

    - arrow (dict; optional):
        配置当前步骤箭头  默认值：`True`.

        `arrow` is a boolean

      Or dict with keys:

        - pointAtCenter (boolean; optional):

            箭头是否指向目标中心.

    - cover (a list of or a singular dash component, string or number; optional):
        组件型，当前步骤弹框的封面内容.

    - title (a list of or a singular dash component, string or number; optional):
        组件型，当前步骤弹框的标题内容.

    - description (a list of or a singular dash component, string or number; optional):
        组件型，当前步骤弹框的描述内容.

    - placement (a value equal to: 'center', 'left', 'leftTop', 'leftBottom', 'right', 'rightTop', 'rightBottom', 'top', 'topLeft', 'topRight', 'bottom', 'bottomLeft', 'bottomRight'; optional):
        当前引导步骤弹框相对目标元素的位置，可选项有`'center'`、`'left'`、`'leftTop'`、`'leftBottom'`、`'right'`、`'rightTop'`、`'rightBottom'`、`'top'`、`'topLeft'`、`'topRight'`、`'bottom'`、`'bottomLeft'`、`'bottomRight'`.

    - mask (dict; optional):
        配置当前步骤蒙版层  默认值：`True`.

        `mask` is a boolean | dict with keys:

        - style (dict; optional):

            当前步骤蒙版层css样式.

        - color (string; optional):

            当前步骤蒙版层颜色.

    - type (a value equal to: 'default', 'primary'; optional):
        当前步骤弹框类型，可选项有`'default'`、`'primary'`  默认值：`'default'`.

    - nextButtonProps (dict; optional):
        配置当前步骤下一步按钮.

        `nextButtonProps` is a dict with keys:

        - children (a list of or a singular dash component, string or number; optional):
            组件型，按钮内嵌元素.

    - prevButtonProps (dict; optional):
        配置当前步骤上一步按钮.

        `prevButtonProps` is a dict with keys:

        - children (a list of or a singular dash component, string or number; optional):
            组件型，按钮内嵌元素.

- arrow (dict; default True):
    统一配置引导步骤弹框箭头  默认值：`True`.

    `arrow` is a boolean | dict with keys:

    - pointAtCenter (boolean; optional):
        箭头是否指向目标中心.

- placement (a value equal to: 'center', 'left', 'leftTop', 'leftBottom', 'right', 'rightTop', 'rightBottom', 'top', 'topLeft', 'topRight', 'bottom', 'bottomLeft', 'bottomRight'; default 'bottom'):
    统一配置引导步骤弹框相对于目标元素的展开方向，可选项有`'center'`、`'left'`、`'leftTop'`、`'leftBottom'`、`'right'`、`'rightTop'`、`'rightBottom'`、`'top'`、`'topLeft'`、`'topRight'`、`'bottom'`、`'bottomLeft'`、`'bottomRight'`
    默认值：`'bottom'`.

- mask (dict; default True):
    统一配置引导弹框蒙版  默认值：`True`.

    `mask` is a boolean | dict with keys:

    - style (dict; optional):
        蒙版层css样式.

    - color (string; optional):
        蒙版层颜色.

- type (a value equal to: 'default', 'primary'; default 'default'):
    统一设置引导步骤弹框类型，可选项有`'default'`、`'primary'`  默认值：`'default'`.

- open (boolean; default False):
    监听或设置当前漫游式引导的打开状态  默认值：`False`.

- current (number; optional):
    监听或设置当前漫游式引导所在步骤序号.

- zIndex (number; default 1001):
    当前漫游式引导z-index  默认值：`1001`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.
