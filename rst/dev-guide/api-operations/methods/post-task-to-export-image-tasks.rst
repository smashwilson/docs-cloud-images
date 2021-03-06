
.. THIS OUTPUT IS GENERATED FROM THE WADL. DO NOT EDIT.

.. _post-task-to-export-image-tasks:

Task to export image
^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^

.. code::

    POST /tasks

Exports an image using an asynchronous task request. See the request body for specific details.

This operation exports an image in VHD format using an asynchronous task request to export. The request begins the export process and returns the task UUID that can be subsequently polled to determine the status of the export by using the `4.4.2. Get task details <http://docs.rackspace.com/images/api/v2/ci-devguide/content/GET_getTask_tasks__taskID__Image_Task_Calls.html>`__ operation. The response conforms to the schema found in `4.5.5. Get tasks schema <http://docs.rackspace.com/images/api/v2/ci-devguide/content/GET_getTasksSchemas_schemas_tasks_Schema_Calls.html>`__. 

.. note::
   The exported image is deposited in your Cloud Files account and is identified by the ``image_uuid`` with a.vhd extension. You are responsible for ensuring that any distribution of your image from the Rackspace open cloud complies with any licensing restrictions.
   
   



This table shows the possible response codes for this operation:


+--------------------------+-------------------------+-------------------------+
|Response Code             |Name                     |Description              |
+==========================+=========================+=========================+
|201                       |Success                  |Task export request      |
|                          |                         |succeeded.               |
+--------------------------+-------------------------+-------------------------+
|400                       |Error                    |A general error has      |
|                          |                         |occured.                 |
+--------------------------+-------------------------+-------------------------+
|401                       |Unauthorized             |Unauthorized.            |
+--------------------------+-------------------------+-------------------------+
|403                       |Forbidden                |Forbidden.               |
+--------------------------+-------------------------+-------------------------+
|405                       |Bad Method               |Bad method.              |
+--------------------------+-------------------------+-------------------------+
|413                       |Over Limit               |The number of items      |
|                          |                         |returned is above the    |
|                          |                         |allowed limit.           |
+--------------------------+-------------------------+-------------------------+
|415                       |Bad Media Type           |Bad media type. This may |
|                          |                         |result if the wrong      |
|                          |                         |media type is used in    |
|                          |                         |the cURL request.        |
+--------------------------+-------------------------+-------------------------+
|500                       |API Fault                |API fault.               |
+--------------------------+-------------------------+-------------------------+
|503                       |Service Unavailable      |The requested service is |
|                          |                         |unavailable.             |
+--------------------------+-------------------------+-------------------------+


Request
""""""""""""""""








This table shows the body parameters for the request:

+------------------------------+-----------------------+-----------------------+
|Name                          |Type                   |Description            |
+==============================+=======================+=======================+
|parameters.\ **type**         |String *(Required)*    |The type of the task.  |
|                              |                       |Use ``export`` for     |
|                              |                       |task exports.          |
+------------------------------+-----------------------+-----------------------+
|parameters.\ **input**        |*(Required)*           |The container for      |
|                              |                       |export input           |
|                              |                       |parameters.            |
+------------------------------+-----------------------+-----------------------+
|parameters.input.\            |String *(Required)*    |The UUID for the       |
|**image_uuid**                |                       |exported image. You    |
|                              |                       |must own the image or  |
|                              |                       |the export task will   |
|                              |                       |fail.                  |
+------------------------------+-----------------------+-----------------------+
|parameters.input.\            |String *(Required)*    |The Cloud Files        |
|**receiving_swift_container** |                       |container for the      |
|                              |                       |exported image. If the |
|                              |                       |container does not     |
|                              |                       |exist, the task fails. |
|                              |                       |The task also fails if |
|                              |                       |the container name     |
|                              |                       |contains any of the    |
|                              |                       |following three        |
|                              |                       |characters: forward    |
|                              |                       |slash ( ``/`` ),       |
|                              |                       |question mark ( ``?``  |
|                              |                       |) or period ( ``.`` ). |
+------------------------------+-----------------------+-----------------------+





**Example Task to export image: JSON request**


.. code::

   {
       "type": "export",
       "input": 
       {
           "image_uuid": "ca5e7f11-5d57-4dd7-8ace-03ab647fe6c6", 
           "receiving_swift_container": "exports"
       }
   }





Response
""""""""""""""""





This table shows the body parameters for the response:

+------------------------------+-------------+---------------------------------------------+
|Name                          |Type         |Description                                  |
+==============================+=============+=============================================+
|parameters.\ **created_at**   |String       |The date and time that the task resource was |
|                              |*(Required)* |created.                                     |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **expires_at**   |String       |The date and time that the task resource     |
|                              |*(Optional)* |expires. Even after the task resource        |
|                              |             |expires (and is thus no longer available to  |
|                              |             |be polled), the result of the task (such as  |
|                              |             |an imported or exported image) still exists. |
|                              |             |.. note:: This parameter is required for     |
|                              |             |responses with ``status`` of ``success`` and |
|                              |             |``failure``.                                 |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **id**           |String       |The UUID of the task resource.               |
|                              |*(Required)* |                                             |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **input**        |*(Required)* |The container for export export input        |
|                              |             |parameters.                                  |
+------------------------------+-------------+---------------------------------------------+
|parameters.input.\            |*(Required)* |The UUID for the exported image.             |
|**image_uuid**                |             |                                             |
+------------------------------+-------------+---------------------------------------------+
|parameters.input.\            |String       |The Cloud Files container for the exported   |
|**receiving_swift_container** |*(Required)* |image.                                       |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **message**      |String       |``None`` if task export succeeded or the     |
|                              |*(Required)* |reason why the export failed.                |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **result**       |*(Optional)* |The container for results. .. note:: This    |
|                              |             |parameter is required for responses with     |
|                              |             |``status`` of ``success``.                   |
+------------------------------+-------------+---------------------------------------------+
|parameters.result.\           |String       |The location of the exported image in Cloud  |
|**export_location**           |*(Optional)* |Files.                                       |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **owner**        |String       |The tenant-id of the task owner.             |
|                              |*(Required)* |                                             |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **schema**       |String       |The schema of the task.                      |
|                              |*(Required)* |                                             |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **self**         |String       |The link to the task.                        |
|                              |*(Required)* |                                             |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **status**       |String       |The status of the task. For possible task    |
|                              |*(Required)* |statuses, see ` 1.4.2. Task statuses         |
|                              |             |<http://docs.rackspace.com/images/api/v2/ci- |
|                              |             |devguide/content/task-statuses.html>`__.     |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **type**         |String       |The type of the task ( ``export`` for task   |
|                              |*(Required)* |exports).                                    |
+------------------------------+-------------+---------------------------------------------+
|parameters.\ **updated_at**   |String       |The date and time that the task resource was |
|                              |*(Required)* |updated.                                     |
+------------------------------+-------------+---------------------------------------------+







**Example Export Task - Pending Response**


.. code::

   {
       "created_at": "2014-02-26T02:01:13Z", 
       "id": "7bdc8ede-9098-4d79-9477-697f586cb333", 
       "input": 
       {
           "image_uuid": "ca5e7f11-5d57-4dd7-8ace-03ab647fe6c6", 
           "receiving_swift_container": "exports"
       }, 
       "message": "None", 
       "owner": "00000123", 
       "schema": "/v2/schemas/task", 
       "self": "/v2/tasks/7bdc8ede-9098-4d79-9477-697f586cb333", 
       "status": "pending", 
       "type": "export", 
       "updated_at": "2014-02-26T02:01:13Z"
   }




