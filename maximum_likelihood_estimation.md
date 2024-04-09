# Table Of Content
[[_TOC_]]

# 1. Maximum Likelihood Estimation

Trong thống kê và học máy thì dữ liệu thường được diễn tả thông qua những phân phối xác suất. Phân phối xác suất thường là một hàm số được đặc trưng bởi những tham số nhất định. Đối với phân phối chuẩn, tham số đặc trưng chính là cặp trung bình và phương sai $\{\mu, \sigma^2\}$. Đối với phân phối Poisson thì tham số đặc trưng là $\lambda$. Nếu đã biết về dạng hàm phân phối, làm thế nào để tìm ra các tham số phân phối hợp lý nhất cho một bộ dữ liệu? Đó chính là mục tiêu mà **_ước lượng hợp lý tối đa (Maximum Likelihood Estimation)_**, viết tắt là MLE, sẽ giải quyết.

Trong thống kê, MLE là 1 phương pháp giúp ước lượng tham số phân phối của dữ liệu thông qua tối đa hóa hàm hợp lý sao cho dưới giả định của mô hình thống kê thì dữ liệu trở nên phù hợp nhất. Tính phù hợp được đo lường thông qua một hàm số được gọi là **_hàm hợp lý (Likelihood Function)_**.

Giả định một bộ dữ liệu gồm $N$ quan sát đầu vào là $D = \{x_1, x_2, ..., x_N\}$ được mô phỏng bởi một phân phối lý thuyết $f(.)$ sao cho phân phối lý thuyết được đặc trưng bởi 1 vector tham số $w = (w_0, w_1, ..., w_k)^T$. Tập hợp tất cả những giá trị có thể của $w được gọi là *không gian tham số  (parameter space) W*. Mục tiêu của MLE là tìm kiếm vector tham số $w$ trong không gian tham số $W$ sao cho giá trị **_hàm hợp lý_** là lớn nhất. Lớn nhất có nghĩa là phù hợp nhất. Thông thường **_Hàm hợp lý_** được ký hiệu là $L(w)$ là một hàm đối với $w$, hàm số này đo lường xác suất đồng thời của tất cả các quan sát thuộc tập dữ liệu đầu vào $D$.

$$L(w) = P(D|w)$$

Trong phương pháp _ước lượng hợp lý tối đa_ thì $D$ được xem như kết quả đã biết trước. Tìm kiếm được một véc-tơ tham số $\hat{w}$ phù hợp nhất cũng giống như đi tìm nguyên nhân để giải thích tốt nhất cho kết quả đã biết. Trong trường hợp các quan sát ngẫu nhiên có phân phối độc lập và xác định (independent and identically distributed) viết tắt là <span style="color:red">iid</span>, thì hàm hợp lý sẽ bằng tích xác suất trên từng quan sát:

$$L(w) = P(D|w) = P(x_1, ..., x_n|w) = \prod_{i=1}^{n}P(x_i|w)$$

vector tham số $w$ phù hợp nhất là nghiệm của bài toán tối ưu hàm hợp lý

$$\hat{w} = \text{argmax}_{x} L(w)$$

Giải bài toán tối ưu của tích là không dễ dàng. Do đó, chúng ta thường sử dụng logarith để chuyển từ tối ưu hàm hợp lý sang tối ưu log của hàm hợp lý (log likelihood). Để phân biệt với hàm hợp lý thì hàm log của hàm hợp lý được ký hiệu là _l_.

$$\hat{w} = \text{argmax}_{w}l(w) = \text{argmax}_{w} log L(w)$$

Nếu dữ liệu phân phối <span style="color:red">iid</span> thì bài toán tối ưu sẽ đẹp hơn:

$$\hat{w} = \text{argmax}_{x} log \prod_{i=1}^{N}P(x_i|w)$$
$$= \text{argmax} \sum_{i=1}^{N} log P(x_i|w)$$

Từ phương pháp ước lượng hợp lý tối đa, chúng ta có thể chứng minh được ước lượng tham số của rất nhiều các phân phối khác nhau.

## Bài tập

