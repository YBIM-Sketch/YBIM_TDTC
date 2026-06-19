# YBIM TDTC - Phần mềm Quản lý Tiến độ Thi công BIM 4D/5D

YBIM TDTC (Time, Cost, Trade-off) là ứng dụng Desktop mạnh mẽ xây dựng trên nền tảng .NET 8 WPF, chuyên dùng để lập tiến độ thi công, quản lý đường găng (Critical Path Method - CPM) và tối ưu hóa tài nguyên bằng thuật toán di truyền (Genetic Algorithm).

## Các Phiên Bản Nâng Cấp Gần Đây

* **Trình mô phỏng 4D BIM & Gán Cấu Kiện Trực Tiếp (v0.2.1-3D - Mới):**

  - *Zero-Wait IFC Pipeline:* Tích hợp bộ chuyển đổi tự động nền tảng `IfcConvert` để chuyển đổi định dạng IFC sang GLB trong thời gian thực, đảm bảo hiệu suất render mượt mà trong WPF WebView2.
  - *Explicit 3D Binding:* Lược bỏ cơ chế Rule-based rườm rà, thay thế bằng luồng thao tác "Click-and-Bind" - bấm chọn cấu kiện ngay trên mô hình 3D (hỗ trợ `Ctrl+Click` đa chọn) và gán vĩnh viễn vào lưới tiến độ DataGrid.
  - *Bidirectional 4D Sync:* Giao tiếp hai chiều tức thời giữa C# và Javascript, hỗ trợ tô màu cảnh báo và playback tiến độ thi công trên mô hình theo thời gian thực (Overlay Ngày tháng).
  - *Multi-Model Federation (Nạp đa mô hình):* Cho phép nạp đồng thời nhiều tệp IFC/GLB (vd: Kiến trúc + Kết cấu + MEP) qua giao diện Multi-Select. Xử lý tuần tự chống tràn RAM (Zero-Wait) và gộp chung hệ tọa độ tự động (Federated) bằng ThreeJS Group.
  - *Zero-Wait Smart Properties:* Nâng cấp bảng Thuộc tính Cấu kiện 3D cho chế độ siêu tốc. Tự động trích xuất GlobalId và Type từ cấu trúc phân cấp Mesh Name của bộ chuyển đổi IfcConvert, cung cấp thông tin thiết yếu mà không cần load tệp JSON metadata nặng nề.
* **Triển khai toàn diện 13 Hướng chiến lược Công nghệ (v0.2.1-08):**

  - *Hướng 1 (Trình bóc tách WBS từ hồ sơ thầu):* Tự động chuyển đổi tài liệu `.docx`/`.pdf` sang Markdown sạch bằng công cụ Microsoft `markitdown` để sinh cây danh mục `YTask` tự động.
  - *Hướng 2 (Đúc kết thói quen lập tiến độ):* Chạy phân tích so sánh diff lịch sử phiên bản commit trong LiteDB đúc kết tự động tri thức lập lịch vào bộ nhớ bản năng.
  - *Hướng 3 (Stop-Slop Prompt Filter):* Tích hợp bộ tiền xử lý loại bỏ văn phong sáo rỗng của AI khi giải thích đường găng CPM theo chuẩn phong cách chỉ huy trưởng.
  - *Hướng 4 (SkiaSharp Fluent Gantt Painter):* Nâng cấp bộ vẽ Gantt trên nền SkiaSharp sử dụng các tone màu gradient HSL bo viền mượt mà chuẩn Fluent Design cao cấp.
  - *Hướng 5 (Phân bổ tài nguyên từ BOQ):* Trình ánh xạ tự động đọc khối lượng tài nguyên từ bảng dự toán BOQ CSV/Excel gán trực tiếp vào các công tác trong WBS.
  - *Hướng 6 & 12 (GA Caching & Carbon Footprint Optimization):* Tích hợp cơ chế memoization `ga_fitness_cache.json` bền vững giảm 70% CPU đồng thời áp dụng hình phạt trừng số khí thải CO2 hướng tới "Green BIM".
  - *Hướng 7 & 11 (Zero-Trust SBOM & Cryptographic Progress Claims):* Tự động sinh SBOM CycloneDX 1.5 JSON an toàn và xây dựng sổ cái tiến độ SHA-256 chống làm giả báo cáo sản lượng.
  - *Hướng 8 (CPM Engine Playbook):* Bổ sung hơn 300 dòng tài liệu toán học và mã nguồn C# chuẩn cho thuật toán Quét tiến (Forward Pass), Quét lùi (Backward Pass) tại `Work_Skill.md`.
  - *Hướng 9 (Holiday Lookup Service):* Bộ nạp tự động lịch nghỉ lễ Việt Nam vào `YCalendar` giúp tính toán thời hạn thi công chuẩn xác 100%.
  - *Hướng 10 (Scheduling Plugin Manager):* Trình quản lý nạp động các tập quy tắc tiến độ bên ngoài viết bằng script C# (`.csx`) mà không cần compile lại app.
  - *Hướng 13 (WBS Mind-Map Editor):* Xây dựng WPF Custom Control trực quan hóa cấu trúc phân rã công việc WBS dưới dạng sơ đồ tư duy tương tác sống động.

