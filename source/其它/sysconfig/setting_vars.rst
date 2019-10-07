配置变量
##########

`Python` 发行版包含一个 `Makefile` 和一个 `pyconfig.h` 头文件，这两个文件对于构建
`Python` 二进制文件本身和使用 `distutils`_ 编译的第三方 `C` 扩展都是必需的。

`sysconfig` 将在这些文件中找到的所有变量放在一个可以使用 ``get_config_vars()`` 或 ``get_config_var()``
访问的字典中。

.. note::
    在 `windows` 上，它的集合要小得多。

.. _sysconfig-get_config_vars:

- sysconfig.get_config_vars(*args)
    如果没有参数，则返回与当前平台相关的所有配置变量的字典。

    使用参数时，返回一个值列表，这些值是通过在配置变量字典中查找每个参数而得到的。

    对于每个参数，如果没有找到值，则返回 ``None``。

.. _sysconfig-get_config_var:

- sysconfig.get_config_var(name)
    返回单个变量名的值。

    相当于 :ref:`get_config_vars().get(name) <sysconfig-get_config_vars>`

    如果没有找到名称，则返回 ``None``。

.. _distutils: https://docs.python.org/zh-cn/3/library/distutils.html?highlight=distutils#module-distutils

用法示例:

>>> import sysconfig
>>> sysconfig.get_config_var('Py_ENABLE_SHARED')
0
>>> sysconfig.get_config_var('LIBDIR')
'/usr/local/lib'
>>> sysconfig.get_config_vars('AR', 'CXX')
['ar', 'g++']
