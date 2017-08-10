FROM circleci/python:3.6

RUN mkdir -p /tmp/prepare && \
    cd /tmp/prepare && \
    curl -L https://github.com/jgm/pandoc/releases/download/1.19.2/pandoc-1.19.2-1-amd64.deb -o pandoc.deb && \
    sudo dpkg -i pandoc.deb && \
    sudo apt-get -y install texlive-xetex texlive-latex-extra texlive-lang-cjk etoolbox && \
    sudo apt-get -y install ttf-wqy-microhei && \
    sudo pip3 install qiniu && \
    sudo rm -rf /tmp/prepare && \
    sudo rm -rf /var/lib/apt/lists/*