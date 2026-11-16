# Design QA — HOMI Learning Loop timeline

## Comparison target

- Source visual truth: `C:\Users\DELL\AppData\Local\Temp\codex-clipboard-6a6b767e-c892-4fb6-829e-774c2e295aa4.png`.
- Implementation: `D:\Code\HuaMei\App_noi\LandingPageKombai\home_homi.html`.
- Implementation preview: `http://127.0.0.1:4173/home_homi.html#phuong-phap`.
- Verified desktop viewport: 1600 × 900 CSS px.

## Findings

- Không còn P0, P1 hoặc P2.
- Bốn mốc giữ viền trắng, quầng sáng và bóng đổ nhưng đã được thu nhỏ 30% theo yêu cầu mới.
- Đường timeline được tăng độ dày; nút kết nối nhỏ nằm đúng tại mép phải của từng mốc.
- Mốc 4 dùng màu vàng và quầng sáng riêng để thể hiện trạng thái kết thúc.
- Nội dung chữ bên phải không thay đổi và không bị timeline che phủ.

## Verification evidence

- Browser render: các mốc 1–3 đo được 53 × 53 px; mốc 4 đo được 59 × 59 px, tương đương 70% kích thước trước.
- Font số trong mốc: 22 px trên desktop.
- Chart width: 531 px; không có overflow ngang ở viewport desktop.
- Mobile CSS chuyển các mốc về 43 × 43 px, bỏ nút nối khi SVG được ẩn, giữ bố cục gọn và dễ đọc.

## Comparison history

