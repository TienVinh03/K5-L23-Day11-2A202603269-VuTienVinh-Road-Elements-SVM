# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): **Khởi - 2A202603290**

Người kiểm (học viên): **Vinh - 2A202603269**

Ngày: **20/11/2026**. Phiên bản guideline: **Road v1.0**.

File được kiểm: [`Khoi-font.zip`](../submissions/khoi/Khoi-font.zip), bản sao nguyên file trong Downloads, giữ đúng tên gốc. **Revision: chưa xác nhận vì chưa có manifest của Khởi**; không dùng manifest của Vinh cho lô này.

SHA-256: `b271c0a52ba80d184962a641e5bd429168656d9610a2b63ac5f7bf825f74dcc4`.

**Số ảnh kiểm: 6 — đúng sáu bản ghi ảnh đầu trong XML, tương ứng A01–A06 (+ 0 ảnh thêm). Không chấm A07 trở đi, không chấm fisheye.**

**Số nhãn đã kiểm: 67 = 43 shape + 24 tag**, gồm 13 lane, 12 drivable, 4 road_curb, 7 traffic_light, 4 crosswalk, 3 traffic_sign và 4 tag trên mỗi ảnh. Mỗi nhãn chỉ tính một lần vào mẫu số dù được rà theo nhiều mã.

| Ảnh | Shape | Tag | Tổng nhãn đã kiểm |
| --- | ---: | ---: | ---: |
| A01 | 7 | 4 | 11 |
| A02 | 6 | 4 | 10 |
| A03 | 4 | 4 | 8 |
| A04 | 11 | 4 | 15 |
| A05 | 3 | 4 | 7 |
| A06 | 12 | 4 | 16 |
| **Tổng** | **43** | **24** | **67** |

Phương pháp: trích riêng sáu ảnh đầu từ XML, đọc thuộc tính, chạy lint chỉ trên phần trích này và đối chiếu nhãn chồng lên ảnh gốc 1280 × 720 trong `data/`. Không có GT hoặc bảng kế hoạch nhóm label từng ảnh từ slide: không khẳng định đã đo sai lệch tối đa với GT, không tự tính mọi đối tượng chưa gán là lỗi bỏ sót. Đây là kết quả lấy mẫu sáu ảnh, không phải điểm chấm toàn bộ ZIP.

**Định danh:** `#n` là thứ tự shape **bắt đầu từ 0 trong từng ảnh XML**, không phải ID trên CVAT. Kèm tọa độ để tìm đúng hình. Minh chứng riêng của lô Khởi nằm trong [`out/qc-khoi-front/`](../out/qc-khoi-front/), không dùng overlay của lô Vinh. Các ảnh minh chứng chỉ phục vụ kiểm tra local.

## Tổng hợp theo mã

| Mã | Loại lỗi | Số mục kiểm | Số lỗi xác nhận | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 tag, trong đó 6 camera | 0 | nặng nếu sai camera; weather/timeofday xem ca mơ hồ |
| QC1-02 đủ L1, R1 | bỏ sót | 12 vị trí L1/R1 dự kiến trên 6 ảnh | 1 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 13 lane | 0 | nặng; ca A06 chờ lead |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 17 polyline: 13 lane + 4 road_curb | 1 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 13 lane | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 13 lane | 1 | chính |
| QC1-07 vùng lái, polygon | sai phạm vi / bỏ sót / thừa | 16 polygon: 12 drivable + 4 crosswalk | 7 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 7 traffic_light | 2 | 1 nặng, 1 chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 10 hộp: 7 đèn + 3 biển | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 3 biển đã gán; phạm vi cần bổ sung chờ slide | 0 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 — chỉ kiểm front | 0 | không áp dụng |
| QC1-12 file | lỗi file | 1 ZIP + 6 bản ghi ảnh trong mẫu | 0 | nhẹ / nặng |

ZIP mở được, đúng CVAT for images 1.1, không kèm ảnh. Sáu ảnh đủ bốn tag, `camera=front`, `source=real`; các giá trị đúng miền taxonomy. Giá trị hợp lệ không bảo đảm weather/timeofday đúng nội dung ảnh. Không ghi lỗi thiếu fisheye vì lượt này chỉ kiểm ZIP front. `0 lỗi xác nhận` không có nghĩa đã chứng minh không còn lỗi.

## Danh sách lỗi (mỗi lỗi một dòng)

| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn và hướng sửa |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-04 | A01 | lane #0, L1, đầu (362,507), cuối (113,720) | chính | Vẽ từ xa xuống gần xe. Đảo thứ tự các điểm để bắt đầu ở (113,720) rồi đi ra xa. [Ảnh](../out/qc-khoi-front/A01-lines.jpg). |
| 2 | QC1-06 | A01 | lane #1, R1, đầu gần (708,717) | chính | `style=solid` nhưng ảnh gốc có các đoạn sơn trắng đứt và khoảng trống rõ. Đổi thành dashed, vẫn giữ một polyline. [Phóng to ảnh gốc](../out/qc-khoi-front/A01-R1-detail.jpg). |
| 3 | QC1-07 | A02 | drivable #3, alternative | chính | Polygon giữa L1/R1 bao làn đang đi nhưng gán alternative. Đổi thành direct và rà lại biên. [Vùng](../out/qc-khoi-front/A02-regions.jpg), [vạch làn](../out/qc-khoi-front/A02-lines.jpg). |
| 4 | QC1-07 | A02 | drivable #5, direct, vùng ngoài cùng bên trái | chính | Làn bên trái L2, ngoài làn xe đang đi, lại được gán direct. Đổi phần làn cùng chiều đó thành alternative. Đây là polygon khác với #3, nên tính hai lỗi thuộc tính trên hai nhãn. [Ảnh](../out/qc-khoi-front/A02-regions.jpg). |
| 5 | QC1-02 | A03 | lane L1 chưa có; vạch vàng sát dải phân cách | nặng | Chỉ có R1/R2, trong khi vạch vàng bên trái làn đang đi nhìn thấy được. Bổ sung lane L1 trên tâm vạch vàng ở đoạn còn thấy; không lấy mép bó vỉa thay vạch sơn. [Ảnh](../out/qc-khoi-front/A03-lines.jpg). |
| 6 | QC1-07 | A04 | crosswalk #9, x≈3–273, y≈362–408 | chính | Polygon bao vỉa hè/miệng góc phố bên trái, không phải vùng vạch qua đường. Bỏ crosswalk sai đối tượng; chỉ vẽ khi có vạch thật. [Ảnh](../out/qc-khoi-front/A04-regions.jpg). |
| 7 | QC1-07 | A04 | crosswalk #10, x≈700–1276, y≈331–451 | chính | Polygon trải dọc vỉa hè bên phải, không phải vùng vạch qua đường. Xóa hoặc sửa đúng đối tượng. [Ảnh](../out/qc-khoi-front/A04-regions.jpg). |
| 8 | QC1-07 | A05 | crosswalk #1, x≈913–1277, y≈304–418 | chính | Bao vỉa hè sát tường và chân cột, không có vùng vạch qua đường tương ứng. Bỏ nhãn crosswalk sai đối tượng. [Ảnh](../out/qc-khoi-front/A05-regions.jpg). |
| 9 | QC1-07 | A05 | drivable #0, đỉnh gần (1,602) | chính | Góc dưới trái polygon đi xuống phần capô/thân xe mình. Cắt lại biên theo mép mặt đường–capô. Không khoét lỗ quanh xe khác che đường. [Ảnh](../out/qc-khoi-front/A05-regions.jpg). |
| 10 | QC1-07 | A06 | crosswalk #9, dải x≈695–1279, y≈406–536 bên phải | chính | Bao dải vỉa hè sau bó vỉa và chân cột. Vạch qua đường thật nằm ngang mặt đường phía trước xe, không phải dải dọc vỉa hè này. Bỏ vùng sai rồi vẽ cả vùng vạch thật nếu ảnh yêu cầu crosswalk. [Ảnh](../out/qc-khoi-front/A06-regions.jpg). |
| 11 | QC1-08 | A06 | traffic_light #7, hộp (286,121)–(369,159) | nặng | `facing=front`, `color=red` nhưng bóng xanh bên phải cụm đèn đang sáng rõ. Đổi color thành green. [Phóng to](../out/qc-khoi-front/boxes.jpg). |
| 12 | QC1-08 | A06 | traffic_light #4, pedestrian, hộp (912,338)–(968,367) | chính | Hộp thừa sang trái, gồm cột/nền; cụm đèn người đi bộ nằm chủ yếu khoảng x≈945–968. Thu hộp sát vỏ đèn. Màu WALK trắng được tách thành ca mơ hồ, không tính thêm lỗi màu. [Phóng to](../out/qc-khoi-front/boxes.jpg), [ảnh đầy đủ](../out/qc-khoi-front/A06-lines.jpg). |
| 13 | QC1-09 | A06 | traffic_sign #1, hộp (560,304)–(595,338) | chính | Biển hình thoi cam cảnh báo/công trường gán `group=prohibitory`. Đổi thành warning theo bảng nhóm biển Mỹ trong guideline. [Phóng to](../out/qc-khoi-front/boxes.jpg). |

