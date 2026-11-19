# BÀI TẬP THỰC HÀNH TỔNG HỢP
## XÂY DỰNG HỆ THỐNG GIA SƯ AI VÀ CHẤM BÀI TỰ ĐỘNG

### 1. Thiết kế giải pháp

Xây dựng chatbot hỗ trợ học tập bằng Prompt Chaining gồm 4 bước:

1. Kiểm tra dữ liệu đầu vào.
2. Giải thích kiến thức theo phương pháp Feynman.
3. Chấm bài theo Rubric.
4. Tổng hợp điểm số và hướng cải thiện.

**Input:** Câu hỏi, câu trả lời của sinh viên và rubric.

**Output:** Giải thích kiến thức, điểm số, nhận xét và đề xuất cải thiện.

### 2. Prompt hệ thống (System Prompt)

```text
Bạn là ChatBot gia sư AI hỗ trợ học tập.
Thực hiện quy trình Prompt Chaining gồm 4 bước:
kiểm tra dữ liệu, giải thích Feynman, chấm Rubric,
tổng hợp kết quả.
Không tự bịa dữ liệu hoặc điểm số.
Nếu thiếu dữ liệu, hãy yêu cầu bổ sung.
Trả lời ngắn gọn và chính xác.
```

### 3. Thực thi Prompt Chaining

**Bước 1: Kiểm tra dữ liệu**

Prompt:
```text
Kiểm tra dữ liệu sau:
Câu hỏi: CPU là gì?
Câu trả lời: CPU là bộ nhớ lưu trữ dữ liệu.

Xác định dữ liệu có đầy đủ, hợp lệ không.
Kiểm tra xem có thiếu thông tin cần thiết không.
```

**Kết quả Gemini:**

### 1. Tính đầy đủ và hợp lệ của dữ liệu

* **Về cấu trúc dữ liệu (Đầy đủ về mặt trường thông tin):** Cặp dữ liệu có đủ 2 trường cơ bản là **Câu hỏi** và **Câu trả lời**, không bị rỗng hay sai định dạng.
* **Về tính chính xác / hợp lệ về mặt kiến thức (Không hợp lệ / Sai):** Câu trả lời **"CPU là bộ nhớ lưu trữ dữ liệu"** là **sai** về mặt kỹ thuật.
* **CPU (Central Processing Unit - Bộ xử lý trung tâm)** có chức năng chính là **xử lý dữ liệu, thực hiện phép tính và điều khiển hoạt động** của máy tính (thông qua các thành phần như ALU, CU và các thanh ghi).
* **Bộ nhớ lưu trữ dữ liệu** là vai trò của **RAM** (bộ nhớ truy cập ngẫu nhiên - lưu tạm thời khi đang chạy) hoặc **ổ cứng / SSD / HDD** (lưu trữ lâu dài), chứ không phải chức năng chính của CPU.



---

### 2. Kiểm tra thông tin cần thiết còn thiếu

* **Trong câu trả lời:** Thiếu định nghĩa đúng về vai trò **xử lý và điều khiển** của CPU, cũng như sự phân biệt cơ bản giữa **bộ xử lý (CPU)** và **bộ nhớ lưu trữ (RAM / ổ cứng)**.
* **Trong ngữ cảnh dữ liệu (tùy mục đích sử dụng):** Nếu đây là dữ liệu dùng để huấn luyện AI, đánh giá/chấm điểm, hoặc lưu trữ trong hệ thống quản lý học tập/dataset, có thể cân nhắc bổ sung thêm các trường metadata như:
* **Đáp án chuẩn / ground truth** (để đối chiếu đúng/sai).
* **Trạng thái kiểm duyệt / nhãn đúng-sai** (ví dụ: `is_valid: false`).
* **Giải thích / nguồn tham khảo** (nêu lý do vì sao câu trả lời hiện tại chưa chính xác).



---

### 3. Gợi ý câu trả lời chuẩn để thay thế

> **CPU (Central Processing Unit - Bộ xử lý trung tâm)** là thành phần thực hiện việc **xử lý dữ liệu, tính toán và điều khiển** các hoạt động của máy tính theo chương trình đã cài đặt; CPU không phải là thiết bị lưu trữ dữ liệu chính như RAM hay ổ cứng.

---

**Bước 2: Giải thích theo Feynman**

Prompt:
```text
Dựa trên kết quả kiểm tra bước 1, hãy giải thích
khái niệm CPU theo phương pháp Feynman.
Sử dụng ngôn ngữ đơn giản và ví dụ dễ hiểu.
```

**Kết quả Gemini:**
### Bước 1: Chỉ ra chỗ sai ban đầu