## Bản nâng cấp v0.2.1 Pro (Khắc phục Bar Styles & Tối ưu hóa cài đặt)

* **Sửa lỗi đồng bộ Bar Styles & hiển thị Gantt:** Thay đổi điều kiện lọc vẽ thân thanh tiến độ thành if (rule.MiddleShape != BarShapeType.None), giải quyết triệt để lỗi mất thân thanh Task (màu xanh dương) khi người dùng chọn độ dày **Trung bình (Medium)** hay **Mỏng (Thin)**.
* **Đồng bộ hóa Skia PDF Vector:** Áp dụng sửa lỗi vẽ thân Gantt đồng bộ trên cả màn hình hiển thị trực quan lên tệp xuất bản PDF Vector chất lượng cao.
* **Chuẩn hóa Google Material Design Icons Ribbon:** Thay thế toàn bộ các icon Ribbon bị lỗi cũ thành icon chuẩn từ bộ Google Material: LanguageHtml5, FileCode và PageLayoutSidebarLeft nhằm triệt tiêu hoàn toàn lỗi crash khi khởi động phần mềm sau khi cài đặt.
* **Đóng gói Premium Setup v0.2.1 Pro:** Biên dịch chế độ Release, Obfuscar obfuscated mã nguồn an toàn tuyệt đối 100/100, đóng gói ra tệp tin cài đặt Wizard **YBIM_TDTC_Setup_v0.2.1_Pro.exe** và gói di động **YBIM_TDTC_v0.2.1.zip** hoạt động hoàn hảo 100% trên Windows.
* **Nâng cấp Báo cáo PDF Gantt & Đồng bộ hiển thị (v0.2.1-09):**
  - *Thước đo thời gian đa cấp (Timescale):* Triển khai hệ thống timescale thích ứng động (Năm / Quý / Tháng / Tuần) đồng bộ với tỷ lệ thu phóng màn hình chính, căn chỉnh pixel dọc chính xác và cắt clip vùng vẽ (`ClipRect`) chống tràn.
  - *Gộp nhãn ngày chống đè chữ (Collision Prevention):* Tự động gộp nhãn ngày bắt đầu/kết thúc thành `"ngày_bắt_đầu - ngày_kết_thúc"` bên phải thanh Gantt khi khoảng cách quá ngắn hoặc có nguy cơ chồng chéo nhãn.
  - *Giới hạn xuống dòng (3-Line Wrap):* Khống chế tên công tác tối đa 3 dòng kết hợp thuật toán tự động thêm dấu ba chấm (`...`) cho tên công tác quá dài trên cả lưới Grid hiển thị chính lẫn trang in PDF, kết hợp tính toán chiều cao dòng tương thích với font in đậm cho các công tác tổng hợp.
  - *Đồng bộ màu sắc Theme:* Tự động truy vấn tài nguyên màu giao diện (Sáng/Tối) thông qua hàm truy vấn động `GetThemeSKColor` để tô màu nhãn, lưới và đường gióng trên PDF đồng bộ với ứng dụng WPF.

