..
    Warning: Do not edit this file. It is automatically generated from the
    software project's code and your changes will be overwritten.

    The tool to generate this file lives in openstack-doc-tools repository.

    Please make any changes needed in the code, then run the
    autogenerate-config-doc tool from the openstack-doc-tools repository, or
    ask for help on the documentation mailing list, IRC channel or meeting.

.. _nova-livemigration:

.. list-table:: Description of live migration configuration options
   :header-rows: 1
   :class: config-ref-table

   * - Configuration option = Default value
     - Description
   * - **[DEFAULT]**
     -
   * - ``live_migration_retry_count`` = ``30``
     - (Integer) Maximum number of 1 second retries in live_migration. It specifies number of retries to iptables when it complains. It happens when an user continously sends live-migration request to same host leading to concurrent request to iptables.

       Possible values:

       * Any positive integer representing retry count.
   * - ``max_concurrent_live_migrations`` = ``1``
     - (Integer) Maximum number of live migrations to run concurrently. This limit is enforced to avoid outbound live migrations overwhelming the host/network and causing failures. It is not recommended that you change this unless you are very sure that doing so is safe and stable in your environment.

       Possible values:

       * 0 : treated as unlimited.

       * Negative value defaults to 0.

       * Any positive integer representing maximum number of live migrations to run concurrently.
   * - **[libvirt]**
     -
   * - ``live_migration_bandwidth`` = ``0``
     - (Integer) Maximum bandwidth(in MiB/s) to be used during migration. If set to 0, will choose a suitable default. Some hypervisors do not support this feature and will return an error if bandwidth is not 0. Please refer to the libvirt documentation for further details
   * - ``live_migration_completion_timeout`` = ``800``
     - (Integer) Time to wait, in seconds, for migration to successfully complete transferring data before aborting the operation. Value is per GiB of guest RAM + disk to be transferred, with lower bound of a minimum of 2 GiB. Should usually be larger than downtime delay * downtime steps. Set to 0 to disable timeouts.  - **Mutable** This option can be changed without restarting.
   * - ``live_migration_downtime`` = ``500``
     - (Integer) Maximum permitted downtime, in milliseconds, for live migration switchover. Will be rounded up to a minimum of 100ms. Use a large value if guest liveness is unimportant.
   * - ``live_migration_downtime_delay`` = ``75``
     - (Integer) Time to wait, in seconds, between each step increase of the migration downtime. Minimum delay is 10 seconds. Value is per GiB of guest RAM + disk to be transferred, with lower bound of a minimum of 2 GiB per device
   * - ``live_migration_downtime_steps`` = ``10``
     - (Integer) Number of incremental steps to reach max downtime value. Will be rounded up to a minimum of 3 steps
   * - ``live_migration_inbound_addr`` = ``None``
     - (String) Live migration target ip or hostname (if this option is set to None, which is the default, the hostname of the migration target compute node will be used)
   * - ``live_migration_permit_auto_converge`` = ``False``
     - (Boolean) This option allows nova to start live migration with auto converge on. Auto converge throttles down CPU if a progress of on-going live migration is slow. Auto converge will only be used if this flag is set to True and post copy is not permitted or post copy is unavailable due to the version of libvirt and QEMU in use. Auto converge requires libvirt>=1.2.3 and QEMU>=1.6.0.

       Related options:

        * live_migration_permit_post_copy
   * - ``live_migration_permit_post_copy`` = ``False``
     - (Boolean) This option allows nova to switch an on-going live migration to post-copy mode, i.e., switch the active VM to the one on the destination node before the migration is complete, therefore ensuring an upper bound on the memory that needs to be transferred. Post-copy requires libvirt>=1.3.3 and QEMU>=2.5.0.

       When permitted, post-copy mode will be automatically activated if a live-migration memory copy iteration does not make percentage increase of at least 10% over the last iteration.

       The live-migration force complete API also uses post-copy when permitted. If post-copy mode is not available, force complete falls back to pausing the VM to ensure the live-migration operation will complete.

       When using post-copy mode, if the source and destination hosts loose network connectivity, the VM being live-migrated will need to be rebooted. For more details, please see the Administration guide.

       Related options:

        * live_migration_permit_auto_converge
   * - ``live_migration_progress_timeout`` = ``150``
     - (Integer) Time to wait, in seconds, for migration to make forward progress in transferring data before aborting the operation. Set to 0 to disable timeouts.  - **Mutable** This option can be changed without restarting.
   * - ``live_migration_tunnelled`` = ``False``
     - (Boolean) Whether to use tunnelled migration, where migration data is transported over the libvirtd connection. If True, we use the VIR_MIGRATE_TUNNELLED migration flag, avoiding the need to configure the network to allow direct hypervisor to hypervisor communication. If False, use the native transport. If not set, Nova will choose a sensible default based on, for example the availability of native encryption support in the hypervisor.
   * - ``live_migration_uri`` = ``None``
     - (String) Override the default libvirt live migration target URI (which is dependent on virt_type) (any included "%s" is replaced with the migration target hostname)
