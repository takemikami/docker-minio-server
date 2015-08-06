# Minio Server on Docker
Minio Server on Docker, Minio Server docker container.

This container is used for local-pc development.
You can use this container, when you develop an application
used AWS S3 for messaging without aws services.

see.
https://www.minio.io/

# Getting started

Start docker container.

```
$ docker pull takemikami/minio-server
$ docker run -d -v /var/log/minio-server:/var/log -v /var/data/minio-server:/var/minio-server -p 9000:9000 -p 9001:9001 -t minio-server
```

Execute sample program.

sample.rb

```
require 'aws-sdk'

s3cli = Aws::S3::Client.new(
  region:             'dummy-s3',
  endpoint:           "http://192.168.59.103:9000",
  access_key_id:      'dummy',
  secret_access_key:  'dummy',
)

p s3cli.create_bucket(bucket: 'BucketName')

p s3cli.put_object(
  body: 'source_file',
  bucket: "BucketName",
  key: "ObjectKey",
)

p s3cli.list_buckets()

#p s3cli.delete_bucket(bucket: 'BucketName')
```

```
$ gem install aws-sdk
$ ruby sample.rb
```

# Build Container

```
$ docker build -t minio-server .
```
