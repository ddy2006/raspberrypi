FROM balenalib/raspberry-pi-debian:buster-run-20210812

RUN echo deb https://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi  > /etc/apt/sources.list \
  && echo deb-src https://mirrors.tuna.tsinghua.edu.cn/raspbian/raspbian/ buster main contrib non-free rpi >> /etc/apt/sources.list \
  && echo deb https://mirrors.tuna.tsinghua.edu.cn/raspberrypi/ buster main ui > /etc/apt/sources.list.d/raspi.list

RUN apt-get update && apt-get upgrade && apt-get install motion

RUN mkdir /mnt/motion && chown motion /mnt/motion
COPY motion.conf /etc/motion/motion.conf

VOLUME /mnt/motion
EXPOSE 8081
ENTRYPOINT ["motion"]
