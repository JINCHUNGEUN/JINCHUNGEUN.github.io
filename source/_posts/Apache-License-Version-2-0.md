---
title: Apache License Version 2.0
date: 2020-04-13 09:48:25
tags:
---

Apache License是著名的非盈利开源组织Apache采用的协议，用于鼓励代码共享和尊重原作者的著作权，同样允许代码修改，再发布（开源或者商业）。需要满足的条件：
1. 需要给代码的用户一份Apache License
2. 如果修改了代码，需要在被修改的文件中说明
3. 在延伸的代码中（修改和有源代码衍生的代码中）需要带有原来的代码中的协议、商标、专利声明和其他原来作者规定需要包含的说明
4. 如果再发布的产品中包含一个Notice文件，则在Notice文件中需要带有Apache License。

使用Apache License 2.0协议的好处
- 永久权利，一旦被授权，永久拥有
- 全球范围的权利，在一个国家获得授权，适用于所有国家
- 授权免费无版税，前期、后期均无任何费用
- 授权无排他性，任何人都可以获得授权
- 授权不可撤销，一旦获得授权，没有任何人可以取消。

样例：
```
# Copyright 2014-present MongoDB, Inc.
#
# Licensed under the Apache License, Version 2.0 (the "License"); you
# may not use this file except in compliance with the License.  You
# may obtain a copy of the License at
#
# http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or
# implied.  See the License for the specific language governing
# permissions and limitations under the License.

"""Class to monitor a MongoDB server on a background thread."""

import weakref

from pymongo import common, periodic_executor
from pymongo.errors import OperationFailure
from pymongo.monotonic import time as _time
from pymongo.read_preferences import MovingAverage
from pymongo.server_description import ServerDescription
from pymongo.server_type import SERVER_TYPE
from pymongo.srv_resolver import _SrvResolver


class MonitorBase(object):
    def __init__(self, *args, **kwargs):
        """Override this method to create an executor."""
        raise NotImplementedError

    def open(self):
        """Start monitoring, or restart after a fork.

        Multiple calls have no effect.
        """
        self._executor.open()

    def close(self):
        """Close and stop monitoring.

        open() restarts the monitor after closing.
        """
        self._executor.close()

    def join(self, timeout=None):
        """Wait for the monitor to stop."""
        self._executor.join(timeout)

    def request_check(self):
        """If the monitor is sleeping, wake it soon."""
        self._executor.wake()
```