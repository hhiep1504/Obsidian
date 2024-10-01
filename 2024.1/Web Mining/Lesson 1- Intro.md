## Semester 
```dataviewjs 
var a = moment("2024-09-05");
var b = moment("2025-01-01");
var n = moment() 
var t = moment().startOf('day'); 
let q = b.diff(a, 'days'); 
let p = b.diff(t, 'days'); 
let r = t.diff(a, 'days'); 
let h = n.diff(a, 'hours'); 
let i = b.diff(a, 'hours'); 
let html = `<progress style="height:10px;width:80%" value="`+h+`" max="`+i+`"></progress>` 
if (r>0 && r<q) { 
	html += `\n#### `+p+` days left of `+q+` days\n` 
	html += (h/i*100).toFixed(2)+`% complete` 
	
} else if (r==0) { 
	html += `\nstars today` 
	
} else if (r==q) { 
	html += `\nends today` 
} else if (r>q) {
	html += `\nended `+-p+` days ago` 
} else { 
	html += `\n#### `+-r+` days to go` 
	} 

dv.paragraph(html) 
```

## 1. WWW là gì?

- **1.1 Tác động của WWW:** Khám phá cách thức web, với thông tin rộng lớn và dễ truy cập, đã cách mạng hóa việc truy xuất thông tin và trở thành một kênh quan trọng cho giao tiếp và giao dịch.
- **1.2 Định nghĩa WWW:** Cung cấp định nghĩa chính thức về World Wide Web, nhấn mạnh kiến trúc máy chủ-client, vai trò của trình duyệt và ý nghĩa của siêu văn bản trong việc liên kết thông tin.
- **1.3 Lịch sử của Web:** Theo dõi sự phát triển của Web từ khi được phát minh bởi Tim Berners-Lee đến sự nổi lên của các công cụ tìm kiếm và sự ra đời của World Wide Web Consortium (W3C). Các cột mốc quan trọng như sự ra đời của Mosaic và bong bóng dot-com được làm nổi bật.

## 2. Data Mining là gì?

- **2.1 Định nghĩa Data Mining:** Định nghĩa data mining (DM) là quá trình khám phá các mẫu có giá trị từ các nguồn dữ liệu đa dạng. Giải thích đặc điểm của các mẫu có giá trị và nhấn mạnh tính liên ngành của data mining.
- **2.2 Lịch sử của Data Mining:** Phác thảo sự tiến triển lịch sử từ các Hệ thống Quản lý Cơ sở Dữ liệu (DBMS) ban đầu đến DBMS nâng cao và sự xuất hiện của kho dữ liệu và phân tích dữ liệu nâng cao.
- **2.3 Các loại dữ liệu:** Cung cấp phân loại các loại dữ liệu khác nhau liên quan đến data mining, bao gồm dữ liệu từ cơ sở dữ liệu, kho dữ liệu, dữ liệu giao dịch và các loại dữ liệu chuyên biệt khác như dữ liệu thời gian, không gian và văn bản. Phần này thảo luận về các thách thức và ứng dụng liên quan đến từng loại dữ liệu.
- **2.4 Các mẫu có thể khám phá được:** Giải thích hai loại nhiệm vụ chính của data mining - mô tả và dự đoán - và khám phá các loại mẫu có thể khám phá được khác nhau: mô tả và phân biệt dữ liệu, mẫu thường xuyên, kết hợp và tương quan, phân loại và hồi quy, nhóm và phát hiện ngoại lệ. Phần này cũng đi sâu vào các đặc điểm của các mẫu tiềm năng và thảo luận về các thước đo khách quan và chủ quan để đánh giá mẫu.
- **2.5 Các kỹ thuật trong Data Mining:** Đánh giá các kỹ thuật chính được sử dụng trong data mining, bao gồm thống kê, học máy, hệ thống quản lý cơ sở dữ liệu, kho dữ liệu và truy xuất thông tin. Điểm mạnh và ứng dụng của từng kỹ thuật trong data mining được nghiên cứu.
- **2.6 Ứng dụng của Data Mining:** Cung cấp các ví dụ về ứng dụng data mining, tập trung vào trí tuệ kinh doanh và tìm kiếm trên web. Nó minh họa cách các kỹ thuật data mining có thể được tận dụng để có được thông tin chi tiết, đưa ra quyết định tốt hơn và nâng cao chức năng của công cụ tìm kiếm.
- **2.7 Thách thức trong Data Mining:** Thảo luận về những thách thức đáng kể trong data mining, bao gồm phát triển các phương pháp khai thác mới, cải thiện tương tác người dùng, đảm bảo hiệu quả và khả năng mở rộng, và giải quyết tác động xã hội của data mining.

## 3. Web Data Mining là gì?

- **3.1 Định nghĩa Web Data Mining:** Định nghĩa web data mining và nhấn mạnh các đặc điểm duy nhất của dữ liệu web khiến nó trở thành một lĩnh vực đầy thách thức nhưng giàu tiềm năng để khám phá kiến thức. Phần này nhấn mạnh khối lượng lớn, đa dạng, dị nhất, tính liên kết, khả năng gây hiểu lầm thông tin, khía cạnh thương mại, tính động và các khía cạnh xã hội của dữ liệu web.
- **3.2 Mục tiêu của Web Data Mining:** Phác thảo các mục tiêu chính của web data mining, chẳng hạn như hiểu sự phân bố thông tin, đặc trưng hóa và phân loại các trang web, theo dõi sự phát triển của web và phân tích mối quan hệ giữa các tác nhân web như trang, người dùng và cộng đồng.

# Quiz
1. **How does the World Wide Web (WWW) impact our daily lives?**
	 **Answer:** The WWW revolutionizes information retrieval, enabling easy access to vast amounts of information through search engines. It also serves as a crucial transaction channel, facilitating online shopping and global communication.
2. **Explain the client-server architecture of the WWW.**
	 **Answer:** The WWW operates on a client-server model where users utilize client software (browsers) to request and display data stored on remote servers. The browser sends requests to the server, receives responses, compiles HTML, and displays content.
3. **What is hypertext and who invented it?**
	**Answer:** Invented by Ted Nelson in 1965, hypertext allows linking documents to other online resources via hyperlinks. This interconnectivity enables users to navigate seamlessly between related content with simple clicks.
4. **Describe the key contributions of Tim Berners-Lee to the development of the WWW.**
	Tim Berners-Lee invented the WWW in 1989. He proposed a protocol for managing distributed documents, leading to the development of essential web components: server, browser, HTTP, HTML, and URL.
5. **What is Data Mining (DM) and what are its key characteristics?**
	Data mining (DM) is the process of extracting useful patterns or knowledge from data sources. These patterns should be correct, understandable, and applicable to real-world scenarios. DM involves various disciplines like machine learning, statistics, and database management.
6. **Explain the difference between data description and data discrimination in the context of DM.**
	Data description aims to summarize common characteristics of a data class, while data discrimination compares general features of one class against others (reflective classes). Data description provides a general overview, while data discrimination highlights differences.
7. **Define association analysis and provide an example of an association rule.**
	Association analysis discovers relationships between items in a dataset. For example, a rule like "If a customer buys bread, they are also likely to buy milk (support=60%, confidence=70%)" indicates a strong association between bread and milk purchases.
8. **What is the main difference between supervised and unsupervised learning in Machine Learning?**
	Supervised learning utilizes labeled data to train models to predict outcomes for new data, like classifying emails as spam or not spam. In contrast, unsupervised learning uses unlabeled data to discover hidden patterns or groupings, like clustering customers based on purchase history.
9. **How does Information Retrieval (IR) differ from traditional Data Mining?**
	IR focuses on retrieving relevant documents based on keyword-based queries, assuming unstructured data. DM aims to extract meaningful patterns and knowledge from potentially structured data, often going beyond simple keyword matching.
10. **List and briefly describe three challenges in the field of Data Mining.**
	- **Data Complexity:** Handling noise, missing values, and uncertainty in data requires sophisticated preprocessing and analysis techniques.
	- **Scalability:** DM algorithms need to be efficient enough to process massive datasets within acceptable timeframes.
	- **Interpretability:** Extracted patterns should be understandable and actionable for users, enabling them to make informed decisions.

### Glossary of Key Terms

- **WWW (World Wide Web):** A system of interconnected documents and resources accessed over the internet.
- **Client-Server Architecture:** A network model where clients (e.g., browsers) request services from servers (e.g., web servers).
- **Hypertext:** Text displayed on a computer or device with references (hyperlinks) to other text that the reader can immediately access.
- **Data Mining (DM):** The process of discovering meaningful patterns and knowledge from large datasets.
- **Data Description:** Summarizing common characteristics of a data class or group.
- **Data Discrimination:** Comparing and contrasting general features of different data classes.
- **Association Analysis:** A data mining technique used to discover frequent patterns and relationships between items in a dataset.
- **Supervised Learning:** A type of machine learning where models are trained on labeled data to predict outcomes for new data.
- **Unsupervised Learning:** A type of machine learning where models are trained on unlabeled data to discover hidden patterns or groupings.
- **Information Retrieval (IR):** The process of obtaining relevant information from a collection of resources, typically in response to a query.