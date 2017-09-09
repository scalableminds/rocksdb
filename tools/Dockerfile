FROM debian:stretch

RUN apt-get update

RUN apt-get install -y g++ cmake git make tar wget

RUN apt-get install -y libjansson-dev libcurl4-openssl-dev

RUN wget https://github.com/google/protobuf/releases/download/v3.4.0/protobuf-cpp-3.4.0.tar.gz

RUN tar -xzf protobuf-cpp-3.4.0.tar.gz

RUN cd /protobuf-3.4.0 && ./configure && make && make check && make install

ADD . /rocksdb

RUN cd /rocksdb/third-party/json2pb && make libjson2pb.so && cp libjson2pb.so /usr/local/lib

RUN ldconfig

RUN mkdir /rocksdb/build && cd /rocksdb/build && cmake -DCMAKE_BUILD_TYPE=Release .. && make ldb

ENTRYPOINT /rocksdb/build/tools/ldb
