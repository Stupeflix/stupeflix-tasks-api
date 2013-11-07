.. highlight:: js

API Reference
=============

General notes
-------------

All requests are done over SSL.

All strings must be UTF-8 encoded.

POST requests parameters are passed in JSON-encoded bodies.

All dates are in `ISO8601 <http://en.wikipedia.org/wiki/ISO_8601>`_ format.


Authentication
--------------

Requests that create tasks such as :http:method:`v2_create` require
authentication. There are two methods to authenticate requests:

.. _v2_secret_key:

Secret key
~~~~~~~~~~

This kind of authentication should only be used for server to server requests,
as it exposes your secret key.

For POST and DELETE requests, the secret key can be passed as a top level
"secret" key in the JSON body::

    {
        "secret": "123456",
        "tasks": {
            "task_name": "image.info", 
            "url": "http://files.com/image.jpg"
        }
    }

The secret key can also be passed via the ``Authorization`` header. The key
should be prefixed by the string ``Secret``, with a whitespace separating the
two strings::

    Authorization: Secret 123456

For GET requests, the secret key must be passed in the querystring:

.. code-block:: none

    https://dragon.stupeflix.com/v2/storage/files?secret=123456

.. _v2_api_key_referer_auth:

Api key + referrer
~~~~~~~~~~~~~~~~~~

As for :ref:`v2_secret_key` authentication, the api key can be passed in the
request JSON body or the ``Authorization`` header:

* in the JSON body::

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
whitelist.

This kind of authentication is what you should use in your javascript code, but
be careful as requests can easilly be forged to fake the ``Referrer`` header.


HTTP Status codes
-----------------

200
    Operation was successful.

400
    Invalid request. The response body contains a description of the errors,
    for example if you forgot the ``tasks`` parameter in a
    :http:method:`v2_create` request::

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

Task are defined by objects with at least a "task_name" key. :doc:`storage`
parameters can be passed in the "task_store" key. Other keys contain the task
parameters. Here is an example of a ``image.info`` task definition, with the
result stored on the :ref:`storage_volatile` storage system::

    {
        "task_name": "image.info", 
        "task_store": {
            "type": "volatile"
        },
        "url": "http://files.com/image.jpg"
    }


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

Statuses contain at minimum the following keys:    

* "status": the current step of the task in the execution pipeline, one of
  "queued", "executing, "success" or "error"
* "key": the server-side key used to identify the task
* "progress": a value representing task progress; its type depends on the
  task and could be anything that is JSON-encodable
* "events": an object containing chronological events of the task:
    * "queued": date at which the task was queued
    * "started": date at which the task has been attributed to a worker
    * "completed": completion date of the task

When a task completes successfully (with ``"status": "success"``), its status
contains an additional "result" key, for example::

    {
        "status": "success",
        "progress": null,
        "events": {
            "completed": "2013-10-31T14:54:52.689272+00:00",
            "queued": "2013-10-31T14:54:51.987459+00:00"
        },
        "key": "UM6EFJKQWMVON5N3CBKPV52NHE",
        "result": {
            "exposure_time": 0.00156,
            "date_time": "2009:11:02 01:21:55",
            "content_type": "image/jpeg",
            "flash": false,
            "height": 1320,
            "width": 1918,
            "iso_speed": 640,
            "focal_length": 2800,
            "alpha": false,
            "rotation": null,
            "type": "image"
        }
    }

Tasks that ended on an error (with ``"status": "error"``) will return a
status with an "error" key. "error" can have two forms:

* a string containing the error message

* for input parameters validation errors, an object describing the
  validation problems, for example::

    {
        "status": "error",
        "progress": null,
        "events": {
            "completed": "2013-09-20T12:56:49.385937+00:00",
            "queued": "2013-09-20T12:56:49.369911+00:00"
        },
        "key": "QJZTXA3LNZKQ6X4RPGQ5EHRSMI",
        "error": {
            "parameters": {
                "url": [
                    "this field is required"
                ]
            }
        }
    }


Tasks results
-------------

By default, output files are stored forever on Amazon S3. Other storage
backends are available, see :doc:`storage` for a complete reference.


Tasks API methods
-----------------

.. http:method:: POST /v2/create
    :label-name: v2_create
    :title: /v2/create

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


.. http:method:: POST /v2/create_file/{filename}
    :label-name: v2_create_file_post
    :title: /v2/create_file (POST)

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
        a 404 is returned if "filename" is invalid or missing. The response
        body contains hints about the error::

            {
                "status": "error", 
                "error": "'medium' is not a valid filename, choose one of: 'small', 'large'"
            }        

    :response 400:
        invalid request, or the task failed in some way. In the latter case,
        the task status is returned::

            {
                "status": "error",
                "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ",
                "error": "File 'http://files.com/cat.jpeg' is not a valid image file",
                "events": {
                    "queued": "2013-04-03T15:47:27.703717+00:00",
                    "completed": "2013-04-03T15:47:27.729026+00:00"
                }
            }


