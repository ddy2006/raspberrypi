IMAGE_NAME:=ddy2006/motion

build:
	docker build --network=host -t $(IMAGE_NAME) .

push:
	docker push $(IMAGE_NAME)

clean:
	docker rmi $(IMAGE_NAME)

run:
	docker run -it --device /dev/video0:/dev/video0 --privileged -v /opt/vc:/opt/vc --rm -v ${PWD}/video:/mnt/motion -p 8081:8081 ddy2006/motion

transfer:
	docker save $(IMAGE_NAME) | zstd -T0 | pv | ssh pi@192.168.1.63 'zstd -T0 -d | docker load'