- Earlier P2: các mốc 76–84 px lớn hơn mật độ mong muốn trong ảnh cập nhật của người dùng.
- Fix: giảm đồng bộ kích thước mốc, chữ số, viền, quầng sáng, bóng đổ, connector và khoảng cách xuống khoảng 30%; dịch đường timeline để giữ thẳng hàng.
- Post-fix evidence: browser đo được 53 px cho mốc 1–3 và 59 px cho mốc 4; không có overflow ngang.
- Latest scoped change: đã xóa riêng đường cong nét đứt theo ảnh đánh dấu, giữ nguyên đường timeline thẳng và nhãn “Lặp lại theo tiến độ của con”.
- Post-change evidence: SVG của HOMI Learning Loop chỉ còn một path là đường dọc; trình duyệt không có overflow ngang hoặc lỗi console.
- Mobile order CTA: container dùng flex với chiều cao tối thiểu 720 px và padding dọc đối xứng để nội dung được căn giữa theo chiều dọc.
- Mobile verification: tại breakpoint mobile, sai lệch tâm giữa content và section là 0 px; không có overflow ngang hoặc lỗi console.
- Mobile hero redesign: tiêu đề, mô tả và dòng độ tuổi được căn giữa; hai CTA hiển thị cùng hàng; ảnh nền được phóng lên 55% chiều cao và canh 88% về bên phải để hiển thị đồng thời mẹ và bé.
- Mobile hero evidence: browser xác nhận `text-align: center`, CTA dùng `flex-direction: row`, background position `88% 100%`; không có overflow ngang hoặc lỗi console.
- Career slider redesign: nút trước/sau được đặt ngoài hai mép card ở desktop, dots căn giữa bên dưới; card vẫn dùng scroll snap và thao tác điều hướng hoạt động.
- Career desktop evidence: nút Next đã đưa `scrollLeft` từ 0 lên 1171 px; dots lệch tâm không đáng kể 8 px và không gây overflow.
- Career mobile evidence: wrapper nút điều hướng có `display: none`, hai nút có kích thước render 0 px; viewport dùng `touch-action: pan-x`, card chừa 32 px để gợi ý còn nội dung có thể vuốt tiếp.
- Career navigation final: hai nút chevron trắng 38 × 38 px được đặt chồng chính xác vào tâm mép trái/phải của slider; trạng thái cuối vòng tự quay về nhóm đầu.
- Career motion evidence: click Next chuyển `scrollLeft` từ 0 lên 1171.25 px bằng native smooth scrolling; lớp chuyển tiếp tạo lift/opacity nhẹ trong 420 ms.
- Final responsive evidence: desktop hiển thị controls dạng flex, mobile ẩn controls và giữ `touch-action: pan-x`; không có console error/warning.
- FAQ accordion behavior: trạng thái ban đầu chỉ mở câu 01; khi chọn câu 02, câu 01 chuyển sang `collapsed` và câu 02 chuyển sang `expanded` trong cùng một thao tác.
- FAQ accessibility evidence: `aria-expanded` được đồng bộ cho cả mục vừa đóng và mục vừa mở; biểu tượng cộng/trừ tiếp tục phản ánh đúng trạng thái.
- FAQ sequential transition: khi chọn câu mới, mục đang mở được gỡ trạng thái trước; JavaScript chờ sự kiện `transitionend` của `max-height` (fallback 500 ms) rồi mới mở mục đích.
- FAQ sequential verification: sau khi chuyển từ câu 01 sang câu 02, chỉ câu 02 ở trạng thái `expanded`; câu 01 đã `collapsed`, không tồn tại giai đoạn hai nội dung cùng mở.
- Mobile hero image source: `assets/images/hero-banner-mobile.png`, ảnh dọc 2:3 được outpaint từ chính ảnh hero ngang để giữ nguyên mẹ, bé, thiết bị HOMI và bộ sách.
- Mobile hero verification: breakpoint dưới 768 px dùng riêng ảnh dọc, canh `center bottom` và `background-size: 100% auto`; phần chữ nằm trên vùng tường sáng, chủ thể và sách hiển thị ở nửa dưới mà không kéo giãn.
- Desktop isolation: ảnh `assets/images/hero-banner.png` và cách bố trí hero desktop không thay đổi.
- Chrome mobile whitespace fix: giảm `padding-top` của khối nội dung hero từ 48 px xuống 12 px, giữ `padding-bottom` 48 px để không làm dồn CTA và ảnh.
- Chrome verification: ảnh chụp trực tiếp trên Chrome mobile cho thấy tiêu đề bắt đầu ngay dưới header với khoảng thở nhỏ, không còn dải trắng dư phía trên; ảnh nền và section kế tiếp vẫn nối liền bình thường.
- Mobile order CTA overlay: giảm lớp phủ navy từ mức `.97/.92` xuống `.94/.82`, đưa vùng chuyển sáng chính lên đúng mốc 50% và kết thúc về trong suốt ở cuối ảnh.
- Overlay intent: nửa trên vẫn giữ tương phản cho chữ trắng; khuôn mặt, áo và sách ở nửa dưới hiển thị rõ hơn, trong khi desktop giữ nguyên gradient ngang hiện tại.
- Mobile order CTA alignment: nhóm “Đăng ký mua Homi” và “Nhắn Zalo để được tư vấn” dùng `align-items: flex-start`; nội dung của cả hai CTA căn trái và bắt đầu cùng một trục với phần mô tả.
- Mobile primary CTA sizing: nút chính không còn kéo giãn toàn chiều rộng; chuyển sang `width: auto`, `min-width: 232px`, padding `13px 26px`, đồng thời vẫn giữ vùng chạm tối thiểu 44 px.
- Scope verification: các điều chỉnh chỉ nằm trong breakpoint dưới 768 px; bố cục CTA desktop không thay đổi.
- Language switcher: thêm nút Việt–Trung trên header, chuyển nội dung chính, CTA, bảng giá, FAQ, tuyển dụng và footer mà không tải lại trang.
- Language persistence: lựa chọn được lưu trong `localStorage` với khóa `homi-language` và tự khôi phục sau khi tải lại.
- Language accessibility: đồng bộ thuộc tính `lang`, nhãn chuyển đổi và nhãn menu mobile cho cả tiếng Việt và tiếng Trung; font Trung Quốc có fallback Microsoft YaHei/PingFang SC/Noto Sans SC.
- Language verification: đã kiểm tra trực tiếp trên mobile — chuyển VI → 中文 và 中文 → VI đều khôi phục đúng nội dung, không làm mất trạng thái FAQ hay điều hướng trang.
- Floating language control: nút chuyển ngôn ngữ đã được đưa ra khỏi header và cố định ở góc dưới bên phải (`right/bottom: 24px` desktop, `16px` mobile với safe-area inset), z-index 70 và vùng bấm tối thiểu 44 px.
- Floating control verification: accessibility tree xác nhận nút là phần tử độc lập sau nội dung trang, không còn nằm trong `site-header`; header mobile chỉ còn logo, CTA đặt hàng và menu.
- Removed speaking-hours ledger: đã xóa toàn bộ khối “Số giờ nói thực tế quyết định mức độ trôi chảy của con”, gồm timeline 0/100/400 giờ, CSS responsive/state và ScrollTrigger liên quan.
- Removal verification: sau khi tải lại, accessibility tree chuyển trực tiếp từ ba thẻ minh họa trong `#noi-dau` sang section `#phuong-phap`; không còn `#hour-ledger` hoặc nội dung timeline.
- Full Vietnamese–Chinese audit: bổ sung bản dịch cho dòng độ tuổi hero, nhãn vòng lặp, ví dụ bài học, toàn bộ lời chứng thực, bảng giá, CTA, FAQ ẩn, tuyển dụng, footer và thông tin liên hệ.
- Translation accessibility: dịch đồng bộ `aria-label`, `alt`, `title` và `placeholder`, bao gồm nhãn slider tuyển dụng được tạo động.
- Bidirectional verification: chuyển 中文 → VI → 中文 khôi phục đúng nội dung; kiểm tra DOM không còn câu tiếng Việt trong bản Trung ngoài ký hiệu tiền tệ `đ` và tên riêng tác giả ảnh; không có lỗi console.

