Callbacks and Errbacks
======================

All tasks accept a ``url_callback`` and ``url_errback`` argument, that allows
to specify a HTTP endpoint that will be called when the task is complete.

This alleviates the need to poll :http:method:`v2_status` to check if a task
was completed and simplifies asynchronous code if you need to queue many tasks
at once.

The callback endpoint will receive a POST containing the full task status as
soon as the task ends (the same JSON that you would get on
:http:method:`v2_status`).  Note that the request is not form-encoded, the POST
request body contains directly the status in JSON.

.. warning::
    If you poll :http:method:`v2_status` just after receiving the callback, it
    will most likely return an "executing" status. This is expected, because it
    takes some time for the status to propagate to the database. This is also
    unneeded, since the final status is contained in the callback request body.
