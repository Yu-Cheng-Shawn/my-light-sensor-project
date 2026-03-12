# my-light-sensor-project
Python OpenCV 光電影像辨識專案
# Light Sensor & Image Recognition Project
High school self-learning project using Python + OpenCV / Arduino.  
Demonstrates problem-solving and engineering thinking for NTUST IICT & NTUT Engineering Tech.
Add OpenCV image recognition project + screenshots
## 完整可執行程式碼
- Google Colab 即時運行版：  
  [點我開啟 Colab]

## 專案檔案
- `import cv2
import matplotlib.pyplot as plt


img = cv2.imread('1.jpg')
gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
edges = cv2.Canny(gray, 100, 200)

# 顯示三張圖
plt.figure(figsize=(15,5))
plt.subplot(1,3,1); plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB)); plt.title('Original')
plt.subplot(1,3,2); plt.imshow(gray, cmap='gray'); plt.title('Grayscale')
plt.subplot(1,3,3); plt.imshow(edges, cmap='gray'); plt.title('Edge Detection')
plt.show()
hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
lower_yellow = (20, 100, 100)
upper_yellow = (30, 255, 255)
mask = cv2.inRange(hsv, lower_yellow, upper_yellow)
plt.imshow(mask, cmap='gray'); plt.title('Defect Detection'); plt.show()

# 計算檢測到的黃色區域數量
num_labels, labels_img, stats, centroids = cv2.connectedComponentsWithStats(mask, 8, cv2.CV_32S)

num_yellow_regions = num_labels - 1

print(f"檢測到的黃色區域數量: {num_yellow_regions}")

output_image = cv2.cvtColor(img, cv2.COLOR_BGR2RGB).copy()
if num_yellow_regions > 0:
    for i in range(1, num_labels): # 從 1 開始，跳過背景
        # 隨機生成顏色
        color = (255, 0, 0) # 可以是隨機顏色 (R, G, B)

        # 繪製邊界框
        x = stats[i, cv2.CC_STAT_LEFT]
        y = stats[i, cv2.CC_STAT_TOP]
        w = stats[i, cv2.CC_STAT_WIDTH]
        h = stats[i, cv2.CC_STAT_HEIGHT]
        cv2.rectangle(output_image, (x, y), (x + w, y + h), color, 2)

        # 在中心點繪製文本
        center_x, center_y = int(centroids[i][0]), int(centroids[i][1])
        cv2.putText(output_image, str(i), (center_x - 10, center_y - 10), cv2.FONT_HERSHEY_SIMPLEX, 0.5, color, 2)

plt.figure(figsize=(10, 8))
plt.imshow(output_image)
plt.title(f'Detected Yellow Regions: {num_yellow_regions}')
plt.show()`（完整程式碼）
- 成果截圖資料夾（original / edges / defect）
