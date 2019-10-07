进程参数
==========

简介
----------
该模块提供了一些方便使用操作系统相关功能的函数。

关于这些函数的可用性的说明：

* 所有 `Python`_ 内建的操作系统相关的模块的设计都是为了使得在同一功能可用的情况下，保持接口的一致性；例如，函数 :ref:`os.stat(path) <os-stat>` 以相同的格式返回关于 `path` 的统计信息（这个函数同时也是起源于 :ref:`POSIX`）。

* 针对特定的操作的拓展同样在可用于 `os` 模块，但是使用它们必然会对可移植性产生威胁。

* 所有接受路径或文件名的函数都同时支持字节串和字符串对象，并在返回路径或文件名时使用相应类型的对象作为结果。


方法属性
--------

这些函数和数据项提供了操作当前进程和用户的信息。

.. _os-ctermid:

- os.ctermid()
    返回与进程控制终端对应的文件名。

    .. note::
        :ref:`可用性`：Unix

        如：`/dev/tty`

.. _os-environ:

- os.environ
    一个表示字符串环境的 `mapping`_ 对象。
    例如，``environ['HOME']`` 是你的主目录（在某些平台上）的路径名，相当于 `C` 中的 ``getenv("HOME")``。

    这个映射是在第一次导入 `os` 模块时捕获的，通常作为 `Python`_ 启动时处理 `site.py` 的一部分。除了通过直接修改 ``os.environ`` 之外，在此之后对环境所做的更改不会反映在 ``os.environ`` 中。

    如果平台支持 `putenv()`_ 函数，这个映射除了可以用于查询环境外还能用于修改环境。 当这个映射被修改时，`putenv()`_
    将被自动调用。

    在Unix系统上，键和值会使用 :ref:`sys.getfilesystemencoding()
    <getfilesystemencoding>` 和 ``surrogateescape``
    的错误处理。如果你想使用其他的编码，使用 :ref:`os.environb <os-environb>`。

    .. note::
        直接调用 `putenv()`_ 并不会影响 ``os.environ``，所以推荐直接修改 ``os.environ``。
    .. note::
         在某些平台上，包括 `FreeBSD` 和 `Mac OS X`，设置 ``environ`` 可能导致内存泄露。参阅 `putenv()`_
         的系统文档。

    如果平台没有提供 `putenv()`_, 为了使启动的子进程使用修改后的环境，一份修改后的映射会被传给合适的进程创建函数。

    如果平台支持 `unsetenv()`_ 函数，你可以通过删除映射中元素的方式来删除对应的环境变量。当一个元素被从 ``os.environ``
    删除时，以及 ``pop()`` 或 ``clear()`` 被调用时， `unsetenv()`_ 会被自动调用。


.. _os-environb:

- os.environb
    字节版本的 :ref:`environ <os-environ>`: 一个以字节串表示环境的 `mapping`_ 对象。

    :ref:`environ <os-environ>` 和 ``environb`` 是同步的（修改 ``environb`` 会更新
    :ref:`environ <os-environ>`，反之亦然）。

    只有在 :ref:`supports_bytes_environ <os-supports_bytes_environ>` 为 ``True``
    的时候 ``environb`` 才是可用的。

    .. note::
        3.2 新版功能.

.. _os-chdir:

- os.chdir(path)
    将当前工作目录更改为 ``path``。

    这个函数可以支持指定文件描述符，描述符必须指向打开的目录，而不是打开的文件。

    这个函数可以引发 :ref:`OSError <OSError>` 和子类，如
    :ref:`FileNotFoundError <OSError-FileNotFoundError>`、:ref:`PermissionError
    <OSError-PermissionError>`
    和 :ref:`NotADirectoryError <OSError-NotADirectoryError>`。

    .. note::
        3.3 新版功能: 在某些平台上添加了对将 ``path`` 指定为文件描述符的支持。

        在 3.6 版更改: 接受一个 `路径类`_ 。
- os.fchdir(fd)
    将当前工作目录更改为文件描述符 ``fd`` 表示的目录，描述符必须指向打开的目录，而不是打开的文件。

    .. note::
        从 `Python 3.3` 开始，这就相当于 ``os.chdir(fd)``。

        :ref:`可用性`：Unix。

.. _os-getcwd:

- os.getcwd()
    返回表示当前工作目录的字符串。



.. _os-fsencode:

- os.fsencode(filename)
    编码 `路径类`_ 文件名 为文件系统接受的形式，使用 ``surrogateescape``
    代理转义编码错误处理器，在 `Windows` 系统上会使用 ``strict`` ；返回 ``bytes`` 字节类型不变。

    :ref:`fsdecode() <os-fsdecode>` 是此函数的逆向函数。

    .. note::
        3.2 新版功能.

        在 3.6 版更改: 增加对实现了 :ref:`os.PathLike <os-PathLike>` 接口的对象的支持。


.. _os-fsdecode:

- os.fsdecode()
    从文件系统编码方式解码为 路径类 文件名，使用 ``surrogateescape`` 代理转义编码错误处理器，在 `Windows` 系统上会使用
    ``strict`` ；返回 ``str`` 字符串不变。

    :ref:`fsencode() <os-fsencode>` 是此函数的逆向函数。

    .. note::
        3.2 新版功能.

        在 3.6 版更改: 增加对实现了 :ref:`os.PathLike <os-PathLike>` 接口的对象的支持。



- os.fspath(path)
    返回路径的文件系统表示。

    如果传入的是 ``str`` 或 ``bytes`` 类型的字符串，将原样返回。否则 :ref:`__fspath__()
    <os-PathLike-__fspath__>`
    将被调用，如果得到的是一个 ``str`` 或 ``bytes`` 类型的对象，那就返回这个值。其他所有情况则会抛出
    :ref:`TypeError <OSError-TypeError>`  异常。

    .. note::
        3.6 新版功能.


.. _os-stat:

- os.stat(path)

.. _os-PathLike:

- os.PathLike
    描述表示一个文件系统路径的 `抽象基类`_ ，如 ``pathlib.PurePath``。

    .. note::
        3.6 新版功能.

    .. _os-PathLike-__fspath__:

    - abstractmethod __fspath__()
        返回当前对象的文件系统表示。

这个方法只应该返回一个 str 字符串或 bytes 字节串，请优先选择 str 字符串。

.. _os-supports_bytes_environ:

- os.supports_bytes_environ
    如果操作系统上原生环境类型是字节型则为 ``True`` (例如在 `Windows` 上为 ``False``)。

    .. note::
        3.2 新版功能.

.. _Python: https://www.python.org/
.. _mapping: https://docs.python.org/zh-cn/3/glossary.html#term-mapping
.. _putenv(): https://docs.python.org/zh-cn/3/library/os.html?highlight=os#os.putenv
.. _unsetenv(): https://docs.python.org/zh-cn/3/library/os.html?highlight=os#os.unsetenv
.. _路径类: https://docs.python.org/zh-cn/3/glossary.html#term-path-like-object
.. _抽象基类: https://docs.python.org/zh-cn/3/glossary.html#term-abstract-base-class