Để ước lượng cân nặng trung bình của một người trưởng thành là một điều rất khó. Chúng ta không thể tìm ra con số chính xác về cân nặng trung bình của tất cả mọi người trưởng thành trên thế giới vì cân nặng luôn biến động và thực hiện quá trình này là tốn kém. Vì vậy chúng ta chỉ có thể tìm ra một ước lượng hợp lý nhất từ một mẫu nhỏ và lấy kết quả này đại diện cho tổng thể. Giả sử tiến hành đo mẫu gồm _N_ người trưởng thành có cân nặng là $D={x_1, x_2, ..., x_N}$. Hãy ước lượng trung bình cân nặng của một người trưởng thành.

## Lời giải

Chúng ta giả định rằng cân nặng tuân theo phân phối chuẩn với trung bình là $\mu$ và phương sai $\sigma^2$. Như vậy theo phân phối chuẩn thì giá trị có xác suất xuất hiện cao nhất sẽ ở vị trí trung bình của phân phối. Tuy nhiên ta không chắc chắn rằng trung bình của _N_ mẫu là ước lượng hợp lý nhất cho cân nặng. Chính vì thế chúng ta sử dụng phương pháp MLE để tìm ra ước lượng hợp lý tối đa. Bạn sẽ thấy ước lượng hợp lý nhất cho cân nặng chính là trung bình.

Thật vậy, vì cân nặng được giả định là tuân theo phân phối chuẩn nên xác suất tại một quan sát $x_i$ sẽ được tính theo hàm mật độ xác suất:
$$P(x_i|\mu, \sigma) = \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x_i-\mu)^2}{2\sigma^2}}$$

Cân nặng của mọi người được giả định là <span style="color:red">iid</span> nên xác suất xảy ra của bộ dữ liệu được tính thông qua tích xác suất trên từng điểm dữ liệu. Khi đó các tham số $\mu, \sigma$ được ước lượng thông qua phương pháp MLE.

$$\hat{\mu}, \hat{\sigma}  = \arg \max_{\mu, \sigma} \sum_{i=1}^{N} \log P(x_i|\mu, \sigma) $$

$$ = \arg \max_{\mu, \sigma} \sum_{i=1}^{N} \log \left[ \frac{1}{\sqrt{2\pi\sigma^2}} e^{-\frac{(x_i-\mu)^2}{2\sigma^2}} \right] $$

$$ = \arg \max_{\mu, \sigma} [\underbrace{-\frac{N}{2}\log 2\pi}_{C} - N \log \sigma - \sum_{i=1}^{N}\frac{(x_i-\mu)^2}{2\sigma^2}] $$

$$ = \arg \max_{\mu, \sigma} [-N \log \sigma - \sum_{i=1}^{N}\frac{(x_i-\mu)^2}{2\sigma^2}] + C $$

Đặt:

$$J(\mu, \sigma) \triangleq \arg \max_{\mu, \sigma} [-N \log \sigma - \sum_{i=1}^{N}\frac{(x_i-\mu)^2}{2\sigma^2}] $$

Điều kiện cần của cực trị theo đạo hàm bậc nhất:

$$\frac{\delta J(\mu, \sigma)}{\delta \mu} =  -\sum_{i=1}^{N} \frac{(x_i-\mu)}{\sigma^2} = 0 \tag{1} $$

$$\frac{\delta J(\mu, \sigma)}{\delta \sigma}  =  -\frac{N}{\sigma}+\sum_{i=1}^{N} \frac{(x_i-\mu)^2}{\sigma^3} = 0 \tag{2} $$

Từ đẳng thức (1) ta suy ra:

$$\hat{\mu} = \frac{1}{N}\sum_{i=1}^{N} x_i$$

Đẳng thức (2) cho thấy:

$$\hat{\sigma}^2 = \frac{1}{N} \sum_{i=1}^{N} (x_i-\mu)^2$$

Đây chính là những ước lượng hợp lý nhất về trung bình và phương sai của mẫu. Từ những ước lượng này chúng ta có thể suy ra những ước lượng về khoảng tin cậy cho biến.