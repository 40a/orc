ORC: Ops Remote Configuration
====================================

A python application/script to export your Ops tools configuration (like: sensu, collectd, HAProxy ...) to a remote git repository.

Installation
---------------------------
.. code-block:: shell

	sudo pip install -e git+https://github.com/rafaelpsouza/orc.git#egg=orc

Usage
---------------------------

Using orc command::
*************************
.. code-block:: shell

	orc -r <REMOTE_REPOSITORY> -e <REMOTE_DIR> -c <CONFIG_DIR> -p <POST_CHANGE_COMMAND> -i <INTERVAL>

.. code-block:: shell

	orc --remote-repository <REMOTE_REPOSITORY> --remote-dir <REMOTE_DIR> --config-dir <CONFIG_DIR> --post-change-command <POST_CHANGE_COMMAND> --interval <INTERVAL>

* **REMOTE_REPOSITORY:** git repository url where the configuration is stored.

* **REMOTE_DIR:** A folder inside the git repository where the configuration is stored. Useful to create one folder per environment. ex: (dev, test, prod)

* **CONFIG_DIR:** Local configuration directory that will be replaced by a remote configuration. Ex: /etc/sensu

* **POST_CHANGE_COMMAND:** Command to be executed after a configuration change. Ex: 'sudo service xxx restart'

* **INTERVAL:** Interval, in seconds, that orc will check for remote configuration changes.

Using orc-runner.py
*************************

If you prefer or customize orc code, you can also clone orc repository and run orc-runner.py script with the same parameters above.

Usages and Examples
---------------------------

Sensu-server remote config
**********************************
.. code-block:: shell

	sudo orc -r https://github.com/rafaelpsouza/remote-config.git -e dev -c /etc/sensu -i 30 -p 'sudo sensu-server restart'

Collectd remote config
*********************************
.. code-block:: shell

	sudo orc -r https://github.com/rafaelpsouza/remote-config.git -e prod -c /etc/collectd -i 30 -p 'sudo collectd restart'