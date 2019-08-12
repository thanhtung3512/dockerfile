FROM ubuntu

ENV GOPATH /opt/go

# get the software proprerties common golang gcc and git
# We need to install the software properties common before doing add-apt-repository, otherwise it will give an error: add-apt-repository: not found
RUN apt-get update && apt-get install -y \
  software-properties-common \
  git \
  gcc

RUN add-apt-repository ppa:gophers/archive
RUN apt-get -q -y install golang-1.11
RUN ln /usr/lib/go-1.11/bin/go /usr/bin/go

RUN add-apt-repository ppa:alex-p/tesseract-ocr && apt-get update

# Get tesseract-ocr packages
RUN apt-get install -y \
  libleptonica-dev \
  libtesseract4 \
  libtesseract-dev \
  tesseract-ocr

# Get language data.
RUN apt-get install -y \
  tesseract-ocr-fin \
  tesseract-ocr-vie \
  tesseract-ocr-eng

RUN mkdir -p $GOPATH

# go get open-ocr
RUN go get -u -v -t github.com/thanhtung3512/ocr

# build open-ocr-httpd binary and copy it to /usr/bin
RUN cd $GOPATH/src/github.com/thanhtung3512/ocr/cli-httpd && go build -v -o open-ocr-httpd && cp open-ocr-httpd /usr/bin

# build open-ocr-worker binary and copy it to /usr/bin
RUN cd $GOPATH/src/github.com/thanhtung3512/ocr/cli-worker && go build -v -o open-ocr-worker && cp open-ocr-worker /usr/bin
