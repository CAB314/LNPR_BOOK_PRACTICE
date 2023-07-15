---
title: pythonをローカル・ドッカーで動かしたい。
category: cab/others
tags: 
created_at: '2023-07-05T22:28:02+09:00'
updated_at: '2023-07-05T22:30:04+09:00'
published: false
number: 500
---


# Ref
https://zenn.dev/ushknn/articles/19e9aa500cb1e7
https://zenn.dev/suzuki_hoge/books/2022-03-docker-practice-8ae36c33424b59/viewer/2-1-points#%E3%82%A4%E3%83%A1%E3%83%BC%E3%82%B8%E3%82%92%E4%BD%9C%E6%88%90%E3%81%99%E3%82%8B

# Hardware
```
Hardware Overview:

  Model Name:	MacBook Pro
  Model Identifier:	MacBookPro18,4
  Chip:	Apple M1 Max
  Total Number of Cores:	10 (8 performance and 2 efficiency)
  Memory:	64 GB
  System Firmware Version:	7429.61.2
  OS Loader Version:	7429.61.2
  Serial Number (system):	WLHD7PL6WR
  Hardware UUID:	33EB66FB-5F09-54FC-81ED-06206DC1BE3C
  Provisioning UDID:	00006001-0004585A0181801E
  Activation Lock Status:	Enabled

```
# やったコード

まず、こんなDockerfile を作る
```Dockerfile
FROM python:3.9

WORKDIR /app

SHELL ["/bin/bash", "-c"]

RUN apt-get update &

RUN pip install --upgrade pip 

RUN pip install notebook
```
composeも
```docker-compose.yml
version: '3'
services:
  app:
    build: .
    volumes:
      - ./:/app
    ports:
      - 8888:8888
    tty: true
```

ターミナルからこれ実行
```zsh
docker-compose up -d
```
<details><summary>output</summary>

```output
Creating network "pyjpy_practice_default" with the default driver
Building app
[+] Building 148.9s (9/9) FINISHED                                                                                                                                                       
 => [internal] load build definition from Dockerfile                                                                                                                                0.0s
 => => transferring dockerfile: 182B                                                                                                                                                0.0s
 => [internal] load .dockerignore                                                                                                                                                   0.0s
 => => transferring context: 2B                                                                                                                                                     0.0s
 => [internal] load metadata for docker.io/library/python:3.9                                                                                                                       3.8s
 => [1/5] FROM docker.io/library/python:3.9@sha256:12f683bbf2fbd7598defa37eedb1eaa6505c310c1a3d859860a58567df8c8e66                                                               104.7s
 => => resolve docker.io/library/python:3.9@sha256:12f683bbf2fbd7598defa37eedb1eaa6505c310c1a3d859860a58567df8c8e66                                                                 0.0s
 => => sha256:12f683bbf2fbd7598defa37eedb1eaa6505c310c1a3d859860a58567df8c8e66 1.86kB / 1.86kB                                                                                      0.0s
 => => sha256:562c7ae00f43e7fff53e5948f4e9728f503463a3033c457adbcb907a102abd7a 2.01kB / 2.01kB                                                                                      0.0s
 => => sha256:9a0518ec57568a70561f7c04650f9554c88dada973f54d88e36f65b0796d35de 23.57MB / 23.57MB                                                                                   13.8s
 => => sha256:18dfab9212e4abdcc9bfd27aafe3f9faf23898b3d26ee4e7223c34366363de86 7.53kB / 7.53kB                                                                                      0.0s
 => => sha256:42cbebf8bc116ba1aed7897e2d0566bf49da9d5c70be71b6a7cb07805d2f5b7a 49.57MB / 49.57MB                                                                                   55.2s
 => => sha256:356172c718acf9930d9465b170864319079e2d2ebac0ddef781d64e85789531e 63.98MB / 63.98MB                                                                                   82.5s
 => => sha256:dddcd3ceb9980caac379e8f8eeafe1e901f017e5768b867705a0834cc1274efa 202.40MB / 202.40MB                                                                                 97.6s
 => => extracting sha256:42cbebf8bc116ba1aed7897e2d0566bf49da9d5c70be71b6a7cb07805d2f5b7a                                                                                           1.5s
 => => sha256:8e07adfdac1deb6e9fc0bd78eaa7a91b586b33b1fc3c87bd3d0c0d1da74e3f08 6.47MB / 6.47MB                                                                                     65.7s
 => => extracting sha256:9a0518ec57568a70561f7c04650f9554c88dada973f54d88e36f65b0796d35de                                                                                           0.5s
 => => sha256:15c3d0061bcfcdef1639fdc87e048b1973639c02bae049991b247617aad62257 15.54MB / 15.54MB                                                                                   78.3s
 => => sha256:134223eb4b12d689a8802f527367be7ca7dfd27e55bf26ed4d83ed3cb058a1de 244B / 244B                                                                                         79.6s
 => => sha256:eceff51d2f01e5c8cd408e9a9df0ac172e3d74bd5f88938f0f55eba8ecb3b865 2.85MB / 2.85MB                                                                                     81.7s
 => => extracting sha256:356172c718acf9930d9465b170864319079e2d2ebac0ddef781d64e85789531e                                                                                           2.0s
 => => extracting sha256:dddcd3ceb9980caac379e8f8eeafe1e901f017e5768b867705a0834cc1274efa                                                                                           5.7s
 => => extracting sha256:8e07adfdac1deb6e9fc0bd78eaa7a91b586b33b1fc3c87bd3d0c0d1da74e3f08                                                                                           0.2s
 => => extracting sha256:15c3d0061bcfcdef1639fdc87e048b1973639c02bae049991b247617aad62257                                                                                           0.5s
 => => extracting sha256:134223eb4b12d689a8802f527367be7ca7dfd27e55bf26ed4d83ed3cb058a1de                                                                                           0.0s
 => => extracting sha256:eceff51d2f01e5c8cd408e9a9df0ac172e3d74bd5f88938f0f55eba8ecb3b865                                                                                           0.2s
 => [2/5] WORKDIR /app                                                                                                                                                              0.4s
 => [3/5] RUN apt-get update &                                                                                                                                                      0.2s
 => [4/5] RUN pip install --upgrade pip                                                                                                                                             4.0s
 => [5/5] RUN pip install notebook                                                                                                                                                 34.8s
 => exporting to image                                                                                                                                                              0.8s 
 => => exporting layers                                                                                                                                                             0.8s 
 => => writing image sha256:22bfc6a8aa5a61287e29a60a5dab48256f2e7e94614ab492fb4f10a1deb0da58                                                                                        0.0s 
 => => naming to docker.io/library/pyjpy_practice_app                                                                                                                               0.0s 
                                                                                                                                                                                         
Use 'docker scan' to run Snyk tests against images to find vulnerabilities and learn how to fix them                                                                                     
WARNING: Image for service app was built because it did not already exist. To rebuild this image you must use `docker-compose build` or `docker-compose up --build`.
Creating pyjpy_practice_app_1 ... done
```

