.. highlight:: js

Storage systems
===============

Storage systems, introduced in the :doc:`/v2 API <api>`, allow you to choose
where your task output files are stored. 

Here is an example request storing two thumbnails in the
:ref:`storage_persistent` and :ref:`storage_volatile` storages::

    {
        "tasks": [
            {
                "task_name": "image.thumb",
                "task_store": {
                    "type": "volatile"
                },
                "url": "http://files.com/image.jpg"
            },
            {
                "task_name": "image.thumb",
                "task_store": {
                    "type": "persistent"
                },
                "url": "http://files.com/image.jpg"
            }
        ]
    }
    
.. _storage_persistent:

persistent
----------

This is the default storage for the :doc:`/v2 API <api>`. It stores files on
Amazon S3. It accepts a single optional parameter:

    * **location** (string) - The location of the bucket, one of:
        * 'EU'
        * 'USWest'
        * 'USWest2'
        * 'SAEast'
        * 'APNortheast'
        * 'APSoutheast'
        * 'APSoutheast2'

It is not possible to change the location once the first result has been stored
for an API key. If you need to store your files in a different location, create
a new API key and pass the desired location in your first task, for example::

    {
        "task_name": "image.thumb",
        "task_store": {
            "type": "persistent",
            "location": "EU"
        },
        "url": "http://foo.com/image.jpg"
    }

By default, files are stored permanently. You can change the lifetime of your
files with :http:method:`v2_storage_expiration_post`.

You can manage the files in your persistent storage with the :ref:`v2_storage_api`.

.. _storage_volatile:

volatile
--------

Files are stored for a week on Stupeflix servers. This is the default storage
for the :doc:`/v1 API <../v1/api>`.

youtube
-------

Upload videos on Youtube. It requires the following parameters:

    * **access_token** (string) - Target user's access token with upload
      authorization.
    * **developer_key** (string) -Youtube developer key of a registered app.
    * **title** (string) - Video title.

The following optional parameters are also accepted:

    * **description** (string) - Video description.
    * **tags** (list of strings) - List of video tags.
    * **category_id** (integer) - Video category ID number.
    * **privacy_status** (string) - Privacy status of the video. Accepted
      values are "public", "private" and "unlisted" *(default: "public")*.

.. warning:: link to the categories documentation
