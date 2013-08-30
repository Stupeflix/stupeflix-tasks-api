.. highlight:: js

REST API Documentation
======================

General notes
-------------

All requests are done over SSL.

All strings must be UTF-8 encoded.

POST requests parameters are passed in JSON-encoded bodies.

Dates are returned in ISO8601 format.

Authentication
--------------

Requests that create tasks such as :http:method:`create` require
authentication. There are two methods to authenticate requests:

.. _secret_key:

Secret key
~~~~~~~~~~

You can add your secret key to requests parameters, here for example for the
:http:method:`create` method::

    {
        "secret": "123456",
        "tasks": {
            "task_name": "image.info", 
            "url": "http://files.com/image.jpg"
        }
    }

The secret key can also be passed via the ``Authorization`` header. The key
should be prefixed by the string ``Secret``, with whitespace separating the two
strings::

    Authorization: Secret 123456

This kind of authentication should only be used for server to server requests.    

.. _api_key_referer_auth:

Api key + referrer
~~~~~~~~~~~~~~~~~~

As for :ref:`secret_key` authentication, the api key can be passed in the
request parameters or the ``Authorization`` header:

* in request parameters::

    {
        "api_key": "654321",
        "tasks": {
            "task_name": "image.info", 
            "url": "http://files.com/image.jpg"
        }
    }

* in the ``Authorization`` header::

    Authorization: Api-Key 654321

The ``Referrer`` header of the request must also be in your account's
whitelist. This kind of authentication is what you should use in your
javascript code.


HTTP Status codes
-----------------

200
    Operation was successful.

400
    Invalid request parameters. The response body contains a description of the
    errors, for example if you forgot the ``tasks`` parameter in a
    :http:method:`create` request::

        {
            "status": "error", 
            "errors": [
                {
                    "name": "tasks",
                    "location": "body", 
                    "description": "tasks is missing"
                }
            ]
        }

401
    Invalid credentials, or account limits reached.


Tasks definitions
-----------------

Task are defined by objects with at least a ``task_name`` key. Other keys
contain the task parameters. Here is an example of a ``image.info`` task
definition, which takes an ``url`` parameter::

    {"task_name": "image.info", "url": "http://files.com/image.jpg"}


Tasks statuses format
---------------------

Tasks statuses are objects of the form::

    {
        "status": "executing",
        "key": "5OYA5JQVFIAHYOMLQG5QV3U33M",
        "progress": 90,
        "events": {
            "started": "2013-04-03T15:47:27.707526+00:00", 
            "queued": "2013-04-03T15:47:27.703674+00:00"
        }
    }

Here are the descriptions of the keys:    

    * ``status``: the current step of the task in the execution pipeline, one of
      "queued", "executing, "success" or "error"
    * ``key``: the server-side key used to identify the task
    * ``progress``: a value representing task progress; its type depends on the
      task and could be anything that is JSON-encodable
    * ``events``: an object containing chronological events of the task:
        * ``queued``: date at which the task was queued
        * ``started``: date at which the task has been attributed to a worker
        * ``completed``: completion date of the task

Tasks results (with a ``status`` "success" or "error") also contain an
additional ``result`` key, containing the task result for successful tasks, or
the error message for tasks that fail.


API Methods
-----------

.. http:method:: POST /v1/create
    :label-name: create
    :title: /v1/create

    Queue one or more tasks and return a list of tasks status.

    Here is an example request creating two tasks::

        {
            "tasks": [
                {"task_name": "image.info", "url": "http://files.com/image.jpg"},
                {"task_name": "image.thumb", "url": "http://files.com/image.jpg"}
            ]
        }

    :param tasks: 
        a list containing the definitions of the tasks to execute. The method
        also accepts a single task definition for convenience.

    :optparam block:
        a boolean indicating if the call should return immediately with the
        current status of the tasks, or wait for all tasks to complete and
        return their final status.

    :response:
        a list of task statuses::

            [
                {
                    "status": "queued", 
                    "events": {"queued": "2013-04-03T15:47:27.703674+00:00"}, 
                    "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"
                }, 
                {
                    "status": "queued", 
                    "events": {"queued": "2013-04-03T15:47:27.703717+00:00"}, 
                    "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"
                }
            ]


