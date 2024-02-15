
## Introduction

1. Giới thiệu về task: trong task này ta sẽ thực hiện phân tích phản hồi của khách hàng, hiểu được cảm nhận của khách hàng về sản phẩm hoặc dịch vụ. Cụ thể ta sẽ phân loại 1 đánh giá của khách hàng về quán ăn là tích cực hay tiêu cực từ đó xác định điểm mạnh và điểm yếu của sản phẩm và đưa ra hướng giải quyết. 

2. Hướng tiếp cận: ta sẽ sử dụng các model deep learning với mục tiêu đạt được kết quả cao nhất. Trong task này ta sẽ sử dụng kiến trúc transfomer và pretrained model BERT sau đó so sánh kết quả giữa 2 model này. Với kiến trúc transfomer ta sẽ code model từ các block, layer... và train lại từ đầu, còn với BERT ta sẽ train lại dựa trên các kiến thức của BERT đã được học từ trước sau đó so sánh kết quả giữa 2 model. 

3. Về data, ta sẽ sử dụng bộ dữ liệu tiếng việt gồm có các câu đánh giá của khách hàng mỗi câu ứng với nhãn 0: đánh giá tiêu cực, 1: đánh giá tich cực. Download dataset tại <a href="https://github.com/congnghia0609/ntc-scv.git">đây</a>. Dữ liệu trước khi đưa vào model cần được xử lí:
   3.1 Chuyển các file text trong data thành dạng DataFrame:
   def restructure_data(folder_path):
    examples = []
    for label in os.listdir(folder_path):
        full_path = os.path.join(folder_path, label)
        for file_name in os.listdir(full_path):
            file_path = os.path.join(full_path, file_name)
            with open(file_path, "r", encoding="utf-8") as f:
                lines = f.readlines()
            sentence = " ".join(lines)
            if label == "neg":
                label = 0
            if label == "pos":
                label = 1
            data = {
                'sentence': sentence,
                'label': label
            }
            examples.append(data)
    return pd.DataFrame(examples)
   3.2 Xóa các thẻ HTML, URL, các dấu câu ...
   def preprocess_text(text):
    # remove URLs https://www.
    url_pattern = re.compile(r'https?://\s+\wwww\.\s+')
    text = url_pattern.sub(r" ", text)

    # remove HTML Tags: <>
    html_pattern = re.compile(r'<[^<>]+>')
    text = html_pattern.sub(" ", text)

    # remove puncs and digits
    replace_chars = list(string.punctuation + string.digits)
    for char in replace_chars:
        text = text.replace(char, " ")

    # remove emoji
    emoji_pattern = re.compile("["
        u"\U0001F600-\U0001F64F"  # emoticons
        u"\U0001F300-\U0001F5FF"  # symbols & pictographs
        u"\U0001F680-\U0001F6FF"  # transport & map symbols
        u"\U0001F1E0-\U0001F1FF"  # flags (iOS)
        u"\U0001F1F2-\U0001F1F4"  # Macau flag
        u"\U0001F1E6-\U0001F1FF"  # flags
        u"\U0001F600-\U0001F64F"
        u"\U00002702-\U000027B0"
        u"\U000024C2-\U0001F251"
        u"\U0001f926-\U0001f937"
        u"\U0001F1F2"
        u"\U0001F1F4"
        u"\U0001F620"
        u"\u200d"
        u"\u2640-\u2642"
        "]+", flags=re.UNICODE)
    text = emoji_pattern.sub(r" ", text)

    # normalize whitespace
    text = " ".join(text.split())

    # lowercasing
    text = text.lower()
    return text

