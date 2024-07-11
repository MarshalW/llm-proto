# 使用nvidia作为基础镜像
FROM nvidia/cuda:12.2.0-devel-ubuntu22.04


# 设置时区环境变量
ENV TZ=Asia/Shanghai

# 设置时区
# 安装 python3/pip/jupyter相关
RUN ln -snf /usr/share/zoneinfo/$TZ /etc/localtime && echo $TZ > /etc/timezone \
    && apt update && apt install python3 pip git -y \
    && apt-get -y install \
        pandoc texlive-xetex texlive-fonts-recommended texlive-plain-generic \
        latex-cjk-all -y \
    && pip config --user set global.index-url https://pypi.tuna.tsinghua.edu.cn/simple \
    && pip install \
        jupyterlab jupyterlab-language-pack-zh-CN jupyterlab-git jupyterlab-github \
        matplotlib \
        numpy \
        sympy \
        mplfonts

# 安装额外的工具
RUN apt-get install -y \
    curl \
    nano

# 初始化中文字体库
RUN mplfonts init

RUN export https_proxy=http://192.168.0.134:7890;export http_proxy=http://192.168.0.134:7890;export all_proxy=socks5://192.168.0.134:7890

# pytorch
RUN pip install torch torchvision torchaudio

# 其他追加的库
RUN pip install ipywidgets

WORKDIR /root/notebook

EXPOSE 8888

RUN mkdir /models

RUN apt-get install -y \
    jq \
    iputils-ping

CMD ["jupyter","lab","--allow-root","--ip","0.0.0.0","--no-browser"]