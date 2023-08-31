# scp with compression

Today, I need to transfer 1GB with of .ndjson files over a not-so-fast internet connection.

You can speed up the transfer by A LOT by enabling compression.

Here's how it works:

```shell
scp -C -i ~/path/whatever.pem \
    -r container-logs \
    ec2-user@ec2-1-2-3-4.eu-west-1.compute.amazonaws.com:/some/path/
```

This will copy the directory `container-logs` to the remote directory `/some/path/`.

The `-C` option enables the compression making a huge difference in transfer time.
