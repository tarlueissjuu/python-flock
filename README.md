Configuration
=============

You have to write the configuration file **/etc/distributed-flock.json** with the following content:
```js
{
    "host"      :   ["hostname1:2181","hostname2:2181","hostname3:2181"],
    "timeout"   :   5,
    "app_id"    :   "my_application_namespace"
    "sleep"     :   "ON"    //ON or OFF - Default OFF
    "maxla"     :   30      // If >=0 -> max loadaverage for work. Default -1
}
```
 * **host** - list of Zookeeper nodes
 * **timeout** - timeout for zookeper connection (sec)
 * **app_id** - namespace for your application in Zookeeper. This means that the lock will be stored  
                in Zookeeper with path likes **/app_id/your_lock_name**
 * **sleep** - Sleep before work. Default: "OFF"
 * **maxla** - Maximal load average. Use if >=0. Default: -1

Usage
=====

To run the application under the supervision of the zk-flock use the command:
```bash
zk-flock <pidname> <application coomand>
```

If your application requires command-line arguments enclose it in double quotes:
```bash
zk-flock my_test_lock "bash /home/user/test.sh arg1 arg2 arg3"
```

Add key **-d** or **--daemonize** to starts this appliction as daemon.

Warning
=======

If you kill zk-flock application with **kill -9**, the lock will be released, but this will not stop your application.