Ở bước kiểm tra trước, ta thấy nhận định *"CPU là bộ nhớ lưu trữ dữ liệu"* bị nhầm vai trò. Nếu coi máy tính như một gian bếp:

* **Ổ cứng / SSD** là **tủ lạnh / kho lương thực** (cất giữ nguyên liệu và công thức nấu ăn lâu dài).
* **RAM** là **mặt bàn bếp** (đặt sẵn nguyên liệu bạn đang dùng ngay lúc này).
* **CPU** chính là **người đầu bếp** (đọc công thức, ra lệnh, cắt gọt, nêm nếm và biến nguyên liệu thành món ăn).

Người đầu bếp không phải cái kho chứa đồ — người đầu bếp là nơi mọi thao tác thực sự diễn ra.

---

### Bước 2: Giải thích CPU bằng ngôn ngữ đơn giản nhất

**CPU (Central Processing Unit — Bộ xử lý trung tâm)** là **"bộ não điều hành"** của máy tính. Nhiệm vụ của nó không phải là cất giữ nhiều dữ liệu, mà là **nhận lệnh, tính toán và điều phối** mọi thứ chạy đúng trình tự hàng tỷ lần mỗi giây.

Bên trong "người đầu bếp" CPU có thể hình dung ba bộ phận chính:

* **Đơn vị điều khiển (CU):** Giống như trưởng bếp đọc công thức và ra lệnh: *"Lấy số này, cộng số kia, rồi gửi kết quả ra màn hình."*
* **Đơn vị số học và logic (ALU):** Giống như đôi tay làm phép tính nhanh (cộng, trừ, so sánh lớn hơn, nhỏ hơn, bằng nhau...).
* **Thanh ghi (RF):** Giống như chiếc đĩa nhỏ ngay trước mặt đầu bếp để giữ tạm vài con số đang tính ngay tức thì — cực nhanh nhưng sức chứa rất nhỏ.

---

### Bước 3: Ví dụ thực tế dễ hiểu

Giả sử bạn bấm máy tính để tính **12 + 8** rồi hiện kết quả lên màn hình:

1. **Lấy dữ liệu:** Máy tính đưa số `12`, số `8` và phép cộng `+` vào vùng làm việc để CPU tiếp nhận.
2. **Điều khiển & tính toán:** Bộ điều khiển (CU) nhận lệnh cộng, đưa `12` và `8` vào bộ tính toán (ALU). ALU tính ra `20`.
3. **Trả kết quả:** CPU gửi kết quả `20` đi để hiển thị lên màn hình cho bạn thấy.

Toàn bộ quá trình này diễn ra nhanh đến mức mắt thường gần như không nhận ra độ trễ.

---

### Bước 4: Tự kiểm tra lại (Tránh "ảo tưởng hiểu bài")

Nếu có ai hỏi *"Thế CPU có lưu file ảnh hay phim không?"*, bạn có thể trả lời gọn gàng rằng: **Không lưu trữ lâu dài.** File ảnh hay phim nằm ở ổ cứng; khi mở xem, dữ liệu được đưa qua RAM rồi CPU xử lý giải mã để hiển thị lên màn hình.

### Kết luận

**CPU là bộ xử lý và điều khiển trung tâm của máy tính — nơi thực hiện tính toán và ra lệnh cho các bộ phận hoạt động, chứ không phải nơi lưu trữ dữ liệu.**
---

**Bước 3: Chấm điểm theo Rubric**

Prompt:
```text
Chấm câu trả lời ban đầu theo Rubric 10 điểm:
- Hiểu khái niệm CPU: 4 điểm.
- Giải thích chức năng: 2 điểm.
- Phân biệt CPU và RAM: 2 điểm.
- Trình bày chính xác: 2 điểm.

Mỗi tiêu chí phải có điểm và lý do cụ thể.
Thiếu nội dung thì không tự suy đoán.
Tính tổng điểm trên thang 10.
```

**Kết quả Gemini:**

Dưới đây là kết quả chấm cho câu trả lời ban đầu: **"CPU là bộ nhớ lưu trữ dữ liệu."** theo Rubric 10 điểm:

