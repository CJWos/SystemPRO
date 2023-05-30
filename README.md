# SystemPRO
시스템 프로그래밍 명령어

1.디렉터리 생성
2.디렉터리 이용
3.파일 크기가 0인 파일 생성
4.파일 권한 변경
5.파일(디렉터리)삭제


                    TEST
        (d)a01    (-)b01     (d)c
        (d)a02            (-)history
        (d)a03            (-)history_30313
       

                 
                 
       history>c/history //c디렉터리 안에 history 파일에 기록저장
       touch b01 //파일 값이 0인 파일 생성
       
       
       :w history_30313 //history원본 파일을 다른이름으로 저장가능
       :q! //나가기
       <권한 변경>
       
       import cv2
import torch
from datetime import datetime, timedelta

# Load YOLOv5 model
model = torch.hub.load('ultralytics/yolov5', 'yolov5n')

# Open the webcam
cap = cv2.VideoCapture(0)
cap.set(cv2.CAP_PROP_FRAME_WIDTH, 480)  # set the width
cap.set(cv2.CAP_PROP_FRAME_HEIGHT, 320)  # set the height

# Open the log file
log_file = open("detection_log.txt", "w")

# Open the result file
result_file = open("result.txt", "w")

# Define danger items
danger_items = {'person'}

# Set timer variables
start_time = datetime.now()
end_time = start_time + timedelta(seconds=3)
num_frames = 0
num_people = 0

while True:
    # Capture frame-by-frame
    ret, frame = cap.read()

    if not ret:
        break

    # Perform object detection
    frame_rgb = cv2.cvtColor(frame, cv2.COLOR_BGR2RGB)  # Convert to RGB
    results = model(frame_rgb)  # Inference

    # Count number of people in frame
    num_people_in_frame = sum(1 for *_, cls in results.xyxy[0] if results.names[int(cls)] == 'person')
    num_people += num_people_in_frame
    num_frames += 1

    # If 3 seconds have passed, calculate the average and reset the timer and counters
    current_time = datetime.now()
    if current_time >= end_time:
        avg_people = num_people / num_frames
        print(f"Average number of people in the last 3 seconds: {avg_people}")
        result_file.write(f"Time: {current_time}, Average number of people in the last 3 seconds: {avg_people}\n")
        start_time = current_time
        end_time = start_time + timedelta(seconds=3)
        num_frames = 0
        num_people = 0

    # Render the image with bounding boxes
    rendered_image = results.render()[0]  # Remove the first dimension
    rendered_image_bgr = cv2.cvtColor(rendered_image, cv2.COLOR_RGB2BGR)  # Convert back to BGR for displaying with cv2.imshow

    # Display the resulting frame
    cv2.imshow('Webcam', rendered_image_bgr)

    # Break the loop on 'q' key press
    if cv2.waitKey(1) & 0xFF == ord('q'):
        break

# After the loop, close the log file and release the capture and destroy all windows
log_file.close()
result_file.close()
cap.release()
cv2.destroyAllWindows()
       chmod -숫자 chmod (권한 2진수 숫자) (파일명)
            
       읽기 권한 있으면 1,없으면 0
       (RWX) 읽,쓰,실
       
       <파일 디렉터리로 삭제>.
       rm -r a01/a02
       
       
       
       
       
       
       
      
      MYSQL
      1번 모든 도서의 이름과 가격을 검색하시오.
      :select bookname,price from book;
      2번 모든 도서의 도서번호,도서이름,출판사,가격을 검색하시오.
      :select * from book;
      3번 가격이 20000원 미만인 도서를 검색하시오.
      :select * from book
      where price <20000;
      4번 출판사가 '굿스포츠'혹은 '대한미디어'인 도서를 검색하시오.
      : select * from book 
      where publisher ='굿스포츠' or publisher = '대한미디어';
      5번 2번 김연아 고객이 주문한 도서의 총 판매액을 구하시오.
      :select sum(saleprice) from orders where custid=2;
      6번 고객별로 주문한 도서의 총 수량과 총 판매액을 구하시오.
      :select custid,count(*),sum(saleprice)
      from orders
      group by custid;
      7번 고객과 고객의 주문에 관한 데이터를 모두 보이시오.
      :select * from customer,orders where customer.custid = orders.custid; 
      8번 고객의 이름과 고객이 주문한 도서의 가격을 검색하시오.
      :select * from name,saleprice where customer.custid = orders.custid; 
      9번 고객의 이름과 고객이 주문한 도서의 이름을 구하시오.
      :select name,bookname from customer,book,orders
      where customer.custid = orders.custid and orders.bookid = book.bookid;
      10번 가격이 10000원 이상인 도서를 주문한 고객의 이름과 도서의 이름을 구하시오.
      where customer.custid = orders.custid and orders.bookid = book.bookid and price >=10000;
      11번 주소가 '대한민국'인 고객의 주문 정보를 구하시오(검색결과 고객이름,주소,도서이름,가격을 보이게 하고 각 항목을 한글로 보이게 할것.)
      select name as 고객이름, address as 주소, bookname as 도서이름, price as 가격 
      from orders,book,customer
      
      
      where customer.custid=orders.custid and orders.bookid=book.bookid and address like "대한민국%";