.. http:method:: GET /v2/create_file/{filename}
    :label-name: v2_create_file_get
    :title: /v2/create_file (GET)

    This is the GET version of :http:method:`v2_tasks_file_post`, allowing to
    create a task, and redirect to one of its output files by using GET
    semantics.
    
    It can be useful for cases where you want to use directly the result of a
    task but can't issue a POST. For example you could create a thumbnail
    directly in an image tag:

    .. code-block:: html
    
        <img src="https://dragon.stupeflix.com/v2/create_file/cat.jpg?task_name=image.thumb&url=http://foo.com/cat.jpg&secret=123456" />

    :arg filename: 
        used to select the desired file, for tasks that output multiple files.
        Can be omited for tasks that output a single file.

    :param task_name:
        task name.

    :param \*:
        remaining querystring parameters are the parameters of the task.

    :response:
        returns the same responses as :http:method:`v2_create_file_post`.


.. http:method:: POST /v2/create_stream
    :label-name: v2_create_stream
    :title: /v2/create_stream

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


.. http:method:: GET /v2/status
    :label-name: v2_status
    :title: /v2/status

    Query the status of one or more tasks.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v2/status?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M&block=true

    :param tasks:
        one or more tasks keys.

    :param block:
        a boolean indicating if the call should return immediately with the
        current status of the task, or wait for all tasks to complete and
        return their final status.

    :response:
        a list of task statuses, see :http:method:`v2_create` for a response
        example.


.. http:method:: POST /v2/status
    :label-name: v2_status_post
    :title: /v2/status

    Same as :http:method:`v2_status` but using POST semantics. Usefull when there
    are too much tasks to query and the querystring size limit is reached.


.. http:method:: GET /v2/status_stream
    :label-name: v2_status_stream
    :title: /v2/status_stream

    Get status streams of one or more tasks.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v2/stream?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M

    :param tasks:
        one or more tasks keys.

    :response:
        a stream of status updates. See :http:method:`v2_create_stream` for a
        description of the output.


.. http:method:: POST /v2/status_stream
    :label-name: v2_status_stream_post
    :title: /v2/status_stream        

    Same as :http:method:`v2_status_stream` but using POST semantics. Usefull when
    there are too much tasks to query and the querystring size limit is
    reached.


.. http:method:: GET /v2/file/{filename}
    :label-name: v2_file
    :title: /v2/file

    Wait for an existing task to complete and redirect to its output.

    Example request:

    .. code-block:: none

        https://dragon.stupeflix.com/v2/file/cat.jpg?task=6GRQ3H5EHU7GXUTIOSS2GUDPGQ

    :arg filename: 
        used to select the desired file, for tasks that output multiple files.
        Can be omited for tasks that output a single file.

    :param task:
        the task key.

    :response:
        returns the same responses as :http:method:`v2_create_file_post`.


.. _v2_storage_api:        

Storage API methods
-------------------

.. http:method:: GET /v2/storage/files/{path}
    :label-name: v2_storage_files_get
    :title: /v2/storage/files (GET)

    List tasks output files.

    :arg path: the path of the directory to list.
    :optparam recursive: 
        a boolean value indicating if *path* sub-directories
        must be traversed too.
    :response: 
        a mapping containing the lists of files and directories, and storage
        space used by these files::

            {
                "files": [
                    [
                        "dragon-image.thumb-IeWutW",
                        4293,
                        "2013-10-28T20:22:21.000Z"
                    ]
                ],
                "directories": [
                    "XDJC6DIS5UDSFBBOLXWMN27ORI/"
                ],
                "usage": 4293
            }

        All paths are relative to the parent *path*. File entries are of the
        form ``[name, size, last_modified]``.


.. http:method:: DELETE /v2/storage/files/{path}
    :label-name: v2_storage_files_delete
    :title: /v2/storage/files (DELETE)

    Delete tasks output files.

    If *path* is empty, recursively delete all output files.

    If *path* points to a directory, recursively delete all output files under
    this directory.

    If *path* points to a file, delete this file.

    Files can also be targeted by date with the *from*, *to* and *max_age*
    parameters. *from* and *to* dates must be `ISO8601
    <http://en.wikipedia.org/wiki/ISO_8601>`_ date time strings; if they don't
    include a timezone they will be interpreted as UTC.

    :arg path: the path of the file or directory to delete.
    :optparam dry_run: 
        if this boolean is true, return the files that would be deleted, but
        don't actually delete them (default: ``false``).
    :optparam from: the date from which point to delete files.
    :optparam to: the date up to which point to delete files.
    :optparam max_age: files older than *max_age* days are deleted.
    :response: 
        a mapping containing the list of deleted files, the number of bytes
        freed and the (approximate) total space used on the storage after the
        operation::

            {
                "files": [
                    "BCSIT5KDDQQTC7GZ6TBJE7NFIU/dragon-image.thumb-9b0E9P",
                    "XDJC6DIS5UDSFBBOLXWMN27ORI/dragon-image.thumb-IeWutW"
                ],
                "freed": 1257,
                "usage": 6578
            }

.. http:method:: POST /v2/storage/expiration
    :label-name: v2_storage_expiration_post
    :title: /v2/storage/expiration (POST)

    Change lifetime of tasks output files.

    :param days: 
        the number of days after which files are deleted in the tasks output
        storage. A value of 0 means that files are never deleted.


.. http:method:: GET /v2/storage/expiration
    :label-name: v2_storage_expiration_get
    :title: /v2/storage/expiration (GET)

    Get the current lifetime of tasks output files.

    :response: 
        the current lifetime of files, in days. A value of 0 means that
        files are never deleted.