</details>

# Jupyterを起動して入ってみる

ターミナルからこれ実行
```zsh
docker-compose exec app bash
```
これで、環境に入れました。

```
root@80fc1c8e59a9:/app# jupyter notebook --port=8888 --ip=0.0.0.0 --allow-root --NotebookApp.token=''
```

<details><summary>output</summary>

```
[I 13:23:38.884 NotebookApp] Writing notebook server cookie secret to /root/.local/share/jupyter/runtime/notebook_cookie_secret
[I 13:23:38.884 NotebookApp] Authentication of /metrics is OFF, since other authentication is disabled.

  _   _          _      _
 | | | |_ __  __| |__ _| |_ ___
 | |_| | '_ \/ _` / _` |  _/ -_)
  \___/| .__/\__,_\__,_|\__\___|
       |_|
                       
Read the migration plan to Notebook 7 to learn about the new features and the actions to take if you are using extensions.

https://jupyter-notebook.readthedocs.io/en/latest/migrate_to_notebook7.html

Please note that updating to Notebook 7 might break some of your extensions.

[W 13:23:39.030 NotebookApp] All authentication is disabled.  Anyone who can connect to this server will be able to run code.
[I 13:23:39.034 NotebookApp] Serving notebooks from local directory: /app
[I 13:23:39.034 NotebookApp] Jupyter Notebook 6.5.4 is running at:
[I 13:23:39.034 NotebookApp] http://80fc1c8e59a9:8888/
[I 13:23:39.034 NotebookApp] Use Control-C to stop this server and shut down all kernels (twice to skip confirmation).
[W 13:23:39.036 NotebookApp] No web browser found: could not locate runnable browser.
```

</details>

入れるようになれました！

<img width="1512" alt="image.png (213.2 kB)" src="https://img.esa.io/uploads/production/attachments/14750/2023/07/05/122166/0a1eb58b-94cb-42c9-8ded-a90a81a5d11d.png">