.. http:method:: POST /v1/create_file/{filename}
    :label-name: create_file_post
    :title: /v1/create_file (POST)

    Queue a task, block until it's finished and redirect to its output file. 

    Example request::

        {
            "task": {"task_name": "image.thumb", "url": "http://files.com/image.jpg"}
        }

    :arg filename: 
        used to select the desired file, for tasks that output multiple files.
        Can be omited for tasks that output a single file.

    :param task:
        a task definition.

    :response 302:
        a redirect to the selected task output file.

    :response 404:
        a 404 is returned if the ``filename`` parameter is invalid or missing.
        The response body contains hints about the error::

            {
                "status": "error", 
                "message": "'medium' is not a valid filename, choose one of: 'small', 'large'"
            }        

    :response 400:
        invalid request, or the task failed in some way. In the latter case,
        the task status is returned::

            {
                "status": "error",
                "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ",
                "result": "File 'http://files.com/cat.jpeg' is not a valid image file",
                "events": {
                    "queued": "2013-04-03T15:47:27.703717+00:00",
                    "completed": "2013-04-03T15:47:27.729026+00:00"
                }
            }


.. http:method:: GET /v1/create_file/{filename}
    :label-name: create_file_get
    :title: /v1/create_file (GET)

    This is the GET version of :http:method:`tasks_file_post`, allowing to
    create a task, and redirect to one of its output files by using GET
    semantics.
    
    It can be useful for cases where you want to use directly the result of a
    task but can't issue a POST. For example you could create a thumbnail
    directly in an image tag:

    .. code-block:: html
    
        <img src="https://dragon.stupeflix.com/v1/create_file/cat.jpg?task_name=image.thumb&url=http://foo.com/cat.jpg" />

    :arg filename: 
        used to select the desired file, for tasks that output multiple files.
        Can be omited for tasks that output a single file.

    :param task_name:
        task name.

    :param \*:
        remaining querystring parameters are the parameters of the task.

    :response:
        returns the same responses as :http:method:`create_file_post`.


.. http:method:: POST /v1/create_stream
    :label-name: create_stream
    :title: /v1/create_stream

    Queue one or more tasks, and stream their status updates.

    Example request::

        {
            "tasks": [
                {"task_name": "hello", "name": "John"},
                {"task_name": "hello", "name": "Jane"},
            ]
        }

    :param tasks:
        a list containing the definitions of the tasks to execute.

    :response:
        here is a sample response for the two tasks above::

            [{"status": "queued", "events": {"queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}, {"status": "queued", "events": {"queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}]
            {"status": "executing", "events": {"started": "2013-04-03T15:47:27.707526+00:00", "queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}
            {"status": "executing", "events": {"started": "2013-04-03T15:47:27.710286+00:00", "queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}
            {"status": "success", "result": "Hello John", "events": {"completed": "2013-04-03T15:47:27.726229+00:00", "queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}
            {"status": "success", "result": "Hello Jane", "events": {"completed": "2013-04-03T15:47:27.729026+00:00", "queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}        

        The first line of the response contains a list with the immediate
        statuses of the tasks. The list is in the same order as the ``tasks``
        parameter, to allow the client to know which key correspond to which
        task.

        The next lines contains interleaved statuses of the two tasks. The
        response is closed when all the tasks have finished.


.. http:method:: GET /v1/status
    :label-name: status
    :title: /v1/status

    Query the status of one or more tasks.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v1/status?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M&block=true

    :param tasks:
        one or more tasks keys.

    :param block:
        a boolean indicating if the call should return immediately with the
        current status of the task, or wait for all tasks to complete and
        return their final status.

    :response:
        a list of task statuses, see :http:method:`create` for a response
        example.


.. http:method:: GET /v1/status_stream
    :label-name: status_stream
    :title: /v1/status_stream

    Get status streams of one or more tasks.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v1/stream?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M

    :param tasks:
        one or more tasks keys.

    :response:
        a stream of status updates. See :http:method:`create_stream` for a
        description of the output.


.. http:method:: GET /v1/file/{filename}
    :label-name: file
    :title: /v1/file

    Wait for an existing task to complete and redirect to its output.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v1/file/cat.jpg?task=6GRQ3H5EHU7GXUTIOSS2GUDPGQ

    :arg filename: 
        used to select the desired file, for tasks that output multiple files.
        Can be omited for tasks that output a single file.

    :param task:
        the task key.

    :response:
        returns the same responses as :http:method:`create_file_post`.
