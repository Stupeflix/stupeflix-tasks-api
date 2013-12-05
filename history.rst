History
=======

??? -- /v2 API
--------------

:doc:`index` introduces :doc:`storage`.

Tasks result objects also slightly change in this versions. Details of errors
are now returned in the "error" key, instead of "result". This avoids mixing
successes and errors in code that doesn't check the "status" key.

09/04/2013 -- /v1 API
---------------------

This is the first release of our API.

