

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- className (string | dict; optional):
    当前组件css类名，支持[动态css](/advanced-classname).

- wrapperClassName (string | dict; optional):
    外层容器css类名.

- spinning (boolean; default False):
    是否处于加载中状态.

- size (a value equal to: 'small', 'middle', 'large'; default 'middle'):
    默认加载状态图标的尺寸，可选项有`'small'`、`'middle'`、`'large'`  默认值：`'middle'`.

- delay (number; optional):
    加载动画渲染延时，单位：毫秒  默认值：`0`.

- text (string; optional):
    加载动画提示文字.

- fullscreen (boolean; default False):
    是否开启全屏模式  默认值：`False`.

- debug (boolean; default False):
    是否开启debug模式，开启后，每次动画加载都会在开发者工具的控制台打印相关`prop`信息  默认值：`False`.

- listenPropsMode (a value equal to: 'default', 'exclude', 'include'; default 'default'):
    监听模式，可选项有`'default'`、`'exclude'`、`'include'`  默认值：`'default'`.

- excludeProps (list of strings; optional):
    `listenPropsMode='exclude'`时，设置需要排除监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- includeProps (list of strings; optional):
    `listenPropsMode='include'`时，设置需要包含监听的回调目标列表，格式如`['组件id1.组件属性1',
    '组件id2.组件属性2', ...]`.

- indicator (a list of or a singular dash component, string or number; optional):
    组件型，自定义加载状态图标.

- manual (boolean; default False):
    是否开启手动控制模式，开启后是否处于加载状态将由`spinning`参数控制，与内部元素参与的回调状态无关
    默认值：`False`.

- percent (number | a value equal to: 'auto'; optional):
    控制加载中状态下的环状进度渲染形式，传入0到100之间数值型时表示实际进度，传入`'auto'`时会预估一个永远不会停止的进度.

- data-* (string; optional):
    `data-*`格式属性通配.

- aria-* (string; optional):
    `aria-*`格式属性通配.