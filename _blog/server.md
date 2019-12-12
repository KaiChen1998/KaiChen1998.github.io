---
date: 2019-08-07 21:30:24
layout: archive
title: '服务器使用经验汇总'
author_profile: true
permalink: /blog/server/
---

- 服务器使用jupyter notebook

  ```bash
  # 服务器上运行
  jupyter notebook --no-browser --port=8889
  # 本地运行
  ssh -N -f -L 127.0.0.1:8889:127.0.0.1:8889 username@address
  # 本地打开 http://localhost:8889/token=...即可
  ```

- 配置环境

  ```bash
  conda create -n py3 python=3.6
  source activate py3
  
  # 可以将指令写在一个sh脚本当中就可以使用nohup后台安装packet
  # test.sh
  echo start
  while read requirement; do conda install --yes $requirement || pip install $requirement; done < requirements.txt
  echo finish
  # run
  nohup ./test.sh &
  ```

- 手动指定conda env位置和pkt cache位置

  ```bash
  # 在用户目录下面创建.condarc文件，并指定
  envs_dirs:
    - /l/vision/v6/kaichen/anaconda/envs
  pkgs_dirs:
    - /l/vision/v6/kaichen/anaconda/pkgs
  ```

- bash_profile

  ```bash
  # 登陆的默认操作
  vim .bash_profile
  ```

- 服务器下载并使用dropbox

  ```bash
  $ wget https://raw.github.com/andreafabrizi/Dropbox-Uploader/master/dropbox_uploader.sh
  $ chmod +x dropbox_uploader.sh
  
  查询用户信息
  $ ./dropbox_uploader.sh info
  显示根目录内容
  $ ./dropbox_uploader.sh list
  要列出某个特定文件夹中的所有内容
  $ ./dropbox_uploader.sh list Documents/manuals
  上传一个本地文件到一个远程的 Dropbox 文件夹
  $ ./dropbox_uploader.sh upload snort.pdf Documents/manuals
  从 Dropbox 下载一个远程的文件到本地
  $ ./dropbox_uploader.sh download Documents/manuals/mysql.pdf ./mysql.pdf
  从 Dropbox 下载一个完整的远程文件夹到一个本地的文件夹
  $ ./dropbox_uploader.sh download Documents/manuals ./manuals
  在 Dropbox 上创建一个新的远程文件夹
  $ ./dropbox_uploader.sh mkdir Documents/whitepapers
  完全删除 Dropbox 中某个远程的文件夹（包括它所含的所有内容）
  $ ./dropbox_uploader.sh delete Documents/manuals
  ```

- screen

  ```bash
  # 建立新的screen，打开一个新的bash
  $ screen
  # ctrl + a + d 将screen置入后台运行，期间可以logout服务器
  
  $ screen -ls
  $ screen -r #process_id
  ```

- python添加环境变量

  ```python
  import sys
  sys.path.append('your path')
  ```

- 进程前后台切换

  ```bash
  $ nohup python train.py &
  
  # 1. 运行程序时，先按ctrl z使其进入后台
  # 2. 使用jobs查看对应的job 编号（和PID不同）
  jobs
  # 3. fg是前台，bg是后台，但是只有nohup是忽略输出
  fg/bg %1
  ```

- 指定GPU

  ```bash
  export CUDA_VISIBLE_DEVICES=ID
  ```

- 清楚process结束之后仍然继续占用GPU的进程

  ```bash
  fuser -v /dev/nvidia*
  kill process_id
  ```

  