| Tiêu chí | Điểm đạt được | Điểm tối đa | Lý do cụ thể |
| --- | --- | --- | --- |
| **Hiểu khái niệm CPU** | **0** | 4 | Câu trả lời đồng nhất CPU với bộ nhớ lưu trữ dữ liệu, không phản ánh đúng khái niệm bộ xử lý trung tâm của máy tính. |
| **Giải thích chức năng** | **0** | 2 | Không nêu được các chức năng thực sự của CPU (xử lý dữ liệu, tính toán, điều khiển thực thi lệnh) mà gán sai chức năng lưu trữ. |
| **Phân biệt CPU và RAM** | **0** | 2 | Không đề cập đến RAM và không có bất kỳ nội dung nào phân biệt CPU với RAM (không tự suy đoán thêm). |
| **Trình bày chính xác** | **0** | 2 | Dù câu ngắn gọn, rõ mặt chữ nhưng nội dung khẳng định sai bản chất kỹ thuật của CPU nên không đạt điểm chính xác. |

---

### Tổng điểm: **0 / 10 điểm**

---

**Bước 4: Tổng hợp kết quả**

Prompt:
```text
Dựa trên kết quả bước 2 và bước 3,
hãy tổng hợp báo cáo gồm:
1. Kiến thức sinh viên cần hiểu.
2. Bảng điểm theo Rubric.
3. Những lỗi sai cần khắc phục.
4. Hướng cải thiện cụ thể.

Trình bày ngắn gọn, rõ ràng, không thêm
điểm số hoặc thông tin chưa được xác nhận.
```

**Kết quả Gemini:**

### 1. Kiến thức sinh viên cần hiểu

* **Khái niệm CPU:** CPU (Central Processing Unit — Bộ xử lý trung tâm) là bộ phận điều hành và xử lý trung tâm của máy tính, thực hiện tính toán và điều phối hoạt động theo chương trình.
* **Chức năng chính của CPU:** Nhận lệnh, điều khiển thực thi và tính toán (số học, logic), đồng thời dùng các thanh ghi (RF) để giữ tạm dữ liệu đang tính ngay tức thì.
* **Phân biệt CPU, RAM và ổ cứng/SSD:**
* **CPU:** Bộ phận trực tiếp xử lý, tính toán và điều khiển (ví dụ: người đầu bếp).
* **RAM:** Bộ nhớ tạm thời phục vụ dữ liệu đang dùng ngay lúc đó (ví dụ: mặt bàn bếp).
* **Ổ cứng / SSD:** Nơi lưu trữ dữ liệu và chương trình lâu dài (ví dụ: tủ lạnh / kho lương thực).



---

### 2. Bảng điểm theo Rubric

| Tiêu chí | Điểm đạt được | Điểm tối đa | Lý do cụ thể |
| --- | --- | --- | --- |
| **Hiểu khái niệm CPU** | **0** | 4 | Đồng nhất CPU với bộ nhớ lưu trữ dữ liệu, chưa nêu đúng khái niệm bộ xử lý trung tâm. |
| **Giải thích chức năng** | **0** | 2 | Không nêu được chức năng xử lý, tính toán và điều khiển thực thi lệnh; gán sai chức năng lưu trữ. |
| **Phân biệt CPU và RAM** | **0** | 2 | Không đề cập đến RAM và không có nội dung phân biệt CPU với RAM. |
| **Trình bày chính xác** | **0** | 2 | Nội dung khẳng định sai bản chất kỹ thuật của CPU nên không đạt điểm chính xác. |

**Tổng điểm:** **0 / 10 điểm**

---

### 3. Những lỗi sai cần khắc phục

* **Nhầm lẫn bản chất:** Khẳng định *"CPU là bộ nhớ lưu trữ dữ liệu"* đồng nghĩa với việc xem CPU như thiết bị lưu trữ.
* **Gán sai chức năng:** Quy cho CPU chức năng lưu trữ thay vì chức năng xử lý, tính toán và điều khiển.
* **Thiếu so sánh/phân biệt:** Không phân biệt vai trò xử lý của CPU với vai trò lưu trữ của RAM hoặc ổ cứng.

---

### 4. Hướng cải thiện cụ thể

* **Nắm lại bản chất bằng ngôn ngữ đơn giản:** Diễn đạt CPU là bộ xử lý và điều khiển trung tâm, gắn với các thành phần như đơn vị điều khiển (CU), đơn vị số học và logic (ALU), thanh ghi (RF).
* **Gắn với ví dụ trực quan:** Dùng phép so sánh người đầu bếp (CPU), mặt bàn bếp (RAM), và tủ lạnh/kho lương thực (ổ cứng/SSD) để ghi nhớ rõ sự khác biệt.
* **Tự kiểm tra qua luồng xử lý thực tế:** Kiểm chứng lại bằng cách mô tả quy trình lấy dữ liệu, tính toán và xuất kết quả (như phép tính đơn giản hoặc mở tệp hiển thị lên màn hình) để tránh nhầm CPU với bộ lưu trữ.
