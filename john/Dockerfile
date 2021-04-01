FROM gcc:5.4 AS build-env
LABEL maintainer "rollwagen <rollwagen@gmail.com>"

RUN apt-get install git

RUN git clone --depth 1 --branch OpenSSL_1_1_1-stable https://github.com/openssl/openssl.git \
        && cd openssl && ./config zlib '-Wl,-rpath,$(LIBRPATH)' \
        && make -sj4 \
        &&  make -s install \
        && apt-get remove openssl -y \
        && ldconfig -v

RUN git clone https://github.com/magnumripper/JohnTheRipper.git && cd JohnTheRipper/src \
        && ./configure || cat config.log \
        && sed -i -E 's/(\-lbz2)/\-Wl\,\-Bstatic\ \1\ \-Wl\,\-Bdynamic/' Makefile \
        && sed -i -E 's/(\-lz)/\-Wl\,\-Bstatic\ \1\ \-Wl\,\-Bdynamic/' Makefile  \
        && make -s clean && make -sj4

FROM gcr.io/distroless/cc
COPY --from=build-env /JohnTheRipper/run /app
WORKDIR /app
ENTRYPOINT ["./john"]
