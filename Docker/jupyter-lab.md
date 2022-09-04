---
title: Docker部署 jupyter lab服务
description: 
published: 1
date: 2022-09-04T18:00:50.397Z
tags: docker, jupyter
editor: markdown
dateCreated: 2022-09-04T18:00:50.397Z
---

### 1.打包镜像
* 创建Dockerfile文件
    ```dockerfile
      FROM python:slim-bullseye
      RUN pip install jupyterlab -i https://pypi.tuna.tsinghua.edu.cn/simple
      RUN jupyter lab --generate-config
      RUN mkdir -p /root/data
      RUN sed -i "s/# c.ServerApp.ip = 'localhost'/c.ServerApp.ip = '*'/" /root/.jupyter/jupyter_lab_config.py
      RUN sed -i "s/# c.ServerApp.root_dir = ''/c.ServerApp.root_dir = '\/root\/data'/" /root/.jupyter/jupyter_lab_config.py
      CMD ["jupyter", "lab", "--allow-root"]
    ```
* 生成镜像
    ```bash
    docker build -t jupyterlab .
    ```
    
### 2.创建容器
* 启动容器并暴露端口
    ```bash
    docker run -itd --restart=always \
    --name jupyterlab \
    -p 8888:8888 \
    jupyterlab
    ```
    
### 3.设置密码
* 进行设置密码操作
    ```bash
    docker exec -it jupyterlab jupyter lab password
    ```
* 设置完成后重启容器
    ```bash
    docker restart jupyterlab
    ```