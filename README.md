
1. Giới thiệu về task: trong task này ta sẽ thực hiện phân tích phản hồi của khách hàng, hiểu được cảm nhận của khách hàng về sản phẩm hoặc dịch vụ. Cụ thể ta sẽ phân loại 1 đánh giá của khách hàng về quán ăn là tích cực hay tiêu cực từ đó xác định điểm mạnh và điểm yếu của sản phẩm và đưa ra hướng giải quyết. 

2. Hướng tiếp cận: ta sẽ sử dụng các model deep learning với mục tiêu đạt được kết quả cao nhất. Trong task này ta sẽ sử dụng kiến trúc transfomer và pretrained model BERT sau đó so sánh kết quả giữa 2 model này. Với kiến trúc transfomer ta sẽ code model từ các block, layer... và train lại từ đầu, còn với BERT ta sẽ train lại dựa trên các kiến thức của BERT đã được học từ trước sau đó so sánh kết quả giữa 2 model. 

3. Về data, ta sẽ sử dụng bộ dữ liệu tiếng việt gồm có các câu đánh giá của khách hàng mỗi câu ứng với nhãn 0: đánh giá tiêu cực, 1: đánh giá tich cực. Download dataset tại <a href="https://github.com/congnghia0609/ntc-scv.git">đây</a>. Dữ liệu trước khi đưa vào model cần được xử lí gồm các bước chính sau:

   a. Data có dạng là các file text, ta cần lấy data ra và đưa chúng vào 1 DataFrame. DataFrame này sẽ có hai cột. Cột đầu tiên là gồm các câu, cột thứ 2 là label của câu đó 

   b. Tiền xử lí dữ liệu như: xóa thẻ HTML, URL ...

   c. Tạo tokenizer và bộ vocab cho model
   
         Đối với transfomer ta sẽ tự tạo tokenizer và vocab cho model
      
         Với model BERT ta sẽ sử dụng tokenizer có sẵn của BERT

   d Tạo dataset và dataloader
   
         Đối với transfomer: ta tự tạo dataset và dataloader dựa vào Pytorch
      
         Đối với BERT ta sẽ tạo tokenizer cho từng batch và data_collator cho quá trình traning

4. Khởi tạo model và training, testing

         Đối với transfomer ta sẽ code lại model từ đầu và traning
      
         Đối với BERT: ta cần khởi tạo thêm metrics cho qua trình traning sau đó load pretrained và training 

5. Evaluate:
   
   a. Đối với model transfomer train từ đầu sau 100 epochs:
   
   ![1](https://github.com/PhamTrinhDuc/Text-Classification-using-Transformer-and-Pretrained-BERT/assets/127647215/6c442e11-d125-4548-be35-4cd8e98952dd)

   b. Đối với pretrained BERT sau 10 epochs:

         {'eval_loss': 0.3751769959926605,
          'eval_accuracy': 0.8438,
          'eval_runtime': 55.469,
          'eval_samples_per_second': 180.281,
          'eval_steps_per_second': 1.424,
          'epoch': 10.0}


6. Nhận thấy cả 2 model có kết quả tương đối nhau mặc dù BERT đã được pretrained. Lí do có thể là: 

   1. Kích thước bộ dữ liệu:
   
      Bộ dữ liệu đánh giá quán ăn thường nhỏ hơn nhiều so với các bộ dữ liệu mà BERT được huấn luyện ban đầu (BooksCorpus và Wikipedia tiếng Anh)
      
      Việc huấn luyện BERT với một lượng dữ liệu nhỏ có thể không đủ để BERT học được các đặc điểm cụ thể của bộ dữ liệu đánh giá quán ăn
   
   2. Chất lượng dữ liệu:
   
      Chất lượng dữ liệu trong bộ dữ liệu đánh giá quán ăn có thể không cao như các bộ dữ liệu mà BERT được huấn luyện ban đầu
      
      Dữ liệu nhiễu hoặc không chính xác
   
   3. Thuật toán huấn luyện:
   
      Thuật toán huấn luyện BERT có thể không được tối ưu hóa cho các bài toán về đánh giá quán ăn
      
   4. Việc fine-tune:
   
      BERT có thể không được fine-tune tốt cho bộ dữ liệu đánh giá quán ăn




   

