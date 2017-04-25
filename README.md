# miniokit
S3-in-a-box (Minio) packaged with LinuxKit

This page will be the reference material for a blog post - to be published soon.

Build the image:

```
# moby build -name minio ./minio.yml
```

Run the appliance:

```
# linuxkit run -disk-size 4096 -disk disk1.img -ip 192.168.65.101 minio
```

Find your access and secret key:

* On the VM shell, type in the following:

```
# / runc exec minio grep "access" /root/.minio/config.json
# / runc exec minio grep "secret" /root/.minio/config.json
```

Now, on your Mac:

* Launch a Docker client and mount the folders you need:

```
# docker run -v $HOME/Downloads:/root/Downloads --entrypoint=sh -ti minio/mc
```

Now set up a remote S3 client entry called `s3` and create your first bucket:

```
# mc config host add s3 http://192.168.65.101:9000 BPLPLXNA6O9HFT0KOA15 kaX6fvkUgfZ2YM8atymxu3kULEkQn8FPH0PcUS6n
# mc mb s3/downloads
```

