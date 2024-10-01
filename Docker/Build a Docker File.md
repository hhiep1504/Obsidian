Sử dụng các lệnh Docker tương tác trực tiếp hết lệnh này đến lệnh khác để lấy image về, tạo container, chạy và cài đặt các thành phần vào container ... Rất nhiều thao tác trong quá trình này có thể lưu vào một file gọi là `Dockerfile`, và ra lệnh cho Docker đọc file đó, chạy từng lệnh theo chỉ thị trong file đó để cuối cùng có được image theo nhu cầu.

## Sử dụng Dockerfile

Dockerfile là một file text, trong đó chứa các dòng chỉ thị để Docker đọc và chạy theo chỉ thị đó để cuối cùng bạn có một image mới theo nhu cầu. Khi đang có một Dockerfile giả sử có tên là `Dockerfile` để ra lệnh cho Docker chạy nó bạn có thể gõ:
``` bash
docker build -t nameimage:version --force-rm -f Dockerfile .
```


Bạn chú ý dấu `.` ở cuối lệnh `docker build` ở trên, có nghĩa tìm file có tên `Dockerfile` ở thư mục hiện tại.

`-t nameimage:version` là đặt tên và tag được gán cho image mới tạo ra.

Bạn có thể dùng `Visual Studio Code` có cài thêm Extension `Docker for Visual Studio Code` để khi soạn thảo file có tên `Dockerfile` nó gợi ý và highlight cú pháp cho bạn.

![Visual Studio Code](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/visualstudiocode.png)

## Tạo Dockerfile đơn gian đầu tiên

Dockerfile là **file text**, bạn dùng bất kỳ trình soạn thảo text nào tạo ra file này, và đưa vào nội dung là các chỉ thị. Giờ ta sẽ vừa thực hành vừa học từng bước. Ví dụ tạo file có tên `Dockerfile` nhập nội dung sau:
``` Dockerfile
# xây dựng image mới từ image centos:latest (CENTOS 7)_
FROM centos:latest

# Thêm hai lệnh sau nếu CENTOS 8 không cập nhật được
# RUN dnf -y --disablerepo '*' --enablerepo=extras swap centos-linux-repos centos-stream-repos
# RUN dnf -y distro-sync_

# Cập nhật các gói và cài vào đó HTTPD, HTOP, VIM_
RUN yum update -y
RUN yum install httpd httpd-tools -y
RUN yum install epel-release -y \
    && yum update -y \
    && yum install htop -y \
    && yum install vim -y

#Thiết lập thư mục hiện tại_
WORKDIR /var/www/html
# Copy tất cả các file trong thư mục hiện tại (.)  vào WORKDIR_
ADD . /var/www/html

#Thiết lập khi tạo container từ image sẽ mở cổng 80 ở mạng mà container nối vào_
EXPOSE 80

# Khi chạy container tự động chạy ngay httpd_
ENTRYPOINT ["/usr/sbin/httpd"]

#chạy terminate_
CMD ["-D", "FOREGROUND"]
```


Do RED HAT công bố CentOS Stream, bản CentOS 8 bị kết thúc vòng đời vào cuối năm 2021, nên sau thời điểm đó khi cập nhật với lệnh **yum update** có dẫn tới lỗi **AppStream**. Để khắc phục, bạn có thể chuyển thành **CentOS Stream 8** bằng lệnh:

dnf -y --disablerepo '*' --enablerepo=extras swap centos-linux-repos centos-stream-repos
dnf -y distro-sync

Cùng thư mục với Dockerfile, bạn cũng tạo thêm một file có tên `test.html` để làm dữ liệu kiệm tra, nội dung của nó đơn giản là:
``` html
<!DOCTYPE html>
<html>
<body>
    <h1>HELLO WORLD!</h1>
</body>
</html>
```


File trên chính là các chỉ thị, để Docker căn cứ vào đó mà thực hiện từng bước một. Bạn có nhìn thấy các chỉ thị như `FROM`, `RUN`, `ADD` ... Các chỉ thị cụ thể sẽ giải thích phần sau.

**Quy tắc viết chỉ thị Dockerfile**

Ở đây bạn chú ý khi viết các chỉ thị trong **Dockerfile** thì một chỉ thị có thể viết theo cấu trúc:
``` bash
# Ghi chú chỉ thị
TÊN_CHỈ_THỊ các_tham_số
```


Ví dụ, chỉ thị `RUN` là chạy một lệnh, muốn chạy lệnh cập nhật của CentOS `yum update -y` thì viết trong Dockerfile
``` Dockerfile
RUN yum update -y
```


**Thực hiện build một image từ Dockerfile**

Hiện giờ đang có Dockerfile với tên `Dockerfile` ở trên, Dockerfile này căn cứ theo các chỉ thị của nó, nó sẽ: xây dựng một image chứa `CentOS`, cài vào đó `Apache HTTPD`, `HTOP`, `VIM`, copy các file ở thư mục hiện tại vào `/home/code`, khi container tạo ra từ Image mới này thì tự động chạy `/usr/sbin/http` (máy chủ web) và `bash` đồng thời mở cổng `80` trên network container nối vào.

Giờ sử dụng file này build ra image xem, image mới sẽ đặt tên là `i-firstserver:version1`, gõ lệnh sau:
``` bash
docker build -t i-firstserver:version1 -f Dockerfile .
```


Sau khi gõ lệnh này, Docker bắt đầu đọc Dockerfile và thực hiện từng bước của chị thị. Nó sẽ tạo container tạm, đưa vào đó các gói, dữ liệu, cấu hình ... theo chỉ thị, mỗi bước này tạo ra một lớp image. Cuối cùng nó tạo ra một image mới có tên và tag do bạn chỉ ra ở trên, lưu trong hệ thống Docker của bạn!.

