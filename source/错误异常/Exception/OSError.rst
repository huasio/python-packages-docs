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

.. _OSError-ValueError:

- exception ValueError
    当操作或函数接收到具有正确类型但值不适合的参数，并且情况不能用更精确的异常例如 :ref:`IndexError
    <OSError-IndexError>` 来描述时将被引发。

.. _OSError-LookupError:

- exception LookupError
    此基类用于派生当映射或序列所使用的键或索引无效时引发的异常: ``IndexError``, ``KeyError``。

    这可以通过 :ref:`codecs.lookup() <codecs-lookup>` 来直接引发。

    .. _OSError-IndexError:

    - exception IndexError
        当序列抽取超出范围时将被引发。 （切片索引会被静默截短到允许的范围；如果指定索引不是整数则 :ref:`TypeError
        <OSError-TypeError>` 会被引发。）

    .. _OSError-KeyError:

    - exception KeyError
        当在现有键集合中找不到指定的映射（字典）键时将被引发。
