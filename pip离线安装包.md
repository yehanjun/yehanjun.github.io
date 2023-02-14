pip离线安装包
外网下载包
pip download -d pkgs -r requirements.txt 

离线安装包
pip install --no-index --find-links=pkgs -r requirements.txt