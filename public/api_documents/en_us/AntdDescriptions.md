

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，传入内部各描述列表子项.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- styles (dict; optional):
    细分控制子元素css样式.

    `styles` is a dict with keys:

    - root (dict; optional):
        根元素css样式.

    - header (dict; optional):
        头部元素css样式.

    - title (dict; optional):
        标题元素css样式.

    - extra (dict; optional):
        额外内容css样式.

    - label (dict; optional):
        标签元素css样式.

    - content (dict; optional):
        内容元素css样式.

- classNames (dict; optional):
    细分控制子元素css类名.

    `classNames` is a dict with keys:

    - root (string; optional):
        根元素css类名.

    - header (string; optional):
        头部元素css类名.

    - title (string; optional):
        标题元素css类名.

    - extra (string; optional):
        额外内容css类名.

    - label (string; optional):
        标签元素css类名.

    - content (string; optional):
        内容元素css类名.

- items (list of dicts; optional):
    配置描述列表子项，优先级高于`children`.

    `items` is a list of dicts with keys:

    - label (a list of or a singular dash component, string or number; optional):
        组件型，子项标题内容.

    - span (number | a value equal to: 'filled'; optional):
        子项所占宽度份数，当设置为`'filled'`时会自适应占满当前行剩余可用空间  默认值：`1`.

    - children (a list of or a singular dash component, string or number; optional):
        组件型，子项内容.

    - style (dict; optional):
        子项css样式.

    - className (string; optional):
        子项css类名.

- title (a list of or a singular dash component, string or number; optional):
    组件型，标题内容.

- column (dict; default 3):
    每行显示的字段项数量，支持响应式  默认值：`3`.

    `column` is a number | dict with keys:

    - xxl (number; optional)

    - xl (number; optional)

    - lg (number; optional)

    - md (number; optional)

    - sm (number; optional)

    - xs (number; optional)

- bordered (boolean; default False):
    是否显示边框  默认值：`False`.

- size (a value equal to: 'small', 'default', 'large'; default 'default'):
    整体尺寸规格，可选项有`'small'`、`'default'`、`'large'`  默认值：`'default'`.

- layout (a value equal to: 'horizontal', 'vertical'; default 'horizontal'):
    布局方式，可选项有`'horizontal'`、`'vertical'`  默认值：`'horizontal'`.

- extra (a list of or a singular dash component, string or number; optional):
    组件型，设置操作区域，显示在右上方.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.