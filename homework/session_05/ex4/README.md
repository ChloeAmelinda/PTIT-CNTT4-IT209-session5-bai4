\# Bài 4: Mô phỏng quy trình Hotfix \& Gitflow thực tế



\## 1. Mục tiêu



Bài thực hành mô phỏng quy trình xử lý một lỗi nghiêm trọng trên hệ thống production bằng mô hình Gitflow.



Hệ thống gồm:



\- `main`: chứa phiên bản production ổn định.

\- `develop`: chứa các chức năng đang phát triển.

\- `hotfix/v1.0.1`: dùng để sửa lỗi khẩn cấp từ nhánh `main`.



\## 2. Quy trình thực hiện



\### Bước 1: Tạo phiên bản production v1.0.0



```bash

git init

git branch -M main



git add app.txt

git commit -m "release: version 1.0.0"



git tag -a v1.0.0 -m "Release version 1.0.0"

```



\### Bước 2: Tạo nhánh develop



```bash

git checkout -b develop

```



Tạo một tính năng đang phát triển và commit:



```bash

git add feature.txt

git commit -m "feat: develop new feature"

```



\### Bước 3: Tạo nhánh Hotfix từ main



Chuyển về `main`:



```bash

git checkout main

```



Tạo nhánh sửa lỗi khẩn cấp:



```bash

git checkout -b hotfix/v1.0.1

```



Sau khi sửa lỗi:



```bash

git add security-fix.txt

git commit -m "fix: prevent user data exposure"

```



\### Bước 4: Merge Hotfix vào main



```bash

git checkout main



git merge --no-ff hotfix/v1.0.1 -m "merge: hotfix v1.0.1 into main"

```



Tạo tag phiên bản mới:



```bash

git tag -a v1.0.1 -m "Release Hotfix 1.0.1"

```



\### Bước 5: Merge Hotfix ngược vào develop



```bash

git checkout develop



git merge --no-ff hotfix/v1.0.1 -m "merge: hotfix v1.0.1 into develop"

```



Việc merge Hotfix vào `develop` giúp đảm bảo lỗi đã sửa trên production không xuất hiện lại trong các phiên bản phát triển sau này.



\## 3. Sơ đồ Gitflow



```text

&#x20;                  hotfix/v1.0.1



