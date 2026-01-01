# AntdComment

## 简介源码：`views/AntdComment/intro.py`
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
                {'title': 'AntdComment 评论'},
            ],
            style={'marginBottom': 8},
        ),
        fac.AntdTitle('AntdComment 评论', level=2),
        fac.AntdParagraph('构建常用的用户评论相关功能。'),
    ]

```

## 示例源码（demos）

### `views/AntdComment/demos/basic_callbacks.py`
```python
import dash
import uuid
from datetime import datetime
import feffery_antd_components as fac
from dash.dependencies import Component, Input, Output, State, ALL

from server import app


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = [
        fac.AntdComment(
            id='comment-demo',
            authorName='费弗里',
            authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
            publishTime={
                'value': '2024-01-01 19:29:01',
                'format': 'YYYY-MM-DD hh:mm:ss',
            },
            commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
            defaultAction='liked',
            likesCount=1,
        ),
        fac.AntdSpace(
            [
                fac.AntdInput(
                    id='comment-demo-input',
                    placeholder='发表你的感想...',
                    mode='text-area',
                    maxLength=140,
                    allowClear=True,
                    showCount=True,
                    style={'width': '100%'},
                ),
                fac.AntdButton(
                    '提交评论',
                    id='comment-demo-submit',
                    type='primary',
                    style={'float': 'right'},
                ),
            ],
            size='large',
            direction='vertical',
            style={'width': '100%'},
        ),
    ]

    return demo_contents


@app.callback(
    [Output('comment-demo', 'children'), Output('comment-demo-input', 'value')],
    [
        Input('comment-demo-submit', 'nClicks'),
        Input({'type': 'comment-demo-children', 'index': ALL}, 'deleteClicks'),
    ],
    [State('comment-demo-input', 'value'), State('comment-demo', 'children')],
    prevent_initial_call=True,
)
def comment_demo_add_children_callback(nClicks, deleteClicks, value, children):
    # 本次回调由子回复删除功能触发
    if 'deleteClicks' in dash.callback_context.triggered[0]['prop_id']:
        triggerIndex = eval(
            dash.callback_context.triggered[0]['prop_id'].replace(
                '.deleteClicks', ''
            )
        )['index']

        return [
            child
            for child in children
            if child['props']['id']['index'] != triggerIndex
        ], dash.no_update

    if value:
        return children + [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ] if children else [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ], None

    else:
        return children, None


code_string = [
    {
        'code': """
[
    fac.AntdComment(
        id='comment-demo',
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        defaultAction='liked',
        likesCount=1,
    ),
    fac.AntdSpace(
        [
            fac.AntdInput(
                id='comment-demo-input',
                placeholder='发表你的感想...',
                mode='text-area',
                maxLength=140,
                allowClear=True,
                showCount=True,
                style={'width': '100%'},
            ),
            fac.AntdButton(
                '提交评论',
                id='comment-demo-submit',
                type='primary',
                style={'float': 'right'},
            ),
        ],
        size='large',
        direction='vertical',
        style={'width': '100%'},
    ),
]

...

@app.callback(
    [Output('comment-demo', 'children'), Output('comment-demo-input', 'value')],
    [
        Input('comment-demo-submit', 'nClicks'),
        Input({'type': 'comment-demo-children', 'index': ALL}, 'deleteClicks'),
    ],
    [State('comment-demo-input', 'value'), State('comment-demo', 'children')],
    prevent_initial_call=True,
)
def comment_demo_add_children_callback(nClicks, deleteClicks, value, children):
    # 本次回调由子回复删除功能触发
    if 'deleteClicks' in dash.callback_context.triggered[0]['prop_id']:
        triggerIndex = eval(
            dash.callback_context.triggered[0]['prop_id'].replace(
                '.deleteClicks', ''
            )
        )['index']

        return [
            child
            for child in children
            if child['props']['id']['index'] != triggerIndex
        ], dash.no_update

    if value:
        return children + [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ] if children else [
            fac.AntdComment(
                id={
                    'type': 'comment-demo-children',
                    'index': str(uuid.uuid4()),
                },
                authorName='dash学习者',
                publishTime={
                    'value': datetime.now().strftime('%Y-%m-%d %H:%M:%S'),
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent=value,
                showReply=False,
                showDelete=True,
            )
        ], None

    else:
        return children, None
"""
    }
]

```

### `views/AntdComment/demos/basic_usage.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdComment(
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
)
"""
    }
]

```

### `views/AntdComment/demos/custom_avatar.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdComment(
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        avatarProps={
            'mode': 'image',
            'src': '/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
        },
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={
        'mode': 'image',
        'src': '/assets/imgs/components/AntdAvatar/avatar-demo.jpg',
    },
)
"""
    }
]

```

### `views/AntdComment/demos/from_now.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdComment(
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
        fromNow=True,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
    fromNow=True,
)
"""
    }
]

```

### `views/AntdComment/demos/initial_status.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdComment(
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        defaultAction='liked',
        likesCount=1,
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdComment(
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    defaultAction='liked',
    likesCount=1,
)
"""
    }
]

```

### `views/AntdComment/demos/nested.py`
```python
import feffery_antd_components as fac
from dash.dependencies import Component


def render() -> Component:
    """渲染当前演示用例"""

    # 构造演示用例相关内容
    demo_contents = fac.AntdComment(
        [
            fac.AntdComment(
                authorName='dash爱好者',
                publishTime={
                    'value': '2024-01-01 19:34:19',
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent='资瓷一个！😊',
            ),
            fac.AntdComment(
                authorName='dash-player',
                publishTime={
                    'value': '2024-01-01 19:40:29',
                    'format': 'YYYY-MM-DD hh:mm:ss',
                },
                commentContent='我要好好学习dash和fac，争取早日开发出自己的个人博客网站！',
            ),
        ],
        authorName='费弗里',
        authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
        publishTime={
            'value': '2024-01-01 19:29:01',
            'format': 'YYYY-MM-DD hh:mm:ss',
        },
        commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
        avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
    )

    return demo_contents


code_string = [
    {
        'code': """
fac.AntdComment(
    [
        fac.AntdComment(
            authorName='dash爱好者',
            publishTime={
                'value': '2024-01-01 19:34:19',
                'format': 'YYYY-MM-DD hh:mm:ss',
            },
            commentContent='资瓷一个！😊',
        ),
        fac.AntdComment(
            authorName='dash-player',
            publishTime={
                'value': '2024-01-01 19:40:29',
                'format': 'YYYY-MM-DD hh:mm:ss',
            },
            commentContent='我要好好学习dash和fac，争取早日开发出自己的个人博客网站！',
        ),
    ],
    authorName='费弗里',
    authorNameHref='https://github.com/CNFeffery/feffery-antd-components',
    publishTime={
        'value': '2024-01-01 19:29:01',
        'format': 'YYYY-MM-DD hh:mm:ss',
    },
    commentContent='我希望feffery-components项目系列组件可以帮助更多人快速开发心仪的应用！😀',
    avatarProps={'mode': 'image', 'src': '/assets/imgs/avatar-demo.jpg'},
)
"""
    }
]

```
