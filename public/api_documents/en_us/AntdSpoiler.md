

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- contentClassName (string | dict; optional):
    内容区css类名，支持[动态css](/advanced-classname).

- contentStyle (dict; optional):
    内容区css样式.

- locale (a value equal to: 'zh-cn', 'en-us', 'de-de', 'ru-ru'; default 'zh-cn'):
    组件文案语种，可选项有`'zh-cn'`（简体中文）、`'en-us'`（英语）、`'de-de'`（德语）、`'ru-ru'`（俄语）
    默认值：`'zh-cn'`.

- hideLabel (a list of or a singular dash component, string or number; optional):
    组件型，展开状态下，收起按钮的文案内容.

- showLabel (a list of or a singular dash component, string or number; optional):
    组件型，收起状态下，展开按钮的文案内容.

- labelPosition (a value equal to: 'left', 'right'; default 'left'):
    展开/收起按钮的位置，可选项有`'left'`、`'right'`  默认值：`'left'`.

- open (boolean; default False):
    监听或设置是否处于展开状态  默认值：`False`.

- maxHeight (number; default 50):
    收起状态下，内容区域最大像素高度  默认值：`50`.

- transitionDuration (number; default 0.1):
    展开/收起过渡动画耗时，单位：秒  默认值：`0.1`.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.