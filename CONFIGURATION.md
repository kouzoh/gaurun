# Configuration for Gaurun

The configuration file format for Gaurun is [TOML](https://github.com/toml-lang/toml).

The configuration for Gaurun has some sections. The example is [here](conf/gaurun.toml).

 * [Core Section](#core-section)
 * [iOS Section](#ios-section)
 * [Android Section](#android-section)
 * [Log Section](#log-section)

## Core Section

| name             | type   | description                                                                     | default          | note                                                                         |
| ---------------- | ------ | ------------------------------------------------------------------------------- | ---------------- | ---------------------------------------------------------------------------- |
| port             | string | port number or unix socket path                                                 | 1056             | e.g.)1056, unix:/tmp/gaurun.sock <br/> `-p` option can overwrite             |
| workers          | int64  | number of workers for push notification                                         | runtime.NumCPU() | `-w` options can overwrite                                                   |
| queues           | int64  | size of internal queue for push notification                                    | 8192             | `-q` options can overwrite                                                   |
| notification_max | int64  | limit of push notifications once                                                | 100              |                                                                              |
| pusher_max       | int64  | maximum goroutines for asynchronous pushing                                     | 0                | If the value is less than or equal to zero, each worker pushes synchronously |
| shutdown_timeout | int64  | timeout to wait for connections to return to idle when server shutdown (second) | 10               |                                                                              |
| pid              | string | path to pid file                                                                |                  |                                                                              |

## iOS Section

| name                | type   | description                                              | default          | note |
| ------------------- | ------ | -------------------------------------------------------- | ---------------- | ---- |
| enabled             | bool   | On/Off for push notication to APNs                       | true             |      |
| pem_cert_path       | string | certification file path for APNs                         |                  |      |
| pem_key_path        | string | secret key file path for APNs                            |                  |      |
| pem_key_passphrase  | string | secret key file pass phrase for APNs                     |                  |      |
| token_auth_key_path | string | secret APNs auth key file (.p8) for token based provider |                  |      |
| token_auth_key_id   | string | APNs key id for token based provider                     |                  |      |
| token_auth_team_id  | string | APNs team id for token based provider                    |                  |      |
| sandbox             | bool   | On/Off for sandbox environment                           | true             |      |
| retry_max           | int    | maximum retry count for push notication to APNs          | 1                |      |
| timeout             | int    | timeout for push notification to APNs                    | 5                |      |
| keepalive_timeout   | int    | time for continuing keep-alive connection to APNs        | 90               |      |
| keepalive_conns     | int    | number of keep-alive connection to APNs                  | runtime.NumCPU() |      |
| topic               | string | the assigned value of `apns-topic` for Request headers   |                  |      |

`topic` is mandatory when the client is connected using the certificate that supports multiple topics.

## Android Section

| name              | type   | description                                      | default          | note |
| ----------------- | ------ | ------------------------------------------------ | ---------------- | ---- |
| enabled           | bool   | On/Off for push notication to FCM                | true             |      |
| apikey            | string | API key string for FCM                           |                  |      |
| timeout           | int    | timeout for push notication to FCM               | 5(sec)           |      |
| keepalive_timeout | int    | time for continuing keep-alive connection to FCM | 90               |      |
| keepalive_conns   | int    | number of keep-alive connection to FCM           | runtime.NumCPU() |      |
| retry_max         | int    | maximum retry count for push notication to FCM   | 1                |      |

## Log Section

| name       | type   | description     | default | note                              |
| ---------- | ------ | --------------- | ------- | --------------------------------- |
| access_log | string | access log path | stdout  |                                   |
| error_log  | string | error log path  | stderr  |                                   |
| level      | string | log level       | error   | panic,fatal,error,warn,info,debug |

`access_log` and `error_log` are allowed to give not only file-path but `stdout` and `stderr` and `discard`.
