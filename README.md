# ethminer-systemd

Configuration and instructions to run Ethminer with Systemd

## Achieving Stability

Running a single Ethminer process in a multi-gpu configuration can cause
frustrating instability problems (particularly when you start to hit 7-8
GPUs). To achieve better stability, and potentially higher overall
performance, the key seems to be running an ethminer process per GPU.

## Edit the Service Definition File (ethminer@.service)

Make sure that you edit the ethminer@.service definition file to include
your account details and running configuration specific to your rig. See
the ethminer help ```ethminer -h``` for more details.

Also make sure that you use the correct absolute path to your ethmniner
process. I compile and install mine to /usr/bin but there is a good chance
that your process resides elsewhere.

Finally make sure that you also change the ```User``` and
```WorkingDirectory``` to reflect the user that you want your ethminer process
to run as and from which directory it should execute. Of course the user
account that you specify must have permissions to execute the ethminer process
as well as operate within the specified working directory.

## Install the Service

Copy the modified ethminer@.service file to the ```/etc/systemd/system```
directory. Then enable the service for each one of your GPUs with the following
command:

```
sudo systemctl enable ethminer@<gpu id>.service
```

Finally, start each instance separately:

```
sudo systemctl start ethminer@<gpu id>.service
```

## Monitoring the Mining Process

If you want see the output of the mining processes you can run the
```journalctl -f``` command.

## Profit :moneybag:

That's it folks. You should now be mining with a stable setup that restarts on
failure.

| Tips :thumbsup:                            |
| :----------------------------------------- |
| 0x7735F34120d2a33815FE5503b1B10b9e126E935C |