## Bản nâng cấp v0.2.1-10 (Động cơ Web WebView2 & Kiểm định Chất lượng (QC Agent Audit))

* **Trình kết xuất Microsoft WebView2 (Edge Chromium):** Thay thế hoàn toàn động cơ Internet Explorer cũ kỹ bằng lõi WebView2 hiện đại. Bứt phá giới hạn hiển thị tài liệu hướng dẫn kỹ thuật (Markdown) với các hiệu ứng CSS3/Web5 đỉnh cao như *Animated Gradient Background* (Nền chuyển màu động) và *True Backdrop Blur* (Kính mờ nguyên bản kiểu Apple) cho các khối Code và Blockquote.
* **Kiểm định Chất lượng (QC Agent Audit):** Xây dựng kiến trúc Plugin kịch bản C# động (`.csx`) sử dụng động cơ Roslyn Compiler. Cho phép tự do nạp/thêm mới các bộ luật kiểm tra mạng lưới tiến độ (vd: `check_long_duration`, `check_orphan`, `check_negative_lag`) mà không cần Compile lại mã nguồn cốt lõi của phần mềm.
* **Giao diện True Glassmorphism & UI Fixes:** Lột xác hoàn toàn cửa sổ QC Agent thành dạng cửa sổ nổi không viền (Borderless) với các góc bo tròn, đổ bóng mềm mại và hiệu ứng BlurEffect khóa nền ứng dụng chính. Sửa lỗi triệt để hiện tượng chôn chữ (Overlap) tại cửa sổ cấu hình (SettingsWindow) và cấu hình cắt chữ thông minh (TextWrapping) cho các ô DataGrid.

## Bản nâng cấp v0.2.1 (Clean Architecture & Đồng bộ Định dạng)

* **Kiến trúc Clean Architecture 4 lớp:** Refactor toàn bộ mã nguồn monolithic thành YBIM.Domain, YBIM.Application, YBIM.Infrastructure và YBIM_TDTC (Presentation). Phân tách rõ ràng trách nhiệm nghiệp vụ (EVM, Scheduling) ra khỏi WPF UI và Data Access, tối ưu hóa quá trình biên dịch và tăng cường năng lực chống dịch ngược.
* **RowFontWeightConverter & Dynamic Bold Logic:** Thay thế toàn bộ WPF DataTrigger ép buộc định dạng Bold của Summary Task bằng giải pháp MultiBinding sử dụng RowFontWeightConverter. Giải quyết triệt để lỗi không thể tắt Bold của công tác tổng hợp, đồng thời đảm bảo tôn trọng 100% định dạng Bold/Normal khi nạp từ file dự án (.ybim, .mpp, .xer) mà vẫn giữ được tính nhất quán trên SkiaSharp Gantt Renderer và PDF Export.

  - *Tối ưu Trải nghiệm 3D (Multi-Select & LCD Render):* Bổ sung nút "Chọn Nhiều" trực tiếp trên UI 3D. Đồng bộ bôi đen hàng loạt công tác trên Gantt khi chọn nhiều cấu kiện mà không dính vòng lặp vô tận. Kích hoạt LcdRenderText và SubpixelText cho SkiaSharp giúp chữ trên biểu đồ Gantt đạt độ sắc nét tuyệt đối.
