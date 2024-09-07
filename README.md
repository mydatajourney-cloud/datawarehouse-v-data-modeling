# datawarehouse-theory and data modeling 
## Overview
Đây là kiến thức mình nhặt được trong quá trình học khoá học udemy về data warehouse. 
## Table of Contents

1. [Quy tắc khi xây dựng datawarehouse](#installation)
2. [Usage](#usage)
3. [Features](#features)
4. [Contributing](#contributing)
5. [License](#license)
6. [Getting Started](#getting-started)
7. [Configuration](#configuration)
8. [Examples](#examples)
9. [Troubleshooting](#troubleshooting)
10. [Contact](#contact)

# How to build DW ?

- Interagrated: DW là một môi trường tích hợp, nói cách khác nó lưu trữ dữ liệu từ nhiều ngồn khác nhau
- Subject oriented: Các dữ liệu lưu trữ trong dw phải được sắp xếp theo các chủ đề, dù cho nó từ nhiều nguồn và các hệ thống khác nhau
- Time variant: Các dữ liệu trong DW phải được lưu dữ ở các khoảng thời gian khác nhau chứ không chỉ là hiện tại .
- Non-volatile: DW không được chịu ảnh hưởng bởi các khoảng cập nhật dữ liệu, sau mỗi lần “refresh”  dw sẽ được cập nhật dữ liệu theo các khối.
- ⇒ Hỗ trợ cho việc phân tích và ra quyết định dựa trên dữ liệu.

Tại sao phải xây dựng DW → Hỗ trợ việc phân tích và ra quyết định dựa trên dữ liệu → tại sao ?

- Quan sát dữ liệu ở quá khứ
- Quan sát dữ liệu ở hiện tại
- Quan sát dữ liệu ở tương lai ( dữ liệu mà ta tin là đúng ví dụ AI)
- Quan sát dữ liệu unknown

DW có thể build trên các: 

- Relational database
- Cubes (multi dimensional database

# Datawarehouse vs datamart

- Datawarehouse và datamart independent khá là giống nhau
- Datamart depend có thể áp dụng trong những trường hợp khi dữ liệu từ datawarehouse đa dạng và khá nhiều chủ đề cần được chia nhỏ ra thành các datamart. Ví dụ phòng marketing chỉ có thể lấy dữ liệu từ datamart phù hợp so với phòng sale.

# DATA warehouse tree
- Centrallized: advantaged  → EDW → Relational database

                                                                       → Specialized database.

                                                       → DATA LAKES → hadoop.

                                                                                    → Specialized database.

                                                                                    → others (aws s3, …) .  

EDW:  Enterprise Data warehouse (old)

DATA LAKES: dành cho các công ty cần quản lý dữ liệu lớn. 

⇒ One stop shopping: dữ liệu từ các nguồn đều tập trung vào 1 dw

⇒ Chịu ảnh hưởng bởi việc thay đổi dữ liệu trong dw (bad)

- Component-based: advantaged → architech → DW + DMS → Depend data marts

                                                                                                                      → Front-end data marts

                                                                                            → DMs only    → DW bus

                                                                    → Non- Architech → Federated EDW

Depend dms: dữ liệu từ data warehouse chạy dọc xuống các data marts 

Front-end dms:  dùng khi một phần dữ liệu đi ngược từ các data marts được đưa xuống data warehouse cho những phân tích khác. 

DW bus: cũ và nên là phương án cuối vì nhiều DMs quá sẽ không tốt.

Federated EDW: cũ và nên là phương án cuối vì nhiều DMs quá sẽ không tốt.

⇒ Decomposion: dữ liệu được chia nhỏ thành các thành phần, tránh ảnh hưởng bởi việc thay đổi dw.

# Data warehouse architechture

*Có 2 lớp ở trong data warehouse: Staging Layer và User Access Layer 

*Staging layer: lưu trữ các dữ liệu lấy từ nguồn với điều kiện là các dữ liệu phải giống với nguồn và ít bị can thiệp.

- Nếu có nhiều nguồn từ nhiều application khác nhau = có nhiều bảng staging tương ứng
- Nếu có nhiều nguồn nhưng cùng một application = có gộp các bảng staging tương ứng

*Có 2 loại Staging Layer: duy trì và không duy trì

- Staging Layer duy trì là dữ liệu ở staging sẽ không bị xoá khi mà dữ liệu đã đi vào User Acess Layer.
    
    ⇒ tốn rất nhiều storage để giữ lại dữ liệu
    
    ⇒ có thể không kiểm soát được quyền truy cập người nào truy cập được dữ liệu ở staging layer. 
    
- Staging Layer không duy trì là dữ liệu ở staging sẽ không được giữ lại khi mà dữ liệu đã đi vào User Acess Layer.
    
    ⇒Tốn ít storage hơn nhưng nếu dữ liệu ở User Acess Layers có vấn đề (bị hư) hoặc cần phải xây dựng lại dataware house thì k có dữ liệu có sẵn. 
    
    ⇒Ngoài ra lưu dữ liệu ở staging layer còn giúp cho việc kiếm tra chất lượng dữ liệu.  
    

*User Access Layer:
