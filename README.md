
1. Giới thiệu về task: trong task này ta sẽ thực hiện phân tích phản hồi của khách hàng, hiểu được cảm nhận của khách hàng về sản phẩm hoặc dịch vụ. Cụ thể ta sẽ phân loại 1 đánh giá của khách hàng về quán ăn là tích cực hay tiêu cực từ đó xác định điểm mạnh và điểm yếu của sản phẩm và đưa ra hướng giải quyết. 

2. Hướng tiếp cận: ta sẽ sử dụng các model deep learning với mục tiêu đạt được kết quả cao nhất. Trong task này ta sẽ sử dụng kiến trúc transfomer và pretrained model BERT sau đó so sánh kết quả giữa 2 model này. Với kiến trúc transfomer ta sẽ code model từ các block, layer... và train lại từ đầu, còn với BERT ta sẽ train lại dựa trên các kiến thức của BERT đã được học từ trước sau đó so sánh kết quả giữa 2 model. 

3. Về data, ta sẽ sử dụng bộ dữ liệu tiếng việt gồm có các câu đánh giá của khách hàng mỗi câu ứng với nhãn 0: đánh giá tiêu cực, 1: đánh giá tich cực. Download dataset tại <a href="https://github.com/congnghia0609/ntc-scv.git">đây</a>. Dữ liệu trước khi đưa vào model cần được xử lí gồm các bước chính sau:

   a. Data có dạng là các file text, ta cần lấy data ra và đưa chúng vào 1 DataFrame. DataFrame này sẽ có hai cột: cột đầu tiên là gồm các câu, cột thứ 2 là label của câu đó 

   b. Tiền xử lí dữ liệu như: xóa thẻ HTML, URL ...

   c. Tạo tokenizer và bộ vocab cho model. Đối với transfomer ta sẽ tự tạo tokenizer và vocab cho model, còn với pretrained model BERT ta sẽ sử dụng tokenizer có sẵn của BERT

   d. Tạo dataset và dataloader

4. Khởi tạo model và training, testing.

5. Evaluate:
   a. Đối với model transfomer train từ đầu:
   ![1](https://github.com/PhamTrinhDuc/Text-Classification-using-Transformer-and-Pretrained-BERT/assets/127647215/6c442e11-d125-4548-be35-4cd8e98952dd)



   

