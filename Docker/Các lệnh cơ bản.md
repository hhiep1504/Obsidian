_#kiểm tra phiên bản_
``` bash
docker --version
```

_#liệt kê các image_
```bash
docker images -a
```

_#xóa một image (phải không container nào đang dùng)_
``` bash
docker images rm imageid
```

_#tải về một image (imagename) từ hub.docker.com_
```bash
docker pull imagename
```

_#liệt kê các container_
```bash
docker container ls -a
```

_#xóa container_
```bash
docker container rm containerid
```

_#tạo mới một container_
```bash
docker run -it imageid
```


_#thoát termial vẫn giữ container đang chạy_
``` bash
CTRL +P, CTRL + Q
```


_#Vào termial container đang chạy_
``` bash
docker container attach containerid
```


_#Chạy container đang dừng_
``` bash
docker container start -i containerid
```

_#Chạy một lệnh trên container đang chạy_
``` bash
docker exec -it containerid command
```


## Làm quen ban đầu Docker

Giờ hãy mở giao diện lệnh `termial` (macOS, Linux) hay `PowerShell` của Windows nên và gõ:

**Kiểm tra phiên bản Docker**
``` bash
docker --version
```


Hoặc lệnh thông tin chi tiết hơn:

``` bash
docker info
```

![Docker Info](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/docker-version.png)

**image và container trong Docker**

`image` là một gói phần mềm trong đó chứa những thứ cần như thư viện, các file cấu hình, biến môi trường để chạy mội ứng dụng nào đó. Nó giống như cái USB chứa bộ cài đặt hệ điều hành Windows!

Khi một phiên bản của image chạy, phiên bản chạy đó gọi là `container` - (vậy muốn có container phải có image). Bất ký lúc nào bạn cũng có thể kiểm tra xem có bao nhiêu `container` đang chạy và nó sinh ra từ image nào.

Bước đầu, để có `image` nào đó bạn tải về từ `https://hub.docker.com/search?q=&type=image`, tại đó có đủ các loại phù hợp với công việc của bạn!

**Tải về một image**

Kiểm tra các `image` bạn đang có

``` bash
docker images -a
```

Nó sẽ liệt kê ra các image bạn đang có, với dạng:

![Docker Info](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/docker-images.png)

- `Repository` tên image trên kho chứa, ví dụ hệ điều hành CentOS có tên trên hub.docker.com là `centos` (xem [centos](https://hub.docker.com/_/centos))
- `TAG` là phiên bản image, với giá trị `latest` có nghĩa là bản cuối. Muốn tải về bản khác `latest` vào mục TAGS trên `hub.docker.com` tìm bản phù hợp.
- `IMAGE ID` một chuỗi định danh duy nhất (tên) của image trên hệ thống của bạn.

Để tải về một image nào đó, dùng lệnh

docker pull nameimage:tag

#Hoặc tải về bản cuối
docker pull nameimage

Bây giờ hệ thống không có hệ điều hành `Ubuntu`, muốn tải nó về - vì trên hub.docker.com nó có tên `ubuntu`, ta sẽ tải về bản mới nhất bằng lệnh:

docker pull ubuntu

![Docker Ubuntu](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/docker-ubuntu.png)

Giờ thì hệ thống sẽ có thêm image với tên ubutu, có thể góc lại lệnh kiểm tra `docker images -a` ở trên để xem.

## Tạo và chạy container

Như trên, container là một phiên bản chạy của image, trước tiên

Kiểm tra có các `container` nào đang chạy:

``` bash
docker ps
```

Liệt kê tất cả các `container`:

``` bash
docker container ls --all
```

![Docker Container](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/docker-container1.png)

Các container bạn đã tạo, liệt kê ra hãy chú ý mấy thứ

- `CONTAINER ID` một con số (mã hash) gán cho container, bạn dùng mã này để quản lý container này, như xóa bỏ, khởi động, dừng lại ...
- `IMAGE` cho biết `container` sinh ra từ image nào.
- `COMMAND` cho biết lệnh, ứng dụng chạy khi container chạy (/bin/bash là terminate)
- `STATUS` cho biết trạng thái, (exit - đang dừng)

Để tạo và chạy một container theo cú pháp:
``` bash
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
```


Các tham số đó là:

- `[OPTIONS]` các thiết lập khi tạo container, có rất nhiều thiết lập tùy mục đích tạo container, sẽ tìm hiểu các thiết lập qua từng trường hợp cụ thể.
- `IMAGE` tên image hoặc ID của image từ nó sinh ra container.
- `[COMMAND] [ARG...]` lệnh và tham số khi container chạy.

Trở lại phần trên, đang có image hệ điều hành Ubuntu, giờ muốn chạy nó (tạo một container từ nó), hãy gõ lệnh sau:

``` bash
docker run -it ubuntu
```

Bạn chú ý có tham số `-it` để khi container chạy, bạn có terminate làm việc ngay với Ubuntu. Tham số này có nghĩa là

- `-t` nó có nghĩa là console, cho phép kết nối với `terminal` để tương tác
- `-i` có nghĩa duy trì mở stdin để nhập lệnh.

Sau lệnh này, bạn đang chạy `Ubuntu`, bạn có thể gõ vài lệnh Ubuntu kiểm tra xem. Ví dụ kiểm tra phiên bản Ubuntu, xem hình dưới với lệnh `cat /ect/*release`. Như vậy bạn đã tạo một container

![Docker Ubuntu](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/docker-ubuntu2.png)

Bạn đang ở `terminal` của Ubuntu, có thể kết thúc bằng lệnh `exit`, hoặc nhấn nhanh`CTRL+P,CTRL+Q` để thoat `termial` nhưng `container` vẫn đang chạy.

**Một vài tham số khác:**

Tạo và chạy container, container tự xóa khi kết thúc thì thêm vào tham số `--rm`

``` bash
docker run -it --rm ubuntu
```

Tạo và chạy container - khi container chạy thi hành ngay một lệnh nào đó, ví dụ `ls -la`

``` bash
docker run -it --rm debian ls -la
```

Tạo và chạy container - ánh xạ một thự mục máy host vào một thư mục container, chia sẻ dữ liệu

``` bash
docker run -it --rm -v path-in-host:path-in-container debian
```

**Vào container đang đang chạy**

Kiểm tra xem bằng lệnh `docker ps`, nếu có một `container` với ID là containerid đang chạy, để quay quay trở lại `terminal` của nó dùng lệnh:

``` bash
docker container attach containerid
```

Chạy một container đang dừng

``` bash
docker container start -i containerid
```

Nếu cần xóa bỏ hẳn một container thì dùng lệnh

``` bash
docker container rm containerid
```

