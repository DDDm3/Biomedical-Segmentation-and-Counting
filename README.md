# Biomedical Segmentation and Object Counting (BBBC005)

## Tổng quan dự án
Dự án nghiên cứu này tập trung vào bài toán phân đoạn ảnh tế bào và đếm số lượng đối tượng trong điều kiện ảnh bị mờ (focus blur), sử dụng bộ dữ liệu BBBC005 (Synthetic Cells).

Mục tiêu chính là so sánh hai hướng tiếp cận:
- Phương pháp truyền thống: Watershed và các kỹ thuật xử lý ảnh kinh điển.
- Phương pháp Machine Learning: K-Means clustering cho phân đoạn vùng tế bào.

## Danh sách thành viên

| STT | Họ và Tên | Lớp | MSSV | GitHub Account |
| :--: | :-------- | :--: | :--: | :------------- |
| 1 | Trần Viết Gia Huy | CS0001 | 31231027056 | @tommyhuy1705 |
| 2 | Nguyễn Minh Nhựt | CS0001 | [MSSV] | @github_nhut |
| 3 | Dương Quang Đông | CS0001 | 31231020389 | @DDDm3 |
| 4 | Nguyễn Minh Huy | CS0001 | [MSSV] | @github_huy |

## Cấu trúc thư mục chuẩn đề xuất

```text
biomedical-segmentation-and-counting/
|
|-- data/                       # Dữ liệu được tách riêng khỏi mã nguồn
|   |-- raw/                    # Ảnh BBBC005 gốc, chưa qua tiền xử lý
|   |-- ground_truth/           # Nhãn đối chiếu (ưu tiên các ảnh F1)
|   `-- details.md              # Mô tả metadata và quy tắc tổ chức dữ liệu
|
|-- notebooks/                  # Nơi thử nghiệm và phân tích tạm thời
|   |-- 01_eda_and_metadata.ipynb
|   |-- 02_traditional_segmentation.ipynb
|   |-- 03_ml_segmentation.ipynb
|   `-- 04_evaluation_metrics.ipynb
|
|-- src/
|   |-- __init__.py
|   |-- data_loader.py
|   |-- preprocess.py
|   |-- models.py
|   |-- algorithm.py
|   `-- evaluation.py -- tính toán metrics
|
|-- app/
|   |-- main.py
|   |-- components.py
|   `-- assets/
|
|-- README.md
|-- requirements.txt
`-- .gitignore
```

Lưu ý: Giai đoạn khởi tạo này chỉ tạo khung dự án và tài liệu mô tả; các file mã nguồn và notebook sẽ được bổ sung ở bước triển khai tiếp theo.

## Tóm tắt phương pháp thực hiện

### 1. Nhánh truyền thống (Traditional CV)
- Tiền xử lý ảnh bằng Gaussian Blur, CLAHE, Median Filter.
- Tách nền/đối tượng bằng thresholding (Otsu/Adaptive).
- Tách cụm tế bào bằng Distance Transform + Watershed.
- Đếm đối tượng bằng Connected Components/Contours.

### 2. Nhánh Machine Learning
- Biểu diễn pixel theo đặc trưng cường độ và lân cận.
- Phân cụm bằng K-Means để tách vùng tế bào và nền.
- Hậu xử lý mask để làm mượt biên và loại nhiễu nhỏ.
- So sánh kết quả đếm với nhãn thật được mã hóa trong tên file.

## Công nghệ sử dụng
- OpenCV
- Scikit-learn
- Streamlit

## Dữ liệu sử dụng
- Dataset: BBBC005 (Synthetic cells) từ Broad Bioimage Benchmark Collection.
- Tài liệu chi tiết về cấu trúc dữ liệu và metadata: xem file `data/details.md`.

## Ghi chú quản trị dự án
- Khuyến nghị đưa thư mục `data/` vào `.gitignore` để tránh commit dữ liệu lớn.
- Mọi thí nghiệm nên ghi nhận cấu hình và chỉ số đánh giá để phục vụ so sánh công bằng giữa các phương pháp.
