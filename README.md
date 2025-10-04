# bt7
# HovaTenSV_BT07.py
# Bài tập 07 - Xử lý ảnh bằng OpenCV
# Họ và tên: Bùi Văn Quag
import cv2
import numpy as np

# ===============================
# 1. Đọc ảnh màu lena.jpg và hiển thị
# ===============================
Img = cv2.imread('lena.jpg')
if Img is None:
    print("Không tìm thấy file lena.jpg! Hãy chắc chắn rằng file nằm cùng thư mục với chương trình.")
    exit()

cv2.imshow("Anh goc - Img", Img)

# ===============================
# 2. Chuyển ảnh sang hệ HSV và hiển thị kênh V
# ===============================
ImgHSV = cv2.cvtColor(Img, cv2.COLOR_BGR2HSV)
H, S, V = cv2.split(ImgHSV)
cv2.imshow("Kenh V", V)

# ===============================
# 3. Xác định chiều cao, chiều rộng ảnh
# ===============================
chieu_cao, chieu_rong, kenh = Img.shape
print("Chiều cao ảnh:", chieu_cao)
print("Chiều rộng ảnh:", chieu_rong)
print("Số kênh màu:", kenh)

# ===============================
# 4. Tạo ảnh nhị phân theo ngưỡng Otsu
# ===============================
ImgXam = cv2.cvtColor(Img, cv2.COLOR_BGR2GRAY)
nguong, ImgO = cv2.threshold(ImgXam, 0, 255, cv2.THRESH_BINARY + cv2.THRESH_OTSU)
print("Ngưỡng Otsu =", nguong)
cv2.imshow("Anh nhi phan Otsu - ImgO", ImgO)

# ===============================
# 5. Làm trơn ảnh theo bộ lọc trung bình 5x5
# ===============================
ImgT = cv2.blur(Img, (5, 5))
cv2.imshow("Anh lam tron 5x5 - ImgT", ImgT)

# ===============================
# 6. (Tùy chọn - nếu học rồi) Dùng Canny lấy biên ảnh
# ===============================
ImgB = cv2.Canny(ImgXam, 100, 200)
cv2.imshow("Anh bien Canny - ImgB", ImgB)

# ===============================
# 7. (Tùy chọn) Vẽ các đường contour lên ảnh gốc
# ===============================
contours, _ = cv2.findContours(ImgB, cv2.RETR_EXTERNAL, cv2.CHAIN_APPROX_SIMPLE)
ImgContour = Img.copy()
cv2.drawContours(ImgContour, contours, -1, (0, 0, 255), 1)
cv2.imshow("Anh co contour - ImgContour", ImgContour)

# ===============================
# Kết thúc
# ===============================
cv2.waitKey(0)
cv2.destroyAllWindows()
