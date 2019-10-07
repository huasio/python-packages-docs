OSError
###########

.. _OSError:

- exception OSError([arg])
    ...... 详细同下

- exception OSError(errno, strerror[, filename[, winerror[, filename2]]])


.. _OSError-FileNotFoundError:

- exception FileNotFoundError
    当所请求的文件或目录不存在时将被引发。 对应于 errno ENOENT。


.. _OSError-PermissionError:

- exception PermissionError
    当在没有足够操作权限的情况下试图执行某个操作时将被引发 —— 例如缺少文件系统权限。 对应于 errno EACCES 和 EPERM。

.. _OSError-NotADirectoryError:

- exception NotADirectoryError
    当请求对一个非目录对象执行目录操作 (例如 os.listdir()) 时将被引发。 对应于 errno ENOTDIR。

.. _OSError-TypeError:

- exception TypeError
    当一个操作或函数被应用于类型不适当的对象时将被引发。 关联的值是一个字符串，给出有关类型不匹配的详情。

    此异常可以由用户代码引发，以表明尝试对某个对象进行的操作不受支持也不应当受支持。 如果某个对象应当支持给定的操作但尚未提供相应的实现，所要引发的适当异常应为 NotImplementedError。

    传入参数的类型错误 (例如在要求 int 时却传入了 list) 应当导致 TypeError，但传入参数的值错误 (例如传入要求范围之外的数值) 则应当导致 ValueError。