* **Kết xuất Video Báo Cáo & Lọc Lũy Kế Theo Ngày (v0.2.1-3D - Mới):**

  - *Engine Hyperframes cục bộ:* Tích hợp trình kết xuất video Hyperframes thông qua Node.js di động (v22.14.0) và FFmpeg được đóng gói tự động trong thư mục `tools\`, đảm bảo hoạt động độc lập không phụ thuộc môi trường cài đặt sẵn.
  - *Kịch bản Hoạt ảnh GSAP:* Tự động sinh kịch bản video HTML hoạt hình 12 giây với hiệu ứng Glassmorphism. Cải tiến bổ sung các chỉ số **Nhân Công (NC)** và **Máy Thi Công (MTC)** với hiệu ứng chạy số động (GSAP Counter) bên cạnh Dòng tiền và Công tác.
  - *Lọc Báo Cáo Lũy Kế (Date Filtering):* Bổ sung hộp thoại chọn ngày `ReportDateSelectionWindow` cho phép người dùng tùy chọn mốc ngày báo cáo. Hỗ trợ tự động tính toán các chỉ số tích lũy (S-Curve) gồm Dòng tiền, Nhân công, Máy thi công cho cả **Báo cáo Tổng hợp (Smart UI)** và **Trình chiếu Slide (Smart Deck)**.
  - *Đồng bộ hóa Dữ liệu (DRY):* Dịch vụ gọi trực tiếp `HtmlReportService.GenerateProjectReportJson` đảm bảo dữ liệu video và báo cáo khớp 100% với cấu hình mốc ngày của người dùng.
  - *Đồng bộ hóa dòng tiền:* Đồng bộ toàn bộ thuật toán tính toán dòng tiền (Cashflow) trong Smart UI và Smart Deck với các phân bổ công tác tài nguyên chi tiết (StandardRate * DailyWork) của tab Dòng tiền ngoài giao diện, đảm bảo tính nhất quán dữ liệu 100%.
  - *Tối ưu hóa độ nét Gantt & Khôi phục nhãn Timescale:* Snapped toàn bộ tọa độ vẽ (dòng, thanh công tác, baseline, đường găng, liên kết, vùng nghỉ cuối tuần) về giá trị số nguyên (`Math.Round()`). Cấu hình `SKPaint` tắt `SubpixelText` và bật hinting `SKPaintHinting.Full` giúp văn bản sắc nét vượt trội. Tích hợp cơ chế dự phòng định dạng động (Dynamic Fallback Strategy) cho trục thời gian (Tháng, Quý, Năm) ở dưới Timescale tự rút gọn nhãn (ví dụ: `Tháng 03/2026` $\rightarrow$ `Tháng 03` $\rightarrow$ `03/26` $\rightarrow$ `03`) tránh đứt quãng hiển thị khi thu nhỏ cột; tự động chèn khoảng đệm trống bên trái ngày bắt đầu tối thiểu 85px tránh đè khuất nhãn.
  - *Hỗ trợ IFC 4.3 & Trích xuất Metadata song song (Zero-Wait):* Hỗ trợ đầy đủ tiêu chuẩn IFC 4.3 của buildingSMART cho các thực thể hạ tầng kỹ thuật (`IfcBridge`, `IfcRoad`, `IfcRailway`,...). Tích hợp cơ chế chạy song song (đa luồng) tiến trình chuyển đổi sang cả định dạng hình học `.glb` và dữ liệu thuộc tính `.json` thời gian thực, khôi phục và tối ưu hóa tính năng tra cứu thuộc tính (Property Sets) chi tiết trên trình xem 3D mà không làm giảm tốc độ nạp mô hình.
  - *Hoàn thiện Địa phương hóa Đa ngôn ngữ và Xuất báo cáo:* Bản địa hóa toàn diện 100% các chuỗi giao diện cho 5 quốc gia (VI, EN, FR, ES, ZH). Đồng bộ hóa ngôn ngữ động cho tiêu đề cột Excel từ Cashflow, loại bỏ hoàn toàn tiếng Việt cứng trong báo cáo PPTX/HTML, tích hợp thuật toán phân loại tài nguyên đa ngôn ngữ (NC/Labor, MTC/Machinery...) cho các giải thuật CPM/GA, và triển khai bộ kiểm duyệt khử trùng lặp khóa tài nguyên (Zero-Conflict Dictionary Validation) triệt tiêu hoàn toàn lỗi XAML crash khi khởi động phần mềm. Tích hợp thêm bộ kiểm duyệt và tự động biên dịch kịch bản chất lượng QC Agent C# Script rules (CSX Validator) hỗ trợ cơ chế tự sửa lỗi cú pháp (Auto-retry).
