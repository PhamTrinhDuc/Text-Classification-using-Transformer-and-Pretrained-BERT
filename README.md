
## Introduction

Trong task này ta sẽ thực hiện phân tích phản hồi của khách hàng, hiểu được cảm nhận của khách hàng về sản phẩm hoặc dịch vụ. Cụ thể ta sẽ phân loại 1 đánh giá của khách hàng về quan ăn là tích cực hay tiêu cực từ đó xác định điểm mạnh và điểm yếu của sản phẩm và đưa ra hướng giải quyết. 

Hướng tiếp cận: ta sẽ sử dụng các model deep learning với mục tiêu đạt được kết quả cao nhất. Trong task này ta sẽ sử dụng kiến trúc transfomer và pretrained model BERT sau đó so sánh kết quả giữa 2 model này. Với kiến trúc transfomer ta sẽ code model từ các block, layer... và train lại từ đầu, còn với BERT ta sẽ train lại dựa trên các kiến thức của BERT đã được học từ trước sau đó so sánh kết quả giữa 2 model. 

Về data, ta sẽ sử dụng bộ dữ liệu tiếng việt gồm có các câu đánh giá của khách hàng mỗi câu ứng với nhãn 0: đánh giá tiêu cực, 1: đánh giá tich cực. 
