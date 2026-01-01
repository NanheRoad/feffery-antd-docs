

- id (string; optional):
    组件唯一id.

- key (string; optional):
    对当前组件的`key`值进行更新，可实现强制重绘当前组件的效果.

- children (a list of or a singular dash component, string or number; optional):
    组件型，内嵌元素.

- token (dict; optional):
    监听当前组件所在作用范围对应的样式`token`参数，需配合上层`AntdConfigProvider`组件使用.