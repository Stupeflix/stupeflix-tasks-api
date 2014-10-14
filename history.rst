History
=======

10/02/2013 -- /v2 API
---------------------

Added support for :doc:`storage`.

Tasks result objects also slightly change in this versions. Details of errors
are now returned in the "error" key, instead of "result". This avoids mixing
successes and errors in code that doesn't check the "status" key. See
:doc:`api` for details.

09/04/2013 -- /v1 API
---------------------

This is the first release of our API.

