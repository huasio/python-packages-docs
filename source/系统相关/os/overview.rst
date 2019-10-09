简介
=========

该模块提供了一些方便使用操作系统相关功能的函数。

关于这些函数的可用性的说明：

* 所有 `Python`_ 内建的操作系统相关的模块的设计都是为了使得在同一功能可用的情况下，保持接口的一致性；例如，函数 :ref:`os.stat(path) <os-stat>` 以相同的格式返回关于 `path` 的统计信息（这个函数同时也是起源于 :ref:`POSIX`）。

* 针对特定的操作的拓展同样在可用于 `os` 模块，但是使用它们必然会对可移植性产生威胁。

* 所有接受路径或文件名的函数都同时支持字节串和字符串对象，并在返回路径或文件名时使用相应类型的对象作为结果。

.. note::
    如果文件名和路径无效或不可访问，或者其他参数的类型正确，但操作系统不接受，则此模块中的所有函数都会引发 :ref:`OSError <OSError>`
    (或其子类)。

- exception os.error
    内建的 OSError 异常的一个别名。

- os.name
    导入的依赖特定操作系统的模块的名称。以下名称目前已注册: ``posix``, ``nt``, ``java``.



.. hint::
     :ref:`sys.platform <sys.platform>` 有更详细的描述. :ref:`os.uname() <os-uname>`
     只给出系统提供的版本信息。:ref:`platform <sys.platform>`
     模块对系统的标识有更详细的检查。


.. _Python: https://www.python.org/
