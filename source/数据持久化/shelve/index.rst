shelve
==========

.. py:module:: shelve

`shelve` 是一个持久的、类似于字典的对象。与 `dbm` 数据库的不同之处在于，`shelve` 中的值(而不是键!)
本质上可以是任意的 `Python`_ 对象，`pickle` 模块可以处理的任何对象。
这包括大多数类实例、递归数据类型和包含大量共享子对象的对象。键是普通的字符串。


.. _shelve-open:

.. py:method:: shelve.open(filename, flag='c', protocol=None, writeback=False)

    :param filename: 文件名，可以包含后缀，但是只会当作文件名处理

    :param flag: `r` 读、`w` 写、`c` 创建、`n` 总是创建新的。如果数据库不存在，`r` 和 `w` 将失败;
                    `c` 只在不存在的情况下创建; `n` 总是创建一个新的数据库。

    :param protocol: 指定 pickle protocol 版本

    :param writeback: 默认 False，True 将会将所有从数据库中读取的对象存放到一个内存缓存

    :type filename: str

    :type flag: str

    :type protocol: int

    :type writeback: bool

    示例：

    >>> #encoding:utf-8
    >>>
    >>> import shelve
    >>> d = shelve.open('./tmp.txt')
    >>> d['d'] = {"a":"a"}
    >>> d.close()

    打开一个持久化字典。指定的文件名是基础数据库的基本文件名。
    一个副作用是，文件名中可能会添加一个扩展名，并可能创建多个文件。
    默认情况下，将打开底层数据库文件进行读写。可选的标志参数与 :ref:`dbm.open() <dbm.open>` 的标志参数具有相同的解释。

    默认情况下，版本 3 `pickle` 用于序列化值，可以使用 `protocol` 参数指定 `pickle` protocol 的版本。

    由于 `Python`_ 语义的原因， `shelve` 无法知道可变的持久化字典条目何时被修改。
    默认情况下修改对象写只有当分配给书架上(见示例)。
    如果可选的 `writeback` 参数设置为 `True`，所有被访问的条目也都缓存在内存中，并在 :ref:`sync() <shelve.sync>` 和 :ref:`close() <shelve.close>`
    上写回，这可以使修改持久化字典中的可变项变得更方便。
    但是，如果访问了许多项，则会消耗大量缓存内存，而且由于所有访问的项都被写回，关闭操作会变得非常慢
    (无法确定哪些访问的项是可变的，也无法确定哪些实际上发生了改变)。

    .. note::

        不要依赖 shelf 自动关闭;当您不再需要它时，总是显式地调用 :ref:`close() <shelve-close>`
        ，或者使用 :ref:`shelve.open() <shelve-open>` 作为上下文管理器:
        ::
            with shelve.open('spam') as db:
                db['eggs'] = 'eggs'


    .. warning::

        因为 `shelve` 模块是由 :ref:`pickle <pickle>` 支持的，所以从不可信的源加载 shelf 是不安全的。
        与 :ref:`pickle <pickle>` 类似，加载 shelf 可以执行任意代码。

    `Shelf` 对象支持字典支持的所有方法。这简化了从基于字典的脚本到需要持久存储的脚本的转换。

    另外还支持两种方法:

.. _shelve-sync:

.. py:method:: shelf.sync()

    如果 `shelf` 被打开且 `writeback` 设置为 `True`，则将缓存中的所有条目写回。
    如果可行，清空缓存并同步磁盘上的持久字典。当使用 :ref:`close() <shelve-close>` 关闭 `shelf`
    时，将自动调用此函数。

.. _shelve-close:

.. py:method:: shelf.close()

    同步并关闭持久 `dict` 对象。对封闭架的操作将失败，并带有一个 :ref:`ValueError
    <OSError-ValueError>` 错误。


.. hint::

    `持久字典 repice`_ 广泛支持的存储格式并且具有本地字典的速度。

.. _Python: https://python.org
.. _持久字典 repice: https://code.activestate.com/recipes/576642/
