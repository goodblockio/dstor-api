Welcome to the dStor developer API (v0)
=======================================

Quickstart
==========

`https://a.dstor.cloud/v0/<dev key>/<store|release|list|stat>[?id=]`

Reference
=========

.. http:get::  /v0/<dev key>/list

    Retrieve a list of stored files

    ** Example **

    .. prompt:: bash $

      curl https://a.dstor.cloud/v0/0123456789abcdef/list

    ** Response **

    .. sourcecode:: js

      [
        ["QmX9b1UChdeCdBXTjFx7o6dAPdHKmMfRFshQWJbEHCWrKe", "telos-logo.png"]
      ]

.. http:get::  /v0/<dev key>/stat

    Retrieve info about a stored file

    ** Example **

    .. prompt:: bash $

      curl https://a.dstor.cloud/v0/0123456789abcdef/stat?id=QmX9b1UChdeCdBXTjFx7o6dAPdHKmMfRFshQWJbEHCWrKe

    ** Response **

    .. sourcecode:: js

      {
        "file_hash": "QmX9b1UChdeCdBXTjFx7o6dAPdHKmMfRFshQWJbEHCWrKe",
        "file_name": "telos-logo.png",
        "created": "2019-10-03 18:20:02.954406-07",
        "life_requests": 10000,
        "l30d_requests": [ 1, 2, 3, 4, 5, 6, 7 ],
        "comment": "Telos Logo added for the Telos Foundation"
      }

.. http:get::  /v0/<dev key>/release

    Release stored file

    ** Example **

    .. prompt:: bash $

      curl https://a.dstor.cloud/v0/0123456789abcdef/release?id=QmX9b1UChdeCdBXTjFx7o6dAPdHKmMfRFshQWJbEHCWrKe

    ** Response **

    .. sourcecode:: js

      {
        "result": "received"
      }

.. http:post::  /v0/<dev key>/store

    Store file

    ** Example **

    .. prompt:: bash $

      dd if=/dev/urandom of=/tmp/dstor-example-file count=1
      curl -X POST -F 'data=@/tmp/dstor-example-file' -d '{"file_name": "telos-logo.png", "comment": "Telos Logo added for the Telos Foundation"}' https://a.dstor.cloud/v0/0123456789abcdef/store

    ** Response **

    .. sourcecode:: js

      {
        "file_hash": "QmX9b1UChdeCdBXTjFx7o6dAPdHKmMfRFshQWJbEHCWrKe",
        "created": "2019-10-03 18:20:02.954406-07"
      }

Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