## Required fidelity surfaces

- Shape: mốc tròn lớn, viền trắng và connector ring rõ ràng.
- Color: turquoise cho 1–3; vàng cho 4; navy cho chữ mốc cuối.
- Depth: quầng màu mềm và bóng đổ nhẹ, không làm mờ nội dung.
- Layout: đường dọc thẳng hàng với connector của cả bốn mốc.

## Hòa Mỹ section — 2026-09-19

- Source visual truth: `C:\Users\DELL\AppData\Local\Temp\codex-clipboard-77af5fbf-0510-4989-bd67-051ccffbde69.png` (1024 × 410 px).
- Implementation: `D:\Code\HuaMei\App_noi\LandingPageKombai\home_homi.html#gioi-thieu`.
- Implementation screenshots: Chrome Browser captures displayed inline in this task at 1024 × 720 and 390 × 844 CSS px; the browser tool did not provide persistent screenshot file paths. Desktop density was 1 CSS px per image px.
- Full-view comparison: the reference and desktop capture were opened together. The section follows testimonials, with the title, five-line paragraph, two actions, and green portrait composition in the same left/right order. Section height measured 414 px against the 410 px reference. Title starts 121 px from the section top and actions 320 px from the top, close to the reference's approximately 126 px and 326 px.
- Focused comparison: title size/color, paragraph line breaks, buttons, portrait and floating-card cluster were visually checked. The generated portrait differs in facial details from the reference, but preserves the intended composition, scale and color.
- Mobile verification: at 390 px, content stacks text/actions above the artwork; artwork is fully visible and buttons stay on one row. At 320 px, both buttons also stay on one row. `document.documentElement.scrollWidth` remained below the viewport width at both sizes.
- Interaction verification: both CTA anchors resolve to the existing Zalo consultation and learning-method targets; VI ↔ 中文 updates the new text and image description. Chrome console showed no errors or warnings.
- Comparison history: initial desktop art was too small and its white raster edge covered paragraph endings. Scaled and shifted the artwork, then placed copy above it; the latest Chrome capture shows the paragraph fully visible and artwork at the reference scale. Initial 320 px buttons wrapped; reduced their small-screen widths and verified a shared row.
- Remaining P3: the generated portrait is a close visual interpretation rather than the exact person in the reference.

## Hòa Mỹ mission section — 2026-09-19

- Source visual truth: `C:\Users\DELL\AppData\Local\Temp\codex-clipboard-737d982f-5b8f-408d-a050-e0d3bb286fd9.png` (998 × 455 px).
- Implementation: `D:\Code\HuaMei\App_noi\LandingPageKombai\home_homi.html#su-menh`.
- Implementation screenshots: Chrome Browser captures displayed inline in this task at 998 × 700, 390 × 844 and 320 × 700 CSS px; this browser tool did not provide persistent screenshot file paths. Desktop density was 1 CSS px per image px.
- Full-view comparison: source and browser render were opened together in one comparison. The mission section immediately follows the Hòa Mỹ introduction. At 998 px, the rendered section height measured 454.6 px against the 455 px source. The centered headline, existing turquoise Hòa Mỹ logo, blue lead and two paragraphs follow the source composition.
- Focused comparison: typography, spacing, colors, logo quality and exact Vietnamese copy were checked. Title begins 33 px below the section top; logo box starts 89.6 px below; lead starts 106.6 px below. These placements match the source's approximate 40 px headline, 110 px visible logo and 113 px lead positions. The original `assets/images/logo.png` is used, so the emblem shape and color are retained.
- Mobile verification: at 390 px and 320 px, title, logo and text stack vertically; paragraphs switch from justified to left aligned for readability. Logo and copy remain within the viewport, and `document.documentElement.scrollWidth` is below viewport width at both sizes.
- Language verification: VI → 中文 → VI updates the title, lead, paragraphs and logo description. Chrome console showed no errors or warnings.
- Findings: no actionable P0, P1 or P2. Minor P3: the desktop title and logo differ by roughly 10–20 px in width from the reference, with no readability or layout impact.

final result: passed
