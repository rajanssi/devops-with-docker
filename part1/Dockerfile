FROM ubuntu:20.04

WORKDIR /usr/src/app

COPY curler.sh .

RUN apt-get update && apt-get install -y curl
RUN chmod +x curler.sh

ENTRYPOINT ["./curler.sh"]

CMD ["helsinki.fi"]
