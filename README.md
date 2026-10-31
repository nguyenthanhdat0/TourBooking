```mermaid
flowchart TB
    %% Định nghĩa các tác nhân
    subgraph Clients["Tương tác người dùng (Clients)"]
        Customer((Customer))
        Provider((Provider))
        Admin((Admin))
    end

    %% Giao diện Frontend
    subgraph Frontend["Frontend (ReactJS)"]
        UI[Web Interface]
        State[State Management]
        UI <--> State
    end

    %% Lõi Backend
    subgraph Backend["Backend (Java Spring MVC)"]
        Security[Spring Security & JWT Filter]
        Controllers[REST Controllers]
        Services[Service Layer\n(Business Logic)]
        Hibernate[Hibernate / JPA Repositories]
        
        Security -->|Xác thực Role| Controllers
        Controllers --> Services
        Services --> Hibernate
    end

    %% Cơ sở dữ liệu và Dịch vụ bên thứ 3
    subgraph Infrastructure["Lưu trữ & Dịch vụ ngoài (Infrastructure)"]
        MySQL[(MySQL Database\n10+ Tables)]
        Cloudinary([Cloudinary\nImage Hosting])
        Payment([VNPay/MoMo\nPayment Gateway])
    end

    %% Luồng giao tiếp (Data flow)
    Customer -->|Tìm kiếm & Đặt chỗ| UI
    Provider -->|Quản lý dịch vụ| UI
    Admin -->|Kiểm duyệt| UI

    UI <-->|HTTP/REST APIs| Security
    Services <-->|Upload/Lấy link ảnh| Cloudinary
    Services <-->|Xử lý giao dịch| Payment
    Hibernate <-->|Truy vấn (SQL)| MySQL
```