## Ca mơ hồ

Chưa cộng các mục sau vào số lỗi xác nhận. Câu hỏi và đề xuất của người kiểm không được coi là lời đáp của lead.

| Mã ca | Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- | --- |
| M1 | A03–A05 | Đều đặt weather=clear, nhưng A04/A05 nhiều mây, A03 ánh sáng cuối ngày. Xin chốt weather từng ảnh và day/dusk ở A03; sai weather nhưng không sai camera ghi mức nào theo quy ước lớp? | Chưa có. A04/A05 nghiêng về overcast; không tự nâng thành lỗi camera nặng. |
| M2 | A05 | Không thấy vạch sơn dọc trên phố có xe đỗ hai bên. Xác nhận ngoại lệ thiếu L1/R1 và chốt hành lang direct để tránh gộp phần ngược chiều/dải đỗ? | Chưa có. Không tạo lane từ thân xe/khoảng trống giữa xe đỗ để hết lint. |
| M3 | A06 | Lane #0 (446,422)→(503,365) bám vạch sơn dọc thật hay mép xe đỗ/khoảng trống? R1 không thấy độc lập: ngoại lệ hay đoạn che ngắn cần nối? | Chưa có. Chưa tính lane #0 là nhãn thừa hoặc thiếu R1 là lỗi nặng khi chưa rõ vạch thật. |
| M4 | A03 | Lane #1 R2/dashed là vạch phân làn chạy xe hay biên dải đỗ? Cần bỏ, đổi other hay giữ R2? Nếu là vạch liền, style phải solid. Alternative #3 có lấy dải đỗ không? | Chưa có. Cần chốt theo chức năng đường. |
| M5 | A06 | Đèn người đi bộ #4 hiển thị WALK trắng, taxonomy không có white: giữ unknown hay quy ước green? Cụm #11 góc trên trái nhìn nghiêng: facing nên side hay back? | Chưa có. Chưa tính thêm lỗi thuộc tính cho hai tình huống này. |
| M6 | A01–A06 | Xin bảng kế hoạch nhóm label từng ảnh từ slide để kiểm bỏ sót biển/đèn, ví dụ biển xanh A01, biển cảnh báo A03. Không mặc nhiên yêu cầu mọi class trên mọi ảnh. | Chưa có. Chưa cộng lỗi bỏ sót nhóm chưa rõ phạm vi; lỗi trên hình đã gán vẫn được ghi nhận. |

## Quyết định

**Lỗi nặng: 2. Lỗi chính: 11 / 67 nhãn = 16,42 %. Lỗi nhẹ: 0. Ca chờ lead: 6.**

**Quyết định: Rework.**

Lý do: có lỗi nặng xác nhận ở **A03 thiếu L1 nhìn thấy được** và **A06 đèn xanh hướng về xe bị gán đỏ**. Đồng thời tỉ lệ lỗi chính 16,42 % vượt ngưỡng 5 %. Một trong hai điều kiện đã đủ Rework; các ca chờ lead không đổi thành Hold khi còn lỗi chắc chắn. Kết luận áp dụng cho mẫu **A01–A06**, không phải mọi ảnh trong file.

Thứ tự sửa và kiểm lại:

1. Sửa màu đèn A06 #7; bổ sung lane L1 trên vạch vàng A03.
2. Đảo chiều lane A01 #0, đổi style #1; sửa direct/alternative A02.
3. Sửa bốn crosswalk gán trên vỉa hè ở A04/A05/A06; cắt capô khỏi drivable A05; thu hộp đèn người đi bộ và đổi group biển cam A06.
4. Xin lead trả lời M1–M6, lưu ngoại lệ không thấy vạch. Sửa trên CVAT, export lại và kiểm đúng sáu ảnh này sau Rework.
5. Giữ ZIP trước sửa. Yêu cầu manifest của Khởi để xác nhận revision; khi nộp lại tăng revision theo [đặc tả bàn giao](../docs/delivery_road_v1.0.md). Không lấy revision của lô Vinh làm revision của Khởi.

Phiếu có hỗ trợ đọc XML và đối chiếu ảnh bằng AI; người kiểm học viên cần xác nhận trước khi bàn giao. Chưa có lời đáp chính thức của lead hoặc kết quả so GT. Thang mức và luật quyết định theo [QC severity Road v1.0](../docs/qc_severity_road_v1.0.md); quy tắc gán theo [guideline](../docs/guideline_road_v1.0.md).
