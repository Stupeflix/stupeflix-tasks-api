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

Requests that create tasks such as :http:post:`/v2/create` require
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
    :http:post:`/v2/create` request::

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

503
    The system is temporarily down and the client should retry later.


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

Some tasks also support partial results, that are sent before the end of the
task. Partial results are like full results, but their status is "executing"
and the "result" mapping only contains a subset of the final result.

Here is an example partial result for the ``video.create`` task. Note that
"result" only contains the "duration" and "preview" keys, while the final
result would also contain the URLs of the final video and thumbnail image in
the "export" and "thumbnail" keys::

    {
        "status": "executing",
        "result": {
            "duration": 10,
            "preview": "http://bill.stupeflix.com/storage/flvstreamer/222/LY5XZIPILG6WKKIAGQAB4RLHBY/360p/preview.flv"
        },
        "key": "LY5XZIPILG6WKKIAGQAB4RLHBY",
        "progress": 100,
        "events": {
            "started": "2013-11-16T06:02:55.669278+00:00",
            "queued": "2013-11-16T06:02:55.667394+00:00"
        }
    }


Tasks results
-------------

By default, output files are stored forever on Amazon S3 and served through Amazon Cloudflare. Other storage
backends are available, see :doc:`storage` for a complete reference.


Tasks API methods
-----------------

.. http:post:: /v2/create

    Queue one or more tasks and return a list of tasks status.

    **Example request**::

        {
            "tasks": [
                {"task_name": "image.info", "url": "http://files.com/image.jpg"},
                {"task_name": "image.thumb", "url": "http://files.com/image.jpg"}
            ]
        }

    **Example response**::

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


    :<json tasks:
        a list containing the definitions of the tasks to execute. The method
        also accepts a single task definition for convenience.

    :<json block:
        a boolean indicating if the call should return immediately with the
        current status of the tasks, or wait for all tasks to complete and
        return their final status.


.. http:post:: /v2/create_stream

    Queue one or more tasks, and stream their status updates.

    **Example request**::

        {
            "tasks": [
                {"task_name": "hello", "name": "John"},
                {"task_name": "hello", "name": "Jane"},
            ]
        }

    **Example response**::

        [{"status": "queued", "events": {"queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}, {"status": "queued", "events": {"queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}]
        {"status": "executing", "events": {"started": "2013-04-03T15:47:27.707526+00:00", "queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}
        {"status": "executing", "events": {"started": "2013-04-03T15:47:27.710286+00:00", "queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}
        {"status": "success", "result": "Hello John", "events": {"completed": "2013-04-03T15:47:27.726229+00:00", "queued": "2013-04-03T15:47:27.703674+00:00"}, "key": "6GRQ3H5EHU7GXUTIOSS2GUDPGQ"}
        {"status": "success", "result": "Hello Jane", "events": {"completed": "2013-04-03T15:47:27.729026+00:00", "queued": "2013-04-03T15:47:27.703717+00:00"}, "key": "5OYA5JQVFIAHYOMLQG5QV3U33M"}

    The first line of the response contains a list with the immediate statuses
    of the tasks. The list is in the same order as the ``tasks`` parameter, to
    allow the client to know which key correspond to which task.

    The next lines contains interleaved statuses of the two tasks. The response
    is closed when all the tasks have finished.

    :<json tasks:
        a list containing the definitions of the tasks to execute.


.. http:get:: /v2/status

    Query the status of one or more tasks.

    **Example request**:

    .. code-block:: none

        https://dragon.stupeflix.com/v2/status?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M&block=true

    The response contains a list of task statuses, see :http:post:`/v2/create`
    for a response example.

    :query tasks:
        one or more tasks keys.

    :query block:
        a boolean indicating if the call should return immediately with the
        current status of the task, or wait for all tasks to complete and
        return their final status.

    :query details:
        if this boolean is true, return more details in the statuses objects
        (tasks parameters, storage details, etc...).


.. http:post:: /v2/status

    Same as :http:get:`/v2/status` but using POST semantics. Useful when there
    are too much tasks to query and the querystring size limit is reached.


.. http:get:: /v2/status_stream

    Get status streams of one or more tasks.

    **Example request**:

    .. code-block:: none

        https://dragon.stupeflix.com/v2/stream?tasks=6GRQ3H5EHU7GXUTIOSS2GUDPGQ&tasks=5OYA5JQVFIAHYOMLQG5QV3U33M

    See :http:post:`/v2/create_stream` for a description of the response.

    :query tasks:
        one or more tasks keys.


.. http:post:: /v2/status_stream

    Same as :http:get:`/v2/status_stream` but using POST semantics. Useful when
    there are too much tasks to query and the querystring size limit is
    reached.


.. _v2_storage_api:

Storage API methods
-------------------

.. http:get:: /v2/storage/files/(path)

    List tasks output files.

    The response is a JSON mapping containing the lists of files and
    directories, and storage space used by these files::

        {
            "files": [
                {
                    "name": "dragon-image.thumb-IeWutW",
                    "size": 4293,
                    "last_modified": "2013-10-28T20:22:21.000Z"
                }
            ],
            "directories": [
                "XDJC6DIS5UDSFBBOLXWMN27ORI/"
            ],
            "usage": 4293
        }

    :param path: the path of the directory to list.
    :query recursive:
        a boolean value indicating if *path* sub-directories must be traversed
        too.


.. http:delete:: /v2/storage/files/(path)

    Delete tasks output files.

    If *path* is empty, recursively delete all output files.

    If *path* points to a directory, recursively delete all output files under
    this directory.

    If *path* points to a file, delete this file.

    Files can also be targeted by date with the *from*, *to* and *max_age*
    parameters. *from* and *to* dates must be `ISO8601
    <http://en.wikipedia.org/wiki/ISO_8601>`_ date time strings; if they don't
    include a timezone they will be interpreted as UTC.

    The *urls* parameter also allows to delete files from absolute URLs.

    The response is a JSON mapping containing the list of deleted files, the
    number of bytes freed and the (approximate) total space used on the
    persistent storage after the operation::

        {
            "deleted": [
                "BCSIT5KDDQQTC7GZ6TBJE7NFIU/dragon-image.thumb-9b0E9P",
                "XDJC6DIS5UDSFBBOLXWMN27ORI/dragon-image.thumb-IeWutW"
            ],
            "freed": 1257,
            "usage": 6578
        }

    :param path: the path of the file or directory to delete.
    :<json urls:
        a list of absolute URLs to delete. If this parameter is used, all other
        selection parameters (*path, from, to, max_age*) are ignored.
    :<json dry_run:
        if this boolean is true, return the files that would be deleted, but
        don't actually delete them (default: ``false``).
    :<json from: the date from which point to delete files.
    :<json to: the date up to which point to delete files.
    :<json max_age: files older than *max_age* days are deleted.

.. http:post:: /v2/storage/expiration

    Set lifetime of tasks output files.

    :<json int days:
        the number of days after which files are deleted in the tasks output
        storage. A value of 0 means that files are never deleted.


.. http:get:: /v2/storage/expiration

    Get the current lifetime of tasks output files.

    The response is the current lifetime of files, in days. A value of 0 means
    that files are never deleted.
