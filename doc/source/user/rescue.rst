==================
Rescue an instance
==================

Rescue mode provides a mechanism for access, even if an image renders
the instance inaccessible. By default, it starts an instance from the
initial image attaching the current boot disk as a secondary one.

.. note::

   Pause, suspend, and stop operations are not allowed when an instance
   is running in rescue mode, as triggering these actions causes the
   loss of the original instance state and makes it impossible to
   unrescue the instance.

   As of the 20.0.0 (Train) release rescuing a volume-backed server
   is not supported.

To perform an instance rescue, use the :command:`openstack server rescue`
command:

.. code-block:: console

   $ openstack server rescue SERVER

.. note::

   On running the :command:`openstack server rescue` command,
   an instance performs a soft shutdown first. This means that
   the guest operating system has a chance to perform
   a controlled shutdown before the instance is powered off.
   The shutdown behavior is configured by the
   :oslo.config:option:`shutdown_timeout` parameter that can be set in the
   ``nova.conf`` file.
   Its value stands for the overall period (in seconds)
   a guest operating system is allowed to complete the shutdown.

   The timeout value can be overridden on a per image basis
   by means of ``os_shutdown_timeout`` that is an image metadata
   setting allowing different types of operating systems to specify
   how much time they need to shut down cleanly.

If you want to rescue an instance with a specific image, rather than the
default one, use the ``--image`` parameter:

.. code-block:: console

   $ openstack server rescue --image IMAGE_ID SERVER

To restart the instance from the normal boot disk, run the following
command:

.. code-block:: console

   $ openstack server unrescue SERVER