Build xong, kiểm tra danh sách image sẽ thấy tên này.
```bash
docker images -a
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
<none>              <none>              cf6721d88752        5 minutes ago       588MB
i-firstserver       version1            740cbb2e87ac        5 minutes ago       588MB
<none>              <none>              3661794c0ee8        5 minutes ago       588MB
<none>              <none>              2027afe1b677        5 minutes ago       588MB
<none>              <none>              59328245bd43        5 minutes ago       588MB

```

**Lưu ý:** trong quá trình Docker build image mới từ Dockerfile, nó có thể tạo ra các image tạm thời gây rác hệ thống. Để xóa các image tạm này hãy dùng lệnh:

``` bash
docker image prune
```

**Tạo - chạy một container từ image mới**

Image mới có tên `i-fitserver:version1` đã được buid ra, giờ bạn có thể tạo container từ nó như bất kỳ image nào khác. Ví dụ:

``` bash
docker run -it --name mywebserver -p 8888:80 -h firstserver i-firstserver:version1
```

Lệnh trên tạo ra một container có tên `mywebserver` từ image `i-firstserver:version1`, khi container chạy nó ánh xạ cổng `8888` vào cổng `80` của container (cổng HTTP đang chạy lắng nghe). Thử kiểm tra bằng gõ vào trình duyệt `http://localhost:8888`.

![Apache](https://raw.githubusercontent.com/xuanthulabnet/swift-learning/master/images/docker/centos-apache.png)

Container đã chạy thành công, điều đó chứng tỏ bạn đã có một image có sẵn `CentOS` và `Apache HTTPD`. Bạn cũng gõ `http://localhost:8888/test.html` để xem dữ liệu được copy vào có thành công!

# Các chỉ thị Dockerfile

Phần này tìm hiểu các chỉ thị cơ bản:

- `FROM` : mọi Docker file đều có chỉ thị này, chỉ định image cơ sở
- `COPY` `ADD` : sao chép dữ liệu
- `ENV` : thiết lập biến môi trường
- `RUN` : chạy các lệnh.
- `VOLUME` : gắn ổ đĩa, thư mục
- `USER` : user
- `WORKDIR` : thư mục làm việc
- `EXPOSE` : thiết lập cổng

### FROM Trong Dockerfile

Như trên đã nói, chỉ thị này chỉ ra image cơ sở để xây dựng nên image mới. Để xây dựng từ image nào đó thì bạn cần đọc document của Image đó để biết trong đó đang chứa gì, có thể chạy các lệnh gì trong đó ... Ví dụ, nếu bạn chọn xây dựng từ image `centos:laste` thì bạn bắt đầu bằng hệ điều hành CentOS và bạn có thể cài đặt, cập nhật các gói với `yum`, ngược lại nếu bạn chọn `ubuntu:latest` thì trình quản lý gói của nó là `APT` ...

### COPY và ADD Trong Dockerfile

Được dùng để thêm thư mục, file vào Image. Cú pháp viết đó là:

```
ADD thư_mục_nguồn thư_mục_đích
```

Trong đó `thư_mục_nguồn` là thư mục ở máy chạy Dockerfile, chứa dữ liệu cần thêm vào. `thư_mục_đích` là nơi dữ liệu được thêm vào ở container.

### ENV Trong Dockerfile

Chỉ thị này dùng để thiết lập biến môi trường, như biến môi trường `PATH` ..., tùy hệ thống hay ứng dụng yêu cầu biến môi trường nào thì căn cứ vào đó để thiết lập.

```
ENV biến giá_trị
```

### RUN Trong Dockerfile

Thi hành các lệnh, tương tự bạn chạy lệnh shell trên OS từ terminal.

```
RUN lệnh-và-tham-số-cần-chạy
```

```
RUN ["lệnh", "tham số1", "tham số 2" ...]
```

### VOLUME Trong Dockerfile

Chỉ thi tạo một ổ đĩa chia sẻ được giữa các container.

```
VOLUME /dir_vol
```

Xem thêm [Chia sẻ dữ liệu giữa các Container](https://xuanthulab.net/chia-se-du-lieu-giua-docker-host-va-container.html#sharecontainer)

### USER Trong Dockerfile

Bạn thêm user được dùng khi chạy các lệnh ở chỉ thị `RUN` `CMD` `WORKDIR`.

```
USER private
```
### WORKDIR Trong Dockerfile

Thiết lập thư mục làm việc hiện tại chi các chỉ thị `CMD`, `ENTRYPOINT`, `ADD` thi hành.

```
WORKDIR path_current_dir
```

### EXPOSE Trong Dockerfile

Để thiết lập cổng mà container lắng nghe, cho phép các container khác trên cùng mạng liên lạc qua cổng này hoặc đỉ ánh xạ cổng host vào cổng này.

```
EXPOSE port
```
### ENTRYPOINT, CMD Trong Dockerfile

Chạy lệnh trong chỉ thị này khi container được chạy.

```
ENTRYPOINT commnad_script
```

```
ENTRYPOINT ["command", "tham-số", ...]
```

`CMD` ý nghĩa tương tự như `ENTRYPOINT`, khác là lệnh chạy bằng shell của container.

```
CMD command param1 param2
```

Chú ý ở dạng sau của CMD thì nó lại là thiết lập tham số cho `ENTRYPOINT`

```
CMD ["tham-số1", "tham-số2"]
```

Đó là các chỉ thị cơ bản, đủ để bạn tự viết các `Dockerfile` xây dựng ra các image chứa các thành phần theo nhu cầu của mình. 